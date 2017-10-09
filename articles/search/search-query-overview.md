---
title: "aaaQuery de índice da Azure Search | Microsoft Docs"
description: "Crie uma consulta de pesquisa na Azure search e utilize a pesquisa parâmetros toofilter e ordenar os resultados da pesquisa."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Consultar o índice da Azure Search
> [!div class="op_single_selector"]
> * [Descrição geral](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Ao submeter pedidos de pesquisa tooAzure pesquisa, existem vários parâmetros que podem ser especificados em conjunto com as palavras reais Olá que são escritas na caixa de pesquisa de Olá da sua aplicação. Estes parâmetros de consulta permitem-lhe tooachieve um maior controlo dos Olá [experiência de pesquisa de texto completo](search-lucene-query-architecture.md).

Segue-se uma lista que explica resumidamente as utilizações comuns dos parâmetros de consulta Olá na Azure Search. Para a cobertura total dos parâmetros de consulta e o respetivo comportamento, consulte Olá detalhadas páginas para Olá [REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) e [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary).

## <a name="types-of-queries"></a>Tipos de consultas
A Azure Search oferece muitas consultas extremamente poderosas de toocreate opções. Olá dois tipos principais de consulta que irá utilizar são `search` e `filter`. A `search` consultar pesquisa um ou mais termos em todos os *pesquisável* campos no seu índice e funciona de forma Olá que seria de esperar um motor de busca como toowork Google ou do Bing. Uma consulta `filter` avalia uma expressão booleana através de todos os campos *filtráveis* num índice. Ao contrário `search` consultas, `filter` consultas correspondem aos conteúdos exatos de Olá de um campo, o que significa que são maiúsculas e minúsculas para campos de cadeia.

Pode utilizar as pesquisas e os filtros em conjunto ou separadamente. Se utilizar o-los em conjunto, o filtro de Olá é aplicada primeiro toohello índice completo e, em seguida, procura Olá é executada nos resultados de Olá do filtro de Olá. Os filtros, por conseguinte, podem ser um desempenho de consulta de tooimprove técnica útil desde que reduzem o conjunto de Olá de documentos que Olá tooprocess de necessidades de consulta de pesquisa.

sintaxe de Olá para expressões de filtro é um subconjunto de Olá [idioma do filtro de OData](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search). Para consultas de pesquisa pode utilizar qualquer um dos Olá [sintaxe simplificada](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) ou Olá [consulta lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) abordadas a seguir.

### <a name="simple-query-syntax"></a>Sintaxe de consulta simples
Olá [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) é o idioma de consulta Olá predefinido utilizado na Azure Search. sintaxe de consulta simples Olá suporta vários operadores de pesquisa comuns, incluindo Olá AND, OR, não, frase, sufixo e operadores de precedência.

### <a name="lucene-query-syntax"></a>Sintaxe de consulta Lucene
Olá [consulta lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) permite-lhe Olá toouse amplamente adotado e idioma de consulta expressivas desenvolvido como parte do [Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

Utilizando esta sintaxe de consulta permite-lhe tooeasily alcançar Olá seguintes capacidades: [consultas de âmbito de campo](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [pesquisa difusa](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [pesquisa de proximidade](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ termo aumento](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [pesquisa de expressão regular](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [pesquisa com carateres universais](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [Noções básicas de sintaxe](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), e [consulta a utilizar operadores booleanos](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean).

## <a name="ordering-results"></a>Ordenar resultados
Ao receber os resultados para uma consulta de pesquisa, pode pedir que da Azure Search serve os resultados de Olá ordenados pelos valores num campo específico. Por predefinição, a Azure Search ordena os resultados da pesquisa Olá com base na classificação de Olá de pontuação de pesquisa de cada documento, que é derivada de [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).

Se pretender que os resultados ordenados por um valor diferente de pontuação de pesquisa de Olá de tooreturn de pesquisa do Azure, pode utilizar Olá `orderby` parâmetro de pesquisa. Pode especificar o valor Olá Olá `orderby` os nomes de campo de tooinclude de parâmetro e chama toohello [ `geo.distance()` função](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) para valores geoespaciais. Cada expressão pode ser seguido `asc` tooindicate que os resultados foram pedidos por ordem ascendente e `desc` tooindicate que os resultados foram pedidos por ordem descendente. Olá predefinido ordem ascendente de classificação.

## <a name="paging"></a>Paginação
A pesquisa do Azure torna mais fácil tooimplement paginação dos resultados da pesquisa. Ao utilizar Olá `top` e `skip` parâmetros, facilmente pode emitir pedidos de pesquisa que permitem-lhe tooreceive conjunto total de Olá dos resultados da pesquisa em subconjuntos geríveis e ordenados que permitem facilmente práticas da IU de pesquisa bom. Quando receber estas subconjuntos de resultados mais pequenos, também pode receber contagem Olá de documentos no conjunto total de Olá dos resultados da pesquisa.

Pode saber mais sobre a paginação os resultados da pesquisa no artigo Olá [como toopage pesquisa resulta na Azure Search](search-pagination-page-layout.md).

## <a name="hit-highlighting"></a>Detetor de ocorrências
Na Azure Search, que realçam parte exata de Olá dos resultados da pesquisa que correspondem à consulta de pesquisa de Olá é efetuada fácil utilizando Olá `highlight`, `highlightPreTag`, e `highlightPostTag` parâmetros. Pode especificar que *pesquisável* campos devem ter o respetivo texto com correspondência emphasized, bem como especificar devolve Olá exato cadeia etiquetas tooappend toohello início e fim de Olá de correspondência de texto que da Azure Search.

## <a name="try-out-query-syntax"></a>Experimente a sintaxe de consulta

diferenças de sintaxe para Olá melhor forma toounderstand é submeter consultas e rever os resultados.

+ Utilize [Explorador de pesquisa](search-explorer.md) no Olá portal do Azure. Ao implementar [índice de exemplo de Olá](search-get-started-portal.md), pode consultar o índice de Olá em minutos com ferramentas no portal de Olá.

+ Utilize [Fiddler](search-fiddler.md) ou o Chrome Postman toosubmit consultas tooan índice que carregou tooyour o serviço de pesquisa. Ambas as ferramentas de suportem de ponto final de REST chamadas tooan HTTP. 
