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
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="6e531-103">Utilizando o ambiente de trabalho remoto tooconnect tooa VM do Linux do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6e531-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="6e531-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6e531-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6e531-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="6e531-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6e531-106">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e531-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6e531-107">Para obter Olá atualizar a versão do Gestor de recursos deste artigo, consulte [aqui](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="6e531-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="6e531-108">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="6e531-108">Overview</span></span>
<span data-ttu-id="6e531-109">RDP (protocolo de ambiente de trabalho remoto) é um protocolo proprietário utilizado para o Windows.</span><span class="sxs-lookup"><span data-stu-id="6e531-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="6e531-110">Como podemos utilizar RDP tooconnect tooa VM com Linux (máquina virtual) remotamente?</span><span class="sxs-lookup"><span data-stu-id="6e531-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="6e531-111">Esta orientação irá dar-lhe Olá resposta!</span><span class="sxs-lookup"><span data-stu-id="6e531-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="6e531-112">Irá ajudá-lo a xrdp tooinstall e configuração no Microsoft Azure Linux VM, que lhe permite ligar tooit com o ambiente de trabalho remoto a partir de um computador Windows.</span><span class="sxs-lookup"><span data-stu-id="6e531-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="6e531-113">Utilizaremos VM com Linux com Ubuntu ou OpenSUSE como exemplo de Olá nesta orientação.</span><span class="sxs-lookup"><span data-stu-id="6e531-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="6e531-114">a ferramenta de xrdp Olá está um open de origem de servidor RDP que lhe permite tooconnect o servidor Linux com o ambiente de trabalho remoto de um computador Windows.</span><span class="sxs-lookup"><span data-stu-id="6e531-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="6e531-115">RDP tem um melhor desempenho ao VNC (informática por rede Virtual).</span><span class="sxs-lookup"><span data-stu-id="6e531-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="6e531-116">VNC composições utilizar gráficos de qualidade de JPEG e pode ser lenta, enquanto que o RDP é rápido e crystal encriptado.</span><span class="sxs-lookup"><span data-stu-id="6e531-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="6e531-117">Já tem de ter uma VM do Azure da Microsoft com o Linux.</span><span class="sxs-lookup"><span data-stu-id="6e531-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="6e531-118">toocreate e configurar uma VM com Linux, consulte Olá [tutorial da VM do Linux do Azure](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="6e531-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="6e531-119">Criar um ponto final para o ambiente de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="6e531-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="6e531-120">Utilizamos ponto final predefinido de Olá 3389 para ambiente de trabalho remoto neste documento. Configurar o ponto final 3389 como `Remote Desktop` tooyour VM com Linux, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="6e531-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![Imagem](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="6e531-122">Se não souber como tooset configurar um ponto final para a VM, consulte [esta orientação](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="6e531-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="6e531-123">Instalar o ambiente de trabalho Gnome</span><span class="sxs-lookup"><span data-stu-id="6e531-123">Install Gnome Desktop</span></span>
<span data-ttu-id="6e531-124">Ligar tooyour VM com Linux através do `putty`e instalar `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="6e531-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="6e531-125">Ubuntu, utilize:</span><span class="sxs-lookup"><span data-stu-id="6e531-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="6e531-126">Para OpenSUSE, utilize:</span><span class="sxs-lookup"><span data-stu-id="6e531-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="6e531-127">Instalar xrdp</span><span class="sxs-lookup"><span data-stu-id="6e531-127">Install xrdp</span></span>
<span data-ttu-id="6e531-128">Ubuntu, utilize:</span><span class="sxs-lookup"><span data-stu-id="6e531-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="6e531-129">Para OpenSUSE, utilize:</span><span class="sxs-lookup"><span data-stu-id="6e531-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="6e531-130">Atualize a versão de OpenSUSE Olá com versão de Olá que estiver a utilizar na Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="6e531-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="6e531-131">exemplo de Olá abaixo destina-se `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="6e531-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="6e531-132">Iniciar xrdp e definir o serviço de xdrp em cima de arranque</span><span class="sxs-lookup"><span data-stu-id="6e531-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="6e531-133">Para OpenSUSE, utilize:</span><span class="sxs-lookup"><span data-stu-id="6e531-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="6e531-134">Para Ubuntu, xrdp será iniciado e eanbled no arranque cópia de segurança automaticamente após a instalação.</span><span class="sxs-lookup"><span data-stu-id="6e531-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="6e531-135">Utilizar xfce se estiver a utilizar uma versão de Ubuntu posterior Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="6e531-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="6e531-136">Porque a versão atual do Olá do xrdp não suporta Gnome ambiente de trabalho para as versões do Ubuntu posterior Ubuntu 12.04LTS, utilizaremos `xfce` ambiente de trabalho em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6e531-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="6e531-137">tooinstall `xfce`, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="6e531-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="6e531-138">Em seguida, ative `xfce` utilizando este comando:</span><span class="sxs-lookup"><span data-stu-id="6e531-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="6e531-139">Editar o ficheiro de configuração de Olá `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="6e531-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="6e531-140">Adicione a linha de Olá `xfce4-session` antes de linha de Olá `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="6e531-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="6e531-141">toorestart Olá xrdp serviço, utilize esta opção:</span><span class="sxs-lookup"><span data-stu-id="6e531-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="6e531-142">Ligar a VM com Linux a partir de uma máquina Windows</span><span class="sxs-lookup"><span data-stu-id="6e531-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="6e531-143">Numa máquina Windows, iniciar o cliente do ambiente de trabalho remoto Olá e introduza o nome de DNS de VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="6e531-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="6e531-144">Ou aceda toohello Dashboard da sua VM na Olá portal do Azure e clique em `Connect` tooconnect na VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="6e531-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="6e531-145">Nesse caso, consulte a janela de início de sessão do Olá:</span><span class="sxs-lookup"><span data-stu-id="6e531-145">In that case, you see hello login window:</span></span>

![Imagem](./media/remote-desktop/no2.png)

<span data-ttu-id="6e531-147">Inicie sessão com o nome de utilizador de Olá e a palavra-passe da sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="6e531-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e531-148">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6e531-148">Next steps</span></span>
<span data-ttu-id="6e531-149">Para obter mais informações sobre como utilizar xrdp, consulte [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="6e531-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
