---
title: problemas de desempenho de aaaTroubleshoot e otimizar a base de dados | Microsoft Docs
description: "Aplicar as recomendações de desempenho tooyour base de dados SQL, bem como lear como toogain informações sobre Olá desempenho das consultas de Olá em execução na sua base de dados"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="b5221-103">Resolver problemas de desempenho e otimizar a base de dados</span><span class="sxs-lookup"><span data-stu-id="b5221-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="b5221-104">Os índices em falta e as consultas mal otimizadas são razões comuns para um desempenho fraco da base de dados.</span><span class="sxs-lookup"><span data-stu-id="b5221-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="b5221-105">Neste tutorial que aprende a:</span><span class="sxs-lookup"><span data-stu-id="b5221-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b5221-106">Reveja, aplicam-se e reverter as recomendações de melhoramento de desempenho</span><span class="sxs-lookup"><span data-stu-id="b5221-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="b5221-107">Localizar consultas com uma utilização intensiva de recursos</span><span class="sxs-lookup"><span data-stu-id="b5221-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="b5221-108">Localizar consultas de execução longa</span><span class="sxs-lookup"><span data-stu-id="b5221-108">Find long running queries</span></span>

> <span data-ttu-id="b5221-109">Precisa de uma carga de trabalho contínua na base de dados com problemas de desempenho – falta um índice, por exemplo tooreceive uma recomendação.</span><span class="sxs-lookup"><span data-stu-id="b5221-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="b5221-110">Início de sessão toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b5221-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="b5221-111">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b5221-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="b5221-112">Rever e aplicar uma recomendação</span><span class="sxs-lookup"><span data-stu-id="b5221-112">Review and apply a recommendation</span></span>

<span data-ttu-id="b5221-113">Siga estes passos tooapply uma recomendação do sistema de Olá da base de dados:</span><span class="sxs-lookup"><span data-stu-id="b5221-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="b5221-114">Clique em Olá **recomendações de desempenho** menu no painel da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5221-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![recomendação de desempenho](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="b5221-116">Na lista de Olá recomendações, selecione uma recomendação de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5221-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="b5221-117">Neste exemplo, criar índice.</span><span class="sxs-lookup"><span data-stu-id="b5221-117">In this example, Create Index.</span></span>

    ![Selecione a recomendação](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="b5221-119">Aplicar a recomendação de Olá clicando Olá **aplicar** botão.</span><span class="sxs-lookup"><span data-stu-id="b5221-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="b5221-120">Opcionalmente, reveja os detalhes de recomendação Olá e ver script Olá T-SQL demasiado ser executado ao clicar no **ver Script** botão.</span><span class="sxs-lookup"><span data-stu-id="b5221-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![aplicar a recomendação](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="b5221-122">[Opcional] Ative a otimização automática para toobe recomendações aplicada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b5221-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![auto Otimização](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="b5221-124">Reverter uma recomendação</span><span class="sxs-lookup"><span data-stu-id="b5221-124">Revert a recommendation</span></span>

<span data-ttu-id="b5221-125">Olá Database Advisor monitoriza cada recomendação implementada.</span><span class="sxs-lookup"><span data-stu-id="b5221-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="b5221-126">Se uma recomendação não melhorar a carga de trabalho Olá, serão automaticamente revertido.</span><span class="sxs-lookup"><span data-stu-id="b5221-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="b5221-127">Reverter manualmente uma recomendação é possíveis, mas não necessariamente na maioria dos casos.</span><span class="sxs-lookup"><span data-stu-id="b5221-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="b5221-128">toorevert uma recomendação:</span><span class="sxs-lookup"><span data-stu-id="b5221-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="b5221-129">Visite o menu de recomendações de desempenho toohello e selecione uma das recomendações de Olá aplicada.</span><span class="sxs-lookup"><span data-stu-id="b5221-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![Selecione a recomendação](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="b5221-131">Na vista de detalhes de Olá, clique em **reverter**.</span><span class="sxs-lookup"><span data-stu-id="b5221-131">In hello details view, click **Revert**.</span></span>

    ![reverter recomendação](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="b5221-133">Localizar a consulta de Olá que consome Olá maioria dos recursos</span><span class="sxs-lookup"><span data-stu-id="b5221-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="b5221-134">Siga estas consultas de Olá passos toofind Olá a consumir mais recursos:</span><span class="sxs-lookup"><span data-stu-id="b5221-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="b5221-135">Clique em Olá **Query Performance Insight** menu no painel da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5221-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="b5221-137">Selecione um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="b5221-137">Select a resource type.</span></span>

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="b5221-139">Selecione Olá primeira consulta numa tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="b5221-139">Select hello first query in hello table.</span></span>

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="b5221-141">Reveja os detalhes de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="b5221-141">Review hello query details.</span></span>

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="b5221-143">Encontrar Olá mais longo, consulta em execução</span><span class="sxs-lookup"><span data-stu-id="b5221-143">Find hello longest running query</span></span>

1. <span data-ttu-id="b5221-144">Aceda tooQuery Performance Insight e selecione Olá **consultas de execução longa** separador.</span><span class="sxs-lookup"><span data-stu-id="b5221-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="b5221-146">Selecione Olá primeira consulta numa tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="b5221-146">Select hello first query in hello table.</span></span>

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="b5221-148">Reveja os detalhes de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="b5221-148">Review hello query details.</span></span>

    ![informações acerca das consultas](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="b5221-150">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b5221-150">Next steps</span></span> 
<span data-ttu-id="b5221-151">Os índices em falta e as consultas mal otimizadas são razões comuns para um desempenho fraco da base de dados.</span><span class="sxs-lookup"><span data-stu-id="b5221-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="b5221-152">Neste tutorial, que aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="b5221-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b5221-153">Reveja, aplicam-se e reverter as recomendações de melhoramento de desempenho</span><span class="sxs-lookup"><span data-stu-id="b5221-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="b5221-154">Localizar consultas com uma utilização intensiva de recursos</span><span class="sxs-lookup"><span data-stu-id="b5221-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="b5221-155">Localizar consultas de execução longa</span><span class="sxs-lookup"><span data-stu-id="b5221-155">Find long running queries</span></span>

[<span data-ttu-id="b5221-156">Sugestões de otimização de desempenho de base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="b5221-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
