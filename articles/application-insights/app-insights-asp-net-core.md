---
title: aaaAzure Application Insights para o ASP.NET Core | Microsoft Docs
description: "Monitorizar aplicações web de disponibilidade, desempenho e utilização."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="f4da3-103">Application Insights para Núcleo do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f4da3-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="f4da3-104">[Application Insights](app-insights-overview.md) permite-lhe monitorizar a sua aplicação web de disponibilidade, desempenho e utilização.</span><span class="sxs-lookup"><span data-stu-id="f4da3-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="f4da3-105">Com comentários de Olá que obter sobre o desempenho de Olá e eficácia da sua aplicação no Olá universal, pode efetuar escolhas-se informado sobre direção Olá da estrutura de Olá em cada ciclo de vida de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f4da3-105">With hello feedback you get about hello performance and effectiveness of your app in hello wild, you can make informed choices about hello direction of hello design in each development lifecycle.</span></span>

![Exemplo](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="f4da3-107">Irá precisar de uma subscrição com [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4da3-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="f4da3-108">Inicie sessão com uma conta Microsoft, que poderá ter para o Windows, o XBox Live ou outros serviços cloud do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f4da3-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="f4da3-109">A equipa pode ter uma subscrição organizacional tooAzure: pedir Olá proprietário tooadd tooit utilizando a sua conta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f4da3-109">Your team might have an organizational subscription tooAzure: ask hello owner tooadd you tooit using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f4da3-110">Introdução</span><span class="sxs-lookup"><span data-stu-id="f4da3-110">Getting started</span></span>

* <span data-ttu-id="f4da3-111">No Explorador de soluções do Visual Studio, clique no seu projeto e selecione **configurar o Application Insights**, ou **adicionar > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="f4da3-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="f4da3-112">[Saiba mais](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="f4da3-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="f4da3-113">Se não vir os comandos de menu, siga Olá [manual guia de introdução ao obter](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="f4da3-113">If you don't see those menu commands, follow hello [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="f4da3-114">Poderá ser necessário toodo este caso o projeto foi criado com uma versão do Visual Studio antes de 2017.</span><span class="sxs-lookup"><span data-stu-id="f4da3-114">You may need toodo this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="f4da3-115">A utilizar o Application Insights</span><span class="sxs-lookup"><span data-stu-id="f4da3-115">Using Application Insights</span></span>
<span data-ttu-id="f4da3-116">Inicie sessão em Olá [portal do Microsoft Azure](https://portal.azure.com), selecione **todos os recursos** ou **Application Insights**e, em seguida, selecione o recurso de Olá criou toomonitor a aplicação.</span><span class="sxs-lookup"><span data-stu-id="f4da3-116">Sign into hello [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select hello resource you created toomonitor your app.</span></span>

<span data-ttu-id="f4da3-117">Na janela de browser separados, utilize a aplicação de tempo.</span><span class="sxs-lookup"><span data-stu-id="f4da3-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="f4da3-118">Irá ver os dados que aparecem nos gráficos de Application Insights Olá.</span><span class="sxs-lookup"><span data-stu-id="f4da3-118">You'll see data appearing in hello Application Insights charts.</span></span> <span data-ttu-id="f4da3-119">(Poderá ter tooclick atualização). Haverá apenas uma pequena quantidade de dados enquanto estiver a desenvolver, mas estes gráficos realmente entrem alive quando publicar a aplicação e têm vários utilizadores.</span><span class="sxs-lookup"><span data-stu-id="f4da3-119">(You might have tooclick Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="f4da3-120">página de descrição geral de Olá mostra gráficos de chave de desempenho: tempo de resposta do servidor, o tempo de carregamento de página e contagens de pedidos falhados.</span><span class="sxs-lookup"><span data-stu-id="f4da3-120">hello overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="f4da3-121">Clique em qualquer gráfico toosee mais dados e gráficos.</span><span class="sxs-lookup"><span data-stu-id="f4da3-121">Click any chart toosee more charts and data.</span></span>

<span data-ttu-id="f4da3-122">Vistas no portal de Olá enquadram-se em três categorias principais:</span><span class="sxs-lookup"><span data-stu-id="f4da3-122">Views in hello portal fall into three main categories:</span></span>

* <span data-ttu-id="f4da3-123">[Explorador de métricas](app-insights-metrics-explorer.md) mostra gráficos e tabelas de métricas e contagens, tais como tempos de resposta, taxas de falha ou as métricas de criar manualmente com Olá [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f4da3-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="f4da3-124">Filtro e o segmento de dados de Olá por tooget de valores de propriedade uma melhor compreensão da sua aplicação e os seus utilizadores.</span><span class="sxs-lookup"><span data-stu-id="f4da3-124">Filter and segment hello data by property values tooget a better understanding of your app and its users.</span></span>
* <span data-ttu-id="f4da3-125">[Explorador de pesquisa](app-insights-diagnostic-search.md) apresenta uma lista de eventos individuais, tais como pedidos específicos, exceções, rastreios de registo ou eventos criados por si com Olá [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f4da3-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="f4da3-126">Filtrar e procurar eventos Olá e navegar entre os problemas de tooinvestigate eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f4da3-126">Filter and search in hello events, and navigate among related events tooinvestigate issues.</span></span>
* <span data-ttu-id="f4da3-127">[Análise de](app-insights-analytics.md) permite-lhe executar consultas de como o SQL Server ao longo da sua telemetria e é uma ferramenta poderosa de analítica e de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="f4da3-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="f4da3-128">Alertas</span><span class="sxs-lookup"><span data-stu-id="f4da3-128">Alerts</span></span>
* <span data-ttu-id="f4da3-129">Obter automaticamente [proativa alertas diagnóstico](app-insights-proactive-diagnostics.md) que indicam sobre alterações anómalas taxas de falha e outras métricas.</span><span class="sxs-lookup"><span data-stu-id="f4da3-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="f4da3-130">Configurar [testes de disponibilidade](app-insights-monitor-web-app-availability.md) tootest seu Web site continuamente a partir de localizações em todo o mundo e obter e-mails, assim que qualquer falha de teste.</span><span class="sxs-lookup"><span data-stu-id="f4da3-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) tootest your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="f4da3-131">Configurar [alertas métricas](app-insights-monitor-web-app-availability.md) tooknow se métricas como tempos de resposta ou taxas de exceção aceda exteriores limites aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="f4da3-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) tooknow if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="f4da3-132">Vídeo</span><span class="sxs-lookup"><span data-stu-id="f4da3-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="f4da3-133">Código fonte aberto</span><span class="sxs-lookup"><span data-stu-id="f4da3-133">Open source</span></span>
[<span data-ttu-id="f4da3-134">Ler e contribuir toohello código</span><span class="sxs-lookup"><span data-stu-id="f4da3-134">Read and contribute toohello code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="f4da3-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f4da3-135">Next steps</span></span>
* <span data-ttu-id="f4da3-136">[Adicionar telemetria tooyour web páginas](app-insights-javascript.md) toomonitor página utilização e desempenho.</span><span class="sxs-lookup"><span data-stu-id="f4da3-136">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page usage and performance.</span></span>
* <span data-ttu-id="f4da3-137">[Monitorizar dependências](app-insights-asp-net-dependencies.md) toosee se REST, SQL Server ou outros recursos externos são abrandamento.</span><span class="sxs-lookup"><span data-stu-id="f4da3-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) toosee if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="f4da3-138">[Utilize a API de Olá](app-insights-api-custom-events-metrics.md) toosend os seus próprios eventos e as métricas para uma vista mais detalhada do desempenho e a utilização da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="f4da3-138">[Use hello API](app-insights-api-custom-events-metrics.md) toosend your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="f4da3-139">[Testes de disponibilidade](app-insights-monitor-web-app-availability.md) Verifique a aplicação constantemente a partir em torno Olá mundo.</span><span class="sxs-lookup"><span data-stu-id="f4da3-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around hello world.</span></span> 

