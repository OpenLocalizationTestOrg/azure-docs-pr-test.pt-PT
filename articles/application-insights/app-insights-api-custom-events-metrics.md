---
title: "aaaApplication Insights API de métricas e eventos personalizados | Microsoft Docs"
description: "Insira alguns linhas de código na sua utilização de tootrack dispositivo ou aplicação de ambiente de trabalho, a página Web ou serviço e diagnosticar problemas."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="04382-103">API do Application Insights para as métricas e eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="04382-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="04382-104">Inserir algumas linhas de código no seu toofind aplicação out que os utilizadores estão a fazer com o mesmo ou toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="04382-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="04382-105">Pode enviar telemetria a partir de aplicações de ambiente de trabalho e dispositivos, os clientes web e servidores web.</span><span class="sxs-lookup"><span data-stu-id="04382-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="04382-106">Olá utilize [Azure Application Insights](app-insights-overview.md) principal API de telemetria toosend e eventos personalizados e métricas, as suas próprias versões de telemetria padrão.</span><span class="sxs-lookup"><span data-stu-id="04382-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="04382-107">Esta API é Olá API mesmo padrão que Olá utilizam os recoletores de dados do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="04382-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="04382-108">Resumo da API</span><span class="sxs-lookup"><span data-stu-id="04382-108">API summary</span></span>
<span data-ttu-id="04382-109">Olá API é uniforme em todas as plataformas, para além dos algumas variações pequenas.</span><span class="sxs-lookup"><span data-stu-id="04382-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="04382-110">Método</span><span class="sxs-lookup"><span data-stu-id="04382-110">Method</span></span> | <span data-ttu-id="04382-111">Utilizado para</span><span class="sxs-lookup"><span data-stu-id="04382-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="04382-112">Páginas, ecrãs, painéis ou formulários.</span><span class="sxs-lookup"><span data-stu-id="04382-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="04382-113">Ações de utilizador e outros eventos.</span><span class="sxs-lookup"><span data-stu-id="04382-113">User actions and other events.</span></span> <span data-ttu-id="04382-114">Utilizado tootrack de desempenho de comportamento ou toomonitor de utilizador.</span><span class="sxs-lookup"><span data-stu-id="04382-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="04382-115">Medidas de desempenho, tais como os comprimentos fila não relacionada com eventos toospecific.</span><span class="sxs-lookup"><span data-stu-id="04382-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="04382-116">Exceções de registo para diagnósticos adicionais.</span><span class="sxs-lookup"><span data-stu-id="04382-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="04382-117">Rastreio onde ocorrer nos eventos de tooother de relação e examine rastreios de pilha.</span><span class="sxs-lookup"><span data-stu-id="04382-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="04382-118">Registo de frequência de Olá e duração de pedidos de servidor para análise de desempenho.</span><span class="sxs-lookup"><span data-stu-id="04382-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="04382-119">Mensagens de registo de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="04382-119">Diagnostic log messages.</span></span> <span data-ttu-id="04382-120">Também pode capturar os registos de terceiros.</span><span class="sxs-lookup"><span data-stu-id="04382-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="04382-121">Duração de Olá de registo e a frequência dos componentes de tooexternal de chamadas que depende da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="04382-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="04382-122">Pode [anexar propriedades e métricas](#properties) toomost destas chamadas à telemetria.</span><span class="sxs-lookup"><span data-stu-id="04382-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="04382-123"><a name="prep"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="04382-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="04382-124">Se ainda não tem uma referência no Application Insights SDK:</span><span class="sxs-lookup"><span data-stu-id="04382-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="04382-125">Adicione o projeto de tooyour Olá Application Insights SDK:</span><span class="sxs-lookup"><span data-stu-id="04382-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="04382-126">Projeto ASP.NET</span><span class="sxs-lookup"><span data-stu-id="04382-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="04382-127">Projeto de Java</span><span class="sxs-lookup"><span data-stu-id="04382-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="04382-128">JavaScript em cada página Web</span><span class="sxs-lookup"><span data-stu-id="04382-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="04382-129">No seu código de servidor web ou de dispositivo, incluem:</span><span class="sxs-lookup"><span data-stu-id="04382-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="04382-130">*C#:*`using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="04382-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="04382-131">*Visual Basic:*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="04382-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="04382-132">*Java:*`import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="04382-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="04382-133">Construir uma instância de TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="04382-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="04382-134">Construir uma instância de `TelemetryClient` (exceto em JavaScript em páginas Web):</span><span class="sxs-lookup"><span data-stu-id="04382-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="04382-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="04382-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="04382-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="04382-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="04382-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="04382-138">TelemetryClient é seguro para thread.</span><span class="sxs-lookup"><span data-stu-id="04382-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="04382-139">Recomendamos que utilize uma instância de TelemetryClient para cada módulo da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="04382-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="04382-140">Por exemplo, pode ter uma instância de TelemetryClient no seu pedidos HTTP recebidos do web service tooreport e outro em eventos de lógica de negócio um middleware classe tooreport.</span><span class="sxs-lookup"><span data-stu-id="04382-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="04382-141">Pode definir as propriedades, tais como `TelemetryClient.Context.User.Id` tootrack utilizadores e sessões, ou `TelemetryClient.Context.Device.Id` máquina de Olá tooidentify.</span><span class="sxs-lookup"><span data-stu-id="04382-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="04382-142">Estas informações são eventos tooall anexado Olá envia de instância.</span><span class="sxs-lookup"><span data-stu-id="04382-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="04382-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="04382-143">TrackEvent</span></span>
<span data-ttu-id="04382-144">No Application Insights, um *evento personalizado* é um ponto de dados que pode apresentar em [Explorador de métricas](app-insights-metrics-explorer.md) como uma conta a contagem agregada e na [pesquisa de diagnóstico](app-insights-diagnostic-search.md) como ocorrências individuais.</span><span class="sxs-lookup"><span data-stu-id="04382-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="04382-145">(Não se encontra tooMVC relacionado ou outros framework "eventos.")</span><span class="sxs-lookup"><span data-stu-id="04382-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="04382-146">Inserir `TrackEvent` chama no seu código toocount vários eventos.</span><span class="sxs-lookup"><span data-stu-id="04382-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="04382-147">Como muitas vezes, os utilizadores devem escolher uma funcionalidade específica, frequência alcançarem estes objetivos específicos ou talvez frequência que efetuam a tipos específicos de prende.</span><span class="sxs-lookup"><span data-stu-id="04382-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="04382-148">Por exemplo, uma aplicação de jogo, envie um evento sempre que um utilizador wins jogo Olá:</span><span class="sxs-lookup"><span data-stu-id="04382-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="04382-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="04382-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="04382-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="04382-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="04382-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="04382-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="04382-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="04382-153">Ver os eventos no portal do Microsoft Azure Olá</span><span class="sxs-lookup"><span data-stu-id="04382-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="04382-154">toosee uma contagem dos seus eventos, abra uma [Explorador de métricas](app-insights-metrics-explorer.md) painel, adicione um novo gráfico e selecione **eventos**.</span><span class="sxs-lookup"><span data-stu-id="04382-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Consulte uma contagem dos eventos personalizados](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="04382-156">contagens de Olá toocompare eventos diferente, defina o tipo de gráfico de Olá demasiado**grelha**e grupo por nome de evento:</span><span class="sxs-lookup"><span data-stu-id="04382-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Definir o tipo de gráfico de Olá e agrupamento](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="04382-158">Na grelha de Olá, clique em através de um evento nome toosee individuais as ocorrências esse evento.</span><span class="sxs-lookup"><span data-stu-id="04382-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="04382-159">toosee mais pormenorizadamente - clique em qualquer ocorrência na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-159">toosee more detail - click any occurrence in hello list.</span></span>

![Exploração de eventos de Olá](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="04382-161">toofocus nos eventos específicos na pesquisa ou no Explorador de métricas, filtro toohello eventos os nomes do painel do conjunto Olá que está interessado em:</span><span class="sxs-lookup"><span data-stu-id="04382-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![Abra os filtros, expanda o nome do evento e selecione um ou mais valores](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="04382-163">Eventos personalizados no Analytics</span><span class="sxs-lookup"><span data-stu-id="04382-163">Custom events in Analytics</span></span>

<span data-ttu-id="04382-164">telemetria de Olá está disponível no Olá `customEvents` tabela no [Application Insights Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="04382-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="04382-165">Cada linha representa uma chamada demasiado`trackEvent(..)` na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="04382-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="04382-166">Se [amostragem](app-insights-sampling.md) está numa operação, a propriedade de itemCount Olá mostra um valor superior a 1.</span><span class="sxs-lookup"><span data-stu-id="04382-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="04382-167">Para o exemplo itemCount = = 10 significa que de 10 chamadas tootrackEvent(), processo de amostragem Olá apenas transmitidos um deles.</span><span class="sxs-lookup"><span data-stu-id="04382-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="04382-168">tooget um número correto de eventos personalizados, deve utilizar, por conseguinte, código de utilização, tais como `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="04382-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="04382-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="04382-169">TrackMetric</span></span>

<span data-ttu-id="04382-170">Application Insights podem gráfico métricas que não estão anexados tooparticular eventos.</span><span class="sxs-lookup"><span data-stu-id="04382-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="04382-171">Por exemplo, pode monitorizar um comprimento de fila em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="04382-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="04382-172">Com a métrica, medidas individuais Olá são de menos interesse que variações Olá e as tendências e estatísticos, por isso, gráficos são úteis.</span><span class="sxs-lookup"><span data-stu-id="04382-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="04382-173">Na ordem toosend métricas tooApplication Insights, pode utilizar Olá `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="04382-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="04382-174">Existem duas formas toosend uma métrica de:</span><span class="sxs-lookup"><span data-stu-id="04382-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="04382-175">Valor único.</span><span class="sxs-lookup"><span data-stu-id="04382-175">Single value.</span></span> <span data-ttu-id="04382-176">Sempre que efetuar uma medida na sua aplicação, enviar valor correspondente Olá tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="04382-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="04382-177">Por exemplo, suponha que tem uma métrica de descrever o número de Olá de itens num contentor.</span><span class="sxs-lookup"><span data-stu-id="04382-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="04382-178">Durante um período de tempo específico, primeiro coloque o três itens num contentor de Olá e, em seguida, remover dois itens.</span><span class="sxs-lookup"><span data-stu-id="04382-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="04382-179">Em conformidade, iria chamar `TrackMetric` duas vezes: primeiro transmitir o valor de Olá `3` e, em seguida, Olá valor `-2`.</span><span class="sxs-lookup"><span data-stu-id="04382-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="04382-180">Application Insights armazena ambos os valores em seu nome.</span><span class="sxs-lookup"><span data-stu-id="04382-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="04382-181">Agregação.</span><span class="sxs-lookup"><span data-stu-id="04382-181">Aggregation.</span></span> <span data-ttu-id="04382-182">Ao trabalhar com as métricas, cada medida único é raramente de interesse.</span><span class="sxs-lookup"><span data-stu-id="04382-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="04382-183">Em vez disso, um resumo do que aconteceu durante um período de tempo específico é importante.</span><span class="sxs-lookup"><span data-stu-id="04382-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="04382-184">Denomina-se um resumo essa _agregação_.</span><span class="sxs-lookup"><span data-stu-id="04382-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="04382-185">Olá acima exemplo, soma métrica agregado Olá para esse período de tempo é `1` e Olá contagem de valores de métrica de Olá é `2`.</span><span class="sxs-lookup"><span data-stu-id="04382-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="04382-186">Quando utilizar a abordagem de agregação de Olá, apenas invocar `TrackMetric` uma vez por período e enviar Olá agregados valores de hora.</span><span class="sxs-lookup"><span data-stu-id="04382-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="04382-187">Este é Olá abordagem recomendada, uma vez que este pode reduzir significativamente o custo de Olá e desempenho dos custos gerais ao enviarem dados menos pontos tooApplication Insights, ao ainda recolher todas as informações relevantes.</span><span class="sxs-lookup"><span data-stu-id="04382-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="04382-188">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="04382-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="04382-189">Valores único</span><span class="sxs-lookup"><span data-stu-id="04382-189">Single values</span></span>

<span data-ttu-id="04382-190">um valor métrico único toosend:</span><span class="sxs-lookup"><span data-stu-id="04382-190">toosend a single metric value:</span></span>

<span data-ttu-id="04382-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="04382-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="04382-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="04382-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="04382-193">Agregar as métricas</span><span class="sxs-lookup"><span data-stu-id="04382-193">Aggregating metrics</span></span>

<span data-ttu-id="04382-194">É recomendado tooaggregate métricas antes de lhes enviar da sua aplicação, tooreduce largura de banda e de desempenho de custos e tooimprove.</span><span class="sxs-lookup"><span data-stu-id="04382-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="04382-195">Eis um exemplo de código agregar:</span><span class="sxs-lookup"><span data-stu-id="04382-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="04382-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="04382-197">Métricas personalizadas no Explorador de métricas</span><span class="sxs-lookup"><span data-stu-id="04382-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="04382-198">resultados de Olá toosee, abra o Explorador de métricas e adicionar um novo gráfico.</span><span class="sxs-lookup"><span data-stu-id="04382-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="04382-199">Edite Olá gráfico tooshow a métrica.</span><span class="sxs-lookup"><span data-stu-id="04382-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="04382-200">A métrica personalizada poderá demorar vários minutos tooappear na lista de Olá de métricas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="04382-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![Adicione um novo gráfico ou selecione um gráfico e, em personalizado, selecione a métrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="04382-202">Métricas personalizadas no Analytics</span><span class="sxs-lookup"><span data-stu-id="04382-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="04382-203">telemetria de Olá está disponível no Olá `customMetrics` tabela no [Application Insights Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="04382-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="04382-204">Cada linha representa uma chamada demasiado`trackMetric(..)` na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="04382-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="04382-205">`valueSum`-Esta é a soma de Olá uma medidas Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="04382-206">valor médio tooget Olá, dividir por `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="04382-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="04382-207">`valueCount`-Olá número de valores que foram agregados neste `trackMetric(..)` chamada.</span><span class="sxs-lookup"><span data-stu-id="04382-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="04382-208">Vistas de página</span><span class="sxs-lookup"><span data-stu-id="04382-208">Page views</span></span>
<span data-ttu-id="04382-209">Numa aplicação ou página Web de dispositivo, a telemetria de visualizações de página é enviada por predefinição quando cada ecrã ou a página é carregada.</span><span class="sxs-lookup"><span data-stu-id="04382-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="04382-210">Mas pode alterar as vistas de página que tootrack em alturas diferentes ou adicionais.</span><span class="sxs-lookup"><span data-stu-id="04382-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="04382-211">Por exemplo, numa aplicação que apresenta os separadores ou em painéis, é aconselhável tootrack uma página sempre que o utilizador Olá abre um novo painel.</span><span class="sxs-lookup"><span data-stu-id="04382-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![Lente de utilização no painel de descrição geral](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="04382-213">Dados de utilizador e de sessão são enviados como propriedades, juntamente com as vistas de página Olá, por isso, gráficos de utilizador e a sessão fique ativo quando não existe telemetria de visualizações de página.</span><span class="sxs-lookup"><span data-stu-id="04382-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="04382-214">Vistas de página personalizada</span><span class="sxs-lookup"><span data-stu-id="04382-214">Custom page views</span></span>
<span data-ttu-id="04382-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="04382-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="04382-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="04382-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="04382-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="04382-218">Se tiver vários separadores dentro páginas HTML diferentes, pode especificar o URL de Olá demasiado:</span><span class="sxs-lookup"><span data-stu-id="04382-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="04382-219">Vistas de página de temporização</span><span class="sxs-lookup"><span data-stu-id="04382-219">Timing page views</span></span>
<span data-ttu-id="04382-220">Por predefinição, os tempos de Olá reportados como **tempo de carregamento da vista de página** são avaliadas da quando browser Olá envia o pedido de Olá, até que o evento de carregamento de página do browser Olá é chamado.</span><span class="sxs-lookup"><span data-stu-id="04382-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="04382-221">Em vez disso, pode:</span><span class="sxs-lookup"><span data-stu-id="04382-221">Instead, you can either:</span></span>

* <span data-ttu-id="04382-222">Defina uma duração de explícita no Olá [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) chamar: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="04382-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="04382-223">Utilize chamadas de temporização de vista de página Olá `startTrackPage` e `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="04382-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="04382-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="04382-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="04382-225">...</span><span class="sxs-lookup"><span data-stu-id="04382-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="04382-226">Olá nome que utilizar como primeiro parâmetro de Olá associa início Olá e pare chamadas.</span><span class="sxs-lookup"><span data-stu-id="04382-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="04382-227">Assume toohello nome da página atual.</span><span class="sxs-lookup"><span data-stu-id="04382-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="04382-228">Olá resultante o carregamento da página apresentadas no Explorador de métricas de durações são derivadas de intervalo de Olá entre Olá iniciar e parar chamadas.</span><span class="sxs-lookup"><span data-stu-id="04382-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="04382-229">Está a funcionar tooyou que intervalo, na verdade, de hora.</span><span class="sxs-lookup"><span data-stu-id="04382-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="04382-230">Telemetria de página no Analytics</span><span class="sxs-lookup"><span data-stu-id="04382-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="04382-231">No [análise](app-insights-analytics.md) duas tabelas mostram dados de operações do browser:</span><span class="sxs-lookup"><span data-stu-id="04382-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="04382-232">Olá `pageViews` tabela contém dados sobre o título de URL e página Olá</span><span class="sxs-lookup"><span data-stu-id="04382-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="04382-233">Olá `browserTimings` tabela contém dados sobre o desempenho do cliente, tais como Olá tempo decorrido tooprocess Olá dados de entrada</span><span class="sxs-lookup"><span data-stu-id="04382-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="04382-234">toofind quanto browser Olá demora tooprocess páginas diferentes:</span><span class="sxs-lookup"><span data-stu-id="04382-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="04382-235">toodiscover popularities de Olá dos browsers diferentes:</span><span class="sxs-lookup"><span data-stu-id="04382-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="04382-236">chamadas de tooAJAX de vistas de página tooassociate, associar dependências:</span><span class="sxs-lookup"><span data-stu-id="04382-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="04382-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="04382-237">TrackRequest</span></span>
<span data-ttu-id="04382-238">o servidor de Olá SDK utiliza TrackRequest toolog os pedidos de HTTP.</span><span class="sxs-lookup"><span data-stu-id="04382-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="04382-239">Pode também chamá-la se pretender que os pedidos de toosimulate num contexto onde não tiver Olá web serviço módulo executado.</span><span class="sxs-lookup"><span data-stu-id="04382-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="04382-240">No entanto, Olá recomendado é de telemetria de pedido de toosend de forma onde pedido Olá age como um <a href="#operation-context">contexto das operações</a>.</span><span class="sxs-lookup"><span data-stu-id="04382-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="04382-241">Contexto de operação</span><span class="sxs-lookup"><span data-stu-id="04382-241">Operation context</span></span>
<span data-ttu-id="04382-242">Pode associar os itens de telemetria em conjunto ligando toothem um ID de operação comuns.</span><span class="sxs-lookup"><span data-stu-id="04382-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="04382-243">módulo de rastreio de pedido padrão Olá efetua este procedimento para exceções e outros eventos que são enviados enquanto está a ser processado um pedido de HTTP.</span><span class="sxs-lookup"><span data-stu-id="04382-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="04382-244">No [pesquisa](app-insights-diagnostic-search.md) e [análise](app-insights-analytics.md), pode utilizar qualquer eventos associados ao pedido de Olá Olá ID tooeasily localizar.</span><span class="sxs-lookup"><span data-stu-id="04382-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="04382-245">Olá mais fácil forma tooset Olá ID é tooset um contexto de operação ao utilizar este padrão:</span><span class="sxs-lookup"><span data-stu-id="04382-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="04382-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="04382-247">Juntamente com a definição de um contexto de operação `StartOperation` cria um item de telemetria do tipo de Olá que especificar.</span><span class="sxs-lookup"><span data-stu-id="04382-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="04382-248">Envia a telemetria Olá item quando eliminar operação hello, ou se chamar explicitamente `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="04382-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="04382-249">Se utilizar `RequestTelemetry` como tipo de telemetria de Olá, a duração está definida toohello excedeu o tempo limite de intervalo entre o início e fim.</span><span class="sxs-lookup"><span data-stu-id="04382-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="04382-250">Não não possível aninhar contextos de operação.</span><span class="sxs-lookup"><span data-stu-id="04382-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="04382-251">Se já houver um contexto de operação, então o respetivo ID está associado a todos os itens de Olá contida, incluindo o item de Olá criado com `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="04382-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="04382-252">Pesquisa, contexto das operações Olá é utilizado toocreate Olá **itens relacionados** lista:</span><span class="sxs-lookup"><span data-stu-id="04382-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![Itens relacionados](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="04382-254">Consulte [aplicação-insights-personalizada-operations-tracking.md] para obter mais informações sobre operações personalizadas de controlo.</span><span class="sxs-lookup"><span data-stu-id="04382-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="04382-255">Pedidos de análise</span><span class="sxs-lookup"><span data-stu-id="04382-255">Requests in Analytics</span></span> 

<span data-ttu-id="04382-256">No [Application Insights Analytics](app-insights-analytics.md), os pedidos Mostrar segurança Olá `requests` tabela.</span><span class="sxs-lookup"><span data-stu-id="04382-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="04382-257">Se [amostragem](app-insights-sampling.md) está numa operação, propriedade de itemCount Olá apresentará um valor superior a 1.</span><span class="sxs-lookup"><span data-stu-id="04382-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="04382-258">Para o exemplo itemCount = = 10 significa que de 10 chamadas tootrackRequest(), processo de amostragem Olá apenas transmitidos um deles.</span><span class="sxs-lookup"><span data-stu-id="04382-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="04382-259">tooget uma contagem de pedidos e a duração média correta segmentada por nomes de pedido, utilize, como o código:</span><span class="sxs-lookup"><span data-stu-id="04382-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="04382-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="04382-260">TrackException</span></span>
<span data-ttu-id="04382-261">Envie exceções tooApplication Insights:</span><span class="sxs-lookup"><span data-stu-id="04382-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="04382-262">demasiado[contagem-los](app-insights-metrics-explorer.md), como uma indicação de frequência de Olá de um problema.</span><span class="sxs-lookup"><span data-stu-id="04382-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="04382-263">demasiado[examinar ocorrências individuais](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="04382-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="04382-264">os relatórios de Olá incluem os rastreios de pilha Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="04382-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="04382-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="04382-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="04382-267">Olá SDKs catch muitas exceções automaticamente, pelo que não tem sempre toocall TrackException explicitamente.</span><span class="sxs-lookup"><span data-stu-id="04382-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="04382-268">ASP.NET: [escrever código toocatch exceções](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="04382-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="04382-269">J2EE: [as excepções são detectadas automaticamente](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="04382-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="04382-270">JavaScript: Exceções são detectadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="04382-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="04382-271">Se pretender que uma coleção automática toodisable, adicione um fragmento de código de toohello linha a inserir na suas páginas Web:</span><span class="sxs-lookup"><span data-stu-id="04382-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="04382-272">Exceções de análise</span><span class="sxs-lookup"><span data-stu-id="04382-272">Exceptions in Analytics</span></span>

<span data-ttu-id="04382-273">No [Application Insights Analytics](app-insights-analytics.md), exceções apresentada na Olá `exceptions` tabela.</span><span class="sxs-lookup"><span data-stu-id="04382-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="04382-274">Se [amostragem](app-insights-sampling.md) estiver a ser utilizada, hello `itemCount` propriedade mostra um valor superior a 1.</span><span class="sxs-lookup"><span data-stu-id="04382-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="04382-275">Para o exemplo itemCount = = 10 significa que de 10 chamadas tootrackException(), processo de amostragem Olá apenas transmitidos um deles.</span><span class="sxs-lookup"><span data-stu-id="04382-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="04382-276">um número correto de exceções de tooget segmentado pelo tipo de exceção, utilize, como o código:</span><span class="sxs-lookup"><span data-stu-id="04382-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="04382-277">Maioria dos Olá importante informações de pilha já são extraídas para variáveis separadas, mas pode solicitar Olá, à excepção `details` estrutura tooget mais.</span><span class="sxs-lookup"><span data-stu-id="04382-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="04382-278">Uma vez que esta estrutura dinâmica, deve de converter o tipo de toohello de resultado de Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="04382-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="04382-279">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="04382-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="04382-280">exceções de tooassociate com os pedidos relacionados, utilize uma associação:</span><span class="sxs-lookup"><span data-stu-id="04382-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="04382-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="04382-281">TrackTrace</span></span>
<span data-ttu-id="04382-282">Utilize TrackTrace toohelp diagnosticar problemas com o envio de um "registo trilho" tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="04382-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="04382-283">Pode enviar os segmentos de dados de diagnóstico e Inspecione os mesmos em [pesquisa de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="04382-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="04382-284">[Iniciar sessão adaptadores](app-insights-asp-net-trace-logs.md) utilizar esta API toosend registos de terceiros toohello portal.</span><span class="sxs-lookup"><span data-stu-id="04382-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="04382-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="04382-286">Pode pesquisar o conteúdo da mensagem, mas (ao contrário dos valores de propriedade) não é possível filtrar no mesmo.</span><span class="sxs-lookup"><span data-stu-id="04382-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="04382-287">limite de tamanho de Olá em `message` é muito superior ao limite de Olá nas propriedades.</span><span class="sxs-lookup"><span data-stu-id="04382-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="04382-288">Uma vantagem TrackTrace é que pode colocar dados relativamente longos na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="04382-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="04382-289">Por exemplo, pode codificar POST data do não existe.</span><span class="sxs-lookup"><span data-stu-id="04382-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="04382-290">Além disso, pode adicionar uma mensagem de tooyour nível de gravidade.</span><span class="sxs-lookup"><span data-stu-id="04382-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="04382-291">E, como outra telemetria, pode adicionar toohelp de valores de propriedade que filtrar ou de pesquisa para diferentes conjuntos de rastreios.</span><span class="sxs-lookup"><span data-stu-id="04382-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="04382-292">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="04382-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="04382-293">No [pesquisa](app-insights-diagnostic-search.md), em seguida, pode facilmente filtrar terminar todas as mensagens de Olá de um nível de gravidade específico que se relacionam com a base de dados específica tooa.</span><span class="sxs-lookup"><span data-stu-id="04382-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="04382-294">Rastreios no Analytics</span><span class="sxs-lookup"><span data-stu-id="04382-294">Traces in Analytics</span></span>

<span data-ttu-id="04382-295">No [Application Insights Analytics](app-insights-analytics.md), chama tooTrackTrace Mostrar cópias de segurança no Olá `traces` tabela.</span><span class="sxs-lookup"><span data-stu-id="04382-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="04382-296">Se [amostragem](app-insights-sampling.md) está numa operação, a propriedade de itemCount Olá mostra um valor superior a 1.</span><span class="sxs-lookup"><span data-stu-id="04382-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="04382-297">Para o exemplo itemCount = = 10 significa que de 10 chamadas demasiado`trackTrace()`, processo de amostragem Olá transmitidos apenas uma delas.</span><span class="sxs-lookup"><span data-stu-id="04382-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="04382-298">tooget uma contagem de chamadas de rastreio correta, deve utilizar, por conseguinte, código como `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="04382-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="04382-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="04382-299">TrackDependency</span></span>
<span data-ttu-id="04382-300">Olá utilize TrackDependency chamar tempos de resposta de Olá tootrack e taxas de êxito da peça de externo tooan chamadas de código.</span><span class="sxs-lookup"><span data-stu-id="04382-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="04382-301">resultados de Olá são apresentados nos gráficos de dependência de Olá no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-301">hello results appear in hello dependency charts in hello portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="04382-302">Lembre-se de que o servidor Olá SDKs incluem um [módulo dependência](app-insights-asp-net-dependencies.md) que Deteta e monitoriza determinadas chamadas de dependência automaticamente – por exemplo, toodatabases e REST APIs.</span><span class="sxs-lookup"><span data-stu-id="04382-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="04382-303">Ter tooinstall um agente no seu módulo Olá do servidor toomake funcione.</span><span class="sxs-lookup"><span data-stu-id="04382-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="04382-304">Utilize esta chamada se pretender que as chamadas de tootrack Olá controlo automatizado não catch ou se não quiser que o agente de Olá tooinstall.</span><span class="sxs-lookup"><span data-stu-id="04382-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="04382-305">Editar tooturn desativar o módulo de registo de dependência padrão Olá, [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) e eliminar a referência de Olá demasiado`DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="04382-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="04382-306">Dependências de análise</span><span class="sxs-lookup"><span data-stu-id="04382-306">Dependencies in Analytics</span></span>

<span data-ttu-id="04382-307">No [Application Insights Analytics](app-insights-analytics.md), chamadas de trackDependency apresentada na Olá `dependencies` tabela.</span><span class="sxs-lookup"><span data-stu-id="04382-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="04382-308">Se [amostragem](app-insights-sampling.md) está numa operação, a propriedade de itemCount Olá mostra um valor superior a 1.</span><span class="sxs-lookup"><span data-stu-id="04382-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="04382-309">Para o exemplo itemCount = = 10 significa que de 10 chamadas tootrackDependency(), processo de amostragem Olá apenas transmitidos um deles.</span><span class="sxs-lookup"><span data-stu-id="04382-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="04382-310">um número correto de dependências de tooget segmentado pelo componente de destino, utilize, como o código:</span><span class="sxs-lookup"><span data-stu-id="04382-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="04382-311">dependências de tooassociate com os pedidos relacionados, utilize uma associação:</span><span class="sxs-lookup"><span data-stu-id="04382-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="04382-312">Dados Flushing</span><span class="sxs-lookup"><span data-stu-id="04382-312">Flushing data</span></span>
<span data-ttu-id="04382-313">Normalmente, Olá SDK envia dados escolhidos por vezes o impacto de Olá toominimize utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="04382-314">No entanto, em alguns casos, pode querer memória intermédia de Olá tooflush – por exemplo, se estiver a utilizar o SDK de Olá numa aplicação que será encerrado.</span><span class="sxs-lookup"><span data-stu-id="04382-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="04382-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="04382-316">Tenha em atenção que a função de Olá é assíncrona para Olá [canal do servidor de telemetria](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="04382-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="04382-317">Utilizadores autenticados</span><span class="sxs-lookup"><span data-stu-id="04382-317">Authenticated users</span></span>
<span data-ttu-id="04382-318">Numa aplicação web, os utilizadores são (por predefinição) identificados por cookies.</span><span class="sxs-lookup"><span data-stu-id="04382-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="04382-319">Um utilizador pode contar mais do que uma vez se acederem a aplicação a partir de outro computador ou browser ou se poderem eliminar cookies.</span><span class="sxs-lookup"><span data-stu-id="04382-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="04382-320">Se os utilizadores iniciam sessão na aplicação tooyour, pode obter uma contagem mais exata, definindo o ID de utilizador Olá autenticado no código de browser Olá:</span><span class="sxs-lookup"><span data-stu-id="04382-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="04382-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="04382-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="04382-322">Na web do ASP.NET aplicação MVC, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="04382-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="04382-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="04382-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="04382-324">Não se encontra toouse necessário Olá nome do utilizador real início de sessão.</span><span class="sxs-lookup"><span data-stu-id="04382-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="04382-325">Tem apenas toobe um ID que é o utilizador toothat exclusivo.</span><span class="sxs-lookup"><span data-stu-id="04382-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="04382-326">Não pode incluir espaços ou nenhum dos carateres Olá `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="04382-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="04382-327">ID de utilizador Olá também definir um cookie de sessão e enviado toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="04382-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="04382-328">Se o servidor de Olá SDK está instalado, Olá autenticados utilizador que ID é enviado como parte das propriedades de contexto de Olá de telemetria de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="04382-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="04382-329">Em seguida, pode filtrar e procurar na mesma.</span><span class="sxs-lookup"><span data-stu-id="04382-329">You can then filter and search on it.</span></span>

<span data-ttu-id="04382-330">Se a sua aplicação grupos de utilizadores em contas, também pode transmitir um identificador de conta Olá (com Olá mesmo caráter restrições).</span><span class="sxs-lookup"><span data-stu-id="04382-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="04382-331">No [Explorador de métricas](app-insights-metrics-explorer.md), pode criar um gráfico que contagens **utilizadores, autenticado**, e **contas de utilizador**.</span><span class="sxs-lookup"><span data-stu-id="04382-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="04382-332">Também pode [pesquisa](app-insights-diagnostic-search.md) para pontos de dados de cliente com contas e os nomes de utilizador específica.</span><span class="sxs-lookup"><span data-stu-id="04382-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="04382-333"><a name="properties"></a>Filtragem, pesquisa e segmentar os seus dados através da utilização de propriedades</span><span class="sxs-lookup"><span data-stu-id="04382-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="04382-334">Pode anexar propriedades e medidas tooyour eventos (e também toometrics, vistas de página, exceções e outros dados de telemetria).</span><span class="sxs-lookup"><span data-stu-id="04382-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="04382-335">*Propriedades* são valores de cadeia que pode utilizar toofilter sua telemetria nos relatórios de utilização de Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="04382-336">Por exemplo, se a aplicação fornece várias jogos, poderá anexar nome Olá do evento de jogos tooeach Olá para que possa ver quais jogos são mais populares.</span><span class="sxs-lookup"><span data-stu-id="04382-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="04382-337">Não há um limite de 8192 no comprimento da cadeia Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="04382-338">(Se quiser toosend grandes segmentos de dados, utilize o parâmetro Mensagem Olá [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="04382-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="04382-339">*Métricas* são valores numéricos que podem ser apresentados graficamente.</span><span class="sxs-lookup"><span data-stu-id="04382-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="04382-340">Por exemplo, é aconselhável toosee se houver um aumento gradual na pontuações Olá que sua gamers alcançarem.</span><span class="sxs-lookup"><span data-stu-id="04382-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="04382-341">gráficos de Olá podem ser segmentados por Olá propriedades que são enviadas com evento Olá, para que pode obter separam ou empilhadas gráficos para jogos diferentes.</span><span class="sxs-lookup"><span data-stu-id="04382-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="04382-342">Para valores métrica toobe apresentado corretamente, devem ser too0 igual ou superior.</span><span class="sxs-lookup"><span data-stu-id="04382-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="04382-343">Existem algumas [limites no número de Olá de propriedades, valores de propriedade e métricas](#limits) que pode utilizar.</span><span class="sxs-lookup"><span data-stu-id="04382-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="04382-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="04382-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="04382-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="04382-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="04382-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="04382-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="04382-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="04382-348">Asseguramos não toolog informações de identificação pessoal nas propriedades.</span><span class="sxs-lookup"><span data-stu-id="04382-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="04382-349">*Se utilizou as métricas*, abra o Explorador de métricas e selecione a métrica de Olá da Olá **personalizada** grupo:</span><span class="sxs-lookup"><span data-stu-id="04382-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![Abra o Explorador de métricas, gráfico de selecione Olá e selecione Olá métrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="04382-351">Se a métrica não aparecer, ou se hello **personalizada** cabeçalho não existe, é de painel de seleção de Olá fechar e tente novamente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="04382-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="04382-352">Métricas, por vezes, podem demorar uma hora toobe agregado através do pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="04382-353">*Se utilizou as propriedades e métricas*, segmentar métrica Olá pela propriedade Olá:</span><span class="sxs-lookup"><span data-stu-id="04382-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![Definir o agrupamento e, em seguida, selecione a propriedade de Olá Agrupar por](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="04382-355">*Na pesquisa de diagnóstico*, pode ver as propriedades de Olá e métricas de ocorrências individuais de um evento.</span><span class="sxs-lookup"><span data-stu-id="04382-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![Selecione uma instância e, em seguida, selecione "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="04382-357">Olá utilize **pesquisa** campo toosee ocorrências de eventos que tenham um valor de propriedade em particular.</span><span class="sxs-lookup"><span data-stu-id="04382-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![Escreva um termo na pesquisa](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="04382-359">[Saiba mais sobre as expressões de pesquisa](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="04382-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="04382-360">Propriedades de tooset de maneira e métricas</span><span class="sxs-lookup"><span data-stu-id="04382-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="04382-361">Se for mais prático, é possível recolher Olá os parâmetros de um evento num objeto separado:</span><span class="sxs-lookup"><span data-stu-id="04382-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="04382-362">Não reutilize Olá mesma instância de item de telemetria (`event` neste exemplo) toocall Track*() várias vezes.</span><span class="sxs-lookup"><span data-stu-id="04382-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="04382-363">Isto pode provocar toobe de telemetria enviado com configuração incorreta.</span><span class="sxs-lookup"><span data-stu-id="04382-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="04382-364">Medidas personalizadas e propriedades na análise</span><span class="sxs-lookup"><span data-stu-id="04382-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="04382-365">No [análise](app-insights-analytics.md), métricas personalizadas e propriedades mostram em Olá `customMeasurements` e `customDimensions` atributos de cada registo de telemetria.</span><span class="sxs-lookup"><span data-stu-id="04382-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="04382-366">Por exemplo, se tiver adicionado uma propriedade com o nome "jogos" tooyour telemetria de pedido, esta consulta contagem de ocorrências de Olá de valores diferentes de "jogo" e mostrar a média de Olá de Olá métrica personalizada "pontuação":</span><span class="sxs-lookup"><span data-stu-id="04382-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="04382-367">Tenha em atenção que:</span><span class="sxs-lookup"><span data-stu-id="04382-367">Notice that:</span></span>

* <span data-ttu-id="04382-368">Quando um valor a extrair Olá customDimensions ou customMeasurements JSON, tem o tipo de dinâmico e, por isso, tem de o transmitir- `tostring` ou `todouble`.</span><span class="sxs-lookup"><span data-stu-id="04382-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="04382-369">conta de tootake da possibilidade de Olá de [amostragem](app-insights-sampling.md), deve utilizar `sum(itemCount)`, não `count()`.</span><span class="sxs-lookup"><span data-stu-id="04382-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="04382-370"><a name="timed"></a>Eventos de temporização</span><span class="sxs-lookup"><span data-stu-id="04382-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="04382-371">Por vezes, pretende toochart quanto tempo demora tooperform uma ação.</span><span class="sxs-lookup"><span data-stu-id="04382-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="04382-372">Por exemplo, poderá pretender tooknow quanto utilizadores levar a cabo tooconsider opções num jogo.</span><span class="sxs-lookup"><span data-stu-id="04382-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="04382-373">Pode utilizar o parâmetro de medição de Olá para este.</span><span class="sxs-lookup"><span data-stu-id="04382-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="04382-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="04382-375"><a name="defaults"></a>Propriedades predefinidas para telemetria personalizada</span><span class="sxs-lookup"><span data-stu-id="04382-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="04382-376">Se pretender que os valores de propriedade do tooset predefinido para alguns dos eventos personalizados Olá se escrever, pode defini-los numa instância TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="04382-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="04382-377">São tooevery ligado ao item de telemetria que é enviado a partir de que o cliente.</span><span class="sxs-lookup"><span data-stu-id="04382-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="04382-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="04382-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="04382-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="04382-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="04382-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="04382-381">Chamadas de telemetria individuais podem substituir os valores predefinidos de Olá no respetivos dicionários de propriedade.</span><span class="sxs-lookup"><span data-stu-id="04382-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="04382-382">*Para JavaScript web clientes*, [utilizar inicializadores de telemetria de JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="04382-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="04382-383">*telemetria de tooall tooadd propriedades*, incluindo dados Olá de módulos de recolha padrão, [implementar `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="04382-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="04382-384">Amostragem, a filtragem e o processamento de telemetria</span><span class="sxs-lookup"><span data-stu-id="04382-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="04382-385">Pode escrever o código tooprocess sua telemetria antes do envio de Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="04382-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="04382-386">processamento de Olá inclui dados enviados a partir de módulos de telemetria padrão de Olá, tais como recolha de pedido HTTP e a recolha de dependência.</span><span class="sxs-lookup"><span data-stu-id="04382-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="04382-387">[Adicionar propriedades](app-insights-api-filtering-sampling.md#add-properties) tootelemetry implementando `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="04382-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="04382-388">Por exemplo, pode adicionar valores que são calculados ou números de versão de outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="04382-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="04382-389">[Filtragem](app-insights-api-filtering-sampling.md#filtering) pode modificar ou eliminar telemetria antes do envio de Olá SDK implementando `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="04382-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="04382-390">Controlar o que é enviado ou eliminado, mas tiver tooaccount para o efeito de Olá nas métricas.</span><span class="sxs-lookup"><span data-stu-id="04382-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="04382-391">Dependendo de como eliminar itens, poderá perder Olá capacidade toonavigate entre itens relacionados.</span><span class="sxs-lookup"><span data-stu-id="04382-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="04382-392">[Amostragem](app-insights-api-filtering-sampling.md) é um volume de Olá tooreduce de solução em pacote de dados que são enviados a partir do portal de toohello de aplicação.</span><span class="sxs-lookup"><span data-stu-id="04382-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="04382-393">Isto é feito sem afetar as métricas de Olá apresentado.</span><span class="sxs-lookup"><span data-stu-id="04382-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="04382-394">E copia-sem afetar os problemas de toodiagnose capacidade ao navegar entre itens relacionados, tais como exceções, dos pedidos e vistas de página.</span><span class="sxs-lookup"><span data-stu-id="04382-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="04382-395">[Saiba mais](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="04382-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="04382-396">Desativar a telemetria</span><span class="sxs-lookup"><span data-stu-id="04382-396">Disabling telemetry</span></span>
<span data-ttu-id="04382-397">demasiado*dinamicamente parar e iniciar* Olá transmissão de telemetria e de coleção:</span><span class="sxs-lookup"><span data-stu-id="04382-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="04382-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="04382-399">demasiado*desativar os recoletores padrão selecionados*– por exemplo, os contadores de desempenho, os pedidos de HTTP ou dependências - eliminar ou comente Olá relevantes linhas [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). Para fazer isto, por exemplo, se quiser toosend os seus próprios dados TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="04382-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="04382-400"><a name="debug"></a>Modo de programador</span><span class="sxs-lookup"><span data-stu-id="04382-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="04382-401">Durante a depuração, é útil toohave a telemetria é emitida através do pipeline de Olá para que possa ver resultados imediatamente.</span><span class="sxs-lookup"><span data-stu-id="04382-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="04382-402">Pode também obter mensagens adicionais que o ajudam a quaisquer problemas com a telemetria de Olá de rastreio.</span><span class="sxs-lookup"><span data-stu-id="04382-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="04382-403">Desactivá-lo na produção, porque pode atrasar da aplicação.</span><span class="sxs-lookup"><span data-stu-id="04382-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="04382-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="04382-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="04382-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="04382-406"><a name="ikey"></a>A definição de chave de instrumentação Olá para telemetria personalizada selecionada</span><span class="sxs-lookup"><span data-stu-id="04382-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="04382-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="04382-408"><a name="dynamic-ikey"></a>Chave de instrumentação dinâmica</span><span class="sxs-lookup"><span data-stu-id="04382-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="04382-409">tooavoid a combinação de telemetria de desenvolvimento, teste e ambientes de produção, pode [criar recursos do Application Insights separados](app-insights-create-new-resource.md) e alterar as respetivas chaves, dependendo do ambiente de Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="04382-410">Em vez de obter a chave de instrumentação Olá do ficheiro de configuração de Olá, pode defini-lo no seu código.</span><span class="sxs-lookup"><span data-stu-id="04382-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="04382-411">Defina a chave de Olá um método de inicialização, tais como global.aspx.cs num serviço ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="04382-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="04382-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="04382-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="04382-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="04382-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="04382-414">Páginas Web, é aconselhável tooset-à partir do servidor web Olá Estado, em vez de codificação-literalmente no script de Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="04382-415">Por exemplo, numa página Web gerada por uma aplicação ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="04382-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="04382-416">*JavaScript em Razor*</span><span class="sxs-lookup"><span data-stu-id="04382-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="04382-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="04382-417">TelemetryContext</span></span>
<span data-ttu-id="04382-418">TelemetryClient tem uma propriedade de contexto, que contém valores que são enviados juntamente com todos os dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="04382-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="04382-419">Normalmente definidos por módulos de telemetria padrão Olá, mas também pode defini-los por si.</span><span class="sxs-lookup"><span data-stu-id="04382-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="04382-420">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="04382-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="04382-421">Se qualquer um destes valores por si, considere remover a linha relevante do Olá de [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), para que os valores e valores padrão Olá não obter confundidos.</span><span class="sxs-lookup"><span data-stu-id="04382-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="04382-422">**Componente**: Olá aplicação e a respetiva versão.</span><span class="sxs-lookup"><span data-stu-id="04382-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="04382-423">**Dispositivo**: dados sobre dispositivos olá onde a aplicação Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="04382-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="04382-424">(Nas web apps, este é o servidor de Olá ou um dispositivo cliente telemetria Olá enviados a partir.)</span><span class="sxs-lookup"><span data-stu-id="04382-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="04382-425">**InstrumentationKey**: Olá recurso do Application Insights no Azure onde a telemetria Olá aparecer.</span><span class="sxs-lookup"><span data-stu-id="04382-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="04382-426">Este é normalmente captado Applicationinsights.</span><span class="sxs-lookup"><span data-stu-id="04382-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="04382-427">**Localização**: Olá localização geográfica do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="04382-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="04382-428">**Operação**: nas web apps, Olá atual pedido HTTP.</span><span class="sxs-lookup"><span data-stu-id="04382-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="04382-429">Em outros tipos de aplicação, pode definir esta eventos toogroup em conjunto.</span><span class="sxs-lookup"><span data-stu-id="04382-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="04382-430">**ID**: itens relacionados com um valor gerado que está correlacionada com diferentes eventos, para que quando inspecionar qualquer evento na pesquisa de diagnóstico, possam localizar.</span><span class="sxs-lookup"><span data-stu-id="04382-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="04382-431">**Nome**: um identificador, normalmente, Olá URL do pedido de Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="04382-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="04382-432">**SyntheticSource**: Se não nulo ou está vazio, uma cadeia que indica que origem Olá de pedido de Olá foi identificada como um teste robot ou web.</span><span class="sxs-lookup"><span data-stu-id="04382-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="04382-433">Por predefinição, esta é excluída da cálculos no Explorador de métricas.</span><span class="sxs-lookup"><span data-stu-id="04382-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="04382-434">**Propriedades**: propriedades que são enviadas com todos os dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="04382-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="04382-435">Pode ser substituído nas chamadas controlar * individuais.</span><span class="sxs-lookup"><span data-stu-id="04382-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="04382-436">**Sessão**: Olá da sessão de utilizador.</span><span class="sxs-lookup"><span data-stu-id="04382-436">**Session**: hello user's session.</span></span> <span data-ttu-id="04382-437">ID de Olá definido valor tooa gerado, o que é alterado quando o utilizador Olá não tiver sido Active Directory para o tempo.</span><span class="sxs-lookup"><span data-stu-id="04382-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="04382-438">**Utilizador**: informações do utilizador.</span><span class="sxs-lookup"><span data-stu-id="04382-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="04382-439">Limites</span><span class="sxs-lookup"><span data-stu-id="04382-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="04382-440">tooavoid atingir o limite de velocidade de dados Olá, utilize [amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="04382-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="04382-441">toodetermine como são mantidos dados longos, consulte [retenção de dados e privacidade](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="04382-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="04382-442">Documentos de referência</span><span class="sxs-lookup"><span data-stu-id="04382-442">Reference docs</span></span>
* [<span data-ttu-id="04382-443">Referência ASP.NET</span><span class="sxs-lookup"><span data-stu-id="04382-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="04382-444">Referência de Java</span><span class="sxs-lookup"><span data-stu-id="04382-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="04382-445">Referência de JavaScript</span><span class="sxs-lookup"><span data-stu-id="04382-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="04382-446">SDK do Android</span><span class="sxs-lookup"><span data-stu-id="04382-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="04382-447">SDK do iOS</span><span class="sxs-lookup"><span data-stu-id="04382-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="04382-448">Código do SDK</span><span class="sxs-lookup"><span data-stu-id="04382-448">SDK code</span></span>
* [<span data-ttu-id="04382-449">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="04382-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="04382-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="04382-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="04382-451">Pacotes do Windows Server</span><span class="sxs-lookup"><span data-stu-id="04382-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="04382-452">SDK Java</span><span class="sxs-lookup"><span data-stu-id="04382-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="04382-453">SDK JavaScript</span><span class="sxs-lookup"><span data-stu-id="04382-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="04382-454">Todas as plataformas</span><span class="sxs-lookup"><span data-stu-id="04382-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="04382-455">Dúvidas</span><span class="sxs-lookup"><span data-stu-id="04382-455">Questions</span></span>
* <span data-ttu-id="04382-456">*As exceções podem emitir chamadas Track_()*</span><span class="sxs-lookup"><span data-stu-id="04382-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="04382-457">nenhum.</span><span class="sxs-lookup"><span data-stu-id="04382-457">None.</span></span> <span data-ttu-id="04382-458">Não precisa de toowrap-las em cláusulas try-catch.</span><span class="sxs-lookup"><span data-stu-id="04382-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="04382-459">Se Olá SDK detetar problemas, irá registar mensagens na saída de consola de depuração Olá e – se hello mensagens chegar - na pesquisa de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="04382-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="04382-460">*Existe um dados tooget de REST API do portal de Olá?*</span><span class="sxs-lookup"><span data-stu-id="04382-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="04382-461">Sim, Olá [API de acesso a dados](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="04382-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="04382-462">Incluem outros dados de tooextract formas [exportar de análise tooPower BI](app-insights-export-power-bi.md) e [a exportação contínua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="04382-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="04382-463"><a name="next"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="04382-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="04382-464">Eventos de pesquisa e registos</span><span class="sxs-lookup"><span data-stu-id="04382-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="04382-465">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="04382-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


