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
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="f53de-103">Notas sobre o serviço de recursos de infraestrutura Reliable Actors escreva serialização</span><span class="sxs-lookup"><span data-stu-id="f53de-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="f53de-104">argumentos Olá de todos os métodos, tipos de resultados das tarefas de Olá devolvido por cada método numa interface ator e objetos armazenados no Gestor de estado de um ator tem de ser [contrato de dados serializáveis](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="f53de-104">hello arguments of all methods, result types of hello tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="f53de-105">Isto também se aplica toohello argumentos dos métodos de Olá definidos no [interfaces de eventos de ator](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="f53de-105">This also applies toohello arguments of hello methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="f53de-106">(Métodos de interface de eventos de ator sempre devolvem void.)</span><span class="sxs-lookup"><span data-stu-id="f53de-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="f53de-107">Tipos de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="f53de-107">Custom data types</span></span>
<span data-ttu-id="f53de-108">Neste exemplo, Olá interface de atores a seguir define um método que devolve um tipo de dados personalizado denominado `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="f53de-108">In this example, hello following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="f53de-109">interface de Olá é implementado por um ator que utiliza toostore de Gestor de estado de Olá um `VoicemailBox` objeto:</span><span class="sxs-lookup"><span data-stu-id="f53de-109">hello interface is implemented by an actor that uses hello state manager toostore a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="f53de-110">Neste exemplo, Olá `VoicemailBox` objeto está a ser serializado quando:</span><span class="sxs-lookup"><span data-stu-id="f53de-110">In this example, hello `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="f53de-111">objeto de Olá é transmitido entre uma instância de ator e um autor da chamada.</span><span class="sxs-lookup"><span data-stu-id="f53de-111">hello object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="f53de-112">objeto de Olá é guardado no Gestor de estado de olá onde é toodisk persistente e replicados tooother nós.</span><span class="sxs-lookup"><span data-stu-id="f53de-112">hello object is saved in hello state manager where it is persisted toodisk and replicated tooother nodes.</span></span>

<span data-ttu-id="f53de-113">arquitetura de Ator fiável Olá utiliza serialização de DataContract.</span><span class="sxs-lookup"><span data-stu-id="f53de-113">hello Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="f53de-114">Por conseguinte, Olá objetos de dados personalizados e os respetivos membros tem de ser anotados com Olá **DataContract** e **DataMember** atributos, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="f53de-114">Therefore, hello custom data objects and their members must be annotated with hello **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="f53de-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f53de-115">Next steps</span></span>
* [<span data-ttu-id="f53de-116">Coleção de ciclo de vida e libertação da memória de ator</span><span class="sxs-lookup"><span data-stu-id="f53de-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="f53de-117">Os temporizadores de ator e lembretes</span><span class="sxs-lookup"><span data-stu-id="f53de-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="f53de-118">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="f53de-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="f53de-119">Reentrancy ator</span><span class="sxs-lookup"><span data-stu-id="f53de-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="f53de-120">Que o polimorfismo ator e padrões de conceção e orientado para objetos</span><span class="sxs-lookup"><span data-stu-id="f53de-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="f53de-121">Monitorização de desempenho e diagnóstico de ator</span><span class="sxs-lookup"><span data-stu-id="f53de-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
