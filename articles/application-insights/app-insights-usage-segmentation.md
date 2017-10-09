---
title: "análise de aaaUser, sessão e eventos no Azure Application Insights | Documentos da Microsoft"
description: "Análise demográficas dos utilizadores da sua aplicação web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="d2a60-103">Análise de utilizadores, sessões e os eventos no Application Insights</span><span class="sxs-lookup"><span data-stu-id="d2a60-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="d2a60-104">Determinar quando pessoas utilizam a sua aplicação web, as páginas que está a mais interessados, onde estão localizados os seus utilizadores, que sistemas operativos e browsers utilizam.</span><span class="sxs-lookup"><span data-stu-id="d2a60-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="d2a60-105">Analisar o negócio e telemetria de utilização através da utilização de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d2a60-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="d2a60-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="d2a60-106">Get started</span></span>

<span data-ttu-id="d2a60-107">Se não vir ainda dados Olá utilizadores, sessões ou painéis de eventos no portal do Application Insights Olá, [Saiba como utilizar a tooget com ferramentas de utilização de Olá](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d2a60-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="d2a60-108">ferramenta de segmentação de utilizadores, sessões e os eventos de Olá</span><span class="sxs-lookup"><span data-stu-id="d2a60-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="d2a60-109">Três utilizam painéis de utilização de Olá Olá mesma ferramenta tooslice e organizam telemetria da sua aplicação web de três perspetivas.</span><span class="sxs-lookup"><span data-stu-id="d2a60-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="d2a60-110">Ao filtrar e dividir dados Olá, pode descobrir informações sobre a utilização de relativo Olá das páginas diferentes e funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="d2a60-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="d2a60-111">**Ferramenta de utilizadores**: como muitas pessoas utilizado a aplicação e as respetivas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="d2a60-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="d2a60-112">Os utilizadores são contados utilizando IDs anónimos armazenados em cookies do browser.</span><span class="sxs-lookup"><span data-stu-id="d2a60-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="d2a60-113">Uma única pessoa através de browsers diferentes ou máquinas será contada como mais do que um utilizador.</span><span class="sxs-lookup"><span data-stu-id="d2a60-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="d2a60-114">**Ferramenta de sessões**: O número de sessões de atividade do utilizador tem incluído determinadas páginas e funcionalidades da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d2a60-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="d2a60-115">Uma sessão é contabilizada após a meia hora de inatividade do utilizador, ou após contínua 24 horas de utilização.</span><span class="sxs-lookup"><span data-stu-id="d2a60-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="d2a60-116">**Ferramenta de eventos**: com que frequência são utilizadas determinadas páginas e funcionalidades da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d2a60-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="d2a60-117">Uma vista de página é contabilizada quando um browser carrega uma página da sua aplicação fornecida tem [instrumentadas-](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="d2a60-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="d2a60-118">Um evento personalizado representa uma ocorrência de algo acontecer na sua aplicação, muitas vezes, uma interação do utilizador como um botão clique ou Olá concluir algumas tarefas.</span><span class="sxs-lookup"><span data-stu-id="d2a60-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="d2a60-119">Inserir código na sua aplicação demasiado[gerar eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="d2a60-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Ferramenta de utilização](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="d2a60-121">Consultar determinados utilizadores</span><span class="sxs-lookup"><span data-stu-id="d2a60-121">Querying for Certain Users</span></span> 

<span data-ttu-id="d2a60-122">Explore a diferentes grupos de utilizadores ao ajustar as opções de consulta de Olá na parte superior de Olá da ferramenta de utilizadores Olá:</span><span class="sxs-lookup"><span data-stu-id="d2a60-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="d2a60-123">Quem utilizada: escolha eventos personalizados e vistas de página.</span><span class="sxs-lookup"><span data-stu-id="d2a60-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="d2a60-124">Durante a: Escolha um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="d2a60-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="d2a60-125">Por: Escolha como toobucket Olá dados, por um período de tempo ou por outra propriedade como browser ou uma localidade.</span><span class="sxs-lookup"><span data-stu-id="d2a60-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="d2a60-126">Dividir por: Escolha uma propriedade ao que dados de Olá toosplit ou segmento.</span><span class="sxs-lookup"><span data-stu-id="d2a60-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="d2a60-127">Adicionar filtros: Limitar os utilizadores toocertain da consulta Olá, sessões ou eventos com base nas respetivas propriedades, tais como o browser ou uma localidade.</span><span class="sxs-lookup"><span data-stu-id="d2a60-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="d2a60-128">Guardar e partilhar relatórios</span><span class="sxs-lookup"><span data-stu-id="d2a60-128">Saving and sharing reports</span></span> 
<span data-ttu-id="d2a60-129">Pode guardar relatórios de utilizadores, ou privada tooyou apenas na secção dos meus relatórios hello, ou partilhado com todas as pessoas pessoa com acesso toothis recurso do Application Insights no Olá secção relatórios partilhado.</span><span class="sxs-lookup"><span data-stu-id="d2a60-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="d2a60-130">Ao guardar um relatório ou editar as respetivas propriedades, escolha toosave "Relativo intervalo de tempo atual", que um relatório será continuamente atualizada de dados, retroceder alguma quantidade de tempo fixa.</span><span class="sxs-lookup"><span data-stu-id="d2a60-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="d2a60-131">Escolha o "Intervalo atual de tempo absoluto" toosave um relatório com um conjunto de dados fixo.</span><span class="sxs-lookup"><span data-stu-id="d2a60-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="d2a60-132">Tenha em atenção que os dados no Application Insights apenas são armazenados durante 90 dias, pelo que o se passem mais do que 90 dias desde um relatório com um intervalo de tempo absoluto foi guardada, relatório de Olá aparecerá em branco.</span><span class="sxs-lookup"><span data-stu-id="d2a60-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="d2a60-133">Instâncias de exemplo</span><span class="sxs-lookup"><span data-stu-id="d2a60-133">Example instances</span></span>

<span data-ttu-id="d2a60-134">secção de instâncias de exemplo de Olá mostra informações sobre alguns a utilizadores individuais, sessões ou eventos que são correspondidos por consulta atual Olá.</span><span class="sxs-lookup"><span data-stu-id="d2a60-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="d2a60-135">Considerar e explorar os comportamentos Olá indivíduos, em adição tooaggregates, podem fornecer informações sobre como as pessoas utilizam, na verdade, a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d2a60-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="d2a60-136">Informações</span><span class="sxs-lookup"><span data-stu-id="d2a60-136">Insights</span></span> 

<span data-ttu-id="d2a60-137">barra lateral Insights de Olá mostra grandes clusters de utilizadores que partilham propriedades comuns.</span><span class="sxs-lookup"><span data-stu-id="d2a60-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="d2a60-138">Esses clusters podem descobrir tendências surprising na forma como as pessoas utilizam a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d2a60-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="d2a60-139">Por exemplo, se 40% de utilização de Olá da sua aplicação todo provenientes de pessoas através de uma funcionalidade único.</span><span class="sxs-lookup"><span data-stu-id="d2a60-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="d2a60-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d2a60-140">Next steps</span></span>
- <span data-ttu-id="d2a60-141">utilização de tooenable experiências, começar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [vistas de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="d2a60-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="d2a60-142">Se já enviar eventos personalizados ou vistas de página, explore Olá utilização ferramentas toolearn como os utilizadores utilizam o serviço.</span><span class="sxs-lookup"><span data-stu-id="d2a60-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="d2a60-143">Funis</span><span class="sxs-lookup"><span data-stu-id="d2a60-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="d2a60-144">Retenção</span><span class="sxs-lookup"><span data-stu-id="d2a60-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="d2a60-145">Fluxos do Utilizador</span><span class="sxs-lookup"><span data-stu-id="d2a60-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="d2a60-146">Livros</span><span class="sxs-lookup"><span data-stu-id="d2a60-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="d2a60-147">Adicionar o contexto de utilizador</span><span class="sxs-lookup"><span data-stu-id="d2a60-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

