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
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="695da-103">Telemetria de métrica: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="695da-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="695da-104">Existem dois tipos de telemetria métrica suportado pelo [Application Insights](app-insights-overview.md): único e medições e uma métrica previamente agregada.</span><span class="sxs-lookup"><span data-stu-id="695da-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="695da-105">Única medida é apenas um nome e valor.</span><span class="sxs-lookup"><span data-stu-id="695da-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="695da-106">Métrica previamente agregada Especifica o valor mínimo e máximo de métrica de Olá no intervalo de agregação de Olá e o desvio-padrão do mesmo.</span><span class="sxs-lookup"><span data-stu-id="695da-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="695da-107">Telemetria de métrica previamente agregada assume esse período de agregação foi um minuto.</span><span class="sxs-lookup"><span data-stu-id="695da-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="695da-108">Existem vários nomes de métricos conhecidos suportados pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="695da-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="695da-109">Métrica que representa os contadores de sistema e do processo:</span><span class="sxs-lookup"><span data-stu-id="695da-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="695da-110">**Nome de .NET**</span><span class="sxs-lookup"><span data-stu-id="695da-110">**.NET name**</span></span>             | <span data-ttu-id="695da-111">**Nome de agnóstico relativamente de plataforma**</span><span class="sxs-lookup"><span data-stu-id="695da-111">**Platform agnostic name**</span></span> | <span data-ttu-id="695da-112">**Nome da API de REST**</span><span class="sxs-lookup"><span data-stu-id="695da-112">**REST API name**</span></span> | <span data-ttu-id="695da-113">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="695da-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="695da-114">Trabalho em curso...</span><span class="sxs-lookup"><span data-stu-id="695da-114">Work in progress...</span></span> | [<span data-ttu-id="695da-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="695da-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="695da-116">CPU de máquinas totais</span><span class="sxs-lookup"><span data-stu-id="695da-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="695da-117">Trabalho em curso...</span><span class="sxs-lookup"><span data-stu-id="695da-117">Work in progress...</span></span> | [<span data-ttu-id="695da-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="695da-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="695da-119">memória disponível no disco</span><span class="sxs-lookup"><span data-stu-id="695da-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="695da-120">Trabalho em curso...</span><span class="sxs-lookup"><span data-stu-id="695da-120">Work in progress...</span></span> | [<span data-ttu-id="695da-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="695da-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="695da-122">CPU de processo Olá alojar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="695da-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="695da-123">Trabalho em curso...</span><span class="sxs-lookup"><span data-stu-id="695da-123">Work in progress...</span></span> | [<span data-ttu-id="695da-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="695da-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="695da-125">memória utilizada pelo processo de Olá alojar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="695da-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="695da-126">Trabalho em curso...</span><span class="sxs-lookup"><span data-stu-id="695da-126">Work in progress...</span></span> | [<span data-ttu-id="695da-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="695da-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="695da-128">velocidade das operações de e/s de executa pelo processo que aloja a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="695da-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="695da-129">Trabalho em curso...</span><span class="sxs-lookup"><span data-stu-id="695da-129">Work in progress...</span></span> | [<span data-ttu-id="695da-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="695da-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="695da-131">taxa de pedidos processados por aplicação</span><span class="sxs-lookup"><span data-stu-id="695da-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="695da-132">Trabalho em curso...</span><span class="sxs-lookup"><span data-stu-id="695da-132">Work in progress...</span></span> | [<span data-ttu-id="695da-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="695da-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="695da-134">taxa de exceções iniciadas pela aplicação</span><span class="sxs-lookup"><span data-stu-id="695da-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="695da-135">Trabalho em curso...</span><span class="sxs-lookup"><span data-stu-id="695da-135">Work in progress...</span></span> | [<span data-ttu-id="695da-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="695da-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="695da-137">tempo de execução média de pedidos</span><span class="sxs-lookup"><span data-stu-id="695da-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="695da-138">Trabalho em curso...</span><span class="sxs-lookup"><span data-stu-id="695da-138">Work in progress...</span></span> | [<span data-ttu-id="695da-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="695da-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="695da-140">número de pedidos à espera do Olá numa fila de processamento</span><span class="sxs-lookup"><span data-stu-id="695da-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="695da-141">Nome</span><span class="sxs-lookup"><span data-stu-id="695da-141">Name</span></span>

<span data-ttu-id="695da-142">Nome da métrica de Olá que gostaria de toosee no portal do Application Insights e IU.</span><span class="sxs-lookup"><span data-stu-id="695da-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="695da-143">Valor</span><span class="sxs-lookup"><span data-stu-id="695da-143">Value</span></span>

<span data-ttu-id="695da-144">Valor único para a medida.</span><span class="sxs-lookup"><span data-stu-id="695da-144">Single value for measurement.</span></span> <span data-ttu-id="695da-145">Soma de medidas individuais para agregação de Olá.</span><span class="sxs-lookup"><span data-stu-id="695da-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="695da-146">Contagem</span><span class="sxs-lookup"><span data-stu-id="695da-146">Count</span></span>

<span data-ttu-id="695da-147">Métrica ponderação da métrica de Olá agregado.</span><span class="sxs-lookup"><span data-stu-id="695da-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="695da-148">Não deve ser definida para uma medida.</span><span class="sxs-lookup"><span data-stu-id="695da-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="695da-149">Mín.</span><span class="sxs-lookup"><span data-stu-id="695da-149">Min</span></span>

<span data-ttu-id="695da-150">Valor mínimo de métrica de Olá agregado.</span><span class="sxs-lookup"><span data-stu-id="695da-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="695da-151">Não deve ser definida para uma medida.</span><span class="sxs-lookup"><span data-stu-id="695da-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="695da-152">Máx</span><span class="sxs-lookup"><span data-stu-id="695da-152">Max</span></span>

<span data-ttu-id="695da-153">Valor máximo de métrica de Olá agregado.</span><span class="sxs-lookup"><span data-stu-id="695da-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="695da-154">Não deve ser definida para uma medida.</span><span class="sxs-lookup"><span data-stu-id="695da-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="695da-155">Desvio-padrão</span><span class="sxs-lookup"><span data-stu-id="695da-155">Standard deviation</span></span>

<span data-ttu-id="695da-156">Desvio-padrão de Olá agregado métrica.</span><span class="sxs-lookup"><span data-stu-id="695da-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="695da-157">Não deve ser definida para uma medida.</span><span class="sxs-lookup"><span data-stu-id="695da-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="695da-158">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="695da-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="695da-159">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="695da-159">Next steps</span></span>

- <span data-ttu-id="695da-160">Saiba como toouse [API do Application Insights para as métricas e eventos personalizados](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="695da-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="695da-161">Consulte [modelo de dados](application-insights-data-model.md) para o modelo de tipos e os dados do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="695da-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="695da-162">Veja [plataformas](app-insights-platforms.md) suportado pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="695da-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
