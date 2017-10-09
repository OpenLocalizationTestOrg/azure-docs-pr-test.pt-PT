---
title: "aaaMonitor estado de funcionamento da sua aplicação e a utilização com o Application Insights"
description: "Introdução ao Application Insights. Analise a utilização, disponibilidade e desempenho dos seus no local ou aplicações do Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="a6cd0-104">Monitorizar o desempenho nas aplicações Web</span><span class="sxs-lookup"><span data-stu-id="a6cd0-104">Monitor performance in web applications</span></span>


<span data-ttu-id="a6cd0-105">Certifique-se de que a aplicação está a executar corretamente e descobrir rapidamente sobre eventuais falhas.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="a6cd0-106">[Application Insights] [ start] conte quaisquer problemas de desempenho e exceções e ajudar a localizar e diagnosticar Olá de causas raiz.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="a6cd0-107">Application Insights podem monitorizar aplicações web de Java e ASP.NET e serviços, serviços do WCF.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="a6cd0-108">Podem ser alojado no local, em máquinas virtuais, ou como Web sites do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="a6cd0-109">No lado do cliente de Olá, Application Insights pode demorar a telemetria de páginas web e uma ampla variedade de dispositivos incluindo dispositivos iOS, Android e aplicações da loja Windows.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="a6cd0-110">Efetuamos uma nova experiência disponível para localizar lenta efetuar páginas na sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="a6cd0-111">Se não tiver acesso tooit, ativá-la ao configurar as opções de pré-visualização com Olá [painel de pré-visualização](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="a6cd0-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="a6cd0-112">Leia sobre esta nova experiência em [localizar e corrigir os congestionamentos de desempenho com investigação de desempenho interativa Olá](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="a6cd0-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="a6cd0-113"><a name="setup"></a>Configurar a monitorização de desempenho</span><span class="sxs-lookup"><span data-stu-id="a6cd0-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="a6cd0-114">Se ainda não adicionou o Application Insights tooyour (ou seja, se não tem Applicationinsights) do projeto, escolha uma das seguintes maneiras tooget iniciado:</span><span class="sxs-lookup"><span data-stu-id="a6cd0-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="a6cd0-115">Aplicações web do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a6cd0-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="a6cd0-116">Adicionar a monitorização de exceções</span><span class="sxs-lookup"><span data-stu-id="a6cd0-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="a6cd0-117">Adicionar a monitorização de dependência</span><span class="sxs-lookup"><span data-stu-id="a6cd0-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="a6cd0-118">Aplicações web J2EE</span><span class="sxs-lookup"><span data-stu-id="a6cd0-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="a6cd0-119">Adicionar a monitorização de dependência</span><span class="sxs-lookup"><span data-stu-id="a6cd0-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="a6cd0-120"><a name="view"></a>Explorar métricas de desempenho</span><span class="sxs-lookup"><span data-stu-id="a6cd0-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="a6cd0-121">No [Olá portal do Azure](https://portal.azure.com), procure o recurso do Application Insights toohello que configurou para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="a6cd0-122">Painel de descrição geral de Olá mostra os dados de desempenho básico:</span><span class="sxs-lookup"><span data-stu-id="a6cd0-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="a6cd0-123">Clique em qualquer gráfico toosee mais detalhes e resultados toosee durante um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="a6cd0-124">Por exemplo, clique no mosaico pedidos Olá e, em seguida, selecione um intervalo de tempo:</span><span class="sxs-lookup"><span data-stu-id="a6cd0-124">For example, click hello Requests tile and then select a time range:</span></span>

![Clicar toomore dados e selecione um intervalo de tempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="a6cd0-126">Clique em toochoose um gráfico que métricas apresenta, ou adicione um novo gráfico e selecionar a métricas:</span><span class="sxs-lookup"><span data-stu-id="a6cd0-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Clique em métricas de toochoose um gráfico](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="a6cd0-128">**Desmarque todas as métricas de Olá** toosee Olá completa seleção que está disponível.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="a6cd0-129">métricas de Olá enquadram-se grupos; Quando qualquer membro de um grupo é selecionado, só hello outros membros desse grupo aparecem.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="a6cd0-130"><a name="metrics"></a>O que faz-média de todos os?</span><span class="sxs-lookup"><span data-stu-id="a6cd0-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="a6cd0-131">Os mosaicos de desempenho e relatórios</span><span class="sxs-lookup"><span data-stu-id="a6cd0-131">Performance tiles and reports</span></span>
<span data-ttu-id="a6cd0-132">Existem várias métricas de desempenho, que pode obter.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="a6cd0-133">Vamos começar com as que são apresentados por predefinição no painel de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="a6cd0-134">Pedidos</span><span class="sxs-lookup"><span data-stu-id="a6cd0-134">Requests</span></span>
<span data-ttu-id="a6cd0-135">Olá número de pedidos HTTP recebidos no período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="a6cd0-136">Compare isto com resultados de Olá no toosee outros relatórios como a aplicação se comporta como Olá carga varia.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="a6cd0-137">Pedidos de HTTP incluem todos os pedidos GET ou POST de páginas, dados e imagens.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="a6cd0-138">Clique em Olá mosaico tooget contagens para URLs específicos.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="a6cd0-139">Tempo de resposta médio</span><span class="sxs-lookup"><span data-stu-id="a6cd0-139">Average response time</span></span>
<span data-ttu-id="a6cd0-140">Tempo de Olá medidas entre um pedido web introduzir a sua aplicação e Olá resposta a ser devolvida.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="a6cd0-141">pontos de Olá mostram uma mudança médio.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-141">hello points show a moving average.</span></span> <span data-ttu-id="a6cd0-142">Se existirem muitos pedidos, poderão existir alguns desvio de média de Olá sem um horário de pico óbvios ou dip no gráfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="a6cd0-143">Procure picos de atividade invulgares.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-143">Look for unusual peaks.</span></span> <span data-ttu-id="a6cd0-144">Em geral, espere toorise de tempo de resposta com um aumento súbito do pedidos.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="a6cd0-145">Se o aumento súbito Olá desproporcionado, a aplicação pode atingir um limite de recursos, tais como a capacidade de CPU ou Olá de um serviço que utiliza.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="a6cd0-146">Clique em tempos de tooget Olá mosaico para URLs específicos.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="a6cd0-147">Pedidos mais lentos</span><span class="sxs-lookup"><span data-stu-id="a6cd0-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="a6cd0-148">Mostra quais os pedidos poderão ter de otimização de desempenho.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="a6cd0-149">Pedidos falhados</span><span class="sxs-lookup"><span data-stu-id="a6cd0-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="a6cd0-150">Uma contagem de pedidos que emitiu exceções não identificadas.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="a6cd0-151">Clique Olá mosaico toosee Olá os detalhes de falhas específicas e selecione um toosee de pedido individual respetivos detalhes.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="a6cd0-152">Apenas uma amostra representativa de falhas é mantida para inspecção individuais.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="a6cd0-153">Outras métricas</span><span class="sxs-lookup"><span data-stu-id="a6cd0-153">Other metrics</span></span>
<span data-ttu-id="a6cd0-154">toosee que outras métricas pode apresentar, clique num gráfico e, em seguida, anular seleção de todas as Olá métricas toosee Olá completa disponível conjunto.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="a6cd0-155">Clique em (i) toosee definição cada métrica.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-155">Click (i) toosee each metric's definition.</span></span>

![Anular seleção de todas as métricas toosee Olá todo conjunto](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="a6cd0-157">Selecionar qualquer Olá desativa métrica outras pessoas que não pode aparecer no Olá mesmo gráfico.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="a6cd0-158">Definir alertas</span><span class="sxs-lookup"><span data-stu-id="a6cd0-158">Set alerts</span></span>
<span data-ttu-id="a6cd0-159">toobe notificado por correio eletrónico dos valores invulgares de qualquer métrica, adicione um alerta.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="a6cd0-160">Pode escolher administradores de conta do toosend Olá e-mail toohello ou toospecific endereços de correio eletrónico.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="a6cd0-161">Defina recurso Olá antes Olá outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="a6cd0-162">Não escolha a recursos de webtest Olá se pretende os alertas de tooset no desempenho ou a métrica de utilização.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="a6cd0-163">Ser unidades de Olá toonote cuidado no qual está a pedido valor de limiar de Olá tooenter.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="a6cd0-164">*Não vejo o botão de alerta Olá adicionar.*</span><span class="sxs-lookup"><span data-stu-id="a6cd0-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="a6cd0-165">-Esta é uma toowhich de conta de grupo têm acesso só de leitura?</span><span class="sxs-lookup"><span data-stu-id="a6cd0-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="a6cd0-166">Consulte o administrador de conta Olá.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="a6cd0-167"><a name="diagnosis"></a>Diagnosticar problemas</span><span class="sxs-lookup"><span data-stu-id="a6cd0-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="a6cd0-168">Eis algumas sugestões para localizar e diagnosticar problemas de desempenho:</span><span class="sxs-lookup"><span data-stu-id="a6cd0-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="a6cd0-169">Configurar [testes web] [ availability] toobe alertado se o web site ficar inativo ou responder lentamente ou incorretamente.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="a6cd0-170">Compare a contagem de pedido de Olá com outra métricas toosee se falhas ou resposta lenta relacionado tooload.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="a6cd0-171">[Inserir, procure as instruções de rastreio] [ diagnostic] no seu código toohelp identificar problemas.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="a6cd0-172">Monitorizar a aplicação Web na operação com [métricas em fluxo em direto][livestream].</span><span class="sxs-lookup"><span data-stu-id="a6cd0-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="a6cd0-173">Capturar estado do Olá da aplicação .net com [instantâneo depurador][snapshot].</span><span class="sxs-lookup"><span data-stu-id="a6cd0-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="a6cd0-174">Localizar e corrigir os congestionamentos de desempenho com uma investigação de desempenho interativa</span><span class="sxs-lookup"><span data-stu-id="a6cd0-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="a6cd0-175">Pode utilizar Olá novo Application Insights desempenho interativa investigação toolocate áreas da sua aplicação Web que são abrandamento desempenho global.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="a6cd0-176">Pode rapidamente localizar específico páginas são abrandamento e utilizam Olá [ferramenta de criação de perfis](app-insights-profiler.md) toosee se houver uma correlação entre estas páginas.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="a6cd0-177">Criar uma lista de páginas lentas de desempenho</span><span class="sxs-lookup"><span data-stu-id="a6cd0-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="a6cd0-178">primeiro passo de Olá para encontrar problemas de desempenho é tooget uma lista de Olá lenta de páginas a responder.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="a6cd0-179">ecrã de Olá captura abaixo demonstra Olá desempenho painel tooget uma lista de potenciais tooinvestigate de páginas ainda mais a utilizar.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="a6cd0-180">Pode ver rapidamente nesta página que ocorreu uma slow-down no tempo de resposta de Olá da aplicação Olá aproximadamente 6:00 PM e novamente em aproximadamente as 22: 00.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="a6cd0-181">Também pode ver que a operação de cliente/detalhes Olá GET tinha execução algumas longa operações com um tempo de resposta mediano de 507.05 milissegundos.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Desempenho interativa do Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="a6cd0-183">Desagregar nas páginas específicas</span><span class="sxs-lookup"><span data-stu-id="a6cd0-183">Drill down on specific pages</span></span>

<span data-ttu-id="a6cd0-184">Assim que tiver um instantâneo do desempenho da aplicação, pode obter mais detalhes nas operações de desempenho lento específicas.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="a6cd0-185">Clique em qualquer operação no Olá lista toosee Olá detalhes, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="a6cd0-186">Do gráfico Olá pode ver se o desempenho de Olá foi com base numa dependência.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="a6cd0-187">Também pode ver quantas Olá experiente de utilizadores vários tempos de resposta.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-187">You can also see how many users experienced hello various response times.</span></span> 

![Painel de operações do Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="a6cd0-189">Desagregar no período de tempo específico</span><span class="sxs-lookup"><span data-stu-id="a6cd0-189">Drill down on a specific time period</span></span>

<span data-ttu-id="a6cd0-190">Depois de identificar um ponto no tempo tooinvestigate, desagregar ainda mais toolook em operações específicas Olá que possam ter provocado slow-down de desempenho de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="a6cd0-191">Quando clica num ponto específico no tempo a obter detalhes de Olá da página Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="a6cd0-192">No Olá exemplo abaixo, pode ver as operações de Olá listadas para um determinado período de tempo, juntamente com códigos de resposta do servidor de Olá e duração de operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="a6cd0-193">Também tem o url de Olá para abrir um item de trabalho do TFS, se precisar de toosend esta equipa de desenvolvimento de tooyour de informações.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Intervalo de tempo do Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="a6cd0-195">Desagregar uma operação específica</span><span class="sxs-lookup"><span data-stu-id="a6cd0-195">Drill down on a specific operation</span></span>

<span data-ttu-id="a6cd0-196">Depois de identificar um ponto no tempo tooinvestigate, desagregar ainda mais toolook em operações específicas Olá que possam ter provocado slow-down de desempenho de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="a6cd0-197">Clique numa operação de Olá lista toosee Olá os detalhes da operação de Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="a6cd0-198">Neste exemplo, pode ver que falha na operação de Olá e Application Insights forneceu Olá os detalhes do Olá emitiu aplicação Olá de exceção.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="a6cd0-199">Novamente, pode facilmente criar um item de trabalho do TFS a partir deste painel.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Painel de operação do Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="a6cd0-201"><a name="next"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a6cd0-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="a6cd0-202">[Testes Web] [ availability] -pedidos web enviaram tooyour aplicação em intervalos regulares de volta Olá mundo.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="a6cd0-203">[Capturar e procurar rastreios de diagnóstico] [ diagnostic] - inserir chamadas de rastreio e pouco úteis através de problemas de toopinpoint Olá resultados.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="a6cd0-204">[Controlo de utilização] [ usage] -saber como as pessoas utilizam a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="a6cd0-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="a6cd0-205">[Resolução de problemas] [ qna] - e as perguntas e respostas</span><span class="sxs-lookup"><span data-stu-id="a6cd0-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



