---
title: aaaAzure modelo de dados do Application Insights | Microsoft Docs
description: "Descreve propriedades exportado a partir da exportação contínua na JSON e utilizados como filtros."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a>Modelo de dados de exportação do Application Insights
Esta tabela lista as propriedades de Olá de telemetria enviada do Olá [Application Insights](app-insights-overview.md) SDKs toohello portal.
Irá ver estas propriedades na saída de dados de [exportação contínua](app-insights-export-telemetry.md).
Também aparecem em filtros de propriedade no [métrica Explorer](app-insights-metrics-explorer.md) e [pesquisa de diagnóstico](app-insights-diagnostic-search.md).

Toonote pontos:

* `[0]`nestas tabelas indica que um ponto no caminho de olá onde tenha tooinsert um índice; mas não se encontra sempre 0.
* Durações de tempo são em décimas de aos microssegundos, por isso, 10000000 = = 1 segundo.
* As datas e horas são UTC e foram fornecidas no formato ISO de Olá`yyyy-MM-DDThh:mm:ss.sssZ`


## <a name="example"></a>Exemplo
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  }

## <a name="context"></a>Contexto
Todos os tipos de telemetria são acompanhados por uma secção de contexto. Todos estes campos são transmitidos com cada ponto de dados.

| Caminho | Tipo | Notas |
| --- | --- | --- |
| Context.Custom.dimensions [0] |[] do objeto |Conjunto de pares chave-valor de cadeia pelo parâmetro propriedades personalizadas. Comprimento máximo da chave 100, valores de comprimento de máximo 1024. Mais de 100 valores exclusivos, a propriedade de Olá pode ser pesquisada mas não pode ser utilizada relativamente à segmentação. Chaves de 200 máx. por ikey. |
| Context.Custom.Metrics [0] |[] do objeto |Pares chave-valor definido pelo parâmetro medidas personalizadas e por TrackMetrics. Comprimento de máximo chave 100, valores podem ser um valor numéricos. |
| context.data.eventTime |Cadeia |UTC |
| context.data.isSynthetic |Valor booleano |Pedido aparece toocome de um teste bot ou web. |
| context.data.samplingRate |Número |Percentagem de telemetria gerada pelo Olá SDK que é enviado tooportal. Intervalo entre 0,0 e 100,0. |
| Context.Device |objeto |Dispositivo cliente |
| Context.Device.browser |Cadeia |Chrome,... |
| context.device.browserVersion |Cadeia |Chrome 48.0,... |
| context.device.deviceModel |Cadeia | |
| context.device.deviceName |Cadeia | |
| Context.Device.ID |Cadeia | |
| Context.Device.locale |Cadeia |en GB, Alemanha-Alemanha,... |
| Context.Device.Network |Cadeia | |
| context.device.oemName |Cadeia | |
| context.device.osVersion |Cadeia |Sistema operativo do anfitrião |
| context.device.roleInstance |Cadeia |ID de anfitrião do servidor |
| context.device.roleName |Cadeia | |
| Context.Device.Type |Cadeia |PC, Browser,... |
| Context.location |objeto |Obtida a partir do clientip. |
| Context.location.City |Cadeia |Derivado clientip, se conhecida |
| Context.location.ClientIP |Cadeia |Última octagon é too0 anónimos. |
| Context.location.continent |Cadeia | |
| Context.location.Country |Cadeia | |
| Context.location.Province |Cadeia |Distrito |
| Context.Operation.ID |Cadeia |Itens que têm o mesmo id de operação são apresentadas como itens relacionados no portal de Olá de Olá. Normalmente, id do pedido Olá. |
| Context.Operation.Name |Cadeia |nome de URL ou a pedido |
| context.operation.parentId |Cadeia |Permite que os itens relacionados aninhados. |
| Context.Session.ID |Cadeia |ID de um grupo de operações a partir de Olá mesma origem. Um período de 30 minutos sem uma extremidade de Olá sinais de operação de uma sessão. |
| context.session.isFirst |Valor booleano | |
| context.user.accountAcquisitionDate |Cadeia | |
| context.user.anonAcquisitionDate |Cadeia | |
| context.user.anonId |Cadeia | |
| context.user.authAcquisitionDate |Cadeia |[Utilizador autenticado](app-insights-api-custom-events-metrics.md#authenticated-users) |
| context.user.isAuthenticated |Valor booleano | |
| internal.data.documentVersion |Cadeia | |
| INTERNAL.data.ID |Cadeia | |

## <a name="events"></a>Eventos
Eventos personalizados gerados pelo [trackevent ()](app-insights-api-custom-events-metrics.md#trackevent).

| Caminho | Tipo | Notas |
| --- | --- | --- |
| Contagem de eventos [0] |número inteiro |100 / ([amostragem](app-insights-sampling.md) taxa). Por exemplo, 4 =&gt; 25%. |
| nome do evento [0] |Cadeia |Nome do evento.  Comprimento de máximo 250. |
| url de eventos [0] |Cadeia | |
| o evento [0] urlData.base |Cadeia | |
| o evento [0] urlData.host |Cadeia | |

## <a name="exceptions"></a>Exceções
Relatórios [exceções](app-insights-asp-net-exceptions.md) em hello do servidor e no browser Olá.

| Caminho | Tipo | Notas |
| --- | --- | --- |
| assemblagem basicException [0] |Cadeia | |
| Contagem de basicException [0] |número inteiro |100 / ([amostragem](app-insights-sampling.md) taxa). Por exemplo, 4 =&gt; 25%. |
| exceptionGroup basicException [0] |Cadeia | |
| exceptionType basicException [0] |Cadeia | |
| failedUserCodeMethod basicException [0] |Cadeia | |
| failedUserCodeAssembly basicException [0] |Cadeia | |
| handledAt basicException [0] |Cadeia | |
| hasFullStack basicException [0] |Valor booleano | |
| id de basicException [0] |Cadeia | |
| método de basicException [0] |Cadeia | |
| mensagem de basicException [0] |Cadeia |Mensagem de exceção. Comprimento de máximo 10k. |
| outerExceptionMessage basicException [0] |Cadeia | |
| outerExceptionThrownAtAssembly basicException [0] |Cadeia | |
| outerExceptionThrownAtMethod basicException [0] |Cadeia | |
| outerExceptionType basicException [0] |Cadeia | |
| outerId basicException [0] |Cadeia | |
| assemblagem de parsedStack [0] basicException [0] |Cadeia | |
| o nome de ficheiro do basicException [0] parsedStack [0] |Cadeia | |
| nível de parsedStack [0] basicException [0] |número inteiro | |
| linha de parsedStack [0] basicException [0] |número inteiro | |
| método de parsedStack [0] basicException [0] |Cadeia | |
| pilha basicException [0] |Cadeia |Comprimento de máximo 10 mil |
| typeName basicException [0] |Cadeia | |

## <a name="trace-messages"></a>Mensagens de rastreio
Enviada pelo [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace)e por Olá [registo adaptadores](app-insights-asp-net-trace-logs.md).

| Caminho | Tipo | Notas |
| --- | --- | --- |
| a mensagem [0] loggerName |Cadeia | |
| parâmetros de mensagem [0] |Cadeia | |
| mensagem [0] em bruto |Cadeia |mensagem do registo Olá, comprimento máximo de 10 mil. |
| nível de gravidade de mensagem [0] |Cadeia | |

## <a name="remote-dependency"></a>Dependência remota
Enviada pelo TrackDependency. Utilizado tooreport desempenho e a utilização de [chama toodependencies](app-insights-asp-net-dependencies.md) no servidor de Olá e chamadas AJAX no browser Olá.

| Caminho | Tipo | Notas |
| --- | --- | --- |
| async remoteDependency [0] |Valor booleano | |
| baseName remoteDependency [0] |Cadeia | |
| commandName remoteDependency [0] |Cadeia |Por exemplo "home/index" |
| Contagem de remoteDependency [0] |número inteiro |100 / ([amostragem](app-insights-sampling.md) taxa). Por exemplo, 4 =&gt; 25%. |
| dependencyTypeName remoteDependency [0] |Cadeia |HTTP, SQL,... |
| durationMetric.value remoteDependency [0] |Número |Tempo da chamada toocompletion da resposta pela dependência |
| id de remoteDependency [0] |Cadeia | |
| nome de remoteDependency [0] |Cadeia |URL. Comprimento de máximo 250. |
| resultCode remoteDependency [0] |Cadeia |de dependência HTTP |
| êxito remoteDependency [0] |Valor booleano | |
| tipo de remoteDependency [0] |Cadeia |Http, Sql,... |
| url de remoteDependency [0] |Cadeia |Comprimento de máximo 2000 |
| urlData.base remoteDependency [0] |Cadeia |Comprimento de máximo 2000 |
| urlData.hashTag remoteDependency [0] |Cadeia | |
| urlData.host remoteDependency [0] |Cadeia |Comprimento de máximo 200 |

## <a name="requests"></a>Pedidos
Enviada pelo [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest). os módulos de padrão de Olá utilizam este tempo de resposta de servidor tooreports, medido no servidor de Olá.

| Caminho | Tipo | Notas |
| --- | --- | --- |
| Contagem de pedido [0] |número inteiro |100 / ([amostragem](app-insights-sampling.md) taxa). Por exemplo: 4 =&gt; 25%. |
| durationMetric.value pedido [0] |Número |Tempo do pedido de tooresponse atrasada. 1e7 = = 1s |
| id do pedido [0] |Cadeia |Id de operação |
| nome do pedido [0] |Cadeia |GET/POST + url base.  Comprimento de máximo 250 |
| responseCode pedido [0] |número inteiro |HTTP resposta enviada tooclient |
| sucesso de pedido [0] |Valor booleano |Predefinição = = (responseCode &lt; 400) |
| url do pedido [0] |Cadeia |Não, incluindo anfitriões |
| urlData.base pedido [0] |Cadeia | |
| urlData.hashTag pedido [0] |Cadeia | |
| urlData.host pedido [0] |Cadeia | |

## <a name="page-view-performance"></a>Desempenho de vista de página
Enviado pelo browser de Olá. Medidas Olá tempo tooprocess uma página, do utilizador iniciar Olá pedido toodisplay concluída (excluindo as chamadas AJAX assíncrona).

Mostram valores de contexto SO de cliente e a versão do browser.

| Caminho | Tipo | Notas |
| --- | --- | --- |
| clientProcess.value clientPerformance [0] |número inteiro |Hora de fim da página do Olá HTML toodisplaying hello a receber. |
| nome de clientPerformance [0] |Cadeia | |
| networkConnection.value clientPerformance [0] |número inteiro |Tempo decorrido tooestablish uma ligação de rede. |
| receiveRequest.value clientPerformance [0] |número inteiro |Hora de fim de envio em reply Olá de tooreceiving Olá pedido HTML. |
| sendRequest.value clientPerformance [0] |número inteiro |Tempo decorrido toosend pedido de Olá HTTP. |
| total.value clientPerformance [0] |número inteiro |Tempo de iniciar a página de Olá toosend Olá pedido toodisplaying. |
| url de clientPerformance [0] |Cadeia |URL deste pedido |
| urlData.base clientPerformance [0] |Cadeia | |
| urlData.hashTag clientPerformance [0] |Cadeia | |
| urlData.host clientPerformance [0] |Cadeia | |
| urlData.protocol clientPerformance [0] |Cadeia | |

## <a name="page-views"></a>Vistas de página
Enviada pelo trackPageView() ou [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)

| Caminho | Tipo | Notas |
| --- | --- | --- |
| Contagem de visualizações [0] |número inteiro |100 / ([amostragem](app-insights-sampling.md) taxa). Por exemplo, 4 =&gt; 25%. |
| Ver durationMetric.value [0] |número inteiro |Valor, opcionalmente, definido na trackPageView() ou startTrackPage() - stopTrackPage(). Não Olá mesmo como clientPerformance valores. |
| nome da vista [0] |Cadeia |Título de página.  Comprimento de máximo 250 |
| url da vista [0] |Cadeia | |
| Ver urlData.base [0] |Cadeia | |
| Ver urlData.hashTag [0] |Cadeia | |
| Ver urlData.host [0] |Cadeia | |

## <a name="availability"></a>Disponibilidade
Relatórios [testes web de disponibilidade](app-insights-monitor-web-app-availability.md).

| Caminho | Tipo | Notas |
| --- | --- | --- |
| availabilityMetric.name disponibilidade [0] |Cadeia |disponibilidade |
| availabilityMetric.value disponibilidade [0] |Número |1.0 ou 0,0 |
| Contagem de disponibilidade [0] |número inteiro |100 / ([amostragem](app-insights-sampling.md) taxa). Por exemplo, 4 =&gt; 25%. |
| dataSizeMetric.name disponibilidade [0] |Cadeia | |
| dataSizeMetric.value disponibilidade [0] |número inteiro | |
| durationMetric.name disponibilidade [0] |Cadeia | |
| durationMetric.value disponibilidade [0] |Número |Duração de teste. 1e7 = = 1s |
| mensagem de disponibilidade [0] |Cadeia |Falha de diagnóstico |
| resultado de disponibilidade [0] |Cadeia |Passagem/falhar |
| runLocation disponibilidade [0] |Cadeia |Origem de Georreplicação de pedidos de http |
| testName disponibilidade [0] |Cadeia | |
| testRunId disponibilidade [0] |Cadeia | |
| testTimestamp disponibilidade [0] |Cadeia | |

## <a name="metrics"></a>Métricas
Gerado por trackmetric ().

valor de métrica de Olá for encontrado na context.custom.metrics[0]

Por exemplo:

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a>Sobre os valores de métricos
Métricos valores, tanto em relatórios de métricos noutro local, como são reportados com uma estrutura de objeto padrão. Por exemplo:

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

Atualmente - Embora isto pode ser alterado na Olá futura - todos os valores comunicados pelas módulos SDK padrão Olá, `count==1` e apenas Olá `name` e `value` campos são úteis. Olá apenas caso em que seriam diferentes seria se escrever as seus próprios chamadas TrackMetric na qual configurou Olá outros parâmetros.

Olá objetivo Olá outros campos é tooallow métricas toobe agregado Olá SDK, o portal de toohello tooreduce tráfego. Por exemplo, foi médio as leituras de sucessivas várias antes de enviar cada relatório de métrico. Em seguida, teria de calcular Olá Mín, Máx, desvio-padrão e valor de agregação (sum ou média) e definir o número de toohello de contagem das leituras dos representado pelo relatório de Olá.

Nas tabelas de Olá acima, podemos ter omitido contagem de campos raramente utilizado Olá, min, max, stdDev e sampledValue.

Em vez de pré-agregar métricas, pode utilizar [amostragem](app-insights-sampling.md) se precisar de volume de Olá tooreduce de telemetria.

### <a name="durations"></a>Durações
Exceto indicação em contrário, em durações são representadas no décimas de aos microssegundos, para que 10000000.0 significa 1 segundo.

## <a name="see-also"></a>Consultar também
* [Application Insights](app-insights-overview.md)
* [Exportação contínua](app-insights-export-telemetry.md)
* [Exemplos de código](app-insights-export-telemetry.md#code-samples)
