---
title: "Ligar Arduino tooAzure IoT - Lesson 1: implementar a aplicação | Microsoft Docs"
description: "Clone Olá exemplo Arduino de aplicação a partir do GitHub e executar gulp toodeploy tooyour esta aplicação Adafruit Feather M0 Wi-Fi. Esta aplicação de exemplo fica intermitente Olá GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino guiado projetos, arduino guiado blink, arduino guiado blink código, arduino blink programa, arduino blink exemplo"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Criar e implementar a aplicação de blink Olá
## <a name="what-you-will-do"></a>O que irá fazer
Clone Olá exemplo Arduino de aplicação a partir do GitHub e utilizar Olá gulp ferramenta toodeploy Olá exemplo aplicação tooyour Adafruit Feather M0 Wi-Fi Arduino quadro. Olá exemplo aplicação fica intermitente Olá GPIO #13 barod GUIADO cada dois segundos.

Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting-page].

## <a name="what-you-will-learn"></a>O que aprenderá
* Como toodeploy e execução Olá aplicação de exemplo no seu painel Arduino.

## <a name="what-you-need"></a>Do que precisa
Tem concluiu com sucesso Olá seguintes operações:

* [Configurar o dispositivo][configure-your-device]
* [Obtenha as ferramentas de Olá][get-the-tools]

## <a name="open-hello-sample-application"></a>Aplicação de exemplo de Olá aberta
Olá tooopen aplicação de exemplo, siga estes passos:

1. Clone o repositório de exemplo de Olá a partir do GitHub executando Olá os seguintes comandos:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Abra a aplicação de exemplo de Olá no Visual Studio Code executando Olá os seguintes comandos:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

Olá `app.ino` ficheiro Olá `app` subpasta é o ficheiro de origem da chave de Olá que contém Olá código toocontrol Olá LED.

### <a name="install-application-dependencies"></a>Instale as dependências da aplicação
Instale as bibliotecas de Olá e outros módulos que precisa para a aplicação de exemplo de Olá executando Olá os seguintes comandos:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurar a ligação ao dispositivo Olá
tooconfigure Olá ligação do dispositivo, siga estes passos:

1. Obter a porta série de Olá do dispositivo Olá com a cli de deteção de dispositivo Olá:

   ```bash
   devdisco list --usb
   ```

   Deverá ver um resultado que é semelhante toohello seguinte e encontrar Olá usb porta COM para a sua placa Arduino: ![deteção de dispositivos][device-discovery]

2. Ficheiro aberto Olá `config.json` no Olá pasta lesson e adicionar valor Olá Olá encontrar o número da porta COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config][config-json]
   > [!NOTE]
   > Para a porta de Olá COM, na plataforma do Windows, tem um formato de Olá `COM1, COM2, ...`. No macOS ou Ubuntu, começa com `/dev/`.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar e executar a aplicação de exemplo de Olá
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Instalar as ferramentas de Olá necessário para a placa de Arduino

Instale Olá SDK do Hub IoT do Azure para a placa de Arduino executando Olá os seguintes comandos:

```bash
gulp install-tools
```

Esta tarefa pode demorar um toocomplete muito tempo, dependendo da sua ligação de rede.

> [!NOTE]
> Saia Olá executar a instância de Arduino IDE quando executar tarefas gulp: `install-tools`, `run`.

### <a name="deploy-and-run-hello-sample-app"></a>Implementar e executar a aplicação de exemplo de Olá
Implementar e executar a aplicação de exemplo de Olá executando Olá os seguintes comandos:

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Verificar Olá aplicação funciona
Se não vir Olá LED blinking, consulte Olá [guia de resolução de problemas] [ troubleshooting-page] para problemas de toocommon soluções.

![LED blinking][led-blinking]

## <a name="summary"></a>Resumo
Ter instalado Olá necessário ferramentas toowork com o seu painel Arduino e implementados um Olá de tooblink quadro do exemplo aplicação tooyour Arduino LED. Agora pode criar, implementar e executar outra aplicação de exemplo que se liga a tooAzure de placa de Arduino toosend do IoT Hub e receber mensagens.

## <a name="next-steps"></a>Passos seguintes
[Obter Olá ferramentas do Azure][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md