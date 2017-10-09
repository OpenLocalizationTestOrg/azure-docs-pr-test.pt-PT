---
title: 'Connect Arduino (C) tooAzure IoT - Lesson 3: executar o exemplo | Microsoft Docs'
description: "Implementar e executar um tooAdafruit de aplicação de exemplo uma Wi do M0-Feather Fi que envia o IoT hub tooyour mensagens e fica intermitente Olá LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem do IOT, arduino enviar dados toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Executar um toosend de aplicação de exemplo mensagens do dispositivo-nuvem
## <a name="what-you-will-do"></a>O que irá fazer
Este artigo irá mostrar como toodeploy e execute um exemplo de aplicação no seu Adafruit Feather M0 Wi-Fi Arduino quadro que envia mensagens tooyour IoT hub.

Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>O que aprenderá
Ficará a saber como toouse Olá gulp toodeploy ferramenta e execute a aplicação de Arduino de exemplo de Olá no seu painel Arduino.

## <a name="what-you-need"></a>Do que precisa
* Antes de começar esta tarefa, deve concluiu com sucesso [criar uma aplicação de função do Azure e um armazenamento conta tooprocess e arquivo IoT hub mensagens][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obter as cadeias de ligação do IoT hub e dispositivos
Olá, a cadeia de ligação do dispositivo é utilizado tooconnect Arduino quadro tooyour hub IoT. cadeia de ligação do Olá IoT hub é utilizado tooconnect a sua identidade dispositivos do IoT hub toohello que representa o Arduino quadro no hub IoT de Olá.

* Lista todos os os IoT hubs no seu grupo de recursos, executando Olá os seguintes comandos da CLI do Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Utilize `iot-sample` como valor Olá `{resource group name}` se não alterar o valor de Olá.

* Obter a cadeia de ligação do Olá IoT hub executando o seguinte comando da CLI do Azure de Olá:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`é o nome de Olá que especificou quando criou o seu hub IoT e registado o seu painel Arduino.

* Obter a cadeia de ligação do dispositivo Olá executando Olá os seguintes comandos:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Utilize `mym0wifi` como valor Olá `{device id}` se não alterar o valor de Olá.
## <a name="configure-hello-device-connection"></a>Configurar a ligação ao dispositivo Olá
tooconfigure Olá ligação do dispositivo, siga estes passos:

1. Obter a porta série de Olá do dispositivo Olá com a cli de deteção de dispositivo Olá:

   ```bash
   devdisco list --usb
   ```

   Deverá ver um resultado que é semelhante toohello seguinte e encontrar Olá usb porta COM para a sua placa Arduino:

   ![Deteção de dispositivos][device-discovery]

2. Ficheiro aberto Olá `config.json` no Olá pasta lesson e adicionar valor Olá Olá encontrar o número da porta COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config][config-json]

   > [!NOTE]
   > Para a porta de Olá COM, na plataforma do Windows, tem um formato de Olá `COM1, COM2, ...`. No macOS ou Ubuntu, começa com `/dev/`.

3. Inicializar o ficheiro de configuração de Olá executando Olá os seguintes comandos:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Ficheiro de configuração de dispositivo Olá abra `config-arduino.json` no Visual Studio Code executando Olá os seguintes comandos:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![configuração arduino.json][config-arduino-json]

5. Tornar Olá seguir substituições no Olá `config-arduino.json` ficheiro:

   * Substitua **[Wi-Fi SSID]** com o SSID de Wi-Fi ligado toohello Internet.
   * Substitua **[Wi-Fi palavra-passe]** com a palavra-passe de Wi-Fi. Remova a cadeia de Olá se Wi-Fi não necessita de palavra-passe.
   * Substitua **[cadeia de ligação do dispositivo IoT]** com Olá `device connection string` obtido.
   * Substitua **[cadeia de ligação do hub IoT]** com Olá `iot hub connection string` obtido.

   > [!NOTE]
   > Não precisa de `azure_storage_connection_string` neste artigo. Mantenha-lo tal como está.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar e executar a aplicação de exemplo de Olá
Implementar e executar aplicações de exemplo de Olá no seu painel Arduino executando Olá os seguintes comandos:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Olá predefinido gulp tarefa é executada `install-tools` e `run` tarefas sequencialmente. Quando lhe [implementado Olá blink aplicação][deployed-the-blink-app], executou estas tarefas separadamente.

## <a name="verify-that-hello-sample-application-works"></a>Certifique-se de que a aplicação de exemplo de Olá funciona
Deverá ver Olá GPIO #0 blinking de LED uma cada dois segundos. Sempre que fica intermitente Olá LED, a aplicação de exemplo de Olá envia uma mensagem tooyour do IoT hub e verifica que essa mensagem de saudação tenha enviada com êxito tooyour IoT hub. Além disso, cada mensagem recebida pelo IoT hub do Olá está impresso na janela de consola Olá. aplicação de exemplo de Olá automaticamente termina após 20 mensagens a enviar.

![Aplicação de exemplo com enviadas e recebidas mensagens][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Resumo
Tiver implementado e execute Olá novo blink exemplo de aplicação no seu IoT hub do Arduino quadro toosend mensagens do dispositivo para nuvem tooyour. Agora a monitorizar as mensagens que são escritos toohello conta de armazenamento.

## <a name="next-steps"></a>Passos seguintes
[Mensagens de leitura continuada no armazenamento do Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md