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
# <a name="event-hubs-net-standard-api-overview"></a>Descrição geral dos Event Hubs .NET API padrão
Este artigo resume algumas das chave Olá Event Hubs .NET padrão APIs do cliente. Não existem atualmente duas bibliotecas de cliente .NET padrão:
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  Esta biblioteca fornece todas as operações de tempo de execução básico.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * Esta biblioteca adiciona funcionalidades adicionais que permite para controlar eventos processados, não sendo Olá tooread de forma mais fácil de um hub de eventos.

## <a name="event-hubs-client"></a>Cliente de Hubs de eventos
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) é hello objeto principal utilizar toosend eventos, criar recetores e informações de tempo de execução tooget. Este cliente está hub de eventos específico de tooa ligado e cria um novo ligação toohello Event Hubs ponto final.

### <a name="create-an-event-hubs-client"></a>Criar um cliente dos Event Hubs
Um [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) objeto é criado a partir de uma cadeia de ligação. Olá tooinstantiate da forma mais simples um novo cliente é mostrado no seguinte exemplo de Olá:

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

tooprogrammatically Editar cadeia de ligação de Olá, pode utilizar Olá [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) classe e passar cadeia de ligação de Olá como um parâmetro demasiado[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Enviar eventos
hub de eventos de tooan eventos toosend, utilize Olá [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) classe. corpo de Olá tem de ser um `byte` matriz, ou um `byte` segmento de matriz.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Receber eventos
Olá recomendada eventos tooreceive de forma a partir dos Hubs de eventos está a utilizar Olá [anfitrião do processador de eventos](#event-processor-host-apis), que fornece funcionalidade tooautomatically manter monitorizar deslocamento e informações de partição. No entanto, existem determinadas situações em que poderá ser útil flexibilidade de Olá toouse de eventos de tooreceive de biblioteca do Olá core dos Event Hubs.

#### <a name="create-a-receiver"></a>Criar um recetor
Recetores estão associadas toospecific partições, por isso, na ordem tooreceive todos os eventos num hub de eventos, terá toocreate várias instâncias. Um modo geral, é informações da partição uma boa prática tooget Olá x509securitytokenparameters, em vez de pré-programar ids de partição Olá. Na ordem toodo por isso, pode utilizar Olá [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) método.

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

Uma vez que os eventos nunca são removidos de um hub de eventos (e apenas expirarem), terá de ponto de partida toospecify Olá adequado. Olá exemplo seguinte mostra as combinações possíveis.

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Consumir um evento
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

## <a name="event-processor-host-apis"></a>APIs de anfitrião do processador de eventos
Estas APIs fornecem os processos de tooworker de resiliência que poderão ficar indisponíveis, por distribuição partições em trabalhadores disponíveis.

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

Olá seguinte é uma implementação de exemplo de Olá [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

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

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre cenários dos Event Hubs, visite estas ligações:

* [O que é Event Hubs do Azure?](event-hubs-what-is-event-hubs.md)
* [Apis de Hubs de eventos disponível](event-hubs-api-overview.md)

Olá .NET API referências são aqui:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)