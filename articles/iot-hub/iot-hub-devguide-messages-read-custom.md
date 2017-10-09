---
title: pontos finais personalizados do aaaUnderstand IoT Hub do Azure | Microsoft Docs
description: Guia para programadores - utilizar encaminhamento regras pontos finais de toocustom de mensagens do dispositivo para nuvem tooroute.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>Utilizar rotas de mensagem e os pontos finais personalizados para mensagens do dispositivo-nuvem

IoT Hub permite-lhe tooroute [mensagens do dispositivo para nuvem] [ lnk-device-to-cloud] tooIoT Hub pontos finais de orientado para o serviço com base nas propriedades da mensagem. Encaminhamento conceder regras Olá flexibilidade toosend necessitam de mensagens onde têm toogo sem Olá para mensagens de tooprocess serviços adicionais ou códigos adicionais toowrite. Cada regra de encaminhamento que configura tem Olá seguintes propriedades:

| Propriedade      | Descrição |
| ------------- | ----------- |
| **Nome**      | Olá nome exclusivo que identifica a regra de Olá. |
| **Origem**    | origem de Olá dos dados de Olá transmitido em fluxo toobe alterada. Por exemplo, a telemetria do dispositivo. |
| **Condição** | expressão de consulta de Olá para a regra de encaminhamento de Olá que é executada no cabeçalhos e corpo de mensagem de saudação e utilizado toodetermine se se trata de uma correspondência para o ponto final de Olá. Para obter mais informações sobre a construção de uma condição de rota, consulte Olá [referência - linguagem de consulta para dispositivos duplos e tarefas][lnk-devguide-query-language]. |
| **Ponto final**  | nome do ponto final de olá onde o IoT Hub envia mensagens que correspondem à condição Olá Olá. Pontos finais devem estar no Olá mesma região que o IoT hub do Olá, caso contrário, poderá cobrada para escreve por várias regiões. |

Uma única mensagem pode correspondem à condição de Olá em várias regras de encaminhamento, na qual caso IoT Hub fornece o ponto final toohello de mensagem Olá associado a cada regra de correspondência. IoT Hub também automaticamente deduplicates entrega de mensagens, pelo que o se corresponder a uma mensagem de várias regras que têm todas Olá mesmo destino, que é apenas escrito toothat destino uma vez.

Um IoT hub tem uma predefinição [ponto final incorporado][lnk-built-in]. Pode criar os pontos finais personalizados tooroute mensagens tooby ligar outros serviços do seu hub de toohello de subscrição. IoT Hub suporta atualmente os Event Hubs, as filas do Service Bus e tópicos do Service Bus como pontos finais personalizados.

> [!WARNING]
> Filas do Service Bus e tópicos com **sessões** ou **duplicado deteção** ativado não são suportados como pontos finais personalizados.

Para obter mais informações sobre a criação de pontos finais personalizados no IoT Hub, consulte [pontos finais de IoT Hub][lnk-devguide-endpoints].

Para obter mais informações sobre a leitura do pontos finais personalizados, consulte:

* Ler a partir de [dos Event Hubs][lnk-getstarted-eh].
* Ler a partir de [filas do Service Bus][lnk-getstarted-queue].
* Ler a partir de [tópicos do Service Bus][lnk-getstarted-topic].

### <a name="next-steps"></a>Passos seguintes

Para mais informações sobre pontos finais de IoT Hub, consulte [pontos finais de IoT Hub][lnk-devguide-endpoints].

Para obter mais informações sobre a linguagem de consulta Olá utilizar regras de encaminhamento toodefine, consulte [idioma de consulta do IoT Hub para dispositivos duplos, tarefas e o encaminhamento de mensagens][lnk-devguide-query-language].

Olá [mensagens de dispositivo para a nuvem do IoT Hub do processo utilizar rotas] [ lnk-d2c-tutorial] tutorial mostra como regras de encaminhamento toouse e os pontos finais personalizados.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
