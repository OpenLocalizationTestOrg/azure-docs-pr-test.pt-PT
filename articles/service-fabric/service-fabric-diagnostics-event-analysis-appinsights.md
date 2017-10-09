---
title: "aaaAzure análise de eventos de recursos de infraestrutura de serviço com o Application Insights | Microsoft Docs"
description: "Saiba mais sobre como visualizar e analisar eventos utilizando o Application Insights para monitorização e diagnóstico de clusters de Service Fabric do Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Análise de eventos e visualização com o Application Insights

Azure Application Insights é uma plataforma extensível para monitorização de aplicações e de diagnóstico. Inclui uma análise poderosa e consultar a ferramenta, dashboard personalizável e visualizações e ainda mais opções, incluindo automática de alertas. É Olá recomendado plataforma para a monitorização e diagnóstico de serviços e aplicações de Service Fabric.

## <a name="setting-up-application-insights"></a>Configurar o Application Insights

### <a name="creating-an-ai-resource"></a>Criar um recurso de AI

recurso toocreate um AI head através de toohello Azure Marketplace e procurar "Application Insights". Deve aparecer como solução primeiro Olá (está sob a categoria "Web + móvel"). Clique em **criar** quando está a visualizar recursos direita Olá (confirmar que o caminho de corresponde à imagem de Olá abaixo).

![Novo recurso do Application Insights](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

Terá de toofill saída algumas informações tooprovision Olá de recursos corretamente. No Olá *tipo de aplicação* campo, utilize "Uma aplicação web ASP.NET" se irá utilizar qualquer um dos recursos de infraestrutura de serviço do modelos de programação ou publicação de um cluster de toohello de aplicações de .NET. Se for implementar convidado executáveis e contentores, utilize "Geral". Em geral, predefinição toousing "Uma aplicação web ASP.NET" tookeep as opções de abrir no Olá futura. nome de Olá segurança tooyour preferência e se o grupo de recursos de Olá e subscrição pós-implementação das partições de recurso Olá. Recomendamos que o recurso de AI está a ser Olá mesmo grupo de recursos do seu cluster. Se precisar de mais informações, consulte [crie um recurso do Application Insights](../application-insights/app-insights-create-new-resource.md)

Terá de Olá chave de instrumentação AI tooconfigure AI com a ferramenta de agregação de eventos. Depois do recurso de AI configurado (demora alguns minutos após a implementação de Olá é validada), navegue até tooit e determinar Olá **propriedades** secção na barra de navegação esquerdo Olá. Um novo painel abre-se que mostra um *chave de instrumentação*. Se precisar de subscrição de Olá toochange ou grupo de recursos do recurso de Olá, pode ser feita aqui bem.

### <a name="configuring-ai-with-wad"></a>Configurar AI com WAD

Existem duas formas de primárias toosend dados WAD tooAzure AI, que são conseguidos ao adicionar uma configuração WAD toohello sink de AI, conforme detalhado em [neste artigo](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Adicionar uma chave de instrumentação AI quando criar um cluster no portal do Azure

![Adicionar um AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

Quando criar um cluster, se Diagnostics está ativada "", um campo opcional tooenter uma chave de instrumentação do Application Insights irá mostrar. Se colar a IKey AI aqui, sink Olá AI será automaticamente configurada por si no modelo do Resource Manager Olá que é utilizado toodeploy o cluster.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Adicionar Olá modelo de Gestor de recursos de toohello Sink de AI

No Olá "WadCfg" do modelo do Resource Manager Olá, adicione "Sink", incluindo Olá seguintes duas alterações:

1. Adicione configuração de receptores de Olá:

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. Inclua Olá Sink Olá DiagnosticMonitorConfiguration adicionando Olá seguinte linha no "DiagnosticMonitorConfiguration" de Olá "WadCfg":

    ```json
    "sinks": "applicationInsights"
    ```

Em ambos os fragmentos de código Olá acima, Olá o nome "applicationInsights" era sink de Olá toodescribe utilizados. Não é um requisito e desde que o nome de Olá do sink Olá está incluído no "sinks", pode definir a cadeia de tooany Olá nome.

Atualmente, os registos do cluster de Olá irão mostrar como rastreios no Visualizador de registo do AI. Uma vez que a maioria rastreios Olá provenientes da plataforma de Olá de nível "Informativa", pode considerar alterar Olá sink configuração tooonly enviar os registos do tipo "Críticas" ou "Error". Isto pode ser feito adicionando o sink de tooyour "Canais de", conforme demonstrado [neste artigo](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>Se utilizar um IKey AI incorreto no portal ou no seu modelo do Resource Manager, terá toomanually alterar a chave de Olá e atualizar cluster Olá / reimplementá-lo. 

### <a name="configuring-ai-with-eventflow"></a>Configurar AI com EventFlow

Se estiver a utilizar EventFlow tooaggregate eventos, certifique-se de que tooimport Olá `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`pacote NuGet. Olá seguinte tem toobe incluído no Olá *produz* secção Olá *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Efetuar alterações de Olá necessário de toomake se os filtros, bem como incluir quaisquer outras entradas (juntamente com os seus respetivos pacotes de NuGet).

## <a name="aisdk"></a>AI. SDK

Recomenda-se geralmente toouse EventFlow e WAD como soluções de agregação, porque permitem para um toodiagnostics abordagem mais modular e a monitorizar, ou seja, se quiser toochange as saídas da EventFlow, necessita de nenhum tooyour alteração real instrumentação, apenas um ficheiro de configuração de tooyour modificação simples. Se, no entanto, decidir tooinvest utilizando o Application Insights e não são toochange provável tooa diferentes plataforma, deve ter o aspeto na utilizando novo SDK do AI para agregar eventos e de lhes enviar tooAI. Isto significa que já não terá tooconfigure EventFlow toosend tooAI os dados, mas em vez disso, irá instalar pacotes de NuGet do Service Fabric do Olá ApplicationInsight. Podem ser encontrados detalhes no pacote de Olá [aqui](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Suportem de Application Insights para micro-serviços e contentores](https://azure.microsoft.com/app-insights-microservices/) mostra algumas das Olá novas funcionalidades que estão a ser trabalhadas (beta ainda atualmente no), que permitem-lhe toohave mais rica out of box opções de monitorização com AI. Estes incluem o controlo de dependência (utilizado na criação de um AppMap de todos os seus serviços e aplicações em cluster e Olá comunicação entre elas) e melhor correlação de rastreios dos seus serviços (ajuda-o no melhor pinpointing um problema no Olá do fluxo de trabalho de uma aplicação ou serviço).

Se estiver a desenvolver no .NET e será provavelmente estar através de alguns dos modelos de programação do Service Fabric e são disposto toouse AI como a plataforma para visualizar e analisar dados de registo de eventos e, em seguida, recomendamos que leia através de Olá rota AI SDK como a monitorização e fluxo de trabalho do diagnóstico. Leitura [isto](../application-insights/app-insights-asp-net-more.md) e [isto](../application-insights/app-insights-asp-net-trace-logs.md) tooget iniciado com a utilização de AI toocollect e apresentar os seus registos.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>A navegação em recursos de AI Olá no portal do Azure

Assim que tiver configurado o AI como uma saída para os eventos e registos, informações devem começar tooshow cópias de segurança no seu recurso AI dentro de alguns minutos. Navegue até o recurso de AI toohello, o que irá demorar, toohello AI dashboard de recursos. Clique em **pesquisa** Olá AI na barra de tarefas toosee Olá mais recentes rastreios que tiver recebido e toobe toofilter consegue através de-los.

*Explorador de métricas* é uma ferramenta útil para a criação de dashboards personalizados com base nas métricas que as aplicações, serviços e cluster podem ser Reporting Services. Consulte [explorar métricas no Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset segurança alguns gráficos para si com base nos dados de Olá está a recolher.

Ao clicar em **análise** leva-o portal do Application Insights Analytics toohello, onde pode consultar eventos e rastreios com o maior âmbito e optionality. Saiba mais sobre no [análise no Application Insights](../application-insights/app-insights-analytics.md).

## <a name="next-steps"></a>Passos seguintes

* [Configurar alertas no AI](../application-insights/app-insights-alerts.md) toobe notificado sobre as alterações no desempenho ou utilização
* [Smart deteção no Application Insights](../application-insights/app-insights-proactive-diagnostics.md) efetua uma análise de telemetria de Olá enviada tooAI toowarn proativa de potenciais problemas de desempenho
