---
title: "IoT Hub do Azure - introdução ao ligar a nuvem de toohello de dispositivos de IoT | Microsoft Docs"
description: Saiba como tooconnect sua quadros de IoT e arranque kits tooAzure IoT Hub. Os seus dispositivos podem enviar telemetria tooIoT Hub IoT Hub pode monitorizar e gerir os seus dispositivos.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: tutorial de hub iot do Azure
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="3901f-105">Azure IoT Hub introdução tutoriais</span><span class="sxs-lookup"><span data-stu-id="3901f-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="3901f-106">Pode utilizar o IoT Hub do Azure e Olá IoT do Azure SDKs toobuild Internet das coisas (IoT) as soluções de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="3901f-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="3901f-107">IoT Hub do Azure é um serviço completamente gerido na nuvem de Olá que estabelece ligação com segurança, monitoriza e gere os dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="3901f-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="3901f-108">Utilize Olá SDKs de dispositivos IoT do Azure tooimplement os dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="3901f-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="3901f-109">Utilize um gateway de IoT cenários mais complexos de IoT.</span><span class="sxs-lookup"><span data-stu-id="3901f-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="3901f-110">Por exemplo, onde tem de tooconsider fatores, tais como dispositivos legados, os custos de largura de banda, políticas de segurança e privacidade ou processamento de dados de limite.</span><span class="sxs-lookup"><span data-stu-id="3901f-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="3901f-111">Estes cenários, utiliza o Azure IoT Edge tooimplement um gateway que liga o IoT hub tooyour dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3901f-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="3901f-112">O que abrangem os tutoriais Olá</span><span class="sxs-lookup"><span data-stu-id="3901f-112">What hello tutorials cover</span></span>

<span data-ttu-id="3901f-113">Estes tutoriais introduzem tooAzure IoT Hub e SDKs do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="3901f-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="3901f-114">tutoriais Olá abrangem IoT cenários toodemonstrate Olá capacidades comuns do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3901f-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="3901f-115">Olá tutoriais também ilustram como toocombine IoT Hub com outro Azure serviços e ferramentas toobuild mais poderosas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="3901f-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="3901f-116">Nos tutoriais Olá, pode escolher toouse simulados ou reais dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="3901f-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="3901f-117">Além disso, pode saber como toouse um gateway tooenable dispositivos tooconnect tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3901f-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="3901f-118">Configurar o dispositivo</span><span class="sxs-lookup"><span data-stu-id="3901f-118">Set up your device</span></span>

<span data-ttu-id="3901f-119">Ligar um tooAzure de dispositivo ou gateway do IoT IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3901f-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="3901f-120">Pode escolher tooget um dispositivo físico ou simulado iniciado:</span><span class="sxs-lookup"><span data-stu-id="3901f-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="3901f-121">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="3901f-121">IoT device</span></span>                       | <span data-ttu-id="3901f-122">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="3901f-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="3901f-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="3901f-123">Raspberry Pi</span></span>                     | <span data-ttu-id="3901f-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="3901f-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="3901f-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="3901f-125">IoT DevKit</span></span>                       | <span data-ttu-id="3901f-126">[Arduino no VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="3901f-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="3901f-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="3901f-127">Intel Edison</span></span>                     | <span data-ttu-id="3901f-128">[NODE.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="3901f-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="3901f-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="3901f-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="3901f-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="3901f-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="3901f-131">Sparkfun ESP8266 coisa Dev</span><span class="sxs-lookup"><span data-stu-id="3901f-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="3901f-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="3901f-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="3901f-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="3901f-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="3901f-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="3901f-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="3901f-135">Dispositivo simulado no PC</span><span class="sxs-lookup"><span data-stu-id="3901f-135">Simulated device on PC</span></span>           | <span data-ttu-id="3901f-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="3901f-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="3901f-137">Simulador de dispositivo online</span><span class="sxs-lookup"><span data-stu-id="3901f-137">Online device simulator</span></span>         | <span data-ttu-id="3901f-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="3901f-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="3901f-139">Além disso, pode utilizar um limite de IoT gateway tooenable dispositivos tooconnect tooyour IoT hub:</span><span class="sxs-lookup"><span data-stu-id="3901f-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="3901f-140">Dispositivo de gateway</span><span class="sxs-lookup"><span data-stu-id="3901f-140">Gateway device</span></span>               | <span data-ttu-id="3901f-141">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="3901f-141">Programming language</span></span> | <span data-ttu-id="3901f-142">Plataforma</span><span class="sxs-lookup"><span data-stu-id="3901f-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="3901f-143">Intel NUC (modelo DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="3901f-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="3901f-144">C</span><span class="sxs-lookup"><span data-stu-id="3901f-144">C</span></span>                    | <span data-ttu-id="3901f-145">[Vento River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="3901f-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="3901f-146">Gateway simulada</span><span class="sxs-lookup"><span data-stu-id="3901f-146">Simulated gateway</span></span>            | <span data-ttu-id="3901f-147">C</span><span class="sxs-lookup"><span data-stu-id="3901f-147">C</span></span>                    | <span data-ttu-id="3901f-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="3901f-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
