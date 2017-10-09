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
# <a name="get-hello-tools-macos-1010"></a>Obter ferramentas Olá (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 ou posterior](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>O que irá fazer
Transferir as ferramentas de desenvolvimento de Olá e software Olá para Olá primeiro exemplo de aplicação para sua 3 de Pi Raspberry. Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Embora Olá linguagem de lógica principal Olá de programação C, Node.js e ferramentas de são utilizadas nos dispositivos do Olá lições toodiscover, criarem e implementar aplicações de exemplo.

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, irá aprender:

* Como tooinstall Git e Node.js.
  * [Git](https://git-scm.com) é um sistema de controlo de versão de código aberto distribuído. aplicação de exemplo de Olá para este artigo é armazenada no Git.
  * [NODE.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um ecossistema de pacote avançado.
* Como toouse NPM tooinstall adicionais Node.js ferramentas de desenvolvimento.
  * Olá versão mínima necessária do Node.js é 4.5 LTS.
  * [NPM](https://www.npmjs.com) é uma das Olá gestores de pacote para Node.js.

## <a name="what-you-need"></a>Do que precisa
toocomplete desta operação, terá de:

* Um toodownload de ligação de Internet Olá ferramentas de desenvolvimento e Olá software.
* Um Mac que esteja a executar macOS Yosemite (10.10) ou posterior.

## <a name="install-git-and-nodejs"></a>Instalar o Git e Node.js
tooinstall Git e Node.js, utilize Olá [Homebrew](http://brew.sh) utilitário de gestão do pacote, seguindo estes passos:

1. Instale Homebrew. Se já instalou Homebrew, visite toostep 2.
   
   1. Prima `Cmd + Space` e introduza `Terminal` tooopen um terminal.
   2. Execute Olá os seguintes comandos:
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Instale o Git e Node.js executando Olá os seguintes comandos:
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Instalar ferramentas de desenvolvimento adicionais do Node.js
Utilize [gulp.js](http://gulpjs.com) tooautomate implementação Olá tooyour de aplicação de exemplo de Olá Pi. Olá utilize [cli de deteção de dispositivo](https://github.com/Azure/device-discovery-cli) informações da rede tooretrieve sobre os seus dispositivos de IoT.

Instalar `gulp` e `device-discovery-cli` executando Olá os seguintes comandos no terminal Olá:

```bash
sudo npm install -g device-discovery-cli gulp
```

Se ocorrerem problemas a instalar estas ferramentas de desenvolvimento adicionais e Node.js no macOS, consulte Olá [guia de resolução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para problemas de toocommon soluções.

## <a name="install-visual-studio-code"></a>Instalar Visual Studio Code
[Transferir](https://code.visualstudio.com/docs/setup/osx) e instalar o Visual Studio Code. Visual Studio Code é um editor de código simples mas potentes origem para o Windows, Linux e macOS. Utilize este editor mais à frente no código de exemplo Olá tutorial tooedit Olá.

## <a name="summary"></a>Resumo
Instalou o software para a primeira aplicação de exemplo Olá e ferramentas de desenvolvimento de Olá necessário. a tarefa seguinte Olá está toocreate, implementar e executar a aplicação de exemplo de Olá no Pi.

## <a name="next-steps"></a>Passos seguintes
[Criar e implementar a aplicação de blink Olá](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

