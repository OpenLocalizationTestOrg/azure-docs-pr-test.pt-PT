---
title: "aaaAzure pesquisa serviço REST API versão pré-visualização 2015-02-28-| Microsoft Docs"
description: "Pré-visualização do Azure pesquisa serviço REST API versão 2015-02-28-inclui funcionalidades experimental como Natural analisadores de idioma e moreLikeThis pesquisas."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>API de REST do serviço de pesquisa do Azure: Versão de pré-visualização 2015-02-28-
Este artigo é a documentação de referência de Olá para `api-version=2015-02-28-Preview`. Esta pré-visualização expande Olá versão atual do geralmente disponível, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), fornecendo Olá experimental funcionalidades a seguir:

* `moreLikeThis`consultar o parâmetro na Olá [documentos sobre pesquisa](#SearchDocs) API. Encontrar outros documentos do documento específico tooanother relevantes.

Algumas partes adicionais de Olá `2015-02-28-Preview` REST API estão documentados em separado. Estas incluem:

* [Perfis de classificação](search-api-scoring-profiles-2015-02-28-preview.md)
* [Indexadores](search-api-indexers-2015-02-28-preview.md)

Serviço de pesquisa do Azure está disponível em múltiplas versões. Consulte demasiado[controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter mais detalhes.

## <a name="apis-in-this-document"></a>APIs neste documento
API do serviço de pesquisa do Azure suporta dois sintaxes de URL para operações de API: simples e OData (consulte [suporte para OData (API da Azure Search)](http://msdn.microsoft.com/library/azure/dn798932.aspx) para obter detalhes). Olá lista seguinte mostra Olá de sintaxe simples.

[Criar o índice](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[Atualizar o índice](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[Obter o índice](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[Índices de listagem](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[Obter estatísticas de índice](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[Analisador de teste](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[Eliminar um índice](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[Adicionar, eliminar e atualizar os dados dentro de um índice](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[Documentos sobre pesquisa](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[Documento de pesquisa](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[Contagem de documentos](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[Sugestões](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>Operações do índice
Pode criar e gerir índices no serviço de pesquisa do Azure através de pedidos de HTTP simples (POST, GET, PUT, DELETE) em relação a um recurso de índice fornecido. toocreate um índice, PUBLICA primeiro um documento JSON que descreve o esquema de índice de Olá. esquema de Olá define os campos de Olá de índice de Olá, os tipos de dados e como pode ser utilizados (por exemplo, no pesquisas de texto completo, os filtros, ordenação ou facetamento). Também define perfis de classificação, dos sugestores e outro atributos tooconfigure Olá comportamento índice Olá.

Olá exemplo seguinte fornece uma ilustração de um esquema utilizada para procurar informações átrios com o campo de descrição de Olá definido dois idiomas. Repare como atributos controlam a forma como o campo de Olá é utilizado. Por exemplo Olá `hotelId` é utilizado como a chave do documento Olá (`"key": true`) e está excluído das pesquisas de texto completo (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

Depois de criar o índice de Olá, deverá carregar documentos preencher Olá índice. Consulte [adicionar ou atualizar documentos](#AddOrUpdateDocuments) para este passo seguinte.

Para um tooindexing de vídeo de introdução na pesquisa do Azure, consulte Olá [episódio de canal 9 nuvem abrangem na Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).

<a name="CreateIndex"></a>

## <a name="create-index"></a>Criar Índice
Um índice é Olá primário meio organizar e procure-os documentos na Azure Search, semelhante toohow uma tabela organiza registos numa base de dados. Cada índice tem uma coleção de documentos que tudo está em conformidade com esquema de índice toohello (nomes de campo, tipos de dados e propriedades), mas os índices também especificar adicionais construções (dos sugestores, perfis de classificação e opções de CORS) que definem noutros comportamentos de pesquisa.

Pode criar um novo índice dentro de um serviço da Azure Search utilizando um pedido POST de HTTP ou PUT. corpo de Olá de pedido de Olá é um esquema JSON que especifica as informações de configuração e o índice de Olá.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Em alternativa, pode utilizar PUT e especificar o nome do índice Olá Olá URI. Se o índice de Olá não existir, será criado.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

Criar um índice determina a estrutura de Olá Olá documentos armazenados e utilizado em operações de pesquisa. Povoar o índice de Olá é uma operação separada. Para este passo, pode utilizar um [indexador](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponíveis para origens de dados suportadas) ou um [adicionar, atualizar ou eliminar documentos](https://msdn.microsoft.com/library/azure/dn798930.aspx) operação. índice de Olá inverted é gerado quando documentos Olá são publicados.

**Tenha em atenção**: Olá número máximo permitido de índices varia consoante o escalão de preço. serviço gratuito Olá permite cópias de segurança too3 índices. O serviço padrão permite 50 índices por serviço de pesquisa. Consulte [limites e restrições](http://msdn.microsoft.com/library/azure/dn798934.aspx) para obter mais detalhes.

**Pedido**

HTTPS é necessário para todos os pedidos de serviço. Olá **Create Index** pedido pode ser construído com um método POST ou PUT. Quando utilizar POST, tem de fornecer um nome de índice no corpo do pedido de Olá, juntamente com a definição de esquema de índice de Olá. Com PUT, o nome do índice Olá faz parte do URL de Olá. Se não existir índice Olá, é criado. Se já existir, é atualizado toohello nova definição.

o nome do índice Olá tem de ter minúsculas, começar com uma letra ou número, ter nenhum barras ou pontos e de ter menos de 128 carateres. Depois de iniciar o nome do índice Olá com uma letra ou número, rest Olá do nome de Olá pode incluir qualquer letra, o número e travessões, desde que os traços Olá não estão consecutivos.

Olá `api-version` é necessária. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter uma lista de versões disponíveis.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `Content-Type`: Necessário. Defina esta opção demasiado`application/json`
* `api-key`: Necessário. Olá `api-key` é utilizado para
* autentica o serviço de pesquisa de tooyour Olá pedido. É um valor de cadeia, o serviço tooyour exclusivo. Olá **Create Index** pedido tem de incluir um `api-key` cabeçalho definir a chave de administrador tooyour (como chave de consulta tooa oposição ao).

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome de serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

<a name="RequestData"></a>
**Sintaxe de corpo do pedido**

corpo de Olá de pedido de Olá contém uma definição de esquema, que inclui Olá lista de campos de dados dentro de documentos que irão ser sejam fornecidos este índice, tipos de dados, atributos, bem como uma lista opcional de perfis de classificação que é utilizado tooscore correspondente documentos em hora de consulta.

Tenha em atenção que um pedido POST, terá de especificar o nome do índice Olá no corpo do pedido de Olá.

Só pode existir um campo de chave no índice Olá. Tem toobe um campo de cadeia. Este campo representa o identificador exclusivo do Olá para cada documento armazenado no índice Olá.

partes principais do Olá de um índice incluem o seguinte Olá:

* `name`
* `fields`que irá ser sejam fornecidas este índice, incluindo nome, tipo de dados e propriedades que definem as ações permitidas nesse campo.
* `suggesters`utilizado para consultas de conclusão automática ou antecipada.
* `scoringProfiles`utilizado para classificação de pontuação de pesquisa personalizada. Consulte [adicionar perfis de classificação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter mais detalhes.
* `analyzers`, `charFilters`, `tokenizers`, `tokenFilters` utilizado toodefine como documentos/consultas são divididas tokens indexable/pesquisáveis. Consulte [análise na Azure Search](https://aka.ms//azsanalysis) para obter mais detalhes.
* `defaultScoringProfile`Utilizar predefinição de Olá toooverwrite comportamentos de classificação.
* `corsOptions`consultas de várias origens de tooallow face ao seu índice.

sintaxe de Olá para structuring payload de pedido de Olá é a seguinte. Um exemplo de pedido é fornecido mais neste tópico.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**Atributos de índice**

Olá seguintes atributos podem ser definidos quando criar um índice. Para obter detalhes sobre a classificação e perfis de classificação, consulte [adicionar perfis de classificação](https://msdn.microsoft.com/library/azure/dn798928.aspx).

`name`-Conjuntos Olá nome do campo Olá.

`type`-Conjuntos Olá tipo de dados para o campo de Olá.

`searchable`-Marca o campo de Olá como texto completo capaz de pesquisa. Isto significa que vai sofrer Analysis Services, tais como o word quebra durante a indexação. Se definir um `searchable` valor do campo tooa como "sunny dia", internamente será dividida em tokens individuais Olá "sunny" e "dia". Isto permite que as pesquisas de texto completo para estes termos. Os campos do tipo `Edm.String` ou `Collection(Edm.String)` são `searchable` por predefinição. Os campos de outros tipos de não podem ser `searchable`.

* **Tenha em atenção**: `searchable` campos consumam espaço adicional no seu índice, uma vez que a Azure Search irão armazenar uma versão tokenized adicional do valor de campo Olá para pesquisas de texto completo. Se quiser toosave espaço seu índice e não precisa de um toobe campo incluído na procura, defina `searchable` demasiado`false`.

`filterable`-Permite Olá campo toobe referenciado no `$filter` consultas. `filterable`difere da `searchable` na forma como são processadas cadeias. Os campos do tipo `Edm.String` ou `Collection(Edm.String)` que são `filterable` não são submetidos a quebra de palavra, pelo que é comparações para apenas corresponde exato. Por exemplo, se definir esse um campo `f` demasiado "sunny dia", `$filter=f eq 'sunny'` encontrará não corresponde, mas `$filter=f eq 'sunny day'` será. Todos os campos são `filterable` por predefinição.

`sortable`-Por predefinição sistema Olá ordena os resultados por pontuação, mas nas experiências muitos utilizadores serão útil toosort para campos de documentos Olá. Os campos do tipo `Collection(Edm.String)` não pode ser `sortable`. Todos os outros campos são `sortable` por predefinição.

`facetable`-Normalmente utilizadas numa apresentação de resultados de pesquisa que inclui o número de acessos por categoria (por exemplo, procure as câmaras digitais e Consulte pedidos pela marca, por megapixels, por preços, etc.). Esta opção não pode ser utilizada com campos do tipo `Edm.GeographyPoint`. Todos os outros campos são `facetable` por predefinição.

* **Tenha em atenção**: campos do tipo `Edm.String` que são `filterable`, `sortable`, ou `facetable` pode ter um máximo de 32 KB de comprimento. Isto acontece porque esses campos são tratados como um termo de pesquisa único e Olá comprimento máximo de um termo de pesquisa do Azure é de 32KB. Se precisar de toostore texto mais mais um campo de cadeia única, terá de tooexplicitly definir `filterable`, `sortable`, e `facetable` demasiado`false` na sua definição de índice.
* **Tenha em atenção**: se um campo tenha nenhum dos Olá acima atributos definido demasiado`true` (`searchable`, `filterable`, `sortable`, ou`facetable`) campo Olá eficazmente está excluído do índice de Olá inverted. Esta opção é útil para os campos que não são utilizados em consultas, mas são necessários nos resultados da pesquisa. Excluir esses campos de índice de Olá melhora o desempenho.

`key`-Marcas de escala Olá campo como contendo identificadores exclusivos para documentos no índice Olá. Deve ser selecionado exatamente um campo como Olá `key` campo e tem de ser do tipo `Edm.String`. Campos de chave podem ser utilizado toolook dos documentos diretamente através do Olá [pesquisa API](#LookupAPI).

`retrievable`-Define se campo Olá pode ser devolvido num resultado da pesquisa.  Isto é útil quando pretende toouse um campo (por exemplo, a margem) como um filtro, ordenação ou mecanismo de classificação, mas não pretende que o utilizador do Olá campo toobe toohello visível final. Este atributo tem de ser `true` para `key` campos.

`analyzer`-Conjuntos Olá nome Olá analisador toouse para campo Olá na hora de pesquisa e indexação hora. Para Olá permitido definido de valores consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx). Esta opção pode ser utilizada apenas com `searchable` campos e não podem ser definidos em conjunto com o `searchAnalyzer` ou `indexAnalyzer`.  Assim que for escolhido o analisador de Olá, não pode ser alterada para o campo de Olá.

`searchAnalyzer`-Conjuntos Olá nome do analisador de Olá utilizada no momento de pesquisa para o campo de Olá. Para Olá permitido definido de valores consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx). Esta opção pode ser utilizada apenas com `searchable` campos. Tem de ser definido em conjunto com `indexAnalyzer` e não pode ser definida em conjunto com Olá `analyzer` opção. Este analisador pode ser atualizado num campo existente.

`indexAnalyzer`-Conjuntos Olá nome do analisador de Olá utilizada no momento de indexação para o campo de Olá. Para Olá permitido definido de valores consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx). Esta opção pode ser utilizada apenas com `searchable` campos. Tem de ser definido em conjunto com `searchAnalyzer` e não pode ser definida em conjunto com Olá `analyzer` opção. Assim que for escolhido o analisador de Olá, não pode ser alterada para o campo de Olá.

`suggesters`-Conjuntos Olá os campos que são Olá origem de conteúdo de Olá para sugestões e modo de procura. Consulte [dos Sugestores](#Suggesters) para obter mais detalhes.

`scoringProfiles`-Define personalizados comportamentos classificação que permitem-lhe influenciar os itens são apresentados nos resultados da pesquisa superiores. Perfis de classificação são constituídos por funções e de peso de campo. Consulte [adicionar perfis de classificação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter mais informações sobre os atributos de Olá utilizados num perfil de classificação.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Suporte de idiomas**

Análise de sofrer de campos pesquisáveis que mais frequentemente envolve a quebra de palavra, normalização de texto e filtrar termos. Por predefinição, os campos pesquisáveis na pesquisa do Azure são analisados com Olá [analisador Apache Lucene padrão](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) que quebras de texto em elementos seguir o["Segmentação de texto Unicode"](http://unicode.org/reports/tr29/) regras. Além disso, o analisador padrão Olá converte todos os formulários de minúsculas de tootheir carateres. Documentos indexados e os termos da procura percorrer analysis Olá durante a indexação e processamento de consultas.

A pesquisa do Azure suporta uma variedade de idiomas. Cada idioma requer um analisador de texto não padrão que as contas do características de um determinado idioma. A pesquisa do Azure oferece dois tipos de analisadores:

* 35 analisadores por Lucene.
* 50 analisadores por proprietária linguagem natural a Microsoft processamento tecnologia utilizada no Office e do Bing.

Alguns programadores poderão preferir Olá solução mais familiar, simple e open source do Lucene. Analisadores de Lucene são mais rápidas, mas analisadores de Microsoft Olá avançaram capacidades, como lemmatization, word decompounding (em idiomas alemão, dinamarquês, neerlandês, sueco, norueguês, estónio, concluir, húngaro, Eslovaco) e de reconhecimento de entidade (URLs mensagens de correio eletrónico, datas, números). Se for possível, deve executar comparações de ambos os Olá Microsoft e Lucene analisadores toodecide qual delas é uma opção melhor.

***A sua comparação***

Analisador de Lucene Olá para inglês expande o analisador de Olá padrão. -Remove possessives (do à direita) palavras, aplica-se de que decorrentes como por [Porter decorrentes algoritmo](http://tartarus.org/~martin/PorterStemmer/)e remove inglês [parar palavras](http://en.wikipedia.org/wiki/Stop_words).

Em comparação, o analisador de Microsoft Olá efetua lemmatization em vez de decorrentes. Significa que pode processar formulários word inflected e dados muito melhores o que resulta em mais relevantes resultados de pesquisa (módulo veja 7 de [apresentação da Azure Search MVA](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) para obter mais detalhes).

A indexação com analisadores de Microsoft em média é duas vezes toothree mais lentas do que os respetivos equivalentes de Lucene, consoante o idioma de Olá. Não deve ser afetado significativamente o desempenho de pesquisa para consultas de tamanho médio.

***Configuração***

Para cada campo na definição de índice de Olá, pode definir Olá `analyzer` tooan analisador nome da propriedade que especifica o idioma e o fornecedor. Olá analisador mesmo será aplicada quando a indexação e procure-os para esse campo.
Por exemplo, pode ter campos separados para inglês, francês e espanhol átrios nas descrições que se existem lado lado a lado na Olá mesmo índice. Olá utilize [parâmetro de consulta 'searchFields'](#SearchQueryParameters) toospecify que toosearch específicas do idioma campo contra nas suas consultas. Pode rever os exemplos de consultas que incluem Olá `analyzer` propriedade no [documentos sobre pesquisa](#SearchDocs). 

***Lista de analisador***

Segue-se uma lista de Olá de idiomas suportados, juntamente com os nomes de analisador Lucene e da Microsoft.

<table style="font-size:12">
    <tr>
        <th>Idioma</th>
        <th>Nome de analisador da Microsoft</th>
        <th>Nome do analisador de Lucene</th>
    </tr>
    <tr>
        <td>Árabe</td>
        <td>ar.Microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>Armenian</td>
        <td></td>
        <td>HY.lucene</td>
      </tr>
    <tr>
        <td>Bangla</td>
        <td>Bn.Microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>Basco</td>
        <td></td>
        <td>eu.lucene</td>
    </tr>
      <tr>
         <td>Búlgaro</td>
        <td>BG.Microsoft</td>
        <td>BG.lucene</td>
      </tr>
      <tr>
        <td>Catalan</td>
        <td>CA.Microsoft</td>
        <td>CA.lucene</td>          
      </tr>
    <tr>
        <td>Chinês simplificado</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>Chinês tradicional</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>Croata</td>
        <td>hr.Microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>Checo</td>
        <td>CS.Microsoft</td>
        <td>CS.lucene</td>        
    </tr>    
    <tr>
        <td>Dinamarquês</td>
        <td>da.Microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>Neerlandês</td>
        <td>NL.Microsoft</td>
        <td>NL.lucene</td>    
    </tr>    
    <tr>
        <td>Português</td>        
        <td>en.Microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>Estónio</td>
        <td>et.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Finlandês</td>
        <td>Fi.Microsoft</td>
        <td>Fi.lucene</td>        
    </tr>    
    <tr>
        <td>Francês</td>
        <td>FR.Microsoft</td>
        <td>FR.lucene</td>        
    </tr>
    <tr>
        <td>Galician</td>
        <td></td>
        <td>GL.lucene</td>        
      </tr>
    <tr>
        <td>Alemão</td>
        <td>de.Microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>Grego</td>
        <td>EL.Microsoft</td>
        <td>EL.lucene</td>        
    </tr>
    <tr>
        <td>Gujarati</td>
        <td>Gu.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hebraico</td>
        <td>he.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hindi</td>
        <td>Hi.Microsoft</td>
        <td>Hi.lucene</td>        
    </tr>
    <tr>
        <td>Húngaro</td>        
        <td>HU.Microsoft</td>
        <td>HU.lucene</td>
    </tr>
    <tr>
        <td>Icelandic</td>
        <td>is.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Indonesian (Bahasa)</td>
        <td>ID.Microsoft</td>
        <td>ID.lucene</td>        
    </tr>
    <tr>
        <td>Irish</td>
        <td></td>
          <td>GA.lucene</td>
    </tr>
    <tr>
        <td>Italiano</td>
        <td>IT.Microsoft</td>
        <td>IT.lucene</td>        
    </tr>
    <tr>
        <td>Japonês</td>
        <td>ja.Microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>Kannada</td>
        <td>Ka.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Coreano</td>
        <td>ko.Microsoft</td>
        <td>ko.lucene</td>
    </tr>
    <tr>
        <td>Letão</td>        
        <td>LV.Microsoft</td>
        <td>LV.lucene</td>    
    </tr>
    <tr>
        <td>Lituano</td>
        <td>lt.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malayalam</td>
        <td>ml.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malaio (Latim)</td>
        <td>MS.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Marathi</td>
        <td>MR.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Norueguês</td>
        <td>NB.Microsoft</td>
        <td>no.lucene</td>        
    </tr>
      <tr>
        <td>Persian</td>
        <td></td>
        <td>fa.lucene</td>        
      </tr>
    <tr>
        <td>Polaco</td>
        <td>PL.Microsoft</td>
        <td>PL.lucene</td>        
    </tr>
    <tr>
        <td>Português (Brasil)</td>
        <td>pt Br.microsoft</td>
        <td>pt Br.lucene</td>        
    </tr>
    <tr>
        <td>Português (Portugal)</td>
        <td>pt Pt.microsoft</td>        
        <td>pt Pt.lucene</td>
    </tr>
    <tr>
        <td>Punjabi</td>
        <td>Pa.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Romeno</td>
        <td>ro.Microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>Russo</td>
        <td>RU.Microsoft</td>
        <td>RU.lucene</td>    
    </tr>
    <tr>
        <td>Sérvio (Cirílico)</td>
        <td>SR-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Sérvio (Latim)</td>
        <td>SR-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Eslovaco</td>
        <td>SK.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Esloveno</td>
        <td>SL.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Espanhol</td>
        <td>es.Microsoft</td>
        <td>es.lucene</td>
    </tr>
    <tr>
        <td>Sueco</td>
        <td>SV.Microsoft</td>
        <td>SV.lucene</td>
    </tr>

    <tr>
        <td>Tamil</td>
        <td>ta.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Telugu</td>
        <td>te.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Tailandês</td>
        <td>TH.Microsoft</td>
        <td>TH.lucene</td>
    </tr>
    <tr>
        <td>Turco</td>
        <td>TR.Microsoft</td>
        <td>TR.lucene</td>        
    </tr>
    <tr>
        <td>Ucraniano</td>
        <td>UK.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Urdu</td>
        <td>your.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Vietnamita</td>
        <td>VI.Microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">Além disso pesquisa do Azure fornece configurações de analisador de idioma desconhecidas</td>
    <tr>
        <td>Subconjunto de validação padrão ASCII</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>Segmentação de texto Unicode (atomizador padrão)</li>
            <li>Filtro de subconjunto de validação ASCII - converte carateres Unicode, que não pertençam toohello conjunto primeiro 127 caracteres ASCII para os respetivos equivalentes de ASCII. Isto é útil para remover diacritics.</li>
        </ul>
        </td>
    </tr>
</table>

Todos os analisadores com nomes anotados com <i>lucene</i> são utiliza a tecnologia de [analisadores de idiomas do Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html). Podem encontrar mais informações sobre ASCII Olá subconjunto de validação do filtro [aqui](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).

**Sugestões**

A `suggester` define os campos num índice são utilizado toosupport a conclusão automática em procuras. Normalmente, cadeias de procura parcial são enviadas toohello [sugestões API](#Suggestions) enquanto utilizador Olá é escrever uma consulta de pesquisa e Olá API devolve um conjunto de expressões sugeridos. Um sugestor por si no índice Olá determina os campos são utilizados toobuild Olá pesquisa antecipada termos. Consulte [dos Sugestores](#Suggesters) para detalhes de configuração.

**Perfis de classificação**

A `scoringProfile` define personalizados comportamentos classificação que permitem-lhe influenciar quais os itens são apresentados nos resultados de pesquisa de Olá superiores. Perfis de classificação são constituídos por funções e de peso de campo. toouse-las, especifique um perfil de por nome na cadeia de consulta Olá.

Um perfil de classificação de predefinido funciona atrás Olá em segundo plano toocompute uma pontuação de pesquisa para cada item num conjunto de resultados. Pode utilizar o perfil de classificação interna, sem nome Olá. Em alternativa, defina `defaultScoringProfile` toouse um perfil personalizado como predefinição de Olá, invocado sempre que um perfil personalizado não está especificado na cadeia de consulta Olá.

Consulte [Adicionar classificação perfis tooa índice de pesquisa (API do REST de serviço de pesquisa do Azure)](search-api-scoring-profiles-2015-02-28-preview.md) para obter mais detalhes.

**Opções de CORS**

Javascript do lado do cliente não é possível chamar as APIs por predefinição, uma vez que o browser Olá irá impedir que todos os pedidos de várias origens. Ativar o CORS (transversal à partilha de recursos) por definição Olá `corsOptions` índice tooyour do atributo tooallow consultas de várias origens. Tenha em atenção que apenas consulta o suporte APIs CORS por motivos de segurança. Olá seguintes opções pode ser definida para CORS:

* `allowedOrigins`(obrigatório): Esta é uma lista de origens que será atribuído o índice de tooyour de acesso. Isto significa que qualquer código Javascript servido a partir destas origens será permitido tooquery seu índice (assumindo que é fornecida Olá chave de API correta). Cada origem costuma formato Olá `protocol://fully-qualified-domain-name:port` embora porta Olá é frequentemente omitida. Consulte [neste artigo](http://go.microsoft.com/fwlink/?LinkId=330822) para obter mais detalhes.
  * Se pretender que as origens de tooall tooallow acesso, incluir `*` como um único item no Olá `allowedOrigins` matriz. Tenha em atenção que **isto não é recomendado prática para serviços de pesquisa de produção.** No entanto, poderá ser útil para programação ou para fins de depuração.
* `maxAgeInSeconds`(opcional): os Browsers utilizam este valor toodetermine Olá duração (em segundos) toocache CORS prévias respostas. Tem de ser um número inteiro não negativo. Este valor é um melhor desempenho de Olá será maior Olá, mas Olá tempo demora para CORS política alterações tootake efeito. Se não for definido, será utilizada uma duração predefinida de 5 minutos.

<a name="CreateUpdateIndexExample"></a>
**Exemplo de corpo do pedido**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**Resposta**

Para um pedido com êxito: "criado 201".

Por predefinição o corpo da resposta Olá irá conter Olá JSON para a definição de índice de Olá que foi criada. Se hello `Prefer` cabeçalho do pedido está definido demasiado`return=minimal`, o corpo da resposta Olá estará vazio e código de estado de êxito Olá "204 nenhum conteúdo" em vez de "criado 201". Isto acontece independentemente se o PUT ou POST foi índice de Olá toocreate utilizados.

**Observações**

Atualmente, não há suporte limitado para atualizações do esquema de índice. As atualizações do esquema que necessitem de nova indexação, como a alteração de tipos de campo não são atualmente suportadas. Embora os campos existentes não podem ser alterados ou eliminados, adicionar novos campos podem ser índice existente tooan em qualquer altura. Quando é adicionado um novo campo, todos os documentos existentes no índice Olá terão automaticamente um valor nulo para esse campo. Não existe espaço de armazenamento adicional será consumido até novos documentos serem adicionados toohello índice.

<a name="Suggesters"></a>

## <a name="suggesters"></a>Sugestões
funcionalidade de sugestões de Olá na pesquisa do Azure é uma capacidade de consulta antecipada ou conclusão automática, que fornece uma lista de potenciais termos de pesquisa na resposta toopartial cadeia entradas introduzidos na caixa de pesquisa. Provavelmente já reparado sugestões de consulta ao utilizar os motores de busca web comerciais: escrever ".NET" no Bing produz uma lista dos termos de ".NET 4.5", ".NET Framework 3.5", etc. Quando utilizar a REST API do serviço de pesquisa Olá, implementar sugestões numa aplicação personalizada da Azure Search necessita seguinte Olá:

* Ativar as sugestões adicionando um **sugestor** construção no seu índice, dá ao nome de Olá, modo de procura e uma lista de campos para o qual antecipada é invocada. Por exemplo, se especificar "cityName" como um campo de origem, escrevendo uma cadeia de pesquisa parcial de "Sea" resultará em "Seattle", "Seaside" e "Seatac" (todos os três nomes cidade real) oferecidas cópias de segurança como utilizador de toohello de sugestões de consulta.
* Invocar sugestões ao chamar Olá [sugestões API](#Suggestions) no código da aplicação. Normalmente, cadeias de procura parcial são enviadas toohello serviço enquanto utilizador Olá é escrever uma consulta de pesquisa e esta API devolve um conjunto de expressões sugeridos.

Este artigo explica como tooconfigure um **sugestor**. Também deve rever Olá [sugestões API](#Suggestions) para obter detalhes sobre como um sugestor é utilizada.

**Utilização**

`Suggesters`são criadas no índice Olá e funcionam melhor quando utilizado toosuggest específicos documentos em vez de termos soltas ou frases reconhecíveis. os campos de candidatos melhor Olá são títulos, nomes e outras expressões relativamente curtos que podem identificar um item. Campos repetitivos, tais como categorias e etiquetas, ou campos muito como campos de descrições ou comentários, são menos eficientes.

Como parte da definição de índice de Olá, pode adicionar um único sugestor toohello `suggesters` coleção. Propriedades que definem uma sugestor incluem o seguinte Olá:

* `name`: nome de Olá do sugestor Olá. Utilizar nome Olá sugestor Olá ao chamar Olá `suggest` API.
* `searchMode`: Olá toosearch estratégia utilizada para expressões candidatas. Olá único modo suportado atualmente é `analyzingInfixMatching`, que executa uma correspondência de expressões no início de Olá ou no meio de Olá das frases flexível.
* `sourceFields`: Uma lista de um ou mais campos que são Olá origem de conteúdo de Olá de sugestões. Apenas os campos do tipo `Edm.String` e `Collection(Edm.String)` poderá origens para sugestões. Podem ser utilizados apenas os campos que não tenham um analisador de idioma personalizado definido.

**Exemplo de sugestor**

Um sugestor faz parte do índice de Olá. Pode existir apenas um sugestor no Olá `suggesters` coleção na versão atual Olá, juntamente com Olá campos de coleção e `scoringProfiles`.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> Se utilizou a versão de pré-visualização pública Olá da Azure Search, `suggesters` substitui uma propriedade booleana anterior (`"suggestions": false`) que só suportadas sugestões de prefixo para cadeias curtas (3-25 carateres). A substituição, `suggesters`, suporta infix correspondente que encontra termos correspondentes no início de Olá ou no meio de Olá do conteúdo de campo, com tolerância a melhor para prende nas cadeias de procura. A partir da versão geralmente disponível Olá, isto é agora Olá única implementação de sugestões de Olá API. Olá mais antigo `suggestions` propriedade que foi introduzida no `api-version=2014-07-31-Preview` continua toowork em que a versão, mas não está operacional em Olá `2015-02-28` ou versões posteriores de pesquisa do Azure.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>Atualizar o índice
Pode atualizar um índice existente na Azure Search utilizando um pedido HTTP PUT. As atualizações podem incluir a adicionar novos campos toohello existente esquema, modificar opções de CORS e modificar perfis de classificação. Consulte [adicionar perfis de classificação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter mais informações. Especifique o nome Olá Olá índice tooupdate no URI do pedido de Olá:

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Importante:** suporte para atualizações do esquema de índice é limitado toooperations que não necessitam de reconstruir o índice de pesquisa de Olá. As atualizações do esquema que necessitem de uma reindexação, tal como alterar os tipos de campo, não são atualmente suportadas. É possível adicionar novos campos em qualquer altura, embora os campos existentes não podem ser alterados ou eliminados. Olá mesmo se aplica demasiado`suggesters`. É possível adicionar novos campos tooa sugestor em campos de Olá Olá tempo são adicionados, mas não não possível remover os campos `suggesters` e os campos existentes não não possível adicionar demasiado`suggesters`.

Ao adicionar um novo campo tooan o índice, todos os documentos existentes no índice Olá terão automaticamente um valor nulo para esse campo. Não existe espaço de armazenamento adicional será consumido até novos documentos serem adicionados toohello índice.

**Pedido**

HTTPS é necessário para todos os pedidos de serviço. Olá **atualização índice** pedido é construído através de HTTP PUT. Com PUT, o nome do índice Olá faz parte do URL de Olá. Se não existir índice Olá, é criado. Se já existe um índice de Olá, é atualizado toohello nova definição.

o nome do índice Olá tem de ter minúsculas, começar com uma letra ou número, ter nenhum barras ou pontos e de ter menos de 128 carateres. Depois de iniciar o nome do índice Olá com uma letra ou número, rest Olá do nome de Olá pode incluir qualquer letra, o número e travessões, desde que os traços Olá não estão consecutivos.

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `Content-Type`: Necessário. Defina esta opção demasiado`application/json`
* `api-key`: Necessário. Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o serviço tooyour exclusivo. Olá **atualização índice** pedido tem de incluir um `api-key` cabeçalho definir a chave de administrador tooyour (como chave de consulta tooa oposição ao).

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Sintaxe de corpo do pedido**

Ao atualizar um índice existente, corpo Olá tem de incluir definição de esquema original Olá, mais campos novos Olá que estiver a adicionar, bem como Olá modificado perfis de classificação, dos sugestores e opções de CORS, se aplicável. Se não modifica os perfis de classificação de Olá e opções de CORS, tem de incluir originals Olá do quando o índice de Olá foi criado. Em geral Olá melhor padrão toouse atualizações é a definição do índice Olá tooretrieve com uma ação obter, modificá-lo e, em seguida, atualizá-lo com PUT.

utilizada a sintaxe de esquema Olá toocreate que um índice é reproduzido aqui para sua comodidade. Consulte [Create Index](#CreateIndex) para obter mais detalhes.

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**Resposta**

Para um pedido com êxito: "204 nenhum conteúdo".

Por predefinição o corpo da resposta Olá estará vazio. No entanto, se hello `Prefer` cabeçalho do pedido está definido demasiado`return=representation`, corpo da resposta Olá irá conter Olá JSON para a definição de índice de Olá que foi atualizada. Neste caso, o código de estado de êxito de Olá será "200 OK".

**Atualizar a definição do índice com analisadores personalizados**

Quando está definido uma analyzer, um atomizador, um filtro de token ou um filtro de char, não pode ser modificado. Novos podem ser adicionados índice existente tooan apenas se hello `allowIndexDowntime` sinalizador é definido tootrue no pedido de actualização do índice Olá: 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

Tenha em atenção que esta operação irá colocar o índice offline para, pelo menos, alguns segundos, fazendo com que a indexação e consulta pedidos toofail. Disponibilidade de desempenho e de escrita do índice de Olá pode ser afetada durante vários minutos após a atualização do índice de Olá ou superior para índices muito grande.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>Índices de lista
Olá **lista índices** operação devolve uma lista de índices de Olá atualmente no seu serviço da Azure Search.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**Pedido**

HTTPS é necessário para todos os pedidos de serviço. Olá **lista índices** pedido pode ser construído com o método GET de Olá.

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `api-key`: Necessário. Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o serviço tooyour exclusivo. Olá **lista índices** pedido tem de incluir um `api-key` conjunto tooan chave de administração (como chave de consulta tooa oposição ao).

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

nenhum.

**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

Eis um corpo de resposta de exemplo:

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

Tenha em atenção que pode filtrar resposta Olá baixo propriedades de Olá toojust que estiver interessado em. Por exemplo, se pretender que apenas uma lista de nomes de índice, utilizar Olá OData `$select` opção de consulta:

    GET /indexes?api-version=2015-02-28-Preview&$select=name

Neste caso, resposta de Olá do Olá acima exemplo deverá aparecer da seguinte forma:

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

Esta é uma largura de banda de toosave técnica útil se tiver muitos dos índices no serviço de pesquisa.

<a name="GetIndex"></a>

## <a name="get-index"></a>Obter o índice
Olá **obter índice** operação obtém a definição de índice de Olá da Azure Search.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Pedido**

HTTPS é necessário para pedidos de serviço. Olá **obter índice** pedido pode ser construído com o método GET de Olá.

Olá [nome do índice] no URI de pedido de Olá Especifica qual tooreturn de índice da coleção de índices de Olá.

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o serviço tooyour exclusivo. Olá **obter índice** pedido tem de incluir um `api-key` conjunto tooan chave de administração (como chave de consulta tooa oposição ao).

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

nenhum.

**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

Consulte o exemplo de Olá JSON no [criando e atualizando um índice](#CreateUpdateIndexExample) para obter um exemplo de Olá de respostas o payload.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>Eliminar o índice
Olá **eliminar índice** operação remove um índice e os documentos associados do seu serviço da Azure Search. Pode obter o nome do índice Olá de dashboard de serviço de Olá no Olá portal do Azure ou de Olá API. Consulte [lista índices](#ListIndexes) para obter mais detalhes.

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Pedido**

HTTPS é necessário para pedidos de serviço. Olá **eliminar índice** pedido pode ser construído com o método DELETE de Olá.

Olá [nome do índice] no URI de pedido de Olá Especifica qual toodelete de índice da coleção de índices de Olá.

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `api-key`: Necessário. Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o URL do serviço tooyour exclusivo. Olá **eliminar índice** pedido tem de incluir um `api-key` cabeçalho definir a chave de administrador tooyour (como chave de consulta tooa oposição ao).

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

nenhum.

**Resposta**

Código de estado: 204 conteúdo não é devolvido para uma resposta com êxito.

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>Obter estatísticas de índice
Olá **obter estatísticas de índice** operação devolve da Azure Search, uma contagem de documentos para o índice atual Olá, mais a utilização do armazenamento.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Estatísticas de documento contagem e tamanho de armazenamento são recolhidas a cada alguns minutos, não em tempo real. Por conseguinte, as estatísticas de Olá devolvidas por esta API podem não refletir alterações causado por operações de indexação recentes.
> 
> 

**Pedido**

HTTPS é necessário para todos os pedidos de serviços. Olá **obter estatísticas de índice** pedido pode ser construído com o método GET de Olá.

Olá [nome do índice] no URI de pedido de Olá indica Olá serviço tooreturn índice as estatísticas de índice especificado Olá.

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o serviço tooyour exclusivo. Olá **obter estatísticas de índice** pedido tem de incluir um `api-key` conjunto tooan chave de administração (como chave de consulta tooa oposição ao).

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

nenhum.

**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

corpo da resposta Olá está a ser Olá seguinte formato:

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>Analisador de teste
Olá **analisar API** mostra como um analisador de quebras de texto em tokens.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Pedido**

HTTPS é necessário para todos os pedidos de serviços. Olá **analisar API** pedido pode ser construído com o método POST de Olá.

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o serviço tooyour exclusivo. Olá **analisar API** pedido tem de incluir um `api-key` conjunto tooan chave de administração (como chave de consulta tooa oposição ao).

Também terá do nome do índice Olá e Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

ou

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

Olá `analyzer_name`, `tokenizer_name`, `token_filter_name` e `char_filter_name` necessário toobe nomes válidos de analisadores de predefinidos ou personalizados, tokenizers, filtros de token e filtros de char para o índice de Olá. toolearn mais informações sobre o processo de Olá de análise lexical consulte [análise na Azure Search](https://aka.ms/azsanalysis).

**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

corpo da resposta Olá está a ser Olá seguinte formato:

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**Analisar o exemplo de API**

**Pedido**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**Resposta**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>Operações do documento
Na Azure Search, um índice é armazenado na nuvem de Olá e povoar utilizando documentos JSON que carregar toohello serviço. Todos os documentos de Olá que carregar é constituída por corpus Olá dos seus dados de pesquisa. Documentos contêm campos, algumas das quais são com token em termos de pesquisa que são carregados. Olá `/docs` segmento de URL no Olá API da Azure Search representa a coleção de Olá de documentos num índice. Todas as operações executadas numa coleção de Olá como carregar, intercalar, eliminar ou consultar documentos ocorrer no contexto de Olá de um índice único, por isso, Olá URLs para estas operações serão sempre começar a utilizar `/indexes/[index name]/docs` para um nome de índice fornecido.

O código da aplicação ou tem de gerar JSON documentos tooupload tooAzure pesquisa ou pode utilizar um [indexador](https://msdn.microsoft.com/library/dn946891.aspx) tooload documentos se a origem de dados de Olá é a SQL Database do Azure ou a base de dados do Azure Cosmos. Normalmente, são povoados índices de um único conjunto de dados que fornecer.

Deve planear ter um documento para cada item que pretende que o toosearch. Uma aplicação de rental filmes pode ter um documento por filmes, uma aplicação storefront pode ter um documento por SKU, uma aplicação online courseware pode ter um documento por decorrer, um firm de pesquisa pode ter um documento para cada documento académico no respetivo repositório e assim sucessivamente.

Documentos é constituída por um ou mais campos. Campos podem conter texto que é atomizado pela pesquisa do Azure em termos de pesquisa, bem como não atomizada ou valores de texto não podem ser utilizados em filtros ou perfis de classificação. Olá nomes, tipos de dados e as funcionalidades de pesquisa são suportadas para cada campo são determinadas pelo esquema de índice de Olá. Um dos campos de Olá cada esquema de índice tem de ser designado como um ID e cada documento tem de ter um valor para o campo de ID de Olá que identifica exclusivamente esse documento no índice Olá. Todos os outros campos de documento são opcionais e serão predefinido tooa um valor nulo se especificado. Tenha em atenção que os valores nulos não demorar até espaço no índice de pesquisa de Olá.

Antes de pode carregar documentos, deve já tiver criado o índice de Olá no serviço de Olá. Consulte [Create Index](#CreateIndex) para obter detalhes sobre neste primeiro passo.

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>Adicionar, atualizar, ou eliminar documentos
Pode carregar, documentos de intercalação, intercalação ou carregamento ou eliminação de um índice especificado utilizando o HTTP POST. Para grandes quantidades de atualizações, a criação de batches de documentos (too1000 documentos por lote) ou cerca de 16 MB por lote é recomendada.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Pedido**

HTTPS é necessário para todos os pedidos de serviço. Pode carregar, documentos de intercalação, intercalação ou carregamento ou eliminação de um índice especificado utilizando o HTTP POST.

pedido de Olá URI inclui [nome do índice], especificando os documentos de toopost do índice. Só pode publicar o índice de tooone documentos cada vez.

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `Content-Type`: Necessário. Defina esta opção demasiado`application/json`
* `api-key`: Necessário. Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o serviço tooyour exclusivo. Olá **adicionar documentos** pedido tem de incluir um `api-key` cabeçalho definir a chave de administrador tooyour (como chave de consulta tooa oposição ao).

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

corpo de Olá de pedido de Olá contém um ou mais documentos toobe indexada. Documentos são identificados por uma chave exclusiva. Cada documento está associado uma ação: carregar, intercalação, mergeOrUpload ou delete. Os pedidos de carregamento tem de incluir dados de documento Olá como um conjunto de pares chave/valor.

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> Chaves de documento só podem conter letras, números, travessões ("-"), carateres de sublinhado ("_") e sinais de igual ("="). Para obter mais detalhes, consulte [regras de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx).
> 
> 

**Ações de documentos**

* `upload`: Uma ação de carregamento é semelhante tooan "upsert" onde o documento de Olá será inserido se for novo e atualizado/substituído se já existir. Tenha em atenção de que todos os campos são substituídos no caso de atualização de Olá.
* `merge`: Atualizações intercalação existente documento com Olá especificado campos. Se não existir documento Olá, intercalação Olá irá falhar. Qualquer campo que especifique numa intercalação irá substituir o campo existente do Olá documento Olá. Isto inclui campos do tipo `Collection(Edm.String)`. Por exemplo, se hello o documento contém um campo "etiquetas" com o valor `["budget"]` e executar uma intercalação com valor `["economy", "pool"]` para "etiquetas", o valor final do Olá do campo de etiquetas"Olá" será `["economy", "pool"]`. Este irá **não** ser `["budget", "economy", "pool"]`.
* `mergeOrUpload`: tem o mesmo comportamento `merge` caso um documento com Olá fornecido chave já exista no índice Olá. Se o documento de Olá não existir, tem o mesmo comportamento `upload` com um novo documento.
* `delete`: Eliminar remove o documento especificado Olá desde o índice de Olá. Tenha em atenção que quaisquer campos que especificar num `delete` operação que não seja o campo de chave Olá será ignorada. Se pretender tooremove um campo individual de um documento, utilize `merge` em vez disso e simplesmente defina o campo de Olá explicitamente demasiado`null`.

**Resposta**

Código de estado 200 (OK) é devolvido para uma resposta com êxito, o que significa que todos os itens têm indexados com êxito. Esta situação é indicada pelo Olá `status` propriedade que está a ser definida tootrue para todos os itens, bem como Olá `statusCode` propriedade que está a ser definida tooeither 201 (para documentos recentemente carregados) ou 200 (para documentos intercalados ou eliminados):

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

Código de estado 207 (estado multi) é devolvido quando pelo menos um item não foi indexado com êxito. Os itens que não foi indexados têm Olá `status` toofalse de conjunto de campos. Olá `errorMessage` e `statusCode` propriedades irão indicar o motivo Olá Olá indexação de erro:

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

Olá, a tabela seguinte explica Olá várias por documento códigos de estado que podem ser devolvidos na resposta Olá. Tenha em atenção que alguns indicam problemas com o pedido de Olá, enquanto outros indicam condições de erro temporário. última dos Olá que deve repetir após um atraso.

<table style="font-size:12">
    <tr>
        <th>Código de estado</th>
        <th>Significado</th>
        <th>Repetição</th>
        <th>Notas</th>
    </tr>
    <tr>
        <td>200</td>
        <td>Documento com êxito foi modificado ou eliminado.</td>
        <td>n/d</td>
        <td>Eliminar operações são <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>. Ou seja, mesmo se uma chave de documento não existe no índice Olá, tentar uma operação de eliminação com essa chave resultará num código de 200 estado.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>Documento foi criado com êxito.</td>
        <td>n/d</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>Ocorreu um erro no documento de Olá que impediu que está a ser indexado.</td>
        <td>Não</td>
        <td>mensagem de erro de saudação na resposta Olá indicará que está errado documento Olá.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>Não foi possível intercalar o documento de Olá porque Olá fornecida a chave não existe no índice Olá.</td>
        <td>Não</td>
        <td>Este erro não ocorrer para carregamentos, uma vez que criarem novos documentos e não ocorre para eliminações por estarem <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Foi detetado um conflito de versões durante a tentativa de tooindex um documento.</td>
        <td>Sim</td>
        <td>Isto pode acontecer quando está a tentar Olá tooindex mesmo documento mais do que uma vez em simultâneo.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>índice de Olá está temporariamente indisponível porque este foi atualizado com too'true de conjunto de sinalizador Olá 'allowIndexDowntime' '.</td>
        <td>Sim</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>O serviço de pesquisa está temporariamente indisponível, possivelmente devido a carga de tooheavy.</td>
        <td>Sim</td>
        <td>O código deve aguardar antes de repetir neste caso, ou o risco de indisponibilidade do serviço de Olá de prolonging.</td>
    </tr>
</table> 

**Tenha em atenção**: se o código de cliente frequentemente encontra uma resposta 207, uma razão possível é a que o sistema de Olá está sob carga. Pode confirmar isto verificando Olá `statusCode` propriedade 503. Se for este caso de Olá, recomendamos que ***limitação de pedidos de indexação***. Caso contrário, se o tráfego de indexação não subside, sistema Olá foi possível iniciar a rejeitar todos os pedidos com 503 erros.

Código de estado 429 indica que excedeu a quota no número de Olá de documentos por índice. Tem de criar um índice novo ou atualizar para os limites de capacidade superiores.

**Exemplo:**

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>Documentos sobre pesquisa
A **pesquisa** operação é emitida como um pedido GET ou POST e especifica os parâmetros que forneça critérios Olá para selecionar documentos correspondentes.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Quando publicar toouse em vez de obter**

Quando utiliza HTTP GET Olá de toocall **pesquisa** API, terá de toobe em atenção de que o comprimento do URL de pedido de Olá Olá não pode exceder os 8 KB. Isto é normalmente suficiente para a maioria das aplicações. No entanto, algumas aplicações produzem consultas muito grandes ou expressões de filtro de OData. Para estas aplicações, utilizando o HTTP POST é uma melhor opção porque permite maiores filtros e consultas que GET. Com o POST, número de Olá de termos de licenciamento ou de cláusulas numa consulta é Olá limitar o fator de tamanho de Olá não da consulta em bruto de Olá, uma vez que o limite de tamanho do pedido de Olá para o POST é aproximadamente 16 MB.

> [!NOTE]
> Apesar do limite de tamanho de pedido POST Olá é muito grande, consultas de pesquisa e expressões de filtro não podem ser arbitrariamente complexas. Consulte [consulta lucene](https://msdn.microsoft.com/library/mt589323.aspx) e [sintaxe de expressão de OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre limitações de complexidade de consulta e o filtro de pesquisa.
> 
> 

**Pedido**

HTTPS é necessário para pedidos de serviço. Olá **pesquisa** pedido pode ser construído com Olá GET ou métodos POST.

URI de pedido de Olá Especifica qual tooquery de índice, para todos os documentos que correspondem aos parâmetros de Olá. Foram especificados parâmetros na cadeia de consulta Olá no caso de Olá de pedidos GET e no pedido de Olá os pedidos de corpo no caso de Olá da publicação.

Como melhor prática quando criar pedidos GET, lembre-se demasiado[codificar o URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específicas Olá de parâmetros durante a chamada de REST API diretamente. Para **pesquisa** operações, isto inclui:

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

Codificação do URL só é recomendada Olá acima parâmetros de consulta. Se lhe codificar inadvertidamente URL hello cadeia de consulta completo (tudo após Olá?), irão interromper a pedidos.

Além disso, a codificação de URL é necessário apenas quando chamar Olá obter a API de REST diretamente utilizando. Sem codificação do URL é necessário quando chamar **pesquisa** utilização do POST, ou ao utilizar Olá [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que processa a codificação do URL para si.

<a name="SearchQueryParameters"></a>
**Parâmetros de consulta**

**Pesquisa** aceita vários parâmetros que fornecem critérios de consulta e também especificam o comportamento de procura. Terá de fornecer estes parâmetros no URL Olá cadeia de consulta ao chamar **pesquisa** via GET e como as propriedades de JSON no corpo do pedido de Olá ao chamar **pesquisa** através de POST. sintaxe de Olá para alguns parâmetros é ligeiramente diferente entre GET e POST. Estas diferenças são assinaladas como aplicável abaixo:

`search=[string]`(opcional) - Olá toosearch de texto para. Todos os `searchable` campos são pesquisados por predefinição, a menos que `searchFields` está especificado. Quando pesquisar `searchable` campos, Olá pesquisa próprio texto é com token, pelo que vários termos podem ser separados por espaços em branco (por exemplo: `search=hello world`). Utilize qualquer prazo de toomatch `*` (pode ser útil para consultas de filtro booleano). A omissão deste parâmetro tem Olá, mesmo que tenha efeito como defini-la demasiado`*`. Consulte [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) para especificações na sintaxe de pesquisa de Olá.

* **Tenha em atenção**: resultados Olá, por vezes, podem ser surprising ao consultar sobre `searchable` campos. atomizador Olá inclui lógica toohandle casos comuns tooEnglish texto como apostrophes, vírgulas números, etc. Por exemplo, `search=123,456` corresponderá um termo único 123,456 em vez de termos de individuais Olá 123 e 456, uma vez que vírgulas são utilizadas como separadores de milhares de grandes quantidades em inglês. Por este motivo, recomendamos que utilize um espaço em branco em vez de termos de tooseparate pontuação no Olá `search` parâmetro.

`searchMode=any|all`(opcional, será assumida demasiado`any`) - se alguns ou todos os termos de pesquisa de Olá devem corresponder no documento de Olá toocount ordem como uma correspondência.

`searchFields=[string]`(opcional) - lista de Olá de toosearch de nomes de campo de valores separados por vírgulas para Olá especificado texto. Campos de destino devem ser assinalados como `searchable`.

`queryType=simple|full`(opcional, será assumida demasiado`simple`) - quando o texto de pesquisa demasiado "simples" do conjunto é interpretado utilizando uma linguagem de consulta simples que permite como símbolos +, * e "". As consultas são avaliadas em todos os campos pesquisáveis (ou campos indicaram `searchFields`) em cada documento por predefinição. Quando o tipo de consulta Olá está definido demasiado`full` texto de pesquisa é interpretado utilizando a linguagem de consulta Lucene do Olá que lhe permite pesquisas específicas do campo e ponderadas. Consulte [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) e [consulta Lucene](https://msdn.microsoft.com/library/mt589323.aspx) para especificações no sintaxes de pesquisa de Olá. 

> [!NOTE]
> Intervalo de pesquisa na Olá Lucene idioma de consulta não é suportado favor $filter que oferece uma funcionalidade semelhante.
> 
> 

`moreLikeThis=[key]`(opcional) **Importante:** esta funcionalidade só está disponível no `2015-02-28-Preview`. Esta opção não pode ser utilizada numa consulta que contém o parâmetro de pesquisa de texto Olá, `search=[string]`. Olá `moreLikeThis` parâmetro localiza documentos que são semelhantes toohello documento especificado pela chave do documento Olá. Quando é efetuado um pedido de pesquisa com `moreLikeThis`, uma lista dos termos de pesquisa é gerada com base na frequência de Olá e rarity dos termos de documento de origem Olá. Os termos encontram-se, em seguida, utilizado toomake Olá pedido. Por predefinição, Olá conteúdos de todos os `searchable` campos são considerados a menos que `searchFields` é utilizado toorestrict serão pesquisados os campos.  

`$skip=#`(opcional) - número de Olá de pesquisa resulta tooskip; Não pode ser superior a 100.000. Se precisar de documentos tooscan na sequência, mas não é possível utilizar `$skip` devido a limitação de toothis, considere a utilização de `$orderby` numa chave completamente ordenadas e `$filter` com um intervalo de consulta em vez disso.

> [!NOTE]
> Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `skip` em vez de `$skip`.
> 
> 

`$top=#`(opcional) - número de Olá de pesquisa resulta tooretrieve. Isto pode ser utilizado em conjunto com `$skip` tooimplement a paginação do lado do cliente dos resultados da pesquisa.

> [!NOTE]
> Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `top` em vez de `$top`.
> 
> 

`$count=true|false`(opcional, será assumida demasiado`false`)-Especifica se toofetch Olá contagem total de resultados. Esta é a contagem de Olá de todos os documentos que correspondam a Olá `search` e `$filter` parâmetros, a ignorar `$top` e `$skip`. Definir este valor demasiado`true` pode ter um impacto no desempenho. Tenha em atenção que a contagem de Olá devolvida é uma aproximação do seu.

> [!NOTE]
> Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `count` em vez de `$count`.
> 
> 

`$orderby=[string]`(opcional) - uma lista de expressões de valores separados por vírgulas toosort Olá resultados por. Cada expressão pode ser um nome de campo ou uma chamada toohello `geo.distance()` função. Cada expressão pode ser seguido `asc` tooindicated ascendente, e `desc` tooindicate descendente. é por ordem ascendente predefinido Olá. TIES irão dividir por pontuações de correspondência de Olá de documentos. Se não `$orderby` for especificado, sequência de ordenação Olá predefinido é descendente pelo modelo de pontuação de correspondência de documento. Há um limite de 32 cláusulas para `$orderby`.

> [!NOTE]
> Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `orderby` em vez de `$orderby`.
> 
> 

`$select=[string]`(opcional) - uma lista de campos de valores separados por vírgulas tooretrieve. Se não for indicado, todos os campos marcados como recuperável no esquema Olá estão incluídos. Pode também explicitamente pedir todos os campos definindo este parâmetro demasiado`*`.

> [!NOTE]
> Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `select` em vez de `$select`.
> 
> 

`facet=[string]`(zero ou mais) - toofacet um campo pelo. Opcionalmente, cadeia Olá pode conter facetamento Olá toocustomize de parâmetros expressado como valores separados por vírgulas `name:value` pares. Os parâmetros válidos são:

* `count`(máximo de número de termos de faceta; predefinição é 10). Não existe nenhum máximo, mas valores superiores implicar uma correspondente penalidade de desempenho, especialmente se o campo por facetas Olá contém um grande número de termos exclusivos.
  * Por exemplo: `facet=category,count:5` obtém Olá superiores cinco categorias nos resultados de aspeto de restrições.  
  * **Tenha em atenção**: se hello `count` parâmetro é inferior ao número de Olá dos termos exclusivos, resultados de Olá podem não ser exata. Isto acontece devido a forma de toohello consultas facetamento estão distribuídas shards. Aumentar `count` geralmente aumenta Olá precisão de contagens de termo Olá, mas um custo de desempenho.
* `sort`(um dos `count` toosort *descendente* por contagem, `-count` toosort *ascendente* por contagem, `value` toosort *ascendente* pelo valor, ou `-value` toosort *descendente* por valor)
  * Por exemplo: `facet=category,count:3,sort:count` obtém Olá superiores três categorias nos resultados de aspeto de restrições por ordem descendente por número de Olá de documentos com cada nome de cidade. Por exemplo, se Olá superior três categorias são orçamento, hotel e luxo e orçamento tem 5 pedidos, hotel tem 6 e luxo tem 4, Olá registos será por ordem de Olá hotel, orçamento, luxo.
  * Por exemplo: `facet=rating,sort:-value` produz registos para todas as classificações possíveis, por ordem descendente por valor. Por exemplo, se as classificações de Olá são de 1 too5, registos de Olá irão ser ordenados, 5, 4, 3, 2, 1, independentemente de quantas documentos correspondem a cada classificação.
* `values`(delimitado por pipe numérica ou `Edm.DateTimeOffset` valores especificando um conjunto de valores de entrada do aspeto dinâmico)
  * Por exemplo: `facet=baseRate,values:10|20` produz registos três: um para taxa base 0 segurança toobut não incluindo 10, um para 10 cópias de segurança toobut não incluindo 20 e outro para 20 ou superior.
  * Por exemplo: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produz dois registos: um para hotéis renovated antes de Fevereiro de 2010 e outro para hotéis renovated Fevereiro partir do dia 1, 2010 ou posterior.
* `interval`(intervalo de número inteiro maior que 0 para números ou `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` para valores de tempo de data)
  * Por exemplo: `facet=baseRate,interval:100` produz registos com base nos intervalos de taxa de base do tamanho 100. Por exemplo, se forem taxas base todos os entre $60 e $600, será registos para 0-100, 100 200, 200 300, 300 400, 400-500 e 500 600.
  * Por exemplo: `facet=lastRenovationDate,interval:year` produz um registo para todos os anos quando foram renovated hotéis.
* `timeoffset`([+-] hh: mm, [+-] hhmm, ou [+-] hh) `timeoffset` é opcional. Só pode ser combinado com Olá `interval` opção e apenas quando aplicados tooa campo do tipo `Edm.DateTimeOffset`. valor de Olá Especifica Olá UTC tooaccount desfasamento de tempo para definir limites de tempo.
  * Por exemplo: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` utiliza Olá limites do dia que começa em UTC 01:00:00 (meia-noite Olá destino fuso horário)
* **Tenha em atenção**: `count` e `sort` podem ser combinados numa Olá mesmo especificação do aspeto, mas não pode ser combinado com `interval` ou `values`, e `interval` e `values` não podem ser combinados.
* **Tenha em atenção**: facetas de intervalo na data hora são calculadas com base na hora UTC se `timeoffset` não está especificado. Por exemplo: para `facet=lastRenovationDate,interval:day`, limites de dia Olá começam às 00:00:00 UTC. 

> [!NOTE]
> Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `facets` em vez de `facet`. Além disso, especificá-la como uma matriz JSON de cadeias, onde cada cadeia é uma expressão de faceta separado.
> 
> 

`$filter=[string]`(opcional) - uma expressão de pesquisa estruturados na sintaxe de OData padrão.

> [!NOTE]
> Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `filter` em vez de `$filter`.
> 
> 

`highlight=[string]`(opcional) - realça um conjunto de nomes de campos de valores separados por vírgulas utilizada para acessos. Apenas `searchable` campos podem ser utilizados para acessos realce.

`highlightPreTag=[string]`(opcional, será assumida demasiado`<em>`) - uma tag prepends toohit destaques de cadeia. Tem de ser definido com `highlightPostTag`.

> [!NOTE]
> Quando chamar **pesquisa** utilizar GET, carateres reservados no URL Olá tem de ser codificado por cento (por exemplo, % 23 em vez de #).
> 
> 

`highlightPostTag=[string]`(opcional, será assumida demasiado`</em>`)-uma tag de cadeia que acrescenta toohit destaques. Tem de ser definido com `highlightPreTag`.

> [!NOTE]
> Quando chamar **pesquisa** utilizar GET, carateres reservados no URL Olá tem de ser codificado por cento (por exemplo, % 23 em vez de #).
> 
> 

`scoringProfile=[string]`(opcional) - Olá nome de um tooevaluate de perfil de classificação de corresponder ao pontuações das classificações para documentos correspondentes nos resultados da ordem toosort Olá.

`scoringParameter=[string]`(zero ou mais) - indica Olá os valores para cada parâmetro definido numa função de classificação (por exemplo, `referencePointParameter`) utilizando o formato de Olá `name-value1,value2,...`.

* Por exemplo, se o perfil de classificação de Olá define uma função com um parâmetro denominado "mylocation" a opção de cadeia de consulta Olá seria `&scoringParameter=mylocation--122.2,44.8`. Traço primeiro Olá separa o nome de Olá na lista de valor de Olá, enquanto dash segundo Olá faz parte de Olá o primeiro valor (longitude neste exemplo).
* Para os parâmetros de classificação como etiqueta de os aumentos que podem conter vírgulas, pode terminar quaisquer esses valores na lista de Olá utilizando plicas. Se os valores de Olá próprios contenham plicas, pode transformá-los por duplicando.
  * Por exemplo, se tiver uma etiqueta os aumentos parâmetro denominado "mytag" e quiser tooboost na tag de Olá valores "Olá, O'Brien" e "Santos", consulta Olá a opção de cadeia seria `&scoringParameter=mytag-'Hello, O''Brien',Smith`. Tenha em atenção que as aspas são apenas necessários para valores com vírgulas.

> [!NOTE]
> Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `scoringParameters` em vez de `scoringParameter`. Além disso, pode especificá-la como uma matriz JSON de cadeias, onde cada cadeia é um separado `name-values` par.
> 
> 

`minimumCoverage`(opcional, será assumida too100) - um número entre 0 e 100 que indica a percentagem de Olá do índice de Olá que deve ser abrangida por uma consulta de pesquisa por ordem para Olá consulta toobe reportados como concluído com êxito. Por predefinição, índice completo Olá tem de estar disponível ou `Search` irá devolver um código de estado HTTP 503. Se definir `minimumCoverage` e `Search` for bem sucedida, irá devolver HTTP 200 e incluir um `@search.coverage` valor na resposta Olá que indica a percentagem de Olá do índice de Olá que foi incluído numa consulta de Olá.

> [!NOTE]
> Definir este valor do parâmetro tooa menor do que 100 pode ser útil para garantir a disponibilidade de pesquisa, mesmo para serviços com apenas uma réplica. No entanto, nem todos os documentos correspondentes garantidos toobe presente nos resultados de pesquisa de Olá. Se devolução de chamada de pesquisa é mais importante tooyour aplicação que a disponibilidade, em seguida, é melhor tooleave `minimumCoverage` no valor predefinido de 100.
> 
> 

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

Nota: Para esta operação, Olá `api-version` está especificado como um parâmetro de consulta no URL Olá independentemente se chamar **pesquisa** com GET ou POST.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o URL do serviço tooyour exclusivo. Olá **pesquisa** pedido pode especificar uma chave de administrador ou de uma chave de consulta para `api-key`.

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

Para o GET: nenhuma.

Para o POST:

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**Continuação de respostas de uma pesquisa parcial**

Por vezes, pesquisa do Azure não pode devolver que todos os Olá resultados pedidos numa única resposta pesquisa. Isto pode acontecer por diferentes motivos como, por exemplo, quando consulta Olá solicita documentos demasiados especificando não `$top` ou especificando um valor para `$top` que é demasiado grande. Nestes casos, a Azure Search incluirá Olá `@odata.nextLink` anotação no corpo de resposta de Olá e também `@search.nextPageParameters` se era um pedido POST. Pode utilizar valores Olá estes tooformulate anotações outra pesquisa pedido tooget Olá seguinte parte da resposta de pesquisa de Olá. Esta opção é denominada uma ***continuação*** de pedido de pesquisa original Olá e Olá anotações são geralmente denominadas ***tokens de continuação***. Consulte [exemplo Olá abaixo](#SearchResponse) para obter detalhes sobre a sintaxe de Olá estes anotações e em que aparecem no corpo da resposta Olá. 

por motivos de Olá por que motivo da Azure Search poderá devolver tokens de continuação são específicos da implementação e assunto do toochange. Os clientes robustos devem ser sempre toohandle pronto casos em que são devolvidos menos documentos que o esperado e um token de continuação é incluído toocontinue obter documentos. Também em atenção que tem de utilizar Olá mesmo método HTTP como o pedido original de Olá na ordem toocontinue. Por exemplo, se enviar um pedido GET, quaisquer pedidos de continuação enviar também tem de utilizar GET (e da mesma forma para o POST).

<a name="SearchResponse"></a>
**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**Exemplos:**

Pode encontrar exemplos adicionais no Olá [OData sintaxe de expressão para a Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) página.

1)    Procure Olá descendente do índice ordenado por data.

    GET /indexes/hotels/docs? pesquisa = * & $orderby = lastRenovationDate desc & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "*", "orderby": "lastRenovationDate desc"}

2)    Uma pesquisa por facetas pesquisar o índice de Olá e obter as facetas de categorias, classificação, etiquetas, bem como itens com baseRate em intervalos específicos:

    GET /indexes/hotels/docs? pesquisa = teste & aspeto = categoria & aspeto = classificação & aspeto = etiquetas & aspeto = baseRate, valores: 80 | 150 | 220 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "teste", "facetas": ["categoria", "classificação", "etiquetas", "baseRate, valores: 80 | 150 | 220"]}

3)    Utilizando um filtro, restringir os resultados da consulta por facetas anterior Olá depois Olá utilizador clica na classificação 3 e a categoria "Hotel":

    GET /indexes/hotels/docs? pesquisa = teste & aspeto = etiquetas & aspeto = baseRate, valores: 80 | 150 | 220 & $filter = classificação eq 3 e categoria eq 'hotel' & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "teste", "facetas": ["etiquetas", "baseRate, valores: 80 | 150 | 220"], "filtro": "classificação eq 3 e categoria eq"Motel""}

4) Numa pesquisa por facetas, defina um limite superior em termos exclusivos devolvidos numa consulta. Olá predefinição é 10, mas pode aumentar ou diminuir este valor utilizando Olá `count` parâmetro no Olá `facet` atributo:

    GET /indexes/hotels/docs? pesquisa = teste & aspeto = cidade, contagem: 5 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "teste", "facetas": ["Cidade, contagem: 5"]}

5)    Procurar Olá índice dentro de campos específicos; Por exemplo, um campo específicas do idioma:

    GET /indexes/hotels/docs? pesquisa = hôtel & searchFields = description_fr & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "hôtel", "searchFields": "description_fr"}

6) Olá índice através de vários campos de pesquisa. Por exemplo, pode armazenar e campos pesquisáveis de consulta em vários idiomas, tudo dentro Olá mesmo índice.  Se as descrições inglês e francês coexistem na Olá mesmo documento, pode devolver quaisquer ou todas as Olá em resultados de consulta:

    GET /indexes/hotels/docs? pesquisa = átrios & searchFields = descrição, description_fr & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "átrios", "searchFields": "descrição, description_fr"}

Tenha em atenção que apenas pode consultar um índice numa altura. Não crie vários índices para cada idioma, a menos que planeia tooquery um cada vez.

7)    A paginação - página de 1ª Olá Get de itens (o tamanho da página é 10):

    GET /indexes/hotels/docs? pesquisa = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "*", "Ignorar": 0, "superior": 10}

8)    A paginação - página de 2nd Olá Get de itens (o tamanho da página é 10):

    GET /indexes/hotels/docs? pesquisa = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "*", "Ignorar": "superior", 10: 10}

9)    Obter um conjunto específico de campos:

    GET /indexes/hotels/docs? pesquisa = * & $select = hotelName, a descrição e a api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "*", "select": "hotelName, descrição"}

10)  Obter documentos correspondente a uma expressão de filtro específico:

    GET /indexes/hotels/docs? $filter = (baseRate ge 60 e baseRate lt 300) ou eq hotelName 'Permaneça Fancy' & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"filtro": "(baseRate ge 60 e baseRate lt 300) ou hotelName eq 'Fancy mantenha-se'"}

11) Índice de pesquisa do Olá e retorno fragmentos com destaques acessos

    GET /indexes/hotels/docs? pesquisa = algo & Realce = descrição & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "algo", "highlight": "Descrição"}

12) Índice de pesquisa do Olá e retorno documentos ordenados do próximo toofarther na direção oposta a uma localização de referência

    GET /indexes/hotels/docs? pesquisa = algo & $orderby=geo.distance (localização, geography'POINT(-122.12315 47.88121)') & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "algo", "orderby": "geo.distance (localização, geography'POINT(-122.12315 47.88121)')"}

13) Pesquisa Olá índice pressuposto de que existe é um perfil de classificação chamado "georreplicação" com duas funções de pontuação de distância, uma definição de um parâmetro denominado "currentLocation" e uma definição de um parâmetro denominado "lastLocation"

    GET /indexes/hotels/docs? pesquisa = algo & scoringProfile = georreplicação & scoringParameter = currentLocation – 122.123,44.77233 & scoringParameter = lastLocation – 121.499,44.2113 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "algo", "scoringProfile": "georreplicação", "scoringParameters": ["currentLocation – 122.123,44.77233", "lastLocation – 121.499,44.2113"]}

14) Localizar documentos no Olá índice utilizando [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx). Esta consulta devolve hotéis onde os campos pesquisáveis contenham Olá termos "comfort" e "localização" mas não "hotel":

    GET /indexes/hotels/docs? pesquisa = comfort + localização-hotel & searchMode = all & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "comfort + localização-motel", "searchMode": "all"}

Tenha em atenção a utilização de Olá de `searchMode=all` acima. Incluindo este parâmetro substitui a predefinição Olá `searchMode=any`, garantindo que que `-motel` significa "E não" em vez de "Ou NOT". Sem `searchMode=all`, obter "Ou NOT" que expande em vez de restringe os resultados da pesquisa e isto pode ser counter-intuitive toosome utilizadores.

15) Localizar documentos no Olá índice utilizando [consulta lucene](https://msdn.microsoft.com/library/mt589323.aspx). Esta consulta devolve hotéis em que o campo de categoria Olá contém termo Olá "orçamento" e pesquisáveis todos os campos que contém o frase Olá "recentemente renovated". Documentos que contém o frase Olá "recentemente renovated" estão ordenados superior, como resultado do valor de aumento Olá termo (3)

    GET /indexes/hotels/docs? pesquisa = categoria: orçamento e \"recentemente renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Preview & querytype = completa

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "categoria: orçamento e \"recentemente renovated\"^ 3", "queryType": "completa", "searchMode": "all"}

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>Documento de pesquisa
Olá **pesquisa documento** operação obtém um documento de pesquisa do Azure. Isto é útil quando um utilizador clica num resultado de pesquisa específica, e pretender toolook segurança detalhes específicos sobre esse documento.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**Pedido**

HTTPS é necessário para pedidos de serviço. Olá **pesquisa documento** pedido pode ser construído a forma.

    GET /indexes/[index name]/docs/key?[query parameters]

Em alternativa, pode utilizar a sintaxe de OData tradicional Olá para pesquisa de chave:

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

pedido de Olá URI inclui um [nome do índice] e [chave], especificando que tooretrieve de documento de que o índice. Só pode obter um documento a uma hora. Utilize **pesquisa** tooget vários documentos num único pedido.

**Parâmetros de consulta**

`$select=[string]`(opcional) - uma lista de campos de valores separados por vírgulas tooretrieve. Se não especificados ou definido demasiado`*`, todos os campos marcados como recuperável no esquema Olá estão incluídos na projecção de Olá.

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

Nota: Para esta operação, Olá `api-version` está especificado como um parâmetro de consulta.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o URL do serviço tooyour exclusivo. Olá **pesquisa documento** pedido pode especificar uma chave de administrador ou de uma chave de consulta para `api-key`.

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

nenhum.

**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**Exemplo**

Documento de Olá de pesquisa que tenha a chave '2'

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

Documento de Olá de pesquisa que tenha a chave "3" utilizando a sintaxe de OData:

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>Contagem de documentos
Olá **contagem de documentos** operação obtém uma contagem do número de Olá dos documentos num índice de pesquisa. Olá `$count` sintaxe faz parte de Olá protocolo OData.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**Pedido**

HTTPS é necessário para pedidos de serviço. Olá **contagem de documentos** pedido pode ser construído com o método GET de Olá.

Olá [nome do índice] no URI de pedido de Olá indica Olá serviço tooreturn uma contagem de todos os itens na coleção de documentos Olá do índice especificado Olá.

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.

* `Accept`: Este valor tem de ser definido demasiado`text/plain`.
* `api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o URL do serviço tooyour exclusivo. Olá **contagem de documentos** pedido pode especificar uma chave de administrador ou de uma chave de consulta para `api-key`.

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

nenhum.

**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

corpo da resposta Olá contém o valor de contagem de Olá como um número inteiro a formatados em texto simples.

<a name="Suggestions"></a>

## <a name="suggestions"></a>Sugestões
Olá **sugestões** operação obtém sugestões com base na entrada de uma pesquisa parcial. Este é normalmente utilizado em sugestões antecipada do tooprovide de caixas de pesquisa, como os utilizadores são introduzir termos de pesquisa.

Sugestão pedidos têm como objetivo em sugerindo documentos de destino, para que Olá sugerida texto pode ser repetido se correspondem a vários documentos candidato Olá mesmo procurar entrada. Pode utilizar `$select` tooretrieve outro campos (incluindo a chave do documento Olá) de documentos para que pode indicar que o documento é origem Olá para cada sugestão.

A **sugestões** operação é emitida como um pedido GET ou POST.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Quando publicar toouse em vez de obter**

Quando utiliza HTTP GET Olá de toocall **sugestões** API, terá de toobe em atenção de que o comprimento do URL de pedido de Olá Olá não pode exceder os 8 KB. Isto é normalmente suficiente para a maioria das aplicações. No entanto, algumas aplicações produzem consultas muito grande, especificamente expressões de filtro de OData. Para estas aplicações, utilizando o HTTP POST é uma melhor opção porque permite filtros maior do que o GET. Com o POST, número de Olá de cláusulas num filtro de fator restritivo Olá, não Olá tamanho da cadeia de filtro em bruto de Olá, uma vez que o limite de tamanho do pedido de Olá para o POST é aproximadamente 16 MB.

> [!NOTE]
> Apesar do limite de tamanho de pedido POST Olá é muito grande, expressões de filtro não podem ser arbitrariamente complexas. Consulte [sintaxe de expressão de OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre as limitações de complexidade de filtro.
> 
> 

**Pedido**

HTTPS é necessário para pedidos de serviço. Olá **sugestões** pedido pode ser construído com Olá GET ou métodos POST.

URI de pedido de Olá Especifica o nome Olá Olá índice tooquery. Parâmetros, tais como o termo de pesquisa parcialmente entrada de Olá, estão especificados na cadeia de consulta Olá no caso de Olá de pedidos GET e no pedido de Olá os pedidos de corpo no caso de Olá da publicação.

Como melhor prática quando criar pedidos GET, lembre-se demasiado[codificar o URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específicas Olá de parâmetros durante a chamada de REST API diretamente. Para **sugestões** operações, isto inclui:

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

Codificação do URL só é recomendada Olá acima parâmetros de consulta. Se lhe codificar inadvertidamente URL hello cadeia de consulta completo (tudo após Olá?), irão interromper a pedidos.

Além disso, a codificação de URL é necessário apenas quando chamar Olá obter a API de REST diretamente utilizando. Sem codificação do URL é necessário quando chamar **sugestões** utilização do POST, ou ao utilizar Olá [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que processa a codificação do URL para si.

**Parâmetros de consulta**

**Sugestões** aceita vários parâmetros que fornecem critérios de consulta e também especificam o comportamento de procura. Terá de fornecer estes parâmetros no URL Olá cadeia de consulta ao chamar **sugestões** via GET e como as propriedades de JSON no corpo do pedido de Olá ao chamar **sugestões** através de POST. sintaxe de Olá para alguns parâmetros é ligeiramente diferente entre GET e POST. Estas diferenças são assinaladas como aplicável abaixo:

`search=[string]`-Olá consultas de toosuggest de toouse de texto de pesquisa. Tem de ser, pelo menos, 1 caráter e não mais do que 100 carateres.

`highlightPreTag=[string]`(opcional) - uma tag de cadeia que prepends toosearch pedidos. Tem de ser definido com `highlightPostTag`.

> [!NOTE]
> Quando chamar **sugestões** utilizar GET, carateres reservados no URL Olá tem de ser codificado por cento (por exemplo, % 23 em vez de #).
> 
> 

`highlightPostTag=[string]`(opcional) - uma tag de cadeia que acrescenta toosearch pedidos. Tem de ser definido com `highlightPreTag`.

> [!NOTE]
> Quando chamar **sugestões** utilizar GET, carateres reservados no URL Olá tem de ser codificado por cento (por exemplo, % 23 em vez de #).
> 
> 

`suggesterName=[string]`-nome de Olá do sugestor Olá como especificado no Olá `suggesters` coleção que faz parte da definição do índice Olá. A `suggester` determina os campos são analisados relativamente a termos de sugestões de consulta. Consulte [dos Sugestores](#Suggesters) para obter mais detalhes.

`fuzzy=[boolean]`(predefinido opcional, = false)-configurar quando o tootrue esta API irá encontrar sugestões, mesmo se existir um caráter substituído ou em falta no texto de pesquisa de Olá. Embora Isto proporciona uma melhor experiência em alguns cenários vem num desempenho de custos como sugestão difusa pesquisas são mais lentas e consumam mais recursos.

`searchFields=[string]`(opcional) - lista de Olá de toosearch de nomes de campo de valores separados por vírgulas para Olá especificado texto de pesquisa. Campos de destino tem de estar ativados para sugestões.

`$top=#`(opcional, predefinição = 5)-Olá diversas tooretrieve de sugestões. Tem de ser um número entre 1 e 100.

> [!NOTE]
> Quando chamar **sugestões** utilização do POST, este parâmetro é denominado `top` em vez de `$top`.
> 
> 

`$filter=[string]`(opcional) - uma expressão que filtra documentos Olá considerados para sugestões.

> [!NOTE]
> Quando chamar **sugestões** utilização do POST, este parâmetro é denominado `filter` em vez de `$filter`.
> 
> 

`$orderby=[string]`(opcional) - uma lista de expressões de valores separados por vírgulas toosort Olá resultados por. Cada expressão pode ser um nome de campo ou uma chamada toohello `geo.distance()` função. Cada expressão pode ser seguido `asc` tooindicated ascendente, e `desc` tooindicate descendente. é por ordem ascendente predefinido Olá. Há um limite de 32 cláusulas para `$orderby`.

> [!NOTE]
> Quando chamar **sugestões** utilização do POST, este parâmetro é denominado `orderby` em vez de `$orderby`.
> 
> 

`$select=[string]`(opcional) - uma lista de campos de valores separados por vírgulas tooretrieve. Se não for indicado, Olá apenas a chave do documento e o texto de sugestão é devolvido. Pode pedir explicitamente todos os campos definindo este parâmetro demasiado`*`.

> [!NOTE]
> Quando chamar **sugestões** utilização do POST, este parâmetro é denominado `select` em vez de `$select`.
> 
> 

`minimumCoverage`(opcional, será assumida too80) - um número entre 0 e 100 que indica a percentagem de Olá do índice de Olá que deve ser abrangida por uma consulta de sugestões por ordem para Olá consulta toobe reportados como concluído com êxito. Por predefinição, pelo menos 80% de índice de Olá tem de estar disponível ou `Suggest` irá devolver um código de estado HTTP 503. Se definir `minimumCoverage` e `Suggest` for bem sucedida, irá devolver HTTP 200 e incluir um `@search.coverage` valor na resposta Olá que indica a percentagem de Olá do índice de Olá que foi incluído numa consulta de Olá.

> [!NOTE]
> Definir este valor do parâmetro tooa menor do que 100 pode ser útil para garantir a disponibilidade de pesquisa, mesmo para serviços com apenas uma réplica. No entanto, nem todas as sugestões correspondentes garantidos toobe presente nos resultados de Olá. Se a devolução de chamada é mais importante tooyour aplicação, a disponibilidade, então o respetivo melhores não toolower `minimumCoverage` abaixo o valor predefinido 80.
> 
> 

`api-version=[string]`(obrigatório). versão de pré-visualização Olá é `api-version=2015-02-28-Preview`. Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

Nota: Para esta operação, Olá `api-version` está especificado como um parâmetro de consulta no URL Olá independentemente se chamar **sugestões** com GET ou POST.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional

* `api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o URL do serviço tooyour exclusivo. Olá **sugestões** pedido pode especificar uma chave de administrador ou de uma chave de consulta como Olá `api-key`.

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure. Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

**Corpo do pedido**

Para o GET: nenhuma.

Para o POST:

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Se a opção de projeção Olá é utilizado tooretrieve campos estiverem incluídas em cada elemento da matriz de Olá:

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**Exemplo**

Obter 5 sugestões em que a entrada de uma pesquisa parcial Olá é 'lux'

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
