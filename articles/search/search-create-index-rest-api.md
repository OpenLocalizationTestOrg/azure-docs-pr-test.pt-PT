---
title: "AAA \"Criar um índice (API REST - pesquisa do Azure) | Microsoft Docs\""
description: "Crie um índice no código utilizando Olá API REST da Azure Search HTTP."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Criar um índice da Azure Search utilizando Olá REST API
> [!div class="op_single_selector"]
>
> * [Descrição geral](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

Este artigo irá guiá-lo através do processo de Olá de criação de uma pesquisa do Azure [índice](https://docs.microsoft.com/rest/api/searchservice/Create-Index) utilizando Olá API REST da Azure Search.

Antes de consultar este guia e criar um índice, deverá já ter [criado um serviço Azure Search](search-create-service-portal.md).

toocreate um índice da Azure Search utilizando Olá REST API, irá emitir um único HTTP POST pedido tooyour da Azure Search URL ponto final do serviço. A definição de índice ficarão contida no corpo do pedido de Olá como o conteúdo JSON corretamente formado.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificar a sua chave de API do administrador do serviço Azure Search
Agora que aprovisionou um serviço da Azure Search, pode emitir pedidos HTTP contra o ponto de final do URL do seu serviço utilizando Olá REST API. *Todos os* pedidos de API tem de incluir Olá-chave de api que foi gerada para Olá serviço de pesquisa que aprovisionou. Ter uma chave válida estabelece fidedignidade, numa base por pedido, entre pedido de Olá envio aplicação Olá e serviço Olá que o processa.

1. toofind tem de iniciar sessão em Olá a chaves do serviço de api [portal do Azure](https://portal.azure.com/)
2. Painel do serviço de pesquisa do Azure aceda tooyour
3. Clique em Olá ícone "Chaves"

O seu serviço terá *chaves de administração* e *chaves de consulta*.

* Os principais e secundários *chaves de administração* conceder direitos totais tooall operações, incluindo o serviço do Olá capacidade toomanage Olá, criar e eliminar índices, indexadores e origens de dados. Existem duas chaves para que possa continuar chave secundária do toouse Olá se decidir chave primária do tooregenerate Olá e vice-versa.
* O *chaves de consulta* conceder acesso só de leitura tooindexes e os documentos e são normalmente distribuída tooclient aplicações emitem pedidos de pesquisa.

Para efeitos de Olá de criação de um índice, pode utilizar tanto a chave de administrador principal ou secundário.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Definir o seu índice da Azure Search utilizando JSON corretamente formado
Um único serviço de tooyour de pedido de HTTP POST irá criar o índice. corpo de Olá do seu pedido de HTTP POST irá conter um único objeto JSON que define o índice da Azure Search.

1. Olá primeira propriedade deste objeto JSON é o nome de Olá do seu índice.
2. Olá segunda propriedade deste objeto JSON é uma matriz JSON com o nome `fields` que contenha um objeto JSON separado para cada campo no seu índice. Cada um destes objetos JSON contém vários pares nome/valor para cada um dos atributos do campo de Olá, incluindo "nome", "tipo", etc.

É importante que tenha suas necessidades de negócio e experiência de utilizador do pesquisa em consideração quando conceber o seu índice como cada campo tem de ser atribuído Olá [atributos adequados](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Estes atributos estabelecem quais as funcionalidades (filtragem, facetamento, ordenação de pesquisa de texto completo, etc.) de pesquisa aplicar toowhich campos. Qualquer atributo que não for especificado, a predefinição de Olá será funcionalidade de pesquisa correspondente do tooenable Olá, a menos que a desative especificamente.

Para o nosso exemplo, atribuímos o nome "hotéis" ao nosso índice e definimos os nossos campos do seguinte modo:

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

Escolhemos cuidadosamente os atributos de índice de Olá para cada campo com base na forma como acreditamos que serão utilizados numa aplicação. Por exemplo, `hotelId` é uma chave exclusiva que as pessoas que procuram hotéis provavelmente não conhecem, desta forma, desativamos a pesquisa em texto completo para esse campo através da definição `searchable` demasiado`false`, que poupa espaço no índice Olá.

Tenha em atenção que exatamente um campo no seu índice do tipo `Edm.String` tem de ser Olá designada como campo de 'key' Olá.

definição de índice de Olá acima utiliza um analisador de idioma para Olá `description_fr` campo porque se trata de texto em francês toostore pretendido. Consulte [tópico de suporte de idioma Olá](https://docs.microsoft.com/rest/api/searchservice/Language-support) , bem como Olá correspondente [blogue](https://azure.microsoft.com/blog/language-support-in-azure-search/) para obter mais informações sobre analisadores de idiomas.

## <a name="issue-hello-http-request"></a>Pedido de Olá HTTP do problema
1. Utilizar a definição de índice como corpo do pedido Olá, emita um URL de ponto final de serviço do HTTP POST pedido tooyour da Azure Search. No URL Olá, ser toouse se o nome do serviço como nome do anfitrião Olá e colocar Olá adequada `api-version` como um parâmetro de cadeia de consulta (Olá versão de API atual é `2016-09-01` momento Olá de publicação deste documento).
2. Nos cabeçalhos de pedido de Olá, especifique Olá `Content-Type` como `application/json`. Também terá de tooprovide chave de administrador do seu serviço que identificou no passo I no Olá `api-key` cabeçalho.

Terá tooprovide o seus próprios nome e a api tooissue chave Olá pedido de serviço abaixo:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Para um pedido com êxito, deve ver o código de estado 201 (Criado). Para obter mais informações sobre como criar um índice através de Olá REST API, visite Olá [referência da API aqui](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Para obter mais informações sobre outros códigos de estado HTTP que possam ser devolvidos em caso de falha, consulte [Códigos de estado HTTP (Pesquisa do Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

Quando tiver terminado com um índice e pretender toodelete-lo, emita apenas um pedido de eliminação HTTP. Por exemplo, trata-se como podemos seria eliminar o índice "Hotéis" de Olá:

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Passos seguintes
Depois de criar um índice da Azure Search, estará pronto demasiado[carregar o conteúdo para o índice de Olá](search-what-is-data-import.md) para que possa começar a pesquisar os seus dados.
