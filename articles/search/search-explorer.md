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
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>Consultar um índice da Azure Search utilizando o Explorador de pesquisa na Olá Portal do Azure
> [!div class="op_single_selector"]
> * [Descrição geral](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Este artigo mostra como tooquery da Azure Search índice utilizando **Explorador de pesquisa** no Olá portal do Azure. Pode utilizar o Explorador de pesquisa toosubmit simple ou completo Lucene consulta cadeias tooany índice existente no seu serviço.

## <a name="open-hello-service-dashboard"></a>Dashboard de serviço Olá aberta
1. Clique em **todos os recursos** na barra de índice de Olá na Olá à esquerda do lado do Olá [portal do Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).
2. Selecione o seu serviço do Azure Search.

## <a name="select-an-index"></a>Selecionar um índice

Índice de Olá selecione gostaria toosearch de Olá **índices** mosaico.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Abrir o Explorador de Procura

Clique em Olá barra de pesquisa do Explorador de pesquisa mosaico tooslide Olá aberta e painel de resultados.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Inicie a pesquisa

Quando utilizar Olá Explorador de pesquisa, pode especificar [parâmetros de consulta](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) consulta de Olá tooformulate.

1. Em **Cadeia de consulta**, escreva uma consulta e, em seguida, prima **Pesquisar**. 

   cadeia de consulta Olá é analisada automaticamente para o pedido adequado Olá URL toosubmit um pedido HTTP relativamente Olá API REST da Azure Search.   
   
   Pode utilizar qualquer simple ou completo Lucene consulta sintaxe toocreate Olá pedido válido. Olá `*` caráter é equivalente tooan pesquisa de vazio ou não que devolve todos os documentos não ordem específica.

2. No **resultados**, os resultados da consulta são apresentados no JSON não processado, toohello idênticos payload devolvido no corpo de resposta HTTP ao emitir pedidos através de programação.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Passos seguintes

Olá, os seguintes recursos fornece informações de sintaxe de consulta adicionais e exemplos.

 + [Sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Sintaxe de consulta Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Exemplos de sintaxe de consulta Lucene](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [Sintaxe de expressão de Filtro OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 