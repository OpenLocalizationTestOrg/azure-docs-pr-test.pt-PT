---
title: aaaDebug Azure Stream Analytics com recetores do hub de eventos | Microsoft Docs
description: "Consultar as melhores práticas para a consideração dos grupos de consumidores de Event Hubs nas tarefas do Stream Analytics."
keywords: limite de hub de eventos, grupo de consumidores
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="1b8ed-104">Depurar o Azure Stream Analytics com recetores do hub de eventos</span><span class="sxs-lookup"><span data-stu-id="1b8ed-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="1b8ed-105">Pode utilizar Event Hubs do Azure no Azure Stream Analytics tooingest ou saída dados de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="1b8ed-106">Uma melhor prática para utilizar Event Hubs é toouse vários grupos de consumidores, tooensure escalabilidade de tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="1b8ed-107">Uma razão é que o número de Olá de leitores na tarefa de Stream Analytics Olá para uma introdução específica afetará número de Olá de leitores num grupo de consumidores único.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="1b8ed-108">detalhes de implementação interno para a lógica da topologia de escalamento horizontal de Olá baseia Olá preciso diversas recetores.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="1b8ed-109">número de Olá de recetores não está exposto externamente.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="1b8ed-110">número de Olá de leitores pode alterar a hora de início de tarefa Olá ou durante as atualizações de tarefa.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="1b8ed-111">Quando o número de Olá de leitores for alterada durante uma atualização de tarefa, avisos transitórios são escritos tooaudit registos.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="1b8ed-112">Tarefas do Stream Analytics recuperar automaticamente a partir destes problemas transitórios.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="1b8ed-113">Número de leitores por partição excede o limite de Event Hubs cinco</span><span class="sxs-lookup"><span data-stu-id="1b8ed-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="1b8ed-114">Cenários em que Olá número de leitores por partição excede o limite de Event Hubs Olá cinco incluem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="1b8ed-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="1b8ed-115">Múltiplas instruções SELECIONADAS: Se utilizar várias instruções que se referem demasiado**mesmo** hub de eventos de entrada, cada instrução SELECIONADA faz com que um toobe recetor nova criada.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="1b8ed-116">UNION: Ao utilizar uma União, é possível toohave várias entradas que se referem toohello **mesmo** grupo hub e consumidores de eventos.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="1b8ed-117">ASSOCIAÇÃO automática: Ao utilizar uma operação de associação automática, é possível toorefer toohello **mesmo** hub de eventos várias vezes.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="1b8ed-118">Solução</span><span class="sxs-lookup"><span data-stu-id="1b8ed-118">Solution</span></span>

<span data-ttu-id="1b8ed-119">Olá melhores práticas seguintes podem ajudar a mitigar cenários em que Olá número de leitores por partição excede o limite de Event Hubs Olá cinco.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="1b8ed-120">Dividir a sua consulta em vários passos, utilizando uma cláusula WITH</span><span class="sxs-lookup"><span data-stu-id="1b8ed-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="1b8ed-121">cláusula WITH de Olá Especifica um conjunto de resultados com nome temporária que pode ser referenciado por uma cláusula FROM na consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="1b8ed-122">É possível definir a cláusula WITH de Olá no âmbito da execução Olá de uma única instrução SELECT.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="1b8ed-123">Por exemplo, em vez desta consulta:</span><span class="sxs-lookup"><span data-stu-id="1b8ed-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="1b8ed-124">Utilize esta consulta:</span><span class="sxs-lookup"><span data-stu-id="1b8ed-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="1b8ed-125">Certifique-se de que as entradas vincular toodifferent grupos de consumidores</span><span class="sxs-lookup"><span data-stu-id="1b8ed-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="1b8ed-126">Para consultas no qual três ou mais entradas estão ligado toohello consumidores de Event Hubs mesmo grupo, criar grupos de consumidores separado.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="1b8ed-127">Isto requer a criação de Olá de entradas de Stream Analytics adicionais.</span><span class="sxs-lookup"><span data-stu-id="1b8ed-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="1b8ed-128">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="1b8ed-128">Get help</span></span>
<span data-ttu-id="1b8ed-129">Para obter assistência adicional, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="1b8ed-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b8ed-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1b8ed-130">Next steps</span></span>
* [<span data-ttu-id="1b8ed-131">Introdução tooStream análise</span><span class="sxs-lookup"><span data-stu-id="1b8ed-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1b8ed-132">Introdução ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1b8ed-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1b8ed-133">Dimensionar tarefas do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1b8ed-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1b8ed-134">Referência de linguagem de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1b8ed-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1b8ed-135">Referência da REST API de gestão de análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="1b8ed-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
