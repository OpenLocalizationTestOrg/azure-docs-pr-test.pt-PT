---
title: "aaaAzure comunicação do IoT Hub protocolos e portas | Microsoft Docs"
description: "Guia para programadores - descreve Olá suportado protocolos de comunicação para as comunicações de dispositivo para nuvem e da nuvem para o dispositivo e números de porta de Olá que tem de estar abertos."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# Referenciar - escolher um protocolo de comunicação

IoT Hub permite dispositivos toouse [MQTT][lnk-mqtt], MQTT através de WebSockets, [AMQP][lnk-amqp], protocolos AMQP através de WebSockets e HTTP para o lado do dispositivo comunicações. Para obter informações sobre como é que estes protocolos suportam funcionalidades específicas do IoT Hub, consulte [documentação de orientação do dispositivo para nuvem comunicações] [ lnk-d2c-guidance] e [orientações de comunicações da nuvem para o dispositivo] [lnk-c2d-guidance].

Olá tabela seguinte fornece recomendações alto nível Olá para à sua escolha de protocolo:

| Protocolo | Quando deve escolher este protocolo |
| --- | --- |
| MQTT <br> MQTT através de WebSocket |Utilizar em todos os dispositivos que não necessitam de tooconnect vários dispositivos (cada um com as suas próprias credenciais por dispositivo) ao longo de Olá mesma ligação TLS. |
| AMQP <br> AMQP através de WebSocket |Utilizar no campo e nuvem gateways tootake das vantagens da ligação de multiplexação em todos os dispositivos. |
| HTTP |Utilize para dispositivos que não é possível suportar outros protocolos. |

Considere Olá seguintes pontos ao escolher o protocolo para as comunicações do lado do dispositivo:

* **Padrão de nuvem para o dispositivo**. HTTP não tem um push de servidor de tooimplement de forma eficiente. Como tal, quando estiver a utilizar HTTP, os dispositivos consultam o IoT Hub para mensagens da nuvem para o dispositivo. Esta abordagem é ineficaz para Olá dispositivo e do IoT Hub. Em diretrizes HTTP atuais, cada dispositivo deve consultar mensagens cada 25 minutos ou mais. No Olá por outro lado, MQTT e AMQP suportam push de servidor ao receber mensagens da nuvem para o dispositivo. Ativar a pushes imediatas de mensagens do dispositivo de toohello do IoT Hub. Se a latência de entrega for uma preocupação, MQTT ou AMQP são Olá melhor toouse de protocolos. Para dispositivos ligados raramente, HTTP funciona bem.
* **Campo gateways**. Ao utilizar MQTT e HTTP, não é possível ligar vários dispositivos (cada um com as suas próprias credenciais por dispositivo) utilizando Olá a mesma ligação TLS. Assim, para [cenários de gateway de campo][lnk-azure-gateway-guidance], estes protocolos são inferior ao ideal – pois requerem que um TLS ligação entre o gateway de campo Olá e IoT Hub para o gateway de campo cada dispositivo ligado toohello.
* **Dispositivos de recursos de baixa**. Olá MQTT e bibliotecas HTTP têm um menores requisitos de espaço que bibliotecas AMQP Olá. Como tal, se hello dispositivo limitou recursos (por exemplo, menor que 1 MB de RAM), estes protocolos podem Olá única implementação de protocolo disponível.
* **Rede transversal**. protocolo AMQP padrão do Olá utiliza a porta 5671, enquanto MQTT escuta na porta 8883, que pode provocar problemas em redes que são protocolos HTTP toonon fechado. MQTT através de WebSockets, AMQP através de WebSockets e HTTP estão disponível toobe utilizada neste cenário.
* **Tamanho do payload**. MQTT e AMQP são protocolos binários, que resultam em mais compacta payloads de HTTP.

> [!WARNING]
> Quando utilizar HTTP, cada dispositivo deve consultar mensagens da nuvem para o dispositivo de cada 25 minutos ou mais. No entanto, durante o desenvolvimento, é aceitável toopoll mais frequentemente do que a cada 25 minutos.

## Números de porta

Dispositivos podem comunicar com o IoT Hub no Azure utilizando vários protocolos. Normalmente, escolha Olá do protocolo está condicionada pelos requisitos específicos de Olá da solução de Olá. Olá tabela seguinte apresenta uma lista de portas de saída Olá que tem de estar abertas para um protocolo específico um dispositivo toobe capaz de toouse:

| Protocolo | Porta |
| --- | --- |
| MQTT |8883 |
| MQTT através de WebSockets |443 |
| AMQP |5671 |
| AMQP através de WebSockets |443 |
| HTTP |443 |

Assim que tiver criado um IoT hub na região do Azure, hello mantém do IoT hub hello mesmo endereço IP para duração Olá do que o IoT hub. No entanto, toomaintain qualidade do serviço, se o Microsoft move Olá IoT hub tooa diferentes a unidade de escala, em seguida, que é atribuída um novo endereço IP.


## Passos seguintes

toolearn mais informações sobre como o IoT Hub implementa o protocolo MQTT Olá, consulte [Communicate com o IoT hub com o protocolo MQTT Olá][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
