---
title: produz aaaHow tooconfigure dados para tarefas do Stream Analytics | Microsoft Docs
description: "Configure as saídas para tarefas do Stream Analytics | Learning segmento de caminho."
keywords: "dados de saída, movimento de dados"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="f7aea-104">Como os dados de tooconfigure produz para tarefas do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f7aea-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="f7aea-105">Tarefas do Stream Analytics do Azure podem ser ligado tooone ou mais saídas de dados, que definem um receptor de dados existente do ligação tooan.</span><span class="sxs-lookup"><span data-stu-id="f7aea-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="f7aea-106">Como a tarefa de Stream Analytics processa e transformações de dados de entrada, um fluxo de eventos de saída de dados é escrito na saída da tarefa tooyour.</span><span class="sxs-lookup"><span data-stu-id="f7aea-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="f7aea-107">Saídas de dados do Stream Analytics podem ser toosource utilizado dashboards de em tempo real ou alertas, fluxos de trabalho de movimento de dados de Acionador ou simplesmente os dados de arquivo para o processamento de lote mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f7aea-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="f7aea-108">Do Stream Analytics tem integração de primeira classe com vários serviços do Azure, que estão documentados em detalhe aqui.</span><span class="sxs-lookup"><span data-stu-id="f7aea-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="f7aea-109">uma tarefa de Stream Analytics tooyour saída tooadd:</span><span class="sxs-lookup"><span data-stu-id="f7aea-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="f7aea-110">No Olá [portal do Azure](https://portal.azure.com), abra o seu trabalho e clique em **saídas** e, em seguida, clique em **adicionar** no painel de saídas Olá que aparece.</span><span class="sxs-lookup"><span data-stu-id="f7aea-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![Adicione saídas](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="f7aea-112">Forneça um nome amigável para esta saída no Olá **Alias de saída** caixa.</span><span class="sxs-lookup"><span data-stu-id="f7aea-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="f7aea-113">Este nome pode ser utilizado na consulta da tarefa mais tarde no toorefer toohello saída.</span><span class="sxs-lookup"><span data-stu-id="f7aea-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="f7aea-114">Preencha o resto Olá Olá necessário ligação propriedades tooconnect tooyour saída.</span><span class="sxs-lookup"><span data-stu-id="f7aea-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="f7aea-115">Estes campos variam consoante o tipo de resultado e estão definidos em detalhe aqui.</span><span class="sxs-lookup"><span data-stu-id="f7aea-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Escolha o tipo de movimento de dados](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="f7aea-117">Dependendo do tipo de saída Olá, poderá ser necessário toospecify como dados de Olá são serializados ou formatados.</span><span class="sxs-lookup"><span data-stu-id="f7aea-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="f7aea-118">definições de serialização específica de Olá para cada tipo de saída estão documentadas aqui.</span><span class="sxs-lookup"><span data-stu-id="f7aea-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="f7aea-119">Preencha o resto Olá Olá ligação necessárias propriedades tooconnect tooyour da origem de dados.</span><span class="sxs-lookup"><span data-stu-id="f7aea-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="f7aea-120">Estes campos variam consoante o tipo de entrada e de origem e estão definidos em detalhe no Olá [artigo Criar tarefa](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="f7aea-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="f7aea-121">Qualquer tarefa adicionada toohello do elemento de saída, tem de existir antes de Olá a tarefa foi iniciada e eventos de iniciar o fluxo.</span><span class="sxs-lookup"><span data-stu-id="f7aea-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="f7aea-122">Por exemplo, se utilizar o Blob storage como resultado, a tarefa de Olá não criará uma conta do storage automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f7aea-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="f7aea-123">Tem de toobe criado por utilizador Olá antes Olá ASA a tarefa foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="f7aea-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="f7aea-124">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="f7aea-124">Get help</span></span>
<span data-ttu-id="f7aea-125">Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f7aea-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7aea-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f7aea-126">Next steps</span></span>
* [<span data-ttu-id="f7aea-127">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f7aea-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f7aea-128">Começar a utilizar o Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f7aea-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f7aea-129">Tarefas de escala do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f7aea-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f7aea-130">Referência do idioma de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f7aea-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f7aea-131">Referência de API do REST de gestão do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f7aea-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

