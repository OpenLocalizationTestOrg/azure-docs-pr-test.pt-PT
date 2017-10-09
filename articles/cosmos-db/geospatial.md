---
title: aaaWorking com dados geoespacial do BD Azure Cosmos | Microsoft Docs
description: "Compreenda como toocreate, índice e consultar geográficos objetos com base de dados do Azure Cosmos e Olá API do DocumentDB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Trabalhar com dados de localização de GeoJSON do BD Azure Cosmos e geoespacial
Este artigo é uma funcionalidade de geoespacial toohello introdução no [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). Depois de ler este artigo, estará Olá tooanswer capaz de seguintes perguntas:

* Como posso armazenar dados geográficos do BD Azure Cosmos?
* Como pode consultar os dados geoespacial na base de dados do Azure Cosmos no SQL Server e LINQ?
* Como ativar ou desativar a indexação geográficos do BD Azure Cosmos?

Este artigo mostra como toowork com dados geográficos com Olá API do DocumentDB. Consulte este [GitHub projeto](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) para exemplos de código.

## <a name="introduction-toospatial-data"></a>Dados de toospatial de introdução
Dados geográficos descreve posição Olá e a forma de objetos de espaço. Na maioria das aplicações, estas correspondem tooobjects na terra hello, ou seja, os dados de geoespacial. Dados geográficos podem ser utilizados toorepresent Olá localização de uma pessoa, um local de interesse ou limites de Olá de uma cidade ou uma lake. Casos de utilização comuns envolvem, muitas vezes, consultas de proximidade, para por exemplo, "encontrar todos os cafés quase meu localização atual". 

### <a name="geojson"></a>GeoJSON
BD do Cosmos do Azure suporta a indexação e consultar geoespacial ponto de dados de que são representados utilizando Olá [GeoJSON especificação](https://tools.ietf.org/html/rfc7946). Estruturas de dados de GeoJSON são sempre objetos JSON válidos, para que podem ser armazenadas e consultados utilizando a base de dados do Azure Cosmos sem quaisquer ferramentas especializadas ou bibliotecas. Olá SDKs de BD do Azure Cosmos fornecem classes de programa auxiliar e métodos que tornam mais fácil toowork com dados geográficos. 

### <a name="points-linestrings-and-polygons"></a>Pontos, Multipoints e polígonos
A **ponto** indica uma posição único no espaço. Dados geoespacial, um ponto de representa a localização exata Olá, que pode ser uma morada de um arquivo de grocery, um quiosque, um automóvel ou uma localidade.  É representado um ponto no par GeoJSON (e base de dados do Azure Cosmos) utilizando o respetiva coordenada ou latitude e longitude. Eis um exemplo JSON para um ponto.

**Pontos do Cosmos BD do Azure**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> Olá GeoJSON especificação Especifica longitude primeiro e latitude segundo. Como nas outras aplicações de mapeamento, latitude e longitude são os ângulos em representado em termos de graus. Os valores de longitude são avaliados da Olá meridiano Prime e encontram-se entre-180 e e 180.0 graus e latitude valores são avaliados do Equador Olá e são entre-90.0 e 90.0 graus. 
> 
> BD do Azure do Cosmos interpreta coordenadas conforme representado por sistema de referência de WGS 84 Olá. Consulte abaixo para obter mais detalhes sobre os sistemas de referência coordenada.
> 
> 

Isto pode ser incorporado um documento de base de dados do Azure Cosmos como o mostrado neste exemplo de um perfil de utilizador que contém dados de localização:

**Utilizar perfil com a localização armazenada na base de dados do Azure Cosmos**

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

Além disso toopoints, GeoJSON também suporta Multipoints e de polígonos. **Multipoints** representa uma série de duas ou mais pontos no espaço e Olá segmentos de linha que ligue-os. Dados geoespacial, Multipoints são frequentemente utilizadas toorepresent highways ou rivers. A **polígono** é um limite de pontos ligados, o que constitui uma LineString fechada. Polígonos são frequentemente utilizadas toorepresent natural formação que resultam em como lagos ou jurisdictions afiliações como cidades e Estados. Eis um exemplo de um polígono do BD Azure Cosmos. 

**Polígonos no GeoJSON**

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> Olá GeoJSON especificação requer que de polígonos válidos, hello último par coordenada fornecido deve ser Olá mesmo como Olá primeiro, toocreate uma forma fechada.
> 
> Pontos de dentro de um polígono tem de ser especificados por ordem counter-no sentido horário. Um polígono especificado na ordem no sentido horário representa inverso Olá da região de Olá dentro da mesma.
> 
> 

Na adição tooPoint, LineString e polígono, GeoJSON também especifica representação Olá como toogroup várias localizações geoespacial, bem como propriedades de arbitrários tooassociate com geolocalização como um **funcionalidade**. Uma vez que estes objetos JSON válido, estes podem todos ser armazenadas e processadas do BD Azure Cosmos. No entanto Azure Cosmos DB só suporta a indexação automática de pontos.

### <a name="coordinate-reference-systems"></a>Coordenar a sistemas de referência
Uma vez que forma Olá de earth Olá dados, coordenadas dos dados geoespacial é representado na muitos sistemas de referência coordenada (CR), cada um com os seus próprios frames de referência e unidades de medida. Por exemplo, Olá "National grelha de Britain" é um sistema de referência for muito exato para Olá Reino Unido, mas não fora-lo. 

Olá CR mais popular utilizado hoje é Olá mundo de sistema Geodetic [WGS 84](http://earth-info.nga.mil/GandG/wgs84/). Dispositivos GPS e muitas mapeamento serviços, incluindo mapas do Google e APIs do Bing Maps utilizam WGS 84. BD do Cosmos do Azure suporta a indexação e consultar dados geoespacial utilizando Olá WGS 84 CR apenas. 

## <a name="creating-documents-with-spatial-data"></a>Criar documentos com dados geográficos
Quando criar documentos que contenham valores GeoJSON, são automaticamente indexados com um índice geográfico na política de indexação toohello accordance da coleção de Olá. Se estiver a trabalhar com um SDK de BD do Azure Cosmos num idioma escrito de forma dinâmica, como o Python ou Node.js, tem de criar GeoJSON válido.

**Criar um documento com dados Geoespacial no Node.js**

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

Se estiver a trabalhar com Olá APIs do DocumentDB, pode utilizar Olá `Point` e `Polygon` classes Olá `Microsoft.Azure.Documents.Spatial` informações de localização do espaço de nomes tooembed dentro os objetos da aplicação. Estas classes ajudam a simplificar a serialização de Olá e anulação da serialização de dados geográficos para GeoJSON.

**Criar um documento com dados Geoespacial no .NET**

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

Se não tem informações de latitude e longitude de Olá, mas tiver endereços físicos Olá ou nome de localização como cidade ou país, pode procurar coordenadas reais Olá utilizando um serviço a codificação geográfica como serviços de REST do Bing Maps. Saiba mais sobre a codificação geográfica Bing Maps [aqui](https://msdn.microsoft.com/library/ff701713.aspx).

## <a name="querying-spatial-types"></a>Consultar os tipos geográficos
Agora que iremos tiver decorrido ver como tooinsert geoespacial dados, vamos ver como tooquery estes dados utilizando a BD do Cosmos do Azure com o SQL e LINQ.

### <a name="spatial-sql-built-in-functions"></a>Geográficos funções incorporadas do SQL Server
BD do Azure do Cosmos suporta Olá seguintes funções incorporadas do abra Geoespacial Consortium (OGC) para consultar o geoespacial. Para obter mais detalhes sobre o conjunto completo de Olá das funções incorporadas no Olá linguagem SQL, consulte demasiado[consulta Azure Cosmos DB](documentdb-sql-query.md).

<table>
<tr>
  <td><strong>Utilização</strong></td>
  <td><strong>Descrição</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (spatial_expr, spatial_expr)</td>
  <td>Devolve a distância Olá entre Olá dois GeoJSON ponto, Polygon ou LineString expressões.</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>Devolve uma expressão booleana que indica se a objetos de GeoJSON primeiro Olá (ponto, polígono ou LineString) é dentro a objetos de GeoJSON segundo Olá (ponto, polígono ou LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Devolve uma expressão de booleana indicando se intersect Olá dois especificados GeoJSON objetos (ponto, polígono ou LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Devolve um valor de Booleano indicando se Olá especificada a expressão de ponto de GeoJSON, polígono ou LineString é válida.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Devolve um valor JSON que contém um valor booleano se Olá especificado GeoJSON ponto, polígono ou LineString expressão é válido e se inválido, Olá, além disso, razão como um valor de cadeia.</td>
</tr>
</table>

Funções geográficos podem ser utilizados tooperform proximidade consultas contra dados geográficos. Por exemplo, aqui está uma consulta que devolva a que família de todos os documentos que está dentro de 30 km de Olá localização especificada utilizando Olá ST_DISTANCE incorporada função. 

**Consulta**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Resultados**

    [{
      "id": "WakefieldFamily"
    }]

Se incluir indexação geográficos na política de indexação, em seguida, "consultas distância" serão servidas forma eficiente através de índice de Olá. Para obter mais detalhes sobre a indexação geográficos, consulte a secção de Olá abaixo. Se não tiver um geográficos índice para Olá especificado caminhos, ainda pode executar consultas geográficos especificando `x-ms-documentdb-query-enable-scan` cabeçalho do pedido com o valor de Olá definido demasiado "true". No .NET, isto pode ser feito através da passagem Olá opcional **FeedOptions** argumento tooqueries com [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) definir tootrue. 

ST_WITHIN podem ser utilizado toocheck se situam-se um ponto dentro de um polígono. Normalmente polígonos são limites toorepresent utilizado como zip códigos, limites de estado ou formação que resultam em natural. Novamente se incluir indexação geográficos na política de indexação, em seguida, "dentro" consultas serão servidas forma eficiente através de índice de Olá. 

Os argumentos polígono ST_WITHIN podem conter apenas um único toque, ou seja, Olá polígonos não podem conter holes nos mesmos. 

**Consulta**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**Resultados**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> Semelhante toohow incompatibilidade de tipos funciona na consulta de base de dados do Azure Cosmos, se o valor de localização de Olá especificado no argumento está incorreto ou é inválido, em seguida, avaliará demasiado**indefinido** , Olá avaliada documento toobe ignorados do Olá resultados da consulta. Se a consulta devolve não existem resultados, execute toodebug ST_ISVALIDDETAILED por que motivo o tipo de spatail Olá é inválido.     
> 
> 

BD do Azure do Cosmos também suporta a execução de consultas tangente, ou seja, pode indexar polígonos ou linhas na base de dados do Azure Cosmos e consultar áreas Olá que contenha um ponto especificado. Este padrão é normalmente utilizado em logística tooidentify por exemplo, quando um camião entra ou sai de uma área designada. 

**Consulta**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**Resultados**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID e ST_ISVALIDDETAILED podem ser utilizado toocheck se um objeto espacial é válido. Por exemplo, Olá seguinte consulta verifica a validade Olá de um ponto com um fora do valor de intervalo de latitude (-132.8). ST_ISVALID devolve apenas um valor booleano, e devolve ST_ISVALIDDETAILED Olá Booleano e uma cadeia contendo o motivo de Olá por que motivo é considerada inválida.

* * Consultar * *

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**Resultados**

    [{
      "$1": false
    }]

Estas funções também podem ser utilizado toovalidate polígonos. Por exemplo, aqui, utilizamos ST_ISVALIDDETAILED toovalidate um polígono que não está fechado. 

**Consulta**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**Resultados**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>Consulta de LINQ no Olá .NET SDK
Olá SDK do .NET DocumentDB também fornecedores stub métodos `Distance()` e `Within()` para utilização nas expressões de LINQ. Olá fornecedor DocumentDB LINQ traduz destas chamadas toohello equivalentes SQL função incorporada chamadas de método (ST_DISTANCE e ST_WITHIN respetivamente). 

Eis um exemplo de uma consulta LINQ localiza todos os documentos na coleção de base de dados do Azure Cosmos Olá cujo valor de "localização" dentro de um radius de 30km de Olá especificado ponto utilizando LINQ.

**Consulta LINQ para distância**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

Da mesma forma, segue-se uma consulta para encontrar todos os documentos de Olá cuja "localização" está dentro do Olá especificado caixa/polígono. 

**Consulta de LINQ para dentro do**

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


Agora que iremos tiver decorrido ver como documentos tooquery utilizando LINQ e SQL, vamos ver como tooconfigure BD do Cosmos do Azure para indexação geográficos.

## <a name="indexing"></a>Indexação
Conforme é descrito em Olá [esquema Agnóstico indexação com base de dados do Azure Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) documento, vamos concebido toobe de motor de base de dados da BD do Azure Cosmos verdadeiramente agnóstico de esquema e fornecer suporte de primeira classe para JSON. motor de base de dados de escrita otimizada Olá da base de dados do Azure Cosmos nativamente compreende dados geográficos (pontos, Multilinestrings e as linhas) representados no padrão de GeoJSON Olá.

Um nutshell, geometria Olá é projetada de coordenadas geodetic para um plane 2D, em seguida, dividida progressivamente células utilizando um **quadtree**. Estes células são mapeadas too1D com base na localização de Olá de célula de Olá dentro de um **Hilbert espaço ao preencher em curva**, que ela vai preservando localidade de pontos. Além disso quando os dados de localização estão indexados, passa através de um processo conhecido como **tecelagem**, ou seja, todas as Olá células que intersect uma localização estão identificadas e armazenadas como chaves de índice de base de dados do Azure Cosmos Olá. No momento da consulta, argumentos como pontos de polígonos, sendo também tessellated tooextract Olá intervalos de ID de célula relevantes, em seguida, utilizado tooretrieve dados desde o índice de Olá.

Se especificar uma política de indexação que inclui o índice geográfico para / * (todos os caminhos), em seguida, todos os pontos de encontrado na coleção de Olá são indexados para consultas geográficos eficiente (ST_WITHIN e ST_DISTANCE). Os índices espaciais não ter um valor de precisão e utilize sempre um valor de precisão predefinido.

> [!NOTE]
> BD do Cosmos do Azure suporta a indexação automática de pontos, Multilinestrings e Multipoints
> 
> 

Olá fragmento JSON seguinte mostra uma política de indexação com indexação geográficos ativado, ou seja, qualquer ponto GeoJSON encontrado documentos para consultas geográficos de índice. Se modifica Olá indexação política utilizando Olá Portal do Azure, pode especificar Olá JSON a seguir para indexação política tooenable geográfico de indexação na sua coleção.

**Coleção JSON de política de indexação com Spatial ativada e de pontos de polígonos**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

Eis um fragmento de código no .NET que mostra como toocreate uma coleção com a indexação geográficos ativada para todos os caminhos que contenham pontos. 

**Criar uma coleção com a indexação geográficos**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

E Eis como pode modificar um existente tootake partido da coleção de indexação geográficos através de quaisquer pontos que estão armazenados em documentos.

**Modificar uma coleção existente com a indexação geográficos**

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> Se a localização de Olá GeoJSON valor dentro do documento Olá incorreto ou é inválido, em seguida,-será não obter indexado para o consultar geográficos. Pode validar utilizando ST_ISVALID e ST_ISVALIDDETAILED valores da localização.
> 
> Se a definição da coleção inclui uma chave de partição, não foi reportado o progresso de transformação de indexação. 
> 
> 

## <a name="next-steps"></a>Passos seguintes
Agora que já learnt sobre como tooget começar geoespacial suporte do BD Azure Cosmos, pode:

* Iniciar a codificação com Olá [exemplos de código Geoespacial .NET no GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* Introdução às mãos com geoespacial consultar em Olá [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)
* Saiba mais sobre [consulta de base de dados do Azure Cosmos](documentdb-sql-query.md)
* Saiba mais sobre [políticas de indexação do Azure Cosmos DB](indexing-policies.md)

