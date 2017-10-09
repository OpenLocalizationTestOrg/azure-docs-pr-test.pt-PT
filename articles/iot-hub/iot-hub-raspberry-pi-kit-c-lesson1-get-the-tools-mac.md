---
title: 'Connect Raspberry PI (C) tooAzure IoT - Lesson 1: obter ferramentas (macOS) | Microsoft Docs'
description: "Transfira e instale as ferramentas necessárias Olá e software para Olá primeiro exemplo de aplicação para Pi no macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento do IOT, software de iot, internet de software coisas, instalação git no mac, gulp executar, instalação nó js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="c79d7-104">Obter ferramentas Olá (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="c79d7-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c79d7-105">Windows 7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="c79d7-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="c79d7-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c79d7-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="c79d7-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="c79d7-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="c79d7-108">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="c79d7-108">What you will do</span></span>
<span data-ttu-id="c79d7-109">Transferir as ferramentas de desenvolvimento de Olá e software Olá para Olá primeiro exemplo de aplicação para sua 3 de Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="c79d7-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="c79d7-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c79d7-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c79d7-111">Embora Olá linguagem de lógica principal Olá de programação C, Node.js e ferramentas de são utilizadas nos dispositivos do Olá lições toodiscover, criarem e implementar aplicações de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c79d7-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c79d7-112">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="c79d7-112">What you will learn</span></span>
<span data-ttu-id="c79d7-113">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="c79d7-113">In this article, you will learn:</span></span>

* <span data-ttu-id="c79d7-114">Como tooinstall Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="c79d7-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="c79d7-115">[Git](https://git-scm.com) é um sistema de controlo de versão de código aberto distribuído.</span><span class="sxs-lookup"><span data-stu-id="c79d7-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="c79d7-116">aplicação de exemplo de Olá para este artigo é armazenada no Git.</span><span class="sxs-lookup"><span data-stu-id="c79d7-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="c79d7-117">[NODE.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um ecossistema de pacote avançado.</span><span class="sxs-lookup"><span data-stu-id="c79d7-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="c79d7-118">Como toouse NPM tooinstall adicionais Node.js ferramentas de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="c79d7-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="c79d7-119">Olá versão mínima necessária do Node.js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="c79d7-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="c79d7-120">[NPM](https://www.npmjs.com) é uma das Olá gestores de pacote para Node.js.</span><span class="sxs-lookup"><span data-stu-id="c79d7-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c79d7-121">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="c79d7-121">What you need</span></span>
<span data-ttu-id="c79d7-122">toocomplete desta operação, terá de:</span><span class="sxs-lookup"><span data-stu-id="c79d7-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="c79d7-123">Um toodownload de ligação de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="c79d7-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="c79d7-124">Um Mac que esteja a executar macOS Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c79d7-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="c79d7-125">Instalar o Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="c79d7-125">Install Git and Node.js</span></span>
<span data-ttu-id="c79d7-126">tooinstall Git e Node.js, utilize Olá [Homebrew](http://brew.sh) utilitário de gestão do pacote, seguindo estes passos:</span><span class="sxs-lookup"><span data-stu-id="c79d7-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="c79d7-127">Instale Homebrew.</span><span class="sxs-lookup"><span data-stu-id="c79d7-127">Install Homebrew.</span></span> <span data-ttu-id="c79d7-128">Se já instalou Homebrew, visite toostep 2.</span><span class="sxs-lookup"><span data-stu-id="c79d7-128">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="c79d7-129">Prima `Cmd + Space` e introduza `Terminal` tooopen um terminal.</span><span class="sxs-lookup"><span data-stu-id="c79d7-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="c79d7-130">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c79d7-130">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="c79d7-131">Instale o Git e Node.js executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c79d7-131">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="c79d7-132">Instalar ferramentas de desenvolvimento adicionais do Node.js</span><span class="sxs-lookup"><span data-stu-id="c79d7-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="c79d7-133">Utilize [gulp.js](http://gulpjs.com) tooautomate implementação Olá tooyour de aplicação de exemplo de Olá Pi.</span><span class="sxs-lookup"><span data-stu-id="c79d7-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Pi.</span></span> <span data-ttu-id="c79d7-134">Olá utilize [cli de deteção de dispositivo](https://github.com/Azure/device-discovery-cli) informações da rede tooretrieve sobre os seus dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="c79d7-134">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="c79d7-135">Instalar `gulp` e `device-discovery-cli` executando Olá os seguintes comandos no terminal Olá:</span><span class="sxs-lookup"><span data-stu-id="c79d7-135">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="c79d7-136">Se ocorrerem problemas a instalar estas ferramentas de desenvolvimento adicionais e Node.js no macOS, consulte Olá [guia de resolução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para problemas de toocommon soluções.</span><span class="sxs-lookup"><span data-stu-id="c79d7-136">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="c79d7-137">Instalar Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c79d7-137">Install Visual Studio Code</span></span>
<span data-ttu-id="c79d7-138">[Transferir](https://code.visualstudio.com/docs/setup/osx) e instalar o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c79d7-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="c79d7-139">Visual Studio Code é um editor de código simples mas potentes origem para o Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="c79d7-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="c79d7-140">Utilize este editor mais à frente no código de exemplo Olá tutorial tooedit Olá.</span><span class="sxs-lookup"><span data-stu-id="c79d7-140">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="c79d7-141">Resumo</span><span class="sxs-lookup"><span data-stu-id="c79d7-141">Summary</span></span>
<span data-ttu-id="c79d7-142">Instalou o software para a primeira aplicação de exemplo Olá e ferramentas de desenvolvimento de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="c79d7-142">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="c79d7-143">a tarefa seguinte Olá está toocreate, implementar e executar a aplicação de exemplo de Olá no Pi.</span><span class="sxs-lookup"><span data-stu-id="c79d7-143">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c79d7-144">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c79d7-144">Next steps</span></span>
[<span data-ttu-id="c79d7-145">Criar e implementar a aplicação de blink Olá</span><span class="sxs-lookup"><span data-stu-id="c79d7-145">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

