---
title: "Ligar Raspberry Pi (nó) tooAzure IoT - Lesson 2: obter ferramentas (Windows) | Microsoft Docs"
description: "Instale o Python e Olá interface de linha de comandos do Azure (CLI do Azure) no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "cli de serviço, do azure de nuvem do IOT"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 25b50214322137ea32861fd1131c474e2fc7ebb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="34eda-104">Obter ferramentas do Azure (Windows 7 e posterior)</span><span class="sxs-lookup"><span data-stu-id="34eda-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34eda-105">Windows 7 e posterior</span><span class="sxs-lookup"><span data-stu-id="34eda-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="34eda-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="34eda-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="34eda-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="34eda-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="34eda-108">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="34eda-108">What you will do</span></span>
<span data-ttu-id="34eda-109">Instalar o Python e Olá interface de linha de comandos do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="34eda-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="34eda-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="34eda-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="34eda-111">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="34eda-111">What you will learn</span></span>
<span data-ttu-id="34eda-112">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="34eda-112">In this article, you will learn:</span></span>
* <span data-ttu-id="34eda-113">Como tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="34eda-113">How tooinstall Python.</span></span>
* <span data-ttu-id="34eda-114">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="34eda-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="34eda-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="34eda-115">What you need</span></span>
* <span data-ttu-id="34eda-116">Um computador Windows com uma ligação à Internet.</span><span class="sxs-lookup"><span data-stu-id="34eda-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="34eda-117">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="34eda-117">An active Azure subscription.</span></span> <span data-ttu-id="34eda-118">Se não tiver uma conta do Azure, crie um [conta de avaliação do Azure gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="34eda-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="34eda-119">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="34eda-119">Install Python</span></span>
<span data-ttu-id="34eda-120">[Instalar o Python](https://www.python.org/downloads/) no seu computador Windows.</span><span class="sxs-lookup"><span data-stu-id="34eda-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="34eda-121">Pode instalar o Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="34eda-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="34eda-122">Este tutorial baseia-se no Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="34eda-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="34eda-123">Se já tiver instalado o Python, aceda a secção seguinte toohello e instalar Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="34eda-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="34eda-124">Também precisa de caminho de Olá tooadd das pastas de olá onde python.exe e pip.exe são instalados toohello sistema `PATH` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="34eda-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="34eda-125">Por predefinição, python.exe é instalado em `C:\Python27` e pip.exe está instalado no `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="34eda-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="34eda-126">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="34eda-126">Install hello Azure CLI</span></span>
<span data-ttu-id="34eda-127">Olá CLI do Azure fornece uma experiência de linha de comandos multiplataformas para o Azure.</span><span class="sxs-lookup"><span data-stu-id="34eda-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="34eda-128">Trabalhar diretamente a partir do seu tooprovision da linha de comandos e gerir os recursos.</span><span class="sxs-lookup"><span data-stu-id="34eda-128">You work directly from your command-line tooprovision and manage resources.</span></span>

<span data-ttu-id="34eda-129">Olá tooinstall CLI do Azure, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="34eda-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="34eda-130">Abra uma janela de linha de comandos como administrador.</span><span class="sxs-lookup"><span data-stu-id="34eda-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="34eda-131">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="34eda-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="34eda-132">Verificar a instalação de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="34eda-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="34eda-133">Consulte a seguinte Olá de saída se a instalação de Olá é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="34eda-133">You see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="34eda-135">Resumo</span><span class="sxs-lookup"><span data-stu-id="34eda-135">Summary</span></span>
<span data-ttu-id="34eda-136">Instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="34eda-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="34eda-137">A seguinte tarefa toocreate sua identidade de dispositivo e do hub IoT do Azure utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="34eda-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34eda-138">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="34eda-138">Next steps</span></span>
[<span data-ttu-id="34eda-139">Crie o seu IoT hub e registe Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="34eda-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

