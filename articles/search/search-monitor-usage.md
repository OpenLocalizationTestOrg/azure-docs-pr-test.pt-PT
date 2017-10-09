---
title: "aaaMonitor utilização e as estatísticas num serviço da Azure Search | Microsoft Docs"
description: "Controlar o tamanho de consumo e o índice de recursos para a Azure Search, um serviço de pesquisa em nuvem alojado no Microsoft Azure."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Monitorizar um serviço da Azure Search

A pesquisa do Azure oferece vários recursos para o registo de utilização e desempenho dos serviços de pesquisa. Dá-lhe aceder toometrics, os registos, estatísticas de índice e as capacidades de monitorização expandidas no Power BI. Este artigo descreve como tooenable Olá diferentes estratégias de monitorização e como toointerpret Olá dados resultantes.

## <a name="azure-search-metrics"></a>Métricas de pesquisa do Azure
Métricas dão-lhe quase em tempo real visibilidade para o serviço de pesquisa e estão disponíveis para cada serviço, com nenhuma configuração adicional. Permitem-lhe monitorizar o desempenho de Olá do seu serviço de cópia de segurança too30 dias.

A pesquisa do Azure recolhe dados de três métricas diferentes:

* Latência de pesquisa: tempo o serviço de pesquisa de Olá necessário tooprocess procurar consultas, agregadas por minuto.
* Procurar consultas por segundo (QPS): número de pesquisa consultas recebidas por segundo, agregados por minuto.
* Percentagem de consulta de pesquisa otimizada: percentagem de consultas de pesquisa que foram limitado, agregado por minuto.

![Atividade de captura de ecrã de QPS][1]

### <a name="set-up-alerts"></a>configurar alertas
Na página de detalhes de métrica de Olá, pode configurar alertas tootrigger uma notificação por e-mail ou uma ação automática quando uma métrica atravesse um limiar que foram definidos.

Para obter mais informações sobre as métricas, consulte a documentação completa da Olá no Monitor do Azure.  

## <a name="how-tootrack-resource-usage"></a>Como tootrack a utilização de recursos
Controlar o crescimento de Olá de índices e o tamanho do documento pode ajudá-lo proativamente ajustar capacidade antes de atingir o limite superior de Olá que estabeleceu para o seu serviço. Pode fazê-lo no portal de Olá ou através de programação utilizando Olá REST API.

### <a name="using-hello-portal"></a>Através do portal Olá

utilização de recursos de toomonitor, ver Olá contagens e estatísticas para o seu serviço na Olá [portal](https://portal.azure.com).

1. Inicie sessão no toohello [portal](https://portal.azure.com).
2. Abra o dashboard de serviço Olá do serviço da Azure Search. Mosaicos para o serviço de Olá podem ser encontrados na Olá Home page, ou pode procurar o serviço de toohello da procura na Olá barre de índice.

Olá secção utilização inclui um medidor que indica que parte dos recursos disponíveis estão atualmente em utilização. Para obter informações sobre limites de serviço a para o armazenamento, índices e documentos, consulte [os limites de serviço](search-limits-quotas-capacity.md).

  ![Mosaico utilização][2]

> [!NOTE]
> Olá captura de ecrã acima para o serviço gratuito Olá, que tem um máximo de uma réplica, cada partição e pode apenas índices de anfitrião, 3, 10 000 documentos ou 50 MB de dados, o que ocorrer primeiro. Serviços criados num escalão básicas ou Standard têm limites de serviço muito maiores. Para obter mais informações sobre como escolher uma camada, consulte [escolha um escalão ou SKU](search-sku-tier.md).
>
>

### <a name="using-hello-rest-api"></a>Utilizar Olá REST API
Olá API REST da Azure Search e Olá .NET SDK fornecem métricas de tooservice acesso programático.  Se estiver a utilizar [indexadores](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload um índice da SQL Database do Azure ou a base de dados do Azure Cosmos, uma API adicional seja tooget disponíveis Olá composto por números precisa.

* [Obter estatísticas de índice](/rest/api/searchservice/get-index-statistics)
* [Contagem de documentos](/rest/api/searchservice/count-documents)
* [Obter o estado do indexador](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Modo de registo de tooexport e métricas

Pode exportar os registos de operações de Olá para os seus dados não processados Olá e do serviço de métricas de Olá descritos Olá anterior a secção. Os registos de operações informá-lo como o serviço de Olá está a ser utilizado e pode ser utilizado a partir do Power BI quando os dados copiados tooa conta de armazenamento. A pesquisa do Azure fornece um pacote de conteúdos do Power BI monitorização para esta finalidade.


### <a name="enabling-monitoring"></a>Ativar a monitorização
Abra o serviço da Azure Search no Olá [portal do Azure](http://portal.azure.com) em Olá opção de ativar a monitorização.

Escolher Olá dados pretende tooexport: registos, métricas ou ambos. Pode copiá-lo a conta de armazenamento tooa, envie-o hub de eventos de tooan ou tooLog análise de exportá-lo.

![Como tooenable monitorização no portal de Olá][3]

tooenable utilizando o PowerShell ou Olá CLI do Azure, consulte a documentação de Olá [aqui](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).

### <a name="logs-and-metrics-schemas"></a>Esquemas de métricas e registos
Quando os dados Olá são copiado tooa armazenamento conta, hello dados são formatados como JSON e do local em dois contentores:

* operationlogs de registos de insights: para registos de tráfego de pesquisa
* insights-as métricas-pt1m: com base nas métricas

Não há um blob, por hora, por contentor.

Caminho de exemplo:`resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>Esquema de registo
Olá registos blobs contém os registos de tráfego do serviço de pesquisa.
Cada blob tem um objeto de raiz denominado **registos** que contém uma matriz de objetos de registo.
Cada blob tem registos na operação Olá todas as, que demorou local durante Olá mesma hora.

| Nome | Tipo | Exemplo | Notas |
| --- | --- | --- | --- |
| hora |DateTime |"2015-12-07T00:00:43.6872559Z" |TimeStamp da operação de Olá |
| resourceId |Cadeia |"SUBSCRIÇÕES/11111111-1111-1111-1111-111111111111 /<br/>FORNECEDORES/PREDEFINIDOS/RESOURCEGROUPS /<br/> MICROSOFT. PESQUISA/SEARCHSERVICES/SEARCHSERVICE" |O ResourceId |
| operationName |Cadeia |"Query.Search" |nome de Olá da operação de Olá |
| operationVersion |Cadeia |"2015-02-28" |Olá utilizada a versão de api |
| categoria |Cadeia |"OperationLogs" |constante |
| resultType |Cadeia |"Êxito" |Os valores possíveis: êxito ou falha |
| resultSignature |Int |200 |Código de resultado HTTP |
| durationMS |Int |50 |Duração da operação de Olá em milissegundos |
| propriedades |objeto |Consulte Olá a tabela seguinte |Objeto que contém dados específicos da operação |

**Esquema de propriedades**
| Nome | Tipo | Exemplo | Notas |
| --- | --- | --- | --- |
| Descrição |Cadeia |"Obter /indexes('content')/docs" |ponto de final da operação de Olá |
| Consulta |Cadeia |"? pesquisa = azuresearch, uma vez & $count = true & api-version = 2015-02-28" |parâmetros de consulta Olá |
| Documentos |Int |42 |Número de documentos processados |
| indexName |Cadeia |"testindex" |Nome do índice de Olá associado a operação de Olá |

#### <a name="metrics-schema"></a>Esquema de métricas
| Nome | Tipo | Exemplo | Notas |
| --- | --- | --- | --- |
| resourceId |Cadeia |"SUBSCRIÇÕES/11111111-1111-1111-1111-111111111111 /<br/>FORNECEDORES/PREDEFINIDOS/RESOURCEGROUPS /<br/>MICROSOFT. PESQUISA/SEARCHSERVICES/SEARCHSERVICE" |o id de recurso |
| metricName |Cadeia |"Latência" |nome de Olá de métrica de Olá |
| hora |DateTime |"2015-12-07T00:00:43.6872559Z" |timestamp da operação de Olá |
| Média |Int |64 |valor médio do Olá de amostras em bruto de Olá no intervalo de tempo de métrica de Olá |
| mínimo |Int |37 |valor mínimo de Olá de exemplos não processados do Olá no intervalo de tempo de métrica de Olá |
| Máximo |Int |78 |valor máximo de Olá de exemplos não processados do Olá no intervalo de tempo de métrica de Olá |
| total |Int |258 |valor de total de Olá de exemplos não processados do Olá no intervalo de tempo de métrica de Olá |
| Contagem |Int |4 |número de Olá de exemplos não processados utilizado métrica de Olá toogenerate |
| intervalo de agregação |Cadeia |"PT1M" |Grão de tempo de Olá de métrica de Olá no ISO 8601 |

Todas as métricas são reportadas nos intervalos de um minuto. Cada métrica expõe valores mínimos, máximo e médio por minuto.

Para a métrica de SearchQueriesPerSecond Olá, mínimo é o valor mais baixo de Olá para consultas de pesquisa por segundo que foi registado durante esse minuto. Olá mesmo se aplica toohello o valor máximo. Média, é Olá agregado em minuto Olá de todo.
Considere sobre este cenário, durante um minuto: um segundo da carga elevada Olá máximo para SearchQueriesPerSecond, seguido de segundos 58 da carga média e, finalmente, um segundo com apenas uma consulta, que é Olá mínimo.

Para ThrottledSearchQueriesPercentage, mínimo, máximo, média e total, têm Olá mesmo valor: Olá percentagem de consultas de pesquisa que foram limitado, do número total de Olá de consultas de pesquisa durante um minuto.

## <a name="analyzing-your-data-with-power-bi"></a>Analisar os dados com o Power BI

Recomendamos que utilize [Power BI](https://powerbi.microsoft.com) tooexplore e visualizar os dados. Pode ligá-lo facilmente tooyour conta do Storage do Azure e começar rapidamente a analisar os dados.

A pesquisa do Azure fornece um [o pacote de conteúdos do Power BI](https://app.powerbi.com/getdata/services/azure-search) que permite-lhe toomonitor e compreender o tráfego de pesquisa com tabelas e gráficos predefinidos. Contém um conjunto de relatórios do Power BI e ligar dados tooyour automaticamente fornecem visual informações sobre o serviço de pesquisa. Para obter mais informações, consulte Olá [página de ajuda do pacote de conteúdos](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).

![Dashboard do Power BI para a pesquisa do Azure][4]

## <a name="next-steps"></a>Passos seguintes
Reveja [dimensionar as réplicas e de partições](search-limits-quotas-capacity.md) para obter orientações sobre como toobalance Olá atribuição de partições e réplicas para um serviço existente.

Visite [gerir o serviço de pesquisa no Microsoft Azure](search-manage.md) para obter mais informações sobre a administração de serviço, ou [desempenho e a otimização de](search-performance-optimization.md) para obter orientações sobre a otimização.

Saiba mais sobre a criação de relatórios incrível. Consulte [introdução ao Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/) para obter detalhes

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
