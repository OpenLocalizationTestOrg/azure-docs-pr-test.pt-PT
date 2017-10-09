---
title: "Connect Intel EDISON (C) tooAzure IoT - Lesson 4: Blink Olá LED | Microsoft Docs"
description: "Personalize Olá toochange mensagens de Olá LED do e desativar o comportamento."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controlo guiado com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c51acb42aa297ca91cfe76d7b0361ad95e2fb2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Alterar Olá e desativar o comportamento de Olá LED
## <a name="what-you-will-do"></a>O que irá fazer
Personalize Olá toochange mensagens de Olá LED do e desativar o comportamento. Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>O que aprenderá
Utilize Olá toochange de funções adicionais LED do e desativar o comportamento.

## <a name="what-you-need"></a>Do que precisa
Tem de concluir com êxito [execute um exemplo de aplicação na nuvem do Intel Edison tooreceive toodevice mensagens][receive-cloud-to-device-messages].

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Adicionar funções toomain.c e gulpfile.js
1. Abra a aplicação de exemplo de Olá no Visual Studio code executando Olá os seguintes comandos:

   ```bash
   cd Lesson4
   code .
   ```
2. Abra Olá `main.c` de ficheiros e, em seguida, adicionar Olá seguintes funções após blinkLED() função:

   ```c
   static void turnOnLED()
   {
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![ficheiro de Main com funções adicionados](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. Adicionar Olá seguintes condições antes de Olá `else if` bloco de Olá `receiveMessageCallback` função:

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
   {
       turnOffLED();
   }
   ```

   Agora que configurou instruções toomore toorespond de aplicação de exemplo de Olá através de mensagens. Ativa a Olá "ativado" instrução Olá LED e Olá "off" instrução se desligar Olá LED.
4. Abrir o ficheiro de gulpfile.js Olá e, em seguida, adicione uma nova função antes da função Olá `sendMessage`:

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   }
   ```

   ![Ficheiro de Gulpfile.js com função adicionado][gulpfile]
5. No Olá `sendMessage` funcionar, substitua a linha de Olá `var message = buildMessage(sentMessageCount);` com linha nova Olá mostrada na Olá seguinte fragmento:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Guarde todas as alterações de Olá.

### <a name="deploy-and-run-hello-sample-application"></a>Implementar e executar a aplicação de exemplo de Olá
Implementar e executar aplicações de exemplo de Olá em Edison executando Olá os seguintes comandos:

```bash
gulp deploy && gulp run
```

Deverá ver ative Olá LED de dois segundos e, em seguida, desative para outro dois segundos. mensagem de saudação último "Parar" deixa de aplicação de exemplo de Olá a execução.

![e desativar][on-and-off]

Parabéns! Mensagens hello que são enviadas tooEdison do seu IoT hub com êxito tiver personalizado.

### <a name="summary"></a>Resumo
Esta secção opcional demonstra como toocustomize mensagens para que a aplicação de exemplo de Olá pode controlar Olá e desativar o comportamento de Olá LED de forma diferente.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
