---
title: "aaaReentrancy em com base em ator micro-serviços do Azure | Microsoft Docs"
description: "Tooreentrancy de introdução para o serviço de recursos de infraestrutura Reliable Actors"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a>Reentrancy do Reliable Actors
tempo de execução de Reliable Actors Olá, por predefinição, permite reentrancy baseado no contexto de chamada lógico. Isto permite reentrant toobe de atores se estão a ser Olá mesma cadeia de contexto de chamada. Por exemplo, Ator A envia um tooActor mensagem B, que envia uma mensagem tooActor C. Como parte do processamento de mensagens de Olá, se Ator C chamadas de Atores A, mensagem de saudação é reentrante, pelo que serão permitida. As mensagens que fazem parte de um contexto de chamada diferente serão bloqueadas no Ator A até terminar o processamento.

Existem duas opções disponíveis para reentrancy ator definido no Olá `ActorReentrancyMode` enum:

* `LogicalCallContext`(comportamento predefinido)
* `Disallowed`-Desativa reentrancy

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
Reentrancy podem ser configuradas num `ActorService`do definições durante o registo. definição de Olá aplica-se em instâncias de ator tooall criadas no serviço de atores Olá.

Olá exemplo seguinte mostra um serviço de atores que define o modo de reentrancy Olá demasiado`ActorReentrancyMode.Disallowed`. Neste caso, se um ator envia um actor de tooanother mensagem reentrantes, uma exceção do tipo `FabricException` será emitida.

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre reentrancy no Olá [documentação de referência da API de Ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)
