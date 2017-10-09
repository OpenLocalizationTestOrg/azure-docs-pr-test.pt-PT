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
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="1a1fb-103">Depuração utilizando o diagrama de tarefa Olá condicionada por dados</span><span class="sxs-lookup"><span data-stu-id="1a1fb-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="1a1fb-104">Diagrama de tarefa Olá no Olá **monitorização** painel no portal do Azure de Olá pode ajudar a visualizar o pipeline de tarefa.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="1a1fb-105">Mostra entradas, saídas e passos de consulta.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="1a1fb-106">Pode utilizar as métricas diagrama Olá tarefa tooexamine Olá para cada passo, toomore Isole rapidamente origem Olá de um problema ao resolver problemas.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="1a1fb-107">Diagrama de tarefa Olá a utilizar</span><span class="sxs-lookup"><span data-stu-id="1a1fb-107">Using hello job diagram</span></span>

<span data-ttu-id="1a1fb-108">No portal do Azure, de Olá enquanto uma tarefa de Stream Analytics, sob **suporte + resolução de problemas**, selecione **diagrama de tarefa**:</span><span class="sxs-lookup"><span data-stu-id="1a1fb-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagrama de tarefa com a métrica - localização](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="1a1fb-110">Selecione cada consulta passo toosee Olá secção correspondente uma painel de edição de consultas.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="1a1fb-111">Um gráfico de métrico para o passo de Olá é apresentado na página Olá um painel inferior.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![Diagrama de tarefa com a métrica - tarefa básico](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="1a1fb-113">Selecione as partições de Olá toosee da entrada de Event Hubs do Azure Olá, **...**</span><span class="sxs-lookup"><span data-stu-id="1a1fb-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="1a1fb-114">É apresentado um menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-114">A context menu appears.</span></span> <span data-ttu-id="1a1fb-115">Também pode ver fusão Olá de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-115">You also can see hello input merger.</span></span>

![Diagrama de tarefa com a métrica - expanda partição](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="1a1fb-117">gráfico de hora métrica do Olá toosee para apenas uma única partição, o nó de partição Olá selecione.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="1a1fb-118">métricas de Olá são apresentadas em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-118">hello metrics are shown at hello bottom of hello page.</span></span>

![Diagrama de tarefa com a métrica - as métricas mais](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="1a1fb-120">gráfico de métricas de Olá toosee para uma fusão, o nó de fusão Olá selecione.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="1a1fb-121">Olá gráfico a seguir mostra que não há eventos foram removidos ou ajustados.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![Diagrama de tarefa com a métrica - grelha](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="1a1fb-123">detalhes de Olá toosee do valor métrico de Olá e a hora, toohello de ponto de gráfico.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![Diagrama com a métrica de tarefa - coloque o cursor](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="1a1fb-125">Resolver problemas utilizando as métricas</span><span class="sxs-lookup"><span data-stu-id="1a1fb-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="1a1fb-126">Olá **QueryLastProcessedTime** métrica indica que um passo específico recebeu dados.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="1a1fb-127">Ao observar a topologia de Olá, pode trabalhar trás do Olá saída processador toosee qual passo não está a receber dados.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="1a1fb-128">Se um passo não está a obter dados, vá passo de consulta toohello imediatamente antes da mesma.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="1a1fb-129">Verifique se hello passo consulta anterior tenha uma janela de tempo e, se houver tempo suficiente foi efectuada com êxito para o mesmo toooutput dados.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="1a1fb-130">(Tenha em atenção que tempo windows são hora toohello ajustado.)</span><span class="sxs-lookup"><span data-stu-id="1a1fb-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="1a1fb-131">Se hello passo consulta anterior é um processador de entrada, utilize Olá resposta Olá métricas entrada toohelp seguintes perguntas de destino.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="1a1fb-132">Podem ajudar a determinar se uma tarefa está a obter dados da sua origem de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="1a1fb-133">Se a consulta de Olá está particionada, examine cada partição.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="1a1fb-134">Quantidade de dados está a ser lido?</span><span class="sxs-lookup"><span data-stu-id="1a1fb-134">How much data is being read?</span></span>

*   <span data-ttu-id="1a1fb-135">**InputEventsSourcesTotal** é Olá número de unidades de dados de leitura.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="1a1fb-136">Por exemplo, Olá número de blobs.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="1a1fb-137">**InputEventsTotal** é Olá número de eventos de leitura.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="1a1fb-138">Esta métrica está disponível por partição.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="1a1fb-139">**InputEventsInBytesTotal** é Olá número de bytes lidos.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="1a1fb-140">**InputEventsLastArrivalTime** é atualizado com a hora de colocados em fila de todos os eventos recebidos.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="1a1fb-141">Tempo está a mover reencaminhar?</span><span class="sxs-lookup"><span data-stu-id="1a1fb-141">Is time moving forward?</span></span> <span data-ttu-id="1a1fb-142">Se real eventos são lidos, pontuação não pode ser emitida.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="1a1fb-143">**InputEventsLastPunctuationTime** indica quando foi emitida uma pontuação tookeep tempo mover reencaminhar.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="1a1fb-144">Se pontuação não é emitida, o fluxo de dados pode obter bloqueado.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="1a1fb-145">Existem erros na entrada de Olá?</span><span class="sxs-lookup"><span data-stu-id="1a1fb-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="1a1fb-146">**InputEventsEventDataNullTotal** é uma contagem de eventos que tenham dados nulo.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="1a1fb-147">**InputEventsSerializerErrorsTotal** é uma contagem dos eventos que não foi anulada corretamente.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="1a1fb-148">**InputEventsDegradedTotal** é uma contagem dos eventos que tenha tido um problema diferente com a anulação da serialização.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="1a1fb-149">São eventos que está a ser removidos ou ajustados?</span><span class="sxs-lookup"><span data-stu-id="1a1fb-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="1a1fb-150">**InputEventsEarlyTotal** é Olá número de eventos que tenham um carimbo de aplicação antes de marca d'água alta Olá.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="1a1fb-151">**InputEventsLateTotal** é Olá número de eventos que tenham uma aplicação timestamp depois marca d'água alta Olá.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="1a1fb-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** é eventos número Olá removidos antes da hora de início da tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="1a1fb-153">São iremos baixar ao ler os dados?</span><span class="sxs-lookup"><span data-stu-id="1a1fb-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="1a1fb-154">**InputEventsSourcesBackloggedTotal** indica quantos mais mensagens necessita toobe ler entradas de IoT Hub do Azure e Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="1a1fb-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="1a1fb-155">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="1a1fb-155">Get help</span></span>
<span data-ttu-id="1a1fb-156">Para obter assistência adicional, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="1a1fb-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a1fb-157">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1a1fb-157">Next steps</span></span>
* [<span data-ttu-id="1a1fb-158">Introdução tooStream análise</span><span class="sxs-lookup"><span data-stu-id="1a1fb-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1a1fb-159">Introdução ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a1fb-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1a1fb-160">Dimensionar tarefas do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a1fb-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1a1fb-161">Referência de linguagem de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a1fb-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1a1fb-162">Referência da REST API de gestão de análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="1a1fb-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
