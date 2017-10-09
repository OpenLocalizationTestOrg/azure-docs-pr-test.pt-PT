---
featureFlags: usabilla
title: "Ligar Raspberry Pi (nó) tooAzure IoT - Lesson 4: nuvem para o dispositivo | Microsoft Docs"
description: "aplicação de exemplo de Olá é executado no Pi e monitoriza mensagens a receber do seu IoT hub. Uma nova tarefa gulp envia mensagens tooPi do seu Olá de tooblink do IoT hub LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: nuvem toodevice, mensagem da nuvem
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="08e2a-105">Executar mensagens hello do exemplo aplicação tooreceive nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="08e2a-105">Run hello sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="08e2a-106">Neste artigo, implementar uma aplicação de exemplo em Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="08e2a-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="08e2a-107">aplicação de exemplo de Olá monitoriza mensagens a receber do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08e2a-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="08e2a-108">Executar também uma tarefa gulp no seu tooPi do computador toosend mensagens do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08e2a-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="08e2a-109">Quando a aplicação de exemplo de Olá recebe mensagens hello, fica intermitente Olá LED.</span><span class="sxs-lookup"><span data-stu-id="08e2a-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="08e2a-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="08e2a-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="08e2a-111">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="08e2a-111">What you will do</span></span>
* <span data-ttu-id="08e2a-112">Ligar Olá exemplo aplicação tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08e2a-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="08e2a-113">Implementar e executar a aplicação de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="08e2a-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="08e2a-114">Envie mensagens do seu Olá de tooblink tooPi LED do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08e2a-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="08e2a-115">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="08e2a-115">What you will learn</span></span>
<span data-ttu-id="08e2a-116">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="08e2a-116">In this article, you will learn:</span></span>
* <span data-ttu-id="08e2a-117">Como toomonitor as mensagens a receber do seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="08e2a-117">How toomonitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="08e2a-118">Como toosend nuvem para o dispositivo mensagens do seu tooPi de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="08e2a-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="08e2a-119">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="08e2a-119">What you need</span></span>
* <span data-ttu-id="08e2a-120">Raspberry Pi 3, configurar para utilização.</span><span class="sxs-lookup"><span data-stu-id="08e2a-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="08e2a-121">toolearn como tooset segurança Pi, consulte [configurar o dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="08e2a-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="08e2a-122">Um IoT hub que é criado na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="08e2a-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="08e2a-123">toolearn como toocreate IoT hub, consulte [crie o seu IoT hub e registe Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="08e2a-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="08e2a-124">Ligar Olá exemplo aplicação tooyour do IoT hub</span><span class="sxs-lookup"><span data-stu-id="08e2a-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="08e2a-125">Certifique-se de que está na pasta do repositório de Olá `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="08e2a-125">Make sure that you're in hello repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="08e2a-126">Abra a aplicação de exemplo de Olá no Visual Studio Code executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="08e2a-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="08e2a-127">Olá aviso `app.js` ficheiro Olá `app` subpasta.</span><span class="sxs-lookup"><span data-stu-id="08e2a-127">Notice hello `app.js` file in hello `app` subfolder.</span></span> <span data-ttu-id="08e2a-128">Olá `app.js` ficheiro é o ficheiro de origem da chave de Olá que contém mensagens hello do código toomonitor recebidos do hub IoT de Olá.</span><span class="sxs-lookup"><span data-stu-id="08e2a-128">hello `app.js` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="08e2a-129">Olá `blinkLED` Olá LED fica intermitente de função.</span><span class="sxs-lookup"><span data-stu-id="08e2a-129">hello `blinkLED` function blinks hello LED.</span></span>
   
   ![Estrutura de repositório na aplicação de exemplo de Olá](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="08e2a-131">Inicializar o ficheiro de configuração de Olá utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="08e2a-131">Initialize hello configuration file by using hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="08e2a-132">Se concluiu passos Olá [criar uma conta de armazenamento e de aplicação de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) neste computador, todas as configurações de Olá são herdadas, para que possa avançar toohello tarefas de implementação e execução de aplicação de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="08e2a-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="08e2a-133">Se concluiu passos Olá [criar uma conta de armazenamento e de aplicação de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) num computador diferente, terá de marcadores de posição do tooreplace Olá no Olá `config-raspberrypi.json` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="08e2a-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="08e2a-134">Olá `config-raspberrypi.json` ficheiro está a ser subpasta Olá da sua pasta raiz.</span><span class="sxs-lookup"><span data-stu-id="08e2a-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>
   
   ![Conteúdo do ficheiro de configuração raspberrypi.json Olá](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="08e2a-136">Substitua **[nome de anfitrião do dispositivo ou endereço IP]** com o endereço IP Olá do nome de anfitrião Pi ou Olá que obtém executando Olá `devdisco list --eth` comando.</span><span class="sxs-lookup"><span data-stu-id="08e2a-136">Replace **[device hostname or IP address]** with hello IP address of Pi or hello host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="08e2a-137">Substitua **[cadeia de ligação do dispositivo IoT]** pela cadeia de ligação de dispositivo Olá que obtém executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="08e2a-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="08e2a-138">Substitua **[cadeia de ligação do hub IoT]** com Olá cadeia de ligação do IoT hub que obtém executando Olá `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="08e2a-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="08e2a-139">Executar **gulp ferramentas de instalação** bem, se ainda não o fez, na Lesson 1.</span><span class="sxs-lookup"><span data-stu-id="08e2a-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="08e2a-140">Implementar e executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="08e2a-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="08e2a-141">Implementar e executar aplicações de exemplo de Olá em Pi executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="08e2a-141">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="08e2a-142">comando Olá implementa tooPi de aplicação de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="08e2a-142">hello command deploys hello sample application tooPi.</span></span> <span data-ttu-id="08e2a-143">Em seguida, executa aplicação Olá Pi e uma tarefa separada no anfitrião do computador toosend 20 blink mensagens tooPi do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08e2a-143">Then, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="08e2a-144">Após a execução da aplicação de exemplo de Olá, começa a escutar toomessages do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08e2a-144">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="08e2a-145">Entretanto, a tarefa de gulp Olá envia várias mensagens "blink" do seu tooPi de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="08e2a-145">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="08e2a-146">Para cada mensagem blink que recebe Pi, a aplicação de exemplo de Olá chama Olá `blinkLED` Olá de tooblink função LED.</span><span class="sxs-lookup"><span data-stu-id="08e2a-146">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="08e2a-147">Deverá ver blink LED Olá cada dois segundos como Olá gulp tarefa envia 20 mensagens do seu tooPi de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="08e2a-147">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="08e2a-148">Olá pela última vez um é uma mensagem "Parar" indicar Olá toostop de aplicação em execução.</span><span class="sxs-lookup"><span data-stu-id="08e2a-148">hello last one is a "stop" message that tells hello application toostop running.</span></span>

![Aplicação de exemplo com gulp comando e blink mensagens](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="08e2a-150">Resumo</span><span class="sxs-lookup"><span data-stu-id="08e2a-150">Summary</span></span>
<span data-ttu-id="08e2a-151">Que enviou com êxito as mensagens do seu Olá de tooblink tooPi LED do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08e2a-151">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="08e2a-152">tarefa seguinte Olá é opcional: altere Olá e desativar o comportamento de Olá LED.</span><span class="sxs-lookup"><span data-stu-id="08e2a-152">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08e2a-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="08e2a-153">Next steps</span></span>
[<span data-ttu-id="08e2a-154">Alterar Olá e desativar o comportamento de Olá LED</span><span class="sxs-lookup"><span data-stu-id="08e2a-154">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

