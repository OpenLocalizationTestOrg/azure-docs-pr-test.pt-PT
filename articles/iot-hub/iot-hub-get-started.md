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
# <a name="azure-iot-hub-get-started-tutorials"></a>Azure IoT Hub introdução tutoriais

Pode utilizar o IoT Hub do Azure e Olá IoT do Azure SDKs toobuild Internet das coisas (IoT) as soluções de dispositivos:

* IoT Hub do Azure é um serviço completamente gerido na nuvem de Olá que estabelece ligação com segurança, monitoriza e gere os dispositivos de IoT. Utilize Olá SDKs de dispositivos IoT do Azure tooimplement os dispositivos de IoT.
* Utilize um gateway de IoT cenários mais complexos de IoT. Por exemplo, onde tem de tooconsider fatores, tais como dispositivos legados, os custos de largura de banda, políticas de segurança e privacidade ou processamento de dados de limite. Estes cenários, utiliza o Azure IoT Edge tooimplement um gateway que liga o IoT hub tooyour dispositivos.

## <a name="what-hello-tutorials-cover"></a>O que abrangem os tutoriais Olá

Estes tutoriais introduzem tooAzure IoT Hub e SDKs do dispositivo Olá. tutoriais Olá abrangem IoT cenários toodemonstrate Olá capacidades comuns do IoT Hub. Olá tutoriais também ilustram como toocombine IoT Hub com outro Azure serviços e ferramentas toobuild mais poderosas soluções de IoT. Nos tutoriais Olá, pode escolher toouse simulados ou reais dispositivos de IoT. Além disso, pode saber como toouse um gateway tooenable dispositivos tooconnect tooyour do IoT hub.

## <a name="set-up-your-device"></a>Configurar o dispositivo

Ligar um tooAzure de dispositivo ou gateway do IoT IoT Hub. Pode escolher tooget um dispositivo físico ou simulado iniciado:

| Dispositivo IoT                       | Linguagem de programação |
|----------------------------------|----------------------|
| Raspberry Pi                     | [Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]  |
| IoT DevKit                       | [Arduino no VSCode][DevKit]     |
| Intel Edison                     | [NODE.js][Ed_Nd], [C][Ed_C]    |
| Adafruit Feather HUZZAH ESP8266  | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 coisa Dev       | [Arduino][Th_Ard]              |
| Adafruit Feather M0              | [Arduino][M0_Ard]              |
| Dispositivo simulado no PC           | [.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth] |
| Simulador de dispositivo online         | [Raspberry Pi (Node.js)][Ol_Sim] |

Além disso, pode utilizar um limite de IoT gateway tooenable dispositivos tooconnect tooyour IoT hub:

| Dispositivo de gateway               | Linguagem de programação | Plataforma         |
|------------------------------|----------------------|------------------|
| Intel NUC (modelo DE3815TYKE) | C                    | [Vento River Linux][NUC_Lnx] |
| Gateway simulada            | C                    | [Linux][Sim_Lnx], [Windows][Sim_Win] |

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
