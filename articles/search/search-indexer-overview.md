---
title: aaaIndexers na Azure Search | Microsoft Docs
description: "Pesquise a base de dados SQL do Azure, Azure Cosmos DB ou dados pesquisáveis do armazenamento do Azure tooextract e preencher um índice da Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Indexadores na Pesquisa do Azure
> [!div class="op_single_selector"]
>
> * [Descrição geral](search-indexer-overview.md)
> * [Portal](search-import-data-portal.md)
> * [SQL do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md)
> * [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)
>
>

Um **indexador** na pesquisa do Azure é um crawler que extrai dados pesquisáveis e metadados a partir de uma origem de dados externa e preenche um índice com base nos mapeamentos campo a campo entre o índice de Olá e a origem de dados. Esta abordagem é por vezes, referidos tooas 'modelo de extração' porque o serviço de Olá obtém dados sem ter toowrite qualquer código que envia o índice de tooan de dados.

Pode utilizar um indexador como único Olá significa para ingestão de dados ou utilizar uma combinação de técnicas que incluem a utilização de Olá de um indexador para carregar apenas alguns dos campos de Olá no seu índice.

Pode executar os indexadores a pedido ou numa agenda de atualização de dados periódica que pode ser executada a cada quinze minutos. Atualizações mais frequentes requerem um modelo de push que atualize em simultâneo os dados na Pesquisa do Azure e a origem de dados externa.

## <a name="approaches-for-creating-and-managing-indexers"></a>Abordagens para criar e gerir indexadores
Para indexadores geralmente disponíveis como o Azure SQL ou o Azure Cosmos DB, pode criar e gerir os indexadores utilizando estas abordagens:

* [Portal > Assistente de Importação de Dados ](search-get-started-portal.md)
* [API REST do Serviço](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [SDK do .NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>Passos de configuração básica
Indexadores podem oferecer funcionalidades que estão a origem de dados de toohello exclusivo. Relativamente a isto, alguns aspetos de configuração do indexador ou da origem de dados irão variar consoante o tipo de indexador. No entanto, todos os indexadores partilham Olá mesma composição básica e requisitos. Passos que são comuns tooall indexadores são abordadas abaixo.

### <a name="step-1-create-an-index"></a>Passo 1: criar um índice
Um indexador será automatizar alguns ingestão de toodata relacionados com tarefas, mas a criação de um índice não é um deles. Como pré-requisito, tem de ter um índice predefinido com campos que correspondam aos existentes na origem de dados externa. Para mais informações sobre a estruturação de um índice, consulte o artigo [Create an Index (Azure Search REST API) (Criar um índice (API REST do Azure Search))](https://msdn.microsoft.com/library/azure/dn798941.aspx).

### <a name="step-2-create-a-data-source"></a>Passo 2: criar uma origem de dados
Um indexador obtém dados a partir de uma **origem de dados** que contém informações como uma cadeia de ligação. Atualmente é suportada as seguintes origens de dados de Olá:

* [Base de Dados SQL ou SQL Server do Azure numa máquina virtual do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [BD do Cosmos para o Azure](search-howto-index-documentdb.md)
* [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md), utilizado tooextract texto de PDF, documentos do Office, HTML ou XML
* [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)

Origens de dados são configuradas e geridas independentemente indexadores Olá que as utilizam, que significa que uma origem de dados pode ser utilizada por vários tooload de indexadores mais do que um índice numa altura.

### <a name="step-3create-and-schedule-hello-indexer"></a>Passo 3: criar e agendar indexador Olá
a definição de indexador Olá é uma construção especificação de índice de Olá, origem de dados e uma agenda. Um indexador pode fazer referência a uma origem de dados de outro serviço, desde que essa origem de dados é de Olá mesma subscrição. Para mais informações sobre a estruturação de um indexador, consulte o artigo [Create Indexer (Azure Search REST API) (Criar um indexador (API REST do Azure Search))](https://msdn.microsoft.com/library/azure/dn946899.aspx).

## <a name="next-steps"></a>Passos seguintes
Agora que tem ideia básico Olá, o passo seguinte Olá é tooreview requisitos e o tipo de origem de dados de tooeach específicas de tarefas.

* [Base de Dados SQL ou SQL Server do Azure numa máquina virtual do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [BD do Cosmos para o Azure](search-howto-index-documentdb.md)
* [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md), utilizado tooextract texto de PDF, documentos do Office, HTML ou XML
* [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)
* [A indexação de blobs CSV com o indexador de Azure Search Blob Olá](search-howto-index-csv-blobs.md)
* [Indexar blobs JSON com o indexador Blob do Azure Search](search-howto-index-json-blobs.md)
