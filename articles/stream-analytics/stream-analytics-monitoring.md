---
title: "aaaUnderstanding monitorização de tarefa do Stream Analytics | Microsoft Docs"
description: "Noções sobre monitorização de tarefa do Stream Analytics"
keywords: monitor de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="fe906-104">Compreender a monitorização de tarefa do Stream Analytics e como toomonitor consultas</span><span class="sxs-lookup"><span data-stu-id="fe906-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="fe906-105">Introdução: página de monitor de Olá</span><span class="sxs-lookup"><span data-stu-id="fe906-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="fe906-106">Olá ambos superfície métricas chave de desempenho que podem ser utilizado toomonitor e resolver problemas de desempenho da sua consulta e a tarefa de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe906-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="fe906-107">toosee estas métricas, navegue até a tarefa de Stream Analytics toohello estiver interessado em ver as métricas para e Olá vista **monitorização** secção na página de descrição geral de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe906-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![Monitorização de ligação](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="fe906-109">será apresentada a janela de Olá conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="fe906-109">hello window will appear as shown:</span></span>

![Tarefa Dashboard de monitorização](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="fe906-111">Métricas disponíveis para o Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe906-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="fe906-112">Métrica</span><span class="sxs-lookup"><span data-stu-id="fe906-112">Metric</span></span>                 | <span data-ttu-id="fe906-113">Definição</span><span class="sxs-lookup"><span data-stu-id="fe906-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="fe906-114">% De utilização de SU</span><span class="sxs-lookup"><span data-stu-id="fe906-114">SU % Utilization</span></span>       | <span data-ttu-id="fe906-115">utilização de Olá de Olá as unidades de transmissão em fluxo atribuído tooa tarefa a partir do separador de escala Olá da tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe906-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="fe906-116">Deve neste indicador atingir 80% ou acima, há probabilidade elevada que o processamento de eventos pode sofrer um atraso ou parado efetuar progresso.</span><span class="sxs-lookup"><span data-stu-id="fe906-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="fe906-117">Eventos de entrada</span><span class="sxs-lookup"><span data-stu-id="fe906-117">Input Events</span></span>           | <span data-ttu-id="fe906-118">Quantidade de dados recebidos pela tarefa de Stream Analytics Olá, número de eventos.</span><span class="sxs-lookup"><span data-stu-id="fe906-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="fe906-119">Isto pode ser utilizado toovalidate que eventos são enviados toohello origem de entrada.</span><span class="sxs-lookup"><span data-stu-id="fe906-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="fe906-120">Eventos de saída</span><span class="sxs-lookup"><span data-stu-id="fe906-120">Output Events</span></span>          | <span data-ttu-id="fe906-121">Quantidade de dados enviados por Olá Stream Analytics tarefa toohello saída destino, no número de eventos.</span><span class="sxs-lookup"><span data-stu-id="fe906-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="fe906-122">Eventos de fora de ordem</span><span class="sxs-lookup"><span data-stu-id="fe906-122">Out-of-Order Events</span></span>    | <span data-ttu-id="fe906-123">Número de eventos recebidos fora de ordem que foram ignorados ou fornecido um ajustada timestamp, com base no Olá política de ordenação de evento.</span><span class="sxs-lookup"><span data-stu-id="fe906-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="fe906-124">Isto pode ser afetado pela configuração de Olá da definição de período de tolerância fora de ordem de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe906-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="fe906-125">Erros de conversão de dados</span><span class="sxs-lookup"><span data-stu-id="fe906-125">Data Conversion Errors</span></span> | <span data-ttu-id="fe906-126">Número de erros de conversão de dados tarifas por uma tarefa de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe906-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="fe906-127">Erros de Runtime</span><span class="sxs-lookup"><span data-stu-id="fe906-127">Runtime Errors</span></span>         | <span data-ttu-id="fe906-128">número total de Olá de erros que ocorrem durante a execução de uma tarefa de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe906-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="fe906-129">Eventos de entrada de enlace tardio</span><span class="sxs-lookup"><span data-stu-id="fe906-129">Late Input Events</span></span>      | <span data-ttu-id="fe906-130">Número de eventos que chegam tarde de origem Olá que optar por ter sido removido ou os respetivos timestamp foi ajustado, com base na configuração de política de ordenação de evento Olá da definição de período de tolerância de chegada tarde Olá.</span><span class="sxs-lookup"><span data-stu-id="fe906-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="fe906-131">Pedidos de função</span><span class="sxs-lookup"><span data-stu-id="fe906-131">Function Requests</span></span>      | <span data-ttu-id="fe906-132">Número de chamadas toohello função do Azure Machine Learning (caso exista).</span><span class="sxs-lookup"><span data-stu-id="fe906-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="fe906-133">Pedidos de função falhada</span><span class="sxs-lookup"><span data-stu-id="fe906-133">Failed Function Requests</span></span> | <span data-ttu-id="fe906-134">Número de chamadas de função, falhadas Azure Machine Learning (caso exista).</span><span class="sxs-lookup"><span data-stu-id="fe906-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="fe906-135">Eventos de função</span><span class="sxs-lookup"><span data-stu-id="fe906-135">Function Events</span></span>        | <span data-ttu-id="fe906-136">Número dos eventos enviados toohello a função do Azure Machine Learning (caso exista).</span><span class="sxs-lookup"><span data-stu-id="fe906-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="fe906-137">Bytes do evento de entrada</span><span class="sxs-lookup"><span data-stu-id="fe906-137">Input Event Bytes</span></span>      | <span data-ttu-id="fe906-138">Quantidade de dados recebidos pela tarefa de Stream Analytics Olá, em bytes.</span><span class="sxs-lookup"><span data-stu-id="fe906-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="fe906-139">Isto pode ser utilizado toovalidate que eventos são enviados toohello origem de entrada.</span><span class="sxs-lookup"><span data-stu-id="fe906-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="fe906-140">Personalizar monitorização no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fe906-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="fe906-141">Pode ajustar o tipo de Olá de gráfico, métricas apresentadas e intervalo nas definições de editar gráfico Olá de tempo.</span><span class="sxs-lookup"><span data-stu-id="fe906-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="fe906-142">Para obter mais informações, consulte [como tooCustomize monitorização](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="fe906-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Gráfico do Monitor de hora de consulta](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="fe906-144">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="fe906-144">Get help</span></span>
<span data-ttu-id="fe906-145">Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="fe906-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe906-146">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fe906-146">Next steps</span></span>
* [<span data-ttu-id="fe906-147">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe906-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fe906-148">Começar a utilizar o Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe906-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fe906-149">Tarefas de escala do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe906-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="fe906-150">Referência do idioma de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe906-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fe906-151">Referência de API do REST de gestão do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe906-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

