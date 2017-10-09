---
title: "análise de aaaUsage para aplicações web com o Azure Application Insights | Documentos da Microsoft"
description: "Compreenda os seus utilizadores e o que fazer com a sua aplicação web."
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="cd67f-103">Análise da utilização de aplicações web com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="cd67f-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="cd67f-104">As funcionalidades da sua aplicação web são mais populares?</span><span class="sxs-lookup"><span data-stu-id="cd67f-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="cd67f-105">Os seus utilizadores alcançar os seus objetivos com a sua aplicação?</span><span class="sxs-lookup"><span data-stu-id="cd67f-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="cd67f-106">De remover estes em determinado pontos e volte mais tarde?</span><span class="sxs-lookup"><span data-stu-id="cd67f-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="cd67f-107">[Azure Application Insights](app-insights-overview.md) ajuda-o a obter informações acerca poderosas como as pessoas utilizam a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="cd67f-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="cd67f-108">Sempre que atualizar a sua aplicação, pode avaliar o quão bem funciona para os utilizadores.</span><span class="sxs-lookup"><span data-stu-id="cd67f-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="cd67f-109">Com este conhecimento, pode efetuar dados orientada por tomar decisões sobre a sua próximas ciclos de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="cd67f-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="cd67f-110">Enviar a telemetria da sua aplicação</span><span class="sxs-lookup"><span data-stu-id="cd67f-110">Send telemetry from your app</span></span>

<span data-ttu-id="cd67f-111">melhor experiência de Olá é obtida pela instalação do Application Insights no seu código de servidor de aplicação tanto nas suas páginas web.</span><span class="sxs-lookup"><span data-stu-id="cd67f-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="cd67f-112">os componentes de cliente e servidor Olá da sua aplicação enviam telemetria back toohello portal do Azure para análise.</span><span class="sxs-lookup"><span data-stu-id="cd67f-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="cd67f-113">**Código do servidor:** instalar módulo adequado de Olá para o seu [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), ou [outros](app-insights-platforms.md) aplicação.</span><span class="sxs-lookup"><span data-stu-id="cd67f-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="cd67f-114">*Não pretende o código do servidor tooinstall? Apenas [crie um recurso do Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="cd67f-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="cd67f-115">**Código de página Web:** Olá abra [portal do Azure](https://portal.azure.com), abra o recurso do Application Insights Olá para a sua aplicação e, em seguida, abra **introdução > monitorizar e diagnosticar do lado do cliente**.</span><span class="sxs-lookup"><span data-stu-id="cd67f-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copie o script Olá para o cabeçalho de Olá da sua página web mestra.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="cd67f-117">**Obter telemetria:** executar o projeto no modo de depuração para alguns minutos e, em seguida, procure os resultados no painel de descrição geral de Olá no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cd67f-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="cd67f-118">Publicar a aplicação toomonitor o desempenho da aplicação e saber que os utilizadores estão a fazer com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="cd67f-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="cd67f-119">Inclui o ID de utilizador e de sessão na sua telemetria</span><span class="sxs-lookup"><span data-stu-id="cd67f-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="cd67f-120">tootrack utilizadores ao longo do tempo, o Application Insights requer uma forma tooidentify-los.</span><span class="sxs-lookup"><span data-stu-id="cd67f-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="cd67f-121">Eventos de Olá ferramenta é Olá única ferramenta de utilização que não requer um ID de utilizador ou um ID de sessão.</span><span class="sxs-lookup"><span data-stu-id="cd67f-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="cd67f-122">Iniciar o envio destes IDs [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="cd67f-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="cd67f-123">Explorar demografia de utilização e estatísticas</span><span class="sxs-lookup"><span data-stu-id="cd67f-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="cd67f-124">Determinar quando as pessoas utilizam a sua aplicação, as páginas que está a mais interessados, onde estão localizados os seus utilizadores, que sistemas operativos e browsers utilizam.</span><span class="sxs-lookup"><span data-stu-id="cd67f-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="cd67f-125">relatórios de utilizadores e sessões Olá filtre os dados por páginas ou eventos personalizados e segmentá-los por propriedades, tais como a localização e o ambiente e página.</span><span class="sxs-lookup"><span data-stu-id="cd67f-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="cd67f-126">Também pode adicionar os seus próprios filtros.</span><span class="sxs-lookup"><span data-stu-id="cd67f-126">You can also add your own filters.</span></span>

![Utilizadores](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="cd67f-128">Conhecimentos aprofundados acerca do Olá direita realçar padrões interessantes no conjunto de Olá de dados.</span><span class="sxs-lookup"><span data-stu-id="cd67f-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="cd67f-129">Olá **utilizadores** relatório conta números de Olá de utilizadores exclusivos que aceder às suas páginas na sua períodos de tempo escolhido.</span><span class="sxs-lookup"><span data-stu-id="cd67f-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="cd67f-130">(Os utilizadores são contados através da utilização de cookies.</span><span class="sxs-lookup"><span data-stu-id="cd67f-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="cd67f-131">Se alguém acede ao seu site com as máquinas de cliente ou browsers diferentes ou limpa os cookies, em seguida, estes serão contados tendo mais do que uma vez.)</span><span class="sxs-lookup"><span data-stu-id="cd67f-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="cd67f-132">Olá **sessões** relatório conta o número de Olá de sessões de utilizador aceder ao site.</span><span class="sxs-lookup"><span data-stu-id="cd67f-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="cd67f-133">Uma sessão é um período de atividade por um utilizador, terminada por um período de inatividade de mais de metade uma hora.</span><span class="sxs-lookup"><span data-stu-id="cd67f-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="cd67f-134">Mais sobre as ferramentas de utilizadores, sessões e os eventos de Olá</span><span class="sxs-lookup"><span data-stu-id="cd67f-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="cd67f-135">Vistas de página</span><span class="sxs-lookup"><span data-stu-id="cd67f-135">Page views</span></span>

<span data-ttu-id="cd67f-136">No painel de utilização de Olá, clicar Olá vistas de página mosaico tooget uma análise detalhada das suas páginas mais populares:</span><span class="sxs-lookup"><span data-stu-id="cd67f-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![No painel de descrição geral de Olá, clique em Olá gráfico de vistas de página](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="cd67f-138">exemplo de Olá acima é de um web site de jogos.</span><span class="sxs-lookup"><span data-stu-id="cd67f-138">hello example above is from a games web site.</span></span> <span data-ttu-id="cd67f-139">De gráficos Olá, pode de forma instantânea, vemos:</span><span class="sxs-lookup"><span data-stu-id="cd67f-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="cd67f-140">Utilização não melhoradas no Olá na última semana.</span><span class="sxs-lookup"><span data-stu-id="cd67f-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="cd67f-141">Talvez é necessário pensar sobre a otimização de motor de pesquisa?</span><span class="sxs-lookup"><span data-stu-id="cd67f-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="cd67f-142">Tennis é Olá página de jogos mais popular.</span><span class="sxs-lookup"><span data-stu-id="cd67f-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="cd67f-143">Vamos concentrar-se na página de toothis mais melhoramentos.</span><span class="sxs-lookup"><span data-stu-id="cd67f-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="cd67f-144">Em média, visitados a página de Tennis Olá sobre três vezes por semana.</span><span class="sxs-lookup"><span data-stu-id="cd67f-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="cd67f-145">(Existem mais de cerca de três vezes sessões que os utilizadores.)</span><span class="sxs-lookup"><span data-stu-id="cd67f-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="cd67f-146">A maioria dos utilizadores visitam o site de Olá durante a semana do Olá E.U.A. trabalhar e, em horas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cd67f-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="cd67f-147">Talvez deve fornecemos um botão "Ocultar rápido" na página web que Olá.</span><span class="sxs-lookup"><span data-stu-id="cd67f-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="cd67f-148">Olá [anotações](app-insights-annotations.md) no gráfico de Olá mostrar quando novas versões do Web site de Olá foram implementadas.</span><span class="sxs-lookup"><span data-stu-id="cd67f-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="cd67f-149">Nenhuma das implementações recente Olá tinha um efeito considerável na utilização.</span><span class="sxs-lookup"><span data-stu-id="cd67f-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="cd67f-150">E se pretende que tooinvestigate Olá tráfego tooyour site em mais detalhe, como dividir por uma propriedade personalizada, que o site envia na sua telemetria de visualizações de página?</span><span class="sxs-lookup"><span data-stu-id="cd67f-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="cd67f-151">Abra Olá **eventos** ferramenta no menu de recurso do Application Insights Olá.</span><span class="sxs-lookup"><span data-stu-id="cd67f-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="cd67f-152">Esta ferramenta permite-lhe analisar quantos vistas de página e eventos personalizados foram enviados da sua aplicação, com base numa variedade de opções de filtragem, cohorting e segmentação.</span><span class="sxs-lookup"><span data-stu-id="cd67f-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="cd67f-153">Na lista pendente "Quem utilizada" Olá, selecione "Qualquer vista de página".</span><span class="sxs-lookup"><span data-stu-id="cd67f-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="cd67f-154">Na lista pendente de "Dividir por" Olá, selecione uma propriedade pela qual toosplit sua página de ver a telemetria.</span><span class="sxs-lookup"><span data-stu-id="cd67f-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="cd67f-155">Retenção - quantos utilizadores voltar?</span><span class="sxs-lookup"><span data-stu-id="cd67f-155">Retention - how many users come back?</span></span>

<span data-ttu-id="cd67f-156">Retenção ajuda-o a compreender com que frequência os seus utilizadores devolvem toouse as respetivas aplicações, com base no cohorts de utilizadores que efetuar qualquer ação do negócio durante um determinado registo de tempo.</span><span class="sxs-lookup"><span data-stu-id="cd67f-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="cd67f-157">Compreender as funcionalidades específicas fazer com que os utilizadores toocome back mais do que outras pessoas</span><span class="sxs-lookup"><span data-stu-id="cd67f-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="cd67f-158">Hypotheses de formulário com base nos dados de utilizador reais</span><span class="sxs-lookup"><span data-stu-id="cd67f-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="cd67f-159">Determinar se o período de retenção é um problema no seu produto</span><span class="sxs-lookup"><span data-stu-id="cd67f-159">Determine whether retention is a problem in your product</span></span> 

![Retenção](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="cd67f-161">controlos de retenção de Olá na parte superior permitem toodefine eventos específicos e retenção de toocalculate de intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="cd67f-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="cd67f-162">Olá gráfico no meio de Olá proporciona uma representação visual de Olá percentagem de retenção global por Olá intervalo de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="cd67f-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="cd67f-163">gráfico Olá na parte inferior de Olá representa retenção individual num determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="cd67f-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="cd67f-164">Este nível de detalhe permite-lhe toounderstand que os utilizadores estão a fazer e o que poderá afetar devolvidos utilizadores uma granularidade mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="cd67f-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="cd67f-165">Mais informações sobre a ferramenta de retenção de Olá</span><span class="sxs-lookup"><span data-stu-id="cd67f-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="cd67f-166">Eventos de negócio personalizado</span><span class="sxs-lookup"><span data-stu-id="cd67f-166">Custom business events</span></span>

<span data-ttu-id="cd67f-167">tooget uma compreensão clara dos que os utilizadores não com a sua aplicação web, é útil tooinsert linhas de eventos do código toolog personalizados.</span><span class="sxs-lookup"><span data-stu-id="cd67f-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="cd67f-168">Estes eventos podem controlar tudo de ações de utilizador de detalhado como clicar botões específicos, eventos de negócio significativas toomore como efetuar uma compra ou prevalecente um jogo.</span><span class="sxs-lookup"><span data-stu-id="cd67f-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="cd67f-169">Embora em alguns casos, as vistas de página podem representar eventos úteis, não se encontra verdadeiro em geral.</span><span class="sxs-lookup"><span data-stu-id="cd67f-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="cd67f-170">Um utilizador pode abrir uma página de produto, sem comprar produto Olá.</span><span class="sxs-lookup"><span data-stu-id="cd67f-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="cd67f-171">Com eventos empresariais específicos, pode gráfico progresso dos seus utilizadores através do seu site.</span><span class="sxs-lookup"><span data-stu-id="cd67f-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="cd67f-172">Pode saber as respetivas preferências para diferentes opções e em que o se remover out ou tem dificuldades.</span><span class="sxs-lookup"><span data-stu-id="cd67f-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="cd67f-173">Com este conhecimento, pode efetuar decisões informadas sobre prioridades Olá no seu registo de segurança de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="cd67f-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="cd67f-174">Eventos podem ser registados no Olá web página:</span><span class="sxs-lookup"><span data-stu-id="cd67f-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="cd67f-175">Ou, no lado do servidor de Olá da aplicação web de Olá:</span><span class="sxs-lookup"><span data-stu-id="cd67f-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="cd67f-176">Pode anexar eventos de toothese de valores de propriedade, para que possa filtrar ou dividir eventos Olá quando inspecioná-las no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="cd67f-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="cd67f-177">Além disso, um conjunto de propriedades padrão é evento tooeach anexado, por exemplo, o ID de utilizador anónimo, que permite a sequência de Olá tootrace das atividades de um utilizador individual.</span><span class="sxs-lookup"><span data-stu-id="cd67f-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="cd67f-178">Saiba mais sobre [eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent) e [propriedades](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="cd67f-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="cd67f-179">Eventos dividem e organizam</span><span class="sxs-lookup"><span data-stu-id="cd67f-179">Slice and dice events</span></span>

<span data-ttu-id="cd67f-180">Nas ferramentas de utilizadores, sessões e os eventos de Olá, pode segmentação e decomposição de eventos personalizados por utilizador, o nome de evento e propriedades.</span><span class="sxs-lookup"><span data-stu-id="cd67f-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="cd67f-181">![Utilizadores](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="cd67f-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="cd67f-182">Design Olá telemetria com aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="cd67f-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="cd67f-183">Ao conceber a cada funcionalidade da sua aplicação, considere como vai toomeasure respetivo êxito com os seus utilizadores.</span><span class="sxs-lookup"><span data-stu-id="cd67f-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="cd67f-184">Decida qual iniciar eventos empresariais precisam toorecord e code Olá chamadas para esses eventos de controlo na sua aplicação de Olá.</span><span class="sxs-lookup"><span data-stu-id="cd67f-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="cd67f-185">A | Testar B</span><span class="sxs-lookup"><span data-stu-id="cd67f-185">A | B Testing</span></span>
<span data-ttu-id="cd67f-186">Se não souber que a variante de uma funcionalidade que será mais bem sucedida, versão ambas, efetuar cada utilizadores toodifferent acessível.</span><span class="sxs-lookup"><span data-stu-id="cd67f-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="cd67f-187">Medir o sucesso de Olá de cada e, em seguida, mova versão unificada tooa.</span><span class="sxs-lookup"><span data-stu-id="cd67f-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="cd67f-188">Para esta técnica, anexar telemetria Olá de tooall de valores de propriedade de diferentes que é enviada por cada versão da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="cd67f-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="cd67f-189">Pode fazê-lo ao definir propriedades na Olá TelemetryContext Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd67f-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="cd67f-190">Estas propriedades predefinidas são adicionadas a mensagem de telemetria de tooevery Olá a aplicação envia - não apenas a mensagens personalizadas, mas Olá padrão telemetria bem.</span><span class="sxs-lookup"><span data-stu-id="cd67f-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="cd67f-191">No portal do Application Insights Olá, filtrar e dividir os dados nos valores de propriedade Olá, assim como versões diferentes do toocompare Olá.</span><span class="sxs-lookup"><span data-stu-id="cd67f-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="cd67f-192">toodo, [configurar um inicializador de telemetria](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="cd67f-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="cd67f-193">No inicializador de aplicação de web de Olá, tais como Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="cd67f-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="cd67f-194">Todos os TelemetryClients novo adicionam automaticamente a especificar o valor da propriedade Olá.</span><span class="sxs-lookup"><span data-stu-id="cd67f-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="cd67f-195">Eventos de telemetria individuais podem substituir os valores predefinidos de Olá.</span><span class="sxs-lookup"><span data-stu-id="cd67f-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd67f-196">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cd67f-196">Next steps</span></span>
   - [<span data-ttu-id="cd67f-197">Utilizadores, Sessões, Eventos</span><span class="sxs-lookup"><span data-stu-id="cd67f-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="cd67f-198">Funis</span><span class="sxs-lookup"><span data-stu-id="cd67f-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="cd67f-199">Retenção</span><span class="sxs-lookup"><span data-stu-id="cd67f-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="cd67f-200">Fluxos do Utilizador</span><span class="sxs-lookup"><span data-stu-id="cd67f-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="cd67f-201">Livros</span><span class="sxs-lookup"><span data-stu-id="cd67f-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="cd67f-202">Adicionar o contexto de utilizador</span><span class="sxs-lookup"><span data-stu-id="cd67f-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
