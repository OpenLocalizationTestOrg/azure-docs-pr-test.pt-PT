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
# <a name="actor-timers-and-reminders"></a>Os temporizadores de ator e lembretes
Atores podem agendar trabalho periódico em si próprios registando temporizadores ou lembretes. Este artigo mostra como toouse temporizadores e lembretes e explica as diferenças de Olá entre eles.

## <a name="actor-timers"></a>Temporizadores de ator
Os temporizadores de ator fornecem um wrapper em torno de uma tooensure de temporizador .NET ou Java simple que métodos de chamada de retorno de Olá respeitem garantias de concorrência com base em vez de Olá Olá Atores fornece o tempo de execução.

Atores podem utilizar Olá `RegisterTimer`(c#) ou `registerTimer`(Java) e `UnregisterTimer`(c#) ou `unregisterTimer`(Java) os métodos no respetivo base tooregister de classe e os temporizadores de anular o registo. exemplo de Olá abaixo mostra a utilização de Olá do temporizador de APIs. Olá APIs são muito semelhante temporizador de .NET toohello ou temporizador de Java. Neste exemplo, quando o temporizador de Olá é devida, tempo de execução de Atores de Olá irá chamar Olá `MoveObject`(c#) ou `moveObject`método (Java). método de Olá é garantido simultaneidade de com base em vez do toorespect Olá. Isto significa que não existem outros métodos de ator ou chamadas de retorno de temporizador/lembrete será em curso até que esta chamada de retorno de conclusão da execução.

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

Olá próximo período do temporizador de Olá é iniciado após a conclusão da chamada de retorno Olá execução. Isto implica que temporizador Olá é parou durante a chamada de retorno Olá está a executar e é iniciada após a conclusão de chamada de retorno Olá.

tempo de execução de Atores de Olá guarda as alterações efetuadas Gestor de estado do ator toohello após a conclusão de chamada de retorno Olá. Se ocorrer um erro ao guardar o estado de Olá, esse objeto de ator vai ser desativado e uma nova instância irá ser ativada.

Todos os temporizadores são parados quando ator Olá é desativado como parte da recolha de lixo. Chamadas de retorno não temporizador são invocadas depois disso. Além disso, tempo de execução de Atores de Olá não mantém qualquer informação sobre os temporizadores de Olá que estavam em execução antes de Desativação. Está a funcionar toohello ator tooregister os temporizadores de que necessita quando este for reactivado no Olá futura. Para obter mais informações, consulte a secção de Olá sobre [recolha de lixo de ator](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Lembretes de ator
Lembretes são um mecanismo tootrigger persistentes chamadas de retorno num ator em especificado vezes. As suas funcionalidades é tootimers semelhantes. Mas, ao contrário temporizadores, lembretes são acionados em todas as circunstâncias até ator Olá explicitamente anula o registo-los ou ator Olá explicitamente é eliminado. Especificamente, lembretes são acionados em deactivations ator e as ativações pós-falha porque o tempo de execução do Olá Atores persiste informações sobre lembretes do ator Olá.

tooregister um lembrete, um ator chama Olá `RegisterReminderAsync` método fornecido na classe base Olá, conforme mostrado no seguinte exemplo de Olá:

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

Neste exemplo, `"Pay cell phone bill"` é Olá lembrete nome. Esta é uma cadeia que Olá ator utiliza toouniquely identificar um lembrete. `BitConverter.GetBytes(amountInDollars)`(C#) é o contexto de Olá que estão associado com lembrete Olá. -Será transmitida back toohello ator como uma argumento toohello lembrete chamada de retorno, ou seja, `IRemindable.ReceiveReminderAsync`(c#) ou `Remindable.receiveReminderAsync`(Java).

Atores que utilizam lembretes tem de implementar Olá `IRemindable` interface, conforme mostrado no exemplo Olá abaixo.

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

Quando um lembrete é acionado, o tempo de execução do Olá Reliable Actors serão invocados Olá `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`Olá Ator método (Java). Um ator pode registar várias lembretes e Olá `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`método (Java) é invocado quando qualquer um desses lembretes é acionada. ator Olá pode utilizar o nome de lembrete de Olá que é transmitido no toohello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(Java) método toofigure saída que lembrete foi acionado.

Olá runtime de Atores guarda estado do ator Olá quando hello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`conclusão de chamada (Java). Se ocorrer um erro ao guardar o estado de Olá, esse objeto de ator vai ser desativado e uma nova instância irá ser ativada.

toounregister um lembrete, um ator chama Olá `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`método (Java), conforme ilustrado nos exemplos de Olá abaixo.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Olá, conforme mostrado acima, `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`método (Java) aceita um `IActorReminder`(c#) ou `ActorReminder`interface (Java). Olá ator classe base suporta um `GetReminder`(c#) ou `getReminder`método (Java) que pode ser utilizados tooretrieve Olá `IActorReminder`(c#) ou `ActorReminder`interface (Java) mediante a transmissão no nome do lembrete de Olá. Este é conveniente porque ator Olá não precisa de toopersist Olá `IActorReminder`(c#) ou `ActorReminder`interface (Java) que foi devolvido de Olá `RegisterReminder`(c#) ou `registerReminder`chamada de método (Java).

## <a name="next-steps"></a>Passos Seguintes
Saiba mais sobre eventos de Ator fiável e reentrancy:
* [Eventos de ator](service-fabric-reliable-actors-events.md)
* [Reentrancy ator](service-fabric-reliable-actors-reentrancy.md)
