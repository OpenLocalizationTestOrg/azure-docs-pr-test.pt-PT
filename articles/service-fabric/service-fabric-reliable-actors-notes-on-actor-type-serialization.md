---
title: "notas de Atores aaaReliable no ator escreva serialização | Microsoft Docs"
description: "Descreve os requisitos básicos para definir serializáveis classes que podem ser utilizado toodefine Estados Reliable Actors do serviço de recursos de infraestrutura e interfaces"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a>Notas sobre o serviço de recursos de infraestrutura Reliable Actors escreva serialização
argumentos Olá de todos os métodos, tipos de resultados das tarefas de Olá devolvido por cada método numa interface ator e objetos armazenados no Gestor de estado de um ator tem de ser [contrato de dados serializáveis](https://msdn.microsoft.com/library/ms731923.aspx). Isto também se aplica toohello argumentos dos métodos de Olá definidos no [interfaces de eventos de ator](service-fabric-reliable-actors-events.md). (Métodos de interface de eventos de ator sempre devolvem void.)

## <a name="custom-data-types"></a>Tipos de dados personalizada
Neste exemplo, Olá interface de atores a seguir define um método que devolve um tipo de dados personalizado denominado `VoicemailBox`:

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

interface de Olá é implementado por um ator que utiliza toostore de Gestor de estado de Olá um `VoicemailBox` objeto:

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

Neste exemplo, Olá `VoicemailBox` objeto está a ser serializado quando:

* objeto de Olá é transmitido entre uma instância de ator e um autor da chamada.
* objeto de Olá é guardado no Gestor de estado de olá onde é toodisk persistente e replicados tooother nós.

arquitetura de Ator fiável Olá utiliza serialização de DataContract. Por conseguinte, Olá objetos de dados personalizados e os respetivos membros tem de ser anotados com Olá **DataContract** e **DataMember** atributos, respetivamente.

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a>Passos seguintes
* [Coleção de ciclo de vida e libertação da memória de ator](service-fabric-reliable-actors-lifecycle.md)
* [Os temporizadores de ator e lembretes](service-fabric-reliable-actors-timers-reminders.md)
* [Eventos de ator](service-fabric-reliable-actors-events.md)
* [Reentrancy ator](service-fabric-reliable-actors-reentrancy.md)
* [Que o polimorfismo ator e padrões de conceção e orientado para objetos](service-fabric-reliable-actors-polymorphism.md)
* [Monitorização de desempenho e diagnóstico de ator](service-fabric-reliable-actors-diagnostics.md)
