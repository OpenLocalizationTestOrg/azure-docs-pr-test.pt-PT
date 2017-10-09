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
# <a name="what-is-search-traffic-analytics"></a>O que é a análise de tráfego de pesquisa
Análise de tráfego de pesquisa é um padrão para implementar um ciclo de comentários do seu serviço de pesquisa. Este padrão descreve os dados necessários Olá e como toocollect-la utilizando o Application Insights, um leader da indústria para monitorização dos serviços em várias plataformas.

Análise de tráfego de pesquisa permite-lhe ganhar visibilidade ao seu serviço de pesquisa e desbloquear informações sobre os seus utilizadores e do respetivo comportamento. Fazendo com que dados sobre o que escolhem os seus utilizadores, é possível toomake decisões que melhorar ainda mais a experiência de pesquisa e tooback desativado quando resultados de Olá são não que o esperado.

A pesquisa do Azure oferece uma solução de telemetria que integra o Azure Application Insights e o Power BI tooprovide aprofundada de monitorização e controlo. Uma vez interação com a Azure Search é apenas através de APIs, tem de ser implementada telemetria Olá pelos programadores Olá utilizando a pesquisa, seguir instruções Olá nesta página.

## <a name="identify-hello-relevant-search-data"></a>Identificar dados de pesquisa relevantes Olá

métricas de pesquisa útil toohave, é necessário toolog algumas sinalizar dos utilizadores Olá da aplicação de pesquisa de Olá. Estes sinais significam conteúdo que os utilizadores estão interessados nas e de que o considerar relevante tootheir precisa.

Existem dois sinais que tem de análise de tráfego de pesquisa:

1. Eventos de pesquisa de gerados pelo utilizador: apenas consultas de pesquisa iniciadas por um utilizador são interessantes. Procurar pedidos utilizados toopopulate aspetos, o conteúdo adicional quaisquer informações internas, não são importantes e poderem prejudicar e bias os resultados.

2. Eventos de clique gerados pelo utilizador: por cliques neste documento, vamos Consulte utilizador tooa selecionando um resultado de pesquisa específico devolvido por uma consulta de pesquisa. Um clique, geralmente, significa que um documento é um resultado relevante para uma consulta de pesquisa específico.

Ao ligar os eventos de pesquisa e clique em com um id de correlação, é possível tooanalyze comportamentos Olá utilizadores na sua aplicação. Estas informações de pesquisa são tooobtain impossível com apenas registos de tráfego de pesquisa.

## <a name="how-tooimplement-search-traffic-analytics"></a>Como tooimplement pesquisar a análise de tráfego

Olá sinais mencionados Olá anterior secção deve ser reunida a partir de aplicação de pesquisa de Olá como utilizador Olá interage com o mesmo. Application Insights é uma solução de monitorização extensível, disponível para várias plataformas, com opções de instrumentação flexível. Utilização do Application Insights permite-lhe tirar partido de relatórios de pesquisa do Power BI do Olá criado através da análise de Olá toomake da Azure Search de dados.

No Olá [portal](https://portal.azure.com) página para o seu serviço da Azure Search, o painel de análise de tráfego de pesquisa de Olá contém uma cábula para seguir este padrão de telemetria. Também pode selecionar ou criar um recurso do Application Insights e ver os dados necessários Olá, num só local.

![Instruções de análise de tráfego de pesquisa][1]

### <a name="1-select-an-application-insights-resource"></a>1. Selecione um recurso do Application Insights

Precisa de tooselect um toouse de recurso do Application Insights ou criar um se ainda não tiver um. Pode utilizar um recurso que já em utilização toolog Olá necessitou eventos personalizados.

Ao criar um novo recurso do Application Insights, todos os tipos de aplicação são válidos para este cenário. Selecione Olá um que melhor se adequa plataforma Olá que estiver a utilizar.

Terá de chave de instrumentação Olá para criar o cliente de telemetria de Olá para a sua aplicação. Pode obtê-lo a partir do dashboard do portal Olá Application Insights ou, pode obtê-lo da página de análise de tráfego de pesquisa de Olá, selecionar a instância de Olá pretende toouse.

### <a name="2-instrument-your-application"></a>2. Instrumente a sua aplicação

Esta fase é onde instrumente a sua própria aplicação de pesquisa, utilizando o recurso do Application Insights Olá sua Olá criada no passo acima. Existem quatro passos toothis processo:

**POSSO. Criar um cliente de telemetria** este é o objeto de Olá que envia eventos toohello recurso do Application Insights.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

Para outros idiomas e plataformas, consulte Olá concluída [lista](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).

**II. Um ID de pesquisa para correlação de pedido** toocorrelate pesquisa pedidos com cliques, é necessário toohave um id de correlação que está relacionada com estes dois eventos distintos. A pesquisa do Azure fornece um Id de pesquisa quando solicitá-la com um cabeçalho:

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. Registo de eventos de pesquisa**

Sempre que um pedido de pesquisa é emitido por um utilizador, deve iniciar que como um evento de procura com Olá seguindo o esquema de um evento personalizado do Application Insights:

**ServiceName**: nome do serviço de pesquisa (cadeia) **SearchId**: identificador de exclusivo (guid) da consulta de pesquisa de Olá (vem na resposta de pesquisa de Olá) **IndexName**: índice de serviço de pesquisa (cadeia) toobe consultado **QueryTerms**: termos de pesquisa (cadeia) introduzidos pelo utilizador Olá **o parâmetro ResultCount**: (int) número de documentos que foram devolvidas (vem na resposta de pesquisa de Olá)  **ScoringProfile**: nome Olá classificação perfil utilizado, caso existam (cadeia)

> [!NOTE]
> Contagem de pedidos em consultas gerados pelo utilizador adicionando $count = true tooyour consulta de pesquisa. Ver mais informação [aqui](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)
>

> [!NOTE]
> Lembre-se a consultas de pesquisa de registo tooonly que são geradas pelos utilizadores.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. Clique em de registo eventos**

Sempre que um utilizador clica num documento, que é um sinal de que tem de ter sessão iniciado para efeitos de análise de pesquisa. Utilize o Application Insights eventos personalizados toolog estes eventos com Olá esquema os seguintes:

**ServiceName**: nome do serviço de pesquisa (cadeia) **SearchId**: identificador de exclusivo (guid) da consulta de pesquisa relacionados Olá **DocId**: identificador de documento (cadeia) **posição** : página de resultados de classificação (int) do documento Olá na pesquisa de Olá

> [!NOTE]
> Posição refere-se toohello cardinal ordem na sua aplicação. São gratuita tooset este número, desde sempre tem hello iguais, tooallow para comparação.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Analisar com o ambiente de trabalho do Power BI

Depois de ter instrumentados a sua aplicação e verificar a que sua aplicação está corretamente ligada tooApplication Insights, pode utilizar um modelo predefinido criado pelo Azure Search para ambiente de trabalho do Power BI.
Este modelo contém gráficos e tabelas que o ajudam a efetuar tooimprove de decisões mais informada o desempenho de pesquisa e relevância.

tooinstantiate Olá Power BI ambiente de trabalho modelo, precisa de três informações sobre o Application Insights. Estes dados podem ser encontrados na página de análise de tráfego de pesquisa de Olá, quando seleciona Olá recursos toouse

![Application Insights dados no painel de análise de tráfego de pesquisa de Olá][2]

Métricas incluídas num modelo de ambiente de trabalho Olá Power BI:

*   Clique em através de velocidade (CTR): o rácio de utilizadores que clique num número específico de documento toohello de pesquisas totais.
*   Procura sem cliques: termos de licenciamento para cima consultas que não registar nenhum cliques
*   Clicou mais documentos: clicado mais documentos por ID de Olá últimas 24 horas, 7 dias e 30 dias.
*   Pares de documento de termo populares: termos de licenciamento que resultam numa Olá clica no mesmo documento, ordenadas pelo cliques.
*   Tempo tooclick: cliques agrupadosm por tempo decorrido desde a consulta de pesquisa de Olá

![Modelo de BI de energia para ler a partir do Application Insights][3]


## <a name="next-steps"></a>Passos Seguintes
Instrumente a sua pesquisa aplicação tooget poderosa e insightful dados sobre o serviço de pesquisa.

Pode encontrar mais informações sobre o Application Insights [aqui](https://go.microsoft.com/fwlink/?linkid=842905). Visite o Application Insights [página de preços](https://azure.microsoft.com/pricing/details/application-insights/) toolearn mais informações sobre os diferentes escalões de serviço.

Saiba mais sobre a criação de relatórios incrível. Consulte [introdução ao Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) para obter detalhes

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
