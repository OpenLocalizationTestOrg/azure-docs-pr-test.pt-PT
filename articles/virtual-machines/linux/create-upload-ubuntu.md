---
title: aaaCreate e carregar um VHD do Ubuntu Linux no Azure
description: "Saiba mais toocreate e carregar um Azure disco rígido virtual (VHD) que contenha um sistema de operativo Ubuntu Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="4d118-103">Preparar uma máquina virtual do Ubuntu para o Azure</span><span class="sxs-lookup"><span data-stu-id="4d118-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="4d118-104">Imagens de nuvem Ubuntu oficiais</span><span class="sxs-lookup"><span data-stu-id="4d118-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="4d118-105">Ubuntu agora publica oficial do Azure VHDs para transferência em [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="4d118-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="4d118-106">Se precisar toobuild sua própria imagem Ubuntu especializada para o Azure, em vez de utilizar o procedimento de manual Olá abaixo do mesmo toostart recomendada com estes conhecido trabalhar VHDs e personalizar conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="4d118-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="4d118-107">versões de imagem mais recentes Olá sempre podem ser encontradas em Olá seguintes localizações:</span><span class="sxs-lookup"><span data-stu-id="4d118-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="4d118-108">Ubuntu 12.04/preciso: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="4d118-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="4d118-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="4d118-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="4d118-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="4d118-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d118-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4d118-111">Prerequisites</span></span>
<span data-ttu-id="4d118-112">Este artigo pressupõe que já tem instalado um disco de rígido virtual do Ubuntu Linux sistema operativo tooa.</span><span class="sxs-lookup"><span data-stu-id="4d118-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="4d118-113">Várias ferramentas existem toocreate os ficheiros. vhd, por exemplo uma solução de virtualização, tais como o Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4d118-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="4d118-114">Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d118-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="4d118-115">**Notas de instalação do Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="4d118-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="4d118-116">Consulte também [geral notas de instalação do Linux](create-upload-generic.md#general-linux-installation-notes) para mais sugestões no preparar Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="4d118-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="4d118-117">formato VHDX Olá não é suportado no Azure, apenas **fixo VHD**.</span><span class="sxs-lookup"><span data-stu-id="4d118-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="4d118-118">Pode converter o formato de tooVHD Olá disco utilizando o Gestor de Hyper-V ou Olá convert-vhd cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4d118-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="4d118-119">Ao instalar o sistema de Linux Olá é recomendado que utilize partições padrão em vez de LVM (frequentemente predefinição Olá para instalações muitos).</span><span class="sxs-lookup"><span data-stu-id="4d118-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="4d118-120">Evitará LVM nome entra em conflito com VMs Clonadas, particularmente se um disco do SO alguma vez necessidades toobe ligado tooanother VM para resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="4d118-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="4d118-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados se preferencial.</span><span class="sxs-lookup"><span data-stu-id="4d118-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="4d118-122">Configure uma partição de comutação em disco do SO Olá.</span><span class="sxs-lookup"><span data-stu-id="4d118-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="4d118-123">agente do Linux Olá pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá.</span><span class="sxs-lookup"><span data-stu-id="4d118-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="4d118-124">Podem encontrar mais informações sobre esta nos passos Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d118-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="4d118-125">Todos os VHDs Olá tem de ter tamanhos que estão em múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="4d118-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="4d118-126">Passos manuais</span><span class="sxs-lookup"><span data-stu-id="4d118-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="4d118-127">Antes de tentar toocreate sua imagem personalizada do Ubuntu do Azure, considere utilizar Olá criadas previamente e testar imagens a partir do [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="4d118-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="4d118-128">No painel de centro de Olá do Gestor de Hyper-V, selecione a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="4d118-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="4d118-129">Clique em **Connect** janela de Olá tooopen para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="4d118-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="4d118-130">Substitua repositórios de atual Olá no repos do Azure do Ubuntu de Olá, imagem toouse.</span><span class="sxs-lookup"><span data-stu-id="4d118-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="4d118-131">passos de Olá variam ligeiramente dependendo das versões do Ubuntu Olá.</span><span class="sxs-lookup"><span data-stu-id="4d118-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="4d118-132">Antes de editar `/etc/apt/sources.list`, é recomendado toomake uma cópia de segurança:</span><span class="sxs-lookup"><span data-stu-id="4d118-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="4d118-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="4d118-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="4d118-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="4d118-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="4d118-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="4d118-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="4d118-136">Olá imagens Ubuntu Azure estão agora a seguir Olá *ativação hardware* kernel (HWE).</span><span class="sxs-lookup"><span data-stu-id="4d118-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="4d118-137">Atualize kernel mais recente do Olá sistema operativo toohello executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4d118-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="4d118-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="4d118-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="4d118-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="4d118-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="4d118-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="4d118-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="4d118-141">**Consulte também:**</span><span class="sxs-lookup"><span data-stu-id="4d118-141">**See also:**</span></span>
    - [<span data-ttu-id="4d118-142">https://Wiki.ubuntu.com/kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="4d118-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="4d118-143">https://Wiki.ubuntu.com/kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="4d118-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="4d118-144">Modifique a linha de arranque de kernel Olá para os parâmetros do Grub tooinclude kernel adicionais para o Azure.</span><span class="sxs-lookup"><span data-stu-id="4d118-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4d118-145">toodo neste abra `/etc/default/grub` num editor de texto, localizar variável Olá denominada `GRUB_CMDLINE_LINUX_DEFAULT` (ou adicioná-la, se necessário) e editá-lo Olá tooinclude os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="4d118-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="4d118-146">Guarde e feche este ficheiro e, em seguida, execute `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="4d118-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="4d118-147">Isto irá garantir que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar o suporte técnico do Azure com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="4d118-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="4d118-148">Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque.</span><span class="sxs-lookup"><span data-stu-id="4d118-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="4d118-149">Isto é normalmente predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="4d118-149">This is usually hello default.</span></span>

7. <span data-ttu-id="4d118-150">Instale Olá agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="4d118-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="4d118-151">Olá `walinuxagent` pacote poderá remover Olá `NetworkManager` e `NetworkManager-gnome` pacotes e, se estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="4d118-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="4d118-152">Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="4d118-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="4d118-153">Clique em **ação -> encerrar baixo** no Gestor de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4d118-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="4d118-154">O VHD de Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4d118-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d118-155">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4d118-155">Next steps</span></span>
<span data-ttu-id="4d118-156">Está agora pronto toouse sua Ubuntu Linux disco rígido virtual toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="4d118-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="4d118-157">Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d118-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="4d118-158">Referências</span><span class="sxs-lookup"><span data-stu-id="4d118-158">References</span></span>
<span data-ttu-id="4d118-159">Ubuntu kernel de ativação (HWE) de hardware:</span><span class="sxs-lookup"><span data-stu-id="4d118-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="4d118-160">http://blog.utlemming.org/2015/01/ubuntu-1404-Azure-Images-Now-Tracking.HTML</span><span class="sxs-lookup"><span data-stu-id="4d118-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="4d118-161">http://blog.utlemming.org/2015/02/1204-Azure-cloud-Images-Now-using-Hwe.HTML</span><span class="sxs-lookup"><span data-stu-id="4d118-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

