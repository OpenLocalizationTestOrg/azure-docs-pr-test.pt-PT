---
title: "aaaUnderstanding monitorização de tarefa do Stream Analytics | Microsoft Docs"
description: "Noções sobre monitorização de tarefa do Stream Analytics"
keywords: monitor de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>Compreender a monitorização de tarefa do Stream Analytics e como toomonitor consultas

## <a name="introduction-hello-monitor-page"></a>Introdução: página de monitor de Olá
Olá ambos superfície métricas chave de desempenho que podem ser utilizado toomonitor e resolver problemas de desempenho da sua consulta e a tarefa de portal do Azure. toosee estas métricas, navegue até a tarefa de Stream Analytics toohello estiver interessado em ver as métricas para e Olá vista **monitorização** secção na página de descrição geral de Olá.  

![Monitorização de ligação](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

será apresentada a janela de Olá conforme mostrado:

![Tarefa Dashboard de monitorização](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Métricas disponíveis para o Stream Analytics
| Métrica                 | Definição                               |
| ---------------------- | ---------------------------------------- |
| % De utilização de SU       | utilização de Olá de Olá as unidades de transmissão em fluxo atribuído tooa tarefa a partir do separador de escala Olá da tarefa de Olá. Deve neste indicador atingir 80% ou acima, há probabilidade elevada que o processamento de eventos pode sofrer um atraso ou parado efetuar progresso. |
| Eventos de entrada           | Quantidade de dados recebidos pela tarefa de Stream Analytics Olá, número de eventos. Isto pode ser utilizado toovalidate que eventos são enviados toohello origem de entrada. |
| Eventos de saída          | Quantidade de dados enviados por Olá Stream Analytics tarefa toohello saída destino, no número de eventos. |
| Eventos de fora de ordem    | Número de eventos recebidos fora de ordem que foram ignorados ou fornecido um ajustada timestamp, com base no Olá política de ordenação de evento. Isto pode ser afetado pela configuração de Olá da definição de período de tolerância fora de ordem de Olá. |
| Erros de conversão de dados | Número de erros de conversão de dados tarifas por uma tarefa de Stream Analytics. |
| Erros de Runtime         | número total de Olá de erros que ocorrem durante a execução de uma tarefa de Stream Analytics. |
| Eventos de entrada de enlace tardio      | Número de eventos que chegam tarde de origem Olá que optar por ter sido removido ou os respetivos timestamp foi ajustado, com base na configuração de política de ordenação de evento Olá da definição de período de tolerância de chegada tarde Olá. |
| Pedidos de função      | Número de chamadas toohello função do Azure Machine Learning (caso exista). |
| Pedidos de função falhada | Número de chamadas de função, falhadas Azure Machine Learning (caso exista). |
| Eventos de função        | Número dos eventos enviados toohello a função do Azure Machine Learning (caso exista). |
| Bytes do evento de entrada      | Quantidade de dados recebidos pela tarefa de Stream Analytics Olá, em bytes. Isto pode ser utilizado toovalidate que eventos são enviados toohello origem de entrada. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>Personalizar monitorização no Olá portal do Azure
Pode ajustar o tipo de Olá de gráfico, métricas apresentadas e intervalo nas definições de editar gráfico Olá de tempo. Para obter mais informações, consulte [como tooCustomize monitorização](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Gráfico do Monitor de hora de consulta](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>Obter ajuda
Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

