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
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="2762c-105">Criar e implementar a aplicação de blink Olá</span><span class="sxs-lookup"><span data-stu-id="2762c-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="2762c-106">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="2762c-106">What you will do</span></span>
<span data-ttu-id="2762c-107">Clone Olá exemplo Arduino de aplicação a partir do GitHub e utilizar Olá gulp ferramenta toodeploy Olá exemplo aplicação tooyour Adafruit Feather M0 Wi-Fi Arduino quadro.</span><span class="sxs-lookup"><span data-stu-id="2762c-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="2762c-108">Olá exemplo aplicação fica intermitente Olá GPIO #13 barod GUIADO cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="2762c-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="2762c-109">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="2762c-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2762c-110">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="2762c-110">What you will learn</span></span>
* <span data-ttu-id="2762c-111">Como toodeploy e execução Olá aplicação de exemplo no seu painel Arduino.</span><span class="sxs-lookup"><span data-stu-id="2762c-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2762c-112">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="2762c-112">What you need</span></span>
<span data-ttu-id="2762c-113">Tem concluiu com sucesso Olá seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="2762c-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="2762c-114">[Configurar o dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="2762c-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="2762c-115">[Obtenha as ferramentas de Olá][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="2762c-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="2762c-116">Aplicação de exemplo de Olá aberta</span><span class="sxs-lookup"><span data-stu-id="2762c-116">Open hello sample application</span></span>
<span data-ttu-id="2762c-117">Olá tooopen aplicação de exemplo, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="2762c-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="2762c-118">Clone o repositório de exemplo de Olá a partir do GitHub executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2762c-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="2762c-119">Abra a aplicação de exemplo de Olá no Visual Studio Code executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2762c-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

<span data-ttu-id="2762c-121">Olá `app.ino` ficheiro Olá `app` subpasta é o ficheiro de origem da chave de Olá que contém Olá código toocontrol Olá LED.</span><span class="sxs-lookup"><span data-stu-id="2762c-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="2762c-122">Instale as dependências da aplicação</span><span class="sxs-lookup"><span data-stu-id="2762c-122">Install application dependencies</span></span>
<span data-ttu-id="2762c-123">Instale as bibliotecas de Olá e outros módulos que precisa para a aplicação de exemplo de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2762c-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="2762c-124">Configurar a ligação ao dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="2762c-124">Configure hello device connection</span></span>
<span data-ttu-id="2762c-125">tooconfigure Olá ligação do dispositivo, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="2762c-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="2762c-126">Obter a porta série de Olá do dispositivo Olá com a cli de deteção de dispositivo Olá:</span><span class="sxs-lookup"><span data-stu-id="2762c-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="2762c-127">Deverá ver um resultado que é semelhante toohello seguinte e encontrar Olá usb porta COM para a sua placa Arduino: ![deteção de dispositivos][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="2762c-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="2762c-128">Ficheiro aberto Olá `config.json` no Olá pasta lesson e adicionar valor Olá Olá encontrar o número da porta COM:</span><span class="sxs-lookup"><span data-stu-id="2762c-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config][config-json]
   > [!NOTE]
   > <span data-ttu-id="2762c-130">Para a porta de Olá COM, na plataforma do Windows, tem um formato de Olá `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="2762c-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="2762c-131">No macOS ou Ubuntu, começa com `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="2762c-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="2762c-132">Implementar e executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="2762c-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="2762c-133">Instalar as ferramentas de Olá necessário para a placa de Arduino</span><span class="sxs-lookup"><span data-stu-id="2762c-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="2762c-134">Instale Olá SDK do Hub IoT do Azure para a placa de Arduino executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2762c-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="2762c-135">Esta tarefa pode demorar um toocomplete muito tempo, dependendo da sua ligação de rede.</span><span class="sxs-lookup"><span data-stu-id="2762c-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="2762c-136">Saia Olá executar a instância de Arduino IDE quando executar tarefas gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="2762c-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="2762c-137">Implementar e executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="2762c-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="2762c-138">Implementar e executar a aplicação de exemplo de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2762c-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="2762c-139">Verificar Olá aplicação funciona</span><span class="sxs-lookup"><span data-stu-id="2762c-139">Verify hello app works</span></span>
<span data-ttu-id="2762c-140">Se não vir Olá LED blinking, consulte Olá [guia de resolução de problemas] [ troubleshooting-page] para problemas de toocommon soluções.</span><span class="sxs-lookup"><span data-stu-id="2762c-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![LED blinking][led-blinking]

## <a name="summary"></a><span data-ttu-id="2762c-142">Resumo</span><span class="sxs-lookup"><span data-stu-id="2762c-142">Summary</span></span>
<span data-ttu-id="2762c-143">Ter instalado Olá necessário ferramentas toowork com o seu painel Arduino e implementados um Olá de tooblink quadro do exemplo aplicação tooyour Arduino LED.</span><span class="sxs-lookup"><span data-stu-id="2762c-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="2762c-144">Agora pode criar, implementar e executar outra aplicação de exemplo que se liga a tooAzure de placa de Arduino toosend do IoT Hub e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="2762c-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2762c-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2762c-145">Next steps</span></span>
<span data-ttu-id="2762c-146">[Obter Olá ferramentas do Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="2762c-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md