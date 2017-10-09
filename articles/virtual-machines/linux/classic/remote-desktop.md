---
title: tooa de ambiente de trabalho aaaRemote VM com Linux | Microsoft Docs
description: "Saiba como tooinstall e configurar o ambiente de trabalho remoto tooconnect tooa VM do Linux do Microsoft Azure para o modelo de implementação clássica Olá"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>Utilizando o ambiente de trabalho remoto tooconnect tooa VM do Linux do Microsoft Azure
> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Para obter Olá atualizar a versão do Gestor de recursos deste artigo, consulte [aqui](../use-remote-desktop.md).

## <a name="overview"></a>Descrição geral
RDP (protocolo de ambiente de trabalho remoto) é um protocolo proprietário utilizado para o Windows. Como podemos utilizar RDP tooconnect tooa VM com Linux (máquina virtual) remotamente?

Esta orientação irá dar-lhe Olá resposta! Irá ajudá-lo a xrdp tooinstall e configuração no Microsoft Azure Linux VM, que lhe permite ligar tooit com o ambiente de trabalho remoto a partir de um computador Windows. Utilizaremos VM com Linux com Ubuntu ou OpenSUSE como exemplo de Olá nesta orientação.

a ferramenta de xrdp Olá está um open de origem de servidor RDP que lhe permite tooconnect o servidor Linux com o ambiente de trabalho remoto de um computador Windows. RDP tem um melhor desempenho ao VNC (informática por rede Virtual). VNC composições utilizar gráficos de qualidade de JPEG e pode ser lenta, enquanto que o RDP é rápido e crystal encriptado.

> [!NOTE]
> Já tem de ter uma VM do Azure da Microsoft com o Linux. toocreate e configurar uma VM com Linux, consulte Olá [tutorial da VM do Linux do Azure](createportal.md).
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>Criar um ponto final para o ambiente de trabalho remoto
Utilizamos ponto final predefinido de Olá 3389 para ambiente de trabalho remoto neste documento. Configurar o ponto final 3389 como `Remote Desktop` tooyour VM com Linux, conforme mostrado abaixo:

![Imagem](./media/remote-desktop/endpoint-for-linux-server.png)

Se não souber como tooset configurar um ponto final para a VM, consulte [esta orientação](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Instalar o ambiente de trabalho Gnome
Ligar tooyour VM com Linux através do `putty`e instalar `Gnome Desktop`.

Ubuntu, utilize:

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


Para OpenSUSE, utilize:

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Instalar xrdp
Ubuntu, utilize:

    #sudo apt-get install xrdp

Para OpenSUSE, utilize:

> [!NOTE]
> Atualize a versão de OpenSUSE Olá com versão de Olá que estiver a utilizar na Olá os seguintes comandos. exemplo de Olá abaixo destina-se `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Iniciar xrdp e definir o serviço de xdrp em cima de arranque
Para OpenSUSE, utilize:

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

Para Ubuntu, xrdp será iniciado e eanbled no arranque cópia de segurança automaticamente após a instalação.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Utilizar xfce se estiver a utilizar uma versão de Ubuntu posterior Ubuntu 12.04LTS
Porque a versão atual do Olá do xrdp não suporta Gnome ambiente de trabalho para as versões do Ubuntu posterior Ubuntu 12.04LTS, utilizaremos `xfce` ambiente de trabalho em vez disso.

tooinstall `xfce`, utilize este comando:

    #sudo apt-get install xubuntu-desktop

Em seguida, ative `xfce` utilizando este comando:

    #echo xfce4-session >~/.xsession

Editar o ficheiro de configuração de Olá `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Adicione a linha de Olá `xfce4-session` antes de linha de Olá `/etc/X11/Xsession`.

toorestart Olá xrdp serviço, utilize esta opção:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Ligar a VM com Linux a partir de uma máquina Windows
Numa máquina Windows, iniciar o cliente do ambiente de trabalho remoto Olá e introduza o nome de DNS de VM do Linux. Ou aceda toohello Dashboard da sua VM na Olá portal do Azure e clique em `Connect` tooconnect na VM com Linux. Nesse caso, consulte a janela de início de sessão do Olá:

![Imagem](./media/remote-desktop/no2.png)

Inicie sessão com o nome de utilizador de Olá e a palavra-passe da sua VM do Linux.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre como utilizar xrdp, consulte [http://www.xrdp.org/](http://www.xrdp.org/).
