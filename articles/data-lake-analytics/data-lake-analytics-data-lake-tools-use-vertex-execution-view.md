---
title: "Olá aaaUse vista de execução de vértice nas ferramentas do Data Lake para Visual Studio | Microsoft Docs"
description: "Saiba como toouse Olá tarefas de Data Lake Analytics tooexam de vista de execução de vértice."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="0fb0a-103">Utilize Olá vista de execução de vértice ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0fb0a-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="0fb0a-104">Saiba como toouse Olá tarefas de Data Lake Analytics tooexam de vista de execução de vértice.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fb0a-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0fb0a-105">Prerequisites</span></span>

<span data-ttu-id="0fb0a-106">É necessário um conhecimento básico da utilização de ferramentas do Data Lake em script do Visual Studio toodevelop U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="0fb0a-107">Consulte [Tutorial: desenvolver scripts U-SQL com ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0fb0a-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="0fb0a-108">Abrir Olá vista de execução de vértice</span><span class="sxs-lookup"><span data-stu-id="0fb0a-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="0fb0a-109">Abra uma tarefa de U-SQL no Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="0fb0a-110">Clique em **vista de execução de vértice** no canto inferior esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="0fb0a-111">Poderá ser pedido tooload perfis pela primeira vez e pode demorar algum tempo consoante a conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Vista de execução de vértice de ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="0fb0a-113">Compreender a vista de execução de vértice</span><span class="sxs-lookup"><span data-stu-id="0fb0a-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="0fb0a-114">Olá vista de execução de vértice tem três partes:</span><span class="sxs-lookup"><span data-stu-id="0fb0a-114">hello Vertex Execution View has three parts:</span></span>

![Vista de execução de vértice de ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="0fb0a-116">Olá **Seletor de vértice** no permite esquerdo Olá selecionar vértices as funcionalidades (tais como dados de 10 de principais de leitura ou optar por fase).</span><span class="sxs-lookup"><span data-stu-id="0fb0a-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="0fb0a-117">Um dos filtros de mais frequentemente utilizadas Olá é toosee Olá **vértices no caminho crítico**.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="0fb0a-118">Olá **caminho crítico** Olá cadeia mais longo de vértices de uma tarefa de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="0fb0a-119">Caminho de crítico de Olá compreender é útil para otimizar as suas tarefas, verificando qual vértice demora tempo mais longo Olá.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Vista de execução de vértice de ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="0fb0a-121">Painel de parte superior ao centro de Olá mostra Olá **com o estado de todos os vértices de Olá**.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Vista de execução de vértice de ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="0fb0a-123">painel do Olá na parte inferior central mostra informações sobre cada vertex:</span><span class="sxs-lookup"><span data-stu-id="0fb0a-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="0fb0a-124">: Processo Olá nome da instância do Olá vértice.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="0fb0a-125">-Lo é composto por diferentes partes no StageName | VertexName | VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="0fb0a-126">Por exemplo, vértice de .v1 [62] Olá SV7_Split representa Olá segunda instância em execução (.v1, índice a partir de 0) número vértice 62 na fase SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="0fb0a-127">Leitura de dados total/Written: Olá estavam dados leitura/escrita por esta vértice.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="0fb0a-128">Estado de estado/saída: Olá estado final quando vértice Olá é terminado.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="0fb0a-129">Tipo de falha do código de saída: Olá Ocorreu um erro ao vértice Olá falhou.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="0fb0a-130">Razão de criação: Por que motivo vértice Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="0fb0a-131">Latência de fila do recurso latência/processe latência/PN: Olá tempo do Olá vértice toowait para recursos, tooprocess dados e toostay na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="0fb0a-132">GUID de processo/criador: GUID vértice do Olá atual em execução ou o criador.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="0fb0a-133">Versão: instância Olá N-ésimo Olá executar vértice (sistema de Olá pode agendar a novas instâncias de um vértice para muitos motivos, por exemplo, ativação pós-falha, computação redundância, etc.)</span><span class="sxs-lookup"><span data-stu-id="0fb0a-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="0fb0a-134">Versão criada tempo.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-134">Version Created Time.</span></span>
* <span data-ttu-id="0fb0a-135">Processar criar início tempo/processe em fila tempo/processe início tempo/processe concluída tempo: quando o processo de vértice Olá começa a criar; Quando o processo de vértice Olá inicia tooqueue; Quando Olá iniciado o processo determinadas vértice; Quando hello determinadas vértice está concluída.</span><span class="sxs-lookup"><span data-stu-id="0fb0a-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fb0a-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0fb0a-136">Next steps</span></span>
* <span data-ttu-id="0fb0a-137">informações de diagnóstico toolog, consulte [aceder a registos de diagnóstico para o Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="0fb0a-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="0fb0a-138">toosee uma consulta mais complexa, consulte [analisar registos de site utilizando o Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="0fb0a-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="0fb0a-139">consulte os detalhes da tarefa tooview, [Browser de tarefa de utilização e a vista de tarefas para tarefas do Azure Data lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="0fb0a-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
