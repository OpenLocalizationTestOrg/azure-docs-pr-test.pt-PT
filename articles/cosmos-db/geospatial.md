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
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="4a0a7-103">Trabalhar com dados de localização de GeoJSON do BD Azure Cosmos e geoespacial</span><span class="sxs-lookup"><span data-stu-id="4a0a7-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="4a0a7-104">Este artigo é uma funcionalidade de geoespacial toohello introdução no [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="4a0a7-105">Depois de ler este artigo, estará Olá tooanswer capaz de seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="4a0a7-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="4a0a7-106">Como posso armazenar dados geográficos do BD Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="4a0a7-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="4a0a7-107">Como pode consultar os dados geoespacial na base de dados do Azure Cosmos no SQL Server e LINQ?</span><span class="sxs-lookup"><span data-stu-id="4a0a7-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="4a0a7-108">Como ativar ou desativar a indexação geográficos do BD Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="4a0a7-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="4a0a7-109">Este artigo mostra como toowork com dados geográficos com Olá API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="4a0a7-110">Consulte este [GitHub projeto](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) para exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="4a0a7-111">Dados de toospatial de introdução</span><span class="sxs-lookup"><span data-stu-id="4a0a7-111">Introduction toospatial data</span></span>
<span data-ttu-id="4a0a7-112">Dados geográficos descreve posição Olá e a forma de objetos de espaço.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="4a0a7-113">Na maioria das aplicações, estas correspondem tooobjects na terra hello, ou seja, os dados de geoespacial.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="4a0a7-114">Dados geográficos podem ser utilizados toorepresent Olá localização de uma pessoa, um local de interesse ou limites de Olá de uma cidade ou uma lake.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="4a0a7-115">Casos de utilização comuns envolvem, muitas vezes, consultas de proximidade, para por exemplo, "encontrar todos os cafés quase meu localização atual".</span><span class="sxs-lookup"><span data-stu-id="4a0a7-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="4a0a7-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="4a0a7-116">GeoJSON</span></span>
<span data-ttu-id="4a0a7-117">BD do Cosmos do Azure suporta a indexação e consultar geoespacial ponto de dados de que são representados utilizando Olá [GeoJSON especificação](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="4a0a7-118">Estruturas de dados de GeoJSON são sempre objetos JSON válidos, para que podem ser armazenadas e consultados utilizando a base de dados do Azure Cosmos sem quaisquer ferramentas especializadas ou bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="4a0a7-119">Olá SDKs de BD do Azure Cosmos fornecem classes de programa auxiliar e métodos que tornam mais fácil toowork com dados geográficos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="4a0a7-120">Pontos, Multipoints e polígonos</span><span class="sxs-lookup"><span data-stu-id="4a0a7-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="4a0a7-121">A **ponto** indica uma posição único no espaço.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="4a0a7-122">Dados geoespacial, um ponto de representa a localização exata Olá, que pode ser uma morada de um arquivo de grocery, um quiosque, um automóvel ou uma localidade.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="4a0a7-123">É representado um ponto no par GeoJSON (e base de dados do Azure Cosmos) utilizando o respetiva coordenada ou latitude e longitude.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="4a0a7-124">Eis um exemplo JSON para um ponto.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="4a0a7-125">**Pontos do Cosmos BD do Azure**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="4a0a7-126">Olá GeoJSON especificação Especifica longitude primeiro e latitude segundo.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="4a0a7-127">Como nas outras aplicações de mapeamento, latitude e longitude são os ângulos em representado em termos de graus.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="4a0a7-128">Os valores de longitude são avaliados da Olá meridiano Prime e encontram-se entre-180 e e 180.0 graus e latitude valores são avaliados do Equador Olá e são entre-90.0 e 90.0 graus.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="4a0a7-129">BD do Azure do Cosmos interpreta coordenadas conforme representado por sistema de referência de WGS 84 Olá.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="4a0a7-130">Consulte abaixo para obter mais detalhes sobre os sistemas de referência coordenada.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="4a0a7-131">Isto pode ser incorporado um documento de base de dados do Azure Cosmos como o mostrado neste exemplo de um perfil de utilizador que contém dados de localização:</span><span class="sxs-lookup"><span data-stu-id="4a0a7-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="4a0a7-132">**Utilizar perfil com a localização armazenada na base de dados do Azure Cosmos**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="4a0a7-133">Além disso toopoints, GeoJSON também suporta Multipoints e de polígonos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="4a0a7-134">**Multipoints** representa uma série de duas ou mais pontos no espaço e Olá segmentos de linha que ligue-os.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="4a0a7-135">Dados geoespacial, Multipoints são frequentemente utilizadas toorepresent highways ou rivers.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="4a0a7-136">A **polígono** é um limite de pontos ligados, o que constitui uma LineString fechada.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="4a0a7-137">Polígonos são frequentemente utilizadas toorepresent natural formação que resultam em como lagos ou jurisdictions afiliações como cidades e Estados.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="4a0a7-138">Eis um exemplo de um polígono do BD Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="4a0a7-139">**Polígonos no GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="4a0a7-140">Olá GeoJSON especificação requer que de polígonos válidos, hello último par coordenada fornecido deve ser Olá mesmo como Olá primeiro, toocreate uma forma fechada.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="4a0a7-141">Pontos de dentro de um polígono tem de ser especificados por ordem counter-no sentido horário.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="4a0a7-142">Um polígono especificado na ordem no sentido horário representa inverso Olá da região de Olá dentro da mesma.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="4a0a7-143">Na adição tooPoint, LineString e polígono, GeoJSON também especifica representação Olá como toogroup várias localizações geoespacial, bem como propriedades de arbitrários tooassociate com geolocalização como um **funcionalidade**.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="4a0a7-144">Uma vez que estes objetos JSON válido, estes podem todos ser armazenadas e processadas do BD Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="4a0a7-145">No entanto Azure Cosmos DB só suporta a indexação automática de pontos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="4a0a7-146">Coordenar a sistemas de referência</span><span class="sxs-lookup"><span data-stu-id="4a0a7-146">Coordinate reference systems</span></span>
<span data-ttu-id="4a0a7-147">Uma vez que forma Olá de earth Olá dados, coordenadas dos dados geoespacial é representado na muitos sistemas de referência coordenada (CR), cada um com os seus próprios frames de referência e unidades de medida.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="4a0a7-148">Por exemplo, Olá "National grelha de Britain" é um sistema de referência for muito exato para Olá Reino Unido, mas não fora-lo.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="4a0a7-149">Olá CR mais popular utilizado hoje é Olá mundo de sistema Geodetic [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="4a0a7-150">Dispositivos GPS e muitas mapeamento serviços, incluindo mapas do Google e APIs do Bing Maps utilizam WGS 84.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="4a0a7-151">BD do Cosmos do Azure suporta a indexação e consultar dados geoespacial utilizando Olá WGS 84 CR apenas.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="4a0a7-152">Criar documentos com dados geográficos</span><span class="sxs-lookup"><span data-stu-id="4a0a7-152">Creating documents with spatial data</span></span>
<span data-ttu-id="4a0a7-153">Quando criar documentos que contenham valores GeoJSON, são automaticamente indexados com um índice geográfico na política de indexação toohello accordance da coleção de Olá.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="4a0a7-154">Se estiver a trabalhar com um SDK de BD do Azure Cosmos num idioma escrito de forma dinâmica, como o Python ou Node.js, tem de criar GeoJSON válido.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="4a0a7-155">**Criar um documento com dados Geoespacial no Node.js**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-155">**Create Document with Geospatial data in Node.js**</span></span>

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

<span data-ttu-id="4a0a7-156">Se estiver a trabalhar com Olá APIs do DocumentDB, pode utilizar Olá `Point` e `Polygon` classes Olá `Microsoft.Azure.Documents.Spatial` informações de localização do espaço de nomes tooembed dentro os objetos da aplicação.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="4a0a7-157">Estas classes ajudam a simplificar a serialização de Olá e anulação da serialização de dados geográficos para GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="4a0a7-158">**Criar um documento com dados Geoespacial no .NET**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="4a0a7-159">Se não tem informações de latitude e longitude de Olá, mas tiver endereços físicos Olá ou nome de localização como cidade ou país, pode procurar coordenadas reais Olá utilizando um serviço a codificação geográfica como serviços de REST do Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="4a0a7-160">Saiba mais sobre a codificação geográfica Bing Maps [aqui](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="4a0a7-161">Consultar os tipos geográficos</span><span class="sxs-lookup"><span data-stu-id="4a0a7-161">Querying spatial types</span></span>
<span data-ttu-id="4a0a7-162">Agora que iremos tiver decorrido ver como tooinsert geoespacial dados, vamos ver como tooquery estes dados utilizando a BD do Cosmos do Azure com o SQL e LINQ.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="4a0a7-163">Geográficos funções incorporadas do SQL Server</span><span class="sxs-lookup"><span data-stu-id="4a0a7-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="4a0a7-164">BD do Azure do Cosmos suporta Olá seguintes funções incorporadas do abra Geoespacial Consortium (OGC) para consultar o geoespacial.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="4a0a7-165">Para obter mais detalhes sobre o conjunto completo de Olá das funções incorporadas no Olá linguagem SQL, consulte demasiado[consulta Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="4a0a7-166"><strong>Utilização</strong></span><span class="sxs-lookup"><span data-stu-id="4a0a7-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="4a0a7-167"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="4a0a7-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a0a7-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="4a0a7-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="4a0a7-169">Devolve a distância Olá entre Olá dois GeoJSON ponto, Polygon ou LineString expressões.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a0a7-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="4a0a7-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="4a0a7-171">Devolve uma expressão booleana que indica se a objetos de GeoJSON primeiro Olá (ponto, polígono ou LineString) é dentro a objetos de GeoJSON segundo Olá (ponto, polígono ou LineString).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a0a7-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="4a0a7-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="4a0a7-173">Devolve uma expressão de booleana indicando se intersect Olá dois especificados GeoJSON objetos (ponto, polígono ou LineString).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a0a7-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="4a0a7-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="4a0a7-175">Devolve um valor de Booleano indicando se Olá especificada a expressão de ponto de GeoJSON, polígono ou LineString é válida.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a0a7-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="4a0a7-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="4a0a7-177">Devolve um valor JSON que contém um valor booleano se Olá especificado GeoJSON ponto, polígono ou LineString expressão é válido e se inválido, Olá, além disso, razão como um valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="4a0a7-178">Funções geográficos podem ser utilizados tooperform proximidade consultas contra dados geográficos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="4a0a7-179">Por exemplo, aqui está uma consulta que devolva a que família de todos os documentos que está dentro de 30 km de Olá localização especificada utilizando Olá ST_DISTANCE incorporada função.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="4a0a7-180">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="4a0a7-181">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="4a0a7-182">Se incluir indexação geográficos na política de indexação, em seguida, "consultas distância" serão servidas forma eficiente através de índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="4a0a7-183">Para obter mais detalhes sobre a indexação geográficos, consulte a secção de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="4a0a7-184">Se não tiver um geográficos índice para Olá especificado caminhos, ainda pode executar consultas geográficos especificando `x-ms-documentdb-query-enable-scan` cabeçalho do pedido com o valor de Olá definido demasiado "true".</span><span class="sxs-lookup"><span data-stu-id="4a0a7-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="4a0a7-185">No .NET, isto pode ser feito através da passagem Olá opcional **FeedOptions** argumento tooqueries com [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) definir tootrue.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="4a0a7-186">ST_WITHIN podem ser utilizado toocheck se situam-se um ponto dentro de um polígono.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="4a0a7-187">Normalmente polígonos são limites toorepresent utilizado como zip códigos, limites de estado ou formação que resultam em natural.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="4a0a7-188">Novamente se incluir indexação geográficos na política de indexação, em seguida, "dentro" consultas serão servidas forma eficiente através de índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="4a0a7-189">Os argumentos polígono ST_WITHIN podem conter apenas um único toque, ou seja, Olá polígonos não podem conter holes nos mesmos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="4a0a7-190">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="4a0a7-191">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="4a0a7-192">Semelhante toohow incompatibilidade de tipos funciona na consulta de base de dados do Azure Cosmos, se o valor de localização de Olá especificado no argumento está incorreto ou é inválido, em seguida, avaliará demasiado**indefinido** , Olá avaliada documento toobe ignorados do Olá resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="4a0a7-193">Se a consulta devolve não existem resultados, execute toodebug ST_ISVALIDDETAILED por que motivo o tipo de spatail Olá é inválido.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="4a0a7-194">BD do Azure do Cosmos também suporta a execução de consultas tangente, ou seja, pode indexar polígonos ou linhas na base de dados do Azure Cosmos e consultar áreas Olá que contenha um ponto especificado.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="4a0a7-195">Este padrão é normalmente utilizado em logística tooidentify por exemplo, quando um camião entra ou sai de uma área designada.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="4a0a7-196">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="4a0a7-197">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="4a0a7-198">ST_ISVALID e ST_ISVALIDDETAILED podem ser utilizado toocheck se um objeto espacial é válido.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="4a0a7-199">Por exemplo, Olá seguinte consulta verifica a validade Olá de um ponto com um fora do valor de intervalo de latitude (-132.8).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="4a0a7-200">ST_ISVALID devolve apenas um valor booleano, e devolve ST_ISVALIDDETAILED Olá Booleano e uma cadeia contendo o motivo de Olá por que motivo é considerada inválida.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="4a0a7-201">* * Consultar * *</span><span class="sxs-lookup"><span data-stu-id="4a0a7-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="4a0a7-202">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="4a0a7-203">Estas funções também podem ser utilizado toovalidate polígonos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="4a0a7-204">Por exemplo, aqui, utilizamos ST_ISVALIDDETAILED toovalidate um polígono que não está fechado.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="4a0a7-205">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="4a0a7-206">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="4a0a7-207">Consulta de LINQ no Olá .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4a0a7-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="4a0a7-208">Olá SDK do .NET DocumentDB também fornecedores stub métodos `Distance()` e `Within()` para utilização nas expressões de LINQ.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="4a0a7-209">Olá fornecedor DocumentDB LINQ traduz destas chamadas toohello equivalentes SQL função incorporada chamadas de método (ST_DISTANCE e ST_WITHIN respetivamente).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="4a0a7-210">Eis um exemplo de uma consulta LINQ localiza todos os documentos na coleção de base de dados do Azure Cosmos Olá cujo valor de "localização" dentro de um radius de 30km de Olá especificado ponto utilizando LINQ.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="4a0a7-211">**Consulta LINQ para distância**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="4a0a7-212">Da mesma forma, segue-se uma consulta para encontrar todos os documentos de Olá cuja "localização" está dentro do Olá especificado caixa/polígono.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="4a0a7-213">**Consulta de LINQ para dentro do**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="4a0a7-214">Agora que iremos tiver decorrido ver como documentos tooquery utilizando LINQ e SQL, vamos ver como tooconfigure BD do Cosmos do Azure para indexação geográficos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="4a0a7-215">Indexação</span><span class="sxs-lookup"><span data-stu-id="4a0a7-215">Indexing</span></span>
<span data-ttu-id="4a0a7-216">Conforme é descrito em Olá [esquema Agnóstico indexação com base de dados do Azure Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) documento, vamos concebido toobe de motor de base de dados da BD do Azure Cosmos verdadeiramente agnóstico de esquema e fornecer suporte de primeira classe para JSON.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="4a0a7-217">motor de base de dados de escrita otimizada Olá da base de dados do Azure Cosmos nativamente compreende dados geográficos (pontos, Multilinestrings e as linhas) representados no padrão de GeoJSON Olá.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="4a0a7-218">Um nutshell, geometria Olá é projetada de coordenadas geodetic para um plane 2D, em seguida, dividida progressivamente células utilizando um **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="4a0a7-219">Estes células são mapeadas too1D com base na localização de Olá de célula de Olá dentro de um **Hilbert espaço ao preencher em curva**, que ela vai preservando localidade de pontos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="4a0a7-220">Além disso quando os dados de localização estão indexados, passa através de um processo conhecido como **tecelagem**, ou seja, todas as Olá células que intersect uma localização estão identificadas e armazenadas como chaves de índice de base de dados do Azure Cosmos Olá.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="4a0a7-221">No momento da consulta, argumentos como pontos de polígonos, sendo também tessellated tooextract Olá intervalos de ID de célula relevantes, em seguida, utilizado tooretrieve dados desde o índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="4a0a7-222">Se especificar uma política de indexação que inclui o índice geográfico para / * (todos os caminhos), em seguida, todos os pontos de encontrado na coleção de Olá são indexados para consultas geográficos eficiente (ST_WITHIN e ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="4a0a7-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="4a0a7-223">Os índices espaciais não ter um valor de precisão e utilize sempre um valor de precisão predefinido.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="4a0a7-224">BD do Cosmos do Azure suporta a indexação automática de pontos, Multilinestrings e Multipoints</span><span class="sxs-lookup"><span data-stu-id="4a0a7-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="4a0a7-225">Olá fragmento JSON seguinte mostra uma política de indexação com indexação geográficos ativado, ou seja, qualquer ponto GeoJSON encontrado documentos para consultas geográficos de índice.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="4a0a7-226">Se modifica Olá indexação política utilizando Olá Portal do Azure, pode especificar Olá JSON a seguir para indexação política tooenable geográfico de indexação na sua coleção.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="4a0a7-227">**Coleção JSON de política de indexação com Spatial ativada e de pontos de polígonos**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="4a0a7-228">Eis um fragmento de código no .NET que mostra como toocreate uma coleção com a indexação geográficos ativada para todos os caminhos que contenham pontos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="4a0a7-229">**Criar uma coleção com a indexação geográficos**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="4a0a7-230">E Eis como pode modificar um existente tootake partido da coleção de indexação geográficos através de quaisquer pontos que estão armazenados em documentos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="4a0a7-231">**Modificar uma coleção existente com a indexação geográficos**</span><span class="sxs-lookup"><span data-stu-id="4a0a7-231">**Modify an existing collection with spatial indexing**</span></span>

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
> <span data-ttu-id="4a0a7-232">Se a localização de Olá GeoJSON valor dentro do documento Olá incorreto ou é inválido, em seguida,-será não obter indexado para o consultar geográficos.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="4a0a7-233">Pode validar utilizando ST_ISVALID e ST_ISVALIDDETAILED valores da localização.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="4a0a7-234">Se a definição da coleção inclui uma chave de partição, não foi reportado o progresso de transformação de indexação.</span><span class="sxs-lookup"><span data-stu-id="4a0a7-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4a0a7-235">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4a0a7-235">Next steps</span></span>
<span data-ttu-id="4a0a7-236">Agora que já learnt sobre como tooget começar geoespacial suporte do BD Azure Cosmos, pode:</span><span class="sxs-lookup"><span data-stu-id="4a0a7-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="4a0a7-237">Iniciar a codificação com Olá [exemplos de código Geoespacial .NET no GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="4a0a7-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="4a0a7-238">Introdução às mãos com geoespacial consultar em Olá [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="4a0a7-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="4a0a7-239">Saiba mais sobre [consulta de base de dados do Azure Cosmos](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="4a0a7-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="4a0a7-240">Saiba mais sobre [políticas de indexação do Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="4a0a7-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

