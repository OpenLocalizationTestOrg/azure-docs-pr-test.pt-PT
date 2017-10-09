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
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="233f9-103">Utilizar rotas de mensagem e os pontos finais personalizados para mensagens do dispositivo-nuvem</span><span class="sxs-lookup"><span data-stu-id="233f9-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="233f9-104">IoT Hub permite-lhe tooroute [mensagens do dispositivo para nuvem] [ lnk-device-to-cloud] tooIoT Hub pontos finais de orientado para o serviço com base nas propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="233f9-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="233f9-105">Encaminhamento conceder regras Olá flexibilidade toosend necessitam de mensagens onde têm toogo sem Olá para mensagens de tooprocess serviços adicionais ou códigos adicionais toowrite.</span><span class="sxs-lookup"><span data-stu-id="233f9-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="233f9-106">Cada regra de encaminhamento que configura tem Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="233f9-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="233f9-107">Propriedade</span><span class="sxs-lookup"><span data-stu-id="233f9-107">Property</span></span>      | <span data-ttu-id="233f9-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="233f9-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="233f9-109">**Nome**</span><span class="sxs-lookup"><span data-stu-id="233f9-109">**Name**</span></span>      | <span data-ttu-id="233f9-110">Olá nome exclusivo que identifica a regra de Olá.</span><span class="sxs-lookup"><span data-stu-id="233f9-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="233f9-111">**Origem**</span><span class="sxs-lookup"><span data-stu-id="233f9-111">**Source**</span></span>    | <span data-ttu-id="233f9-112">origem de Olá dos dados de Olá transmitido em fluxo toobe alterada.</span><span class="sxs-lookup"><span data-stu-id="233f9-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="233f9-113">Por exemplo, a telemetria do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="233f9-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="233f9-114">**Condição**</span><span class="sxs-lookup"><span data-stu-id="233f9-114">**Condition**</span></span> | <span data-ttu-id="233f9-115">expressão de consulta de Olá para a regra de encaminhamento de Olá que é executada no cabeçalhos e corpo de mensagem de saudação e utilizado toodetermine se se trata de uma correspondência para o ponto final de Olá.</span><span class="sxs-lookup"><span data-stu-id="233f9-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="233f9-116">Para obter mais informações sobre a construção de uma condição de rota, consulte Olá [referência - linguagem de consulta para dispositivos duplos e tarefas][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="233f9-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="233f9-117">**Ponto final**</span><span class="sxs-lookup"><span data-stu-id="233f9-117">**Endpoint**</span></span>  | <span data-ttu-id="233f9-118">nome do ponto final de olá onde o IoT Hub envia mensagens que correspondem à condição Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="233f9-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="233f9-119">Pontos finais devem estar no Olá mesma região que o IoT hub do Olá, caso contrário, poderá cobrada para escreve por várias regiões.</span><span class="sxs-lookup"><span data-stu-id="233f9-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="233f9-120">Uma única mensagem pode correspondem à condição de Olá em várias regras de encaminhamento, na qual caso IoT Hub fornece o ponto final toohello de mensagem Olá associado a cada regra de correspondência.</span><span class="sxs-lookup"><span data-stu-id="233f9-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="233f9-121">IoT Hub também automaticamente deduplicates entrega de mensagens, pelo que o se corresponder a uma mensagem de várias regras que têm todas Olá mesmo destino, que é apenas escrito toothat destino uma vez.</span><span class="sxs-lookup"><span data-stu-id="233f9-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="233f9-122">Um IoT hub tem uma predefinição [ponto final incorporado][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="233f9-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="233f9-123">Pode criar os pontos finais personalizados tooroute mensagens tooby ligar outros serviços do seu hub de toohello de subscrição.</span><span class="sxs-lookup"><span data-stu-id="233f9-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="233f9-124">IoT Hub suporta atualmente os Event Hubs, as filas do Service Bus e tópicos do Service Bus como pontos finais personalizados.</span><span class="sxs-lookup"><span data-stu-id="233f9-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="233f9-125">Filas do Service Bus e tópicos com **sessões** ou **duplicado deteção** ativado não são suportados como pontos finais personalizados.</span><span class="sxs-lookup"><span data-stu-id="233f9-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="233f9-126">Para obter mais informações sobre a criação de pontos finais personalizados no IoT Hub, consulte [pontos finais de IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="233f9-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="233f9-127">Para obter mais informações sobre a leitura do pontos finais personalizados, consulte:</span><span class="sxs-lookup"><span data-stu-id="233f9-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="233f9-128">Ler a partir de [dos Event Hubs][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="233f9-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="233f9-129">Ler a partir de [filas do Service Bus][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="233f9-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="233f9-130">Ler a partir de [tópicos do Service Bus][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="233f9-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="233f9-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="233f9-131">Next steps</span></span>

<span data-ttu-id="233f9-132">Para mais informações sobre pontos finais de IoT Hub, consulte [pontos finais de IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="233f9-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="233f9-133">Para obter mais informações sobre a linguagem de consulta Olá utilizar regras de encaminhamento toodefine, consulte [idioma de consulta do IoT Hub para dispositivos duplos, tarefas e o encaminhamento de mensagens][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="233f9-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="233f9-134">Olá [mensagens de dispositivo para a nuvem do IoT Hub do processo utilizar rotas] [ lnk-d2c-tutorial] tutorial mostra como regras de encaminhamento toouse e os pontos finais personalizados.</span><span class="sxs-lookup"><span data-stu-id="233f9-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
