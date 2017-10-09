---
title: aaaPrepare um Debian Linux VHD no Azure | Microsoft Docs
description: "Saiba como toocreate Debian 7 & 8 VHD ficheiros para a implementação no Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="98620-103">Preparar um VHD Debian para o Azure</span><span class="sxs-lookup"><span data-stu-id="98620-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="98620-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="98620-104">Prerequisites</span></span>
<span data-ttu-id="98620-105">Esta secção assume que já tem instalado um sistema operativo Debian Linux de um ficheiro. ISO transferido a partir de Olá [site Debian](https://www.debian.org/distrib/) tooa disco de rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="98620-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="98620-106">Várias ferramentas existem toocreate ficheiros. vhd Hyper-V é apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="98620-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="98620-107">Para obter instruções sobre como utilizar o Hyper-V, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="98620-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="98620-108">Notas de instalação</span><span class="sxs-lookup"><span data-stu-id="98620-108">Installation notes</span></span>
* <span data-ttu-id="98620-109">Consulte também [geral notas de instalação do Linux](create-upload-generic.md#general-linux-installation-notes) para mais sugestões no preparar Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="98620-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="98620-110">formato VHDX mais recente Olá não é suportado no Azure.</span><span class="sxs-lookup"><span data-stu-id="98620-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="98620-111">Pode converter o formato de tooVHD Olá disco utilizando o Gestor de Hyper-V ou Olá **convert-vhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="98620-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="98620-112">Ao instalar o sistema de Linux Olá é recomendado que utilize partições padrão em vez de LVM (frequentemente predefinição Olá para instalações muitos).</span><span class="sxs-lookup"><span data-stu-id="98620-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="98620-113">Evitará LVM nome entra em conflito com VMs Clonadas, particularmente se um disco do SO alguma vez necessidades toobe ligado tooanother VM para resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98620-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="98620-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados se preferencial.</span><span class="sxs-lookup"><span data-stu-id="98620-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="98620-115">Configure uma partição de comutação em disco do SO Olá.</span><span class="sxs-lookup"><span data-stu-id="98620-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="98620-116">agente Linux do Azure de Olá pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá.</span><span class="sxs-lookup"><span data-stu-id="98620-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="98620-117">Podem encontrar mais informações sobre esta nos passos Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="98620-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="98620-118">Todos os VHDs Olá tem de ter tamanhos que estão em múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="98620-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="98620-119">Utilize a gerir o Azure toocreate Debian os VHDs</span><span class="sxs-lookup"><span data-stu-id="98620-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="98620-120">Existem ferramentas disponíveis para a geração de VHDs Debian do Azure, tais como Olá [azure-gerir](https://github.com/credativ/azure-manage) scripts de [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="98620-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="98620-121">Este é Olá recomendado abordagem versus criar uma imagem a partir do zero.</span><span class="sxs-lookup"><span data-stu-id="98620-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="98620-122">Por exemplo, toocreate um VHD de 8 Debian executar Olá os seguintes comandos do azure-gerir toodownload (e as dependências) e execute o script de azure_build_image Olá:</span><span class="sxs-lookup"><span data-stu-id="98620-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="98620-123">Preparar manualmente uma VHD Debian</span><span class="sxs-lookup"><span data-stu-id="98620-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="98620-124">No Gestor de Hyper-V, selecione a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="98620-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="98620-125">Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="98620-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="98620-126">Comente a linha de Olá **CD-ROM de deb** no `/etc/apt/source.list` se configurou Olá VM em relação a um ficheiro ISO.</span><span class="sxs-lookup"><span data-stu-id="98620-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="98620-127">Editar Olá `/etc/default/grub` de ficheiros e modificar Olá **GRUB_CMDLINE_LINUX** parâmetro da seguinte forma tooinclude parâmetros de kernel adicionais para o Azure.</span><span class="sxs-lookup"><span data-stu-id="98620-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="98620-128">Reconstruir grub Olá e execute:</span><span class="sxs-lookup"><span data-stu-id="98620-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="98620-129">Adicione repositórios do Azure too/etc/apt/sources.list do Debian Debian 7 ou 8:</span><span class="sxs-lookup"><span data-stu-id="98620-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="98620-130">**Debian 7. x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="98620-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="98620-131">**Debian 8. x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="98620-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="98620-132">Instale Olá agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="98620-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="98620-133">Para Debian 7, é kernel toorun necessários com base em 3.16 Olá do repositório de wheezy backports Olá.</span><span class="sxs-lookup"><span data-stu-id="98620-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="98620-134">Em primeiro lugar, crie um ficheiro chamado /etc/apt/preferences.d/linux.pref com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="98620-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="98620-135">Em seguida, execute o kernel novo Olá tooinstall "apt sudo-get instalar amd64 de imagem de linux".</span><span class="sxs-lookup"><span data-stu-id="98620-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="98620-136">Desaprovisionar a máquina virtual de Olá e prepará-la para o aprovisionamento no Azure e execute:</span><span class="sxs-lookup"><span data-stu-id="98620-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="98620-137">Clique em **ação** -> Encerrar para baixo no Gestor de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="98620-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="98620-138">O VHD de Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="98620-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98620-139">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="98620-139">Next steps</span></span>
<span data-ttu-id="98620-140">Está agora pronto toouse as disco de rígido virtual Debian toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="98620-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="98620-141">Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98620-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

