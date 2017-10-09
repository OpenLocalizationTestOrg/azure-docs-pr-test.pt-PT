---
title: 'Simulated dispositivo & Gateway do IoT do Azure - Lesson 3: ler mensagens | Microsoft Docs'
description: "Execute um código de exemplo no seu mensagens hello do anfitrião computador tooread do seu IoT hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados em nuvem Olá, recolha de dados de nuvem, serviço de nuvem do iot, dados de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Ler mensagens do seu IoT hub

## <a name="what-you-will-do"></a>O que irá fazer

- Execute o código de exemplo no seu anfitrião mensagens tooread de computador do seu IoT hub.

Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que aprenderá

Como toouse Olá gulp mensagens de tooread ferramenta do seu IoT hub.

## <a name="what-you-need"></a>Do que precisa

- exemplo de dispositivo simulado Olá no [configurar e executar uma nuvem de dispositivo simulado carregar a aplicação de exemplo](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obter as cadeias de ligação do IoT hub e dispositivos

cadeia de ligação do dispositivo Olá é utilizada pelo seu dispositivo simulado tooconnect tooyour do IoT hub. Olá cadeia de ligação do hub IoT é o registo de identidade toohello tooconnect utilizados nos seus dispositivos Olá do IoT hub toomanage que são permitidos tooconnect tooyour IoT hub.

- Lista todos os os IoT hubs no seu grupo de recursos, executando Olá os seguintes comandos:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Utilize `iot-gateway` como valor Olá `{resource group name}` se não alterá-la.
- Obter a cadeia de ligação do Olá IoT hub executando Olá os seguintes comandos:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`é o nome de Olá que especificou no Lesson 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Configurar a ligação ao dispositivo para o código de exemplo de Olá Olá

Atualizar o IoT hub e o dispositivo de ligação configurações `config-azure.json` efetuando Olá os seguintes passos:

1. Abra `config-azure.json` no Visual Studio Code executando Olá seguinte comando numa janela de consola:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Tornar Olá seguir substituições no Olá `config-azure.json` ficheiro:

   ![captura de ecrã da configuração do azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Substitua `[IoT hub connection string]` com Olá cadeia de ligação do IoT hub.

## <a name="read-messages-from-your-iot-hub"></a>Ler mensagens do seu IoT hub

Executar a aplicação de exemplo Olá simulado dispositivo e ler mensagens de IoT Hub por Olá os seguintes comandos:

```bash
gulp run --iot-hub
```

comando Olá executa a aplicação de Olá que envia o IoT hub tooyour mensagens cada 2 segundos. É também cria uma mensagem de saudação do tooreceive de processo subordinado.

mensagens Hello que estão a ser enviadas e recebidos são todos os Olá apresentados de forma instantânea na mesma consola janela no Olá computador anfitrião. aplicação Olá será fechada em segundos, 40.

![Aplicação de exemplo simulada com mensagens enviadas e recebidas](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Resumo

Que já executou com êxito o Olá exemplo aplicação toosend dados tooyour do IoT hub com o dispositivo simulado. Também já leu mensagens hello que foram enviadas tooyour IoT hub.

## <a name="next-steps"></a>Passos seguintes
[Criar uma aplicação de função do Azure e uma Conta de Armazenamento do Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


