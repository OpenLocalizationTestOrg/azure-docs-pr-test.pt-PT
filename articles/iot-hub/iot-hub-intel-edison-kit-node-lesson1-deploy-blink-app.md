---
title: "Ligar Intel Edison (nó) tooAzure IoT - Lesson 1: implementar a aplicação | Microsoft Docs"
description: "Clone a aplicação de exemplo C Olá a partir do GitHub e execute gulp toodeploy tooyour esta aplicação quadro Intel Edison. Esta aplicação de exemplo fica intermitente Olá LED ligado toohello quadro cada dois segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino guiado projetos, arduino guiado blink, arduino guiado blink código, arduino blink programa, arduino blink exemplo"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Criar e implementar a aplicação de blink Olá
## <a name="what-you-will-do"></a>O que irá fazer
Clone a aplicação de exemplo C Olá a partir do GitHub e utilizar Olá gulp ferramenta toodeploy Olá exemplo aplicação tooIntel Edison. aplicação de exemplo de Olá fica intermitente Olá LED ligado toohello quadro cada dois segundos. Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>O que aprenderá
* Como toodeploy e execução Olá aplicação de exemplo no Edison.

## <a name="what-you-need"></a>Do que precisa
Tem concluiu com sucesso Olá seguintes operações:

* [Configurar o dispositivo][configure-your-device]
* [Obtenha as ferramentas de Olá][get-the-tools]

## <a name="open-hello-sample-application"></a>Aplicação de exemplo de Olá aberta
Olá tooopen aplicação de exemplo, siga estes passos:

1. Clone o repositório de exemplo de Olá a partir do GitHub executando Olá os seguintes comandos:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Abra a aplicação de exemplo de Olá no Visual Studio Code executando Olá os seguintes comandos:

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

ficheiro Olá Olá `app` subpasta é o ficheiro de origem da chave de Olá que contém Olá código toocontrol Olá LED.

### <a name="install-application-dependencies"></a>Instale as dependências da aplicação
Instale as bibliotecas de Olá e outros módulos que precisa para a aplicação de exemplo de Olá executando Olá os seguintes comandos:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurar a ligação ao dispositivo Olá
tooconfigure Olá ligação do dispositivo, siga estes passos:

1. Gere o ficheiro de configuração de dispositivo Olá executando Olá os seguintes comandos:

   ```bash
   gulp init
   ```

   ficheiro de configuração de Olá `config-edison.json` contém credenciais de utilizador de Olá utilize toolog tooEdison. fuga de Olá tooavoid das credenciais do utilizador, o ficheiro de configuração de Olá é gerado na subpasta Olá `.iot-hub-getting-started` da pasta raiz de Olá no seu computador.

2. Abra o ficheiro de configuração de dispositivo Olá no Visual Studio Code executando Olá os seguintes comandos:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Substitua o marcador de posição de Olá `[device hostname or IP address]` e `[device password]` com o endereço IP Olá e a palavra-passe que marcado para baixo no lesson anterior.

   ![Config](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Parabéns! Criou com êxito Olá primeiro exemplo de aplicação para Edison.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar e executar a aplicação de exemplo de Olá

### <a name="deploy-and-run-hello-sample-app"></a>Implementar e executar a aplicação de exemplo de Olá
Implementar e executar a aplicação de exemplo de Olá executando Olá os seguintes comandos:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Verificar Olá aplicação funciona
aplicação de exemplo de Olá automaticamente termina após Olá LED fica intermitente para 20 vezes. Se não vir Olá LED blinking, consulte Olá [guia de resolução de problemas] [ troubleshooting] para problemas de toocommon soluções.

![LED blinking][led-blinking]

## <a name="summary"></a>Resumo
Ter instalado Olá necessário ferramentas toowork com Edison e implementado um Olá no exemplo aplicação tooEdison tooblink LED. Agora pode criar, implementar e executar outra aplicação de exemplo que se liga Edison tooAzure toosend do IoT Hub e receber mensagens.

## <a name="next-steps"></a>Passos seguintes
[Obter Olá ferramentas do Azure][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
