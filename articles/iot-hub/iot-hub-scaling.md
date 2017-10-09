---
title: dimensionamento do aaaAzure IoT Hub | Microsoft Docs
description: "Como tooscale sua toosupport de hub IoT o débito de mensagem previsto. Inclui um resumo das opções de fragmentação e débito Olá suportado para cada camada."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>Dimensionar a sua solução de hub IoT
IoT Hub do Azure pode suportar dispositivos ligados em simultâneo milhões de tooa. Para obter mais informações, consulte [IoT Hub preços][lnk-pricing]. Cada unidade de IoT Hub permite que um determinado número de mensagens diárias.

tooproperly dimensionar a sua solução, considere a utilização do IoT Hub específica. Em particular, considere o débito de pico Olá necessário para Olá seguintes categorias de operações:

* Mensagens do dispositivo para a cloud
* Mensagens da nuvem para dispositivo
* Operações de registo de identidade

Informações de débito toothis de adição, consulte [quotas do IoT Hub e limitações] [ IoT Hub quotas and throttles] e estruturar a solução em conformidade.

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>Débito de mensagens do dispositivo para nuvem e da nuvem para o dispositivo
Olá melhor forma toosize uma solução de IoT Hub é o tráfego de Olá tooevaluate numa base por unidade.

Mensagens do dispositivo para nuvem siga estas diretrizes de débito constante.

| Escalão | Débito constante | Velocidade de envio constante |
| --- | --- | --- |
| S1 |Cópia de segurança too1111 KB por minuto por unidade<br/>(1,5 GB/dia/unidade) |Média de mensagens por minuto 278 por unidade<br/>(um máximo de 400.000 mensagens diário por unidade) |
| S2 |Cópia de segurança too16 MB por minuto por unidade<br/>(22.8 GB/dia/unidade) |Média de mensagens por minuto 4,167 por unidade<br/>(milhões de 6 mensagens diário por unidade) |
| S3 |Cópia de segurança too814 MB por minuto por unidade<br/>(1144.4 GB/dia/unidade) |Média de mensagens por minuto 208,333 por unidade<br/>(milhões de 300 mensagens diário por unidade) |

## <a name="identity-registry-operation-throughput"></a>Débito de operação de registo de identidade
Operações de registo de identidade do IoT Hub não são supostas toobe operações de tempo de execução, conforme forem principalmente relacionada toodevice aprovisionamento.

Para números de desempenho de rajada específicos, consulte [quotas do IoT Hub e limitações][IoT Hub quotas and throttles].

## <a name="sharding"></a>Fragmentação
Embora um único IoT hub pode dimensionar toomillions dos dispositivos, por vezes, a solução requer características de desempenho específica que não pode garantir que um único IoT hub. Nesse caso, é recomendado que partição os seus dispositivos para vários os hubs IoT. Vários aos hubs IoT uniforme bursts de tráfego e obter débito necessário Olá ou taxas de operação que são necessárias.

## <a name="next-steps"></a>Passos seguintes
toofurther explorar Olá das capacidades do IoT Hub, consulte:

* [Guia para programadores do IoT Hub][lnk-devguide]
* [Simulando um dispositivo com o Azure IoT Edge][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
