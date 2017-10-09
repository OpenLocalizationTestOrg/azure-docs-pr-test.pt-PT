---
title: "Introdução ao ligar a dispositivos físicos tooAzure IoT Hub | Microsoft Docs"
description: "Saiba como tooconnect físico dispositivos e quadros tooAzure IoT Hub. Os seus dispositivos podem enviar telemetria tooIoT Hub IoT Hub pode monitorizar e gerir os seus dispositivos."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: tutorial de hub iot do Azure
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 47ce289c438b2f495d499d724c38ddc4b3307425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="577e7-105">Introdução ao IoT Hub do Azure tutoriais de dispositivos físicos</span><span class="sxs-lookup"><span data-stu-id="577e7-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="577e7-106">Estes tutoriais introduzem tooAzure IoT Hub e SDKs do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="577e7-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="577e7-107">tutoriais Olá abrangem IoT cenários toodemonstrate Olá capacidades comuns do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="577e7-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="577e7-108">Olá tutoriais também ilustram como toocombine IoT Hub com outro Azure serviços e ferramentas toobuild mais poderosas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="577e7-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="577e7-109">Olá tutoriais listados no Olá seguintes Mostrar tabela, como dispositivos de IoT físicos toocreate.</span><span class="sxs-lookup"><span data-stu-id="577e7-109">hello tutorials listed in hello following table show you how toocreate physical IoT devices.</span></span>

| <span data-ttu-id="577e7-110">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="577e7-110">IoT device</span></span>                       | <span data-ttu-id="577e7-111">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="577e7-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="577e7-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="577e7-112">Raspberry Pi</span></span>                    | <span data-ttu-id="577e7-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="577e7-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="577e7-114">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="577e7-114">IoT DevKit</span></span>                      | <span data-ttu-id="577e7-115">[Arduino no VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="577e7-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="577e7-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="577e7-116">Intel Edison</span></span>                    | <span data-ttu-id="577e7-117">[NODE.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="577e7-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="577e7-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="577e7-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="577e7-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="577e7-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="577e7-120">Sparkfun ESP8266 coisa Dev</span><span class="sxs-lookup"><span data-stu-id="577e7-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="577e7-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="577e7-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="577e7-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="577e7-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="577e7-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="577e7-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="577e7-124">Além disso, pode utilizar um limite de IoT gateway tooenable dispositivos tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="577e7-124">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="577e7-125">Dispositivo de gateway</span><span class="sxs-lookup"><span data-stu-id="577e7-125">Gateway device</span></span>               | <span data-ttu-id="577e7-126">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="577e7-126">Programming language</span></span> | <span data-ttu-id="577e7-127">Plataforma</span><span class="sxs-lookup"><span data-stu-id="577e7-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="577e7-128">Intel NUC (modelo DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="577e7-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="577e7-129">C</span><span class="sxs-lookup"><span data-stu-id="577e7-129">C</span></span>                    | <span data-ttu-id="577e7-130">[Vento River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="577e7-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
