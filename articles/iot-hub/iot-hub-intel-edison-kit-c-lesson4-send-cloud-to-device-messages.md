---
title: 'Connect Intel EDISON (C) tooAzure IoT - Lesson 4: receber mensagens | Microsoft Docs'
description: "Um exemplo de aplicação é executada em Edison e monitoriza mensagens a receber do seu IoT hub. Uma nova tarefa gulp envia mensagens tooEdison do seu Olá de tooblink do IoT hub LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "controlo de arduino guiado da web, controlo de arduino guiado através da web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f0424506ff755e0b9514684787b37584d406d320
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="6a419-105">Executar um tooreceive de aplicação de exemplo mensagens da nuvem para dispositivo</span><span class="sxs-lookup"><span data-stu-id="6a419-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="6a419-106">Neste artigo, implementar uma aplicação de exemplo no Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="6a419-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="6a419-107">aplicação de exemplo de Olá monitoriza mensagens a receber do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a419-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="6a419-108">Executar também uma tarefa gulp no seu tooEdison do computador toosend mensagens do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a419-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="6a419-109">Quando a aplicação de exemplo de Olá recebe mensagens hello, fica intermitente Olá LED.</span><span class="sxs-lookup"><span data-stu-id="6a419-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="6a419-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="6a419-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6a419-111">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="6a419-111">What you will do</span></span>
* <span data-ttu-id="6a419-112">Ligar Olá exemplo aplicação tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a419-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="6a419-113">Implementar e executar a aplicação de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a419-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="6a419-114">Envie mensagens do seu Olá de tooblink tooEdison LED do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a419-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6a419-115">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="6a419-115">What you will learn</span></span>
<span data-ttu-id="6a419-116">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="6a419-116">In this article, you will learn:</span></span>
* <span data-ttu-id="6a419-117">Como toomonitor as mensagens a receber do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a419-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="6a419-118">Como toosend nuvem para o dispositivo mensagens do seu tooEdison de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6a419-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6a419-119">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="6a419-119">What you need</span></span>
* <span data-ttu-id="6a419-120">Intel Edison, configurar para utilização.</span><span class="sxs-lookup"><span data-stu-id="6a419-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="6a419-121">toolearn como tooset segurança Edison, consulte [configurar o dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="6a419-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="6a419-122">Um IoT hub que é criado na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a419-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="6a419-123">toolearn como toocreate IoT hub, consulte [criar o seu IoT Hub do Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="6a419-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="6a419-124">Ligar Olá exemplo aplicação tooyour do IoT hub</span><span class="sxs-lookup"><span data-stu-id="6a419-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="6a419-125">Certifique-se de que está na pasta do repositório de Olá `iot-hub-c-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="6a419-125">Make sure that you're in hello repo folder `iot-hub-c-edison-getting-started`.</span></span> <span data-ttu-id="6a419-126">Abra a aplicação de exemplo de Olá no Visual Studio Code executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6a419-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="6a419-127">ficheiro Olá Olá `app` subpasta é o ficheiro de origem da chave de Olá que contém mensagens hello do código toomonitor recebidos do hub IoT de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a419-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="6a419-128">Olá `blinkLED` Olá LED fica intermitente de função.</span><span class="sxs-lookup"><span data-stu-id="6a419-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Estrutura de repositório na aplicação de exemplo de Olá][repo-structure]
2. <span data-ttu-id="6a419-130">Inicializar o ficheiro de configuração de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6a419-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="6a419-131">Se concluiu passos Olá [criar uma conta de armazenamento e de aplicação de função do Azure] [ create-an-azure-function-app-and-storage-account] neste computador, todas as configurações de Olá são herdadas, para que possa avançar tarefas de toohello Olá passo da implementação e a executar a aplicação de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a419-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="6a419-132">Se concluiu passos Olá [criar uma conta de armazenamento e de aplicação de função do Azure] [ create-an-azure-function-app-and-storage-account] num computador diferente, terá de marcadores de posição do tooreplace Olá no Olá `config-edison.json` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6a419-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="6a419-133">Olá `config-edison.json` ficheiro está a ser subpasta Olá da sua pasta raiz.</span><span class="sxs-lookup"><span data-stu-id="6a419-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Conteúdo do ficheiro de configuração edison.json Olá](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="6a419-135">Substitua **[nome de anfitrião do dispositivo ou endereço IP]** com o endereço IP do dispositivo do Olá marcado como inativo quando configurou o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6a419-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="6a419-136">Substitua **[cadeia de ligação do dispositivo IoT]** pela cadeia de ligação de dispositivo Olá que obtém executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.</span><span class="sxs-lookup"><span data-stu-id="6a419-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="6a419-137">Substitua **[cadeia de ligação do hub IoT]** com Olá cadeia de ligação do IoT hub que obtém executando Olá `az iot hub show-connection-string --name {my hub name}` comando.</span><span class="sxs-lookup"><span data-stu-id="6a419-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6a419-138">Executar **gulp ferramentas de instalação** bem, se ainda não o fez, na Lesson 1.</span><span class="sxs-lookup"><span data-stu-id="6a419-138">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="6a419-139">Implementar e executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="6a419-139">Deploy and run hello sample application</span></span>
<span data-ttu-id="6a419-140">Implementar e executar aplicações de exemplo de Olá em Edison executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6a419-140">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="6a419-141">comando de gulp Olá implementa tooEdison de aplicação de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a419-141">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="6a419-142">Em seguida, executa aplicação Olá Edison e uma tarefa separada no anfitrião do computador toosend 20 blink mensagens tooEdison do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a419-142">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="6a419-143">Após a execução da aplicação de exemplo de Olá, começa a escutar toomessages do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a419-143">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="6a419-144">Entretanto, a tarefa de gulp Olá envia várias mensagens "blink" do seu tooEdison de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6a419-144">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="6a419-145">Para cada mensagem blink que recebe Edison, a aplicação de exemplo de Olá chama Olá `blinkLED` Olá de tooblink função LED.</span><span class="sxs-lookup"><span data-stu-id="6a419-145">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="6a419-146">Deverá ver blink LED Olá cada dois segundos como Olá gulp tarefa envia 20 mensagens do seu tooEdison de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6a419-146">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="6a419-147">Olá pela última vez um é uma mensagem de "Parar" deixa de aplicação Olá em execução.</span><span class="sxs-lookup"><span data-stu-id="6a419-147">hello last one is a "stop" message that stops hello application from running.</span></span>

![Aplicação de exemplo com gulp comando e blink mensagens][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="6a419-149">Resumo</span><span class="sxs-lookup"><span data-stu-id="6a419-149">Summary</span></span>
<span data-ttu-id="6a419-150">Que enviou com êxito as mensagens do seu Olá de tooblink tooEdison LED do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a419-150">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="6a419-151">tarefa seguinte Olá é opcional: altere Olá e desativar o comportamento de Olá LED.</span><span class="sxs-lookup"><span data-stu-id="6a419-151">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a419-152">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6a419-152">Next steps</span></span>
<span data-ttu-id="6a419-153">[Alterar Olá e desativar o comportamento de Olá LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="6a419-153">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md