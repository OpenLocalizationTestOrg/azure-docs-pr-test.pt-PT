---
title: "Ligar Intel Edison (nó) tooAzure IoT - Lesson 2: ferramentas do Azure (Ubuntu) | Microsoft Docs"
description: Instale o Python e interface de linha de comandos do Azure (CLI do Azure) no Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do Azure, o serviço de nuvem do iot, arduino nuvem"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 6dcb34bf-54a3-4af0-ba89-95d5cfafceff
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca2996b779a4d3cde833c5f2824d19ec46241bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="72e48-104">Obter ferramentas do Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="72e48-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="72e48-105">[Windows 7 e posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="72e48-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="72e48-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="72e48-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="72e48-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="72e48-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="72e48-108">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="72e48-108">What you will do</span></span>
<span data-ttu-id="72e48-109">Instale Olá interface de linha de comandos do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="72e48-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="72e48-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="72e48-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="72e48-111">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="72e48-111">What you will learn</span></span>
<span data-ttu-id="72e48-112">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="72e48-112">In this article, you will learn:</span></span>
* <span data-ttu-id="72e48-113">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="72e48-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="72e48-114">Como tooadd um subgrupo IoT de Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="72e48-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="72e48-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="72e48-115">What you need</span></span>
* <span data-ttu-id="72e48-116">Um computador de Ubuntu com uma ligação à Internet.</span><span class="sxs-lookup"><span data-stu-id="72e48-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="72e48-117">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="72e48-117">An active Azure subscription.</span></span> <span data-ttu-id="72e48-118">Se não tiver uma conta, pode criar um [conta de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="72e48-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="72e48-119">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="72e48-119">Install hello Azure CLI</span></span>
<span data-ttu-id="72e48-120">Olá CLI do Azure fornece uma experiência multiplataformas de linha de comandos do Azure, permitindo-lhe toowork diretamente a partir do seu tooprovision de linha de comandos e gerir os recursos.</span><span class="sxs-lookup"><span data-stu-id="72e48-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="72e48-121">tooinstall hello mais recente CLI do Azure, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="72e48-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="72e48-122">Olá execute os seguintes comandos numa janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="72e48-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="72e48-123">Poderá demorar cinco minutos tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="72e48-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="72e48-124">Verificar a instalação de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="72e48-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="72e48-125">Deverá ver a seguinte Olá de saída se a instalação de Olá é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="72e48-125">You should see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="72e48-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="72e48-127">Summary</span></span>
<span data-ttu-id="72e48-128">Instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="72e48-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="72e48-129">A próxima tarefa consiste toocreate o hub IoT do Azure e, em seguida, utilizar identidade de dispositivo Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="72e48-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72e48-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="72e48-130">Next steps</span></span>
<span data-ttu-id="72e48-131">[Crie o seu IoT hub e registe Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="72e48-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
