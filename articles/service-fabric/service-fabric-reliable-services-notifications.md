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
# <a name="reliable-services-notifications"></a><span data-ttu-id="19750-103">Notificações de serviços fiáveis</span><span class="sxs-lookup"><span data-stu-id="19750-103">Reliable Services notifications</span></span>
<span data-ttu-id="19750-104">Notificações de permitir que os clientes alterações de Olá tootrack que estão a ser efetuadas tooan objeto que o se estiverem interessados em.</span><span class="sxs-lookup"><span data-stu-id="19750-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="19750-105">Notificações de suportam dois tipos de objetos: *fiável Gestor de estado* e *dicionário fiável*.</span><span class="sxs-lookup"><span data-stu-id="19750-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="19750-106">Os motivos mais comuns para utilizar as notificações são:</span><span class="sxs-lookup"><span data-stu-id="19750-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="19750-107">Edifício materializada vistas, tais como índices secundários ou vistas filtradas de estado da réplica Olá agregadas.</span><span class="sxs-lookup"><span data-stu-id="19750-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="19750-108">Um exemplo é um índice ordenado de todas as chaves no dicionário fiável.</span><span class="sxs-lookup"><span data-stu-id="19750-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="19750-109">Enviar dados de monitorização, como o número de Olá de utilizadores adicionadas no Olá última hora.</span><span class="sxs-lookup"><span data-stu-id="19750-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="19750-110">As notificações são desencadeadas como parte da aplicação de operações.</span><span class="sxs-lookup"><span data-stu-id="19750-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="19750-111">Devido a que, notificações devem ser processadas como rápido eventos possíveis e síncronos não devem incluir quaisquer operações dispendiosas.</span><span class="sxs-lookup"><span data-stu-id="19750-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="19750-112">Notificações do Gestor de estado de fiável</span><span class="sxs-lookup"><span data-stu-id="19750-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="19750-113">O Gestor de estado de fiável fornece notificações para Olá seguintes eventos:</span><span class="sxs-lookup"><span data-stu-id="19750-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="19750-114">Transação</span><span class="sxs-lookup"><span data-stu-id="19750-114">Transaction</span></span>
  * <span data-ttu-id="19750-115">Consolidação</span><span class="sxs-lookup"><span data-stu-id="19750-115">Commit</span></span>
* <span data-ttu-id="19750-116">Gestor de estado</span><span class="sxs-lookup"><span data-stu-id="19750-116">State manager</span></span>
  * <span data-ttu-id="19750-117">Reconstrução</span><span class="sxs-lookup"><span data-stu-id="19750-117">Rebuild</span></span>
  * <span data-ttu-id="19750-118">Adição de um Estado fiável</span><span class="sxs-lookup"><span data-stu-id="19750-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="19750-119">Remoção de um Estado de fiável</span><span class="sxs-lookup"><span data-stu-id="19750-119">Removal of a reliable state</span></span>

<span data-ttu-id="19750-120">Gestor de estado de fiável controla as de transações Olá atual em utilização.</span><span class="sxs-lookup"><span data-stu-id="19750-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="19750-121">alteração apenas da Olá num Estado de transação que faz com que um toobe notificação desencadeado é uma transação ser consolidada.</span><span class="sxs-lookup"><span data-stu-id="19750-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="19750-122">Gestor de estado de fiável mantém uma coleção de Estados fiáveis como dicionário fiável e fiável de fila.</span><span class="sxs-lookup"><span data-stu-id="19750-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="19750-123">Gestor de estado de fiável desencadeado notificações quando as alterações esta coleção: um Estado fiável é adicionado ou removido, ou o conjunto completo de Olá for reconstruído.</span><span class="sxs-lookup"><span data-stu-id="19750-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="19750-124">Olá coleção do Gestor de estado fiável for reconstruído em três casos:</span><span class="sxs-lookup"><span data-stu-id="19750-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="19750-125">Recuperação: Quando uma réplica é iniciado,-recupera o estado anterior do disco de Olá.</span><span class="sxs-lookup"><span data-stu-id="19750-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="19750-126">No final de Olá de recuperação, utiliza **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de Olá dos Estados fiáveis recuperados.</span><span class="sxs-lookup"><span data-stu-id="19750-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="19750-127">Total de cópia: antes de uma réplica pode associar conjunto de configurações de Olá, tem toobe incorporada.</span><span class="sxs-lookup"><span data-stu-id="19750-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="19750-128">Por vezes, isto requer uma cópia completa do Estado de fiável do Gestor de estado de Olá réplica primária toobe toohello aplicados inativo réplica secundária.</span><span class="sxs-lookup"><span data-stu-id="19750-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="19750-129">Gestor de estado de fiável Olá réplica secundária utiliza **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de Olá fiáveis de Estados de que que adquiriu a partir da réplica primária Olá.</span><span class="sxs-lookup"><span data-stu-id="19750-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="19750-130">Restauro: Em cenários de recuperação após desastre, estado da réplica Olá pode ser restaurado a partir de uma cópia de segurança através de **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="19750-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="19750-131">Nestes casos, utiliza fiável Gestor de estado na réplica primária Olá **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de Olá fiáveis de Estados de que restaurada a partir de cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="19750-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="19750-132">tooregister para notificações de transação e/ou notificações do Gestor de estado, terá de tooregister com Olá **TransactionChanged** ou **StateManagerChanged** eventos no Gestor de estado fiável.</span><span class="sxs-lookup"><span data-stu-id="19750-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="19750-133">Um local comum tooregister com estes processadores de eventos é construtor Olá do seu serviço de monitorização de estado.</span><span class="sxs-lookup"><span data-stu-id="19750-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="19750-134">Quando registar o construtor de Olá, não irá perder as notificações que é causada por uma alteração durante a duração de Olá de **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="19750-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="19750-135">Olá **TransactionChanged** utiliza o processador de eventos **NotifyTransactionChangedEventArgs** tooprovide detalhes sobre o evento de Olá.</span><span class="sxs-lookup"><span data-stu-id="19750-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="19750-136">Contém a propriedade de ação de Olá (por exemplo, **NotifyTransactionChangedAction.Commit**) que especifica o tipo de Olá de alteração.</span><span class="sxs-lookup"><span data-stu-id="19750-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="19750-137">Também contém a propriedade transaction Olá que fornece uma transação de toohello de referência que foi alterado.</span><span class="sxs-lookup"><span data-stu-id="19750-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="19750-138">Hoje em dia, **TransactionChanged** eventos são gerados apenas se a transação de Olá está consolidada.</span><span class="sxs-lookup"><span data-stu-id="19750-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="19750-139">Olá ação é, em seguida, igual demasiado**NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="19750-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="19750-140">Mas no Olá futura, eventos poderão ser gerados para outros tipos de transação de alterações de estado.</span><span class="sxs-lookup"><span data-stu-id="19750-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="19750-141">Recomendamos a verificar a ação de Olá e processar o evento de Olá apenas se for um que espera.</span><span class="sxs-lookup"><span data-stu-id="19750-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="19750-142">Segue-se um exemplo **TransactionChanged** processador de eventos.</span><span class="sxs-lookup"><span data-stu-id="19750-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="19750-143">Olá **StateManagerChanged** utiliza o processador de eventos **NotifyStateManagerChangedEventArgs** tooprovide detalhes sobre o evento de Olá.</span><span class="sxs-lookup"><span data-stu-id="19750-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="19750-144">**NotifyStateManagerChangedEventArgs** tem dois subclasses: **NotifyStateManagerRebuildEventArgs** e **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="19750-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="19750-145">Utilizar a propriedade de ação de Olá no **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** subclasse correto toohello:</span><span class="sxs-lookup"><span data-stu-id="19750-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="19750-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="19750-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="19750-147">**NotifyStateManagerChangedAction.Add** e **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="19750-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="19750-148">Segue-se um exemplo **StateManagerChanged** processador de notificação.</span><span class="sxs-lookup"><span data-stu-id="19750-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="19750-149">Notificações de dicionário fiáveis</span><span class="sxs-lookup"><span data-stu-id="19750-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="19750-150">Dicionário fiável fornece notificações para Olá seguintes eventos:</span><span class="sxs-lookup"><span data-stu-id="19750-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="19750-151">A reconstrução: Chamado quando **ReliableDictionary** recuperou o estado de uma cópia de segurança ou recuperado ou copiado de estado local.</span><span class="sxs-lookup"><span data-stu-id="19750-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="19750-152">Limpar: Chamado quando Olá estado **ReliableDictionary** foi limpo através de Olá **ClearAsync** método.</span><span class="sxs-lookup"><span data-stu-id="19750-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="19750-153">Adicione: Chamado quando um item foi adicionado demasiado**ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="19750-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="19750-154">Atualização: Chamado quando um item na **IReliableDictionary** foi atualizada.</span><span class="sxs-lookup"><span data-stu-id="19750-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="19750-155">Remover: Chamado quando um item na **IReliableDictionary** foi eliminado.</span><span class="sxs-lookup"><span data-stu-id="19750-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="19750-156">notificações de dicionário fiável tooget, terá de tooregister com Olá **DictionaryChanged** processador de eventos no **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="19750-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="19750-157">Um local comum tooregister com estes processadores de eventos está a ser Olá **ReliableStateManager.StateManagerChanged** adicionar notificação.</span><span class="sxs-lookup"><span data-stu-id="19750-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="19750-158">Registar quando **IReliableDictionary** é adicionada demasiado**IReliableStateManager** garante que não irá perder quaisquer notificações.</span><span class="sxs-lookup"><span data-stu-id="19750-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="19750-159">**ProcessStateManagerSingleEntityNotification** é o método de exemplo de Olá esse Olá anterior **OnStateManagerChangedHandler** chamadas de exemplo.</span><span class="sxs-lookup"><span data-stu-id="19750-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="19750-160">Olá código anterior define Olá **IReliableNotificationAsyncCallback** interface, along com **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="19750-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="19750-161">Porque **NotifyDictionaryRebuildEventArgs** contém um **IAsyncEnumerable** interface – que têm de toobe enumerado de forma assíncrona - notificações de reconstrução são desencadeadas através de  **RebuildNotificationAsyncCallback** em vez de **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="19750-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="19750-162">No Olá precedente código, como parte do processamento de notificação de reconstrução Olá Olá primeiro mantida Estado agregado está desmarcado.</span><span class="sxs-lookup"><span data-stu-id="19750-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="19750-163">Porque a coleção fiável Olá está a ser reconstruída com um Estado de novo, todas as notificações anteriores são irrelevantes.</span><span class="sxs-lookup"><span data-stu-id="19750-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="19750-164">Olá **DictionaryChanged** utiliza o processador de eventos **NotifyDictionaryChangedEventArgs** tooprovide detalhes sobre o evento de Olá.</span><span class="sxs-lookup"><span data-stu-id="19750-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="19750-165">**NotifyDictionaryChangedEventArgs** tem cinco subclasses.</span><span class="sxs-lookup"><span data-stu-id="19750-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="19750-166">Utilize a propriedade ação Olá **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** subclasse correto toohello:</span><span class="sxs-lookup"><span data-stu-id="19750-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="19750-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="19750-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="19750-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="19750-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="19750-169">**NotifyDictionaryChangedAction.Add** e **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="19750-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="19750-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="19750-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="19750-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="19750-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="19750-172">Recomendações</span><span class="sxs-lookup"><span data-stu-id="19750-172">Recommendations</span></span>
* <span data-ttu-id="19750-173">*Efetue* concluir mais rápido possíveis eventos de notificação.</span><span class="sxs-lookup"><span data-stu-id="19750-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="19750-174">*Não* executar quaisquer operações dispendiosas (por exemplo, operações de e/s) como parte dos eventos síncronos.</span><span class="sxs-lookup"><span data-stu-id="19750-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="19750-175">*Efetue* verificar o tipo de ação de Olá antes de processar o evento de Olá.</span><span class="sxs-lookup"><span data-stu-id="19750-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="19750-176">Novos tipos de ação podem ser adicionados em Olá futura.</span><span class="sxs-lookup"><span data-stu-id="19750-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="19750-177">Eis algumas coisas tookeep em mente:</span><span class="sxs-lookup"><span data-stu-id="19750-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="19750-178">As notificações são desencadeadas como parte da execução de Olá de uma operação.</span><span class="sxs-lookup"><span data-stu-id="19750-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="19750-179">Por exemplo, uma notificação de restauro é desencadeada como último passo de Olá de uma operação de restauro.</span><span class="sxs-lookup"><span data-stu-id="19750-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="19750-180">Um restauro não será concluída até que o evento de notificação de Olá é processado.</span><span class="sxs-lookup"><span data-stu-id="19750-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="19750-181">Porque as notificações são desencadeadas como parte da Olá aplicando operações, os clientes ver apenas as notificações para operações localmente consolidadas.</span><span class="sxs-lookup"><span data-stu-id="19750-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="19750-182">E porque operações garantidas apenas toobe consolidada localmente (por outras palavras, tem sessão iniciada), podem ou não pode ser anuladas no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="19750-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="19750-183">No caminho de Refazer Olá, uma única notificação é desencadeada para cada operação aplicada.</span><span class="sxs-lookup"><span data-stu-id="19750-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="19750-184">Isto significa que, se a transação T1 inclui Create(X), Delete(X) e Create(X), irá obter uma notificação para Olá criação de X, para eliminação de Olá e um para a criação de Olá novamente, por essa ordem.</span><span class="sxs-lookup"><span data-stu-id="19750-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="19750-185">Para transações que contêm várias operações, operações são aplicadas por ordem de Olá em que foram recebidos na réplica primária do Olá de utilizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="19750-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="19750-186">Como parte do processamento de progresso FALSO, algumas operações podem ser anuladas.</span><span class="sxs-lookup"><span data-stu-id="19750-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="19750-187">As notificações são geradas para operações anulação, sucessiva Estado Olá Olá réplica back tooa estável ponto.</span><span class="sxs-lookup"><span data-stu-id="19750-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="19750-188">Uma diferença importante de notificações de anulação é que são agregados eventos que tenham chaves duplicadas.</span><span class="sxs-lookup"><span data-stu-id="19750-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="19750-189">Por exemplo, se está a ser anulada transação T1, verá uma notificação único tooDelete(X).</span><span class="sxs-lookup"><span data-stu-id="19750-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="19750-190">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="19750-190">Next steps</span></span>
* [<span data-ttu-id="19750-191">Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="19750-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="19750-192">Início rápido de serviços fiável</span><span class="sxs-lookup"><span data-stu-id="19750-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="19750-193">Reliable Services de cópia de segurança e restaurar (recuperação após desastre)</span><span class="sxs-lookup"><span data-stu-id="19750-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="19750-194">Referência para programadores para coleções fiável</span><span class="sxs-lookup"><span data-stu-id="19750-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

