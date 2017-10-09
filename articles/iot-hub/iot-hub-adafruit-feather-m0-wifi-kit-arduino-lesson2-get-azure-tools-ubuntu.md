---
title: 'Ligar Arduino tooAzure IoT - Lesson 2: ferramentas do Azure (Ubuntu) | Microsoft Docs'
description: Instale o Python e interface de linha de comandos do Azure (CLI do Azure) no Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do Azure, o serviço de nuvem do iot, arduino nuvem"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7eb9c891a6340fee018894883583022d740ecb6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="d70b8-104">Obter ferramentas do Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="d70b8-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="d70b8-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="d70b8-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="d70b8-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="d70b8-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="d70b8-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="d70b8-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d70b8-108">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="d70b8-108">What you will do</span></span>

<span data-ttu-id="d70b8-109">Instale Olá interface de linha de comandos do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="d70b8-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="d70b8-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) para seu painel Adafruit Feather M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="d70b8-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d70b8-111">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="d70b8-111">What you will learn</span></span>
<span data-ttu-id="d70b8-112">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="d70b8-112">In this article, you will learn:</span></span>
* <span data-ttu-id="d70b8-113">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d70b8-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="d70b8-114">Como tooadd um subgrupo IoT de Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d70b8-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d70b8-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="d70b8-115">What you need</span></span>
* <span data-ttu-id="d70b8-116">Um computador de Ubuntu com uma ligação à Internet.</span><span class="sxs-lookup"><span data-stu-id="d70b8-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="d70b8-117">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d70b8-117">An active Azure subscription.</span></span> <span data-ttu-id="d70b8-118">Se não tiver uma conta, pode criar um [conta de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d70b8-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="d70b8-119">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d70b8-119">Install hello Azure CLI</span></span>
<span data-ttu-id="d70b8-120">Olá CLI do Azure fornece uma experiência multiplataformas de linha de comandos do Azure, permitindo-lhe toowork diretamente a partir do seu tooprovision de linha de comandos e gerir os recursos.</span><span class="sxs-lookup"><span data-stu-id="d70b8-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="d70b8-121">tooinstall hello mais recente CLI do Azure, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="d70b8-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="d70b8-122">Olá execute os seguintes comandos numa janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="d70b8-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="d70b8-123">Poderá demorar cinco minutos tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d70b8-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="d70b8-124">Verificar a instalação de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d70b8-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="d70b8-125">Deverá ver a seguinte Olá de saída se a instalação de Olá é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="d70b8-125">You should see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito][output]

## <a name="summary"></a><span data-ttu-id="d70b8-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="d70b8-127">Summary</span></span>
<span data-ttu-id="d70b8-128">Instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d70b8-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="d70b8-129">A próxima tarefa consiste toocreate o hub IoT do Azure e, em seguida, utilizar identidade de dispositivo Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d70b8-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d70b8-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d70b8-130">Next steps</span></span>
<span data-ttu-id="d70b8-131">[Criar o seu IoT hub e registar o seu painel Arduino][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="d70b8-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md