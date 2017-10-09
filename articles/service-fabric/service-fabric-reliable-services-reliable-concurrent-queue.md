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
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>Introdução tooReliableConcurrentQueue no Azure Service Fabric
Fiável fila em simultâneo é uma fila assíncrona, transacional e replicada que simultaneidade elevada de funcionalidades para colocar em fila e anular operações. É concebida toodeliver débito alto e baixa latência por simplificar Olá strict FIFO ordenação fornecida pelo [fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) e em vez disso, fornece uma ordenação de melhor esforço.

## <a name="apis"></a>APIs

|Fila em simultâneo                |Fila simultânea fiável                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Tarefa EnqueueAsync (tx ITransaction, item de T)                       |
| bool TryDequeue (saída de resultado de T)  | Tarefa < ConditionalValue < T >> TryDequeueAsync (ITransaction tx)  |
| Int existente                    | muito existente                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>Comparação com [fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx)

Fiável fila em simultâneo é oferecida como uma alternativa demasiado[fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx). Deve ser utilizado em casos onde o ordenação de FIFO strict não é necessária, como guaranteeing FIFO requer um compromisso com a simultaneidade.  [Fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) utiliza bloqueios tooenforce FIFO ordenação, com um máximo de uma transação permitido tooenqueue e na maioria de uma transação permitido toodequeue de cada vez. Em comparação, fila simultâneas fiável relaxes Olá ordenação restrição e permite que qualquer número toointerleave de transações em simultâneo os colocar em fila e anular operações. Ordenação de melhor esforço é fornecido, no entanto Olá ordenação relativo de dois valores numa fila simultâneas fiável nunca pode ser garantida.

Fila de simultâneas fiável proporciona um maior débito e latência inferior do que [fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) sempre que existem várias transações concorrentes efetuar enqueues e/ou dequeues.

Exemplo de utilizar as maiúsculas e minúsculas para Olá ReliableConcurrentQueue é Olá [fila de mensagens](https://en.wikipedia.org/wiki/Message_queue) cenário. Neste cenário, um ou mais produtores de mensagem criarem e adicionar itens toohello fila e um ou mais consumidores de mensagem solicitar mensagens da fila de Olá e processá-los. Vários produtores e consumidores podem trabalhar de forma independente, utilizando transações concorrentes na fila de Olá tooprocess de ordem.

## <a name="usage-guidelines"></a>Diretrizes de utilização
* fila de Olá espera que os itens de Olá na fila de Olá têm um período de retenção baixa. Ou seja, itens de Olá não seriam permanecem na fila de Olá durante muito tempo.
* fila de Olá não garante a ordenação de FIFO rigorosa.
* fila de Olá não ler as suas próprias escritas. Se um item é colocados em fila dentro de uma transação, não será visível tooa dequeuer dentro Olá mesma transação.
* Dequeues não estão isoladas umas das outras. Se o item *A* é removida na transação *txnA*, mesmo que *txnA* não está consolidada, item *A* não seria tooa visível em simultâneo transação *txnB*.  Se *txnA* interrompe, *A* ficarão visíveis demasiado*txnB* imediatamente.
* *TryPeekAsync* comportamento pode ser implementado utilizando um *TryDequeueAsync* e, em seguida, abortar a transação de Olá. Um exemplo desta situação pode ser encontrado na secção de padrões de programação de Olá.
* A contagem é não transacional. Pode ser utilizado tooget uma ideia dos número Olá de elementos na fila de Olá, mas representa um ponto no tempo e não pode ser confiada.
* Dispendiosas processamento Olá removidas itens devem não ser efetuadas enquanto a transação de Olá está ativa, transações de longa execução tooavoid podem ter um impacto no desempenho no sistema de Olá.

## <a name="code-snippets"></a>Fragmentos de código
Informe-nos observe alguns fragmentos de código e as respetivas saídas esperadas. Processamento de exceções é ignorado nesta secção.

### <a name="enqueueasync"></a>EnqueueAsync
Seguem-se alguns fragmentos de código para utilizar EnqueueAsync seguido as respetivas saídas esperadas.

- *Cenário 1: Único colocar em fila de tarefas*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Partem do princípio dessa tarefa Olá foi concluída com êxito e que não existem transações concorrentes modificar fila Olá ocorreram. utilizador de Olá pode esperar itens do Olá fila toocontain Olá em nenhum dos Olá ordens os seguintes:

> 10, 20

> 20, 10


- *Caso 2: Paralela colocar em fila de tarefas*

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

Partem do princípio de que as tarefas de Olá são concluídas com êxito, se as tarefas de Olá executaram em paralelo e que ocorreram não existem transações concorrentes modificar fila Olá. A inferência não pode ser efetuada sobre ordem Olá de itens na fila de Olá. Para este fragmento de código, itens de Olá podem aparecer em qualquer um dos Olá 4! orderings possíveis.  fila de Olá tentará itens de Olá tookeep ordem Olá original (colocados em fila), mas pode ser forçada tooreordê-las devido a operações de tooconcurrent ou falhas.


### <a name="dequeueasync"></a>DequeueAsync
Seguem-se alguns fragmentos de código para utilizar TryDequeueAsync seguido saídas Olá esperado. Suponha que fila Olá já está preenchida com Olá seguintes itens na fila de Olá:
> 10, 20, 30, 40, 50, 60

- *Cenário 1: Único anular tarefas*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Partem do princípio dessa tarefa Olá foi concluída com êxito e que não existem transações concorrentes modificar fila Olá ocorreram. Uma vez que a inferência não pode ser efetuada sobre a ordem de Olá dos itens de Olá na fila de Olá, poderão ser removida qualquer três itens Olá, por qualquer ordem. fila de Olá tentará itens de Olá tookeep ordem Olá original (colocados em fila), mas pode ser forçada tooreordê-las devido a operações de tooconcurrent ou falhas.  

- *Caso 2: Efetuada em paralelo anular a tarefa*

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

Partem do princípio de que as tarefas de Olá são concluídas com êxito, se as tarefas de Olá executaram em paralelo e que ocorreram não existem transações concorrentes modificar fila Olá. Uma vez que a inferência não pode ser efetuada sobre a ordem de Olá dos itens de Olá na fila de Olá, Olá listas *dequeue1* e *dequeue2* cada conterá os dois itens, por qualquer ordem.

Olá mesmo item será *não* aparecer em ambos. Por conseguinte, se tiver dequeue1 *10*, *30*, em seguida, teria dequeue2 *20*, *40*.

- *Cenário 3: Anular a ordenação com Abort de transação*

Abortar uma transação com em trânsito dequeues PUT itens Olá fazer uma cópia no cabeçalho de Olá da fila de Olá. ordem de Olá na qual os itens de Olá são colocados para trás no cabeçalho de Olá da fila de Olá não é garantida. Informe-nos observe Olá seguinte código:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
Partem do princípio de que itens Olá foram removidas no Olá seguinte ordem:
> 10, 20

Quando é abortar a transação de Olá, itens de Olá seriam adicionados toohello fundo do cabeçalho da fila Olá em nenhum dos Olá seguir as ordens de:
> 10, 20

> 20, 10

Olá mesmo se aplica a todos os casos em que a transação de Olá não era com êxito de *consolidado*.

## <a name="programming-patterns"></a>Padrões de programação
Nesta secção, informe-nos observe alguns programação padrões que poderão ser útil utilizar ReliableConcurrentQueue.

### <a name="batch-dequeues"></a>Dequeues do batch
A recomendado é de programação padrão para Olá consumidor tarefas toobatch respetivo dequeues em vez de efetuar um anular cada vez. utilizador Olá pode escolher toothrottle atrasos entre cada tamanho de lote do batch ou Olá. Olá seguinte fragmento de código mostra este modelo de programação.  Tenha em atenção que neste exemplo, processamento de Olá é efetuado após a conclusão da transação de Olá consolidada, para que o se um índice de falhas toooccur ao processar, hello itens não processados serão perdidas sem ter sido processada.  Em alternativa, pode ser feito processamento Olá dentro do âmbito da transação Olá, no entanto Isto pode ter um impacto negativo no desempenho e necessita de processamento de itens de Olá já processados.

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

### <a name="best-effort-notification-based-processing"></a>Processamento de com base na notificação de melhor esforço
Padrão de programação interessante outro utiliza Olá API de contagem. Aqui, pode implementar processamento de melhor esforço baseada na notificação para a fila de Olá. fila de Olá contagem pode ser utilizado toothrottle um colocar em fila ou uma tarefa de dequeue.  Tenha em atenção que exemplo Olá anterior, uma vez que o processamento de Olá ocorre fora de transação de Olá, não processados itens podem ser perdidas se ocorrer uma falha durante o processamento.

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

### <a name="best-effort-drain"></a>Drenagem de melhor esforço
Uma drenagem da fila de Olá não poderá ser garantida devido toohello natureza simultâneas da estrutura de dados de Olá.  É possível que, mesmo que não existem operações do utilizador na fila de Olá estão em trânsito, uma chamada de determinado tooTryDequeueAsync pode não devolver um item que foi anteriormente colocados em fila e consolidada.  item de colocados em fila Olá fique demasiado*eventualmente* ficam visível toodequeue, no entanto, sem um mecanismo de comunicação fora de banda, um consumidor de independente não é possível saber essa fila Olá atingiu um Estado de repouso mesmo quando todos os foram parados produtores e não existem operações de colocar em fila novo são permitidas. Assim, a operação de drenagem Olá é melhor esforço conforme implementado abaixo.

utilizador Olá deve parar todas as outras produtor e tarefas de consumidor e aguarde qualquer toocommit de transações em trânsito ou a abortar, antes de repetir a fila de Olá toodrain.  Se for o utilizador de Olá sabe o número de Olá esperado de itens na fila de Olá, estes podem configurar uma notificação que indica que todos os itens de tem sido removidos.

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

### <a name="peek"></a>Pré-visualizar
ReliableConcurrentQueue não fornece Olá *TryPeekAsync* api. Os utilizadores podem obter a peek Olá semântica utilizando um *TryDequeueAsync* e, em seguida, abortar a transação de Olá. Neste exemplo, dequeues são processados apenas se o valor do item de Olá é superior ao *10*.

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

## <a name="must-read"></a>Tem de leitura
* [Início rápido Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Trabalhar com as Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Notificações de serviços fiáveis](service-fabric-reliable-services-notifications.md)
* [Reliable Services de cópia de segurança e restaurar (recuperação após desastre)](service-fabric-reliable-services-backup-restore.md)
* [Configuração do Gestor de estado fiável](service-fabric-reliable-services-configuration.md)
* [Introdução aos serviços de API Web do Service Fabric](service-fabric-reliable-services-communication-webapi.md)
* [Utilização avançada de Olá fiável modelo de programação de serviços](service-fabric-reliable-services-advanced-usage.md)
* [Referência para programadores para coleções fiáveis](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
