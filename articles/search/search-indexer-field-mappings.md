---
title: mapeamentos de aaaField na indexadores de pesquisa do Azure
description: "Configurar a Azure Search indexador campo mapeamentos tooaccount para diferenças na representações de dados e os nomes de campo"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Mapeamentos de campo na indexadores de pesquisa do Azure
Quando utilizar indexadores de pesquisa do Azure, pode encontrar sozinho ocasionalmente em situações em que os dados de entrada não bastante corresponde ao esquema Olá do seu índice de destino. Nesses casos, pode utilizar **campo mapeamentos** tootransform os dados em Olá pretendido forma.

Algumas situações em que os mapeamentos de campo são úteis:

* A origem de dados tem um campo `_id`, mas da Azure Search não permite que os nomes de campo começados por um caráter de sublinhado. Um mapeamento de campos permite demasiado "mudar o nome de" um campo.
* Pretende toopopulate vários campos no Olá índice com Olá dados, por exemplo de origem de dados mesmos porque pretende que os campos de toothose tooapply analisadores de diferentes. Mapeamentos de campo permitem-lhe "copiar" um campo da origem de dados.
* Terá de tooBase64 codificar ou descodificar os seus dados. Mapeamentos de campo suportam vários **mapeamento de funções**, incluindo funções para Base64 e codificação e descodificação.   

## <a name="setting-up-field-mappings"></a>Configurar os mapeamentos de campo
Pode adicionar mapeamentos de campo ao criar um indexador novo utilizando Olá [criar indexador](https://msdn.microsoft.com/library/azure/dn946899.aspx) API. Pode gerir os mapeamentos de campo num indexador indexação utilizando Olá [atualização indexador](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.

Um mapeamento de campo é composta por 3 partes:

1. A `sourceFieldName`, que representa um campo da sua origem de dados. Esta propriedade é necessária.
2. Opcional `targetFieldName`, que representa um campo no seu índice de pesquisa. Se for omitido, Olá o mesmo nome que aparece Olá origem de dados é utilizada.
3. Opcional `mappingFunction`, que podem transformar os seus dados através de um dos vários predefinidas funções. Olá lista completa de funções está [abaixo](#mappingFunctions).

Mapeamentos de campos são adicionados toohello `fieldMappings` matriz na definição de indexador Olá.

Por exemplo, eis como pode acomodar as diferenças nos nomes de campo:

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

Um indexador pode ter vários mapeamentos de campo. Por exemplo, eis o que pode "copiar" um campo:

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> A pesquisa do Azure utiliza comparação sensível tooresolve Olá campo função nomes e mapeamentos de campo. Isto é conveniente (não tiver tooget todos os Olá tem maiúsculas e minúsculas corretas), mas significa que a origem de dados ou o índice não pode ter campos que só diferem a maiúsculas e minúsculas.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>Funções de mapeamento de campo
Estas funções são atualmente suportadas:

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
Efetua *URL segura* codificação Base64 de Olá a cadeia de entrada. Assume que a entrada de Olá codificado UTF-8.

#### <a name="sample-use-case"></a>Caso de utilização de exemplo
Apenas carateres de URL seguro podem aparecer uma chave de documento de pesquisa do Azure (porque os clientes têm de ser capaz de tooaddress documento de Olá utilizando Olá API de pesquisa, por exemplo). Se os dados contém carateres não seguro URL e quiser toouse-toopopulate um campo de chave no seu índice de pesquisa, utilize esta função.   

#### <a name="example"></a>Exemplo
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Executa descodificação Base64 da cadeia de entrada Olá. Olá entrada é assumida tooa *URL segura* cadeia com codificação Base64.

#### <a name="sample-use-case"></a>Caso de utilização de exemplo
Os valores de metadados personalizados do blob tem de ser codificado-ASCII. Pode utilizar Base64 codificação toorepresent arbitrários cadeias Unicode nos metadados personalizados do blob. No entanto, a pesquisa de toomake significativa, pode utilizar estas função tooturn Olá codificado dados novamente nas cadeias "regulares" ao povoar o índice de pesquisa.  

#### <a name="example"></a>Exemplo
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Divisões um campo de cadeia utilizando Olá especificado delimitador e escolhe o token de Olá em Olá posição especificada na divisão resultante Olá.

Por exemplo, se hello entrada é `Jane Doe`, Olá `delimiter` é `" "`(espaço) e Olá `position` é 0, o resultado de Olá `Jane`; se hello `position` é 1, resultado Olá é `Doe`. Se a posição de Olá refere-se o token de tooa que não existe, será devolvido um erro.

#### <a name="sample-use-case"></a>Caso de utilização de exemplo
A origem de dados contém um `PersonName` campo e pretender que tooindex-o como dois separado `FirstName` e `LastName` campos. Pode utilizar este Olá toosplit de função utilizando o caráter de espaço de Olá conforme Olá delimitador de entrada.

#### <a name="parameters"></a>Parâmetros
* `delimiter`: um toouse de cadeia como separador Olá quando dividir Olá a cadeia de entrada.
* `position`: uma posição baseada em zero de número inteiro de Olá toopick token após a cadeia de entrada de Olá é dividida.    

#### <a name="example"></a>Exemplo
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
Transformações de uma cadeia formatada como uma matriz JSON de cadeias para uma matriz de cadeia que pode ser utilizado toopopulate um `Collection(Edm.String)` campo no índice Olá.

Por exemplo, se a cadeia de entrada de Olá é `["red", "white", "blue"]`, em seguida, no campo de destino Olá do tipo `Collection(Edm.String)` irá ser preenchida com valores de Olá três `red`, `white` e `blue`. Para os valores de entrada que não podem ser analisados como as matrizes de cadeia JSON, será devolvido um erro.

#### <a name="sample-use-case"></a>Caso de utilização de exemplo
Base de dados SQL do Azure não tem um tipo de dados incorporados naturalmente mapeia demasiado`Collection(Edm.String)` campos na Azure Search. toopopulate campos de coleção de cadeia, formatar os dados de origem como uma matriz de cadeia JSON e utilizar esta função.

#### <a name="example"></a>Exemplo
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Ajude-na tornar o melhor da Azure Search
Se tiver de pedidos de funcionalidades ou ideias para melhoramentos, contacte toous no nosso [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).
