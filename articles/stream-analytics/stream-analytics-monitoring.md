---
title: "Noções sobre tarefa de Stream Analytics monitorização | Microsoft Docs"
description: "Noções sobre monitorização de tarefa do Stream Analytics"
keywords: monitor de consulta
services: stream-analytics
documentationcenter: 
author: jseb225
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 7474f45494c6190ffcac354e75458b18f5777fb9
ms.sourcegitcommit: be0d1aaed5c0bbd9224e2011165c5515bfa8306c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a>Compreender como monitorizar consultas e de monitorização de tarefa do Stream Analytics

## <a name="introduction-the-monitor-page"></a>Introdução: A página objeto da monitorização
O Azure portal ambos superfície métricas chave de desempenho que podem ser utilizadas para monitorizar e resolver problemas de desempenho da sua consulta e a tarefa. Para ver estas métricas, navegue para a tarefa de Stream Analytics está interessado em ver as métricas para e ver o **monitorização** secção na página de descrição geral.  

![Monitorização de ligação](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

A janela irá aparecer da seguinte forma:

![Tarefa Dashboard de monitorização](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Métricas disponíveis para o Stream Analytics
| Métrica                 | Definição                               |
| ---------------------- | ---------------------------------------- |
| % de utilização SU       | A utilização da ou as unidades de transmissão em fluxo atribuído a um trabalho a partir do separador escala da tarefa. Deve neste indicador atingir 80% ou acima, há probabilidade elevada que o processamento de eventos pode sofrer um atraso ou parado efetuar progresso. |
| Eventos de Entrada           | Quantidade de dados recebidos pela tarefa de Stream Analytics, número de eventos. Isto pode ser utilizado para validar que eventos são enviados para a origem de entrada. |
| Eventos de Saída          | Quantidade de dados enviados pela tarefa de Stream Analytics para o destino de saída, no número de eventos. |
| Eventos de fora de ordem    | Número de eventos recebidos fora de ordem que foram ignorados ou fornecido um ajustada timestamp, com base na política de ordenação de eventos. Isto pode ser afetado pela configuração da definição de período de tolerância fora de ordem. |
| Erros de Conversão de Dados | Número de erros de conversão de dados tarifas por uma tarefa de Stream Analytics. |
| Erros de Tempo de Execução         | Número total de erros relacionados com o processamento de consulta (excluindo a erros encontrados ao ingestão relacionadas eventos ou resultados outputing) |
| Eventos de Entrada atrasados      | Número de eventos que chegam tarde de origem que optar por ter sido removido ou os respetivos timestamp foi ajustado, com base na configuração da política de ordenação de eventos da definição de período de tolerância de chegada tarde. |
| Pedidos de Função      | Número de chamadas para a função do Azure Machine Learning (caso exista). |
| Falha no pedido de funções | Número de chamadas de função, falhadas Azure Machine Learning (caso exista). |
| Eventos de Função        | Número de eventos enviados para a função do Azure Machine Learning (caso exista). |
| Bytes de Evento de Entrada      | Quantidade de dados recebidos pela tarefa de Stream Analytics, em bytes. Isto pode ser utilizado para validar que eventos são enviados para a origem de entrada. |


## <a name="customizing-monitoring-in-the-azure-portal"></a>Personalizar monitorização no portal do Azure
Pode ajustar o tipo de gráfico, métricas apresentadas e intervalo nas definições de editar gráfico de tempo. Para obter mais informações, consulte [como personalizar monitorização](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Gráfico do Monitor de hora de consulta](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="latest-output"></a>Saída mais recente
Outro ponto de dados interessantes para monitorizar a tarefa é a hora do último saída, apresentada na página de descrição geral.
Este tempo é o tempo de aplicação (ou seja, a hora de utilizar o carimbo dos dados do evento) do resultado da tarefa mais recente.

## <a name="get-help"></a>Obter ajuda
Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passos seguintes
* [Introdução ao Azure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

