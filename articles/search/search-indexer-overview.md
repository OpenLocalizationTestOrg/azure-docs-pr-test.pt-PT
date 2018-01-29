---
title: Indexadores na Azure Search | Microsoft Docs
description: "Pesquise a base de dados SQL do Azure, o Azure Cosmos DB ou o armazenamento do Azure para extrair dados pesquisáveis e preencher um índice do Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/17/2017
ms.author: heidist
ms.openlocfilehash: a51aa48a9a2c3c062c374885d45f08ae0b397ce1
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/09/2018
---
# <a name="indexers-in-azure-search"></a>Indexadores na Pesquisa do Azure
> [!div class="op_single_selector"]
>
> * [Descrição geral](search-indexer-overview.md)
> * [Portal](search-import-data-portal.md)
> * [SQL do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [BD do Cosmos para o Azure](search-howto-index-cosmosdb.md)
> * [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md)
> * [Table Storage do Azure](search-howto-indexing-azure-tables.md)
>

Um *indexador* na Pesquisa do Azure é um crawler que extrai dados pesquisáveis e metadados de uma origem de dados externa e preenche um índice com base nos mapeamentos campo a campo entre o índice e a sua origem de dados. Esta abordagem é por vezes referida como 'modelo de extração' porque o serviço obtém dados sem precisar de escrever qualquer código que envia dados para um índice.

Os indexadores baseiam-se em tipos de origens de dados ou plataformas, com indexadores individuais para o SQL Server no Azure, o Cosmos DB, o Armazenamento de Tabelas do Azure e o Armazenamento de Blobs, etc.

Pode utilizar um indexador como único meio para ingestão de dados ou utilizar uma combinação de técnicas que incluem a utilização de um indexador para carregar apenas alguns dos campos no seu índice.

Pode executar os indexadores a pedido ou numa agenda de atualização de dados periódica que pode ser executada a cada quinze minutos. Atualizações mais frequentes requerem um modelo de push que atualize em simultâneo os dados na Pesquisa do Azure e a origem de dados externa.

## <a name="approaches-for-creating-and-managing-indexers"></a>Abordagens para criar e gerir indexadores

Pode criar e gerir indexadores com estas abordagens:

* [Portal > Assistente de Importação de Dados ](search-get-started-portal.md)
* [API REST do Serviço](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [SDK do .NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

Inicialmente, um indexador novo é anunciado como uma funcionalidade de pré-visualização. As funcionalidades de pré-visualização são introduzidas em APIs (REST e .NET) e, em seguida, são integradas no portal, após passarem para disponibilidade geral. Se estiver a avaliar um indexador novo, deverá planear sobre como escrever código.

## <a name="basic-configuration-steps"></a>Passos de configuração básica
Os indexadores podem oferecer funcionalidades que são exclusivas da origem de dados. Relativamente a isto, alguns aspetos de configuração do indexador ou da origem de dados irão variar consoante o tipo de indexador. No entanto, todos os indexadores partilham da mesma composição e requisitos básicos. Os passos que são comuns a todos os indexadores são abordados abaixo.

### <a name="step-1-create-a-data-source"></a>Passo 1: criar uma origem de dados
Um indexador solicita dados de uma *origem de dados* que contém informações como uma cadeia de ligação e, possivelmente, credenciais. Atualmente são suportadas as seguintes origens de dados:

* [Base de Dados SQL ou SQL Server do Azure numa máquina virtual do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [BD do Cosmos para o Azure](search-howto-index-cosmosdb.md)
* [Armazenamento de blobs do Azure](search-howto-indexing-azure-blob-storage.md) para determinados tipos de conteúdos
* [Table Storage do Azure](search-howto-indexing-azure-tables.md)

As origens de dados são configuradas e geridas independentemente dos indexadores que as utilizam, o que significa que uma origem de dados pode ser utilizada por vários indexadores para carregar mais de um índice de cada vez.

### <a name="step-2-create-an-index"></a>Passo 2: criar um índice
Um indexador irá automatizar algumas tarefas relacionadas com a ingestão de dados, mas geralmente a criação de um índice não é uma delas. Como pré-requisito, tem de ter um índice predefinido com campos que correspondam aos existentes na origem de dados externa. Para mais informações sobre a estruturação de um índice, consulte o artigo [Create an Index (Azure Search REST API) (Criar um índice (API REST do Azure Search))](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Para obter ajuda com associações de campo, veja [Mapeamentos de campo em indexadores do Azure Search](search-indexer-field-mappings.md).

> [!Tip]
> Apesar de os indexadores não poderem gerar um índice para si, o assistente **Importar dados** do portal pode ser útil. Na maioria dos casos, o assistente pode inferir um esquema de índice a partir dos metadados existentes na origem, apresentando um esquema de índice preliminar que pode editar em linha enquanto o assistente está ativo. Assim que o índice é criado no serviço, as outras edições no portal são limitadas principalmente à adição de novos campos. Considere o assistente para criar, mas não para rever um índice. Para aprendizagem prática, siga os passos no [portal de instruções](search-get-started-portal.md).

### <a name="step-3-create-and-schedule-the-indexer"></a>Passo 3: criar e agendar o indexador
A definição de indexador é uma construção que especifica o índice, a origem de dados e uma agenda. Um indexador pode fazer referência a uma origem de dados de outro serviço, desde que essa origem de dados seja da mesma subscrição. Para mais informações sobre a estruturação de um indexador, consulte o artigo [Create Indexer (Azure Search REST API) (Criar um indexador (API REST do Azure Search))](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).

## <a name="next-steps"></a>Passos seguintes
Agora que tem uma noção básica, o passo seguinte é rever os requisitos e as tarefas específicas de cada tipo de origem de dados.

* [Base de Dados SQL ou SQL Server do Azure numa máquina virtual do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [BD do Cosmos para o Azure](search-howto-index-cosmosdb.md)
* [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md)
* [Table Storage do Azure](search-howto-indexing-azure-tables.md)
* [Indexar blobs CSV com o indexador Blob do Azure Search](search-howto-index-csv-blobs.md)
* [Indexar blobs JSON com o indexador Blob do Azure Search](search-howto-index-json-blobs.md)
