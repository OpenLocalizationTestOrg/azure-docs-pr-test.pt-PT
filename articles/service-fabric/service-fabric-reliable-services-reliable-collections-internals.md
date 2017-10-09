---
title: "aaaAzure características de Gestor de estado do serviço de recursos de infraestrutura fiável e fiável de coleção | Microsoft Docs"
description: "Descrição profunda sobre conceitos de coleção fiável e estrutura no Service Fabric do Azure."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="d6268-103">Características de Gestor de estado de fiável de recursos de infraestrutura de serviço do Azure e fiável de coleção</span><span class="sxs-lookup"><span data-stu-id="d6268-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="d6268-104">Este documento delves no interior do Gestor de estado fiável e coleções fiável toosee como funcionam os componentes principais em segundo plano de Olá.</span><span class="sxs-lookup"><span data-stu-id="d6268-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="d6268-105">Este documento é trabalho em curso.</span><span class="sxs-lookup"><span data-stu-id="d6268-105">This document is work in-progress.</span></span> <span data-ttu-id="d6268-106">Adicionar comentários toothis artigo tootell-nos que tópico que gostaria de mais informações sobre toolearn.</span><span class="sxs-lookup"><span data-stu-id="d6268-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="d6268-107">Modelo de persistência local: registo e ponto de verificação</span><span class="sxs-lookup"><span data-stu-id="d6268-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="d6268-108">Olá fiável Gestor de estado e coleções fiável siga um modelo de persistência que é chamado registo e ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="d6268-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="d6268-109">Neste modelo, cada alteração de estado é registada no disco pela primeira vez e, em seguida, aplicada na memória.</span><span class="sxs-lookup"><span data-stu-id="d6268-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="d6268-110">Estado de conclusão de Olá próprio é persistente apenas ocasionalmente (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="d6268-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="d6268-111">Ponto de verificação).</span><span class="sxs-lookup"><span data-stu-id="d6268-111">Checkpoint).</span></span>
<span data-ttu-id="d6268-112">benefício de Olá é que deltas transformados sequenciais acrescentar apenas operações de escrita no disco para um melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="d6268-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="d6268-113">toobetter compreender Olá registo e o modelo de ponto de verificação, vamos ver pela primeira vez no cenário de disco infinita Olá.</span><span class="sxs-lookup"><span data-stu-id="d6268-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="d6268-114">Olá fiável Gestor de estado os registos de cada operação está a replicar.</span><span class="sxs-lookup"><span data-stu-id="d6268-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="d6268-115">Registo permite-operação de Olá Olá coleções fiável tooapply apenas na memória.</span><span class="sxs-lookup"><span data-stu-id="d6268-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="d6268-116">Uma vez que os registos são mantidos, mesmo quando a réplica Olá falha e precisa de toobe reiniciado, Olá fiável Gestor de estado tem informações suficientes no respetivo registo tooreplay todas as operações de Olá perdeu-se a réplica de Olá.</span><span class="sxs-lookup"><span data-stu-id="d6268-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="d6268-117">Como disco de Olá é infinito, registos nunca precisam de toobe removido e hello fiável necessita de estado do toomanage apenas Olá dentro da memória.</span><span class="sxs-lookup"><span data-stu-id="d6268-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="d6268-118">Agora vamos ver cenário de Olá de disco finito.</span><span class="sxs-lookup"><span data-stu-id="d6268-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="d6268-119">Conforme registos acumularem, Olá fiável Gestor de estado irá executar sem espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="d6268-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="d6268-120">Antes do que acontece, Olá fiável Gestor de estado tem tootruncate sala de toomake respetivo registo para os registos de Olá mais recentes.</span><span class="sxs-lookup"><span data-stu-id="d6268-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="d6268-121">Pedidos de Gestor de estado de fiável Olá coleções fiável toocheckpoint toodisk respetivo estado na memória.</span><span class="sxs-lookup"><span data-stu-id="d6268-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="d6268-122">Neste momento, coleções fiável Olá seria manter o estado de memória.</span><span class="sxs-lookup"><span data-stu-id="d6268-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="d6268-123">Depois de coleções fiável Olá concluir os respetivos pontos de verificação, Olá fiável Gestor de estado pode truncar Olá registo toofree espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="d6268-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="d6268-124">Quando a réplica de Olá tem toobe reiniciado, coleções fiável recuperar o respetivo estado checkpointed e hello fiável Gestor de estado recupera e reproduz todas as alterações de estado de Olá que ocorreram desde o último ponto de verificação Olá.</span><span class="sxs-lookup"><span data-stu-id="d6268-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="d6268-125">Adicionar outro valor de ponto de verificação é o que melhora os tempos de recuperação em cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="d6268-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="d6268-126">Registo contém todas as operações que ocorreram desde o último ponto de verificação Olá.</span><span class="sxs-lookup"><span data-stu-id="d6268-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="d6268-127">Por isso,-pode incluir várias versões de um item como vários valores para uma linha fornecido no dicionário fiável.</span><span class="sxs-lookup"><span data-stu-id="d6268-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="d6268-128">Em contrapartida, pontos de verificação uma coleção fiável Olá apenas a versão mais recente de cada valor de uma chave.</span><span class="sxs-lookup"><span data-stu-id="d6268-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6268-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d6268-129">Next steps</span></span>
* [<span data-ttu-id="d6268-130">Transações e bloqueios</span><span class="sxs-lookup"><span data-stu-id="d6268-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

