---
title: aaaAzure modelo de dados de telemetria do Application Insights | Microsoft Docs
description: "Descrição geral do Application Insights dados modelo"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Modelo de dados de telemetria do Application Insights

[Azure Application Insights](app-insights-overview.md) envia a telemetria da sua toohello de aplicação web portal do Azure, para que possa analisar o desempenho de Olá e a utilização da sua aplicação. modelo de telemetria de Olá está padronizado para que seja possível toocreate plataforma e independente de idioma de monitorização. 

Dados recolhidos pelo Application Insights modelos deste padrão de execução da aplicação típica:

![Modelo de aplicação do Application Insights](./media/application-insights-data-model/application-insights-data-model.png)

Olá seguintes tipos de telemetria são utilizados toomonitor Olá execução da sua aplicação. Olá seguintes três tipos são normalmente recolhidos automaticamente pelo Olá Application Insights SDK da estrutura da aplicação Olá web:

* [**Pedido** ](application-insights-data-model-request-telemetry.md) -gerado toolog um pedido recebido pela sua aplicação. Por exemplo, Olá web do Application Insights que SDK gera automaticamente um item de telemetria de pedido para cada pedido HTTP que recebe a sua aplicação web. 

    Um **operação** é Olá de threads de execução que processa um pedido. Também pode [escrever código](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor outros tipos de operação, tal como uma "reativar" numa web da tarefa ou periodicamente a função que processa os dados.  Cada operação tem um ID. Este ID que pode ser utilizados too[group]((application-insights-correlation.md) toda a telemetria gerada enquanto a aplicação está a processar o pedido de Olá. Cada operação ou com êxito ou falha e tem uma duração de tempo.
* [**Exceção** ](application-insights-data-model-exception-telemetry.md) -normalmente, representa uma exceção que faz com que uma operação toofail.
* [**Dependência** ](application-insights-data-model-dependency-telemetry.md) -representa uma chamada a partir do seu externo do serviço de aplicações tooan ou o armazenamento, como uma REST API ou SQL Server. No ASP.NET, tooSQL de chamadas de dependência são definidos pelo `System.Data`. Pontos finais de tooHTTP chamadas são definidos pelo `System.Net`. 

Application Insights fornece três tipos de dados adicionais para telemetria personalizada:

* [Rastreio](application-insights-data-model-trace-telemetry.md) - utilizado a diretamente ou através de um registo de diagnóstico do adaptador tooimplement utilizando uma arquitetura de instrumentação que está familiarizado tooyou, tais como `Log4Net` ou `System.Diagnostics`.
* [Evento](application-insights-data-model-event-telemetry.md) -normalmente utilizadas toocapture interação do utilizador com o serviço, tooanalyze padrões de utilização.
* [Métrica](application-insights-data-model-metric-telemetry.md) -utilizado tooreport valores de escalar periódica.

Todos os itens de telemetria podem definir Olá [informações de contexto](application-insights-data-model-context.md) como id de sessão de utilizador ou a versão de aplicação. O contexto é um conjunto de campos com tipo seguro que unblocks determinados cenários. Quando a versão da aplicação foi inicializada corretamente, o Application Insights pode detetar novos padrões no comportamento correlacionado com a reimplementação da aplicação. Id de sessão pode ser utilizado toocalculate Olá falha ou um problema impacto sobre os utilizadores. Calcular a contagem distinta de valores de id de sessão para determinados falhou a dependência, o rastreio de erro ou exceção crítica fornece uma boa compreensão de impacto.

Application Insights modelo telemetria define uma forma demasiado[correlacionar](application-insights-correlation.md) operação toohello de telemetria do qual faz parte. Por exemplo, um pedido pode solicitar uma base de dados SQL e registada informações de diagnóstico. Pode definir o contexto de correlação de Olá para esses itens de telemetria que associar-back toohello telemetria de pedido.

## <a name="schema-improvements"></a>Melhoramentos de esquema

Modelo de dados do Application Insights é um toomodel de forma simples e básico, mas poderosa telemetria da sua aplicação. Iremos esforçar-nos cenários essenciais do tookeep Olá modelo toosupport simples e slim e permitir que o esquema de Olá tooextend para utilização avançada.

problemas de modelo ou um esquema de dados de tooreport e sugestões de utilizam o GitHub [ApplicationInsights Home](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) repositório.

## <a name="next-steps"></a>Passos seguintes

- [Grave a telemetria personalizada](app-insights-api-custom-events-metrics.md)
- Saiba como demasiado[expandir e filtrar telemetria](app-insights-api-filtering-sampling.md).
- Utilize [amostragem](app-insights-sampling.md) toominimize quantidade de telemetria baseado no modelo de dados.
- Veja [plataformas](app-insights-platforms.md) suportado pelo Application Insights.
