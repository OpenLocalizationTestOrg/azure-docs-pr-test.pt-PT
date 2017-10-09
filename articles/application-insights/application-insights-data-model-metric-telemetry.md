---
title: "aaaAzure modelo de dados do Application Insights telemetria - métrica telemetria | Microsoft Docs"
description: "Modelo de dados do Application Insights para telemetria métrica"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a>Telemetria de métrica: modelo de dados do Application Insights

Existem dois tipos de telemetria métrica suportado pelo [Application Insights](app-insights-overview.md): único e medições e uma métrica previamente agregada. Única medida é apenas um nome e valor. Métrica previamente agregada Especifica o valor mínimo e máximo de métrica de Olá no intervalo de agregação de Olá e o desvio-padrão do mesmo.

Telemetria de métrica previamente agregada assume esse período de agregação foi um minuto.

Existem vários nomes de métricos conhecidos suportados pelo Application Insights. 

Métrica que representa os contadores de sistema e do processo:

| **Nome de .NET**             | **Nome de agnóstico relativamente de plataforma** | **Nome da API de REST** | **Descrição**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | Trabalho em curso... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | CPU de máquinas totais
| `\Memory\Available Bytes`                 | Trabalho em curso... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | memória disponível no disco
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | Trabalho em curso... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | CPU de processo Olá alojar a aplicação Olá
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | Trabalho em curso... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | memória utilizada pelo processo de Olá alojar a aplicação Olá
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | Trabalho em curso... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | velocidade das operações de e/s de executa pelo processo que aloja a aplicação Olá
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | Trabalho em curso... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | taxa de pedidos processados por aplicação 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | Trabalho em curso... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | taxa de exceções iniciadas pela aplicação
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | Trabalho em curso... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | tempo de execução média de pedidos
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | Trabalho em curso... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | número de pedidos à espera do Olá numa fila de processamento

## <a name="name"></a>Nome

Nome da métrica de Olá que gostaria de toosee no portal do Application Insights e IU. 

## <a name="value"></a>Valor

Valor único para a medida. Soma de medidas individuais para agregação de Olá.

## <a name="count"></a>Contagem

Métrica ponderação da métrica de Olá agregado. Não deve ser definida para uma medida.

## <a name="min"></a>Mín.

Valor mínimo de métrica de Olá agregado. Não deve ser definida para uma medida.

## <a name="max"></a>Máx

Valor máximo de métrica de Olá agregado. Não deve ser definida para uma medida.

## <a name="standard-deviation"></a>Desvio-padrão

Desvio-padrão de Olá agregado métrica. Não deve ser definida para uma medida.

## <a name="custom-properties"></a>Propriedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Passos seguintes

- Saiba como toouse [API do Application Insights para as métricas e eventos personalizados](app-insights-api-custom-events-metrics.md#trackmetric).
- Consulte [modelo de dados](application-insights-data-model.md) para o modelo de tipos e os dados do Application Insights.
- Veja [plataformas](app-insights-platforms.md) suportado pelo Application Insights.
