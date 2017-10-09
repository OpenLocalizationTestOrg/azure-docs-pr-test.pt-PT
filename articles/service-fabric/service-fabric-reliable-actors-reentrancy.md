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
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="f6e2c-103">Reentrancy do Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="f6e2c-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="f6e2c-104">tempo de execução de Reliable Actors Olá, por predefinição, permite reentrancy baseado no contexto de chamada lógico.</span><span class="sxs-lookup"><span data-stu-id="f6e2c-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="f6e2c-105">Isto permite reentrant toobe de atores se estão a ser Olá mesma cadeia de contexto de chamada.</span><span class="sxs-lookup"><span data-stu-id="f6e2c-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="f6e2c-106">Por exemplo, Ator A envia um tooActor mensagem B, que envia uma mensagem tooActor C. Como parte do processamento de mensagens de Olá, se Ator C chamadas de Atores A, mensagem de saudação é reentrante, pelo que serão permitida.</span><span class="sxs-lookup"><span data-stu-id="f6e2c-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="f6e2c-107">As mensagens que fazem parte de um contexto de chamada diferente serão bloqueadas no Ator A até terminar o processamento.</span><span class="sxs-lookup"><span data-stu-id="f6e2c-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="f6e2c-108">Existem duas opções disponíveis para reentrancy ator definido no Olá `ActorReentrancyMode` enum:</span><span class="sxs-lookup"><span data-stu-id="f6e2c-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="f6e2c-109">`LogicalCallContext`(comportamento predefinido)</span><span class="sxs-lookup"><span data-stu-id="f6e2c-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="f6e2c-110">`Disallowed`-Desativa reentrancy</span><span class="sxs-lookup"><span data-stu-id="f6e2c-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="f6e2c-111">Reentrancy podem ser configuradas num `ActorService`do definições durante o registo.</span><span class="sxs-lookup"><span data-stu-id="f6e2c-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="f6e2c-112">definição de Olá aplica-se em instâncias de ator tooall criadas no serviço de atores Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e2c-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="f6e2c-113">Olá exemplo seguinte mostra um serviço de atores que define o modo de reentrancy Olá demasiado`ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="f6e2c-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="f6e2c-114">Neste caso, se um ator envia um actor de tooanother mensagem reentrantes, uma exceção do tipo `FabricException` será emitida.</span><span class="sxs-lookup"><span data-stu-id="f6e2c-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="f6e2c-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f6e2c-115">Next steps</span></span>
* <span data-ttu-id="f6e2c-116">Saiba mais sobre reentrancy no Olá [documentação de referência da API de Ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="f6e2c-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
