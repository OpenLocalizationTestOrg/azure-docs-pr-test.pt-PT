---
title: aaaCreate e carregar um VHD de Linux CentOS baseado no Azure
description: "Saiba mais toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema operativo baseado em CentOS Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="867dc-103">Preparar uma máquina virtual baseada em CentOS para o Azure</span><span class="sxs-lookup"><span data-stu-id="867dc-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="867dc-104">Preparar uma máquina de virtual do CentOS 6. x para o Azure</span><span class="sxs-lookup"><span data-stu-id="867dc-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="867dc-105">Preparar uma máquina virtual do CentOS 7.0 + Azure</span><span class="sxs-lookup"><span data-stu-id="867dc-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="867dc-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="867dc-106">Prerequisites</span></span>
<span data-ttu-id="867dc-107">Este artigo pressupõe que já tem instalado um CentOS (ou semelhante derivativo) Linux sistema operativo tooa disco virtual.</span><span class="sxs-lookup"><span data-stu-id="867dc-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="867dc-108">Várias ferramentas existem toocreate os ficheiros. vhd, por exemplo uma solução de virtualização, tais como o Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="867dc-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="867dc-109">Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="867dc-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="867dc-110">**Notas de instalação do centOS**</span><span class="sxs-lookup"><span data-stu-id="867dc-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="867dc-111">Consulte também [geral notas de instalação do Linux](create-upload-generic.md#general-linux-installation-notes) para mais sugestões no preparar Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="867dc-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="867dc-112">formato VHDX Olá não é suportado no Azure, apenas **fixo VHD**.</span><span class="sxs-lookup"><span data-stu-id="867dc-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="867dc-113">Pode converter o formato de tooVHD Olá disco utilizando o Gestor de Hyper-V ou Olá convert-vhd cmdlet.</span><span class="sxs-lookup"><span data-stu-id="867dc-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="867dc-114">Se estiver a utilizar VirtualBox significa que a seleção **um tamanho fixo** como opposed predefinido toohello dinamicamente atribuído ao criar o disco de Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="867dc-115">Ao instalar o sistema de Linux Olá é *recomendado* que utilize partições padrão em vez de LVM (frequentemente predefinição Olá para instalações muitos).</span><span class="sxs-lookup"><span data-stu-id="867dc-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="867dc-116">Evitará LVM nome entra em conflito com VMs Clonadas, particularmente se um disco de SO alguma vez precisar de toobe ligado tooanother VM idêntico para resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="867dc-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="867dc-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="867dc-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="867dc-118">É necessário suporte de kernel para montar a sistemas de ficheiros UDF.</span><span class="sxs-lookup"><span data-stu-id="867dc-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="867dc-119">No primeiro arranque no Azure Olá configuração aprovisionamento é transmitida toohello VM com Linux através do UDF formatado suporte de dados é anexado toohello convidado.</span><span class="sxs-lookup"><span data-stu-id="867dc-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="867dc-120">agente Linux do Azure de Olá tem de ser capaz de toomount Olá UDF ficheiro sistema tooread respetiva configuração e aprovisionar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="867dc-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="867dc-121">Versões de kernel do Linux abaixo 2.6.37 não suportam no Hyper-V com tamanhos de VM maiores.</span><span class="sxs-lookup"><span data-stu-id="867dc-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="867dc-122">Isto emitir principalmente impactos distribuições anteriores utilizando Olá upstream kernel do Red Hat 2.6.32 e foi corrigido em RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="867dc-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="867dc-123">Sistemas com kernels personalizados anteriores 2.6.37 ou baseado em RHEL kernels mais antigos que tem de definir 2.6.32-504 Olá parâmetro arranque `numa=off` no kernel Olá da linha de comandos no grub.conf.</span><span class="sxs-lookup"><span data-stu-id="867dc-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="867dc-124">Para obter mais informações consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="867dc-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="867dc-125">Configure uma partição de comutação em disco do SO Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="867dc-126">agente do Linux Olá pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="867dc-127">Podem encontrar mais informações sobre esta nos passos Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="867dc-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="867dc-128">Todos os VHDs Olá tem de ter tamanhos que estão em múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="867dc-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="867dc-129">CentOS 6. x</span><span class="sxs-lookup"><span data-stu-id="867dc-129">CentOS 6.x</span></span>

1. <span data-ttu-id="867dc-130">No Gestor de Hyper-V, selecione a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="867dc-131">Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="867dc-132">No 6 do CentOS, NetworkManager pode interferir com agente Linux do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="867dc-133">Desinstale este pacote executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="867dc-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="867dc-134">Criar ou editar o ficheiro de Olá `/etc/sysconfig/network` e adicione Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="867dc-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="867dc-135">Criar ou editar o ficheiro de Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="867dc-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="867dc-136">Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="867dc-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="867dc-137">Estas regras podem causar problemas ao clonar uma máquina virtual no Microsoft Azure ou o Hyper-v:</span><span class="sxs-lookup"><span data-stu-id="867dc-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="867dc-138">Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="867dc-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="867dc-139">Se quiser espelhos de OpenLogic de Olá toouse que estão alojados no Olá centros de dados do Azure, em seguida, substitua Olá `/etc/yum.repos.d/CentOS-Base.repo` ficheiro com Olá repositórios a seguir.</span><span class="sxs-lookup"><span data-stu-id="867dc-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="867dc-140">Também irá adicionar Olá **[openlogic]** repositório inclui pacotes adicionais, tais como o agente Linux do Azure de Olá:</span><span class="sxs-lookup"><span data-stu-id="867dc-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="867dc-141">Olá guia restante será partem do princípio de que está a utilizar, pelo menos, Olá `[openlogic]` repositório, que será utilizado tooinstall Olá Azure agente do Linux abaixo.</span><span class="sxs-lookup"><span data-stu-id="867dc-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="867dc-142">Adicione Olá linha too/etc/yum.conf os seguintes:</span><span class="sxs-lookup"><span data-stu-id="867dc-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="867dc-143">Execute Olá comando tooclear Olá yum metadados e atualização Olá sistema atual com pacotes mais recentes Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="867dc-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="867dc-144">A menos que estiver a criar uma imagem para uma versão antiga do CentOS, recomenda-se tooupdate que Olá, todos os pacotes toohello mais recentes:</span><span class="sxs-lookup"><span data-stu-id="867dc-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="867dc-145">Reiniciar o computador poderá ser necessário depois de executar este comando.</span><span class="sxs-lookup"><span data-stu-id="867dc-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="867dc-146">(Opcional) Instale os controladores de Olá para Olá serviços de integração Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="867dc-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="867dc-147">passo Olá é **necessário** para CentOS 6.3 e anteriores e opcionais para versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="867dc-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="867dc-148">Em alternativa, pode seguir as instruções de instalação manual de Olá no Olá [página de transferência de LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall Olá RPM para a VM.</span><span class="sxs-lookup"><span data-stu-id="867dc-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="867dc-149">Instale Olá agente Linux do Azure e as dependências:</span><span class="sxs-lookup"><span data-stu-id="867dc-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="867dc-150">pacote de WALinuxAgent Olá irá remover Olá NetworkManager e pacotes de NetworkManager gnome se estes não foram já removidas conforme descrito no passo 3.</span><span class="sxs-lookup"><span data-stu-id="867dc-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="867dc-151">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="867dc-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="867dc-152">toodo, abra `/boot/grub/menu.lst` num editor de texto e certifique-se de que kernel de predefinição Olá inclui Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="867dc-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="867dc-153">Isto também vai assegurar todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="867dc-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="867dc-154">Além disso toohello acima, recomenda-se demasiado*remover* Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="867dc-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="867dc-155">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="867dc-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="867dc-156">Olá `crashkernel` opção pode ser esquerda configurado se assim o desejar, mas tenha em atenção que este parâmetro irá reduzir Olá quantidade de memória disponível em Olá VM 128 MB ou mais, que pode ser problemático em tamanhos de VM mais pequenos Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="867dc-157">CentOS 6.5 e anteriores também devem definir o parâmetro de kernel Olá `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="867dc-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="867dc-158">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="867dc-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="867dc-159">Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque.</span><span class="sxs-lookup"><span data-stu-id="867dc-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="867dc-160">Isto é normalmente predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-160">This is usually hello default.</span></span>

15. <span data-ttu-id="867dc-161">Não crie o espaço de comutação em disco do SO Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="867dc-162">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando o disco do Olá recurso local que esteja anexado toohello VM após o aprovisionamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="867dc-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="867dc-163">Tenha em atenção é o disco de recurso local que Olá um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="867dc-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="867dc-164">Depois de instalar Olá agente Linux do Azure (consulte o passo anterior), modifique Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:</span><span class="sxs-lookup"><span data-stu-id="867dc-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="867dc-165">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="867dc-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="867dc-166">Clique em **ação -> encerrar baixo** no Gestor de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="867dc-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="867dc-167">O VHD de Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="867dc-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="867dc-168">CentOS 7.0 +</span><span class="sxs-lookup"><span data-stu-id="867dc-168">CentOS 7.0+</span></span>
<span data-ttu-id="867dc-169">**Alterações no CentOS 7 (e derivados semelhantes)**</span><span class="sxs-lookup"><span data-stu-id="867dc-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="867dc-170">Preparar uma máquina virtual do CentOS 7 para o Azure é muito semelhante tooCentOS 6, no entanto, existem várias diferenças importantes vale a pena realçar:</span><span class="sxs-lookup"><span data-stu-id="867dc-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="867dc-171">Olá NetworkManager do pacote já não está em conflito com o agente do Olá Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="867dc-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="867dc-172">Este pacote é instalado por predefinição e recomendamos que não é removida.</span><span class="sxs-lookup"><span data-stu-id="867dc-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="867dc-173">GRUB2 agora ser utilizada como Olá bootloader predefinido, para que o procedimento de Olá para editar os parâmetros de kernel foi alterada (ver abaixo).</span><span class="sxs-lookup"><span data-stu-id="867dc-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="867dc-174">XFS é agora o sistema de ficheiros Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="867dc-174">XFS is now hello default file system.</span></span> <span data-ttu-id="867dc-175">sistema de ficheiros de ext4 Olá ainda pode ser utilizado se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="867dc-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="867dc-176">**Passos de configuração**</span><span class="sxs-lookup"><span data-stu-id="867dc-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="867dc-177">No Gestor de Hyper-V, selecione a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="867dc-178">Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="867dc-179">Criar ou editar o ficheiro de Olá `/etc/sysconfig/network` e adicione Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="867dc-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="867dc-180">Criar ou editar o ficheiro de Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="867dc-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="867dc-181">Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="867dc-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="867dc-182">Estas regras podem causar problemas ao clonar uma máquina virtual no Microsoft Azure ou o Hyper-v:</span><span class="sxs-lookup"><span data-stu-id="867dc-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="867dc-183">Se quiser espelhos de OpenLogic de Olá toouse que estão alojados no Olá centros de dados do Azure, em seguida, substitua Olá `/etc/yum.repos.d/CentOS-Base.repo` ficheiro com Olá repositórios a seguir.</span><span class="sxs-lookup"><span data-stu-id="867dc-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="867dc-184">Também irá adicionar Olá **[openlogic]** repositório inclui pacotes de agente Linux do Azure de Olá:</span><span class="sxs-lookup"><span data-stu-id="867dc-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="867dc-185">Olá guia restante será partem do princípio de que está a utilizar, pelo menos, Olá `[openlogic]` repositório, que será utilizado tooinstall Olá Azure agente do Linux abaixo.</span><span class="sxs-lookup"><span data-stu-id="867dc-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="867dc-186">Executar Olá os seguintes comandos tooclear Olá atual yum metadados e instalar quaisquer atualizações:</span><span class="sxs-lookup"><span data-stu-id="867dc-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="867dc-187">A menos que estiver a criar uma imagem para uma versão antiga do CentOS, recomenda-se tooupdate que Olá, todos os pacotes toohello mais recentes:</span><span class="sxs-lookup"><span data-stu-id="867dc-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="867dc-188">Reiniciar o computador pode ser necessário depois de executar este comando.</span><span class="sxs-lookup"><span data-stu-id="867dc-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="867dc-189">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="867dc-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="867dc-190">toodo, abra `/etc/default/grub` no Olá de editor e edição de texto `GRUB_CMDLINE_LINUX` parâmetro, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="867dc-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="867dc-191">Isto também vai assegurar todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="867dc-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="867dc-192">É também desativa Olá novo CentOS 7 convenções de nomenclatura para NICs.</span><span class="sxs-lookup"><span data-stu-id="867dc-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="867dc-193">Além disso toohello acima, recomenda-se demasiado*remover* Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="867dc-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="867dc-194">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="867dc-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="867dc-195">Olá `crashkernel` opção pode ser esquerda configurado se assim o desejar, mas tenha em atenção que este parâmetro irá reduzir Olá quantidade de memória disponível em Olá VM 128 MB ou mais, que pode ser problemático em tamanhos de VM mais pequenos Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="867dc-196">Quando tiver terminado edição `/etc/default/grub` por acima, execute Olá configuração do comando toorebuild Olá grub os seguintes:</span><span class="sxs-lookup"><span data-stu-id="867dc-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="867dc-197">Se criar a imagem de Olá de **VMWare, VirtualBox ou KVM:** Certifique-se de controladores de Olá Hyper-V estão incluídos no Olá initramfs:</span><span class="sxs-lookup"><span data-stu-id="867dc-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="867dc-198">Editar `/etc/dracut.conf`, adicionar conteúdo:</span><span class="sxs-lookup"><span data-stu-id="867dc-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="867dc-199">Reconstrua Olá initramfs:</span><span class="sxs-lookup"><span data-stu-id="867dc-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="867dc-200">Instale Olá agente Linux do Azure e as dependências:</span><span class="sxs-lookup"><span data-stu-id="867dc-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="867dc-201">Não crie o espaço de comutação em disco do SO Olá.</span><span class="sxs-lookup"><span data-stu-id="867dc-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="867dc-202">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando o disco do Olá recurso local que esteja anexado toohello VM após o aprovisionamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="867dc-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="867dc-203">Tenha em atenção é o disco de recurso local que Olá um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="867dc-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="867dc-204">Depois de instalar Olá agente Linux do Azure (consulte o passo anterior), modifique Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:</span><span class="sxs-lookup"><span data-stu-id="867dc-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="867dc-205">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="867dc-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="867dc-206">Clique em **ação -> encerrar baixo** no Gestor de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="867dc-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="867dc-207">O VHD de Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="867dc-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="867dc-208">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="867dc-208">Next steps</span></span>
<span data-ttu-id="867dc-209">Está agora pronto toouse sua CentOS Linux disco rígido virtual toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="867dc-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="867dc-210">Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="867dc-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

