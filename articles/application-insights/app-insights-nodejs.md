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
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Monitorizar os seus serviços e aplicações Node.js com o Application Insights

[Azure Application Insights](app-insights-overview.md) monitoriza os seus serviços de back-end e componentes depois de implementá-las toohelp [detete e Diagnostique rapidamente o desempenho e outros problemas](app-insights-detect-triage-diagnose.md). Utilize-o em serviços Node.js alojados em qualquer sítio, no seu datacenter, em VMs do Azure, em Aplicações Web e, inclusivamente, noutras clouds públicas.

tooreceive, armazenar e explore os dados de monitorização, siga Olá seguir instruções tooinclude um agente no seu código e configurar um recurso do Application Insights correspondente no Azure. agente de Olá envia recurso dos toothat de dados para análise adicional e exploração.

agente de Node.js Olá automaticamente pode monitorizar recebidos e enviados HTTP pedidos, vários sistema métricas e exceções. A partir da versão v0.20, também pode monitorizar alguns pacotes de terceiros comuns, como `mongodb`, `mysql` e `redis`. Todos os eventos relacionados com o pedido de HTTP recebido tooan são correlacionado para resolução de problemas mais rapidamente.

Pode monitorizar mais aspetos da sua aplicação e de sistema por manualmente instrumentação-los através da API de agente Olá descrito mais à frente.

![Gráficos de exemplo da monitorização do desempenho](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>Introdução

Vamos avançar para a configuração da monitorização de um serviço ou aplicação.

### <a name="resource"></a>Configurar um recurso do App Insights

**Antes de começar**, certifique-se de que tem uma subscrição do Azure ou [obtenha uma nova gratuitamente][azure-free-offer]. Se a sua organização já tem uma subscrição do Azure, pode seguir um administrador [estas instruções] [ add-aad-user] tooadd tooit.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

Agora iniciar sessão toohello [portal do Azure] [ portal] e crie um recurso do Application Insights, conforme ilustrado no seguinte Olá - clique em "Novo" > "Ferramentas de programador" > "Application Insights". recurso de Olá inclui um ponto final para receber dados de telemetria, o armazenamento para estes dados, guardada relatórios e dashboards, regra e configuração de alerta e muito mais.

![Criar um recurso do App Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

Na página de criação de recursos de Olá, escolha "Aplicação Node.js" de Olá aplicação tipo pendente. tipo de aplicação Olá determina conjunto predefinido de Olá dos dashboards e relatórios criados por si. Mas não se preocupe. Todos os recursos do App Insights podem, efetivamente, recolher dados de qualquer linguagem e plataforma.

![Formulário de recurso novo do App Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Configurar o agente de Node.js Olá

Agora é agente de Olá tooinclude tempo na sua aplicação para que este possa reunir dados.
Comece por copiar a chave de instrumentação do recurso (hereinafter referido tooas sua `ikey`) do portal de Olá, conforme mostrado abaixo. Olá Insights aplicação sistema utiliza este tooyour de dados de chave toomap recursos do Azure, por isso terá de toospecify-lo numa variável de ambiente ou o código para Olá toouse de agente.  

![Copiar a chave de instrumentação](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

Em seguida, adicione as dependências de Olá Node.js agente biblioteca tooyour da aplicação através de Package. JSON. A partir da pasta raiz de Olá da sua aplicação, execute:

```bash
npm install applicationinsights --save
```

Agora é preciso tooexplicitly carregamento da biblioteca Olá no seu código. Porque o agente de Olá injects instrumentação em muitas outras bibliotecas, deve carregá-lo antecipadamente quanto possível, mesmo antes de outros `require` instruções. tooget iniciado, Olá parte superior do seu primeiro ficheiro. js adicionar:

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

Olá `setup` método configura a chave de instrumentação Olá (e, consequentemente, os recursos do Azure) toobe utilizado por predefinição para todos os controlado itens. Chamar `start` após a conclusão da configuração toobegin terminar recolha e envio de dados de telemetria.

Também pode fornecer um ikey através de variável de ambiente de Olá APPINSIGHTS\_INSTRUMENTATIONKEY em vez de passou-a manualmente demasiado `setup()` ou `getClient()`. Esta prática permite-lhe manter ikeys fora do código de origem consolidada e toospecify ikeys diferente para os diferentes ambientes.

Estão documentadas abaixo opções de configuração adicionais.

Pode tentar agente Olá sem enviar telemetria definindo Olá instrumentação tooany chave de cadeia não vazia.

### <a name="monitor"></a> Monitorizar a sua aplicação

agente de Olá reúne automaticamente telemetria sobre o tempo de execução do Olá Node.js e alguns módulos de terceiros comuns. Utilize o toogenerate agora de aplicação alguns destes dados.

Em seguida, no Olá [portal do Azure] [ portal] procurar toohello recurso do Application Insights que criou anteriormente e procure o primeiro alguns pontos de dados na linha de tempo da descrição geral Olá, tal como em Olá seguinte imagem. Clique nos gráficos de Olá para obter mais detalhes.

![Primeiros pontos de dados](./media/app-insights-nodejs/12-first-perf.png)

Clique em Olá aplicação mapa botão tooview Olá topologia detetada para a sua aplicação, tal como em Olá seguinte imagem. Clique nos componentes no mapa de Olá para obter mais detalhes.

![Mapa de aplicação individual](./media/app-insights-nodejs/06-appinsights_appmap.png)

Saiba mais sobre a sua aplicação e resolver problemas utilizando Olá outras vistas disponíveis em Olá "Investigar" secção.

![Secção Investigar](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>Não existem dados?

Porque o agente de Olá lotes de dados para submissão pode existir um atraso itens são apresentados no portal de Olá. Se não vir dados no seu recurso experimente algumas das Olá seguintes correções:

* Utilizar a aplicação Olá algumas mais; efetuar mais ações toogenerate mais telemetria.
* Clique em **atualizar** na vista de portal recursos Olá. Os gráficos automaticamente atualizam próprios periodicamente mas atualizar força este toohappen imediatamente.
* Confirme que as [portas de saída necessárias](app-insights-ip-addresses.md) estão abertas.
* Abra Olá [pesquisa](app-insights-diagnostic-search.md) mosaico e procure eventos individuais.
* Verifique Olá [FAQ][].


## <a name="agent-configuration"></a>Configuração do Agente

Seguem-se métodos de configuração do agente de Olá e os respetivos valores predefinidos.

eventos de correlacionar toofully num serviço, ser tooset se `.setAutoDependencyCorrelation(true)`. Isto permite que o agente de Olá tootrack contexto em chamadas de retorno assíncronas no Node.js.

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

## <a name="agent-api"></a>API de Agente

<!-- TODO: Fully document agent API. -->

Olá API .NET do agente é descrito totalmente [aqui](app-insights-api-custom-events-metrics.md).

Pode controlar qualquer pedido, eventos, métrica ou exceção utilizando Olá Application Insights Node.js cliente. Olá exemplo seguinte demonstra Algumas das Olá as APIs disponíveis.

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

### <a name="track-your-dependencies"></a>Monitorizar as dependências

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

### <a name="add-a-custom-property-tooall-events"></a>Adicionar eventos de tooall uma propriedade personalizada

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>Monitorizar pedidos HTTP GET

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>Monitorizar o tempo de arranque do servidor

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>Mais recursos

* [Monitorizar a telemetria no portal de Olá](app-insights-dashboards.md)
* [Escrever consultas de análise sobre a telemetria](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[FAQ]: app-insights-troubleshoot-faq.md
