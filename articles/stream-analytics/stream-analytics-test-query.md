---
title: teste de consulta do aaaAzure Stream Analytics | Microsoft Docs
description: Como tootest as suas consultas nas tarefas do Stream Analytics.
keywords: testar a consulta, resolver problemas de consulta
documentation center: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a>Testar a consultas do Azure Stream Analytics Olá portal do Azure

Com o Azure Stream Analytics, pode testar consultas Olá portal do Azure sem precisar de toostart ou parar uma tarefa.

## <a name="test-hello-input"></a>Entrada de Olá de teste

1. tootest com dados de entrada de exemplo, faça duplo clique de qualquer uma das entradas e, em seguida, selecione **carregar dados de exemplo do ficheiro**.

    ![consulta de teste do editor de consulta do Stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. Após a conclusão do carregamento de Olá, clique em **teste** tootest esta consulta contra Olá exemplo dados que forneceu.

    ![dados de exemplo de teste do editor de consulta do Stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

saída Olá da sua consulta é apresentada no browser Olá, com transferências resultados ligação se pretender que resultado do teste toosave Olá para utilização posterior. Pode facilmente e iteratively modifique a consulta e testá-lo repetidamente toosee como saída Olá é alterado.

![Saída de exemplo do editor de consulta do Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

Com várias saídas utilizadas numa consulta, pode ver resultados de Olá para ambas as saídas separadamente e facilmente alternar entre elas.

Depois de se satisfeito com os resultados de Olá apresentados no browser Olá, pode guardar a consulta, iniciar a tarefa e permitem processar eventos sem erros.

## <a name="get-help"></a>Obter ajuda

Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passos seguintes

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
