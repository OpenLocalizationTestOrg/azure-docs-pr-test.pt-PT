---
title: "aaaSearch análise de tráfego para a Azure Search | Microsoft Docs"
description: "Ative a análise de tráfego de pesquisa para a Azure Search, um serviço de pesquisa em nuvem alojado no Microsoft Azure, toounlock informações sobre os seus utilizadores e os dados."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="28c24-103">O que é a análise de tráfego de pesquisa</span><span class="sxs-lookup"><span data-stu-id="28c24-103">What is search traffic analytics</span></span>
<span data-ttu-id="28c24-104">Análise de tráfego de pesquisa é um padrão para implementar um ciclo de comentários do seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="28c24-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="28c24-105">Este padrão descreve os dados necessários Olá e como toocollect-la utilizando o Application Insights, um leader da indústria para monitorização dos serviços em várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="28c24-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="28c24-106">Análise de tráfego de pesquisa permite-lhe ganhar visibilidade ao seu serviço de pesquisa e desbloquear informações sobre os seus utilizadores e do respetivo comportamento.</span><span class="sxs-lookup"><span data-stu-id="28c24-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="28c24-107">Fazendo com que dados sobre o que escolhem os seus utilizadores, é possível toomake decisões que melhorar ainda mais a experiência de pesquisa e tooback desativado quando resultados de Olá são não que o esperado.</span><span class="sxs-lookup"><span data-stu-id="28c24-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="28c24-108">A pesquisa do Azure oferece uma solução de telemetria que integra o Azure Application Insights e o Power BI tooprovide aprofundada de monitorização e controlo.</span><span class="sxs-lookup"><span data-stu-id="28c24-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="28c24-109">Uma vez interação com a Azure Search é apenas através de APIs, tem de ser implementada telemetria Olá pelos programadores Olá utilizando a pesquisa, seguir instruções Olá nesta página.</span><span class="sxs-lookup"><span data-stu-id="28c24-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="28c24-110">Identificar dados de pesquisa relevantes Olá</span><span class="sxs-lookup"><span data-stu-id="28c24-110">Identify hello relevant search data</span></span>

<span data-ttu-id="28c24-111">métricas de pesquisa útil toohave, é necessário toolog algumas sinalizar dos utilizadores Olá da aplicação de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="28c24-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="28c24-112">Estes sinais significam conteúdo que os utilizadores estão interessados nas e de que o considerar relevante tootheir precisa.</span><span class="sxs-lookup"><span data-stu-id="28c24-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="28c24-113">Existem dois sinais que tem de análise de tráfego de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="28c24-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="28c24-114">Eventos de pesquisa de gerados pelo utilizador: apenas consultas de pesquisa iniciadas por um utilizador são interessantes.</span><span class="sxs-lookup"><span data-stu-id="28c24-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="28c24-115">Procurar pedidos utilizados toopopulate aspetos, o conteúdo adicional quaisquer informações internas, não são importantes e poderem prejudicar e bias os resultados.</span><span class="sxs-lookup"><span data-stu-id="28c24-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="28c24-116">Eventos de clique gerados pelo utilizador: por cliques neste documento, vamos Consulte utilizador tooa selecionando um resultado de pesquisa específico devolvido por uma consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="28c24-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="28c24-117">Um clique, geralmente, significa que um documento é um resultado relevante para uma consulta de pesquisa específico.</span><span class="sxs-lookup"><span data-stu-id="28c24-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="28c24-118">Ao ligar os eventos de pesquisa e clique em com um id de correlação, é possível tooanalyze comportamentos Olá utilizadores na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="28c24-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="28c24-119">Estas informações de pesquisa são tooobtain impossível com apenas registos de tráfego de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="28c24-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="28c24-120">Como tooimplement pesquisar a análise de tráfego</span><span class="sxs-lookup"><span data-stu-id="28c24-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="28c24-121">Olá sinais mencionados Olá anterior secção deve ser reunida a partir de aplicação de pesquisa de Olá como utilizador Olá interage com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="28c24-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="28c24-122">Application Insights é uma solução de monitorização extensível, disponível para várias plataformas, com opções de instrumentação flexível.</span><span class="sxs-lookup"><span data-stu-id="28c24-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="28c24-123">Utilização do Application Insights permite-lhe tirar partido de relatórios de pesquisa do Power BI do Olá criado através da análise de Olá toomake da Azure Search de dados.</span><span class="sxs-lookup"><span data-stu-id="28c24-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="28c24-124">No Olá [portal](https://portal.azure.com) página para o seu serviço da Azure Search, o painel de análise de tráfego de pesquisa de Olá contém uma cábula para seguir este padrão de telemetria.</span><span class="sxs-lookup"><span data-stu-id="28c24-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="28c24-125">Também pode selecionar ou criar um recurso do Application Insights e ver os dados necessários Olá, num só local.</span><span class="sxs-lookup"><span data-stu-id="28c24-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![Instruções de análise de tráfego de pesquisa][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="28c24-127">1. Selecione um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="28c24-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="28c24-128">Precisa de tooselect um toouse de recurso do Application Insights ou criar um se ainda não tiver um.</span><span class="sxs-lookup"><span data-stu-id="28c24-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="28c24-129">Pode utilizar um recurso que já em utilização toolog Olá necessitou eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="28c24-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="28c24-130">Ao criar um novo recurso do Application Insights, todos os tipos de aplicação são válidos para este cenário.</span><span class="sxs-lookup"><span data-stu-id="28c24-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="28c24-131">Selecione Olá um que melhor se adequa plataforma Olá que estiver a utilizar.</span><span class="sxs-lookup"><span data-stu-id="28c24-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="28c24-132">Terá de chave de instrumentação Olá para criar o cliente de telemetria de Olá para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="28c24-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="28c24-133">Pode obtê-lo a partir do dashboard do portal Olá Application Insights ou, pode obtê-lo da página de análise de tráfego de pesquisa de Olá, selecionar a instância de Olá pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="28c24-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="28c24-134">2. Instrumente a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="28c24-134">2. Instrument your application</span></span>

<span data-ttu-id="28c24-135">Esta fase é onde instrumente a sua própria aplicação de pesquisa, utilizando o recurso do Application Insights Olá sua Olá criada no passo acima.</span><span class="sxs-lookup"><span data-stu-id="28c24-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="28c24-136">Existem quatro passos toothis processo:</span><span class="sxs-lookup"><span data-stu-id="28c24-136">There are four steps toothis process:</span></span>

<span data-ttu-id="28c24-137">**POSSO. Criar um cliente de telemetria** este é o objeto de Olá que envia eventos toohello recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="28c24-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="28c24-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="28c24-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="28c24-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="28c24-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="28c24-140">Para outros idiomas e plataformas, consulte Olá concluída [lista](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="28c24-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="28c24-141">**II. Um ID de pesquisa para correlação de pedido** toocorrelate pesquisa pedidos com cliques, é necessário toohave um id de correlação que está relacionada com estes dois eventos distintos.</span><span class="sxs-lookup"><span data-stu-id="28c24-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="28c24-142">A pesquisa do Azure fornece um Id de pesquisa quando solicitá-la com um cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="28c24-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="28c24-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="28c24-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="28c24-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="28c24-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="28c24-145">**III. Registo de eventos de pesquisa**</span><span class="sxs-lookup"><span data-stu-id="28c24-145">**III. Log Search events**</span></span>

<span data-ttu-id="28c24-146">Sempre que um pedido de pesquisa é emitido por um utilizador, deve iniciar que como um evento de procura com Olá seguindo o esquema de um evento personalizado do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="28c24-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="28c24-147">**ServiceName**: nome do serviço de pesquisa (cadeia) **SearchId**: identificador de exclusivo (guid) da consulta de pesquisa de Olá (vem na resposta de pesquisa de Olá) **IndexName**: índice de serviço de pesquisa (cadeia) toobe consultado **QueryTerms**: termos de pesquisa (cadeia) introduzidos pelo utilizador Olá **o parâmetro ResultCount**: (int) número de documentos que foram devolvidas (vem na resposta de pesquisa de Olá)  **ScoringProfile**: nome Olá classificação perfil utilizado, caso existam (cadeia)</span><span class="sxs-lookup"><span data-stu-id="28c24-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="28c24-148">Contagem de pedidos em consultas gerados pelo utilizador adicionando $count = true tooyour consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="28c24-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="28c24-149">Ver mais informação [aqui](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="28c24-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="28c24-150">Lembre-se a consultas de pesquisa de registo tooonly que são geradas pelos utilizadores.</span><span class="sxs-lookup"><span data-stu-id="28c24-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="28c24-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="28c24-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="28c24-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="28c24-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="28c24-153">**IV. Clique em de registo eventos**</span><span class="sxs-lookup"><span data-stu-id="28c24-153">**IV. Log Click events**</span></span>

<span data-ttu-id="28c24-154">Sempre que um utilizador clica num documento, que é um sinal de que tem de ter sessão iniciado para efeitos de análise de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="28c24-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="28c24-155">Utilize o Application Insights eventos personalizados toolog estes eventos com Olá esquema os seguintes:</span><span class="sxs-lookup"><span data-stu-id="28c24-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="28c24-156">**ServiceName**: nome do serviço de pesquisa (cadeia) **SearchId**: identificador de exclusivo (guid) da consulta de pesquisa relacionados Olá **DocId**: identificador de documento (cadeia) **posição** : página de resultados de classificação (int) do documento Olá na pesquisa de Olá</span><span class="sxs-lookup"><span data-stu-id="28c24-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="28c24-157">Posição refere-se toohello cardinal ordem na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="28c24-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="28c24-158">São gratuita tooset este número, desde sempre tem hello iguais, tooallow para comparação.</span><span class="sxs-lookup"><span data-stu-id="28c24-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="28c24-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="28c24-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="28c24-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="28c24-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="28c24-161">3. Analisar com o ambiente de trabalho do Power BI</span><span class="sxs-lookup"><span data-stu-id="28c24-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="28c24-162">Depois de ter instrumentados a sua aplicação e verificar a que sua aplicação está corretamente ligada tooApplication Insights, pode utilizar um modelo predefinido criado pelo Azure Search para ambiente de trabalho do Power BI.</span><span class="sxs-lookup"><span data-stu-id="28c24-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="28c24-163">Este modelo contém gráficos e tabelas que o ajudam a efetuar tooimprove de decisões mais informada o desempenho de pesquisa e relevância.</span><span class="sxs-lookup"><span data-stu-id="28c24-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="28c24-164">tooinstantiate Olá Power BI ambiente de trabalho modelo, precisa de três informações sobre o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="28c24-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="28c24-165">Estes dados podem ser encontrados na página de análise de tráfego de pesquisa de Olá, quando seleciona Olá recursos toouse</span><span class="sxs-lookup"><span data-stu-id="28c24-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Application Insights dados no painel de análise de tráfego de pesquisa de Olá][2]

<span data-ttu-id="28c24-167">Métricas incluídas num modelo de ambiente de trabalho Olá Power BI:</span><span class="sxs-lookup"><span data-stu-id="28c24-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="28c24-168">Clique em através de velocidade (CTR): o rácio de utilizadores que clique num número específico de documento toohello de pesquisas totais.</span><span class="sxs-lookup"><span data-stu-id="28c24-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="28c24-169">Procura sem cliques: termos de licenciamento para cima consultas que não registar nenhum cliques</span><span class="sxs-lookup"><span data-stu-id="28c24-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="28c24-170">Clicou mais documentos: clicado mais documentos por ID de Olá últimas 24 horas, 7 dias e 30 dias.</span><span class="sxs-lookup"><span data-stu-id="28c24-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="28c24-171">Pares de documento de termo populares: termos de licenciamento que resultam numa Olá clica no mesmo documento, ordenadas pelo cliques.</span><span class="sxs-lookup"><span data-stu-id="28c24-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="28c24-172">Tempo tooclick: cliques agrupadosm por tempo decorrido desde a consulta de pesquisa de Olá</span><span class="sxs-lookup"><span data-stu-id="28c24-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Modelo de BI de energia para ler a partir do Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="28c24-174">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="28c24-174">Next Steps</span></span>
<span data-ttu-id="28c24-175">Instrumente a sua pesquisa aplicação tooget poderosa e insightful dados sobre o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="28c24-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="28c24-176">Pode encontrar mais informações sobre o Application Insights [aqui](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="28c24-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="28c24-177">Visite o Application Insights [página de preços](https://azure.microsoft.com/pricing/details/application-insights/) toolearn mais informações sobre os diferentes escalões de serviço.</span><span class="sxs-lookup"><span data-stu-id="28c24-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="28c24-178">Saiba mais sobre a criação de relatórios incrível.</span><span class="sxs-lookup"><span data-stu-id="28c24-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="28c24-179">Consulte [introdução ao Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="28c24-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
