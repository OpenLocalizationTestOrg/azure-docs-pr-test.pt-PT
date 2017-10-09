---
title: "aaaJob dimensionamento com as funções do Azure Stream Analytics & AzureML | Microsoft Docs"
description: "Saiba como tooproperly dimensionar as tarefas do Stream Analytics (criação de partições, a quantidade SU e mais) ao utilizar as funções do Azure Machine Learning."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>Dimensionar a sua tarefa do Stream Analytics com as funções do Azure Machine Learning
Muitas vezes, é fácil bastante tooset se uma tarefa de Stream Analytics e executar alguns dados de exemplo através do mesmo. O fazer quando é necessário toorun Olá mesmo da tarefa com o volume de dados superior? Requer toounderstand como tooconfigure Olá Stream Analytics da tarefa para que sejam dimensionadas-nos. Neste documento, iremos focar-nos aspetos de especial Olá de dimensionamento do Stream Analytics tarefas com as funções de Machine Learning. Para obter informações sobre como tarefas do Stream Analytics tooscale em geral, consulte o artigo de Olá [dimensionamento tarefas](stream-analytics-scale-jobs.md).

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>O que é uma função do Azure Machine Learning no Stream Analytics?
Uma função de Machine Learning no Stream Analytics pode ser utilizada como uma chamada de função regulares em Olá idioma de consulta do Stream Analytics. No entanto, por trás de cenas Olá, chamadas de função Olá são, na verdade, os pedidos de serviço Web do Azure Machine Learning. Suporte "criação de batches" várias linhas, que é chamado batch mini de serviços web do Machine Learning, no Olá mesmo web chamada à API do serviço, tooimprove débito global. Consulte Olá seguintes artigos para obter mais detalhes; [Funções do azure Machine Learning no Stream Analytics](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/) e [serviços Web do Azure Machine Learning](../machine-learning/machine-learning-consume-web-services.md).

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>Configurar uma tarefa de Stream Analytics com as funções de Machine Learning
Quando configurar uma função de Machine Learning para a tarefa de Stream Analytics, existem dois parâmetros tooconsider, tamanho do lote Olá de chamadas de função do Machine Learning Olá e Olá unidades (SUs) aprovisionadas para a tarefa de Stream Analytics Olá de transmissão em fluxo. toodetermine Olá os valores adequados para estas, primeiro uma decisão têm de ser efetuada entre a latência e débito, ou seja, a latência da tarefa de Stream Analytics Olá e débito de cada SU. Sempre podem ser adicionados tooa tarefa tooincrease débito uma consulta do Stream Analytics bem particionada, SUs embora SUs adicionais aumenta o custo de Olá de tarefa Olá em execução.

Por conseguinte, é importante toodetermine Olá *tolerância* de latência em execução uma tarefa de Stream Analytics. Latência adicional a execução de pedidos de serviço do Azure Machine Learning naturalmente irá aumentar com o tamanho do lote, que será composta latência Olá da tarefa de Stream Analytics Olá. No Olá por outro lado, aumentar o tamanho do lote permite tooprocess de tarefa do Stream Analytics Olá * mais eventos com Olá *mesmo número* do Machine Learning pedidos de serviço da web. Muitas vezes, o aumento de Olá de latência de serviço web de Machine Learning é toohello subplano linear aumento do tamanho do lote, pelo que é importante tooconsider Olá mais económico tamanho do lote para um serviço web do Machine Learning em qualquer situação de determinado. tamanho de lote Olá predefinido para o serviço web de Olá pedidos é 1000 e pode ser modificado utilizando Olá [API de REST do Stream Analytics](https://msdn.microsoft.com/library/mt653706.aspx "API de REST do Stream Analytics") ou Olá [PowerShell cliente para o Stream Analytics](stream-analytics-monitor-and-manage-jobs-use-powershell.md "PowerShell de cliente para o Stream Analytics").

Depois de um tamanho de lote foi considerado, quantidade de Olá de transmissão em fluxo unidades (SUs) podem ser determinadas, com base no Olá número de eventos que função Olá tem tooprocess por segundo. Para obter mais informações sobre unidades de transmissão em fluxo, consulte [Stream Analytics Dimensionar tarefas](stream-analytics-scale-jobs.md).

Em geral, existem 20 ligações simultâneas serviço de web do Machine Learning toohello para cada 6 SUs, exceto que as tarefas de SU 1 e 3 tarefas SU obterá 20 ligações simultâneas também.  Por exemplo, se a taxa de dados de entrada Olá é 200 000 eventos por segundo e o tamanho do lote Olá for deixado toohello predefinido de 1000 Olá resultante web service latência com o batch mini do 1000 eventos é de 200 MS. Isto significa que cada ligação possa fazer 5 pedidos serviço de web do Machine Learning toohello num segundo. Com 20 ligações, tarefa de Stream Analytics Olá pode processar e, por conseguinte, 100 000 eventos de 20000 eventos 200 MS num segundo. Por isso, tooprocess inferior 200.000 eventos por segundo, tarefa de Stream Analytics Olá necessita de 40 ligações em simultâneo, vem saída too12 SUs. Diagrama de Olá abaixo mostra os pedidos de Olá de Olá Stream Analytics tarefa toohello Machine Learning web ponto final de serviço – cada 6 SUs tem 20 serviço de web do Learning tooMachine ligações simultâneas no máximo.

![Dimensionar o Stream Analytics com o exemplo de trabalho do Machine Learning funções 2](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "escala Stream Analytics com o exemplo de trabalho do Machine Learning funções 2")

Em geral, ***B*** para o tamanho do lote, ***L*** de latência de serviço de web de Olá no tamanho do lote B em milissegundos, Olá débito de uma tarefa de Stream Analytics com ***N*** SUs é:

![Dimensionar o do Stream Analytics com Machine Learning funções fórmula](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "do Stream Analytics com Machine Learning funções fórmula de dimensionamento")

Uma consideração adicional pode ser Olá 'Máx. de chamadas em simultâneo' no Olá lado de serviço web Machine Learning, é recomendado tooset este valor máximo de toohello (200 atualmente).

Para mais informações sobre esta definição reveja Olá [artigo de dimensionamento para serviços Web Machine Learning](../machine-learning/machine-learning-scaling-webservice.md).

## <a name="example--sentiment-analysis"></a>Exemplo-Sentiment análise
Olá exemplo seguinte inclui uma tarefa de Stream Analytics com a análise de dados de sentimento Olá função do Machine Learning, conforme descrito em Olá [tutorial de integração de aprendizagem do Stream Analytics](stream-analytics-machine-learning-integration-tutorial.md).

Olá consulta é uma consulta simples totalmente particionada, seguida de Olá **sentimento** funcionem, como mostrado abaixo:

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

Considere Olá seguir o cenário; com um débito de 10 000 tweets por segundo deve ser criada uma tarefa de Stream Analytics análise de dados de sentimento tooperform de tweets Olá (eventos). Utilizar 1 SU, esta tarefa de Stream Analytics dever toohandle capaz de tráfego de Olá? Utilizar o tamanho de lote Olá predefinido da tarefa de Olá 1000 deve ser capaz de tookeep cópias de segurança com entrada de Olá. Olá mais Adicionar função de Machine Learning deve gerar não mais do que um segundo de latência, que é a latência de predefinição geral Olá da análise de dados de sentimento Olá serviço web Machine Learning (com um tamanho de lote de predefinição de 1000). tarefa de Stream Analytics a Olá **geral** ou latência ponto-a-ponto, normalmente, seria alguns segundos. Veja mais detalhadas para esta tarefa de Stream Analytics *especialmente* Olá chamadas de função do Machine Learning. Ter o tamanho do lote Olá como 1000, um débito de 10 000 eventos irá demorar cerca de 10 pedidos tooweb serviço. Mesmo com 1 SU, existem suficiente tooaccommodate de ligações simultâneas este tráfego de entrada.

Mas e se a taxa de eventos de entrada Olá aumenta ao 100 x e agora a tarefa de Stream Analytics Olá tem tooprocess 1.000.000 tweets por segundo? Existem duas opções:

1. Aumentar o tamanho do lote hello, ou
2. Partição Olá o fluxo de entrada tooprocess Olá eventos em paralelo

Com a opção de primeiro Olá, Olá tarefa **latência** irá aumentar.

Com a segunda opção Olá, SUs mais seriam necessário toobe aprovisionado e, por conseguinte, gerar mais pedidos simultâneos de Machine Learning web service. Isto significa que a tarefa de Olá **custo** irá aumentar.

Partem do princípio de latência de Olá da análise de dados de sentimento Olá serviço web Machine Learning é 200 MS para lotes de 1000 eventos ou abaixo, 250ms para eventos de 5000 lotes, 300ms para 10 000 eventos lotes ou 500ms para lotes 25,000-o evento.

1. Utilizando a opção de primeiro Olá, (**não** aprovisionamento mais SUs), o tamanho do lote Olá pode ser aumentado demasiado**25,000**. Isto por sua vez permitiria que Olá tarefa tooprocess 1.000.000 eventos com 20 ligações simultâneas toohello serviço web Machine Learning (com uma latência de 500ms por chamada). Olá, por isso, a latência adicional da tarefa de Stream Analytics Olá devido a pedidos de função de sentimento toohello contra Olá Machine Learning pedidos de serviço web teriam de ser aumentados de **200 MS** demasiado**500ms**. No entanto, tenha em atenção que o tamanho do lote **não é possível** ser aumentado infinitamente como hello serviços web do Machine Learning, precisa de tamanho do payload Olá de um pedido web mais pequeno o tempo limite de pedidos de serviço após 100 segundos da operação ou ser 4 MB.
2. Utilizar a segunda opção de Olá, tamanho do lote Olá for deixado em 1000, com uma latência de serviço web de 200 MS, todos os serviço de web de toohello 20 ligações simultâneas seria capaz de tooprocess 1000 * 20 * 5 eventos = 100 000 por segundo. Por isso, tooprocess 1.000.000 eventos por segundo, tarefa de Olá teria 60 SUs. Em comparação com toohello primeira opção, Stream Analytics tarefa iria tornar mais pedidos de batch de serviço, da web por sua vez gerar um custo de aumento.

Segue-se uma tabela para o débito de Olá da tarefa de Stream Analytics Olá para diferentes SUs e tamanhos de lote (num número de eventos por segundo).

| tamanho de lote (latência de ML) | 500 (200 MS) | 1000 (200 MS) | 5000 (250ms) | 10 000 (300ms) | 25,000 (500ms) |
| --- | --- | --- | --- | --- | --- |
| **1 SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **3 SUs** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **6 SUs** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **12 SUs** |5,000 |10,000 |40,000 |60,000 |100,000 |
| **18 SUs** |7,500 |15,000 |60,000 |90,000 |150,000 |
| **24 SUs** |10,000 |20,000 |80,000 |120,000 |200,000 |
| **…** |… |… |… |… |… |
| **60 SUs** |25,000 |50,000 |200,000 |300,000 |500,000 |

Por agora, já deverá ter uma boa compreensão sobre como funcionam as funções de Machine Learning no Stream Analytics. Provavelmente também compreende que tarefas do Stream Analytics "solicitar" dados a partir de origens de dados e cada "pull" devolve um lote de eventos para Olá tooprocess de tarefa do Stream Analytics. Como é que este modelo de extração afetar os pedidos de serviço web do Olá Machine Learning?

Normalmente, o tamanho do lote Olá que definimos para funções de Machine Learning exatamente será divisible por número de Olá de eventos devolvidos por cada tarefa de Stream Analytics "solicitação". Quando isto ocorre Olá serviço web Machine Learning será chamado com lotes "parciais". Isto é feito toonot implicar a latência de trabalhos adicionais sobrecarga em eventos de agregação de toopull de extração.

## <a name="new-function-related-monitoring-metrics"></a>Nova função monitorização das métricas relacionadas com
Na área de Monitor de uma tarefa de Stream Analytics Olá, foram adicionadas três métricas adicionais relacionados com a função. Estes são pedidos de função, eventos de função e função de pedidos FALHADOS, conforme apresentado no gráfico Olá abaixo.

![Dimensionar o do Stream Analytics com a métrica de funções do Machine Learning](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "dimensionar o do Stream Analytics com a métrica de funções do Machine Learning")

Olá são definidos do seguinte modo:

**PEDIDOS de função**: Olá número de pedidos de função.

**EVENTOS de função**: eventos de número de Olá no Olá funcionarem pedidos.

**PEDIDOS FALHADOS de função**: Olá número de pedidos de função falhada.

## <a name="key-takeaways"></a>Chaves Takeaways
toosummarize Olá principal pontos, tooscale ordem uma tarefa de Stream Analytics com as funções de Machine Learning, hello seguintes itens têm de ser considerados:

1. taxa de eventos de entrada de Olá
2. Olá tolerated latência para Olá executar tarefa de Stream Analytics (e, por conseguinte, o tamanho do lote Olá do serviço de web do Machine Learning Olá pedidos)
3. Olá aprovisionado Stream Analytics SUs e número de Olá de pedidos de serviço web Machine Learning (Olá relacionadas com a função custos adicionais)

Uma consulta do Stream Analytics totalmente particionada foi utilizada como exemplo. Se necessitar de uma consulta mais complexa Olá [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) é um ótimo recurso para obter ajuda adicional da equipa de Stream Analytics Olá.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre o Stream Analytics, consulte:

* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
