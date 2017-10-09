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
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Depurar o Azure Stream Analytics com recetores do hub de eventos

Pode utilizar Event Hubs do Azure no Azure Stream Analytics tooingest ou saída dados de uma tarefa. Uma melhor prática para utilizar Event Hubs é toouse vários grupos de consumidores, tooensure escalabilidade de tarefa. Uma razão é que o número de Olá de leitores na tarefa de Stream Analytics Olá para uma introdução específica afetará número de Olá de leitores num grupo de consumidores único. detalhes de implementação interno para a lógica da topologia de escalamento horizontal de Olá baseia Olá preciso diversas recetores. número de Olá de recetores não está exposto externamente. número de Olá de leitores pode alterar a hora de início de tarefa Olá ou durante as atualizações de tarefa.

> [!NOTE]
> Quando o número de Olá de leitores for alterada durante uma atualização de tarefa, avisos transitórios são escritos tooaudit registos. Tarefas do Stream Analytics recuperar automaticamente a partir destes problemas transitórios.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>Número de leitores por partição excede o limite de Event Hubs cinco

Cenários em que Olá número de leitores por partição excede o limite de Event Hubs Olá cinco incluem o seguinte Olá:

* Múltiplas instruções SELECIONADAS: Se utilizar várias instruções que se referem demasiado**mesmo** hub de eventos de entrada, cada instrução SELECIONADA faz com que um toobe recetor nova criada.
* UNION: Ao utilizar uma União, é possível toohave várias entradas que se referem toohello **mesmo** grupo hub e consumidores de eventos.
* ASSOCIAÇÃO automática: Ao utilizar uma operação de associação automática, é possível toorefer toohello **mesmo** hub de eventos várias vezes.

## <a name="solution"></a>Solução

Olá melhores práticas seguintes podem ajudar a mitigar cenários em que Olá número de leitores por partição excede o limite de Event Hubs Olá cinco.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>Dividir a sua consulta em vários passos, utilizando uma cláusula WITH

cláusula WITH de Olá Especifica um conjunto de resultados com nome temporária que pode ser referenciado por uma cláusula FROM na consulta de Olá. É possível definir a cláusula WITH de Olá no âmbito da execução Olá de uma única instrução SELECT.

Por exemplo, em vez desta consulta:

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Utilize esta consulta:

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

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>Certifique-se de que as entradas vincular toodifferent grupos de consumidores

Para consultas no qual três ou mais entradas estão ligado toohello consumidores de Event Hubs mesmo grupo, criar grupos de consumidores separado. Isto requer a criação de Olá de entradas de Stream Analytics adicionais.


## <a name="get-help"></a>Obter ajuda
Para obter assistência adicional, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooStream análise](stream-analytics-introduction.md)
* [Introdução ao Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar tarefas do Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência de linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da REST API de gestão de análise de fluxo](https://msdn.microsoft.com/library/azure/dn835031.aspx)
