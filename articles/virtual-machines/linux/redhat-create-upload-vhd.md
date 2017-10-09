---
title: "aaaCreate e carregar um VHD do Red Hat Enterprise Linux para utilização no Azure | Microsoft Docs"
description: "Saiba mais toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema operativo Red Hat Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="fe6b2-103">Preparar uma máquina virtual baseada em Red Hat para o Azure</span><span class="sxs-lookup"><span data-stu-id="fe6b2-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="fe6b2-104">Neste artigo, ficará a saber como tooprepare uma máquina virtual do Red Hat Enterprise Linux (RHEL) para utilização no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="fe6b2-105">versões de Olá do RHEL que são abordadas neste artigo são 6.7 + e 7.1 +.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="fe6b2-106">Olá hipervisores de preparação, que são abordadas neste artigo são Hyper-V, com base em kernel a máquina virtual (KVM) e VMware.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="fe6b2-107">Para obter mais informações sobre os requisitos de elegibilidade para participar no programa de acesso à nuvem do Red Hat, consulte [Web site de acesso à nuvem do Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) e [RHEL em execução no Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="fe6b2-108">Preparar uma máquina de virtual baseado no Red Hat a partir do Gestor de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="fe6b2-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fe6b2-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fe6b2-109">Prerequisites</span></span>
<span data-ttu-id="fe6b2-110">Esta secção assume que já tenham obteve um ficheiro ISO do Web site do Red Hat Olá e Olá instalado RHEL imagem tooa disco rígido virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="fe6b2-111">Para obter mais detalhes sobre como toouse Gestor de Hyper-V tooinstall uma imagem do sistema operativo, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="fe6b2-112">**Notas de instalação do RHEL**</span><span class="sxs-lookup"><span data-stu-id="fe6b2-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="fe6b2-113">Azure não suporta o formato VHDX Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="fe6b2-114">Azure suporta apenas fixo VHD.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="fe6b2-115">Pode utilizar o formato de tooVHD do Gestor de Hyper-V tooconvert Olá disco ou, pode utilizar o cmdlet do Olá convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="fe6b2-116">Se utilizar VirtualBox, selecione **um tamanho fixo** por oposição ao predefinido de toohello dinamicamente atribuído opção ao criar o disco de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="fe6b2-117">Azure suporta apenas máquinas de virtuais de geração 1.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="fe6b2-118">Pode converter uma máquina virtual de geração 1 formato de ficheiro VHD de toohello VHDX e de disco de tamanho fixo tooa de expansão dinâmica.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="fe6b2-119">Não é possível alterar a geração de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="fe6b2-120">Para obter mais informações, consulte [deve criar máquinas virtuais de geração 1 ou 2 no Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="fe6b2-121">Olá tamanho máximo permitido para Olá VHD é 1,023 GB.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="fe6b2-122">Quando instalar o sistema de operativo Linux Olá, recomendamos que utilize partições padrão em vez de Gestor de Volume lógica (LVM), que é frequentemente predefinição de Olá para várias instalações.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="fe6b2-123">Esta prática evitará LVM nome entra em conflito com as máquinas virtuais Clonadas, particularmente se alguma vez precisar de tooattach uma máquina de virtual idênticas do sistema operativo disco tooanother para resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="fe6b2-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="fe6b2-125">É necessário suporte de kernel para montar a sistemas de ficheiros de formato de disco Universal (UDF).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="fe6b2-126">No primeiro arranque no, Olá formatado UDF Media Services do Azure que é anexado toohello convidado transmite Olá aprovisionamento configuração toohello máquina virtual com Linux.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="fe6b2-127">Olá agente Linux do Azure tem de ser capaz de toomount Olá UDF ficheiro sistema tooread respetiva configuração e aprovisionar a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="fe6b2-128">Versões de kernel de Linux Olá anteriores ao 2.6.37 não suportam acesso não uniforme memória (NUMA) no Hyper-V com maior tamanhos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="fe6b2-129">Isto emitir principalmente impactos distribuições mais antigas que utilizam Olá upstream kernel do Red Hat 2.6.32 e foi corrigido em RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="fe6b2-130">Sistemas que executam kernels personalizados que são mais antigos do que 2.6.37 ou baseado em RHEL kernels que são mais antigas do que 2.6.32-504 tem de definir Olá `numa=off` arranque parâmetro na linha de comandos de kernel Olá no grub.conf.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="fe6b2-131">Para obter mais informações, consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="fe6b2-132">Configure uma partição de comutação em disco do sistema operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="fe6b2-133">Olá agente Linux pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="fe6b2-134">Podem encontrar mais informações sobre esta no Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="fe6b2-135">Todos os VHDs têm de ter tamanhos que estão em múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="fe6b2-136">Preparar uma máquina virtual do RHEL 6 a partir do Gestor de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="fe6b2-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="fe6b2-137">No Gestor de Hyper-V, selecione a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="fe6b2-138">Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="fe6b2-139">No RHEL 6, NetworkManager pode interferir com agente Linux do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="fe6b2-140">Desinstale este pacote executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="fe6b2-141">Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="fe6b2-142">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="fe6b2-143">Mova (ou remova) Olá udev regras tooavoid gerar regras estáticas para a interface da Ethernet Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="fe6b2-144">Estas regras provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou o Hyper-v:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="fe6b2-145">Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="fe6b2-146">Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="fe6b2-147">pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="fe6b2-148">Ative o repositório de extras Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="fe6b2-149">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="fe6b2-150">toodo esta modificação, abra `/boot/grub/menu.lst` num editor de texto e certifique-se de que kernel de predefinição Olá inclui Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="fe6b2-151">Isto também vai assegurar que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="fe6b2-152">Além disso, recomendamos que remova Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="fe6b2-153">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="fe6b2-154">Pode deixar Olá `crashkernel` opção configurada se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="fe6b2-155">Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="fe6b2-156">Esta configuração pode ser problemática em tamanhos de máquinas virtuais mais pequenos.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="fe6b2-157">RHEL 6.5 e anterior também tem de definir Olá `numa=off` parâmetro de kernel.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="fe6b2-158">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="fe6b2-159">Certifique-se de que servidor de secure shell (SSH) Olá está instalado e configurado toostart no momento do arranque, que é normalmente predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="fe6b2-160">Modificar /etc/ssh/sshd_config tooinclude Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="fe6b2-161">Instale Olá agente Linux do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="fe6b2-162">Instalar pacote de WALinuxAgent Olá remove Olá NetworkManager e pacotes de NetworkManager gnome se estes não foram removidos no passo 3.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="fe6b2-163">Não crie o espaço de comutação em disco do sistema operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="fe6b2-164">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="fe6b2-165">Tenha em atenção que Olá local disco de recursos é um disco temporário e que-lo poderá de ser esvaziada quando a máquina virtual de Olá é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="fe6b2-166">Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modifique Olá adequadamente os seguintes parâmetros /etc/waagent.conf:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="fe6b2-167">Anular o registo da subscrição Olá (se necessário) através da execução Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="fe6b2-168">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="fe6b2-169">Clique em **ação** > **Encerrar** no Gestor de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="fe6b2-170">O VHD de Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="fe6b2-171">Preparar uma máquina virtual do RHEL 7 a partir do Gestor de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="fe6b2-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="fe6b2-172">No Gestor de Hyper-V, selecione a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="fe6b2-173">Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="fe6b2-174">Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="fe6b2-175">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="fe6b2-176">Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="fe6b2-177">Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="fe6b2-178">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="fe6b2-179">toodo esta modificação, abra `/etc/default/grub` num editor de texto e edite Olá `GRUB_CMDLINE_LINUX` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="fe6b2-180">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="fe6b2-181">Isto também vai assegurar que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="fe6b2-182">Esta configuração também desativa-se Olá novo RHEL 7 convenções de nomenclatura para NICs.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="fe6b2-183">Além disso, recomendamos que remova Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="fe6b2-184">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="fe6b2-185">Pode deixar Olá `crashkernel` opção configurada se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="fe6b2-186">Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="fe6b2-187">Depois de terminar edição `/etc/default/grub`, execute hello os seguintes comandos toorebuild Olá grub configuração:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="fe6b2-188">Certifique-se de que servidor SSH Olá está instalado e configurado toostart no momento do arranque, que é normalmente predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="fe6b2-189">Modificar `/etc/ssh/sshd_config` Olá tooinclude seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="fe6b2-190">pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="fe6b2-191">Ative o repositório de extras Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="fe6b2-192">Instale Olá agente Linux do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="fe6b2-193">Não crie o espaço de comutação em disco do sistema operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="fe6b2-194">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="fe6b2-195">Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="fe6b2-196">Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="fe6b2-197">Se pretender que a subscrição de Olá toounregister, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="fe6b2-198">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="fe6b2-199">Clique em **ação** > **Encerrar** no Gestor de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="fe6b2-200">O VHD de Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="fe6b2-201">Preparar uma máquina de virtual baseado no Red Hat do KVM</span><span class="sxs-lookup"><span data-stu-id="fe6b2-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="fe6b2-202">Preparar uma máquina virtual do RHEL 6 do KVM</span><span class="sxs-lookup"><span data-stu-id="fe6b2-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="fe6b2-203">Transferir imagem KVM Olá do RHEL 6 do Web site do Red Hat Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="fe6b2-204">Defina uma palavra-passe de raiz.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-204">Set a root password.</span></span>

    <span data-ttu-id="fe6b2-205">Gerar uma palavra-passe encriptada e copiar Olá resultado do comando de Olá:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="fe6b2-206">Defina uma palavra-passe de raiz com guestfish:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="fe6b2-207">Campo de segundo Olá alteração do utilizador raiz Olá "!"</span><span class="sxs-lookup"><span data-stu-id="fe6b2-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="fe6b2-208">toohello encriptados palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="fe6b2-209">Crie uma máquina virtual no KVM da imagem de qcow2 de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="fe6b2-210">Definir o tipo de disco Olá demasiado**qcow2**e definir o modelo de dispositivo de interface de rede virtual Olá demasiado**virtio**.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="fe6b2-211">Em seguida, iniciar a máquina virtual de Olá e inicie sessão como raiz.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="fe6b2-212">Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="fe6b2-213">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="fe6b2-214">Mova (ou remova) Olá udev regras tooavoid gerar regras estáticas para a interface da Ethernet Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="fe6b2-215">Estas regras provocar problemas ao clonar uma máquina virtual no Azure ou do Hyper-v:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="fe6b2-216">Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="fe6b2-217">Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="fe6b2-218">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="fe6b2-219">toodo nesta configuração, abra `/boot/grub/menu.lst` num editor de texto e certifique-se de que kernel de predefinição Olá inclui Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="fe6b2-220">Isto também vai assegurar que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="fe6b2-221">Além disso, recomendamos que remova Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="fe6b2-222">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="fe6b2-223">Pode deixar Olá `crashkernel` opção configurada se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="fe6b2-224">Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="fe6b2-225">RHEL 6.5 e anterior também tem de definir Olá `numa=off` parâmetro de kernel.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="fe6b2-226">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="fe6b2-227">Adicione tooinitramfs de módulos do Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="fe6b2-228">Editar `/etc/dracut.conf`e adicione Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="fe6b2-229">Reconstrua initramfs:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="fe6b2-230">Desinstale init de cloud:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="fe6b2-231">Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="fe6b2-232">Modificar /etc/ssh/sshd_config tooinclude Olá seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="fe6b2-233">pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="fe6b2-234">Ative o repositório de extras Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="fe6b2-235">Instale Olá agente Linux do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="fe6b2-236">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="fe6b2-237">Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="fe6b2-238">Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no **/etc/waagent.conf** corretamente:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="fe6b2-239">Anular o registo da subscrição Olá (se necessário) através da execução Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="fe6b2-240">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="fe6b2-241">Encerre a máquina virtual Olá KVM.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="fe6b2-242">Converta o formato VHD do Olá qcow2 imagem toohello.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="fe6b2-243">Comece por converter o formato de tooraw Olá imagem:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="fe6b2-244">Certifique-se de que o tamanho da imagem não processados Olá Olá está alinhado com 1 MB.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="fe6b2-245">Caso contrário, arredonda por excesso Olá tamanho tooalign com 1 MB:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="fe6b2-246">Converter tooa de disco em bruto de Olá fixo tamanho VHD:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="fe6b2-247">Preparar uma máquina virtual do RHEL 7 do KVM</span><span class="sxs-lookup"><span data-stu-id="fe6b2-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="fe6b2-248">Transferir imagem KVM Olá RHEL 7 do Web site do Red Hat Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="fe6b2-249">Este procedimento utiliza RHEL 7 como exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="fe6b2-250">Defina uma palavra-passe de raiz.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-250">Set a root password.</span></span>

    <span data-ttu-id="fe6b2-251">Gerar uma palavra-passe encriptada e copiar Olá resultado do comando de Olá:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="fe6b2-252">Defina uma palavra-passe de raiz com guestfish:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="fe6b2-253">Campo de segundo Olá alteração de utilizador de raiz de "!"</span><span class="sxs-lookup"><span data-stu-id="fe6b2-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="fe6b2-254">toohello encriptados palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="fe6b2-255">Crie uma máquina virtual no KVM da imagem de qcow2 de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="fe6b2-256">Definir o tipo de disco Olá demasiado**qcow2**e definir o modelo de dispositivo de interface de rede virtual Olá demasiado**virtio**.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="fe6b2-257">Em seguida, iniciar a máquina virtual de Olá e inicie sessão como raiz.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="fe6b2-258">Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="fe6b2-259">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="fe6b2-260">Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="fe6b2-261">Registe a instalação do Red Hat subscrição tooenable de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="fe6b2-262">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="fe6b2-263">toodo nesta configuração, abra `/etc/default/grub` num editor de texto e edite Olá `GRUB_CMDLINE_LINUX` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="fe6b2-264">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="fe6b2-265">Este comando também garante que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="fe6b2-266">comando Olá também desativa-se Olá novo RHEL 7 convenções de nomenclatura para NICs.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="fe6b2-267">Além disso, recomendamos que remova Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="fe6b2-268">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="fe6b2-269">Pode deixar Olá `crashkernel` opção configurada se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="fe6b2-270">Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="fe6b2-271">Depois de terminar edição `/etc/default/grub`, execute hello os seguintes comandos toorebuild Olá grub configuração:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="fe6b2-272">Adicione módulos do Hyper-V em initramfs.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="fe6b2-273">Editar `/etc/dracut.conf` e adicionar conteúdo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="fe6b2-274">Reconstrua initramfs:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="fe6b2-275">Desinstale init de cloud:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="fe6b2-276">Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="fe6b2-277">Modificar /etc/ssh/sshd_config tooinclude Olá seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="fe6b2-278">pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="fe6b2-279">Ative o repositório de extras Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="fe6b2-280">Instale Olá agente Linux do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="fe6b2-281">Ative o serviço de waagent Olá:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="fe6b2-282">Não crie o espaço de comutação em disco do sistema operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="fe6b2-283">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="fe6b2-284">Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="fe6b2-285">Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="fe6b2-286">Anular o registo da subscrição Olá (se necessário) através da execução Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="fe6b2-287">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="fe6b2-288">Encerre a máquina virtual Olá KVM.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="fe6b2-289">Converta o formato VHD do Olá qcow2 imagem toohello.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="fe6b2-290">Comece por converter o formato de tooraw Olá imagem:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="fe6b2-291">Certifique-se de que o tamanho da imagem não processados Olá Olá está alinhado com 1 MB.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="fe6b2-292">Caso contrário, arredonda por excesso Olá tamanho tooalign com 1 MB:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="fe6b2-293">Converter tooa de disco em bruto de Olá fixo tamanho VHD:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="fe6b2-294">Preparar uma máquina de virtual baseado no Red Hat do VMware</span><span class="sxs-lookup"><span data-stu-id="fe6b2-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="fe6b2-295">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fe6b2-295">Prerequisites</span></span>
<span data-ttu-id="fe6b2-296">Esta secção assume que já instalou uma máquina virtual do RHEL no VMware.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="fe6b2-297">Para obter detalhes sobre como tooinstall um sistema operativo no VMware, consulte o artigo [guia de instalação de sistema operativo de convidado de VMware](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="fe6b2-298">Quando instalar o sistema de operativo Linux Olá, recomendamos que utilize partições padrão em vez de LVM, que é frequentemente predefinição de Olá para várias instalações.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="fe6b2-299">Evitará LVM nome entra em conflito com a máquina virtual clonada, particularmente se um disco de sistema operativo tem alguma vez toobe ligado tooanother máquinas para resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="fe6b2-300">LVM RAID pode ser utilizado ou em discos de dados se preferencial.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="fe6b2-301">Configure uma partição de comutação em disco do sistema operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="fe6b2-302">Pode configurar Olá Linux agente toocreate um ficheiro de comutação no disco de recursos temporário Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="fe6b2-303">Pode encontrar mais informações sobre esta nos passos de Olá que se seguem.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="fe6b2-304">Quando criar o disco de rígido virtual Olá, selecione **disco virtual de armazenamento como um único ficheiro**.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="fe6b2-305">Preparar uma máquina virtual do RHEL 6 do VMware</span><span class="sxs-lookup"><span data-stu-id="fe6b2-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="fe6b2-306">No RHEL 6, NetworkManager pode interferir com agente Linux do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="fe6b2-307">Desinstale este pacote executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="fe6b2-308">Crie um ficheiro denominado **rede** Olá /etc/hosts/sysconfig/diretório que contém Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="fe6b2-309">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="fe6b2-310">Mova (ou remova) Olá udev regras tooavoid gerar regras estáticas para a interface da Ethernet Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="fe6b2-311">Estas regras provocar problemas ao clonar uma máquina virtual no Azure ou do Hyper-v:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="fe6b2-312">Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="fe6b2-313">Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="fe6b2-314">pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="fe6b2-315">Ative o repositório de extras Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="fe6b2-316">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="fe6b2-317">toodo, abra `/etc/default/grub` num editor de texto e edite Olá `GRUB_CMDLINE_LINUX` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="fe6b2-318">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="fe6b2-319">Isto também vai assegurar que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="fe6b2-320">Além disso, recomendamos que remova Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="fe6b2-321">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="fe6b2-322">Pode deixar Olá `crashkernel` opção configurada se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="fe6b2-323">Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="fe6b2-324">Adicione tooinitramfs de módulos do Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="fe6b2-325">Editar `/etc/dracut.conf`e adicione Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="fe6b2-326">Reconstrua initramfs:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="fe6b2-327">Certifique-se de que servidor SSH Olá está instalado e configurado toostart no momento do arranque, que é normalmente predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="fe6b2-328">Modificar `/etc/ssh/sshd_config` Olá tooinclude seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="fe6b2-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="fe6b2-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="fe6b2-330">Instale Olá agente Linux do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="fe6b2-331">Não crie o espaço de comutação em disco do sistema operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="fe6b2-332">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="fe6b2-333">Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="fe6b2-334">Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="fe6b2-335">Anular o registo da subscrição Olá (se necessário) através da execução Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="fe6b2-336">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="fe6b2-337">Encerre a máquina virtual de Olá e converta o ficheiro de. vhd do Olá VMDK ficheiro tooa.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="fe6b2-338">Comece por converter o formato de tooraw Olá imagem:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="fe6b2-339">Certifique-se de que o tamanho da imagem não processados Olá Olá está alinhado com 1 MB.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="fe6b2-340">Caso contrário, arredonda por excesso Olá tamanho tooalign com 1 MB:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="fe6b2-341">Converter tooa de disco em bruto de Olá fixo tamanho VHD:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="fe6b2-342">Preparar uma máquina virtual do RHEL 7 do VMware</span><span class="sxs-lookup"><span data-stu-id="fe6b2-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="fe6b2-343">Criar ou editar Olá `/etc/sysconfig/network` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="fe6b2-344">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de ficheiros e adicionar Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="fe6b2-345">Certifique-se de que o serviço de rede Olá será iniciada no momento do arranque executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="fe6b2-346">Registe a instalação do Red Hat subscrição tooenable Olá de pacotes do repositório RHEL Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="fe6b2-347">Modifique a linha de arranque de kernel Olá no seu grub tooinclude kernel adicionais os parâmetros da configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="fe6b2-348">toodo esta modificação, abra `/etc/default/grub` num editor de texto e edite Olá `GRUB_CMDLINE_LINUX` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="fe6b2-349">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="fe6b2-350">Esta configuração também garante que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar a Azure suporte com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="fe6b2-351">É também desativa Olá novo RHEL 7 convenções de nomenclatura para NICs.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="fe6b2-352">Além disso, recomendamos que remova Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="fe6b2-353">Arranque gráfica e silenciosos não são úteis num ambiente de nuvem em que pretende é que todos os Olá registos toobe enviados toohello de porta série.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="fe6b2-354">Pode deixar Olá `crashkernel` opção configurada se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="fe6b2-355">Tenha em atenção que este parâmetro reduz a quantidade de Olá de memória disponível na máquina virtual de Olá 128 MB ou mais, que pode ser problemático em tamanhos de máquinas virtuais mais pequenos.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="fe6b2-356">Depois de terminar edição `/etc/default/grub`, execute hello os seguintes comandos toorebuild Olá grub configuração:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="fe6b2-357">Adicione tooinitramfs de módulos do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="fe6b2-358">Editar `/etc/dracut.conf`, adicionar conteúdo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="fe6b2-359">Reconstrua initramfs:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="fe6b2-360">Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="fe6b2-361">Esta é normalmente Olá predefinição.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-361">This setting is usually hello default.</span></span> <span data-ttu-id="fe6b2-362">Modificar `/etc/ssh/sshd_config` Olá tooinclude seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="fe6b2-363">pacote de WALinuxAgent Olá, `WALinuxAgent-<version>`, tiver sido feito o Push repositório de extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="fe6b2-364">Ative o repositório de extras Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="fe6b2-365">Instale Olá agente Linux do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="fe6b2-366">Não crie o espaço de comutação em disco do sistema operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="fe6b2-367">Olá agente Linux do Azure pode configurar automaticamente o espaço de comutação utilizando Olá disco de recurso local que está a máquina virtual de toohello anexado depois de máquina virtual de Olá é aprovisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="fe6b2-368">Tenha em atenção que hello disco de recurso local é um disco temporário e poderá ser esvaziada quando a máquina virtual de Olá é desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="fe6b2-369">Depois de instalar Olá agente Linux do Azure no passo anterior Olá, modificar Olá seguir os parâmetros no `/etc/waagent.conf` corretamente:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="fe6b2-370">Se pretender que a subscrição de Olá toounregister, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="fe6b2-371">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="fe6b2-372">Encerre a máquina virtual de Olá e converter Olá ficheiro toohello VHD no formato VMDK.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="fe6b2-373">Comece por converter o formato de tooraw Olá imagem:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="fe6b2-374">Certifique-se de que o tamanho da imagem não processados Olá Olá está alinhado com 1 MB.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="fe6b2-375">Caso contrário, arredonda por excesso Olá tamanho tooalign com 1 MB:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="fe6b2-376">Converter tooa de disco em bruto de Olá fixo tamanho VHD:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="fe6b2-377">Preparar uma máquina de virtual baseado no Red Hat a partir de um ficheiro ISO utilizando um ficheiro de kickstart automaticamente</span><span class="sxs-lookup"><span data-stu-id="fe6b2-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="fe6b2-378">Preparar uma máquina virtual de RHEL 7 de um ficheiro de kickstart</span><span class="sxs-lookup"><span data-stu-id="fe6b2-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="fe6b2-379">Criar um ficheiro de kickstart que inclui Olá seguir o conteúdo e guarde o ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="fe6b2-380">Para obter mais informações sobre a instalação de kickstart, consulte Olá [guia de instalação Kickstart](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. <span data-ttu-id="fe6b2-381">Coloque o ficheiro de kickstart olá onde o sistema de instalação de Olá consegue aceder-lhe.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="fe6b2-382">No Gestor de Hyper-V, crie uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="fe6b2-383">No Olá **ligar disco rígido Virtual** página, selecione **anexar um disco rígido virtual mais tarde**e concluída Olá Assistente Nova Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="fe6b2-384">Abra as definições da máquina virtual de Olá:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="fe6b2-385">a.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-385">a.</span></span>  <span data-ttu-id="fe6b2-386">Anexe uma nova máquina de virtual toohello de disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="fe6b2-387">Certifique-se de que tooselect **formato VHD** e **de tamanho fixo**.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="fe6b2-388">b.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-388">b.</span></span>  <span data-ttu-id="fe6b2-389">Anexe unidade de DVD toohello ISO de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="fe6b2-390">c.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-390">c.</span></span>  <span data-ttu-id="fe6b2-391">Definir Olá BIOS tooboot a partir do CD.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="fe6b2-392">Inicie máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-392">Start hello virtual machine.</span></span> <span data-ttu-id="fe6b2-393">Quando for apresentado o guia de instalação de Olá, prima **separador** opções de arranque de Olá tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="fe6b2-394">Introduza `inst.ks=<hello location of hello kickstart file>` no fim de Olá de opções de arranque Olá e prima **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="fe6b2-395">Aguarde Olá toofinish de instalação.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="fe6b2-396">Quando estiver concluída, máquina virtual de Olá será automaticamente encerrada.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="fe6b2-397">O VHD de Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="fe6b2-398">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="fe6b2-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="fe6b2-399">controlador de Hyper-V Olá não foi incluído na inicial do disco de RAM Olá quando utilizar um hipervisor não Hyper-V</span><span class="sxs-lookup"><span data-stu-id="fe6b2-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="fe6b2-400">Em alguns casos, programas de instalação do Linux podem não incluir controladores de Olá do Hyper-V no Olá inicial RAM do disco (initrd ou initramfs), a menos que Linux Deteta que está em execução num ambiente Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="fe6b2-401">Quando estiver a utilizar um tooprepare de sistema (ou seja, Virtualbox Xen, etc.) de Virtualização diferentes a imagem do Linux, poderá ser necessário toorebuild initrd tooensure que, pelo menos, Olá hv_vmbus e módulos de kernel hv_storvsc estão disponíveis no disco de RAM inicial Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="fe6b2-402">Este é um problema conhecido, pelo menos, em sistemas baseados no montante de distribuição Red Hat Olá.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="fe6b2-403">tooresolve este problema, adicione tooinitramfs de módulos do Hyper-V e reconstrui-lo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="fe6b2-404">Editar `/etc/dracut.conf`e adicione Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="fe6b2-405">Reconstrua initramfs:</span><span class="sxs-lookup"><span data-stu-id="fe6b2-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="fe6b2-406">Para obter mais detalhes, consulte as informações de Olá [reconstruir initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe6b2-407">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fe6b2-407">Next steps</span></span>
<span data-ttu-id="fe6b2-408">Está agora pronto toouse das Red Hat Enterprise Linux disco rígido virtual toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b2-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="fe6b2-409">Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="fe6b2-410">Para obter mais detalhes sobre Olá hipervisores que são certificadas toorun Red Hat Enterprise Linux, consulte [Web site do Red Hat Olá](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="fe6b2-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
