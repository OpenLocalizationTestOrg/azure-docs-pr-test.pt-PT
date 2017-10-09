---
title: "aaaFilter telemetria do Azure Application Insights na aplicação web Java | Microsoft Docs"
description: "Reduzir o tráfego de telemetria por filtrar eventos Olá não precisa de toomonitor."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="0d151-103">Filtrar a telemetria na aplicação web Java</span><span class="sxs-lookup"><span data-stu-id="0d151-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="0d151-104">Filtros de fornecem uma telemetria de Olá de tooselect de forma a [aplicação web Java envia tooApplication Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0d151-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="0d151-105">Existem alguns filtros out of box, que pode utilizar e, também pode escrever o seus próprio filtros personalizados.</span><span class="sxs-lookup"><span data-stu-id="0d151-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="0d151-106">os filtros de out of box Olá incluem:</span><span class="sxs-lookup"><span data-stu-id="0d151-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="0d151-107">Nível de gravidade de rastreio</span><span class="sxs-lookup"><span data-stu-id="0d151-107">Trace severity level</span></span>
* <span data-ttu-id="0d151-108">URLs específicos, as palavras-chave ou códigos de resposta</span><span class="sxs-lookup"><span data-stu-id="0d151-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="0d151-109">As respostas do rápida - ou seja, pedidos toowhich a aplicação respondeu tooquickly</span><span class="sxs-lookup"><span data-stu-id="0d151-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="0d151-110">Nomes de evento específico</span><span class="sxs-lookup"><span data-stu-id="0d151-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="0d151-111">Filtros de desfasamento métricas Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="0d151-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="0d151-112">Por exemplo, poderá decidir que, na ordem toodiagnose lentas, defina um tempos de resposta rápidos de toodiscard de filtro.</span><span class="sxs-lookup"><span data-stu-id="0d151-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="0d151-113">Mas deve ter em atenção que os tempos de resposta médio de Olá comunicados pelo Application Insights, em seguida, será mais lentos do que a velocidade de verdadeiro Olá e contagem de Olá de pedidos serão inferior a contagem real Olá.</span><span class="sxs-lookup"><span data-stu-id="0d151-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="0d151-114">Se esta for uma preocupação, utilize [amostragem](app-insights-sampling.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="0d151-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="0d151-115">Definir filtros</span><span class="sxs-lookup"><span data-stu-id="0d151-115">Setting filters</span></span>

<span data-ttu-id="0d151-116">No ApplicationInsights.xml, adicione um `TelemetryProcessors` secção com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="0d151-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want toosee -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




<span data-ttu-id="0d151-117">[Inspecione o conjunto completo de Olá de processadores incorporadas](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="0d151-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="0d151-118">Filtros incorporados</span><span class="sxs-lookup"><span data-stu-id="0d151-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="0d151-119">Filtro de telemetria métrico</span><span class="sxs-lookup"><span data-stu-id="0d151-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="0d151-120">`NotNeeded`-Lista separados por vírgulas de nomes de métricas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0d151-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="0d151-121">Filtro de telemetria de visualizações de página</span><span class="sxs-lookup"><span data-stu-id="0d151-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="0d151-122">`DurationThresholdInMS`-Duração refere-se o tempo de toohello decorrido página de Olá tooload.</span><span class="sxs-lookup"><span data-stu-id="0d151-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="0d151-123">Se isto estiver definido, as páginas que carregar mais rapidamente do que este período de tempo não são reportadas.</span><span class="sxs-lookup"><span data-stu-id="0d151-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="0d151-124">`NotNeededNames`-Lista separados por vírgulas de nomes de página.</span><span class="sxs-lookup"><span data-stu-id="0d151-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="0d151-125">`NotNeededUrls`-Os fragmentos de lista separados por vírgulas de URL.</span><span class="sxs-lookup"><span data-stu-id="0d151-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="0d151-126">Por exemplo, `"home"` filtra todas as páginas que tenham "página principal" no URL Olá.</span><span class="sxs-lookup"><span data-stu-id="0d151-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="0d151-127">Filtro de telemetria de pedido</span><span class="sxs-lookup"><span data-stu-id="0d151-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="0d151-128">Filtro de origem sintético</span><span class="sxs-lookup"><span data-stu-id="0d151-128">Synthetic Source filter</span></span>

<span data-ttu-id="0d151-129">Filtra a toda a telemetria que têm valores em Olá SyntheticSource propriedade.</span><span class="sxs-lookup"><span data-stu-id="0d151-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="0d151-130">Estes incluem pedidos de bots, spiders e testes de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0d151-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="0d151-131">Filtre a telemetria para todos os pedidos sintéticos:</span><span class="sxs-lookup"><span data-stu-id="0d151-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="0d151-132">Filtre a telemetria origens sintéticas específicas:</span><span class="sxs-lookup"><span data-stu-id="0d151-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="0d151-133">`NotNeeded`-Lista de nomes de origem sintético separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="0d151-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="0d151-134">Filtro de eventos de telemetria</span><span class="sxs-lookup"><span data-stu-id="0d151-134">Telemetry Event filter</span></span>

<span data-ttu-id="0d151-135">Filtra eventos personalizados (registado utilizando [trackevent ()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="0d151-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="0d151-136">`NotNeededNames`-Lista de nomes do evento separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="0d151-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="0d151-137">Filtro de telemetria de rastreio</span><span class="sxs-lookup"><span data-stu-id="0d151-137">Trace Telemetry filter</span></span>

<span data-ttu-id="0d151-138">Filtros de rastreios de registo (registado utilizando [tracktrace ()](app-insights-api-custom-events-metrics.md#tracktrace) ou um [recoletor de arquitetura de registo](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="0d151-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="0d151-139">`FromSeverityLevel`os valores válidos são:</span><span class="sxs-lookup"><span data-stu-id="0d151-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="0d151-140">DESATIVAR - filtrar todos os rastreios</span><span class="sxs-lookup"><span data-stu-id="0d151-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="0d151-141">RASTREIO - nenhuma filtragem.</span><span class="sxs-lookup"><span data-stu-id="0d151-141">TRACE           - No filtering.</span></span> <span data-ttu-id="0d151-142">nível de tooTrace de é igual a</span><span class="sxs-lookup"><span data-stu-id="0d151-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="0d151-143">INFORMAÇÃO - filtro o nível de rastreio</span><span class="sxs-lookup"><span data-stu-id="0d151-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="0d151-144">AVISO - filtro de rastreio e de informações</span><span class="sxs-lookup"><span data-stu-id="0d151-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="0d151-145">ERRO - o filtro de saída de rastreio de aviso, informações,</span><span class="sxs-lookup"><span data-stu-id="0d151-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="0d151-146">CRÍTICO - filtro enviados todos os léxicos crítico</span><span class="sxs-lookup"><span data-stu-id="0d151-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="0d151-147">Filtros personalizados</span><span class="sxs-lookup"><span data-stu-id="0d151-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="0d151-148">1. O filtro de código</span><span class="sxs-lookup"><span data-stu-id="0d151-148">1. Code your filter</span></span>

<span data-ttu-id="0d151-149">No seu código, crie uma classe que implementa `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="0d151-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="0d151-150">2. Invocar o filtro no ficheiro de configuração de Olá</span><span class="sxs-lookup"><span data-stu-id="0d151-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="0d151-151">No ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="0d151-151">In ApplicationInsights.xml:</span></span>

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a><span data-ttu-id="0d151-152">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="0d151-152">Troubleshooting</span></span>

<span data-ttu-id="0d151-153">*A minha filtro não está a funcionar.*</span><span class="sxs-lookup"><span data-stu-id="0d151-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="0d151-154">Certifique-se de que forneceu valores de parâmetro válido.</span><span class="sxs-lookup"><span data-stu-id="0d151-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="0d151-155">Por exemplo, durações devem ser números inteiros.</span><span class="sxs-lookup"><span data-stu-id="0d151-155">For example, durations should be integers.</span></span> <span data-ttu-id="0d151-156">Valores inválidos fará Olá filtro toobe ignorada.</span><span class="sxs-lookup"><span data-stu-id="0d151-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="0d151-157">Se o seu filtro personalizado emite uma exceção de um construtor ou método definido, será ignorado.</span><span class="sxs-lookup"><span data-stu-id="0d151-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d151-158">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0d151-158">Next steps</span></span>

* <span data-ttu-id="0d151-159">[Amostragem](app-insights-sampling.md) -considere amostragem como alternativa que não desfasamento as métricas.</span><span class="sxs-lookup"><span data-stu-id="0d151-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
