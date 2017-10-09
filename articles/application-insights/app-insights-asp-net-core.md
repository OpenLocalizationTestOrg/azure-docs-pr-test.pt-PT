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
# <a name="application-insights-for-aspnet-core"></a>Application Insights para Núcleo do ASP.NET
[Application Insights](app-insights-overview.md) permite-lhe monitorizar a sua aplicação web de disponibilidade, desempenho e utilização. Com comentários de Olá que obter sobre o desempenho de Olá e eficácia da sua aplicação no Olá universal, pode efetuar escolhas-se informado sobre direção Olá da estrutura de Olá em cada ciclo de vida de desenvolvimento.

![Exemplo](./media/app-insights-asp-net-core/sample.png)

Irá precisar de uma subscrição com [Microsoft Azure](http://azure.com). Inicie sessão com uma conta Microsoft, que poderá ter para o Windows, o XBox Live ou outros serviços cloud do Microsoft. A equipa pode ter uma subscrição organizacional tooAzure: pedir Olá proprietário tooadd tooit utilizando a sua conta Microsoft.

## <a name="getting-started"></a>Introdução

* No Explorador de soluções do Visual Studio, clique no seu projeto e selecione **configurar o Application Insights**, ou **adicionar > Application Insights**. [Saiba mais](app-insights-asp-net.md).
* Se não vir os comandos de menu, siga Olá [manual guia de introdução ao obter](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started). Poderá ser necessário toodo este caso o projeto foi criado com uma versão do Visual Studio antes de 2017.

## <a name="using-application-insights"></a>A utilizar o Application Insights
Inicie sessão em Olá [portal do Microsoft Azure](https://portal.azure.com), selecione **todos os recursos** ou **Application Insights**e, em seguida, selecione o recurso de Olá criou toomonitor a aplicação.

Na janela de browser separados, utilize a aplicação de tempo. Irá ver os dados que aparecem nos gráficos de Application Insights Olá. (Poderá ter tooclick atualização). Haverá apenas uma pequena quantidade de dados enquanto estiver a desenvolver, mas estes gráficos realmente entrem alive quando publicar a aplicação e têm vários utilizadores. 

página de descrição geral de Olá mostra gráficos de chave de desempenho: tempo de resposta do servidor, o tempo de carregamento de página e contagens de pedidos falhados. Clique em qualquer gráfico toosee mais dados e gráficos.

Vistas no portal de Olá enquadram-se em três categorias principais:

* [Explorador de métricas](app-insights-metrics-explorer.md) mostra gráficos e tabelas de métricas e contagens, tais como tempos de resposta, taxas de falha ou as métricas de criar manualmente com Olá [API](app-insights-api-custom-events-metrics.md). Filtro e o segmento de dados de Olá por tooget de valores de propriedade uma melhor compreensão da sua aplicação e os seus utilizadores.
* [Explorador de pesquisa](app-insights-diagnostic-search.md) apresenta uma lista de eventos individuais, tais como pedidos específicos, exceções, rastreios de registo ou eventos criados por si com Olá [API](app-insights-api-custom-events-metrics.md). Filtrar e procurar eventos Olá e navegar entre os problemas de tooinvestigate eventos relacionados.
* [Análise de](app-insights-analytics.md) permite-lhe executar consultas de como o SQL Server ao longo da sua telemetria e é uma ferramenta poderosa de analítica e de diagnóstico.

## <a name="alerts"></a>Alertas
* Obter automaticamente [proativa alertas diagnóstico](app-insights-proactive-diagnostics.md) que indicam sobre alterações anómalas taxas de falha e outras métricas.
* Configurar [testes de disponibilidade](app-insights-monitor-web-app-availability.md) tootest seu Web site continuamente a partir de localizações em todo o mundo e obter e-mails, assim que qualquer falha de teste.
* Configurar [alertas métricas](app-insights-monitor-web-app-availability.md) tooknow se métricas como tempos de resposta ou taxas de exceção aceda exteriores limites aceitáveis.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>Código fonte aberto
[Ler e contribuir toohello código](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>Passos seguintes
* [Adicionar telemetria tooyour web páginas](app-insights-javascript.md) toomonitor página utilização e desempenho.
* [Monitorizar dependências](app-insights-asp-net-dependencies.md) toosee se REST, SQL Server ou outros recursos externos são abrandamento.
* [Utilize a API de Olá](app-insights-api-custom-events-metrics.md) toosend os seus próprios eventos e as métricas para uma vista mais detalhada do desempenho e a utilização da sua aplicação.
* [Testes de disponibilidade](app-insights-monitor-web-app-availability.md) Verifique a aplicação constantemente a partir em torno Olá mundo. 

