---
title: "AAA \"consultar um índice (portal - pesquisa do Azure) | Microsoft Docs\""
description: "Emita uma consulta de pesquisa no Explorador de pesquisa do Portal do Azure Olá."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="a5be8-103">Consultar um índice da Azure Search utilizando o Explorador de pesquisa na Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a5be8-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a5be8-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="a5be8-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="a5be8-105">Portal</span><span class="sxs-lookup"><span data-stu-id="a5be8-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="a5be8-106">.NET</span><span class="sxs-lookup"><span data-stu-id="a5be8-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="a5be8-107">REST</span><span class="sxs-lookup"><span data-stu-id="a5be8-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="a5be8-108">Este artigo mostra como tooquery da Azure Search índice utilizando **Explorador de pesquisa** no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5be8-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="a5be8-109">Pode utilizar o Explorador de pesquisa toosubmit simple ou completo Lucene consulta cadeias tooany índice existente no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="a5be8-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="a5be8-110">Dashboard de serviço Olá aberta</span><span class="sxs-lookup"><span data-stu-id="a5be8-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="a5be8-111">Clique em **todos os recursos** na barra de índice de Olá na Olá à esquerda do lado do Olá [portal do Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="a5be8-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="a5be8-112">Selecione o seu serviço do Azure Search.</span><span class="sxs-lookup"><span data-stu-id="a5be8-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="a5be8-113">Selecionar um índice</span><span class="sxs-lookup"><span data-stu-id="a5be8-113">Select an index</span></span>

<span data-ttu-id="a5be8-114">Índice de Olá selecione gostaria toosearch de Olá **índices** mosaico.</span><span class="sxs-lookup"><span data-stu-id="a5be8-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="a5be8-115">Abrir o Explorador de Procura</span><span class="sxs-lookup"><span data-stu-id="a5be8-115">Open Search Explorer</span></span>

<span data-ttu-id="a5be8-116">Clique em Olá barra de pesquisa do Explorador de pesquisa mosaico tooslide Olá aberta e painel de resultados.</span><span class="sxs-lookup"><span data-stu-id="a5be8-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="a5be8-117">Inicie a pesquisa</span><span class="sxs-lookup"><span data-stu-id="a5be8-117">Start searching</span></span>

<span data-ttu-id="a5be8-118">Quando utilizar Olá Explorador de pesquisa, pode especificar [parâmetros de consulta](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) consulta de Olá tooformulate.</span><span class="sxs-lookup"><span data-stu-id="a5be8-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="a5be8-119">Em **Cadeia de consulta**, escreva uma consulta e, em seguida, prima **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="a5be8-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="a5be8-120">cadeia de consulta Olá é analisada automaticamente para o pedido adequado Olá URL toosubmit um pedido HTTP relativamente Olá API REST da Azure Search.</span><span class="sxs-lookup"><span data-stu-id="a5be8-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="a5be8-121">Pode utilizar qualquer simple ou completo Lucene consulta sintaxe toocreate Olá pedido válido.</span><span class="sxs-lookup"><span data-stu-id="a5be8-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="a5be8-122">Olá `*` caráter é equivalente tooan pesquisa de vazio ou não que devolve todos os documentos não ordem específica.</span><span class="sxs-lookup"><span data-stu-id="a5be8-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="a5be8-123">No **resultados**, os resultados da consulta são apresentados no JSON não processado, toohello idênticos payload devolvido no corpo de resposta HTTP ao emitir pedidos através de programação.</span><span class="sxs-lookup"><span data-stu-id="a5be8-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="a5be8-124">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a5be8-124">Next steps</span></span>

<span data-ttu-id="a5be8-125">Olá, os seguintes recursos fornece informações de sintaxe de consulta adicionais e exemplos.</span><span class="sxs-lookup"><span data-stu-id="a5be8-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="a5be8-126">Sintaxe de consulta simples</span><span class="sxs-lookup"><span data-stu-id="a5be8-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="a5be8-127">Sintaxe de consulta Lucene</span><span class="sxs-lookup"><span data-stu-id="a5be8-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="a5be8-128">Exemplos de sintaxe de consulta Lucene</span><span class="sxs-lookup"><span data-stu-id="a5be8-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="a5be8-129">Sintaxe de expressão de Filtro OData</span><span class="sxs-lookup"><span data-stu-id="a5be8-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 