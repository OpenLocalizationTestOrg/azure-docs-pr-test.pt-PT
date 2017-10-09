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
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a><span data-ttu-id="967d2-104">Testar a consultas do Azure Stream Analytics Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="967d2-104">Test Azure Stream Analytics queries in hello Azure portal</span></span>

<span data-ttu-id="967d2-105">Com o Azure Stream Analytics, pode testar consultas Olá portal do Azure sem precisar de toostart ou parar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="967d2-105">With Azure Stream Analytics, you can test queries in hello Azure portal without needing toostart or stop a job.</span></span>

## <a name="test-hello-input"></a><span data-ttu-id="967d2-106">Entrada de Olá de teste</span><span class="sxs-lookup"><span data-stu-id="967d2-106">Test hello input</span></span>

1. <span data-ttu-id="967d2-107">tootest com dados de entrada de exemplo, faça duplo clique de qualquer uma das entradas e, em seguida, selecione **carregar dados de exemplo do ficheiro**.</span><span class="sxs-lookup"><span data-stu-id="967d2-107">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![consulta de teste do editor de consulta do Stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="967d2-109">Após a conclusão do carregamento de Olá, clique em **teste** tootest esta consulta contra Olá exemplo dados que forneceu.</span><span class="sxs-lookup"><span data-stu-id="967d2-109">After hello upload is complete, click **Test** tootest this query against hello sample data you have provided.</span></span>

    ![dados de exemplo de teste do editor de consulta do Stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="967d2-111">saída Olá da sua consulta é apresentada no browser Olá, com transferências resultados ligação se pretender que resultado do teste toosave Olá para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="967d2-111">hello output of your query is displayed in hello browser, with Download results link should you want toosave hello test output for later use.</span></span> <span data-ttu-id="967d2-112">Pode facilmente e iteratively modifique a consulta e testá-lo repetidamente toosee como saída Olá é alterado.</span><span class="sxs-lookup"><span data-stu-id="967d2-112">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Saída de exemplo do editor de consulta do Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="967d2-114">Com várias saídas utilizadas numa consulta, pode ver resultados de Olá para ambas as saídas separadamente e facilmente alternar entre elas.</span><span class="sxs-lookup"><span data-stu-id="967d2-114">With multiple outputs used in a query, you can see hello results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="967d2-115">Depois de se satisfeito com os resultados de Olá apresentados no browser Olá, pode guardar a consulta, iniciar a tarefa e permitem processar eventos sem erros.</span><span class="sxs-lookup"><span data-stu-id="967d2-115">After you are satisfied with hello results shown in hello browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="967d2-116">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="967d2-116">Get help</span></span>

<span data-ttu-id="967d2-117">Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="967d2-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="967d2-118">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="967d2-118">Next steps</span></span>

* [<span data-ttu-id="967d2-119">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="967d2-119">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="967d2-120">Começar a utilizar o Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="967d2-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="967d2-121">Tarefas de escala do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="967d2-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="967d2-122">Referência do idioma de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="967d2-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="967d2-123">Referência de API do REST de gestão do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="967d2-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
