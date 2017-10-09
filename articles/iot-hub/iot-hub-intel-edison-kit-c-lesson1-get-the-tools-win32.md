---
title: 'Connect Intel EDISON (C) tooAzure IoT - Lesson 1: obter ferramentas (Windows) | Microsoft Docs'
description: "Transfira e instale as ferramentas necessárias Olá e software para Olá primeiro exemplo de aplicação para Edison no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ferramentas de desenvolvimento arduino, desenvolvimento de iot, iot software, internet de software coisas, git de instalação no windows, instale nó js windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 7d29a358-544d-4657-a504-5ed9b79c2925
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 64d8684ffcb858845de02276a11cf2b2e5c701a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="82543-104">Obter ferramentas Olá (Windows 7 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="82543-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="82543-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="82543-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="82543-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="82543-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="82543-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="82543-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="82543-108">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="82543-108">What you will do</span></span>
<span data-ttu-id="82543-109">Transferir as ferramentas de desenvolvimento de Olá e software Olá para Olá primeiro exemplo de aplicação para Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="82543-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="82543-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="82543-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="82543-111">Embora Olá linguagem de lógica principal Olá de programação C, Node.js ferramentas são utilizadas no Olá lições toobuild e implementar aplicações de exemplo.</span><span class="sxs-lookup"><span data-stu-id="82543-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="82543-112">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="82543-112">What you will learn</span></span>
<span data-ttu-id="82543-113">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="82543-113">In this article, you will learn:</span></span>

* <span data-ttu-id="82543-114">Como tooinstall Git e Node.js.</span><span class="sxs-lookup"><span data-stu-id="82543-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="82543-115">[Git](https://git-scm.com) é um sistema de controlo de versão de código aberto distribuído.</span><span class="sxs-lookup"><span data-stu-id="82543-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="82543-116">aplicação de exemplo de Olá para este artigo é armazenada no Git.</span><span class="sxs-lookup"><span data-stu-id="82543-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="82543-117">[NODE.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um ecossistema de pacote avançado.</span><span class="sxs-lookup"><span data-stu-id="82543-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="82543-118">Como toouse NPM tooinstall adicionais Node.js ferramentas de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="82543-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="82543-119">é o requisito de versão mínima de Olá do Node.js 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="82543-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="82543-120">[NPM](https://www.npmjs.com) é uma das Olá gestores de pacote para Node.js.</span><span class="sxs-lookup"><span data-stu-id="82543-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="82543-121">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="82543-121">What you need</span></span>

<span data-ttu-id="82543-122">toocomplete desta operação, terá de:</span><span class="sxs-lookup"><span data-stu-id="82543-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="82543-123">Um toodownload de ligação de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="82543-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="82543-124">Um computador que está a executar o Windows.</span><span class="sxs-lookup"><span data-stu-id="82543-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="82543-125">Instalar o Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="82543-125">Install Git and Node.js</span></span>

<span data-ttu-id="82543-126">Clique nas ligações de Olá abaixo toodownload e instalar o Git e LTS Node.js para o Windows.</span><span class="sxs-lookup"><span data-stu-id="82543-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="82543-127">Obter o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="82543-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="82543-128">Obter Node.js LTS para o Windows</span><span class="sxs-lookup"><span data-stu-id="82543-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="82543-129">Instalar ferramentas de desenvolvimento adicionais do Node.js</span><span class="sxs-lookup"><span data-stu-id="82543-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="82543-130">Utilize [gulp.js](http://gulpjs.com) tooautomate implementação Olá tooEdison de aplicação de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="82543-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="82543-131">Inicie uma linha de comandos como administrador.</span><span class="sxs-lookup"><span data-stu-id="82543-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="82543-132">Instalar `gulp` executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="82543-132">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="82543-133">Se ocorrerem problemas instalar Node.js e estas ferramentas de desenvolvimento do Node.js adicionais no seu computador, consulte Olá [guia de resolução de problemas] [ troubleshooting] para problemas de toocommon soluções.</span><span class="sxs-lookup"><span data-stu-id="82543-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="82543-134">Instalar Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="82543-134">Install Visual Studio Code</span></span>

<span data-ttu-id="82543-135">[Transferir](https://code.visualstudio.com/docs/setup/windows) e instalar o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="82543-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="82543-136">Visual Studio Code é um editor de código simples mas potentes origem para o Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="82543-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="82543-137">Utilize este editor mais à frente no código de exemplo Olá tutorial tooedit Olá.</span><span class="sxs-lookup"><span data-stu-id="82543-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="82543-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="82543-138">Summary</span></span>

<span data-ttu-id="82543-139">Instalou o software para a primeira aplicação de exemplo Olá e ferramentas de desenvolvimento de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="82543-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="82543-140">a tarefa seguinte Olá está toocreate, implementar e executar a aplicação de exemplo de Olá no Edison.</span><span class="sxs-lookup"><span data-stu-id="82543-140">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82543-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="82543-141">Next steps</span></span>

<span data-ttu-id="82543-142">[Criar e implementar a aplicação de blink Olá][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="82543-142">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
