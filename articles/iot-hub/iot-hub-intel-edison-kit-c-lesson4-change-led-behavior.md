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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="9351d-104">Alterar Olá e desativar o comportamento de Olá LED</span><span class="sxs-lookup"><span data-stu-id="9351d-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9351d-105">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="9351d-105">What you will do</span></span>
<span data-ttu-id="9351d-106">Personalize Olá toochange mensagens de Olá LED do e desativar o comportamento.</span><span class="sxs-lookup"><span data-stu-id="9351d-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="9351d-107">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9351d-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9351d-108">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="9351d-108">What you will learn</span></span>
<span data-ttu-id="9351d-109">Utilize Olá toochange de funções adicionais LED do e desativar o comportamento.</span><span class="sxs-lookup"><span data-stu-id="9351d-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9351d-110">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="9351d-110">What you need</span></span>
<span data-ttu-id="9351d-111">Tem de concluir com êxito [execute um exemplo de aplicação na nuvem do Intel Edison tooreceive toodevice mensagens][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="9351d-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="9351d-112">Adicionar funções toomain.c e gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="9351d-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="9351d-113">Abra a aplicação de exemplo de Olá no Visual Studio code executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9351d-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="9351d-114">Abra Olá `main.c` de ficheiros e, em seguida, adicionar Olá seguintes funções após blinkLED() função:</span><span class="sxs-lookup"><span data-stu-id="9351d-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

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

3. <span data-ttu-id="9351d-116">Adicionar Olá seguintes condições antes de Olá `else if` bloco de Olá `receiveMessageCallback` função:</span><span class="sxs-lookup"><span data-stu-id="9351d-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="9351d-117">Agora que configurou instruções toomore toorespond de aplicação de exemplo de Olá através de mensagens.</span><span class="sxs-lookup"><span data-stu-id="9351d-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="9351d-118">Ativa a Olá "ativado" instrução Olá LED e Olá "off" instrução se desligar Olá LED.</span><span class="sxs-lookup"><span data-stu-id="9351d-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="9351d-119">Abrir o ficheiro de gulpfile.js Olá e, em seguida, adicione uma nova função antes da função Olá `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="9351d-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="9351d-121">No Olá `sendMessage` funcionar, substitua a linha de Olá `var message = buildMessage(sentMessageCount);` com linha nova Olá mostrada na Olá seguinte fragmento:</span><span class="sxs-lookup"><span data-stu-id="9351d-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="9351d-122">Guarde todas as alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="9351d-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="9351d-123">Implementar e executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="9351d-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="9351d-124">Implementar e executar aplicações de exemplo de Olá em Edison executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9351d-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="9351d-125">Deverá ver ative Olá LED de dois segundos e, em seguida, desative para outro dois segundos.</span><span class="sxs-lookup"><span data-stu-id="9351d-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="9351d-126">mensagem de saudação último "Parar" deixa de aplicação de exemplo de Olá a execução.</span><span class="sxs-lookup"><span data-stu-id="9351d-126">hello last "stop" message stops hello sample application from running.</span></span>

![e desativar][on-and-off]

<span data-ttu-id="9351d-128">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9351d-128">Congratulations!</span></span> <span data-ttu-id="9351d-129">Mensagens hello que são enviadas tooEdison do seu IoT hub com êxito tiver personalizado.</span><span class="sxs-lookup"><span data-stu-id="9351d-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="9351d-130">Resumo</span><span class="sxs-lookup"><span data-stu-id="9351d-130">Summary</span></span>
<span data-ttu-id="9351d-131">Esta secção opcional demonstra como toocustomize mensagens para que a aplicação de exemplo de Olá pode controlar Olá e desativar o comportamento de Olá LED de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="9351d-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
