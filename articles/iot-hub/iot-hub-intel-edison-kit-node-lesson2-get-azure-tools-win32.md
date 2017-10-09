---
title: "Ligar Intel Edison (nó) tooAzure IoT - Lesson 2: ferramentas do Azure (Windows) | Microsoft Docs"
description: "Instale o Python e Olá interface de linha de comandos do Azure (CLI do Azure) no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do Azure, o serviço de nuvem do iot, arduino nuvem"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 60631b54-6d2e-4e8a-88bf-7c2f8e7e1f29
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0a2e941119f9106add708591d52f32eb9ed08451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="ff1e5-104">Obter ferramentas do Azure (Windows 7 e posterior)</span><span class="sxs-lookup"><span data-stu-id="ff1e5-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="ff1e5-105">[Windows 7 e posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="ff1e5-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="ff1e5-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="ff1e5-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="ff1e5-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="ff1e5-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ff1e5-108">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="ff1e5-108">What you will do</span></span>
<span data-ttu-id="ff1e5-109">Instalar o Python e Olá interface de linha de comandos do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="ff1e5-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="ff1e5-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="ff1e5-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ff1e5-111">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="ff1e5-111">What you will learn</span></span>
<span data-ttu-id="ff1e5-112">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="ff1e5-112">In this article, you will learn:</span></span>
* <span data-ttu-id="ff1e5-113">Como tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-113">How tooinstall Python.</span></span>
* <span data-ttu-id="ff1e5-114">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ff1e5-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="ff1e5-115">What you need</span></span>
* <span data-ttu-id="ff1e5-116">Um computador Windows com uma ligação à Internet.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="ff1e5-117">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-117">An active Azure subscription.</span></span> <span data-ttu-id="ff1e5-118">Se não tiver uma conta do Azure, crie um [conta de avaliação do Azure gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="ff1e5-119">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="ff1e5-119">Install Python</span></span>
<span data-ttu-id="ff1e5-120">[Instalar o Python](https://www.python.org/downloads/) no seu computador Windows.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="ff1e5-121">Pode instalar o Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="ff1e5-122">Este tutorial baseia-se no Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="ff1e5-123">Se já tiver instalado o Python, aceda a secção seguinte toohello e instalar Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="ff1e5-124">Também precisa de caminho de Olá tooadd das pastas de olá onde python.exe e pip.exe são instalados toohello sistema `PATH` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="ff1e5-125">Por predefinição, python.exe é instalado em `C:\Python27` e pip.exe está instalado no `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="ff1e5-126">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ff1e5-126">Install hello Azure CLI</span></span>
<span data-ttu-id="ff1e5-127">Olá CLI do Azure fornece uma experiência de linha de comandos multiplataformas para o Azure.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="ff1e5-128">Trabalhar diretamente a partir do seu tooprovision de linha de comandos e gerir os recursos.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="ff1e5-129">Olá tooinstall CLI do Azure, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="ff1e5-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="ff1e5-130">Abra uma janela de linha de comandos como administrador.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="ff1e5-131">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ff1e5-131">Run hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="ff1e5-132">Verificar a instalação de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ff1e5-132">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="ff1e5-133">Consulte a seguinte Olá de saída se a instalação de Olá é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-133">You see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="ff1e5-135">Resumo</span><span class="sxs-lookup"><span data-stu-id="ff1e5-135">Summary</span></span>
<span data-ttu-id="ff1e5-136">Instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="ff1e5-137">A seguinte tarefa toocreate sua identidade de dispositivo e do hub IoT do Azure utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff1e5-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff1e5-138">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ff1e5-138">Next steps</span></span>
<span data-ttu-id="ff1e5-139">[Crie o seu IoT hub e registe Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="ff1e5-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
