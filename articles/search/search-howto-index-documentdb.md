---
title: aaaIndexing uma origem de dados de base de dados do Cosmos para a Azure Search | Microsoft Docs
description: Este artigo mostra como toocreate um indexador de Azure Search com base de dados do Cosmos como uma origem de dados.
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Ligar a BD do Cosmos Azure Search utilizando indexadores

Se quiser tooimplement uma pesquisa excelente experiência sobre os dados de base de dados do Cosmos, pode utilizar dados de toopull do indexador de Azure Search para um índice da Azure Search. Neste artigo, vamos mostrar-lhe como toointegrate base de dados do Azure Cosmos com da Azure Search, sem ter toowrite qualquer infraestrutura de indexação de toomaintain de código.

tooset configurar um indexador Cosmos DB, tem de ter um [serviço da Azure Search](search-create-service-portal.md)e criar um índice, da origem de dados e, finalmente, indexador Olá. Pode criar estes objetos utilizando Olá [portal](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), ou [REST API](/rest/api/searchservice/) para todos os idiomas não .NET. 

Se optar por para o portal de Olá, Olá [Assistente para importar dados](search-import-data-portal.md) orienta-o criação de Olá de todos estes recursos.

> [!NOTE]
> BD do cosmos é Olá próxima geração do DocumentDB. Embora o nome do produto Olá é alterado, sintaxe é Olá mesmo como anteriormente. Continuar toospecify `documentdb` conforme indicado neste artigo do indexador. 

> [!TIP]
> Pode iniciar Olá **importar dados** Assistente de Olá Cosmos DB dashboard toosimplify indexação para essa origem de dados. Na navegação à esquerda, vá demasiado**coleções** > **adicionar Azure Search** tooget foi iniciado.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Conceitos do indexador de pesquisa do Azure
Azure Search suporta Olá criação e gestão de origens de dados (incluindo Cosmos DB) e indexadores que operam contra dessas origens de dados.

A **origem de dados** Especifica Olá dados tooindex, credenciais e políticas para identificar as alterações nos dados de Olá (por exemplo, documentos modificados ou eliminados no interior da sua coleção). origem de dados de Olá está definida como um recurso independente para que possa ser utilizado por vários indexadores.

Um **indexador** descreve a forma como os dados de Olá fluem da sua origem de dados para um índice de pesquisa de destino. Um indexador pode ser utilizado para:

* Efetue uma cópia única do Olá dados toopopulate um índice.
* Um índice com as alterações da origem de dados de Olá com base numa agenda de sincronização. agenda de Olá faz parte da definição de indexador Olá.
* Invocar o índice de tooan atualizações a pedido conforme necessário.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>Passo 1: Criar uma origem de dados
toocreate uma origem de dados, efetue um pedido POST:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

corpo de Olá de pedido de Olá contém uma definição de origem do Olá dados, que deve incluir Olá seguintes campos:

* **nome**: escolha toorepresent qualquer nome da base de dados de base de dados do Cosmos.
* **tipo**: tem de ser `documentdb`.
* **credenciais**:
  
  * **connectionString**: necessário. Especifique a base de dados do Olá ligação informações tooyour Azure Cosmos DB no Olá seguinte formato:`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **contentor**:
  
  * **nome**: necessário. Especifique o id Olá Olá Cosmos DB coleção toobe indexada.
  * **consulta**: opcional. Pode especificar uma consulta tooflatten um documento JSON arbitrário para um esquema simples que pode índice da Azure Search.
* **dataChangeDetectionPolicy**: recomendado. Consulte [indexar documentos alterado](#DataChangeDetectionPolicy) secção.
* **dataDeletionDetectionPolicy**: opcional. Consulte [indexar documentos eliminado](#DataDeletionDetectionPolicy) secção.

### <a name="using-queries-tooshape-indexed-data"></a>Utilizar consultas tooshape indexada dados
Pode especificar um tooflatten de consulta de base de dados do Cosmos aninhada propriedades ou matrizes, as propriedades de JSON do projeto e filtrar Olá dados toobe indexada. 

Documento de exemplo:

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

Consulta de filtro:

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

Pelo consulta:

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
Consultas de projecção:

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


Matriz flattening consulta:

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>Passo 2: Criar um índice
Se ainda não tiver uma, crie um índice de pesquisa do Azure de destino. Pode criar um índice utilizando Olá [IU do portal do Azure](search-create-index-portal.md), Olá [criar API REST do índice](/rest/api/searchservice/create-index) ou [índice classe](/dotnet/api/microsoft.azure.search.models.index).

Olá seguinte exemplo cria um índice com um campo de id e a descrição:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

Certifique-se de que Olá esquema do seu índice de destino é compatível com o esquema de Olá de Olá origem de documentos JSON ou saída de Olá da sua projecção de consulta personalizada.

> [!NOTE]
> Para coleções particionadas, chave de documento predefinida Olá é da BD do Cosmos `_rid` propriedade, o que obtém mudar o nome demasiado`rid` na Azure Search. Do além disso, Cosmos BD `_rid` valores contém caracteres inválidos nas chaves de pesquisa do Azure. Por este motivo, Olá `_rid` os valores são codificados em Base64.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mapeamento entre tipos de dados JSON e tipos de dados de pesquisa do Azure
| TIPO DE DADOS JSON | TIPOS DE CAMPO DE ÍNDICE DE DESTINO COMPATÍVEL |
| --- | --- |
| bool |Boolean, EDM |
| Números de aspeto de números inteiros |EDM Edm.Int32, Edm.Int64, |
| Números esse aspeto pontos de vírgula flutuante |Edm.Double, EDM |
| Cadeia |Edm.String |
| Matrizes de tipos primitivos, por exemplo ["a", "b", "c"] |Coleção (Edm.String) |
| Cadeias de aspeto de datas |Edm.DateTimeOffset, EDM |
| Por exemplo GeoJSON objetos {"type": "Ponto", "coordenadas": [lat longo]} |Edm.GeographyPoint |
| Outros objetos JSON |N/D |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>Passo 3: Criar um indexador

Assim que a origem de dados e índice Olá ter sido criado, está pronto toocreate indexador de Olá:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Este indexador for executado a cada duas horas (intervalo de agendamento está definido demasiado "PT2H"). toorun um indexador cada 30 minutos, defina o intervalo de Olá demasiado "PT30M". intervalo de suportados mais curto Olá é de 5 minutos. Olá agenda é opcional - se for omitido, um indexador é executado apenas uma vez quando é criado. No entanto, pode executar uma indexador a pedido em qualquer altura.   

Para obter mais detalhes sobre Olá criar API indexador, veja [criar indexador](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Executar o indexador a pedido
Na adição toorunning periodicamente com base numa agenda, um indexador também pode ser invocado a pedido:

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> Quando executar API devolve com êxito, foi agendada invocação de indexador Olá, mas o processamento real Olá acontece de forma assíncrona. 

Pode monitorizar o estado de indexador de Olá no portal de Olá ou Olá obter indexador Estado API, que iremos descrever junto a utilizar. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Ao obter o estado do indexador
Pode obter o histórico de estado e a execução de Olá de um indexador:

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

resposta Olá contém o estado geral de indexador, invocação de indexador último (ou em curso) Olá e histórico de Olá de invocações de indexador recentes.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

Histórico de execução contém a cópia de segurança toohello 50 mais recentes concluída execuções, que são ordenadas por ordem cronológica inversa (para que execução mais recente Olá vem primeira na resposta Olá).

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Indexar documentos alterados
objetivo Olá de um dado de alterar a política de deteção é tooefficiently identificar itens de dados alterados. Atualmente, a política de Olá só suportada é Olá `High Water Mark` política utilizando Olá `_ts` propriedade (timestamp) fornecida pelo Cosmos DB, que é especificado da seguinte forma:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

Utilizar esta política é vivamente o desempenho de indexador boa tooensure. 

Se estiver a utilizar uma consulta personalizada, certifique-se de que Olá `_ts` propriedade é projetada pela consulta Olá.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Progresso de incremental e consultas personalizadas
Progresso incremental durante a indexação garante que se a execução do indexador for interrompida por falhas transitórias ou o limite de tempo de execução, indexador Olá pode recolher onde foi deixada próxima vez é executado, em vez de ter o conjunto completo de Olá toore índice do zero. Isto é especialmente importante quando indexação coleções de grandes dimensões. 

progresso de incremental tooenable quando utilizar uma consulta personalizada, certifique-se de que a consulta ordena os resultados de Olá por Olá `_ts` coluna. Isto permite periódica verificação apontando da Azure Search que utiliza o progresso de incremental tooprovide na presença de Olá de falhas.   

Em alguns casos, mesmo se a consulta contém um `ORDER BY [collection alias]._ts` cláusula, pesquisa do Azure pode não inferir essa consulta Olá está ordenada por Olá `_ts`. Pode dizer da Azure Search que os resultados são ordenados por utilizando Olá `assumeOrderByHighWaterMarkColumn` propriedade de configuração. toospecify desta sugestão, criar ou atualizar o indexador, da seguinte forma: 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>A indexação eliminar documentos
Quando as linhas são eliminadas da coleção de Olá, normalmente, pretende toodelete as linhas do índice de pesquisa de Olá bem. objetivo Olá uma política de deteção de eliminação de dados é tooefficiently identificar itens de dados eliminadas. Atualmente, a política de Olá só suportada é Olá `Soft Delete` política (eliminação está assinalada com um sinalizador de algumas ordenação), que é especificado da seguinte forma:

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

Se estiver a utilizar uma consulta personalizada, certifique-se essa propriedade Olá referenciada pelo `softDeleteColumnName` é projetada pela consulta Olá.

Olá seguinte exemplo cria uma origem de dados com uma política de eliminação de forma recuperável:

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>Passos seguintes
Parabéns! Aprendeu como toointegrate BD do Cosmos do Azure com a utilização da Azure Search Olá indexador para DB do Cosmos.

* toolearn como mais sobre a BD do Cosmos do Azure, consulte Olá [página do serviço de base de dados do Cosmos](https://azure.microsoft.com/services/documentdb/).
* toolearn como mais sobre a Azure Search, consulte Olá [página do serviço de pesquisa](https://azure.microsoft.com/services/search/).
