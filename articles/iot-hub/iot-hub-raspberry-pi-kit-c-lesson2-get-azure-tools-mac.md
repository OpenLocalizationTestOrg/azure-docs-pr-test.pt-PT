---
title: 'Connect Raspberry PI (C) tooAzure IoT - Lesson 2: ferramentas do Azure (macOS) | Microsoft Docs'
description: Instale o Python e interface de linha de comandos do Azure (CLI do Azure) no macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli de serviço, do azure de nuvem do IOT"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="67413-104">Obter ferramentas do Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="67413-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67413-105">Windows 7 e posterior</span><span class="sxs-lookup"><span data-stu-id="67413-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="67413-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="67413-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="67413-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="67413-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="67413-108">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="67413-108">What you will do</span></span>
<span data-ttu-id="67413-109">Instale Olá interface de linha de comandos do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="67413-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="67413-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="67413-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="67413-111">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="67413-111">What you will learn</span></span>
<span data-ttu-id="67413-112">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="67413-112">In this article, you will learn:</span></span>
* <span data-ttu-id="67413-113">Como tooinstall CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="67413-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="67413-114">Como tooadd um subgrupo IoT de Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="67413-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="67413-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="67413-115">What you need</span></span>
* <span data-ttu-id="67413-116">Um Mac com uma ligação à Internet.</span><span class="sxs-lookup"><span data-stu-id="67413-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="67413-117">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="67413-117">An active Azure subscription.</span></span> <span data-ttu-id="67413-118">Se não tiver uma conta do Azure, pode criar um [conta de avaliação do Azure gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="67413-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="67413-119">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="67413-119">Install Python</span></span>
<span data-ttu-id="67413-120">Embora macOS é fornecido com o Python 2.7 Box Olá, recomendamos que instale Python através de Homebrew.</span><span class="sxs-lookup"><span data-stu-id="67413-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="67413-121">Consulte [instalar o Python no macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="67413-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="67413-122">Instale o Python e pip executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="67413-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="67413-123">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="67413-123">Install hello Azure CLI</span></span>
<span data-ttu-id="67413-124">Olá CLI do Azure fornece uma experiência de linha de comandos multiplataformas para o Azure.</span><span class="sxs-lookup"><span data-stu-id="67413-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="67413-125">Trabalhar diretamente a partir do seu tooprovision de linha de comandos e gerir os recursos.</span><span class="sxs-lookup"><span data-stu-id="67413-125">You work directly from your command line tooprovision and manage resources.</span></span> 

<span data-ttu-id="67413-126">tooinstall hello mais recente CLI do Azure, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="67413-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="67413-127">Olá execute os seguintes comandos numa janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="67413-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="67413-128">Poderá demorar cinco minutos tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="67413-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="67413-129">Verificar a instalação de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="67413-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="67413-130">Deverá ver a seguinte Olá de saída se a instalação de Olá é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="67413-130">You should see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="67413-132">Resumo</span><span class="sxs-lookup"><span data-stu-id="67413-132">Summary</span></span>
<span data-ttu-id="67413-133">Instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="67413-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="67413-134">A próxima tarefa consiste toocreate sua identidade do Azure IoT hub e dispositivos através da utilização de Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="67413-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67413-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="67413-135">Next steps</span></span>
[<span data-ttu-id="67413-136">Crie o seu IoT hub e registe Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="67413-136">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

