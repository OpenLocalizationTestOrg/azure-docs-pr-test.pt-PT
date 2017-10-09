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
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="5b212-104">Executar um toosend de aplicação de exemplo mensagens do dispositivo-nuvem</span><span class="sxs-lookup"><span data-stu-id="5b212-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5b212-105">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="5b212-105">What you will do</span></span>
<span data-ttu-id="5b212-106">Este artigo irá mostrar como toodeploy e execute um exemplo de aplicação no seu Adafruit Feather M0 Wi-Fi Arduino quadro que envia mensagens tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5b212-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="5b212-107">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5b212-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5b212-108">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="5b212-108">What you will learn</span></span>
<span data-ttu-id="5b212-109">Ficará a saber como toouse Olá gulp toodeploy ferramenta e execute a aplicação de Arduino de exemplo de Olá no seu painel Arduino.</span><span class="sxs-lookup"><span data-stu-id="5b212-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5b212-110">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="5b212-110">What you need</span></span>
* <span data-ttu-id="5b212-111">Antes de começar esta tarefa, deve concluiu com sucesso [criar uma aplicação de função do Azure e um armazenamento conta tooprocess e arquivo IoT hub mensagens][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="5b212-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="5b212-112">Obter as cadeias de ligação do IoT hub e dispositivos</span><span class="sxs-lookup"><span data-stu-id="5b212-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="5b212-113">Olá, a cadeia de ligação do dispositivo é utilizado tooconnect Arduino quadro tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b212-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="5b212-114">cadeia de ligação do Olá IoT hub é utilizado tooconnect a sua identidade dispositivos do IoT hub toohello que representa o Arduino quadro no hub IoT de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b212-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="5b212-115">Lista todos os os IoT hubs no seu grupo de recursos, executando Olá os seguintes comandos da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="5b212-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="5b212-116">Utilize `iot-sample` como valor Olá `{resource group name}` se não alterar o valor de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b212-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="5b212-117">Obter a cadeia de ligação do Olá IoT hub executando o seguinte comando da CLI do Azure de Olá:</span><span class="sxs-lookup"><span data-stu-id="5b212-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="5b212-118">`{my hub name}`é o nome de Olá que especificou quando criou o seu hub IoT e registado o seu painel Arduino.</span><span class="sxs-lookup"><span data-stu-id="5b212-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="5b212-119">Obter a cadeia de ligação do dispositivo Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5b212-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="5b212-120">Utilize `mym0wifi` como valor Olá `{device id}` se não alterar o valor de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b212-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="5b212-121">Configurar a ligação ao dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5b212-121">Configure hello device connection</span></span>
<span data-ttu-id="5b212-122">tooconfigure Olá ligação do dispositivo, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="5b212-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="5b212-123">Obter a porta série de Olá do dispositivo Olá com a cli de deteção de dispositivo Olá:</span><span class="sxs-lookup"><span data-stu-id="5b212-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="5b212-124">Deverá ver um resultado que é semelhante toohello seguinte e encontrar Olá usb porta COM para a sua placa Arduino:</span><span class="sxs-lookup"><span data-stu-id="5b212-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Deteção de dispositivos][device-discovery]

2. <span data-ttu-id="5b212-126">Ficheiro aberto Olá `config.json` no Olá pasta lesson e adicionar valor Olá Olá encontrar o número da porta COM:</span><span class="sxs-lookup"><span data-stu-id="5b212-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config][config-json]

   > [!NOTE]
   > <span data-ttu-id="5b212-128">Para a porta de Olá COM, na plataforma do Windows, tem um formato de Olá `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="5b212-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="5b212-129">No macOS ou Ubuntu, começa com `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="5b212-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="5b212-130">Inicializar o ficheiro de configuração de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5b212-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="5b212-131">Ficheiro de configuração de dispositivo Olá abra `config-arduino.json` no Visual Studio Code executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5b212-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![configuração arduino.json][config-arduino-json]

5. <span data-ttu-id="5b212-133">Tornar Olá seguir substituições no Olá `config-arduino.json` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="5b212-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="5b212-134">Substitua **[Wi-Fi SSID]** com o SSID de Wi-Fi ligado toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="5b212-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="5b212-135">Substitua **[Wi-Fi palavra-passe]** com a palavra-passe de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="5b212-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="5b212-136">Remova a cadeia de Olá se Wi-Fi não necessita de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="5b212-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="5b212-137">Substitua **[cadeia de ligação do dispositivo IoT]** com Olá `device connection string` obtido.</span><span class="sxs-lookup"><span data-stu-id="5b212-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="5b212-138">Substitua **[cadeia de ligação do hub IoT]** com Olá `iot hub connection string` obtido.</span><span class="sxs-lookup"><span data-stu-id="5b212-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5b212-139">Não precisa de `azure_storage_connection_string` neste artigo.</span><span class="sxs-lookup"><span data-stu-id="5b212-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="5b212-140">Mantenha-lo tal como está.</span><span class="sxs-lookup"><span data-stu-id="5b212-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="5b212-141">Implementar e executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="5b212-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="5b212-142">Implementar e executar aplicações de exemplo de Olá no seu painel Arduino executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5b212-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="5b212-143">Olá predefinido gulp tarefa é executada `install-tools` e `run` tarefas sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="5b212-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="5b212-144">Quando lhe [implementado Olá blink aplicação][deployed-the-blink-app], executou estas tarefas separadamente.</span><span class="sxs-lookup"><span data-stu-id="5b212-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="5b212-145">Certifique-se de que a aplicação de exemplo de Olá funciona</span><span class="sxs-lookup"><span data-stu-id="5b212-145">Verify that hello sample application works</span></span>
<span data-ttu-id="5b212-146">Deverá ver Olá GPIO #0 blinking de LED uma cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="5b212-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="5b212-147">Sempre que fica intermitente Olá LED, a aplicação de exemplo de Olá envia uma mensagem tooyour do IoT hub e verifica que essa mensagem de saudação tenha enviada com êxito tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5b212-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="5b212-148">Além disso, cada mensagem recebida pelo IoT hub do Olá está impresso na janela de consola Olá.</span><span class="sxs-lookup"><span data-stu-id="5b212-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="5b212-149">aplicação de exemplo de Olá automaticamente termina após 20 mensagens a enviar.</span><span class="sxs-lookup"><span data-stu-id="5b212-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![Aplicação de exemplo com enviadas e recebidas mensagens][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="5b212-151">Resumo</span><span class="sxs-lookup"><span data-stu-id="5b212-151">Summary</span></span>
<span data-ttu-id="5b212-152">Tiver implementado e execute Olá novo blink exemplo de aplicação no seu IoT hub do Arduino quadro toosend mensagens do dispositivo para nuvem tooyour.</span><span class="sxs-lookup"><span data-stu-id="5b212-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="5b212-153">Agora a monitorizar as mensagens que são escritos toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5b212-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b212-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5b212-154">Next steps</span></span>
<span data-ttu-id="5b212-155">[Mensagens de leitura continuada no armazenamento do Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="5b212-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md