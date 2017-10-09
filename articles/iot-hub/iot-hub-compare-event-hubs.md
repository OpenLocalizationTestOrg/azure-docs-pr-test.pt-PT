---
title: aaaCompare IoT Hub do Azure tooAzure Event Hubs | Microsoft Docs
description: "Uma comparação Olá IoT Hub do Azure Hubs de eventos dos serviços de e realce diferenças funcionais e casos de utilização. comparação de Olá inclui protocolos suportados, gestão de dispositivos, monitorização, e carrega o ficheiro."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Comparação do IoT Hub do Azure e Event Hubs do Azure
Um dos casos de utilização principal Olá do IoT Hub é toogather telemetria dos dispositivos. Por este motivo, o IoT Hub, muitas vezes, é comparado demasiado[Event Hubs do Azure][Azure Event Hubs]. Como o IoT Hub, os Event Hubs são um serviço que permite a entrada de telemetria e eventos de processamento de eventos toohello nuvem em grande escala, com baixa latência e alta fiabilidade.

No entanto, os serviços de Olá tem várias diferenças são detalhadas no Olá a tabela seguinte:

| Área | IoT Hub | Event Hubs |
| --- | --- | --- |
| Padrões de comunicação | Permite [comunicações de dispositivo para nuvem] [ lnk-d2c-guidance] (mensagens de ficheiro carregamentos e propriedades comunicadas) e [comunicações de nuvem para o dispositivo] [ lnk-c2d-guidance] (diretos métodos, propriedades pretendidas, messaging). |Permite apenas a entrada de eventos (normalmente considerada para cenários de dispositivo para a nuvem). |
| Informações de estado do dispositivo | [Dispositivos duplos] [ lnk-twins] pode armazenar e consultar as informações de estado do dispositivo. | Não existem informações de estado do dispositivo podem ser armazenadas. |
| Suporte de protocolos de dispositivo |Suporta MQTT, MQTT através de WebSockets, AMQP, AMQP através de WebSockets e HTTP. Além disso, o IoT Hub funciona com Olá [gateway de protocolo do Azure IoT][lnk-azure-protocol-gateway], um protocolo personalizável gateway implementação toosupport protocolos personalizados. |Suporta AMQP, AMQP através de WebSockets e HTTP. |
| Segurança |Fornece identidade por dispositivo e controlo de acesso revocable. Consulte Olá [secção de segurança de Olá guia para programadores do IoT Hub]. |Fornece ao nível do Event Hubs [partilhado políticas de acesso][Event Hubs - security], com revogação limitada suportam através de [políticas do publicador][Event Hubs publisher policies]. Soluções de IoT são frequentemente credenciais tooimplement necessário uma solução personalizada toosupport por dispositivo e medidas de spoofing de antimalware. |
| Monitorização de operações |Permite que o IoT soluções toosubscribe tooa conjunto avançado de identidade gestão e a conectividade de eventos do dispositivo, como erros de autenticação de dispositivo individual, limitação e exceções de formato incorreto. Estes eventos permitem-lhe tooquickly identificar problemas de conectividade ao nível do Olá dispositivo individual. |Expõe apenas agregadas métricas. |
| Escala |É otimizada toosupport milhões de dispositivos ligados em simultâneo. |Medidores Olá ligações como por [quotas de Event Hubs do Azure][Azure Event Hubs quotas]. No Olá por outro lado, os Event Hubs permitem partição de Olá toospecify para cada mensagem enviada. |
| SDKs do dispositivo |Fornece [SDKs do dispositivo] [ Azure IoT SDKs] para uma grande variedade de plataformas e idiomas, em adição toodirect MQTT, AMQP e HTTP APIs. |É suportado no .NET, Java e C, adição tooAMQP e interfaces de envio HTTP. |
| Carregamento de ficheiros |Permite que os ficheiros de tooupload do IoT soluções de nuvem de toohello de dispositivos. Inclui um ponto final da notificação ficheiro para a integração de fluxo de trabalho e a uma categoria para suporte de depuração de monitorização de operações. | Não é suportado. |
| Pontos finais de toomultiple de mensagens de rota | Cópia de segurança too10 pontos finais personalizados são suportados. As regras determinam como as mensagens são pontos finais de toocustom encaminhadas. Para obter mais informações, consulte [enviar e receber mensagens com o IoT Hub][lnk-devguide-messaging]. | Requer toobe adicionais de código escrito e alojados para emissão de mensagem. |

Em resumo, mesmo que esteja Olá caso de utilização única entrada de telemetria do dispositivo para a nuvem, o IoT Hub fornece um serviço que foi concebido para conectividade de dispositivos de IoT. Continua propostas de valor de Olá tooexpand nestes cenários com funcionalidades específicas do IoT. Hubs de eventos foi concebida para entrada de evento em grande escala, ambos no contexto de Olá dos cenários de centro de dados inter- e intra-datacenter.

Não é toouse invulgar IoT Hub e Event Hubs no Olá mesma solução. IoT Hub processa a comunicação do dispositivo para a nuvem de Olá e Event Hubs processa a entrada de evento de fase posterior para motores de processamento em tempo real.

### <a name="next-steps"></a>Passos seguintes
toolearn mais sobre o planeamento da sua implementação do IoT Hub, consulte [dimensionamento, HA e DR][lnk-scaling].

toofurther explorar Olá das capacidades do IoT Hub, consulte:

* [Guia para programadores do IoT Hub][lnk-devguide]
* [Simulando um dispositivo com o limite de IoT][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[secção de segurança de Olá guia para programadores do IoT Hub]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
