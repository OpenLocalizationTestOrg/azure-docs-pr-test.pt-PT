---
title: aaaCreate e carregar um VHD do Oracle Linux | Microsoft Docs
description: "Saiba mais toocreate e carregar um Azure disco rígido virtual (VHD) que contenha um sistema de operativo Oracle Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="215fa-103">Preparar uma máquina virtual do Oracle Linux para o Azure</span><span class="sxs-lookup"><span data-stu-id="215fa-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="215fa-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="215fa-104">Prerequisites</span></span>
<span data-ttu-id="215fa-105">Este artigo pressupõe que já tem instalado um disco de rígido virtual do Oracle Linux sistema operativo tooa.</span><span class="sxs-lookup"><span data-stu-id="215fa-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="215fa-106">Várias ferramentas existem toocreate os ficheiros. vhd, por exemplo uma solução de virtualização, tais como o Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="215fa-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="215fa-107">Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="215fa-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="215fa-108">Notas de instalação do Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="215fa-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="215fa-109">Consulte também [geral notas de instalação do Linux](create-upload-generic.md#general-linux-installation-notes) para mais sugestões no preparar Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="215fa-110">Kernel compatível do Red Hat do Oracle e os respetivos UEK3 (Unbreakable Enterprise Kernel) são ambas suportadas no Hyper-V e do Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="215fa-111">Para obter os melhores resultados, ser tooupdate se toohello mais recente kernel ao preparar o VHD do Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="215fa-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="215fa-112">UEK2 do Oracle não é suportado no Hyper-V e o Azure, não inclua controladores Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="215fa-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="215fa-113">formato VHDX Olá não é suportado no Azure, apenas **fixo VHD**.</span><span class="sxs-lookup"><span data-stu-id="215fa-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="215fa-114">Pode converter o formato de tooVHD Olá disco utilizando o Gestor de Hyper-V ou Olá convert-vhd cmdlet.</span><span class="sxs-lookup"><span data-stu-id="215fa-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="215fa-115">Ao instalar o sistema de Linux Olá é recomendado que utilize partições padrão em vez de LVM (frequentemente predefinição Olá para instalações muitos).</span><span class="sxs-lookup"><span data-stu-id="215fa-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="215fa-116">Evitará LVM nome entra em conflito com VMs Clonadas, particularmente se um disco do SO alguma vez necessidades toobe ligado tooanother VM para resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="215fa-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="215fa-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados se preferencial.</span><span class="sxs-lookup"><span data-stu-id="215fa-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="215fa-118">NUMA não é suportada para tamanhos de VM maiores devido a erros de tooa nas versões anteriores de kernel do Linux ao 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="215fa-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="215fa-119">Isto emitir principalmente os impactos distribuições utilizando Olá Red montante kernel Hat 2.6.32.</span><span class="sxs-lookup"><span data-stu-id="215fa-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="215fa-120">Instalação manual do agente Linux do Azure de Olá (waagent) desativará automaticamente na configuração de GRUB Olá para kernel do Olá Linux.</span><span class="sxs-lookup"><span data-stu-id="215fa-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="215fa-121">Podem encontrar mais informações sobre esta nos passos Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="215fa-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="215fa-122">Configure uma partição de comutação em disco do SO Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="215fa-123">agente do Linux Olá pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="215fa-124">Podem encontrar mais informações sobre esta nos passos Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="215fa-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="215fa-125">Todos os VHDs Olá tem de ter tamanhos que estão em múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="215fa-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="215fa-126">Certifique-se de que Olá `Addons` repositório está ativado.</span><span class="sxs-lookup"><span data-stu-id="215fa-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="215fa-127">Edite o ficheiro de Olá `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) e altere a linha de Olá `enabled=0` demasiado`enabled=1` em **[ol6_addons]** ou **[ol7_addons]** deste ficheiro.</span><span class="sxs-lookup"><span data-stu-id="215fa-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="215fa-128">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="215fa-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="215fa-129">Tem de concluir os passos de configuração específicos no sistema de operativo Olá para Olá toorun de máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="215fa-130">No painel de centro de Olá do Gestor de Hyper-V, selecione a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="215fa-131">Clique em **Connect** janela de Olá tooopen para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="215fa-132">Desinstale NetworkManager executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="215fa-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="215fa-133">**Nota:** se pacote Olá já não estiver instalado, este comando irá falhar com uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="215fa-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="215fa-134">Isto é esperado.</span><span class="sxs-lookup"><span data-stu-id="215fa-134">This is expected.</span></span>
4. <span data-ttu-id="215fa-135">Crie um ficheiro denominado **rede** no Olá `/etc/sysconfig/` diretório que contém Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="215fa-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="215fa-136">Crie um ficheiro denominado **ifcfg eth0** no Olá `/etc/sysconfig/network-scripts/` diretório que contém Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="215fa-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="215fa-137">Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="215fa-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="215fa-138">Estas regras podem causar problemas ao clonar uma máquina virtual no Microsoft Azure ou o Hyper-v:</span><span class="sxs-lookup"><span data-stu-id="215fa-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="215fa-139">Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="215fa-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="215fa-140">Instale o python pyasn1 executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="215fa-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="215fa-141">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="215fa-142">toodo neste abrir "/ boot/grub/menu.lst" num editor de texto e certifique-se de que kernel de predefinição Olá inclui Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="215fa-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="215fa-143">Isto também vai assegurar todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="215fa-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="215fa-144">Este procedimento desactivará NUMA devido a erros de tooa nas kernel compatível do Red Hat do Oracle.</span><span class="sxs-lookup"><span data-stu-id="215fa-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="215fa-145">Além disso toohello acima, recomenda-se demasiado*remover* Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="215fa-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="215fa-146">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="215fa-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="215fa-147">Olá `crashkernel` opção pode ser esquerda configurado se assim o desejar, mas tenha em atenção que este parâmetro irá reduzir Olá quantidade de memória disponível em Olá VM 128 MB ou mais, que pode ser problemático em tamanhos de VM mais pequenos Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="215fa-148">Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque.</span><span class="sxs-lookup"><span data-stu-id="215fa-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="215fa-149">Isto é normalmente predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-149">This is usually hello default.</span></span>
11. <span data-ttu-id="215fa-150">Instale Olá agente Linux do Azure executando Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="215fa-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="215fa-151">a versão mais recente Olá é 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="215fa-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="215fa-152">Tenha em atenção que instalar pacote de WALinuxAgent Olá removerá Olá NetworkManager e pacotes de NetworkManager gnome se estes não foram já removidas conforme descrito no passo 2.</span><span class="sxs-lookup"><span data-stu-id="215fa-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="215fa-153">Não crie o espaço de comutação em disco do SO Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="215fa-154">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando o disco do Olá recurso local que esteja anexado toohello VM após o aprovisionamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="215fa-155">Tenha em atenção é o disco de recurso local que Olá um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="215fa-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="215fa-156">Depois de instalar Olá agente Linux do Azure (consulte o passo anterior), modifique Olá adequadamente os seguintes parâmetros /etc/waagent.conf:</span><span class="sxs-lookup"><span data-stu-id="215fa-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="215fa-157">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="215fa-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="215fa-158">Clique em **ação -> encerrar baixo** no Gestor de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="215fa-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="215fa-159">O VHD de Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="215fa-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="215fa-160">Oracle Linux 7.0 +</span><span class="sxs-lookup"><span data-stu-id="215fa-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="215fa-161">**Alterações no Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="215fa-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="215fa-162">Preparar uma máquina virtual do Oracle Linux 7 para o Azure é muito semelhante tooOracle Linux 6, no entanto, existem várias diferenças importantes vale a pena realçar:</span><span class="sxs-lookup"><span data-stu-id="215fa-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="215fa-163">Kernel compatível do Red Hat Olá e UEK3 do Oracle são suportadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="215fa-164">kernel de UEK3 Olá é recomendada.</span><span class="sxs-lookup"><span data-stu-id="215fa-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="215fa-165">Olá NetworkManager do pacote já não está em conflito com o agente do Olá Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="215fa-166">Este pacote é instalado por predefinição e recomendamos que não é removida.</span><span class="sxs-lookup"><span data-stu-id="215fa-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="215fa-167">GRUB2 agora ser utilizada como Olá bootloader predefinido, para que o procedimento de Olá para editar os parâmetros de kernel foi alterada (ver abaixo).</span><span class="sxs-lookup"><span data-stu-id="215fa-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="215fa-168">XFS é agora o sistema de ficheiros Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="215fa-168">XFS is now hello default file system.</span></span> <span data-ttu-id="215fa-169">sistema de ficheiros de ext4 Olá ainda pode ser utilizado se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="215fa-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="215fa-170">**Passos de configuração**</span><span class="sxs-lookup"><span data-stu-id="215fa-170">**Configuration steps**</span></span>

1. <span data-ttu-id="215fa-171">No Gestor de Hyper-V, selecione a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="215fa-172">Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="215fa-173">Crie um ficheiro denominado **rede** no Olá `/etc/sysconfig/` diretório que contém Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="215fa-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="215fa-174">Crie um ficheiro denominado **ifcfg eth0** no Olá `/etc/sysconfig/network-scripts/` diretório que contém Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="215fa-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="215fa-175">Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="215fa-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="215fa-176">Estas regras podem causar problemas ao clonar uma máquina virtual no Microsoft Azure ou o Hyper-v:</span><span class="sxs-lookup"><span data-stu-id="215fa-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="215fa-177">Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="215fa-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="215fa-178">Instale o pacote do python pyasn1 de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="215fa-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="215fa-179">Executar Olá os seguintes comandos tooclear Olá atual yum metadados e instalar quaisquer atualizações:</span><span class="sxs-lookup"><span data-stu-id="215fa-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="215fa-180">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="215fa-181">toodo neste abrir "/ predefinido/etc/grub" no Olá de editor e edição de texto `GRUB_CMDLINE_LINUX` parâmetro, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="215fa-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="215fa-182">Isto também vai assegurar todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="215fa-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="215fa-183">É também desativa Olá novo OEL 7 convenções de nomenclatura para NICs.</span><span class="sxs-lookup"><span data-stu-id="215fa-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="215fa-184">Além disso toohello acima, recomenda-se demasiado*remover* Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="215fa-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="215fa-185">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="215fa-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="215fa-186">Olá `crashkernel` opção pode ser esquerda configurado se assim o desejar, mas tenha em atenção que este parâmetro irá reduzir Olá quantidade de memória disponível em Olá VM 128 MB ou mais, que pode ser problemático em tamanhos de VM mais pequenos Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="215fa-187">Quando tiver terminado edição "/ predefinido/etc/grub" por acima, execute Olá configuração do comando toorebuild Olá grub os seguintes:</span><span class="sxs-lookup"><span data-stu-id="215fa-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="215fa-188">Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque.</span><span class="sxs-lookup"><span data-stu-id="215fa-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="215fa-189">Isto é normalmente predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-189">This is usually hello default.</span></span>
12. <span data-ttu-id="215fa-190">Instale Olá agente Linux do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="215fa-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="215fa-191">Não crie o espaço de comutação em disco do SO Olá.</span><span class="sxs-lookup"><span data-stu-id="215fa-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="215fa-192">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando o disco do Olá recurso local que esteja anexado toohello VM após o aprovisionamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="215fa-193">Tenha em atenção é o disco de recurso local que Olá um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="215fa-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="215fa-194">Depois de instalar Olá agente Linux do Azure (consulte o passo anterior Olá), modifique Olá adequadamente os seguintes parâmetros /etc/waagent.conf:</span><span class="sxs-lookup"><span data-stu-id="215fa-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="215fa-195">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="215fa-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="215fa-196">Clique em **ação -> encerrar baixo** no Gestor de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="215fa-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="215fa-197">O VHD de Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="215fa-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="215fa-198">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="215fa-198">Next steps</span></span>
<span data-ttu-id="215fa-199">Está agora pronto toouse as Oracle Linux VHD toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="215fa-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="215fa-200">Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="215fa-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

