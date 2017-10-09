---
title: aaaReliableConcurrentQueue no Azure Service Fabric
description: "ReliableConcurrentQueue é uma fila de débito elevado que permite enqueues paralelas e dequeues."
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="059a5-103">Introdução tooReliableConcurrentQueue no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="059a5-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="059a5-104">Fiável fila em simultâneo é uma fila assíncrona, transacional e replicada que simultaneidade elevada de funcionalidades para colocar em fila e anular operações.</span><span class="sxs-lookup"><span data-stu-id="059a5-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="059a5-105">É concebida toodeliver débito alto e baixa latência por simplificar Olá strict FIFO ordenação fornecida pelo [fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) e em vez disso, fornece uma ordenação de melhor esforço.</span><span class="sxs-lookup"><span data-stu-id="059a5-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="059a5-106">APIs</span><span class="sxs-lookup"><span data-stu-id="059a5-106">APIs</span></span>

|<span data-ttu-id="059a5-107">Fila em simultâneo</span><span class="sxs-lookup"><span data-stu-id="059a5-107">Concurrent Queue</span></span>                |<span data-ttu-id="059a5-108">Fila simultânea fiável</span><span class="sxs-lookup"><span data-stu-id="059a5-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="059a5-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="059a5-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="059a5-110">Tarefa EnqueueAsync (tx ITransaction, item de T)</span><span class="sxs-lookup"><span data-stu-id="059a5-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="059a5-111">bool TryDequeue (saída de resultado de T)</span><span class="sxs-lookup"><span data-stu-id="059a5-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="059a5-112">Tarefa < ConditionalValue < T >> TryDequeueAsync (ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="059a5-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="059a5-113">Int existente</span><span class="sxs-lookup"><span data-stu-id="059a5-113">int Count()</span></span>                    | <span data-ttu-id="059a5-114">muito existente</span><span class="sxs-lookup"><span data-stu-id="059a5-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="059a5-115">Comparação com [fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="059a5-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="059a5-116">Fiável fila em simultâneo é oferecida como uma alternativa demasiado[fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="059a5-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="059a5-117">Deve ser utilizado em casos onde o ordenação de FIFO strict não é necessária, como guaranteeing FIFO requer um compromisso com a simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="059a5-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="059a5-118">[Fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) utiliza bloqueios tooenforce FIFO ordenação, com um máximo de uma transação permitido tooenqueue e na maioria de uma transação permitido toodequeue de cada vez.</span><span class="sxs-lookup"><span data-stu-id="059a5-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="059a5-119">Em comparação, fila simultâneas fiável relaxes Olá ordenação restrição e permite que qualquer número toointerleave de transações em simultâneo os colocar em fila e anular operações.</span><span class="sxs-lookup"><span data-stu-id="059a5-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="059a5-120">Ordenação de melhor esforço é fornecido, no entanto Olá ordenação relativo de dois valores numa fila simultâneas fiável nunca pode ser garantida.</span><span class="sxs-lookup"><span data-stu-id="059a5-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="059a5-121">Fila de simultâneas fiável proporciona um maior débito e latência inferior do que [fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) sempre que existem várias transações concorrentes efetuar enqueues e/ou dequeues.</span><span class="sxs-lookup"><span data-stu-id="059a5-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="059a5-122">Exemplo de utilizar as maiúsculas e minúsculas para Olá ReliableConcurrentQueue é Olá [fila de mensagens](https://en.wikipedia.org/wiki/Message_queue) cenário.</span><span class="sxs-lookup"><span data-stu-id="059a5-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="059a5-123">Neste cenário, um ou mais produtores de mensagem criarem e adicionar itens toohello fila e um ou mais consumidores de mensagem solicitar mensagens da fila de Olá e processá-los.</span><span class="sxs-lookup"><span data-stu-id="059a5-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="059a5-124">Vários produtores e consumidores podem trabalhar de forma independente, utilizando transações concorrentes na fila de Olá tooprocess de ordem.</span><span class="sxs-lookup"><span data-stu-id="059a5-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="059a5-125">Diretrizes de utilização</span><span class="sxs-lookup"><span data-stu-id="059a5-125">Usage Guidelines</span></span>
* <span data-ttu-id="059a5-126">fila de Olá espera que os itens de Olá na fila de Olá têm um período de retenção baixa.</span><span class="sxs-lookup"><span data-stu-id="059a5-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="059a5-127">Ou seja, itens de Olá não seriam permanecem na fila de Olá durante muito tempo.</span><span class="sxs-lookup"><span data-stu-id="059a5-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="059a5-128">fila de Olá não garante a ordenação de FIFO rigorosa.</span><span class="sxs-lookup"><span data-stu-id="059a5-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="059a5-129">fila de Olá não ler as suas próprias escritas.</span><span class="sxs-lookup"><span data-stu-id="059a5-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="059a5-130">Se um item é colocados em fila dentro de uma transação, não será visível tooa dequeuer dentro Olá mesma transação.</span><span class="sxs-lookup"><span data-stu-id="059a5-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="059a5-131">Dequeues não estão isoladas umas das outras.</span><span class="sxs-lookup"><span data-stu-id="059a5-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="059a5-132">Se o item *A* é removida na transação *txnA*, mesmo que *txnA* não está consolidada, item *A* não seria tooa visível em simultâneo transação *txnB*.</span><span class="sxs-lookup"><span data-stu-id="059a5-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="059a5-133">Se *txnA* interrompe, *A* ficarão visíveis demasiado*txnB* imediatamente.</span><span class="sxs-lookup"><span data-stu-id="059a5-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="059a5-134">*TryPeekAsync* comportamento pode ser implementado utilizando um *TryDequeueAsync* e, em seguida, abortar a transação de Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="059a5-135">Um exemplo desta situação pode ser encontrado na secção de padrões de programação de Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="059a5-136">A contagem é não transacional.</span><span class="sxs-lookup"><span data-stu-id="059a5-136">Count is non-transactional.</span></span> <span data-ttu-id="059a5-137">Pode ser utilizado tooget uma ideia dos número Olá de elementos na fila de Olá, mas representa um ponto no tempo e não pode ser confiada.</span><span class="sxs-lookup"><span data-stu-id="059a5-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="059a5-138">Dispendiosas processamento Olá removidas itens devem não ser efetuadas enquanto a transação de Olá está ativa, transações de longa execução tooavoid podem ter um impacto no desempenho no sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="059a5-139">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="059a5-139">Code Snippets</span></span>
<span data-ttu-id="059a5-140">Informe-nos observe alguns fragmentos de código e as respetivas saídas esperadas.</span><span class="sxs-lookup"><span data-stu-id="059a5-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="059a5-141">Processamento de exceções é ignorado nesta secção.</span><span class="sxs-lookup"><span data-stu-id="059a5-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="059a5-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="059a5-142">EnqueueAsync</span></span>
<span data-ttu-id="059a5-143">Seguem-se alguns fragmentos de código para utilizar EnqueueAsync seguido as respetivas saídas esperadas.</span><span class="sxs-lookup"><span data-stu-id="059a5-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="059a5-144">*Cenário 1: Único colocar em fila de tarefas*</span><span class="sxs-lookup"><span data-stu-id="059a5-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="059a5-145">Partem do princípio dessa tarefa Olá foi concluída com êxito e que não existem transações concorrentes modificar fila Olá ocorreram.</span><span class="sxs-lookup"><span data-stu-id="059a5-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="059a5-146">utilizador de Olá pode esperar itens do Olá fila toocontain Olá em nenhum dos Olá ordens os seguintes:</span><span class="sxs-lookup"><span data-stu-id="059a5-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="059a5-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="059a5-147">10, 20</span></span>

> <span data-ttu-id="059a5-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="059a5-148">20, 10</span></span>


- <span data-ttu-id="059a5-149">*Caso 2: Paralela colocar em fila de tarefas*</span><span class="sxs-lookup"><span data-stu-id="059a5-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="059a5-150">Partem do princípio de que as tarefas de Olá são concluídas com êxito, se as tarefas de Olá executaram em paralelo e que ocorreram não existem transações concorrentes modificar fila Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="059a5-151">A inferência não pode ser efetuada sobre ordem Olá de itens na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="059a5-152">Para este fragmento de código, itens de Olá podem aparecer em qualquer um dos Olá 4!</span><span class="sxs-lookup"><span data-stu-id="059a5-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="059a5-153">orderings possíveis.</span><span class="sxs-lookup"><span data-stu-id="059a5-153">possible orderings.</span></span>  <span data-ttu-id="059a5-154">fila de Olá tentará itens de Olá tookeep ordem Olá original (colocados em fila), mas pode ser forçada tooreordê-las devido a operações de tooconcurrent ou falhas.</span><span class="sxs-lookup"><span data-stu-id="059a5-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="059a5-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="059a5-155">DequeueAsync</span></span>
<span data-ttu-id="059a5-156">Seguem-se alguns fragmentos de código para utilizar TryDequeueAsync seguido saídas Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="059a5-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="059a5-157">Suponha que fila Olá já está preenchida com Olá seguintes itens na fila de Olá:</span><span class="sxs-lookup"><span data-stu-id="059a5-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="059a5-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="059a5-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="059a5-159">*Cenário 1: Único anular tarefas*</span><span class="sxs-lookup"><span data-stu-id="059a5-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="059a5-160">Partem do princípio dessa tarefa Olá foi concluída com êxito e que não existem transações concorrentes modificar fila Olá ocorreram.</span><span class="sxs-lookup"><span data-stu-id="059a5-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="059a5-161">Uma vez que a inferência não pode ser efetuada sobre a ordem de Olá dos itens de Olá na fila de Olá, poderão ser removida qualquer três itens Olá, por qualquer ordem.</span><span class="sxs-lookup"><span data-stu-id="059a5-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="059a5-162">fila de Olá tentará itens de Olá tookeep ordem Olá original (colocados em fila), mas pode ser forçada tooreordê-las devido a operações de tooconcurrent ou falhas.</span><span class="sxs-lookup"><span data-stu-id="059a5-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="059a5-163">*Caso 2: Efetuada em paralelo anular a tarefa*</span><span class="sxs-lookup"><span data-stu-id="059a5-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="059a5-164">Partem do princípio de que as tarefas de Olá são concluídas com êxito, se as tarefas de Olá executaram em paralelo e que ocorreram não existem transações concorrentes modificar fila Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="059a5-165">Uma vez que a inferência não pode ser efetuada sobre a ordem de Olá dos itens de Olá na fila de Olá, Olá listas *dequeue1* e *dequeue2* cada conterá os dois itens, por qualquer ordem.</span><span class="sxs-lookup"><span data-stu-id="059a5-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="059a5-166">Olá mesmo item será *não* aparecer em ambos.</span><span class="sxs-lookup"><span data-stu-id="059a5-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="059a5-167">Por conseguinte, se tiver dequeue1 *10*, *30*, em seguida, teria dequeue2 *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="059a5-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="059a5-168">*Cenário 3: Anular a ordenação com Abort de transação*</span><span class="sxs-lookup"><span data-stu-id="059a5-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="059a5-169">Abortar uma transação com em trânsito dequeues PUT itens Olá fazer uma cópia no cabeçalho de Olá da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="059a5-170">ordem de Olá na qual os itens de Olá são colocados para trás no cabeçalho de Olá da fila de Olá não é garantida.</span><span class="sxs-lookup"><span data-stu-id="059a5-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="059a5-171">Informe-nos observe Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="059a5-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="059a5-172">Partem do princípio de que itens Olá foram removidas no Olá seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="059a5-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="059a5-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="059a5-173">10, 20</span></span>

<span data-ttu-id="059a5-174">Quando é abortar a transação de Olá, itens de Olá seriam adicionados toohello fundo do cabeçalho da fila Olá em nenhum dos Olá seguir as ordens de:</span><span class="sxs-lookup"><span data-stu-id="059a5-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="059a5-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="059a5-175">10, 20</span></span>

> <span data-ttu-id="059a5-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="059a5-176">20, 10</span></span>

<span data-ttu-id="059a5-177">Olá mesmo se aplica a todos os casos em que a transação de Olá não era com êxito de *consolidado*.</span><span class="sxs-lookup"><span data-stu-id="059a5-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="059a5-178">Padrões de programação</span><span class="sxs-lookup"><span data-stu-id="059a5-178">Programming Patterns</span></span>
<span data-ttu-id="059a5-179">Nesta secção, informe-nos observe alguns programação padrões que poderão ser útil utilizar ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="059a5-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="059a5-180">Dequeues do batch</span><span class="sxs-lookup"><span data-stu-id="059a5-180">Batch Dequeues</span></span>
<span data-ttu-id="059a5-181">A recomendado é de programação padrão para Olá consumidor tarefas toobatch respetivo dequeues em vez de efetuar um anular cada vez.</span><span class="sxs-lookup"><span data-stu-id="059a5-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="059a5-182">utilizador Olá pode escolher toothrottle atrasos entre cada tamanho de lote do batch ou Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="059a5-183">Olá seguinte fragmento de código mostra este modelo de programação.</span><span class="sxs-lookup"><span data-stu-id="059a5-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="059a5-184">Tenha em atenção que neste exemplo, processamento de Olá é efetuado após a conclusão da transação de Olá consolidada, para que o se um índice de falhas toooccur ao processar, hello itens não processados serão perdidas sem ter sido processada.</span><span class="sxs-lookup"><span data-stu-id="059a5-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="059a5-185">Em alternativa, pode ser feito processamento Olá dentro do âmbito da transação Olá, no entanto Isto pode ter um impacto negativo no desempenho e necessita de processamento de itens de Olá já processados.</span><span class="sxs-lookup"><span data-stu-id="059a5-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="059a5-186">Processamento de com base na notificação de melhor esforço</span><span class="sxs-lookup"><span data-stu-id="059a5-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="059a5-187">Padrão de programação interessante outro utiliza Olá API de contagem.</span><span class="sxs-lookup"><span data-stu-id="059a5-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="059a5-188">Aqui, pode implementar processamento de melhor esforço baseada na notificação para a fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="059a5-189">fila de Olá contagem pode ser utilizado toothrottle um colocar em fila ou uma tarefa de dequeue.</span><span class="sxs-lookup"><span data-stu-id="059a5-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="059a5-190">Tenha em atenção que exemplo Olá anterior, uma vez que o processamento de Olá ocorre fora de transação de Olá, não processados itens podem ser perdidas se ocorrer uma falha durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="059a5-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="059a5-191">Drenagem de melhor esforço</span><span class="sxs-lookup"><span data-stu-id="059a5-191">Best-Effort Drain</span></span>
<span data-ttu-id="059a5-192">Uma drenagem da fila de Olá não poderá ser garantida devido toohello natureza simultâneas da estrutura de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="059a5-193">É possível que, mesmo que não existem operações do utilizador na fila de Olá estão em trânsito, uma chamada de determinado tooTryDequeueAsync pode não devolver um item que foi anteriormente colocados em fila e consolidada.</span><span class="sxs-lookup"><span data-stu-id="059a5-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="059a5-194">item de colocados em fila Olá fique demasiado*eventualmente* ficam visível toodequeue, no entanto, sem um mecanismo de comunicação fora de banda, um consumidor de independente não é possível saber essa fila Olá atingiu um Estado de repouso mesmo quando todos os foram parados produtores e não existem operações de colocar em fila novo são permitidas.</span><span class="sxs-lookup"><span data-stu-id="059a5-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="059a5-195">Assim, a operação de drenagem Olá é melhor esforço conforme implementado abaixo.</span><span class="sxs-lookup"><span data-stu-id="059a5-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="059a5-196">utilizador Olá deve parar todas as outras produtor e tarefas de consumidor e aguarde qualquer toocommit de transações em trânsito ou a abortar, antes de repetir a fila de Olá toodrain.</span><span class="sxs-lookup"><span data-stu-id="059a5-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="059a5-197">Se for o utilizador de Olá sabe o número de Olá esperado de itens na fila de Olá, estes podem configurar uma notificação que indica que todos os itens de tem sido removidos.</span><span class="sxs-lookup"><span data-stu-id="059a5-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="059a5-198">Pré-visualizar</span><span class="sxs-lookup"><span data-stu-id="059a5-198">Peek</span></span>
<span data-ttu-id="059a5-199">ReliableConcurrentQueue não fornece Olá *TryPeekAsync* api.</span><span class="sxs-lookup"><span data-stu-id="059a5-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="059a5-200">Os utilizadores podem obter a peek Olá semântica utilizando um *TryDequeueAsync* e, em seguida, abortar a transação de Olá.</span><span class="sxs-lookup"><span data-stu-id="059a5-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="059a5-201">Neste exemplo, dequeues são processados apenas se o valor do item de Olá é superior ao *10*.</span><span class="sxs-lookup"><span data-stu-id="059a5-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="059a5-202">Tem de leitura</span><span class="sxs-lookup"><span data-stu-id="059a5-202">Must Read</span></span>
* [<span data-ttu-id="059a5-203">Início rápido Reliable Services</span><span class="sxs-lookup"><span data-stu-id="059a5-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="059a5-204">Trabalhar com as Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="059a5-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="059a5-205">Notificações de serviços fiáveis</span><span class="sxs-lookup"><span data-stu-id="059a5-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="059a5-206">Reliable Services de cópia de segurança e restaurar (recuperação após desastre)</span><span class="sxs-lookup"><span data-stu-id="059a5-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="059a5-207">Configuração do Gestor de estado fiável</span><span class="sxs-lookup"><span data-stu-id="059a5-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="059a5-208">Introdução aos serviços de API Web do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="059a5-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="059a5-209">Utilização avançada de Olá fiável modelo de programação de serviços</span><span class="sxs-lookup"><span data-stu-id="059a5-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="059a5-210">Referência para programadores para coleções fiáveis</span><span class="sxs-lookup"><span data-stu-id="059a5-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
