---
title: aaaReliable Atores temporizadores e lembretes | Microsoft Docs
description: "Introdução tootimers e lembretes dos Reliable Actors do serviço de recursos de infraestrutura."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="ce11b-103">Os temporizadores de ator e lembretes</span><span class="sxs-lookup"><span data-stu-id="ce11b-103">Actor timers and reminders</span></span>
<span data-ttu-id="ce11b-104">Atores podem agendar trabalho periódico em si próprios registando temporizadores ou lembretes.</span><span class="sxs-lookup"><span data-stu-id="ce11b-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="ce11b-105">Este artigo mostra como toouse temporizadores e lembretes e explica as diferenças de Olá entre eles.</span><span class="sxs-lookup"><span data-stu-id="ce11b-105">This article shows how toouse timers and reminders and explains hello differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="ce11b-106">Temporizadores de ator</span><span class="sxs-lookup"><span data-stu-id="ce11b-106">Actor timers</span></span>
<span data-ttu-id="ce11b-107">Os temporizadores de ator fornecem um wrapper em torno de uma tooensure de temporizador .NET ou Java simple que métodos de chamada de retorno de Olá respeitem garantias de concorrência com base em vez de Olá Olá Atores fornece o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="ce11b-107">Actor timers provide a simple wrapper around a .NET or Java timer tooensure that hello callback methods respect hello turn-based concurrency guarantees that hello Actors runtime provides.</span></span>

<span data-ttu-id="ce11b-108">Atores podem utilizar Olá `RegisterTimer`(c#) ou `registerTimer`(Java) e `UnregisterTimer`(c#) ou `unregisterTimer`(Java) os métodos no respetivo base tooregister de classe e os temporizadores de anular o registo.</span><span class="sxs-lookup"><span data-stu-id="ce11b-108">Actors can use hello `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class tooregister and unregister their timers.</span></span> <span data-ttu-id="ce11b-109">exemplo de Olá abaixo mostra a utilização de Olá do temporizador de APIs.</span><span class="sxs-lookup"><span data-stu-id="ce11b-109">hello example below shows hello use of timer APIs.</span></span> <span data-ttu-id="ce11b-110">Olá APIs são muito semelhante temporizador de .NET toohello ou temporizador de Java.</span><span class="sxs-lookup"><span data-stu-id="ce11b-110">hello APIs are very similar toohello .NET timer or Java timer.</span></span> <span data-ttu-id="ce11b-111">Neste exemplo, quando o temporizador de Olá é devida, tempo de execução de Atores de Olá irá chamar Olá `MoveObject`(c#) ou `moveObject`método (Java).</span><span class="sxs-lookup"><span data-stu-id="ce11b-111">In this example, when hello timer is due, hello Actors runtime will call hello `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="ce11b-112">método de Olá é garantido simultaneidade de com base em vez do toorespect Olá.</span><span class="sxs-lookup"><span data-stu-id="ce11b-112">hello method is guaranteed toorespect hello turn-based concurrency.</span></span> <span data-ttu-id="ce11b-113">Isto significa que não existem outros métodos de ator ou chamadas de retorno de temporizador/lembrete será em curso até que esta chamada de retorno de conclusão da execução.</span><span class="sxs-lookup"><span data-stu-id="ce11b-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="ce11b-114">Olá próximo período do temporizador de Olá é iniciado após a conclusão da chamada de retorno Olá execução.</span><span class="sxs-lookup"><span data-stu-id="ce11b-114">hello next period of hello timer starts after hello callback completes execution.</span></span> <span data-ttu-id="ce11b-115">Isto implica que temporizador Olá é parou durante a chamada de retorno Olá está a executar e é iniciada após a conclusão de chamada de retorno Olá.</span><span class="sxs-lookup"><span data-stu-id="ce11b-115">This implies that hello timer is stopped while hello callback is executing and is started when hello callback finishes.</span></span>

<span data-ttu-id="ce11b-116">tempo de execução de Atores de Olá guarda as alterações efetuadas Gestor de estado do ator toohello após a conclusão de chamada de retorno Olá.</span><span class="sxs-lookup"><span data-stu-id="ce11b-116">hello Actors runtime saves changes made toohello actor's State Manager when hello callback finishes.</span></span> <span data-ttu-id="ce11b-117">Se ocorrer um erro ao guardar o estado de Olá, esse objeto de ator vai ser desativado e uma nova instância irá ser ativada.</span><span class="sxs-lookup"><span data-stu-id="ce11b-117">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="ce11b-118">Todos os temporizadores são parados quando ator Olá é desativado como parte da recolha de lixo.</span><span class="sxs-lookup"><span data-stu-id="ce11b-118">All timers are stopped when hello actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="ce11b-119">Chamadas de retorno não temporizador são invocadas depois disso.</span><span class="sxs-lookup"><span data-stu-id="ce11b-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="ce11b-120">Além disso, tempo de execução de Atores de Olá não mantém qualquer informação sobre os temporizadores de Olá que estavam em execução antes de Desativação.</span><span class="sxs-lookup"><span data-stu-id="ce11b-120">Also, hello Actors runtime does not retain any information about hello timers that were running before deactivation.</span></span> <span data-ttu-id="ce11b-121">Está a funcionar toohello ator tooregister os temporizadores de que necessita quando este for reactivado no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="ce11b-121">It is up toohello actor tooregister any timers that it needs when it is reactivated in hello future.</span></span> <span data-ttu-id="ce11b-122">Para obter mais informações, consulte a secção de Olá sobre [recolha de lixo de ator](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="ce11b-122">For more information, see hello section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="ce11b-123">Lembretes de ator</span><span class="sxs-lookup"><span data-stu-id="ce11b-123">Actor reminders</span></span>
<span data-ttu-id="ce11b-124">Lembretes são um mecanismo tootrigger persistentes chamadas de retorno num ator em especificado vezes.</span><span class="sxs-lookup"><span data-stu-id="ce11b-124">Reminders are a mechanism tootrigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="ce11b-125">As suas funcionalidades é tootimers semelhantes.</span><span class="sxs-lookup"><span data-stu-id="ce11b-125">Their functionality is similar tootimers.</span></span> <span data-ttu-id="ce11b-126">Mas, ao contrário temporizadores, lembretes são acionados em todas as circunstâncias até ator Olá explicitamente anula o registo-los ou ator Olá explicitamente é eliminado.</span><span class="sxs-lookup"><span data-stu-id="ce11b-126">But unlike timers, reminders are triggered under all circumstances until hello actor explicitly unregisters them or hello actor is explicitly deleted.</span></span> <span data-ttu-id="ce11b-127">Especificamente, lembretes são acionados em deactivations ator e as ativações pós-falha porque o tempo de execução do Olá Atores persiste informações sobre lembretes do ator Olá.</span><span class="sxs-lookup"><span data-stu-id="ce11b-127">Specifically, reminders are triggered across actor deactivations and failovers because hello Actors runtime persists information about hello actor's reminders.</span></span>

<span data-ttu-id="ce11b-128">tooregister um lembrete, um ator chama Olá `RegisterReminderAsync` método fornecido na classe base Olá, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="ce11b-128">tooregister a reminder, an actor calls hello `RegisterReminderAsync` method provided on hello base class, as shown in hello following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

<span data-ttu-id="ce11b-129">Neste exemplo, `"Pay cell phone bill"` é Olá lembrete nome.</span><span class="sxs-lookup"><span data-stu-id="ce11b-129">In this example, `"Pay cell phone bill"` is hello reminder name.</span></span> <span data-ttu-id="ce11b-130">Esta é uma cadeia que Olá ator utiliza toouniquely identificar um lembrete.</span><span class="sxs-lookup"><span data-stu-id="ce11b-130">This is a string that hello actor uses toouniquely identify a reminder.</span></span> <span data-ttu-id="ce11b-131">`BitConverter.GetBytes(amountInDollars)`(C#) é o contexto de Olá que estão associado com lembrete Olá.</span><span class="sxs-lookup"><span data-stu-id="ce11b-131">`BitConverter.GetBytes(amountInDollars)`(C#) is hello context that is associated with hello reminder.</span></span> <span data-ttu-id="ce11b-132">-Será transmitida back toohello ator como uma argumento toohello lembrete chamada de retorno, ou seja, `IRemindable.ReceiveReminderAsync`(c#) ou `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="ce11b-132">It will be passed back toohello actor as an argument toohello reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="ce11b-133">Atores que utilizam lembretes tem de implementar Olá `IRemindable` interface, conforme mostrado no exemplo Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="ce11b-133">Actors that use reminders must implement hello `IRemindable` interface, as shown in hello example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="ce11b-134">Quando um lembrete é acionado, o tempo de execução do Olá Reliable Actors serão invocados Olá `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`Olá Ator método (Java).</span><span class="sxs-lookup"><span data-stu-id="ce11b-134">When a reminder is triggered, hello Reliable Actors runtime will invoke hello  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on hello Actor.</span></span> <span data-ttu-id="ce11b-135">Um ator pode registar várias lembretes e Olá `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`método (Java) é invocado quando qualquer um desses lembretes é acionada.</span><span class="sxs-lookup"><span data-stu-id="ce11b-135">An actor can register multiple reminders, and hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="ce11b-136">ator Olá pode utilizar o nome de lembrete de Olá que é transmitido no toohello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(Java) método toofigure saída que lembrete foi acionado.</span><span class="sxs-lookup"><span data-stu-id="ce11b-136">hello actor can use hello reminder name that is passed in toohello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method toofigure out which reminder was triggered.</span></span>

<span data-ttu-id="ce11b-137">Olá runtime de Atores guarda estado do ator Olá quando hello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`conclusão de chamada (Java).</span><span class="sxs-lookup"><span data-stu-id="ce11b-137">hello Actors runtime saves hello actor's state when hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="ce11b-138">Se ocorrer um erro ao guardar o estado de Olá, esse objeto de ator vai ser desativado e uma nova instância irá ser ativada.</span><span class="sxs-lookup"><span data-stu-id="ce11b-138">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="ce11b-139">toounregister um lembrete, um ator chama Olá `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`método (Java), conforme ilustrado nos exemplos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="ce11b-139">toounregister a reminder, an actor calls hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in hello examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="ce11b-140">Olá, conforme mostrado acima, `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`método (Java) aceita um `IActorReminder`(c#) ou `ActorReminder`interface (Java).</span><span class="sxs-lookup"><span data-stu-id="ce11b-140">As shown above, hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="ce11b-141">Olá ator classe base suporta um `GetReminder`(c#) ou `getReminder`método (Java) que pode ser utilizados tooretrieve Olá `IActorReminder`(c#) ou `ActorReminder`interface (Java) mediante a transmissão no nome do lembrete de Olá.</span><span class="sxs-lookup"><span data-stu-id="ce11b-141">hello actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used tooretrieve hello `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in hello reminder name.</span></span> <span data-ttu-id="ce11b-142">Este é conveniente porque ator Olá não precisa de toopersist Olá `IActorReminder`(c#) ou `ActorReminder`interface (Java) que foi devolvido de Olá `RegisterReminder`(c#) ou `registerReminder`chamada de método (Java).</span><span class="sxs-lookup"><span data-stu-id="ce11b-142">This is convenient because hello actor does not need toopersist hello `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from hello `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce11b-143">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="ce11b-143">Next Steps</span></span>
<span data-ttu-id="ce11b-144">Saiba mais sobre eventos de Ator fiável e reentrancy:</span><span class="sxs-lookup"><span data-stu-id="ce11b-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="ce11b-145">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="ce11b-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="ce11b-146">Reentrancy ator</span><span class="sxs-lookup"><span data-stu-id="ce11b-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
