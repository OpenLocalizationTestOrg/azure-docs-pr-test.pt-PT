---
title: "aaaOverview de Olá APIs de .NET de Hubs de eventos do Azure Standard | Microsoft Docs"
description: "Descrição geral de API padrão do .NET"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="9dad3-103">Descrição geral dos Event Hubs .NET API padrão</span><span class="sxs-lookup"><span data-stu-id="9dad3-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="9dad3-104">Este artigo resume algumas das chave Olá Event Hubs .NET padrão APIs do cliente.</span><span class="sxs-lookup"><span data-stu-id="9dad3-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="9dad3-105">Não existem atualmente duas bibliotecas de cliente .NET padrão:</span><span class="sxs-lookup"><span data-stu-id="9dad3-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="9dad3-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="9dad3-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="9dad3-107">Esta biblioteca fornece todas as operações de tempo de execução básico.</span><span class="sxs-lookup"><span data-stu-id="9dad3-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="9dad3-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="9dad3-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="9dad3-109">Esta biblioteca adiciona funcionalidades adicionais que permite para controlar eventos processados, não sendo Olá tooread de forma mais fácil de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="9dad3-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="9dad3-110">Cliente de Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="9dad3-110">Event Hubs client</span></span>
<span data-ttu-id="9dad3-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) é hello objeto principal utilizar toosend eventos, criar recetores e informações de tempo de execução tooget.</span><span class="sxs-lookup"><span data-stu-id="9dad3-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="9dad3-112">Este cliente está hub de eventos específico de tooa ligado e cria um novo ligação toohello Event Hubs ponto final.</span><span class="sxs-lookup"><span data-stu-id="9dad3-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="9dad3-113">Criar um cliente dos Event Hubs</span><span class="sxs-lookup"><span data-stu-id="9dad3-113">Create an Event Hubs client</span></span>
<span data-ttu-id="9dad3-114">Um [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) objeto é criado a partir de uma cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="9dad3-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="9dad3-115">Olá tooinstantiate da forma mais simples um novo cliente é mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="9dad3-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="9dad3-116">tooprogrammatically Editar cadeia de ligação de Olá, pode utilizar Olá [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) classe e passar cadeia de ligação de Olá como um parâmetro demasiado[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="9dad3-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="9dad3-117">Enviar eventos</span><span class="sxs-lookup"><span data-stu-id="9dad3-117">Send events</span></span>
<span data-ttu-id="9dad3-118">hub de eventos de tooan eventos toosend, utilize Olá [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) classe.</span><span class="sxs-lookup"><span data-stu-id="9dad3-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="9dad3-119">corpo de Olá tem de ser um `byte` matriz, ou um `byte` segmento de matriz.</span><span class="sxs-lookup"><span data-stu-id="9dad3-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="9dad3-120">Receber eventos</span><span class="sxs-lookup"><span data-stu-id="9dad3-120">Receive events</span></span>
<span data-ttu-id="9dad3-121">Olá recomendada eventos tooreceive de forma a partir dos Hubs de eventos está a utilizar Olá [anfitrião do processador de eventos](#event-processor-host-apis), que fornece funcionalidade tooautomatically manter monitorizar deslocamento e informações de partição.</span><span class="sxs-lookup"><span data-stu-id="9dad3-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="9dad3-122">No entanto, existem determinadas situações em que poderá ser útil flexibilidade de Olá toouse de eventos de tooreceive de biblioteca do Olá core dos Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="9dad3-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="9dad3-123">Criar um recetor</span><span class="sxs-lookup"><span data-stu-id="9dad3-123">Create a receiver</span></span>
<span data-ttu-id="9dad3-124">Recetores estão associadas toospecific partições, por isso, na ordem tooreceive todos os eventos num hub de eventos, terá toocreate várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="9dad3-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="9dad3-125">Um modo geral, é informações da partição uma boa prática tooget Olá x509securitytokenparameters, em vez de pré-programar ids de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="9dad3-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="9dad3-126">Na ordem toodo por isso, pode utilizar Olá [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) método.</span><span class="sxs-lookup"><span data-stu-id="9dad3-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

<span data-ttu-id="9dad3-127">Uma vez que os eventos nunca são removidos de um hub de eventos (e apenas expirarem), terá de ponto de partida toospecify Olá adequado.</span><span class="sxs-lookup"><span data-stu-id="9dad3-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="9dad3-128">Olá exemplo seguinte mostra as combinações possíveis.</span><span class="sxs-lookup"><span data-stu-id="9dad3-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="9dad3-129">Consumir um evento</span><span class="sxs-lookup"><span data-stu-id="9dad3-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="9dad3-130">APIs de anfitrião do processador de eventos</span><span class="sxs-lookup"><span data-stu-id="9dad3-130">Event Processor Host APIs</span></span>
<span data-ttu-id="9dad3-131">Estas APIs fornecem os processos de tooworker de resiliência que poderão ficar indisponíveis, por distribuição partições em trabalhadores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9dad3-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="9dad3-132">Olá seguinte é uma implementação de exemplo de Olá [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="9dad3-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="9dad3-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9dad3-133">Next steps</span></span>
<span data-ttu-id="9dad3-134">toolearn mais informações sobre cenários dos Event Hubs, visite estas ligações:</span><span class="sxs-lookup"><span data-stu-id="9dad3-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="9dad3-135">O que é Event Hubs do Azure?</span><span class="sxs-lookup"><span data-stu-id="9dad3-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="9dad3-136">Apis de Hubs de eventos disponível</span><span class="sxs-lookup"><span data-stu-id="9dad3-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="9dad3-137">Olá .NET API referências são aqui:</span><span class="sxs-lookup"><span data-stu-id="9dad3-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="9dad3-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="9dad3-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="9dad3-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="9dad3-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)