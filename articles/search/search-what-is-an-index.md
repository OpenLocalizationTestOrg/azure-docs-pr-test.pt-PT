---
title: "aaaCreate um índice da Azure Search | Microsoft Azure | Serviço de pesquisa de nuvem alojada"
description: "O que é um índice da Azure Search e como é utilizado?"
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>Criar um índice da Azure Search
> [!div class="op_single_selector"]
> * [Descrição geral](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>O que é um índice?
Um *índice* é um arquivo persistente de *documentos* e outras construções utilizado por um serviço Azure Search. Um documento é uma unidade de dados pesquisáveis no índice. Por exemplo, um retalhista de comércio eletrónico pode ter um documento para cada artigo que vende, uma empresa jornalística pode ter um documento para cada artigo, etc. Mapeamento equivalentes de base de dados familiar estes conceitos toomore: um *índice* é, conceptualmente, semelhante tooa *tabela*, e *documentos* são quase equivalentes demasiado*linhas* numa tabela.

Quando lhe adiciona/carrega documentos e submeter consultas de pesquisa tooAzure pesquisa, submeter o índice de específica de tooa pedidos no serviço de pesquisa.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Tipos de campo e atributos num índice da Azure Search
Como definir o esquema, tem de especificar o nome Olá, tipo e atributos de cada campo no seu índice. tipo de campo Olá classifica os dados de Olá armazenados nesse campo. Os atributos são definidos em campos individuais toospecify como o campo de Olá é utilizado. Olá tabelas seguintes enumeram os tipos de Olá e atributos que pode especificar.

### <a name="field-types"></a>Tipos de campo
| Tipo | Descrição |
| --- | --- |
| *Edm.String* |Texto que pode, opcionalmente, ser atomizado para pesquisa em texto completo (separação de palavras, lematização, etc.). |
| *Collection(Edm.String)* |Uma lista de cadeias que pode, opcionalmente, ser atomizada para pesquisa em texto completo. Não existe nenhum limite superior teórico do número de Olá de itens numa coleção, mas limite superior de 16 MB Olá tamanho de payload aplica-se toocollections. |
| *Edm.Boolean* |Contém valores verdadeiro/falso. |
| *Edm.Int32* |Valores inteiros de 32 bits. |
| *Edm.Int64* |Valores inteiros de 64 bits. |
| *Edm.Double* |Dados numéricos de dupla precisão. |
| *Edm.DateTimeOffset* |Data de valores de hora representados no formato de Olá OData V4 (por exemplo, `yyyy-MM-ddTHH:mm:ss.fffZ` ou `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Um ponto que representa uma localização geográfica no globo Olá. |

Pode encontrar mais informações detalhadas sobre os [tipos de dados suportados aqui](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) do Azure Search.

### <a name="field-attributes"></a>Atributos do campo
| Atributo | Descrição |
| --- | --- |
| *Chave* |Uma cadeia que fornece Olá ID exclusivo de cada documento, utilizada para procura de documentos. Todos os índices devem ter uma chave. Apenas um campo pode ser chave Olá e o tipo tem de ser definido tooEdm.String. |
| *Recuperável* |Especifica se um campo pode ser devolvido num resultado da pesquisa. |
| *Filtrável* |Permite Olá campo toobe utilizado nas consultas de filtro. |
| *Ordenável* |Permite a uma consulta os resultados da pesquisa toosort através deste campo. |
| *Facetável* |Permite que um toobe campo utilizado um [navegação por facetas](search-faceted-navigation.md) estrutura para o utilizador auto-direcionada filtragem. Normalmente, os campos com valores repetitivos que pode utilizar toogroup em conjunto de vários documentos (por exemplo, vários documentos abrangidos numa única marca ou categoria de serviço) funcionam melhor como facetas. |
| *Pesquisável* |Marcas de escala Olá campo como pesquisável de texto completo. |

Pode encontrar mais informações detalhadas sobre os [atributos de índice aqui](https://docs.microsoft.com/rest/api/searchservice/Create-Index) do Azure Search.

## <a name="guidance-for-defining-an-index-schema"></a>Orientações para definir um esquema de índice
Como a criação do índice, reserve tempo na Olá planeamento fase toothink cada decisão. É importante que tenha suas necessidades de negócio e experiência de utilizador do pesquisa em consideração quando conceber o seu índice como cada campo tem de ser atribuído Olá [atributos adequados](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Alteração de um índice após a respetiva implementação implica reconstruir e recarregar os dados de Olá.

Caso os requisitos de armazenamento de dados alterem ao longo do tempo, pode aumentar ou diminuir a capacidade adicionando ou removendo partições. Para obter detalhes, consulte [Gerir o serviço de Pesquisa no Azure](search-manage.md) ou [Limites de Serviço](search-limits-quotas-capacity.md).

