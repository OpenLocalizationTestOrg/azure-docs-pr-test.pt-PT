---
title: "notificações de serviços de aaaReliable | Microsoft Docs"
description: "Documentação conceptual para notificações de Service Fabric Reliable Services"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a>Notificações de serviços fiáveis
Notificações de permitir que os clientes alterações de Olá tootrack que estão a ser efetuadas tooan objeto que o se estiverem interessados em. Notificações de suportam dois tipos de objetos: *fiável Gestor de estado* e *dicionário fiável*.

Os motivos mais comuns para utilizar as notificações são:

* Edifício materializada vistas, tais como índices secundários ou vistas filtradas de estado da réplica Olá agregadas. Um exemplo é um índice ordenado de todas as chaves no dicionário fiável.
* Enviar dados de monitorização, como o número de Olá de utilizadores adicionadas no Olá última hora.

As notificações são desencadeadas como parte da aplicação de operações. Devido a que, notificações devem ser processadas como rápido eventos possíveis e síncronos não devem incluir quaisquer operações dispendiosas.

## <a name="reliable-state-manager-notifications"></a>Notificações do Gestor de estado de fiável
O Gestor de estado de fiável fornece notificações para Olá seguintes eventos:

* Transação
  * Consolidação
* Gestor de estado
  * Reconstrução
  * Adição de um Estado fiável
  * Remoção de um Estado de fiável

Gestor de estado de fiável controla as de transações Olá atual em utilização. alteração apenas da Olá num Estado de transação que faz com que um toobe notificação desencadeado é uma transação ser consolidada.

Gestor de estado de fiável mantém uma coleção de Estados fiáveis como dicionário fiável e fiável de fila. Gestor de estado de fiável desencadeado notificações quando as alterações esta coleção: um Estado fiável é adicionado ou removido, ou o conjunto completo de Olá for reconstruído.
Olá coleção do Gestor de estado fiável for reconstruído em três casos:

* Recuperação: Quando uma réplica é iniciado,-recupera o estado anterior do disco de Olá. No final de Olá de recuperação, utiliza **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de Olá dos Estados fiáveis recuperados.
* Total de cópia: antes de uma réplica pode associar conjunto de configurações de Olá, tem toobe incorporada. Por vezes, isto requer uma cópia completa do Estado de fiável do Gestor de estado de Olá réplica primária toobe toohello aplicados inativo réplica secundária. Gestor de estado de fiável Olá réplica secundária utiliza **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de Olá fiáveis de Estados de que que adquiriu a partir da réplica primária Olá.
* Restauro: Em cenários de recuperação após desastre, estado da réplica Olá pode ser restaurado a partir de uma cópia de segurança através de **RestoreAsync**. Nestes casos, utiliza fiável Gestor de estado na réplica primária Olá **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de Olá fiáveis de Estados de que restaurada a partir de cópia de segurança de Olá.

tooregister para notificações de transação e/ou notificações do Gestor de estado, terá de tooregister com Olá **TransactionChanged** ou **StateManagerChanged** eventos no Gestor de estado fiável. Um local comum tooregister com estes processadores de eventos é construtor Olá do seu serviço de monitorização de estado. Quando registar o construtor de Olá, não irá perder as notificações que é causada por uma alteração durante a duração de Olá de **IReliableStateManager**.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

Olá **TransactionChanged** utiliza o processador de eventos **NotifyTransactionChangedEventArgs** tooprovide detalhes sobre o evento de Olá. Contém a propriedade de ação de Olá (por exemplo, **NotifyTransactionChangedAction.Commit**) que especifica o tipo de Olá de alteração. Também contém a propriedade transaction Olá que fornece uma transação de toohello de referência que foi alterado.

> [!NOTE]
> Hoje em dia, **TransactionChanged** eventos são gerados apenas se a transação de Olá está consolidada. Olá ação é, em seguida, igual demasiado**NotifyTransactionChangedAction.Commit**. Mas no Olá futura, eventos poderão ser gerados para outros tipos de transação de alterações de estado. Recomendamos a verificar a ação de Olá e processar o evento de Olá apenas se for um que espera.
> 
> 

Segue-se um exemplo **TransactionChanged** processador de eventos.

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

Olá **StateManagerChanged** utiliza o processador de eventos **NotifyStateManagerChangedEventArgs** tooprovide detalhes sobre o evento de Olá.
**NotifyStateManagerChangedEventArgs** tem dois subclasses: **NotifyStateManagerRebuildEventArgs** e **NotifyStateManagerSingleEntityChangedEventArgs**.
Utilizar a propriedade de ação de Olá no **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** subclasse correto toohello:

* **NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** e **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**

Segue-se um exemplo **StateManagerChanged** processador de notificação.

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a>Notificações de dicionário fiáveis
Dicionário fiável fornece notificações para Olá seguintes eventos:

* A reconstrução: Chamado quando **ReliableDictionary** recuperou o estado de uma cópia de segurança ou recuperado ou copiado de estado local.
* Limpar: Chamado quando Olá estado **ReliableDictionary** foi limpo através de Olá **ClearAsync** método.
* Adicione: Chamado quando um item foi adicionado demasiado**ReliableDictionary**.
* Atualização: Chamado quando um item na **IReliableDictionary** foi atualizada.
* Remover: Chamado quando um item na **IReliableDictionary** foi eliminado.

notificações de dicionário fiável tooget, terá de tooregister com Olá **DictionaryChanged** processador de eventos no **IReliableDictionary**. Um local comum tooregister com estes processadores de eventos está a ser Olá **ReliableStateManager.StateManagerChanged** adicionar notificação.
Registar quando **IReliableDictionary** é adicionada demasiado**IReliableStateManager** garante que não irá perder quaisquer notificações.

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> **ProcessStateManagerSingleEntityNotification** é o método de exemplo de Olá esse Olá anterior **OnStateManagerChangedHandler** chamadas de exemplo.
> 
> 

Olá código anterior define Olá **IReliableNotificationAsyncCallback** interface, along com **DictionaryChanged**. Porque **NotifyDictionaryRebuildEventArgs** contém um **IAsyncEnumerable** interface – que têm de toobe enumerado de forma assíncrona - notificações de reconstrução são desencadeadas através de  **RebuildNotificationAsyncCallback** em vez de **OnDictionaryChangedHandler**.

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> No Olá precedente código, como parte do processamento de notificação de reconstrução Olá Olá primeiro mantida Estado agregado está desmarcado. Porque a coleção fiável Olá está a ser reconstruída com um Estado de novo, todas as notificações anteriores são irrelevantes.
> 
> 

Olá **DictionaryChanged** utiliza o processador de eventos **NotifyDictionaryChangedEventArgs** tooprovide detalhes sobre o evento de Olá.
**NotifyDictionaryChangedEventArgs** tem cinco subclasses. Utilize a propriedade ação Olá **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** subclasse correto toohello:

* **NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** e **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a>Recomendações
* *Efetue* concluir mais rápido possíveis eventos de notificação.
* *Não* executar quaisquer operações dispendiosas (por exemplo, operações de e/s) como parte dos eventos síncronos.
* *Efetue* verificar o tipo de ação de Olá antes de processar o evento de Olá. Novos tipos de ação podem ser adicionados em Olá futura.

Eis algumas coisas tookeep em mente:

* As notificações são desencadeadas como parte da execução de Olá de uma operação. Por exemplo, uma notificação de restauro é desencadeada como último passo de Olá de uma operação de restauro. Um restauro não será concluída até que o evento de notificação de Olá é processado.
* Porque as notificações são desencadeadas como parte da Olá aplicando operações, os clientes ver apenas as notificações para operações localmente consolidadas. E porque operações garantidas apenas toobe consolidada localmente (por outras palavras, tem sessão iniciada), podem ou não pode ser anuladas no Olá futura.
* No caminho de Refazer Olá, uma única notificação é desencadeada para cada operação aplicada. Isto significa que, se a transação T1 inclui Create(X), Delete(X) e Create(X), irá obter uma notificação para Olá criação de X, para eliminação de Olá e um para a criação de Olá novamente, por essa ordem.
* Para transações que contêm várias operações, operações são aplicadas por ordem de Olá em que foram recebidos na réplica primária do Olá de utilizador de Olá.
* Como parte do processamento de progresso FALSO, algumas operações podem ser anuladas. As notificações são geradas para operações anulação, sucessiva Estado Olá Olá réplica back tooa estável ponto. Uma diferença importante de notificações de anulação é que são agregados eventos que tenham chaves duplicadas. Por exemplo, se está a ser anulada transação T1, verá uma notificação único tooDelete(X).

## <a name="next-steps"></a>Passos seguintes
* [Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Início rápido de serviços fiável](service-fabric-reliable-services-quick-start.md)
* [Reliable Services de cópia de segurança e restaurar (recuperação após desastre)](service-fabric-reliable-services-backup-restore.md)
* [Referência para programadores para coleções fiável](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

