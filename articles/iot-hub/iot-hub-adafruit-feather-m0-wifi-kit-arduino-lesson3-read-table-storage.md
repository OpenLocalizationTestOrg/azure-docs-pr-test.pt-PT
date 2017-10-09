---
title: 'Connect Arduino (C) tooAzure IoT - Lesson 3: armazenamento de tabela | Microsoft Docs'
description: "Monitorizar mensagens hello do dispositivo para a nuvem, eles são escritas tooyour Table storage do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados em nuvem Olá, recolha de dados de nuvem, serviço de nuvem do iot, dados de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Mensagens de leitura continuada no armazenamento do Azure
## <a name="what-you-will-do"></a>O que irá fazer
Mensagens do dispositivo para nuvem de Olá monitor que são enviadas do seu IoT hub do Adafruit Feather M0 Wi-Fi Arduino quadro tooyour como mensagens hello são escritas tooyour Table storage do Azure.

Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, ficará a saber como toouse mensagens hello do gulp tarefa mensagem de leitura tooread continuada no seu armazenamento de tabelas do Azure.

## <a name="what-you-need"></a>Do que precisa
Antes de iniciar este processo, tem concluiu com sucesso [executar a aplicação de exemplo Olá blink do Azure no seu painel Arduino][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Novas mensagens de leitura da sua conta de armazenamento
No artigo anterior Olá, ficou um exemplo de aplicação no seu painel Arduino. aplicação de exemplo de Olá enviadas mensagens tooyour Azure do IoT hub. mensagens Hello enviadas tooyour IoT hub são armazenadas no seu armazenamento de tabelas do Azure através da aplicação Olá função do Azure. Terá de mensagens de tooread de cadeia de ligação de armazenamento do Azure de Olá do seu armazenamento de tabelas do Azure.

mensagens de tooread armazenadas no seu armazenamento de tabelas do Azure, siga estes passos:

1. Obter a cadeia de ligação de Olá executando Olá os seguintes comandos:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   comando primeiro Olá obtém Olá `storage name` que é utilizado no Olá segundo comando tooget Olá cadeia de ligação. Utilize `iot-sample` como valor Olá `{resource group name}` se não alterar o valor de Olá.
2. Ficheiro de configuração aberta Olá `config-arduino.json` no Visual Studio Code executando Olá os seguintes comandos:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Substitua `[Azure storage connection string]` com a cadeia de ligação de Olá que obteve no passo 1.
4. Guardar Olá `config-arduino.json` ficheiro.
5. Enviar mensagens novamente e lê-los do seu armazenamento de tabelas do Azure executando Olá os seguintes comandos:

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   Olá lógica para ler a partir do Table storage do Azure está a ser Olá `azure-table.js` ficheiro.

   ![gulp executar – armazenamento de leitura][gulp-run]

## <a name="summary"></a>Resumo
Tiver ligado Arduino quadro tooyour hub IoT na nuvem de Olá e utilizado mensagens dispositivo-nuvem da toosend aplicação Olá blink exemplo com êxito. Também utilizado Olá função do Azure aplicação toostore entrado IoT hub mensagens tooyour Table storage do Azure. Agora pode enviar mensagens de nuvem para o dispositivo do seu tooyour do hub IoT Arduino quadro.

## <a name="next-steps"></a>Passos seguintes
[Enviar mensagens da nuvem para dispositivo][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md