---
title: "AAA Azure Stream Analytics condicionada por dados depuração utilizando o diagrama de tarefa Olá | Microsoft Docs"
description: "Resolver problemas relacionados com a sua tarefa do Stream Analytics utilizando o diagrama de tarefa Olá e métricas."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>Depuração utilizando o diagrama de tarefa Olá condicionada por dados

Diagrama de tarefa Olá no Olá **monitorização** painel no portal do Azure de Olá pode ajudar a visualizar o pipeline de tarefa. Mostra entradas, saídas e passos de consulta. Pode utilizar as métricas diagrama Olá tarefa tooexamine Olá para cada passo, toomore Isole rapidamente origem Olá de um problema ao resolver problemas.

## <a name="using-hello-job-diagram"></a>Diagrama de tarefa Olá a utilizar

No portal do Azure, de Olá enquanto uma tarefa de Stream Analytics, sob **suporte + resolução de problemas**, selecione **diagrama de tarefa**:

![Diagrama de tarefa com a métrica - localização](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Selecione cada consulta passo toosee Olá secção correspondente uma painel de edição de consultas. Um gráfico de métrico para o passo de Olá é apresentado na página Olá um painel inferior.

![Diagrama de tarefa com a métrica - tarefa básico](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

Selecione as partições de Olá toosee da entrada de Event Hubs do Azure Olá, **...** É apresentado um menu de contexto. Também pode ver fusão Olá de entrada.

![Diagrama de tarefa com a métrica - expanda partição](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

gráfico de hora métrica do Olá toosee para apenas uma única partição, o nó de partição Olá selecione. métricas de Olá são apresentadas em Olá parte inferior da página Olá.

![Diagrama de tarefa com a métrica - as métricas mais](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

gráfico de métricas de Olá toosee para uma fusão, o nó de fusão Olá selecione. Olá gráfico a seguir mostra que não há eventos foram removidos ou ajustados.

![Diagrama de tarefa com a métrica - grelha](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

detalhes de Olá toosee do valor métrico de Olá e a hora, toohello de ponto de gráfico.

![Diagrama com a métrica de tarefa - coloque o cursor](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Resolver problemas utilizando as métricas

Olá **QueryLastProcessedTime** métrica indica que um passo específico recebeu dados. Ao observar a topologia de Olá, pode trabalhar trás do Olá saída processador toosee qual passo não está a receber dados. Se um passo não está a obter dados, vá passo de consulta toohello imediatamente antes da mesma. Verifique se hello passo consulta anterior tenha uma janela de tempo e, se houver tempo suficiente foi efectuada com êxito para o mesmo toooutput dados. (Tenha em atenção que tempo windows são hora toohello ajustado.)
 
Se hello passo consulta anterior é um processador de entrada, utilize Olá resposta Olá métricas entrada toohelp seguintes perguntas de destino. Podem ajudar a determinar se uma tarefa está a obter dados da sua origem de entrada. Se a consulta de Olá está particionada, examine cada partição.
 
### <a name="how-much-data-is-being-read"></a>Quantidade de dados está a ser lido?

*   **InputEventsSourcesTotal** é Olá número de unidades de dados de leitura. Por exemplo, Olá número de blobs.
*   **InputEventsTotal** é Olá número de eventos de leitura. Esta métrica está disponível por partição.
*   **InputEventsInBytesTotal** é Olá número de bytes lidos.
*   **InputEventsLastArrivalTime** é atualizado com a hora de colocados em fila de todos os eventos recebidos.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>Tempo está a mover reencaminhar? Se real eventos são lidos, pontuação não pode ser emitida.

*   **InputEventsLastPunctuationTime** indica quando foi emitida uma pontuação tookeep tempo mover reencaminhar. Se pontuação não é emitida, o fluxo de dados pode obter bloqueado.
 
### <a name="are-there-any-errors-in-hello-input"></a>Existem erros na entrada de Olá?

*   **InputEventsEventDataNullTotal** é uma contagem de eventos que tenham dados nulo.
*   **InputEventsSerializerErrorsTotal** é uma contagem dos eventos que não foi anulada corretamente.
*   **InputEventsDegradedTotal** é uma contagem dos eventos que tenha tido um problema diferente com a anulação da serialização.
 
### <a name="are-events-being-dropped-or-adjusted"></a>São eventos que está a ser removidos ou ajustados?

*   **InputEventsEarlyTotal** é Olá número de eventos que tenham um carimbo de aplicação antes de marca d'água alta Olá.
*   **InputEventsLateTotal** é Olá número de eventos que tenham uma aplicação timestamp depois marca d'água alta Olá.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** é eventos número Olá removidos antes da hora de início da tarefa de Olá.
 
### <a name="are-we-falling-behind-in-reading-data"></a>São iremos baixar ao ler os dados?

*   **InputEventsSourcesBackloggedTotal** indica quantos mais mensagens necessita toobe ler entradas de IoT Hub do Azure e Hubs de eventos.


## <a name="get-help"></a>Obter ajuda
Para obter assistência adicional, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooStream análise](stream-analytics-introduction.md)
* [Introdução ao Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar tarefas do Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência de linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da REST API de gestão de análise de fluxo](https://msdn.microsoft.com/library/azure/dn835031.aspx)
