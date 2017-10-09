---
title: "referência de aaaApplicationInsights.config - Azure | Microsoft Docs"
description: "Ativar ou desativar os módulos de recolha de dados e adicionar os contadores de desempenho e outros parâmetros."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="d3ca0-103">Configurar Olá Application Insights SDK com Applicationinsights ou. XML</span><span class="sxs-lookup"><span data-stu-id="d3ca0-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="d3ca0-104">Olá SDK .NET do Application Insights é composta por um número de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="d3ca0-105">O [pacote core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fornece Olá API para enviar telemetria ao hello do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="d3ca0-106">[Pacotes adicionais](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) fornecer telemetria *módulos* e *inicializadores* para controlo automaticamente telemetria da sua aplicação e o respetivo contexto.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="d3ca0-107">Ao ajustar o ficheiro de configuração de Olá, pode ativar ou desativar os módulos de telemetria e inicializadores e definir os parâmetros de algumas delas.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="d3ca0-108">nome do ficheiro de configuração de Olá `ApplicationInsights.config` ou `ApplicationInsights.xml`, consoante o tipo de Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="d3ca0-109">É automaticamente adicionado tooyour projeto quando [instalar a maioria das versões do SDK de Olá][start].</span><span class="sxs-lookup"><span data-stu-id="d3ca0-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="d3ca0-110">Foi também adicionada a aplicação web tooa [Monitor de estado num servidor IIS][redfield], ou quando seleciona Olá Appplication Insights [extensão para um Web site Azure ou VM](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="d3ca0-111">Não é um Olá de toocontrol ficheiro equivalente [SDK numa página web][client].</span><span class="sxs-lookup"><span data-stu-id="d3ca0-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="d3ca0-112">Este documento descreve secções Olá que vê na configuração de Olá ficheiro, como controlarem estes componentes Olá de Olá SDK, e quais os pacotes NuGet carregar desses componentes.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="d3ca0-113">Módulos de telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="d3ca0-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="d3ca0-114">Cada módulo telemetria recolhe um tipo específico de dados e utiliza core Olá dados de Olá toosend de API.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="d3ca0-115">módulos de Olá estão instalados por diferentes pacotes de NuGet, que também adicionar o ficheiro do Olá linhas necessária toohello. config.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="d3ca0-116">Não há um nó no ficheiro de configuração de Olá para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="d3ca0-117">toodisable um módulo, elimine o nó de Olá ou comente-lo.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="d3ca0-118">Controlo de dependência</span><span class="sxs-lookup"><span data-stu-id="d3ca0-118">Dependency Tracking</span></span>
<span data-ttu-id="d3ca0-119">[Controlo de dependência](app-insights-asp-net-dependencies.md) recolhe telemetria sobre as chamadas a aplicação faz com que serviços externos e toodatabases e bases de dados.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="d3ca0-120">tooallow toowork este módulo, um servidor de IIS, terá de demasiado[instalar Monitor de estado][redfield].</span><span class="sxs-lookup"><span data-stu-id="d3ca0-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="d3ca0-121">toouse-lo em aplicações web do Azure ou VMs, [selecionar extensão do Application Insights Olá](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="d3ca0-122">Também pode escrever o seu próprio controlo código utilizando Olá de dependência [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="d3ca0-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="d3ca0-124">Recoletor de desempenho</span><span class="sxs-lookup"><span data-stu-id="d3ca0-124">Performance collector</span></span>
<span data-ttu-id="d3ca0-125">[Recolhe os contadores de desempenho do sistema](app-insights-performance-counters.md) tais como CPU, memória e rede carregar das instalações do IIS.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="d3ca0-126">Pode especificar que toocollect contadores, incluindo os contadores de desempenho que configurou por si.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="d3ca0-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="d3ca0-128">Telemetria de diagnóstico do Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3ca0-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="d3ca0-129">Olá `DiagnosticsTelemetryModule` relatórios de erros no Olá código de instrumentação do Application Insights em si.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="d3ca0-130">Por exemplo, se o código de Olá não é possível aceder contadores de desempenho ou se um `ITelemetryInitializer` emite uma exceção.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="d3ca0-131">Telemetria de rastreio registada por este módulo é apresentado no Olá [pesquisa de diagnóstico][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="d3ca0-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="d3ca0-132">Envia dados de diagnóstico toodc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="d3ca0-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="d3ca0-134">Se apenas a instalar este pacote, o ficheiro de Applicationinsights Olá não é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="d3ca0-135">Modo de programador</span><span class="sxs-lookup"><span data-stu-id="d3ca0-135">Developer Mode</span></span>
<span data-ttu-id="d3ca0-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`força Olá Application Insights `TelemetryChannel` toosend dados imediatamente, itens de um telemetria cada vez, quando um depurador for anexado toohello processo da aplicação.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="d3ca0-137">Esta reduz Olá período de tempo entre o momento de Olá quando a aplicação controla telemetria e quando é apresentado no portal do Application Insights Olá.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="d3ca0-138">Causa overhead significativo na largura de banda de CPU e da rede.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="d3ca0-139">[Windows Server do Application Insights](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="d3ca0-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="d3ca0-140">Pedido de Web de controlo</span><span class="sxs-lookup"><span data-stu-id="d3ca0-140">Web Request Tracking</span></span>
<span data-ttu-id="d3ca0-141">Olá relatórios [código de tempo e o resultado da resposta](app-insights-asp-net.md) de pedidos HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="d3ca0-142">[Applicationinsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="d3ca0-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="d3ca0-143">Controlo de exceções</span><span class="sxs-lookup"><span data-stu-id="d3ca0-143">Exception tracking</span></span>
<span data-ttu-id="d3ca0-144">`ExceptionTrackingTelemetryModule`controla exceções não processadas na aplicação web.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="d3ca0-145">Consulte [falhas e exceções][exceptions].</span><span class="sxs-lookup"><span data-stu-id="d3ca0-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="d3ca0-146">[Applicationinsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="d3ca0-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="d3ca0-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-controla [não observada exceções tarefas](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="d3ca0-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-controla exceções não processadas para as funções de trabalho, serviços do windows e aplicações de consola.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="d3ca0-149">[Windows Server do Application Insights](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="d3ca0-150">Controlo de EventSource</span><span class="sxs-lookup"><span data-stu-id="d3ca0-150">EventSource Tracking</span></span>
<span data-ttu-id="d3ca0-151">`EventSourceTelemetryModule`permite-lhe tooconfigure toobe de eventos de EventSource enviado tooApplication Insights como rastreios.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="d3ca0-152">Para obter informações sobre o registo de eventos de EventSource, consulte [através de eventos de EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="d3ca0-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="d3ca0-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="d3ca0-154">Registo de eventos do ETW</span><span class="sxs-lookup"><span data-stu-id="d3ca0-154">ETW Event Tracking</span></span>
<span data-ttu-id="d3ca0-155">`EtwCollectorTelemetryModule`permite-lhe tooconfigure eventos do ETW fornecedores toobe enviado tooApplication Insights como rastreios.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="d3ca0-156">Para obter informações sobre o registo de eventos ETW, consulte [através de eventos do ETW](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="d3ca0-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="d3ca0-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="d3ca0-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="d3ca0-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="d3ca0-159">pacote de Microsoft.ApplicationInsights Olá fornece Olá [principal API](https://msdn.microsoft.com/library/mt420197.aspx) de Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="d3ca0-160">Olá outros módulos de telemetria utilizá-lo e também pode [utilizá-lo toodefine sua própria telemetria](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="d3ca0-161">Nenhuma entrada no Applicationinsights.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="d3ca0-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="d3ca0-163">Se instalar apenas esta NuGet, não é gerado nenhum ficheiro. config.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="d3ca0-164">Canal de telemetria</span><span class="sxs-lookup"><span data-stu-id="d3ca0-164">Telemetry Channel</span></span>
<span data-ttu-id="d3ca0-165">canal de telemetria de Olá gere a colocação em memória intermédia e transmissão de telemetria toohello serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="d3ca0-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`é Olá predefinido canal para os serviços.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="d3ca0-167">Este serve de memória intermédia dados na memória.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-167">It buffers data in memory.</span></span>
* <span data-ttu-id="d3ca0-168">`Microsoft.ApplicationInsights.PersistenceChannel`é uma alternativa para aplicações de consola.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="d3ca0-169">Pode poupar qualquer armazenamento de toopersistent unflushed dados quando a aplicação fecha-se para baixo e irá enviar quando inicia a aplicação Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="d3ca0-170">Inicializadores de telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="d3ca0-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="d3ca0-171">Os inicializadores de telemetria definir propriedades de contexto, que são enviadas juntamente com todos os itens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="d3ca0-172">Pode [escrever os seus próprios inicializadores](app-insights-api-filtering-sampling.md#add-properties) tooset propriedades de contexto.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="d3ca0-173">Os inicializadores padrão Olá estão todos definidos por pacotes de Web ou WindowsServer NuGet Olá:</span><span class="sxs-lookup"><span data-stu-id="d3ca0-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="d3ca0-174">`AccountIdTelemetryInitializer`Define a propriedade de AccountId Olá.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="d3ca0-175">`AuthenticatedUserIdTelemetryInitializer`Define a propriedade de AuthenticatedUserId de Olá conforme definido por Olá JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="d3ca0-176">`AzureRoleEnvironmentTelemetryInitializer`Olá atualizações `RoleName` e `RoleInstance` propriedades de Olá `Device` contexto de todos os itens de telemetria com informações extraídas do ambiente de tempo de execução do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="d3ca0-177">`BuildInfoConfigComponentVersionTelemetryInitializer`Olá atualizações `Version` propriedade Olá `Component` contexto de todos os itens de telemetria com o valor de Olá extraídos de Olá `BuildInfo.config` ficheiro produzidos por MS Build.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="d3ca0-178">`ClientIpHeaderTelemetryInitializer`atualizações `Ip` propriedade Olá `Location` contexto de todos os itens de telemetria com base no Olá `X-Forwarded-For` cabeçalho HTTP do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="d3ca0-179">`DeviceTelemetryInitializer`Olá atualizações seguintes propriedades de Olá `Device` contexto de todos os itens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="d3ca0-180">`Type`está definido demasiado "PC"</span><span class="sxs-lookup"><span data-stu-id="d3ca0-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="d3ca0-181">`Id`está definido toohello o nome de domínio do computador olá onde a aplicação web de Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="d3ca0-182">`OemName`definir o valor toohello extraído de Olá `Win32_ComputerSystem.Manufacturer` campo através do WMI.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="d3ca0-183">`Model`definir o valor toohello extraído de Olá `Win32_ComputerSystem.Model` campo através do WMI.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="d3ca0-184">`NetworkType`definir o valor toohello extraído de Olá `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="d3ca0-185">`Language`está a definir o nome toohello Olá `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="d3ca0-186">`DomainNameRoleInstanceTelemetryInitializer`Olá atualizações `RoleInstance` propriedade Olá `Device` contexto de todos os itens de telemetria com o nome de domínio Olá do computador olá onde a aplicação web de Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="d3ca0-187">`OperationNameTelemetryInitializer`Olá atualizações `Name` propriedade Olá `RequestTelemetry` e Olá `Name` propriedade Olá `Operation` contexto de todos os itens de telemetria com base no método Olá HTTP, bem como os nomes de Olá de tooprocess invocado de controlador e a ação de MVC do ASP.NET pedido.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="d3ca0-188">`OperationIdTelemetryInitializer`ou `OperationCorrelationTelemetryInitializer` Olá atualizações `Operation.Id` propriedade de contexto de todos os itens de telemetria controlados durante o processamento de um pedido com Olá gerado automaticamente `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="d3ca0-189">`SessionTelemetryInitializer`Olá atualizações `Id` propriedade Olá `Session` contexto de todos os itens de telemetria com valor extraídos de Olá `ai_session` cookie gerados pelo Olá, código de instrumentação de ApplicationInsights JavaScript em execução no browser do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="d3ca0-190">`SyntheticTelemetryInitializer`ou `SyntheticUserAgentTelemetryInitializer` Olá atualizações `User`, `Session` e `Operation` controlado de propriedades de contextos de todos os itens de telemetria ao processar um pedido de uma origem sintética, tal como um disponibilidade testar ou bot do motor de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="d3ca0-191">Por predefinição, [Explorador de métricas](app-insights-metrics-explorer.md) não apresenta a telemetria sintética.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="d3ca0-192">Olá `<Filters>` definir propriedades de pedidos de Olá a identificar.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="d3ca0-193">`UserAgentTelemetryInitializer`Olá atualizações `UserAgent` propriedade Olá `User` contexto de todos os itens de telemetria com base no Olá `User-Agent` cabeçalho HTTP do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="d3ca0-194">`UserTelemetryInitializer`Olá atualizações `Id` e `AcquisitionDate` propriedades de `User` contexto de todos os itens de telemetria com valores extraídos de Olá `ai_user` cookie gerado pelo Olá Application Insights instrumentação no código JavaScript em execução no Olá browser do utilizador.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="d3ca0-195">`WebTestTelemetryInitializer`conjuntos de Olá id de utilizador, id de sessão e propriedades da origem sintético para pedidos de HTTP que provenientes do [testes de disponibilidade](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="d3ca0-196">Olá `<Filters>` definir propriedades de pedidos de Olá a identificar.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="d3ca0-197">Para aplicações de .NET em execução no Service Fabric, pode incluir Olá `Microsoft.ApplicationInsights.ServiceFabric` pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="d3ca0-198">Este pacote inclui um `FabricTelemetryInitializer`, que adiciona itens de tootelemetry de propriedades de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="d3ca0-199">Para obter mais informações, consulte Olá [página do GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sobre as propriedades de Olá adicionadas por este pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="d3ca0-200">Processadores de telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="d3ca0-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="d3ca0-201">Processadores de telemetria podem filtrar e modificar cada item de telemetria apenas antes de ser enviada partir Olá SDK toohello do portal.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="d3ca0-202">Pode [escrever os seus próprios processadores de telemetria](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="d3ca0-203">Processador de telemetria de amostragem adaptável (a partir de 2.0.0-Beta3)</span><span class="sxs-lookup"><span data-stu-id="d3ca0-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="d3ca0-204">Opção ativada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-204">This is enabled by default.</span></span> <span data-ttu-id="d3ca0-205">Se a aplicação envia uma grande quantidade de telemetria, este processador remove algumas do mesmo.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="d3ca0-206">parâmetro de Olá fornece destino Olá que Olá algoritmo tenta tooachieve.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="d3ca0-207">Cada instância de Olá que SDK funciona de forma independente, pelo que o se o servidor for um cluster de vários computadores, o volume real de Olá de telemetria irá ser multiplicado em conformidade.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="d3ca0-208">[Saiba mais sobre amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="d3ca0-209">A amostragem-taxa telemetria processador (2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="d3ca0-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="d3ca0-210">Também é uma norma [amostragem processador telemetria](app-insights-api-filtering-sampling.md) (a partir de 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="d3ca0-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="d3ca0-211">Parâmetros do canal (Java)</span><span class="sxs-lookup"><span data-stu-id="d3ca0-211">Channel parameters (Java)</span></span>
<span data-ttu-id="d3ca0-212">Estes parâmetros afetam como Olá SDK de Java deve armazenar e esvaziar dados de telemetria de Olá que recolhe.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="d3ca0-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="d3ca0-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="d3ca0-214">número de Olá de itens de telemetria que podem ser armazenados no armazenamento de dentro da memória do Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="d3ca0-215">Quando este número for atingido, a memória intermédia de telemetria de Olá for descarregada - ou seja, itens de telemetria de Olá são enviados por servidor do Application Insights toohello.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="d3ca0-216">Mínimo: 1</span><span class="sxs-lookup"><span data-stu-id="d3ca0-216">Min: 1</span></span>
* <span data-ttu-id="d3ca0-217">Máx.: 1000</span><span class="sxs-lookup"><span data-stu-id="d3ca0-217">Max: 1000</span></span>
* <span data-ttu-id="d3ca0-218">Predefinição: 500</span><span class="sxs-lookup"><span data-stu-id="d3ca0-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="d3ca0-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="d3ca0-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="d3ca0-220">Determina a frequência hello dados armazenados no armazenamento de dentro da memória Olá devem ser removida da cache (enviado tooApplication Insights).</span><span class="sxs-lookup"><span data-stu-id="d3ca0-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="d3ca0-221">Mínimo: 1</span><span class="sxs-lookup"><span data-stu-id="d3ca0-221">Min: 1</span></span>
* <span data-ttu-id="d3ca0-222">Máx.: 300</span><span class="sxs-lookup"><span data-stu-id="d3ca0-222">Max: 300</span></span>
* <span data-ttu-id="d3ca0-223">Predefinição: 5</span><span class="sxs-lookup"><span data-stu-id="d3ca0-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="d3ca0-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="d3ca0-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="d3ca0-225">Determina o tamanho máximo do Olá em MB, que é atribuído toohello armazenamento persistente num disco local Olá.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="d3ca0-226">Este tipo de armazenamento é utilizado para itens de telemetria persistentes que falharam toobe transmitido toohello Application Insights endpoint.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="d3ca0-227">Quando o tamanho de armazenamento Olá tem sido cumprido, novos itens de telemetria serão eliminados.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="d3ca0-228">Mínimo: 1</span><span class="sxs-lookup"><span data-stu-id="d3ca0-228">Min: 1</span></span>
* <span data-ttu-id="d3ca0-229">Máxima: 100</span><span class="sxs-lookup"><span data-stu-id="d3ca0-229">Max: 100</span></span>
* <span data-ttu-id="d3ca0-230">Predefinição: 10</span><span class="sxs-lookup"><span data-stu-id="d3ca0-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="d3ca0-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="d3ca0-231">InstrumentationKey</span></span>
<span data-ttu-id="d3ca0-232">Isto determina o recurso do Application Insights Olá na qual os dados são apresentados.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="d3ca0-233">Normalmente, crie um recurso de separado, com uma chave separada, para cada uma das suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="d3ca0-234">Se pretende tooset Olá chave dinamicamente - por exemplo, se quiser toosend resultados dos seus recursos de toodifferent da aplicação - pode omitir a chave de Olá Olá ficheiro de configuração e configurá-lo no código.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="d3ca0-235">chave de Olá tooset para todas as instâncias TelemetryClient, incluindo módulos de telemetria padrão, defina a chave de Olá no TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="d3ca0-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="d3ca0-236">Fazê-lo um método de inicialização, tais como global.aspx.cs num serviço ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="d3ca0-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="d3ca0-237">Se pretender apenas toosend específicos de um conjunto de recursos diferente de tooa de eventos, pode definir chave Olá para um TelemetryClient específico:</span><span class="sxs-lookup"><span data-stu-id="d3ca0-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="d3ca0-238">tooget uma nova chave, [criar um novo recurso no portal do Application Insights Olá][new].</span><span class="sxs-lookup"><span data-stu-id="d3ca0-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3ca0-239">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d3ca0-239">Next steps</span></span>
<span data-ttu-id="d3ca0-240">[Saiba mais sobre Olá API][api].</span><span class="sxs-lookup"><span data-stu-id="d3ca0-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
