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
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Preparar uma máquina virtual do Ubuntu para o Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>Imagens de nuvem Ubuntu oficiais
Ubuntu agora publica oficial do Azure VHDs para transferência em [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/). Se precisar toobuild sua própria imagem Ubuntu especializada para o Azure, em vez de utilizar o procedimento de manual Olá abaixo do mesmo toostart recomendada com estes conhecido trabalhar VHDs e personalizar conforme necessário. versões de imagem mais recentes Olá sempre podem ser encontradas em Olá seguintes localizações:

* Ubuntu 12.04/preciso: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que já tem instalado um disco de rígido virtual do Ubuntu Linux sistema operativo tooa. Várias ferramentas existem toocreate os ficheiros. vhd, por exemplo uma solução de virtualização, tais como o Hyper-V. Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma Máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

**Notas de instalação do Ubuntu**

* Consulte também [geral notas de instalação do Linux](create-upload-generic.md#general-linux-installation-notes) para mais sugestões no preparar Linux para o Azure.
* formato VHDX Olá não é suportado no Azure, apenas **fixo VHD**.  Pode converter o formato de tooVHD Olá disco utilizando o Gestor de Hyper-V ou Olá convert-vhd cmdlet.
* Ao instalar o sistema de Linux Olá é recomendado que utilize partições padrão em vez de LVM (frequentemente predefinição Olá para instalações muitos). Evitará LVM nome entra em conflito com VMs Clonadas, particularmente se um disco do SO alguma vez necessidades toobe ligado tooanother VM para resolução de problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pode ser utilizado em discos de dados se preferencial.
* Configure uma partição de comutação em disco do SO Olá. agente do Linux Olá pode ser configurado toocreate um ficheiro de comutação no disco de recursos temporário Olá.  Podem encontrar mais informações sobre esta nos passos Olá abaixo.
* Todos os VHDs Olá tem de ter tamanhos que estão em múltiplos de 1 MB.

## <a name="manual-steps"></a>Passos manuais
> [!NOTE]
> Antes de tentar toocreate sua imagem personalizada do Ubuntu do Azure, considere utilizar Olá criadas previamente e testar imagens a partir do [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) em vez disso.
> 
> 

1. No painel de centro de Olá do Gestor de Hyper-V, selecione a máquina virtual de Olá.

2. Clique em **Connect** janela de Olá tooopen para a máquina virtual de Olá.

3. Substitua repositórios de atual Olá no repos do Azure do Ubuntu de Olá, imagem toouse. passos de Olá variam ligeiramente dependendo das versões do Ubuntu Olá.
   
    Antes de editar `/etc/apt/sources.list`, é recomendado toomake uma cópia de segurança:
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. Olá imagens Ubuntu Azure estão agora a seguir Olá *ativação hardware* kernel (HWE). Atualize kernel mais recente do Olá sistema operativo toohello executando Olá os seguintes comandos:

    Ubuntu 12.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **Consulte também:**
    - [https://Wiki.ubuntu.com/kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://Wiki.ubuntu.com/kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Modifique a linha de arranque de kernel Olá para os parâmetros do Grub tooinclude kernel adicionais para o Azure. toodo neste abra `/etc/default/grub` num editor de texto, localizar variável Olá denominada `GRUB_CMDLINE_LINUX_DEFAULT` (ou adicioná-la, se necessário) e editá-lo Olá tooinclude os seguintes parâmetros:
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    Guarde e feche este ficheiro e, em seguida, execute `sudo update-grub`. Isto irá garantir que todas as mensagens de consola são enviadas toohello primeiro porta série, que pode ajudar o suporte técnico do Azure com problemas de depuração.

6. Certifique-se de que o servidor SSH Olá está instalado e configurado toostart no momento do arranque.  Isto é normalmente predefinido Olá.

7. Instale Olá agente Linux do Azure:
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    Olá `walinuxagent` pacote poderá remover Olá `NetworkManager` e `NetworkManager-gnome` pacotes e, se estiverem instalados.

8. Olá executar comandos seguintes toodeprovision Olá máquina e prepará-la para o aprovisionamento no Azure:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. Clique em **ação -> encerrar baixo** no Gestor de Hyper-V. O VHD de Linux está agora pronto toobe carregado tooAzure.

## <a name="next-steps"></a>Passos seguintes
Está agora pronto toouse sua Ubuntu Linux disco rígido virtual toocreate novas máquinas virtuais no Azure. Se este for Olá pela primeira vez que está a carregar tooAzure de ficheiro. VHD de Olá, consulte os passos 2 e 3 na [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="references"></a>Referências
Ubuntu kernel de ativação (HWE) de hardware:

* [http://blog.utlemming.org/2015/01/ubuntu-1404-Azure-Images-Now-Tracking.HTML](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-Azure-cloud-Images-Now-using-Hwe.HTML](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

