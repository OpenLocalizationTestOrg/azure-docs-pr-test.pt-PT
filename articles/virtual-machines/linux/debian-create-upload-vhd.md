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
# <a name="prepare-a-debian-vhd-for-azure"></a>Preparar um VHD Debian para o Azure
## <a name="prerequisites"></a>Pré-requisitos
Esta secção assume que já tem instalado um sistema operativo Debian Linux de um ficheiro. ISO transferido a partir de Olá [site Debian](https://www.debian.org/distrib/) tooa disco de rígido virtual. Várias ferramentas existem toocreate ficheiros. vhd Hyper-V é apenas um exemplo. Para obter instruções sobre como utilizar o Hyper-V, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](https://technet.microsoft.com/library/hh846766.aspx).

## <a name="installation-notes"></a>Notas de instalação
* Consulte também [geral notas de instalação do Linux](create-upload-generic.md#general-linux-installation-notes) para mais sugestões no preparar Linux para o Azure.
* formato VHDX mais recente Olá não é suportado no Azure. Pode converter o formato de tooVHD Olá disco utilizando o Gestor de Hyper-V ou Olá **convert-vhd** cmdlet.
* Ao instalar o sistema de Linux Olá é recomendado que utilize partições padrão em vez de LVM (frequentemente predefinição Olá para instalações muitos). Evitará LVM nome entra em conflito com VMs Clonadas, particularmente se um disco do SO alguma vez necessidades toobe ligado tooanother VM para resolução de problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados se preferencial.
* Configure uma partição de comutação em disco do SO Olá. agente Linux do Azure de Olá pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá. Podem encontrar mais informações sobre esta nos passos Olá abaixo.
* Todos os VHDs Olá tem de ter tamanhos que estão em múltiplos de 1 MB.

## <a name="use-azure-manage-toocreate-debian-vhds"></a>Utilize a gerir o Azure toocreate Debian os VHDs
Existem ferramentas disponíveis para a geração de VHDs Debian do Azure, tais como Olá [azure-gerir](https://github.com/credativ/azure-manage) scripts de [credativ](http://www.credativ.com/). Este é Olá recomendado abordagem versus criar uma imagem a partir do zero. Por exemplo, toocreate um VHD de 8 Debian executar Olá os seguintes comandos do azure-gerir toodownload (e as dependências) e execute o script de azure_build_image Olá:

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>Preparar manualmente uma VHD Debian
1. No Gestor de Hyper-V, selecione a máquina virtual de Olá.
2. Clique em **Connect** tooopen uma janela da consola da máquina virtual de Olá.
3. Comente a linha de Olá **CD-ROM de deb** no `/etc/apt/source.list` se configurou Olá VM em relação a um ficheiro ISO.
4. Editar Olá `/etc/default/grub` de ficheiros e modificar Olá **GRUB_CMDLINE_LINUX** parâmetro da seguinte forma tooinclude parâmetros de kernel adicionais para o Azure.
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. Reconstruir grub Olá e execute:
   
        # sudo update-grub
6. Adicione repositórios do Azure too/etc/apt/sources.list do Debian Debian 7 ou 8:
   
    **Debian 7. x "Wheezy"**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8. x "Jessie"**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. Instale Olá agente Linux do Azure:
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Para Debian 7, é kernel toorun necessários com base em 3.16 Olá do repositório de wheezy backports Olá. Em primeiro lugar, crie um ficheiro chamado /etc/apt/preferences.d/linux.pref com Olá seguinte conteúdo:
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    Em seguida, execute o kernel novo Olá tooinstall "apt sudo-get instalar amd64 de imagem de linux".
3. Desaprovisionar a máquina virtual de Olá e prepará-la para o aprovisionamento no Azure e execute:
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. Clique em **ação** -> Encerrar para baixo no Gestor de Hyper-V. O VHD de Linux está agora pronto toobe carregado tooAzure.

## <a name="next-steps"></a>Passos seguintes
Está agora pronto toouse as disco de rígido virtual Debian toocreate novas máquinas virtuais no Azure. Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

