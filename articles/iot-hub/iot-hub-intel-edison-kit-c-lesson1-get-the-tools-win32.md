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
# <a name="get-hello-tools-windows-7-or-later"></a>Obter ferramentas Olá (Windows 7 ou posterior)
> [!div class="op_single_selector"]
> * [Windows 7 ou posterior][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>O que irá fazer
Transferir as ferramentas de desenvolvimento de Olá e software Olá para Olá primeiro exemplo de aplicação para Intel Edison. Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].

> [!NOTE]
> Embora Olá linguagem de lógica principal Olá de programação C, Node.js ferramentas são utilizadas no Olá lições toobuild e implementar aplicações de exemplo.

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, irá aprender:

* Como tooinstall Git e Node.js.
  * [Git](https://git-scm.com) é um sistema de controlo de versão de código aberto distribuído. aplicação de exemplo de Olá para este artigo é armazenada no Git.
  * [NODE.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um ecossistema de pacote avançado.
* Como toouse NPM tooinstall adicionais Node.js ferramentas de desenvolvimento.
  * é o requisito de versão mínima de Olá do Node.js 4.5 LTS.
  * [NPM](https://www.npmjs.com) é uma das Olá gestores de pacote para Node.js.

## <a name="what-you-need"></a>Do que precisa

toocomplete desta operação, terá de:

* Um toodownload de ligação de Internet Olá ferramentas de desenvolvimento e Olá software.
* Um computador que está a executar o Windows.

## <a name="install-git-and-nodejs"></a>Instalar o Git e Node.js

Clique nas ligações de Olá abaixo toodownload e instalar o Git e LTS Node.js para o Windows.

* [Obter o Git para Windows](https://git-scm.com/download/win/)
* [Obter Node.js LTS para o Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Instalar ferramentas de desenvolvimento adicionais do Node.js

Utilize [gulp.js](http://gulpjs.com) tooautomate implementação Olá tooEdison de aplicação de exemplo de Olá.

Inicie uma linha de comandos como administrador. Instalar `gulp` executando Olá os seguintes comandos:

```cmd
npm install -g gulp
```

Se ocorrerem problemas instalar Node.js e estas ferramentas de desenvolvimento do Node.js adicionais no seu computador, consulte Olá [guia de resolução de problemas] [ troubleshooting] para problemas de toocommon soluções.

## <a name="install-visual-studio-code"></a>Instalar Visual Studio Code

[Transferir](https://code.visualstudio.com/docs/setup/windows) e instalar o Visual Studio Code. Visual Studio Code é um editor de código simples mas potentes origem para o Windows, Linux e macOS. Utilize este editor mais à frente no código de exemplo Olá tutorial tooedit Olá.

## <a name="summary"></a>Resumo

Instalou o software para a primeira aplicação de exemplo Olá e ferramentas de desenvolvimento de Olá necessário. a tarefa seguinte Olá está toocreate, implementar e executar a aplicação de exemplo de Olá no Edison.

## <a name="next-steps"></a>Passos seguintes

[Criar e implementar a aplicação de blink Olá][create-and-deploy-the-blink-application]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
