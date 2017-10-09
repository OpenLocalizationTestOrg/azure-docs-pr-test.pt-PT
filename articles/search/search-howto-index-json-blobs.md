---
title: aaaIndexing JSON blobs com o indexador de blob do Azure Search
description: "A indexação de blobs JSON com o indexador de blob do Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>A indexação de blobs JSON com o indexador de blob do Azure Search
Este artigo mostra como tooconfigure da Azure Search blob indexador tooextract estruturados conteúdo de blobs que contêm JSON.

## <a name="scenarios"></a>Cenários
Por predefinição, [indexador de blob do Azure Search](search-howto-indexing-azure-blob-storage.md) analisa JSON blobs como um segmento de texto único. Muitas vezes, quer de estrutura de Olá toopreserve dos seus documentos JSON. Por exemplo, dado o documento JSON de Olá

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Pode querer tooparse para uma pesquisa do Azure o documento com "text", "datePublished" e "etiquetas" campos.

Em alternativa, quando os blobs contêm um **matriz de objetos JSON**, poderá pretender que a cada elemento da Olá matriz toobecome um documento de Azure Search separado. Por exemplo, fornecido um blob com este JSON:  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

Pode povoar o índice da Azure Search com três documentos separados, cada um com os campos "id" e "text".

> [!IMPORTANT]
> matriz JSON Olá análise funcionalidade está atualmente em pré-visualização. Está disponível apenas na versão de API REST do Olá **pré-visualização 2015-02-28**. Lembre-se, pré-visualizar APIs foram concebidas para avaliação e de teste e não deve ser utilizadas em ambientes de produção.
>
>

## <a name="setting-up-json-indexing"></a>Como configurar a indexação de JSON
A indexação de JSON blobs é a extração de documento regular toohello semelhantes. Em primeiro lugar, crie Olá datasource exatamente tal como faria normalmente: 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

Em seguida, crie o índice de pesquisa de destino Olá se ainda não tiver um. 

Por fim, crie um indexador e defina Olá `parsingMode` parâmetro demasiado`json` (tooindex cada blob como um único documento) ou `jsonArray` (se os blobs contém matrizes JSON e tem de cada elemento da toobe matriz tratado como um documento separado):

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

Se necessário, utilize **campo mapeamentos** toopick Olá propriedades de Olá origem JSON documento utilizado toopopulate o índice de pesquisa de destino, conforme mostrado na secção seguinte Olá.

> [!IMPORTANT]
> Quando utiliza `json` ou `jsonArray` análise modo da Azure Search parte do princípio de que todos os blobs na sua origem de dados contém o JSON. Se precisar de toosupport uma mistura de JSON e blobs não JSON no Olá mesma origem de dados, permitem-na conhecer no [nosso site UserVoice](https://feedback.azure.com/forums/263029-azure-search).
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>Utilização de documentos de pesquisa do campo mapeamentos toobuild
Atualmente, da Azure Search não é possível indexar documentos JSON arbitrários diretamente, porque suporta tipos de dados apenas primitivos, as matrizes de cadeia e GeoJSON pontos. No entanto, pode utilizar **campo mapeamentos** toopick partes do seu JSON documentar e "de comparação de precisão"-los em campos de nível superior do documento de pesquisa de Olá. toolearn sobre noções básicas de mapeamentos de campo, consulte [mapeamentos de campo de indexador de Azure Search ponte Olá as diferenças entre as origens de dados e os índices de pesquisa](search-indexer-field-mappings.md).

Regressam documento JSON de exemplo tooour:

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Vamos supor que tem um índice de pesquisa com Olá seguintes campos: `text` do tipo `Edm.String`, `date` do tipo `Edm.DateTimeOffset`, e `tags` do tipo `Collection(Edm.String)`. toomap o JSON para Olá pretendido forma, utilize Olá mapeamentos campo a seguir:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

Olá nomes de campo de origem no mapeamentos Olá são especificados utilizando Olá [JSON ponteiro](http://tools.ietf.org/html/rfc6901) notação. Pode começa com uma barra toorefer toohello de raiz do seu documento JSON, em seguida, escolha propriedade Olá pretendida (a arbitrário nível de aninhamento) utilizando o caminho de valores separados por uma barra de reencaminhar.

Também pode consultar os elementos de matriz de tooindividual através da utilização de um índice baseado em zero. Por exemplo, o primeiro elemento da toopick Olá da matriz de "etiquetas" Olá de Olá acima exemplo, utilizar um mapeamento de campo como esta:

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> Se um nome de campo de origem num caminho de mapeamento de campo refere-se a propriedade tooa que não existe no JSON, esse mapeamento é ignorado sem um erro. Isto é feito para que pode suportamos documentos com um esquema diferente (que é um caso de utilização comum). Porque não há nenhuma validação, terá de erros de digitação do tootake cuidado tooavoid na sua especificação de mapeamento de campo.
>
>

Se os documentos JSON só contenham propriedades simples de nível superior, pode não necessitar de mapeamentos de campo de todo. Por exemplo, se o seu JSON assemelha, propriedades de nível superior de Olá "text", "datePublished" e "etiquetas" diretamente mapeia toohello campos correspondente no índice de pesquisa de Olá:

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

Eis um payload completo de indexador com mapeamentos campo:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>A indexação de matrizes aninhadas de JSON
E se pretende tooindex uma matriz de objetos JSON, mas essa matriz é aninhado algures documento Olá? Pode escolher cuja propriedade contém uma matriz de Olá utilizando Olá `documentRoot` propriedade de configuração. Por exemplo, se os blobs tem o seguinte aspeto:

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

utilizar esta matriz de Olá configuração tooindex contida no Olá `level2` propriedade:

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Ajude-na tornar o melhor da Azure Search
Se tiver de pedidos de funcionalidades ou ideias para melhoramentos, entrar toous no nosso [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).
