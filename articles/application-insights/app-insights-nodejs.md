---
title: "Serviços de aaaMonitor Node.js com o Azure Application Insights | Microsoft Docs"
description: "Monitorize o desempenho e diagnostique problemas em serviços Node.js com o Application Insights."
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="1b011-103">Monitorizar os seus serviços e aplicações Node.js com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="1b011-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="1b011-104">[Azure Application Insights](app-insights-overview.md) monitoriza os seus serviços de back-end e componentes depois de implementá-las toohelp [detete e Diagnostique rapidamente o desempenho e outros problemas](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="1b011-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="1b011-105">Utilize-o em serviços Node.js alojados em qualquer sítio, no seu datacenter, em VMs do Azure, em Aplicações Web e, inclusivamente, noutras clouds públicas.</span><span class="sxs-lookup"><span data-stu-id="1b011-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="1b011-106">tooreceive, armazenar e explore os dados de monitorização, siga Olá seguir instruções tooinclude um agente no seu código e configurar um recurso do Application Insights correspondente no Azure.</span><span class="sxs-lookup"><span data-stu-id="1b011-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="1b011-107">agente de Olá envia recurso dos toothat de dados para análise adicional e exploração.</span><span class="sxs-lookup"><span data-stu-id="1b011-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="1b011-108">agente de Node.js Olá automaticamente pode monitorizar recebidos e enviados HTTP pedidos, vários sistema métricas e exceções.</span><span class="sxs-lookup"><span data-stu-id="1b011-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="1b011-109">A partir da versão v0.20, também pode monitorizar alguns pacotes de terceiros comuns, como `mongodb`, `mysql` e `redis`.</span><span class="sxs-lookup"><span data-stu-id="1b011-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="1b011-110">Todos os eventos relacionados com o pedido de HTTP recebido tooan são correlacionado para resolução de problemas mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="1b011-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="1b011-111">Pode monitorizar mais aspetos da sua aplicação e de sistema por manualmente instrumentação-los através da API de agente Olá descrito mais à frente.</span><span class="sxs-lookup"><span data-stu-id="1b011-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![Gráficos de exemplo da monitorização do desempenho](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="1b011-113">Introdução</span><span class="sxs-lookup"><span data-stu-id="1b011-113">Getting Started</span></span>

<span data-ttu-id="1b011-114">Vamos avançar para a configuração da monitorização de um serviço ou aplicação.</span><span class="sxs-lookup"><span data-stu-id="1b011-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="1b011-115"><a name="resource"></a>Configurar um recurso do App Insights</span><span class="sxs-lookup"><span data-stu-id="1b011-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="1b011-116">**Antes de começar**, certifique-se de que tem uma subscrição do Azure ou [obtenha uma nova gratuitamente][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="1b011-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="1b011-117">Se a sua organização já tem uma subscrição do Azure, pode seguir um administrador [estas instruções] [ add-aad-user] tooadd tooit.</span><span class="sxs-lookup"><span data-stu-id="1b011-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="1b011-118">Agora iniciar sessão toohello [portal do Azure] [ portal] e crie um recurso do Application Insights, conforme ilustrado no seguinte Olá - clique em "Novo" > "Ferramentas de programador" > "Application Insights".</span><span class="sxs-lookup"><span data-stu-id="1b011-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="1b011-119">recurso de Olá inclui um ponto final para receber dados de telemetria, o armazenamento para estes dados, guardada relatórios e dashboards, regra e configuração de alerta e muito mais.</span><span class="sxs-lookup"><span data-stu-id="1b011-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Criar um recurso do App Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="1b011-121">Na página de criação de recursos de Olá, escolha "Aplicação Node.js" de Olá aplicação tipo pendente.</span><span class="sxs-lookup"><span data-stu-id="1b011-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="1b011-122">tipo de aplicação Olá determina conjunto predefinido de Olá dos dashboards e relatórios criados por si.</span><span class="sxs-lookup"><span data-stu-id="1b011-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="1b011-123">Mas não se preocupe. Todos os recursos do App Insights podem, efetivamente, recolher dados de qualquer linguagem e plataforma.</span><span class="sxs-lookup"><span data-stu-id="1b011-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Formulário de recurso novo do App Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="1b011-125"><a name="agent"></a>Configurar o agente de Node.js Olá</span><span class="sxs-lookup"><span data-stu-id="1b011-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="1b011-126">Agora é agente de Olá tooinclude tempo na sua aplicação para que este possa reunir dados.</span><span class="sxs-lookup"><span data-stu-id="1b011-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="1b011-127">Comece por copiar a chave de instrumentação do recurso (hereinafter referido tooas sua `ikey`) do portal de Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1b011-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="1b011-128">Olá Insights aplicação sistema utiliza este tooyour de dados de chave toomap recursos do Azure, por isso terá de toospecify-lo numa variável de ambiente ou o código para Olá toouse de agente.</span><span class="sxs-lookup"><span data-stu-id="1b011-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![Copiar a chave de instrumentação](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="1b011-130">Em seguida, adicione as dependências de Olá Node.js agente biblioteca tooyour da aplicação através de Package. JSON.</span><span class="sxs-lookup"><span data-stu-id="1b011-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="1b011-131">A partir da pasta raiz de Olá da sua aplicação, execute:</span><span class="sxs-lookup"><span data-stu-id="1b011-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="1b011-132">Agora é preciso tooexplicitly carregamento da biblioteca Olá no seu código.</span><span class="sxs-lookup"><span data-stu-id="1b011-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="1b011-133">Porque o agente de Olá injects instrumentação em muitas outras bibliotecas, deve carregá-lo antecipadamente quanto possível, mesmo antes de outros `require` instruções.</span><span class="sxs-lookup"><span data-stu-id="1b011-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="1b011-134">tooget iniciado, Olá parte superior do seu primeiro ficheiro. js adicionar:</span><span class="sxs-lookup"><span data-stu-id="1b011-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="1b011-135">Olá `setup` método configura a chave de instrumentação Olá (e, consequentemente, os recursos do Azure) toobe utilizado por predefinição para todos os controlado itens.</span><span class="sxs-lookup"><span data-stu-id="1b011-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="1b011-136">Chamar `start` após a conclusão da configuração toobegin terminar recolha e envio de dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="1b011-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="1b011-137">Também pode fornecer um ikey através de variável de ambiente de Olá APPINSIGHTS\_INSTRUMENTATIONKEY em vez de passou-a manualmente demasiado `setup()` ou `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="1b011-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="1b011-138">Esta prática permite-lhe manter ikeys fora do código de origem consolidada e toospecify ikeys diferente para os diferentes ambientes.</span><span class="sxs-lookup"><span data-stu-id="1b011-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="1b011-139">Estão documentadas abaixo opções de configuração adicionais.</span><span class="sxs-lookup"><span data-stu-id="1b011-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="1b011-140">Pode tentar agente Olá sem enviar telemetria definindo Olá instrumentação tooany chave de cadeia não vazia.</span><span class="sxs-lookup"><span data-stu-id="1b011-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="1b011-141"><a name="monitor"></a> Monitorizar a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="1b011-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="1b011-142">agente de Olá reúne automaticamente telemetria sobre o tempo de execução do Olá Node.js e alguns módulos de terceiros comuns.</span><span class="sxs-lookup"><span data-stu-id="1b011-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="1b011-143">Utilize o toogenerate agora de aplicação alguns destes dados.</span><span class="sxs-lookup"><span data-stu-id="1b011-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="1b011-144">Em seguida, no Olá [portal do Azure] [ portal] procurar toohello recurso do Application Insights que criou anteriormente e procure o primeiro alguns pontos de dados na linha de tempo da descrição geral Olá, tal como em Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="1b011-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="1b011-145">Clique nos gráficos de Olá para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="1b011-145">Click through hello charts for more details.</span></span>

![Primeiros pontos de dados](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="1b011-147">Clique em Olá aplicação mapa botão tooview Olá topologia detetada para a sua aplicação, tal como em Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="1b011-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="1b011-148">Clique nos componentes no mapa de Olá para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="1b011-148">Click through components in hello map for more details.</span></span>

![Mapa de aplicação individual](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="1b011-150">Saiba mais sobre a sua aplicação e resolver problemas utilizando Olá outras vistas disponíveis em Olá "Investigar" secção.</span><span class="sxs-lookup"><span data-stu-id="1b011-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![Secção Investigar](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="1b011-152">Não existem dados?</span><span class="sxs-lookup"><span data-stu-id="1b011-152">No data?</span></span>

<span data-ttu-id="1b011-153">Porque o agente de Olá lotes de dados para submissão pode existir um atraso itens são apresentados no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="1b011-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="1b011-154">Se não vir dados no seu recurso experimente algumas das Olá seguintes correções:</span><span class="sxs-lookup"><span data-stu-id="1b011-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="1b011-155">Utilizar a aplicação Olá algumas mais; efetuar mais ações toogenerate mais telemetria.</span><span class="sxs-lookup"><span data-stu-id="1b011-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="1b011-156">Clique em **atualizar** na vista de portal recursos Olá.</span><span class="sxs-lookup"><span data-stu-id="1b011-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="1b011-157">Os gráficos automaticamente atualizam próprios periodicamente mas atualizar força este toohappen imediatamente.</span><span class="sxs-lookup"><span data-stu-id="1b011-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="1b011-158">Confirme que as [portas de saída necessárias](app-insights-ip-addresses.md) estão abertas.</span><span class="sxs-lookup"><span data-stu-id="1b011-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="1b011-159">Abra Olá [pesquisa](app-insights-diagnostic-search.md) mosaico e procure eventos individuais.</span><span class="sxs-lookup"><span data-stu-id="1b011-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="1b011-160">Verifique Olá [FAQ][].</span><span class="sxs-lookup"><span data-stu-id="1b011-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="1b011-161">Configuração do Agente</span><span class="sxs-lookup"><span data-stu-id="1b011-161">Agent Configuration</span></span>

<span data-ttu-id="1b011-162">Seguem-se métodos de configuração do agente de Olá e os respetivos valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="1b011-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="1b011-163">eventos de correlacionar toofully num serviço, ser tooset se `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="1b011-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="1b011-164">Isto permite que o agente de Olá tootrack contexto em chamadas de retorno assíncronas no Node.js.</span><span class="sxs-lookup"><span data-stu-id="1b011-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a><span data-ttu-id="1b011-165">API de Agente</span><span class="sxs-lookup"><span data-stu-id="1b011-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="1b011-166">Olá API .NET do agente é descrito totalmente [aqui](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="1b011-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="1b011-167">Pode controlar qualquer pedido, eventos, métrica ou exceção utilizando Olá Application Insights Node.js cliente.</span><span class="sxs-lookup"><span data-stu-id="1b011-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="1b011-168">Olá exemplo seguinte demonstra Algumas das Olá as APIs disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1b011-168">hello following example demonstrates some of hello available APIs.</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="1b011-169">Monitorizar as dependências</span><span class="sxs-lookup"><span data-stu-id="1b011-169">Track your dependencies</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="1b011-170">Adicionar eventos de tooall uma propriedade personalizada</span><span class="sxs-lookup"><span data-stu-id="1b011-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="1b011-171">Monitorizar pedidos HTTP GET</span><span class="sxs-lookup"><span data-stu-id="1b011-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="1b011-172">Monitorizar o tempo de arranque do servidor</span><span class="sxs-lookup"><span data-stu-id="1b011-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="1b011-173">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="1b011-173">More resources</span></span>

* [<span data-ttu-id="1b011-174">Monitorizar a telemetria no portal de Olá</span><span class="sxs-lookup"><span data-stu-id="1b011-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="1b011-175">Escrever consultas de análise sobre a telemetria</span><span class="sxs-lookup"><span data-stu-id="1b011-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[FAQ]: app-insights-troubleshoot-faq.md
