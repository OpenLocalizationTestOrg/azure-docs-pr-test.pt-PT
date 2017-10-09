---
title: aaaSimulated Raspberry Pi toocloud (Node.js) - ligar Raspberry Pi web simulador tooAzure IoT Hub | Microsoft Docs
description: Ligar Raspberry Pi web simulador tooAzure IoT Hub para Raspberry Pi toosend dados toohello em nuvem do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: raspberry pi simulador, azure raspberry pi, raspberry pi iot hub iot, raspberry pi enviar dados toocloud, raspberry pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="6f1bc-104">Ligar Raspberry Pi simulador online tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="6f1bc-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="6f1bc-105">Neste tutorial, comece por learning Olá Noções básicas de trabalhar com simulador online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="6f1bc-106">Em seguida, saiba como tooseamlessly estabelecer a ligação em nuvem do Olá Pi simulador toohello utilizando [IoT Hub do Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="6f1bc-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="6f1bc-107">Se tiver dispositivos físicos, visite [ligar Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="6f1bc-108">O que fazer</span><span class="sxs-lookup"><span data-stu-id="6f1bc-108">What you do</span></span>

* <span data-ttu-id="6f1bc-109">Saiba Olá Noções básicas do simulador online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="6f1bc-110">Crie um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-110">Create an IoT hub.</span></span>
* <span data-ttu-id="6f1bc-111">Registe um dispositivo para Pi no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="6f1bc-112">Execute um exemplo de aplicação no Pi toosend simulado sensor dados tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="6f1bc-113">Ligar simulado Raspberry Pi tooan IoT hub que criou.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="6f1bc-114">Em seguida, execute uma aplicação de exemplo com dados de sensores do Olá simulador toogenerate.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="6f1bc-115">Por fim, enviar Olá sensor dados tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6f1bc-116">O que irá aprender</span><span class="sxs-lookup"><span data-stu-id="6f1bc-116">What you learn</span></span>

* <span data-ttu-id="6f1bc-117">Como toocreate um hub IoT do Azure e obter a cadeia de ligação do novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="6f1bc-118">Se não tiver uma conta do Azure, [criar uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="6f1bc-119">Como toowork com simulador online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="6f1bc-120">Como toosend sensor dados tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="6f1bc-121">Descrição geral do simulador de web Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="6f1bc-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="6f1bc-122">Clique em simulador online do Olá botão toolaunch Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="6f1bc-123">Iniciar o simulador Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="6f1bc-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="6f1bc-124">Existem três áreas no simulador do Olá web.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-124">There are three areas in hello web simulator.</span></span>
* <span data-ttu-id="6f1bc-125">Área de assemblagem - circuito de predefinição Olá é que um Pi estabelece ligação com um sensor BME280 e um LED.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="6f1bc-126">área de Olá está bloqueada na versão de pré-visualização, por isso, atualmente não é possível efetuar a personalização.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="6f1bc-127">Codificação área - um editor de código online para toocode com Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="6f1bc-128">aplicação de exemplo Olá predefinida ajuda toocollect dados de sensores do BME280 sensor e envia tooyour IoT Hub do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="6f1bc-129">aplicação Olá é totalmente compatível com dispositivos de Pi reais.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-129">hello application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="6f1bc-130">Janela de consola integrada - Mostra saída Olá do seu código.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="6f1bc-131">Na parte superior de Olá desta janela, existem três botões.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="6f1bc-132">**Executar** -executar a aplicação de Olá no Olá codificação área.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="6f1bc-133">**Repor** -Olá de reposição de codificação área toohello predefinido exemplo de aplicação.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="6f1bc-134">**Expandir/subconjuntos de validação** - no Olá direita lado existe é um botão para que expanda/toofold Olá janela da consola.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="6f1bc-135">simulador de web de Raspberry Pi Olá está agora disponível numa versão de pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="6f1bc-136">Gostaríamos toohear sua voz no Olá [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="6f1bc-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="6f1bc-137">código de origem Olá é público no [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="6f1bc-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Descrição geral do simulador online Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="6f1bc-139">Execute um exemplo de aplicação no simulador do instalador de plataforma web</span><span class="sxs-lookup"><span data-stu-id="6f1bc-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="6f1bc-140">Na área de codificação, certifique-se de que está a trabalhar na aplicação de exemplo Olá predefinida.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="6f1bc-141">Substitua o marcador de posição de Olá na linha 15 por Olá cadeia de ligação de dispositivos do Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="6f1bc-142">![Substitua a cadeia de ligação do dispositivo Olá](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="6f1bc-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="6f1bc-143">Clique em **executar** ou tipo `npm start` aplicação de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="6f1bc-144">Deverá ver a saída de Olá seguinte que mostra os dados de sensores de Olá Olá mensagens e que são enviados tooyour IoT hub ![saída - dados de sensor enviados a partir do IoT hub tooyour Raspberry Pi](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="6f1bc-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="6f1bc-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6f1bc-145">Next steps</span></span>

<span data-ttu-id="6f1bc-146">Executar um dados de sensores de toocollect de aplicação de exemplo e enviá-lo tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6f1bc-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
