---
title: carregamento de aaaData na Azure Search | Microsoft Docs
description: "Saiba como tooupload dados tooan índice da Azure Search."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>Carregar dados tooAzure pesquisa
> [!div class="op_single_selector"]
> * [Descrição geral](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Existem duas formas toopopulate um índice com os seus dados. opção de primeiro Olá é no envio manual dos seus dados para o índice de Olá utilizando Olá da Azure Search [REST API](search-import-data-rest-api.md) ou [.NET SDK](search-import-data-dotnet.md). segunda opção de Olá é demasiado[apontar uma origem de dados suportada](search-indexer-overview.md) tooyour índice e permitir que a Azure Search extraia automaticamente os dados de Olá.

## <a name="push-data-tooan-index"></a>Índice de tooan de dados de push
Esta abordagem diz respeito tooprogrammatically enviar toomake de pesquisa de tooAzure os dados disponíveis para pesquisa-lo. Para aplicações com requisitos de latência muito baixa (por exemplo, se precisar de procurar operações toobe sincronizado com bases de dados de inventário dinâmicas), o modelo de envio de Olá é a única opção.

Pode utilizar Olá [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) ou [.NET SDK](search-import-data-dotnet.md) índice de tooan toopush dados. Não são atualmente suportadas ferramenta para envio de dados através do portal de Olá.

Esta abordagem é mais flexível do que o modelo de extração Olá porque pode carregar documentos individualmente ou em lotes (cópia de segurança too1000 por lote ou 16 MB, consoante o limite que ocorrer primeiro). modelo de envio de Olá também permite-lhe tooupload documentos tooAzure pesquisa, independentemente de onde os dados estão.

formato de dados de Olá compreendido por da Azure Search é JSON e todos os documentos no conjunto de dados de Olá tem de ter campos que mapeiam toofields definida no seu esquema de índice. 

## <a name="pull-data-into-an-index"></a>Extrair dados para um índice
modelo de extração Olá pesquisa uma origem de dados suportada e carrega automaticamente os dados de Olá para o seu índice. No Azure Search, esta função é implementada através de *indexadores*, atualmente disponíveis para [Armazenamento de Blobs](search-howto-indexing-azure-blob-storage.md), [Armazenamento de Tabelas](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [Base de Dados SQL do Azure e SQL Server em VMs do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 

Indexadores ligar uma origem de dados de tooa índice (normalmente, uma tabela, vista ou estrutura equivalente) e campos de tooequivalent de campos de origem no índice de Olá do mapa. Durante a execução, o conjunto de linhas do Olá é automaticamente transformado tooJSON e carregados para o índice especificado Olá. Todos os indexadores suportam o agendamento de modo a que pode especificar a frequência dados Olá são toobe atualizadas. A maioria dos indexadores fornecem se a origem de dados de Olá suportar o controlo de alterações. Ao registar alterações e eliminações tooexisting Ademais documentos toorecognizing novos documentos, indexadores remover a necessidade de Olá tooactively gerir dados Olá no seu índice. 

Funcionalidade de indexador está exposta no Olá [portal do Azure](search-import-data-portal.md), Olá [REST API](/rest/api/searchservice/Indexer-operations)e Olá [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations). 

Um portal de Olá toousing vantagem é que da Azure Search pode normalmente gerar um esquema de índice predefinido para si ao ler os metadados de Olá do conjunto de dados de origem de Olá. Pode modificar o índice gerado Olá até que o índice de Olá é processado, após o qual Olá apenas as edições do esquema permitidos são aqueles que não necessitam de reindexing. Se pretender que o impacto de toomake de alterações de Olá hello esquema diretamente, terá de índice de Olá toorebuild. 

Depois de índice de Olá é preenchido, pode utilizar **Explorador de pesquisa** na barra de comando portal Olá como um passo de verificação.

## <a name="query-an-index-using-search-explorer"></a>Consultar índices com o Explorador de Pesquisas

Uma forma rápida de tooperform uma verificação preliminar no carregamento do documento Olá é toouse **Explorador de pesquisa** no portal de Olá. Explorador de Olá permite-lhe consultar um índice sem ter toowrite qualquer código. Olá experiência de pesquisa é com base nas predefinições, tais como Olá [sintaxe simples](/rest/api/searchservice/simple-query-syntax-in-azure-search) e predefinido [parâmetro de consulta searchMode](/rest/api/searchservice/search-documents). Os resultados são devolvidos em JSON, de modo a que pode inspecionar documento completo Olá.

> [!TIP]
> Várias [exemplos de código da Azure Search](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) incluem incorporados ou prontamente disponíveis conjuntos de dados, oferece uma forma fácil tooget foi iniciado. portal de Olá também fornece um indexador de exemplo e a origem de dados constituída por um conjunto de dados de pequena propriedade de real (com o nome "realestate-nos-sample"). Quando executar o indexador pré-configurada Olá na origem de dados de exemplo de Olá, um índice é criado e carregado com documentos que, em seguida, podem ser consultados no Explorador de pesquisa ou por código de escrita.
