---
title: 'Connect Intel EDISON (C) tooAzure IoT - Lesson 3: monitorizar as mensagens | Microsoft Docs'
description: "Monitorizar mensagens hello do dispositivo para a nuvem, eles são escritas tooyour Table storage do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados em nuvem Olá, recolha de dados de nuvem, serviço de nuvem do iot, dados de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2679b22f2987f77ecd1eea03044ed8ea03bf73f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Mensagens de leitura continuada no armazenamento do Azure
## <a name="what-you-will-do"></a>O que irá fazer
Mensagens do dispositivo para nuvem de Olá monitor que são enviadas a partir do IoT hub tooyour Intel Edison como mensagens hello são escritas tooyour Table storage do Azure. Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, ficará a saber como toouse mensagens hello do gulp tarefa mensagem de leitura tooread continuada no seu armazenamento de tabelas do Azure.

## <a name="what-you-need"></a>Do que precisa
Antes de iniciar este processo, tem concluiu com sucesso [executar a aplicação de exemplo Olá blink do Azure no Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Novas mensagens de leitura da sua conta de armazenamento
No artigo anterior Olá, foi executada uma aplicação de exemplo na Edison. aplicação de exemplo de Olá enviadas mensagens tooyour Azure do IoT hub. mensagens Hello enviadas tooyour IoT hub são armazenadas no seu armazenamento de tabelas do Azure através da aplicação Olá função do Azure. Terá de mensagens de tooread de cadeia de ligação de armazenamento do Azure de Olá do seu armazenamento de tabelas do Azure.

mensagens de tooread armazenadas no seu armazenamento de tabelas do Azure, siga estes passos:

1. Obter a cadeia de ligação de Olá executando Olá os seguintes comandos:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   comando primeiro Olá obtém Olá `storage name` que é utilizado no Olá segundo comando tooget Olá cadeia de ligação. Utilize `iot-sample` como valor Olá `{resource group name}` se não alterar o valor de Olá.
2. Ficheiro de configuração aberta Olá `config-edison.json` no Visual Studio Code executando Olá os seguintes comandos:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Substitua `[Azure storage connection string]` com a cadeia de ligação de Olá que obteve no passo 1.
4. Guardar Olá `config-edison.json` ficheiro.
5. Enviar mensagens novamente e lê-los do seu armazenamento de tabelas do Azure executando Olá os seguintes comandos:

   ```bash
   gulp run --read-storage
   ```

   Olá lógica para ler a partir do Table storage do Azure está a ser Olá `azure-table.js` ficheiro.

   ![gulp executar – armazenamento de leitura][gulp run]

## <a name="summary"></a>Resumo
Tiver ligado Edison tooyour do IoT hub na nuvem de Olá e utilizado mensagens dispositivo-nuvem da toosend aplicação Olá blink exemplo com êxito. Também utilizado Olá função do Azure aplicação toostore entrado IoT hub mensagens tooyour Table storage do Azure. Agora pode enviar mensagens de nuvem para o dispositivo do seu tooEdison de hub IoT.

## <a name="next-steps"></a>Passos seguintes
[Executar um tooreceive de aplicação de exemplo mensagens da nuvem para dispositivo][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md