---
title: "aaaAzure Application Insights suporte para vários componentes, micro-serviços e contentores | Microsoft Docs"
description: "Monitorização de aplicações que consistem em vários componentes do ou funções para o desempenho e utilização."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>Monitorizar aplicações com múltiplos componente com o Application Insights (pré-visualização)

Pode monitorizar as aplicações que consistem de vários componentes de servidor, funções ou serviços com [Azure Application Insights](app-insights-overview.md). Estado de funcionamento de Olá dos componentes de Olá e relações de Olá entre eles são apresentados num mapa de aplicação único. Pode analisar individuais operações através de vários componentes com a correlação de HTTP automática. Diagnóstico de contentor pode ser integrado e correlacionado com a telemetria da aplicação. Utilize um único recurso do Application Insights para todos os componentes de Olá da sua aplicação. 

![Mapa de múltiplos componente da aplicação](./media/app-insights-monitor-multi-role-apps/app-map.png)

Utilizamos 'componente' toomean aqui qualquer parte de uma aplicação grande funcionar. Por exemplo, uma aplicação comercial normal pode consistir em código de cliente em execução nos browsers da web, falar com tooone ou mais serviços de aplicação web, que por sua vez voltar a utilizar serviços de fim. Componentes de servidor podem ser alojado no local na nuvem de Olá, poderão ser funções da web e de trabalho do Azure ou podem executar nos contentores, tais como Docker ou de Service Fabric. 

### <a name="sharing-a-single-application-insights-resource"></a>Partilhar um único recurso do Application Insights 

Olá chave técnica aqui é toosend a telemetria de cada componente no seu toohello aplicação mesmo recurso do Application Insights, mas utilize Olá `cloud_RoleName` componentes de toodistinguish propriedade quando for necessário. Olá Application Insights SDK adiciona Olá `cloud_RoleName` emissão de componentes de telemetria de toohello de propriedade. Por exemplo, Olá SDK irá adicionar um nome do web site ou toohello de nome de função de serviço `cloud_RoleName` propriedade. Pode substituir este valor com um telemetryinitializer. Olá o mapeamento de aplicações utiliza Olá `cloud_RoleName` propriedade tooidentify Olá componentes mapa Olá.

Para obter mais informações sobre como substituir Olá `cloud_RoleName` propriedade consulte [adicionar propriedades: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).  

Em alguns casos, este não poderá ser apropriado e pode preferir toouse recursos separados para diferentes grupos de componentes. Por exemplo, poderá ter toouse diferentes recursos de gestão ou fins de faturação. Utilizar recursos separados significa que não veja todos os componentes de Olá apresentados num mapa de aplicação único; e que não é possível consultar componentes no [análise](app-insights-analytics.md). Também tem tooset recursos separado Olá.

Com esse advertência, iremos assumir resto Olá deste documento que pretende que os dados de toosend de vários componentes tooone recurso do Application Insights.

## <a name="configure-multi-component-applications"></a>Configurar aplicações com múltiplos componente

mapa de uma aplicação com múltiplos componente tooget, tem de tooachieve estes objetivos:

* **Instalar a versão de pré-lançamento mais recente Olá** pacote do Application Insights em cada componente da aplicação Olá. 
* **Partilhar um único recurso do Application Insights** para Olá todos os componentes da aplicação.
* **Ativar o mapa de aplicação de função Multi** no painel de pré-visualizações Olá.

Configure cada componente da aplicação utilizando o método adequado Olá para o respetivo tipo. ([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)

### <a name="1-install-hello-latest-pre-release-package"></a>1. Instalar o pacote de versão de pré-lançamento Olá mais recente

Atualizar ou instalar pacotes de Appication Insights Olá no projeto de Olá para cada componente do servidor. Se estiver a utilizar o Visual Studio:

1. Um projeto com o botão direito e selecione **gerir pacotes NuGet**. 
2. Selecione **incluir pré-lançamento**.
3. Se o Application Insights pacotes são apresentados nas atualizações, selecione-os. 

    Caso contrário, procurar e instalar pacote adequado Olá:
    
    * Microsoft.ApplicationInsights.WindowsServer
    * Microsoft.ApplicationInsights.ServiceFabric - de componentes em execução como convidado executáveis e contentores de Docker a executar uma aplicação de Service Fabric em
    * Microsoft.ApplicationInsights.ServiceFabric.Native - fiável dos serviços de no ServiceFabric aplicações
    * Microsoft.ApplicationInsights.Kubernetes de componentes em execução no Docker Kubernetes

### <a name="2-share-a-single-application-insights-resource"></a>2. Partilhar um único recurso do Application Insights

* No Visual Studio, clique com o botão direito um projeto e selecione **configurar o Application Insights**, ou **Application Insights > configurar**. Para o primeiro projeto Olá, utilize Olá assistente toocreate um recurso do Application Insights. Para projetos subsequentes, selecione Olá mesmo recurso.
* Se não houver nenhuma menu do Application Insights, configure manualmente:

   1. No [portal do Azure](https://portal,azure.com), abra o recurso do Application Insights Olá já criado para outro componente.
   2. No painel de descrição geral de Olá, separador de abrir Olá pendente Essentials e Olá cópia **chave de instrumentação.**
   3. No seu projeto, abra Applicationinsights e inserir:`<InstrumentationKey>your copied key</InstrumentationKey>`

![Copiar ficheiro. config do Olá instrumentação toohello chave](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3. Ativar função multi o mapeamento de aplicações

No portal do Azure Olá, abra o recurso Olá para a sua aplicação. No painel de pré-visualizações Olá, ativar *mapa de aplicação de função Multi*.

### <a name="4-enable-docker-metrics-optional"></a>4. Ativar as métricas de Docker (opcional) 

Se um componente é executado num Docker alojada em VM Windows do Azure, pode recolher métricas adicionais do contentor de Olá. Insira-o no seu [diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md) ficheiro de configuração:

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>Utilizar cloud_RoleName tooseparate componentes

Olá `cloud_RoleName` propriedade é anexado tooall telemetria. Identifica componente Olá - serviço ou função Olá - que origina telemetria Olá. (É não Olá mesmo como cloud_RoleInstance, que separa idênticas funções que estejam a executar em paralelo em vários processos de servidor ou máquinas.)

No portal de Olá, pode filtrar ou segmentar a telemetria com esta propriedade. Neste exemplo, o painel de falhas de Olá é tooshow filtrado informações apenas do serviço de front-end web Olá, filtragem de falhas de back-end de API do CRM de Olá:

![Métrico gráfico segmentado pelo nome da função de nuvem](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>Operações de rastreio entre componentes

Pode rastrear a partir de um componente tooanother, as chamadas de Olá efetuadas ao processar uma operação individual.


![Mostrar a telemetria para a operação](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

Clicar tooa lista correlacionado de telemetria para esta operação no servidor web front-end de Olá e Olá API de back-end:

![Componentes de pesquisa](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>Passos seguintes

* [Telemetria separada de desenvolvimento, teste e produção](app-insights-separate-resources.md)
