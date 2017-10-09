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
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="056a7-103">API de REST do serviço de pesquisa do Azure: Versão de pré-visualização 2015-02-28-</span><span class="sxs-lookup"><span data-stu-id="056a7-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="056a7-104">Este artigo é a documentação de referência de Olá para `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-105">Esta pré-visualização expande Olá versão atual do geralmente disponível, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), fornecendo Olá experimental funcionalidades a seguir:</span><span class="sxs-lookup"><span data-stu-id="056a7-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="056a7-106">`moreLikeThis`consultar o parâmetro na Olá [documentos sobre pesquisa](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="056a7-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="056a7-107">Encontrar outros documentos do documento específico tooanother relevantes.</span><span class="sxs-lookup"><span data-stu-id="056a7-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="056a7-108">Algumas partes adicionais de Olá `2015-02-28-Preview` REST API estão documentados em separado.</span><span class="sxs-lookup"><span data-stu-id="056a7-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="056a7-109">Estas incluem:</span><span class="sxs-lookup"><span data-stu-id="056a7-109">These include:</span></span>

* [<span data-ttu-id="056a7-110">Perfis de classificação</span><span class="sxs-lookup"><span data-stu-id="056a7-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="056a7-111">Indexadores</span><span class="sxs-lookup"><span data-stu-id="056a7-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="056a7-112">Serviço de pesquisa do Azure está disponível em múltiplas versões.</span><span class="sxs-lookup"><span data-stu-id="056a7-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="056a7-113">Consulte demasiado[controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="056a7-114">APIs neste documento</span><span class="sxs-lookup"><span data-stu-id="056a7-114">APIs in this document</span></span>
<span data-ttu-id="056a7-115">API do serviço de pesquisa do Azure suporta dois sintaxes de URL para operações de API: simples e OData (consulte [suporte para OData (API da Azure Search)](http://msdn.microsoft.com/library/azure/dn798932.aspx) para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="056a7-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="056a7-116">Olá lista seguinte mostra Olá de sintaxe simples.</span><span class="sxs-lookup"><span data-stu-id="056a7-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="056a7-117">Criar o índice</span><span class="sxs-lookup"><span data-stu-id="056a7-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-118">Atualizar o índice</span><span class="sxs-lookup"><span data-stu-id="056a7-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-119">Obter o índice</span><span class="sxs-lookup"><span data-stu-id="056a7-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-120">Índices de listagem</span><span class="sxs-lookup"><span data-stu-id="056a7-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-121">Obter estatísticas de índice</span><span class="sxs-lookup"><span data-stu-id="056a7-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-122">Analisador de teste</span><span class="sxs-lookup"><span data-stu-id="056a7-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-123">Eliminar um índice</span><span class="sxs-lookup"><span data-stu-id="056a7-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-124">Adicionar, eliminar e atualizar os dados dentro de um índice</span><span class="sxs-lookup"><span data-stu-id="056a7-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-125">Documentos sobre pesquisa</span><span class="sxs-lookup"><span data-stu-id="056a7-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-126">Documento de pesquisa</span><span class="sxs-lookup"><span data-stu-id="056a7-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="056a7-127">Contagem de documentos</span><span class="sxs-lookup"><span data-stu-id="056a7-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="056a7-128">Sugestões</span><span class="sxs-lookup"><span data-stu-id="056a7-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="056a7-129">Operações do índice</span><span class="sxs-lookup"><span data-stu-id="056a7-129">Index Operations</span></span>
<span data-ttu-id="056a7-130">Pode criar e gerir índices no serviço de pesquisa do Azure através de pedidos de HTTP simples (POST, GET, PUT, DELETE) em relação a um recurso de índice fornecido.</span><span class="sxs-lookup"><span data-stu-id="056a7-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="056a7-131">toocreate um índice, PUBLICA primeiro um documento JSON que descreve o esquema de índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="056a7-132">esquema de Olá define os campos de Olá de índice de Olá, os tipos de dados e como pode ser utilizados (por exemplo, no pesquisas de texto completo, os filtros, ordenação ou facetamento).</span><span class="sxs-lookup"><span data-stu-id="056a7-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="056a7-133">Também define perfis de classificação, dos sugestores e outro atributos tooconfigure Olá comportamento índice Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="056a7-134">Olá exemplo seguinte fornece uma ilustração de um esquema utilizada para procurar informações átrios com o campo de descrição de Olá definido dois idiomas.</span><span class="sxs-lookup"><span data-stu-id="056a7-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="056a7-135">Repare como atributos controlam a forma como o campo de Olá é utilizado.</span><span class="sxs-lookup"><span data-stu-id="056a7-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="056a7-136">Por exemplo Olá `hotelId` é utilizado como a chave do documento Olá (`"key": true`) e está excluído das pesquisas de texto completo (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="056a7-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

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

<span data-ttu-id="056a7-137">Depois de criar o índice de Olá, deverá carregar documentos preencher Olá índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="056a7-138">Consulte [adicionar ou atualizar documentos](#AddOrUpdateDocuments) para este passo seguinte.</span><span class="sxs-lookup"><span data-stu-id="056a7-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="056a7-139">Para um tooindexing de vídeo de introdução na pesquisa do Azure, consulte Olá [episódio de canal 9 nuvem abrangem na Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="056a7-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="056a7-140">Criar Índice</span><span class="sxs-lookup"><span data-stu-id="056a7-140">Create Index</span></span>
<span data-ttu-id="056a7-141">Um índice é Olá primário meio organizar e procure-os documentos na Azure Search, semelhante toohow uma tabela organiza registos numa base de dados.</span><span class="sxs-lookup"><span data-stu-id="056a7-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="056a7-142">Cada índice tem uma coleção de documentos que tudo está em conformidade com esquema de índice toohello (nomes de campo, tipos de dados e propriedades), mas os índices também especificar adicionais construções (dos sugestores, perfis de classificação e opções de CORS) que definem noutros comportamentos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="056a7-143">Pode criar um novo índice dentro de um serviço da Azure Search utilizando um pedido POST de HTTP ou PUT.</span><span class="sxs-lookup"><span data-stu-id="056a7-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="056a7-144">corpo de Olá de pedido de Olá é um esquema JSON que especifica as informações de configuração e o índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="056a7-145">Em alternativa, pode utilizar PUT e especificar o nome do índice Olá Olá URI.</span><span class="sxs-lookup"><span data-stu-id="056a7-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="056a7-146">Se o índice de Olá não existir, será criado.</span><span class="sxs-lookup"><span data-stu-id="056a7-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="056a7-147">Criar um índice determina a estrutura de Olá Olá documentos armazenados e utilizado em operações de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="056a7-148">Povoar o índice de Olá é uma operação separada.</span><span class="sxs-lookup"><span data-stu-id="056a7-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="056a7-149">Para este passo, pode utilizar um [indexador](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponíveis para origens de dados suportadas) ou um [adicionar, atualizar ou eliminar documentos](https://msdn.microsoft.com/library/azure/dn798930.aspx) operação.</span><span class="sxs-lookup"><span data-stu-id="056a7-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="056a7-150">índice de Olá inverted é gerado quando documentos Olá são publicados.</span><span class="sxs-lookup"><span data-stu-id="056a7-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="056a7-151">**Tenha em atenção**: Olá número máximo permitido de índices varia consoante o escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="056a7-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="056a7-152">serviço gratuito Olá permite cópias de segurança too3 índices.</span><span class="sxs-lookup"><span data-stu-id="056a7-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="056a7-153">O serviço padrão permite 50 índices por serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="056a7-154">Consulte [limites e restrições](http://msdn.microsoft.com/library/azure/dn798934.aspx) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="056a7-155">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-155">**Request**</span></span>

<span data-ttu-id="056a7-156">HTTPS é necessário para todos os pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="056a7-157">Olá **Create Index** pedido pode ser construído com um método POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="056a7-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="056a7-158">Quando utilizar POST, tem de fornecer um nome de índice no corpo do pedido de Olá, juntamente com a definição de esquema de índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="056a7-159">Com PUT, o nome do índice Olá faz parte do URL de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="056a7-160">Se não existir índice Olá, é criado.</span><span class="sxs-lookup"><span data-stu-id="056a7-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="056a7-161">Se já existir, é atualizado toohello nova definição.</span><span class="sxs-lookup"><span data-stu-id="056a7-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="056a7-162">o nome do índice Olá tem de ter minúsculas, começar com uma letra ou número, ter nenhum barras ou pontos e de ter menos de 128 carateres.</span><span class="sxs-lookup"><span data-stu-id="056a7-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="056a7-163">Depois de iniciar o nome do índice Olá com uma letra ou número, rest Olá do nome de Olá pode incluir qualquer letra, o número e travessões, desde que os traços Olá não estão consecutivos.</span><span class="sxs-lookup"><span data-stu-id="056a7-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="056a7-164">Olá `api-version` é necessária.</span><span class="sxs-lookup"><span data-stu-id="056a7-164">hello `api-version` is required.</span></span> <span data-ttu-id="056a7-165">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter uma lista de versões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="056a7-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="056a7-166">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-166">**Request Headers**</span></span>

<span data-ttu-id="056a7-167">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-168">`Content-Type`: Necessário.</span><span class="sxs-lookup"><span data-stu-id="056a7-168">`Content-Type`: Required.</span></span> <span data-ttu-id="056a7-169">Defina esta opção demasiado`application/json`</span><span class="sxs-lookup"><span data-stu-id="056a7-169">Set this too`application/json`</span></span>
* <span data-ttu-id="056a7-170">`api-key`: Necessário.</span><span class="sxs-lookup"><span data-stu-id="056a7-170">`api-key`: Required.</span></span> <span data-ttu-id="056a7-171">Olá `api-key` é utilizado para</span><span class="sxs-lookup"><span data-stu-id="056a7-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="056a7-172">autentica o serviço de pesquisa de tooyour Olá pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-173">É um valor de cadeia, o serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="056a7-174">Olá **Create Index** pedido tem de incluir um `api-key` cabeçalho definir a chave de administrador tooyour (como chave de consulta tooa oposição ao).</span><span class="sxs-lookup"><span data-stu-id="056a7-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="056a7-175">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-176">Pode obter o nome de serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-177">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-178"><a name="RequestData"></a>
**Sintaxe de corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="056a7-179">corpo de Olá de pedido de Olá contém uma definição de esquema, que inclui Olá lista de campos de dados dentro de documentos que irão ser sejam fornecidos este índice, tipos de dados, atributos, bem como uma lista opcional de perfis de classificação que é utilizado tooscore correspondente documentos em hora de consulta.</span><span class="sxs-lookup"><span data-stu-id="056a7-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="056a7-180">Tenha em atenção que um pedido POST, terá de especificar o nome do índice Olá no corpo do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="056a7-181">Só pode existir um campo de chave no índice Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="056a7-182">Tem toobe um campo de cadeia.</span><span class="sxs-lookup"><span data-stu-id="056a7-182">It has toobe a string field.</span></span> <span data-ttu-id="056a7-183">Este campo representa o identificador exclusivo do Olá para cada documento armazenado no índice Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="056a7-184">partes principais do Olá de um índice incluem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="056a7-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="056a7-185">`fields`que irá ser sejam fornecidas este índice, incluindo nome, tipo de dados e propriedades que definem as ações permitidas nesse campo.</span><span class="sxs-lookup"><span data-stu-id="056a7-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="056a7-186">`suggesters`utilizado para consultas de conclusão automática ou antecipada.</span><span class="sxs-lookup"><span data-stu-id="056a7-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="056a7-187">`scoringProfiles`utilizado para classificação de pontuação de pesquisa personalizada.</span><span class="sxs-lookup"><span data-stu-id="056a7-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="056a7-188">Consulte [adicionar perfis de classificação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="056a7-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` utilizado toodefine como documentos/consultas são divididas tokens indexable/pesquisáveis.</span><span class="sxs-lookup"><span data-stu-id="056a7-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="056a7-190">Consulte [análise na Azure Search](https://aka.ms//azsanalysis) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="056a7-191">`defaultScoringProfile`Utilizar predefinição de Olá toooverwrite comportamentos de classificação.</span><span class="sxs-lookup"><span data-stu-id="056a7-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="056a7-192">`corsOptions`consultas de várias origens de tooallow face ao seu índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="056a7-193">sintaxe de Olá para structuring payload de pedido de Olá é a seguinte.</span><span class="sxs-lookup"><span data-stu-id="056a7-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="056a7-194">Um exemplo de pedido é fornecido mais neste tópico.</span><span class="sxs-lookup"><span data-stu-id="056a7-194">A sample request is provided further on in this topic.</span></span>

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

<span data-ttu-id="056a7-195">**Atributos de índice**</span><span class="sxs-lookup"><span data-stu-id="056a7-195">**Index Attributes**</span></span>

<span data-ttu-id="056a7-196">Olá seguintes atributos podem ser definidos quando criar um índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="056a7-197">Para obter detalhes sobre a classificação e perfis de classificação, consulte [adicionar perfis de classificação](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="056a7-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="056a7-198">`name`-Conjuntos Olá nome do campo Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="056a7-199">`type`-Conjuntos Olá tipo de dados para o campo de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="056a7-200">`searchable`-Marca o campo de Olá como texto completo capaz de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="056a7-201">Isto significa que vai sofrer Analysis Services, tais como o word quebra durante a indexação.</span><span class="sxs-lookup"><span data-stu-id="056a7-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="056a7-202">Se definir um `searchable` valor do campo tooa como "sunny dia", internamente será dividida em tokens individuais Olá "sunny" e "dia".</span><span class="sxs-lookup"><span data-stu-id="056a7-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="056a7-203">Isto permite que as pesquisas de texto completo para estes termos.</span><span class="sxs-lookup"><span data-stu-id="056a7-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="056a7-204">Os campos do tipo `Edm.String` ou `Collection(Edm.String)` são `searchable` por predefinição.</span><span class="sxs-lookup"><span data-stu-id="056a7-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="056a7-205">Os campos de outros tipos de não podem ser `searchable`.</span><span class="sxs-lookup"><span data-stu-id="056a7-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="056a7-206">**Tenha em atenção**: `searchable` campos consumam espaço adicional no seu índice, uma vez que a Azure Search irão armazenar uma versão tokenized adicional do valor de campo Olá para pesquisas de texto completo.</span><span class="sxs-lookup"><span data-stu-id="056a7-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="056a7-207">Se quiser toosave espaço seu índice e não precisa de um toobe campo incluído na procura, defina `searchable` demasiado`false`.</span><span class="sxs-lookup"><span data-stu-id="056a7-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="056a7-208">`filterable`-Permite Olá campo toobe referenciado no `$filter` consultas.</span><span class="sxs-lookup"><span data-stu-id="056a7-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="056a7-209">`filterable`difere da `searchable` na forma como são processadas cadeias.</span><span class="sxs-lookup"><span data-stu-id="056a7-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="056a7-210">Os campos do tipo `Edm.String` ou `Collection(Edm.String)` que são `filterable` não são submetidos a quebra de palavra, pelo que é comparações para apenas corresponde exato.</span><span class="sxs-lookup"><span data-stu-id="056a7-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="056a7-211">Por exemplo, se definir esse um campo `f` demasiado "sunny dia", `$filter=f eq 'sunny'` encontrará não corresponde, mas `$filter=f eq 'sunny day'` será.</span><span class="sxs-lookup"><span data-stu-id="056a7-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="056a7-212">Todos os campos são `filterable` por predefinição.</span><span class="sxs-lookup"><span data-stu-id="056a7-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="056a7-213">`sortable`-Por predefinição sistema Olá ordena os resultados por pontuação, mas nas experiências muitos utilizadores serão útil toosort para campos de documentos Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="056a7-214">Os campos do tipo `Collection(Edm.String)` não pode ser `sortable`.</span><span class="sxs-lookup"><span data-stu-id="056a7-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="056a7-215">Todos os outros campos são `sortable` por predefinição.</span><span class="sxs-lookup"><span data-stu-id="056a7-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="056a7-216">`facetable`-Normalmente utilizadas numa apresentação de resultados de pesquisa que inclui o número de acessos por categoria (por exemplo, procure as câmaras digitais e Consulte pedidos pela marca, por megapixels, por preços, etc.).</span><span class="sxs-lookup"><span data-stu-id="056a7-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="056a7-217">Esta opção não pode ser utilizada com campos do tipo `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="056a7-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="056a7-218">Todos os outros campos são `facetable` por predefinição.</span><span class="sxs-lookup"><span data-stu-id="056a7-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="056a7-219">**Tenha em atenção**: campos do tipo `Edm.String` que são `filterable`, `sortable`, ou `facetable` pode ter um máximo de 32 KB de comprimento.</span><span class="sxs-lookup"><span data-stu-id="056a7-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="056a7-220">Isto acontece porque esses campos são tratados como um termo de pesquisa único e Olá comprimento máximo de um termo de pesquisa do Azure é de 32KB.</span><span class="sxs-lookup"><span data-stu-id="056a7-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="056a7-221">Se precisar de toostore texto mais mais um campo de cadeia única, terá de tooexplicitly definir `filterable`, `sortable`, e `facetable` demasiado`false` na sua definição de índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="056a7-222">**Tenha em atenção**: se um campo tenha nenhum dos Olá acima atributos definido demasiado`true` (`searchable`, `filterable`, `sortable`, ou`facetable`) campo Olá eficazmente está excluído do índice de Olá inverted.</span><span class="sxs-lookup"><span data-stu-id="056a7-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="056a7-223">Esta opção é útil para os campos que não são utilizados em consultas, mas são necessários nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="056a7-224">Excluir esses campos de índice de Olá melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="056a7-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="056a7-225">`key`-Marcas de escala Olá campo como contendo identificadores exclusivos para documentos no índice Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="056a7-226">Deve ser selecionado exatamente um campo como Olá `key` campo e tem de ser do tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="056a7-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="056a7-227">Campos de chave podem ser utilizado toolook dos documentos diretamente através do Olá [pesquisa API](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="056a7-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="056a7-228">`retrievable`-Define se campo Olá pode ser devolvido num resultado da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="056a7-229">Isto é útil quando pretende toouse um campo (por exemplo, a margem) como um filtro, ordenação ou mecanismo de classificação, mas não pretende que o utilizador do Olá campo toobe toohello visível final.</span><span class="sxs-lookup"><span data-stu-id="056a7-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="056a7-230">Este atributo tem de ser `true` para `key` campos.</span><span class="sxs-lookup"><span data-stu-id="056a7-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="056a7-231">`analyzer`-Conjuntos Olá nome Olá analisador toouse para campo Olá na hora de pesquisa e indexação hora.</span><span class="sxs-lookup"><span data-stu-id="056a7-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="056a7-232">Para Olá permitido definido de valores consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="056a7-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="056a7-233">Esta opção pode ser utilizada apenas com `searchable` campos e não podem ser definidos em conjunto com o `searchAnalyzer` ou `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="056a7-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="056a7-234">Assim que for escolhido o analisador de Olá, não pode ser alterada para o campo de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="056a7-235">`searchAnalyzer`-Conjuntos Olá nome do analisador de Olá utilizada no momento de pesquisa para o campo de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="056a7-236">Para Olá permitido definido de valores consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="056a7-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="056a7-237">Esta opção pode ser utilizada apenas com `searchable` campos.</span><span class="sxs-lookup"><span data-stu-id="056a7-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="056a7-238">Tem de ser definido em conjunto com `indexAnalyzer` e não pode ser definida em conjunto com Olá `analyzer` opção.</span><span class="sxs-lookup"><span data-stu-id="056a7-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="056a7-239">Este analisador pode ser atualizado num campo existente.</span><span class="sxs-lookup"><span data-stu-id="056a7-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="056a7-240">`indexAnalyzer`-Conjuntos Olá nome do analisador de Olá utilizada no momento de indexação para o campo de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="056a7-241">Para Olá permitido definido de valores consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="056a7-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="056a7-242">Esta opção pode ser utilizada apenas com `searchable` campos.</span><span class="sxs-lookup"><span data-stu-id="056a7-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="056a7-243">Tem de ser definido em conjunto com `searchAnalyzer` e não pode ser definida em conjunto com Olá `analyzer` opção.</span><span class="sxs-lookup"><span data-stu-id="056a7-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="056a7-244">Assim que for escolhido o analisador de Olá, não pode ser alterada para o campo de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="056a7-245">`suggesters`-Conjuntos Olá os campos que são Olá origem de conteúdo de Olá para sugestões e modo de procura.</span><span class="sxs-lookup"><span data-stu-id="056a7-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="056a7-246">Consulte [dos Sugestores](#Suggesters) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="056a7-247">`scoringProfiles`-Define personalizados comportamentos classificação que permitem-lhe influenciar os itens são apresentados nos resultados da pesquisa superiores.</span><span class="sxs-lookup"><span data-stu-id="056a7-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="056a7-248">Perfis de classificação são constituídos por funções e de peso de campo.</span><span class="sxs-lookup"><span data-stu-id="056a7-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="056a7-249">Consulte [adicionar perfis de classificação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter mais informações sobre os atributos de Olá utilizados num perfil de classificação.</span><span class="sxs-lookup"><span data-stu-id="056a7-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="056a7-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Suporte de idiomas**</span><span class="sxs-lookup"><span data-stu-id="056a7-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="056a7-251">Análise de sofrer de campos pesquisáveis que mais frequentemente envolve a quebra de palavra, normalização de texto e filtrar termos.</span><span class="sxs-lookup"><span data-stu-id="056a7-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="056a7-252">Por predefinição, os campos pesquisáveis na pesquisa do Azure são analisados com Olá [analisador Apache Lucene padrão](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) que quebras de texto em elementos seguir o["Segmentação de texto Unicode"](http://unicode.org/reports/tr29/) regras.</span><span class="sxs-lookup"><span data-stu-id="056a7-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="056a7-253">Além disso, o analisador padrão Olá converte todos os formulários de minúsculas de tootheir carateres.</span><span class="sxs-lookup"><span data-stu-id="056a7-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="056a7-254">Documentos indexados e os termos da procura percorrer analysis Olá durante a indexação e processamento de consultas.</span><span class="sxs-lookup"><span data-stu-id="056a7-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="056a7-255">A pesquisa do Azure suporta uma variedade de idiomas.</span><span class="sxs-lookup"><span data-stu-id="056a7-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="056a7-256">Cada idioma requer um analisador de texto não padrão que as contas do características de um determinado idioma.</span><span class="sxs-lookup"><span data-stu-id="056a7-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="056a7-257">A pesquisa do Azure oferece dois tipos de analisadores:</span><span class="sxs-lookup"><span data-stu-id="056a7-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="056a7-258">35 analisadores por Lucene.</span><span class="sxs-lookup"><span data-stu-id="056a7-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="056a7-259">50 analisadores por proprietária linguagem natural a Microsoft processamento tecnologia utilizada no Office e do Bing.</span><span class="sxs-lookup"><span data-stu-id="056a7-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="056a7-260">Alguns programadores poderão preferir Olá solução mais familiar, simple e open source do Lucene.</span><span class="sxs-lookup"><span data-stu-id="056a7-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="056a7-261">Analisadores de Lucene são mais rápidas, mas analisadores de Microsoft Olá avançaram capacidades, como lemmatization, word decompounding (em idiomas alemão, dinamarquês, neerlandês, sueco, norueguês, estónio, concluir, húngaro, Eslovaco) e de reconhecimento de entidade (URLs mensagens de correio eletrónico, datas, números).</span><span class="sxs-lookup"><span data-stu-id="056a7-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="056a7-262">Se for possível, deve executar comparações de ambos os Olá Microsoft e Lucene analisadores toodecide qual delas é uma opção melhor.</span><span class="sxs-lookup"><span data-stu-id="056a7-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="056a7-263">***A sua comparação***</span><span class="sxs-lookup"><span data-stu-id="056a7-263">***How they compare***</span></span>

<span data-ttu-id="056a7-264">Analisador de Lucene Olá para inglês expande o analisador de Olá padrão.</span><span class="sxs-lookup"><span data-stu-id="056a7-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="056a7-265">-Remove possessives (do à direita) palavras, aplica-se de que decorrentes como por [Porter decorrentes algoritmo](http://tartarus.org/~martin/PorterStemmer/)e remove inglês [parar palavras](http://en.wikipedia.org/wiki/Stop_words).</span><span class="sxs-lookup"><span data-stu-id="056a7-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="056a7-266">Em comparação, o analisador de Microsoft Olá efetua lemmatization em vez de decorrentes.</span><span class="sxs-lookup"><span data-stu-id="056a7-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="056a7-267">Significa que pode processar formulários word inflected e dados muito melhores o que resulta em mais relevantes resultados de pesquisa (módulo veja 7 de [apresentação da Azure Search MVA](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) para obter mais detalhes).</span><span class="sxs-lookup"><span data-stu-id="056a7-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="056a7-268">A indexação com analisadores de Microsoft em média é duas vezes toothree mais lentas do que os respetivos equivalentes de Lucene, consoante o idioma de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="056a7-269">Não deve ser afetado significativamente o desempenho de pesquisa para consultas de tamanho médio.</span><span class="sxs-lookup"><span data-stu-id="056a7-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="056a7-270">***Configuração***</span><span class="sxs-lookup"><span data-stu-id="056a7-270">***Configuration***</span></span>

<span data-ttu-id="056a7-271">Para cada campo na definição de índice de Olá, pode definir Olá `analyzer` tooan analisador nome da propriedade que especifica o idioma e o fornecedor.</span><span class="sxs-lookup"><span data-stu-id="056a7-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="056a7-272">Olá analisador mesmo será aplicada quando a indexação e procure-os para esse campo.</span><span class="sxs-lookup"><span data-stu-id="056a7-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="056a7-273">Por exemplo, pode ter campos separados para inglês, francês e espanhol átrios nas descrições que se existem lado lado a lado na Olá mesmo índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="056a7-274">Olá utilize [parâmetro de consulta 'searchFields'](#SearchQueryParameters) toospecify que toosearch específicas do idioma campo contra nas suas consultas.</span><span class="sxs-lookup"><span data-stu-id="056a7-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="056a7-275">Pode rever os exemplos de consultas que incluem Olá `analyzer` propriedade no [documentos sobre pesquisa](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="056a7-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="056a7-276">***Lista de analisador***</span><span class="sxs-lookup"><span data-stu-id="056a7-276">***Analyzer list***</span></span>

<span data-ttu-id="056a7-277">Segue-se uma lista de Olá de idiomas suportados, juntamente com os nomes de analisador Lucene e da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="056a7-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="056a7-278">Idioma</span><span class="sxs-lookup"><span data-stu-id="056a7-278">Language</span></span></th>
        <th><span data-ttu-id="056a7-279">Nome de analisador da Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="056a7-280">Nome do analisador de Lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-281">Árabe</span><span class="sxs-lookup"><span data-stu-id="056a7-281">Arabic</span></span></td>
        <td><span data-ttu-id="056a7-282">ar.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-284">Armenian</span><span class="sxs-lookup"><span data-stu-id="056a7-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="056a7-285">HY.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="056a7-286">Bangla</span><span class="sxs-lookup"><span data-stu-id="056a7-286">Bangla</span></span></td>
        <td><span data-ttu-id="056a7-287">Bn.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="056a7-288">Basco</span><span class="sxs-lookup"><span data-stu-id="056a7-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="056a7-289">eu.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="056a7-290">Búlgaro</span><span class="sxs-lookup"><span data-stu-id="056a7-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="056a7-291">BG.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-292">BG.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="056a7-293">Catalan</span><span class="sxs-lookup"><span data-stu-id="056a7-293">Catalan</span></span></td>
        <td><span data-ttu-id="056a7-294">CA.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-295">CA.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="056a7-296">Chinês simplificado</span><span class="sxs-lookup"><span data-stu-id="056a7-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="056a7-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-299">Chinês tradicional</span><span class="sxs-lookup"><span data-stu-id="056a7-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="056a7-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="056a7-302">Croata</span><span class="sxs-lookup"><span data-stu-id="056a7-302">Croatian</span></span></td>
        <td><span data-ttu-id="056a7-303">hr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-304">Checo</span><span class="sxs-lookup"><span data-stu-id="056a7-304">Czech</span></span></td>
        <td><span data-ttu-id="056a7-305">CS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-306">CS.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="056a7-307">Dinamarquês</span><span class="sxs-lookup"><span data-stu-id="056a7-307">Danish</span></span></td>
        <td><span data-ttu-id="056a7-308">da.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="056a7-310">Neerlandês</span><span class="sxs-lookup"><span data-stu-id="056a7-310">Dutch</span></span></td>
        <td><span data-ttu-id="056a7-311">NL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-312">NL.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="056a7-313">Português</span><span class="sxs-lookup"><span data-stu-id="056a7-313">English</span></span></td>        
        <td><span data-ttu-id="056a7-314">en.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-316">Estónio</span><span class="sxs-lookup"><span data-stu-id="056a7-316">Estonian</span></span></td>
        <td><span data-ttu-id="056a7-317">et.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-318">Finlandês</span><span class="sxs-lookup"><span data-stu-id="056a7-318">Finnish</span></span></td>
        <td><span data-ttu-id="056a7-319">Fi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-320">Fi.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="056a7-321">Francês</span><span class="sxs-lookup"><span data-stu-id="056a7-321">French</span></span></td>
        <td><span data-ttu-id="056a7-322">FR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-323">FR.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-324">Galician</span><span class="sxs-lookup"><span data-stu-id="056a7-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="056a7-325">GL.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="056a7-326">Alemão</span><span class="sxs-lookup"><span data-stu-id="056a7-326">German</span></span></td>
        <td><span data-ttu-id="056a7-327">de.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-329">Grego</span><span class="sxs-lookup"><span data-stu-id="056a7-329">Greek</span></span></td>
        <td><span data-ttu-id="056a7-330">EL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-331">EL.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-332">Gujarati</span><span class="sxs-lookup"><span data-stu-id="056a7-332">Gujarati</span></span></td>
        <td><span data-ttu-id="056a7-333">Gu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-334">Hebraico</span><span class="sxs-lookup"><span data-stu-id="056a7-334">Hebrew</span></span></td>
        <td><span data-ttu-id="056a7-335">he.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="056a7-336">Hindi</span></span></td>
        <td><span data-ttu-id="056a7-337">Hi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-338">Hi.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-339">Húngaro</span><span class="sxs-lookup"><span data-stu-id="056a7-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="056a7-340">HU.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-341">HU.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-342">Icelandic</span><span class="sxs-lookup"><span data-stu-id="056a7-342">Icelandic</span></span></td>
        <td><span data-ttu-id="056a7-343">is.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-344">Indonesian (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="056a7-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="056a7-345">ID.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-346">ID.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-347">Irish</span><span class="sxs-lookup"><span data-stu-id="056a7-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="056a7-348">GA.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-349">Italiano</span><span class="sxs-lookup"><span data-stu-id="056a7-349">Italian</span></span></td>
        <td><span data-ttu-id="056a7-350">IT.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-351">IT.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-352">Japonês</span><span class="sxs-lookup"><span data-stu-id="056a7-352">Japanese</span></span></td>
        <td><span data-ttu-id="056a7-353">ja.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="056a7-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="056a7-355">Kannada</span></span></td>
        <td><span data-ttu-id="056a7-356">Ka.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-357">Coreano</span><span class="sxs-lookup"><span data-stu-id="056a7-357">Korean</span></span></td>
        <td><span data-ttu-id="056a7-358">ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-360">Letão</span><span class="sxs-lookup"><span data-stu-id="056a7-360">Latvian</span></span></td>        
        <td><span data-ttu-id="056a7-361">LV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-362">LV.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-363">Lituano</span><span class="sxs-lookup"><span data-stu-id="056a7-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="056a7-364">lt.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-365">Malayalam</span><span class="sxs-lookup"><span data-stu-id="056a7-365">Malayalam</span></span></td>
        <td><span data-ttu-id="056a7-366">ml.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-367">Malaio (Latim)</span><span class="sxs-lookup"><span data-stu-id="056a7-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="056a7-368">MS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="056a7-369">Marathi</span></span></td>
        <td><span data-ttu-id="056a7-370">MR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-371">Norueguês</span><span class="sxs-lookup"><span data-stu-id="056a7-371">Norwegian</span></span></td>
        <td><span data-ttu-id="056a7-372">NB.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="056a7-374">Persian</span><span class="sxs-lookup"><span data-stu-id="056a7-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="056a7-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="056a7-376">Polaco</span><span class="sxs-lookup"><span data-stu-id="056a7-376">Polish</span></span></td>
        <td><span data-ttu-id="056a7-377">PL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-378">PL.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-379">Português (Brasil)</span><span class="sxs-lookup"><span data-stu-id="056a7-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="056a7-380">pt Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-381">pt Br.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-382">Português (Portugal)</span><span class="sxs-lookup"><span data-stu-id="056a7-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="056a7-383">pt Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="056a7-384">pt Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-385">Punjabi</span><span class="sxs-lookup"><span data-stu-id="056a7-385">Punjabi</span></span></td>
        <td><span data-ttu-id="056a7-386">Pa.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-387">Romeno</span><span class="sxs-lookup"><span data-stu-id="056a7-387">Romanian</span></span></td>
        <td><span data-ttu-id="056a7-388">ro.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-390">Russo</span><span class="sxs-lookup"><span data-stu-id="056a7-390">Russian</span></span></td>
        <td><span data-ttu-id="056a7-391">RU.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-392">RU.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-393">Sérvio (Cirílico)</span><span class="sxs-lookup"><span data-stu-id="056a7-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="056a7-394">SR-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-395">Sérvio (Latim)</span><span class="sxs-lookup"><span data-stu-id="056a7-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="056a7-396">SR-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-397">Eslovaco</span><span class="sxs-lookup"><span data-stu-id="056a7-397">Slovak</span></span></td>
        <td><span data-ttu-id="056a7-398">SK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-399">Esloveno</span><span class="sxs-lookup"><span data-stu-id="056a7-399">Slovenian</span></span></td>
        <td><span data-ttu-id="056a7-400">SL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-401">Espanhol</span><span class="sxs-lookup"><span data-stu-id="056a7-401">Spanish</span></span></td>
        <td><span data-ttu-id="056a7-402">es.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-404">Sueco</span><span class="sxs-lookup"><span data-stu-id="056a7-404">Swedish</span></span></td>
        <td><span data-ttu-id="056a7-405">SV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-406">SV.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="056a7-407">Tamil</span><span class="sxs-lookup"><span data-stu-id="056a7-407">Tamil</span></span></td>
        <td><span data-ttu-id="056a7-408">ta.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-409">Telugu</span><span class="sxs-lookup"><span data-stu-id="056a7-409">Telugu</span></span></td>
        <td><span data-ttu-id="056a7-410">te.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-411">Tailandês</span><span class="sxs-lookup"><span data-stu-id="056a7-411">Thai</span></span></td>
        <td><span data-ttu-id="056a7-412">TH.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-413">TH.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-414">Turco</span><span class="sxs-lookup"><span data-stu-id="056a7-414">Turkish</span></span></td>
        <td><span data-ttu-id="056a7-415">TR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="056a7-416">TR.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-417">Ucraniano</span><span class="sxs-lookup"><span data-stu-id="056a7-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="056a7-418">UK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="056a7-419">Urdu</span></span></td>
        <td><span data-ttu-id="056a7-420">your.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-421">Vietnamita</span><span class="sxs-lookup"><span data-stu-id="056a7-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="056a7-422">VI.Microsoft</span><span class="sxs-lookup"><span data-stu-id="056a7-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="056a7-423">Além disso pesquisa do Azure fornece configurações de analisador de idioma desconhecidas</span><span class="sxs-lookup"><span data-stu-id="056a7-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="056a7-424">Subconjunto de validação padrão ASCII</span><span class="sxs-lookup"><span data-stu-id="056a7-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="056a7-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="056a7-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="056a7-426">Segmentação de texto Unicode (atomizador padrão)</span><span class="sxs-lookup"><span data-stu-id="056a7-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="056a7-427">Filtro de subconjunto de validação ASCII - converte carateres Unicode, que não pertençam toohello conjunto primeiro 127 caracteres ASCII para os respetivos equivalentes de ASCII.</span><span class="sxs-lookup"><span data-stu-id="056a7-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="056a7-428">Isto é útil para remover diacritics.</span><span class="sxs-lookup"><span data-stu-id="056a7-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="056a7-429">Todos os analisadores com nomes anotados com <i>lucene</i> são utiliza a tecnologia de [analisadores de idiomas do Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="056a7-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="056a7-430">Podem encontrar mais informações sobre ASCII Olá subconjunto de validação do filtro [aqui](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="056a7-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="056a7-431">**Sugestões**</span><span class="sxs-lookup"><span data-stu-id="056a7-431">**Suggesters**</span></span>

<span data-ttu-id="056a7-432">A `suggester` define os campos num índice são utilizado toosupport a conclusão automática em procuras.</span><span class="sxs-lookup"><span data-stu-id="056a7-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="056a7-433">Normalmente, cadeias de procura parcial são enviadas toohello [sugestões API](#Suggestions) enquanto utilizador Olá é escrever uma consulta de pesquisa e Olá API devolve um conjunto de expressões sugeridos.</span><span class="sxs-lookup"><span data-stu-id="056a7-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="056a7-434">Um sugestor por si no índice Olá determina os campos são utilizados toobuild Olá pesquisa antecipada termos.</span><span class="sxs-lookup"><span data-stu-id="056a7-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="056a7-435">Consulte [dos Sugestores](#Suggesters) para detalhes de configuração.</span><span class="sxs-lookup"><span data-stu-id="056a7-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="056a7-436">**Perfis de classificação**</span><span class="sxs-lookup"><span data-stu-id="056a7-436">**Scoring profiles**</span></span>

<span data-ttu-id="056a7-437">A `scoringProfile` define personalizados comportamentos classificação que permitem-lhe influenciar quais os itens são apresentados nos resultados de pesquisa de Olá superiores.</span><span class="sxs-lookup"><span data-stu-id="056a7-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="056a7-438">Perfis de classificação são constituídos por funções e de peso de campo.</span><span class="sxs-lookup"><span data-stu-id="056a7-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="056a7-439">toouse-las, especifique um perfil de por nome na cadeia de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="056a7-440">Um perfil de classificação de predefinido funciona atrás Olá em segundo plano toocompute uma pontuação de pesquisa para cada item num conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="056a7-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="056a7-441">Pode utilizar o perfil de classificação interna, sem nome Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="056a7-442">Em alternativa, defina `defaultScoringProfile` toouse um perfil personalizado como predefinição de Olá, invocado sempre que um perfil personalizado não está especificado na cadeia de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="056a7-443">Consulte [Adicionar classificação perfis tooa índice de pesquisa (API do REST de serviço de pesquisa do Azure)](search-api-scoring-profiles-2015-02-28-preview.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="056a7-444">**Opções de CORS**</span><span class="sxs-lookup"><span data-stu-id="056a7-444">**CORS Options**</span></span>

<span data-ttu-id="056a7-445">Javascript do lado do cliente não é possível chamar as APIs por predefinição, uma vez que o browser Olá irá impedir que todos os pedidos de várias origens.</span><span class="sxs-lookup"><span data-stu-id="056a7-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="056a7-446">Ativar o CORS (transversal à partilha de recursos) por definição Olá `corsOptions` índice tooyour do atributo tooallow consultas de várias origens.</span><span class="sxs-lookup"><span data-stu-id="056a7-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="056a7-447">Tenha em atenção que apenas consulta o suporte APIs CORS por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="056a7-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="056a7-448">Olá seguintes opções pode ser definida para CORS:</span><span class="sxs-lookup"><span data-stu-id="056a7-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="056a7-449">`allowedOrigins`(obrigatório): Esta é uma lista de origens que será atribuído o índice de tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="056a7-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="056a7-450">Isto significa que qualquer código Javascript servido a partir destas origens será permitido tooquery seu índice (assumindo que é fornecida Olá chave de API correta).</span><span class="sxs-lookup"><span data-stu-id="056a7-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="056a7-451">Cada origem costuma formato Olá `protocol://fully-qualified-domain-name:port` embora porta Olá é frequentemente omitida.</span><span class="sxs-lookup"><span data-stu-id="056a7-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="056a7-452">Consulte [neste artigo](http://go.microsoft.com/fwlink/?LinkId=330822) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="056a7-453">Se pretender que as origens de tooall tooallow acesso, incluir `*` como um único item no Olá `allowedOrigins` matriz.</span><span class="sxs-lookup"><span data-stu-id="056a7-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="056a7-454">Tenha em atenção que **isto não é recomendado prática para serviços de pesquisa de produção.**</span><span class="sxs-lookup"><span data-stu-id="056a7-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="056a7-455">No entanto, poderá ser útil para programação ou para fins de depuração.</span><span class="sxs-lookup"><span data-stu-id="056a7-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="056a7-456">`maxAgeInSeconds`(opcional): os Browsers utilizam este valor toodetermine Olá duração (em segundos) toocache CORS prévias respostas.</span><span class="sxs-lookup"><span data-stu-id="056a7-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="056a7-457">Tem de ser um número inteiro não negativo.</span><span class="sxs-lookup"><span data-stu-id="056a7-457">This must be a non-negative integer.</span></span> <span data-ttu-id="056a7-458">Este valor é um melhor desempenho de Olá será maior Olá, mas Olá tempo demora para CORS política alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="056a7-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="056a7-459">Se não for definido, será utilizada uma duração predefinida de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="056a7-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="056a7-460"><a name="CreateUpdateIndexExample"></a>
**Exemplo de corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

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

<span data-ttu-id="056a7-461">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-461">**Response**</span></span>

<span data-ttu-id="056a7-462">Para um pedido com êxito: "criado 201".</span><span class="sxs-lookup"><span data-stu-id="056a7-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="056a7-463">Por predefinição o corpo da resposta Olá irá conter Olá JSON para a definição de índice de Olá que foi criada.</span><span class="sxs-lookup"><span data-stu-id="056a7-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="056a7-464">Se hello `Prefer` cabeçalho do pedido está definido demasiado`return=minimal`, o corpo da resposta Olá estará vazio e código de estado de êxito Olá "204 nenhum conteúdo" em vez de "criado 201".</span><span class="sxs-lookup"><span data-stu-id="056a7-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="056a7-465">Isto acontece independentemente se o PUT ou POST foi índice de Olá toocreate utilizados.</span><span class="sxs-lookup"><span data-stu-id="056a7-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="056a7-466">**Observações**</span><span class="sxs-lookup"><span data-stu-id="056a7-466">**Remarks**</span></span>

<span data-ttu-id="056a7-467">Atualmente, não há suporte limitado para atualizações do esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="056a7-468">As atualizações do esquema que necessitem de nova indexação, como a alteração de tipos de campo não são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="056a7-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="056a7-469">Embora os campos existentes não podem ser alterados ou eliminados, adicionar novos campos podem ser índice existente tooan em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="056a7-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="056a7-470">Quando é adicionado um novo campo, todos os documentos existentes no índice Olá terão automaticamente um valor nulo para esse campo.</span><span class="sxs-lookup"><span data-stu-id="056a7-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="056a7-471">Não existe espaço de armazenamento adicional será consumido até novos documentos serem adicionados toohello índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="056a7-472">Sugestões</span><span class="sxs-lookup"><span data-stu-id="056a7-472">Suggesters</span></span>
<span data-ttu-id="056a7-473">funcionalidade de sugestões de Olá na pesquisa do Azure é uma capacidade de consulta antecipada ou conclusão automática, que fornece uma lista de potenciais termos de pesquisa na resposta toopartial cadeia entradas introduzidos na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="056a7-474">Provavelmente já reparado sugestões de consulta ao utilizar os motores de busca web comerciais: escrever ".NET" no Bing produz uma lista dos termos de ".NET 4.5", ".NET Framework 3.5", etc.</span><span class="sxs-lookup"><span data-stu-id="056a7-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="056a7-475">Quando utilizar a REST API do serviço de pesquisa Olá, implementar sugestões numa aplicação personalizada da Azure Search necessita seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="056a7-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="056a7-476">Ativar as sugestões adicionando um **sugestor** construção no seu índice, dá ao nome de Olá, modo de procura e uma lista de campos para o qual antecipada é invocada.</span><span class="sxs-lookup"><span data-stu-id="056a7-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="056a7-477">Por exemplo, se especificar "cityName" como um campo de origem, escrevendo uma cadeia de pesquisa parcial de "Sea" resultará em "Seattle", "Seaside" e "Seatac" (todos os três nomes cidade real) oferecidas cópias de segurança como utilizador de toohello de sugestões de consulta.</span><span class="sxs-lookup"><span data-stu-id="056a7-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="056a7-478">Invocar sugestões ao chamar Olá [sugestões API](#Suggestions) no código da aplicação.</span><span class="sxs-lookup"><span data-stu-id="056a7-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="056a7-479">Normalmente, cadeias de procura parcial são enviadas toohello serviço enquanto utilizador Olá é escrever uma consulta de pesquisa e esta API devolve um conjunto de expressões sugeridos.</span><span class="sxs-lookup"><span data-stu-id="056a7-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="056a7-480">Este artigo explica como tooconfigure um **sugestor**.</span><span class="sxs-lookup"><span data-stu-id="056a7-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="056a7-481">Também deve rever Olá [sugestões API](#Suggestions) para obter detalhes sobre como um sugestor é utilizada.</span><span class="sxs-lookup"><span data-stu-id="056a7-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="056a7-482">**Utilização**</span><span class="sxs-lookup"><span data-stu-id="056a7-482">**Usage**</span></span>

<span data-ttu-id="056a7-483">`Suggesters`são criadas no índice Olá e funcionam melhor quando utilizado toosuggest específicos documentos em vez de termos soltas ou frases reconhecíveis.</span><span class="sxs-lookup"><span data-stu-id="056a7-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="056a7-484">os campos de candidatos melhor Olá são títulos, nomes e outras expressões relativamente curtos que podem identificar um item.</span><span class="sxs-lookup"><span data-stu-id="056a7-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="056a7-485">Campos repetitivos, tais como categorias e etiquetas, ou campos muito como campos de descrições ou comentários, são menos eficientes.</span><span class="sxs-lookup"><span data-stu-id="056a7-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="056a7-486">Como parte da definição de índice de Olá, pode adicionar um único sugestor toohello `suggesters` coleção.</span><span class="sxs-lookup"><span data-stu-id="056a7-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="056a7-487">Propriedades que definem uma sugestor incluem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="056a7-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="056a7-488">`name`: nome de Olá do sugestor Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="056a7-489">Utilizar nome Olá sugestor Olá ao chamar Olá `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="056a7-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="056a7-490">`searchMode`: Olá toosearch estratégia utilizada para expressões candidatas.</span><span class="sxs-lookup"><span data-stu-id="056a7-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="056a7-491">Olá único modo suportado atualmente é `analyzingInfixMatching`, que executa uma correspondência de expressões no início de Olá ou no meio de Olá das frases flexível.</span><span class="sxs-lookup"><span data-stu-id="056a7-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="056a7-492">`sourceFields`: Uma lista de um ou mais campos que são Olá origem de conteúdo de Olá de sugestões.</span><span class="sxs-lookup"><span data-stu-id="056a7-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="056a7-493">Apenas os campos do tipo `Edm.String` e `Collection(Edm.String)` poderá origens para sugestões.</span><span class="sxs-lookup"><span data-stu-id="056a7-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="056a7-494">Podem ser utilizados apenas os campos que não tenham um analisador de idioma personalizado definido.</span><span class="sxs-lookup"><span data-stu-id="056a7-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="056a7-495">**Exemplo de sugestor**</span><span class="sxs-lookup"><span data-stu-id="056a7-495">**Suggester Example**</span></span>

<span data-ttu-id="056a7-496">Um sugestor faz parte do índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-496">A suggester is part of hello index.</span></span> <span data-ttu-id="056a7-497">Pode existir apenas um sugestor no Olá `suggesters` coleção na versão atual Olá, juntamente com Olá campos de coleção e `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="056a7-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

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
> <span data-ttu-id="056a7-498">Se utilizou a versão de pré-visualização pública Olá da Azure Search, `suggesters` substitui uma propriedade booleana anterior (`"suggestions": false`) que só suportadas sugestões de prefixo para cadeias curtas (3-25 carateres).</span><span class="sxs-lookup"><span data-stu-id="056a7-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="056a7-499">A substituição, `suggesters`, suporta infix correspondente que encontra termos correspondentes no início de Olá ou no meio de Olá do conteúdo de campo, com tolerância a melhor para prende nas cadeias de procura.</span><span class="sxs-lookup"><span data-stu-id="056a7-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="056a7-500">A partir da versão geralmente disponível Olá, isto é agora Olá única implementação de sugestões de Olá API.</span><span class="sxs-lookup"><span data-stu-id="056a7-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="056a7-501">Olá mais antigo `suggestions` propriedade que foi introduzida no `api-version=2014-07-31-Preview` continua toowork em que a versão, mas não está operacional em Olá `2015-02-28` ou versões posteriores de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="056a7-502">Atualizar o índice</span><span class="sxs-lookup"><span data-stu-id="056a7-502">Update Index</span></span>
<span data-ttu-id="056a7-503">Pode atualizar um índice existente na Azure Search utilizando um pedido HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="056a7-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="056a7-504">As atualizações podem incluir a adicionar novos campos toohello existente esquema, modificar opções de CORS e modificar perfis de classificação.</span><span class="sxs-lookup"><span data-stu-id="056a7-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="056a7-505">Consulte [adicionar perfis de classificação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="056a7-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="056a7-506">Especifique o nome Olá Olá índice tooupdate no URI do pedido de Olá:</span><span class="sxs-lookup"><span data-stu-id="056a7-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="056a7-507">**Importante:** suporte para atualizações do esquema de índice é limitado toooperations que não necessitam de reconstruir o índice de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="056a7-508">As atualizações do esquema que necessitem de uma reindexação, tal como alterar os tipos de campo, não são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="056a7-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="056a7-509">É possível adicionar novos campos em qualquer altura, embora os campos existentes não podem ser alterados ou eliminados.</span><span class="sxs-lookup"><span data-stu-id="056a7-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="056a7-510">Olá mesmo se aplica demasiado`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="056a7-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="056a7-511">É possível adicionar novos campos tooa sugestor em campos de Olá Olá tempo são adicionados, mas não não possível remover os campos `suggesters` e os campos existentes não não possível adicionar demasiado`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="056a7-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="056a7-512">Ao adicionar um novo campo tooan o índice, todos os documentos existentes no índice Olá terão automaticamente um valor nulo para esse campo.</span><span class="sxs-lookup"><span data-stu-id="056a7-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="056a7-513">Não existe espaço de armazenamento adicional será consumido até novos documentos serem adicionados toohello índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="056a7-514">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-514">**Request**</span></span>

<span data-ttu-id="056a7-515">HTTPS é necessário para todos os pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="056a7-516">Olá **atualização índice** pedido é construído através de HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="056a7-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="056a7-517">Com PUT, o nome do índice Olá faz parte do URL de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="056a7-518">Se não existir índice Olá, é criado.</span><span class="sxs-lookup"><span data-stu-id="056a7-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="056a7-519">Se já existe um índice de Olá, é atualizado toohello nova definição.</span><span class="sxs-lookup"><span data-stu-id="056a7-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="056a7-520">o nome do índice Olá tem de ter minúsculas, começar com uma letra ou número, ter nenhum barras ou pontos e de ter menos de 128 carateres.</span><span class="sxs-lookup"><span data-stu-id="056a7-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="056a7-521">Depois de iniciar o nome do índice Olá com uma letra ou número, rest Olá do nome de Olá pode incluir qualquer letra, o número e travessões, desde que os traços Olá não estão consecutivos.</span><span class="sxs-lookup"><span data-stu-id="056a7-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="056a7-522">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-523">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-524">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-525">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-525">**Request Headers**</span></span>

<span data-ttu-id="056a7-526">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-527">`Content-Type`: Necessário.</span><span class="sxs-lookup"><span data-stu-id="056a7-527">`Content-Type`: Required.</span></span> <span data-ttu-id="056a7-528">Defina esta opção demasiado`application/json`</span><span class="sxs-lookup"><span data-stu-id="056a7-528">Set this too`application/json`</span></span>
* <span data-ttu-id="056a7-529">`api-key`: Necessário.</span><span class="sxs-lookup"><span data-stu-id="056a7-529">`api-key`: Required.</span></span> <span data-ttu-id="056a7-530">Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-531">É um valor de cadeia, o serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="056a7-532">Olá **atualização índice** pedido tem de incluir um `api-key` cabeçalho definir a chave de administrador tooyour (como chave de consulta tooa oposição ao).</span><span class="sxs-lookup"><span data-stu-id="056a7-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="056a7-533">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-534">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-535">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-536">**Sintaxe de corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-536">**Request Body Syntax**</span></span>

<span data-ttu-id="056a7-537">Ao atualizar um índice existente, corpo Olá tem de incluir definição de esquema original Olá, mais campos novos Olá que estiver a adicionar, bem como Olá modificado perfis de classificação, dos sugestores e opções de CORS, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="056a7-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="056a7-538">Se não modifica os perfis de classificação de Olá e opções de CORS, tem de incluir originals Olá do quando o índice de Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="056a7-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="056a7-539">Em geral Olá melhor padrão toouse atualizações é a definição do índice Olá tooretrieve com uma ação obter, modificá-lo e, em seguida, atualizá-lo com PUT.</span><span class="sxs-lookup"><span data-stu-id="056a7-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="056a7-540">utilizada a sintaxe de esquema Olá toocreate que um índice é reproduzido aqui para sua comodidade.</span><span class="sxs-lookup"><span data-stu-id="056a7-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="056a7-541">Consulte [Create Index](#CreateIndex) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-541">See [Create Index](#CreateIndex) for more details.</span></span>

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


<span data-ttu-id="056a7-542">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-542">**Response**</span></span>

<span data-ttu-id="056a7-543">Para um pedido com êxito: "204 nenhum conteúdo".</span><span class="sxs-lookup"><span data-stu-id="056a7-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="056a7-544">Por predefinição o corpo da resposta Olá estará vazio.</span><span class="sxs-lookup"><span data-stu-id="056a7-544">By default hello response body will be empty.</span></span> <span data-ttu-id="056a7-545">No entanto, se hello `Prefer` cabeçalho do pedido está definido demasiado`return=representation`, corpo da resposta Olá irá conter Olá JSON para a definição de índice de Olá que foi atualizada.</span><span class="sxs-lookup"><span data-stu-id="056a7-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="056a7-546">Neste caso, o código de estado de êxito de Olá será "200 OK".</span><span class="sxs-lookup"><span data-stu-id="056a7-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="056a7-547">**Atualizar a definição do índice com analisadores personalizados**</span><span class="sxs-lookup"><span data-stu-id="056a7-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="056a7-548">Quando está definido uma analyzer, um atomizador, um filtro de token ou um filtro de char, não pode ser modificado.</span><span class="sxs-lookup"><span data-stu-id="056a7-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="056a7-549">Novos podem ser adicionados índice existente tooan apenas se hello `allowIndexDowntime` sinalizador é definido tootrue no pedido de actualização do índice Olá:</span><span class="sxs-lookup"><span data-stu-id="056a7-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="056a7-550">Tenha em atenção que esta operação irá colocar o índice offline para, pelo menos, alguns segundos, fazendo com que a indexação e consulta pedidos toofail.</span><span class="sxs-lookup"><span data-stu-id="056a7-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="056a7-551">Disponibilidade de desempenho e de escrita do índice de Olá pode ser afetada durante vários minutos após a atualização do índice de Olá ou superior para índices muito grande.</span><span class="sxs-lookup"><span data-stu-id="056a7-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="056a7-552">Índices de lista</span><span class="sxs-lookup"><span data-stu-id="056a7-552">List Indexes</span></span>
<span data-ttu-id="056a7-553">Olá **lista índices** operação devolve uma lista de índices de Olá atualmente no seu serviço da Azure Search.</span><span class="sxs-lookup"><span data-stu-id="056a7-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="056a7-554">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-554">**Request**</span></span>

<span data-ttu-id="056a7-555">HTTPS é necessário para todos os pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="056a7-556">Olá **lista índices** pedido pode ser construído com o método GET de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="056a7-557">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-558">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-559">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-560">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-560">**Request Headers**</span></span>

<span data-ttu-id="056a7-561">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-562">`api-key`: Necessário.</span><span class="sxs-lookup"><span data-stu-id="056a7-562">`api-key`: Required.</span></span> <span data-ttu-id="056a7-563">Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-564">É um valor de cadeia, o serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="056a7-565">Olá **lista índices** pedido tem de incluir um `api-key` conjunto tooan chave de administração (como chave de consulta tooa oposição ao).</span><span class="sxs-lookup"><span data-stu-id="056a7-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="056a7-566">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-567">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-568">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-569">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-569">**Request Body**</span></span>

<span data-ttu-id="056a7-570">nenhum.</span><span class="sxs-lookup"><span data-stu-id="056a7-570">None.</span></span>

<span data-ttu-id="056a7-571">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-571">**Response**</span></span>

<span data-ttu-id="056a7-572">Código de estado: 200 OK é devolvido para uma resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="056a7-573">Eis um corpo de resposta de exemplo:</span><span class="sxs-lookup"><span data-stu-id="056a7-573">Here is an example response body:</span></span>

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

<span data-ttu-id="056a7-574">Tenha em atenção que pode filtrar resposta Olá baixo propriedades de Olá toojust que estiver interessado em.</span><span class="sxs-lookup"><span data-stu-id="056a7-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="056a7-575">Por exemplo, se pretender que apenas uma lista de nomes de índice, utilizar Olá OData `$select` opção de consulta:</span><span class="sxs-lookup"><span data-stu-id="056a7-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="056a7-576">Neste caso, resposta de Olá do Olá acima exemplo deverá aparecer da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="056a7-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="056a7-577">Esta é uma largura de banda de toosave técnica útil se tiver muitos dos índices no serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="056a7-578">Obter o índice</span><span class="sxs-lookup"><span data-stu-id="056a7-578">Get Index</span></span>
<span data-ttu-id="056a7-579">Olá **obter índice** operação obtém a definição de índice de Olá da Azure Search.</span><span class="sxs-lookup"><span data-stu-id="056a7-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="056a7-580">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-580">**Request**</span></span>

<span data-ttu-id="056a7-581">HTTPS é necessário para pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="056a7-582">Olá **obter índice** pedido pode ser construído com o método GET de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="056a7-583">Olá [nome do índice] no URI de pedido de Olá Especifica qual tooreturn de índice da coleção de índices de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="056a7-584">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-585">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-586">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-587">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-587">**Request Headers**</span></span>

<span data-ttu-id="056a7-588">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-589">`api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-590">É um valor de cadeia, o serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="056a7-591">Olá **obter índice** pedido tem de incluir um `api-key` conjunto tooan chave de administração (como chave de consulta tooa oposição ao).</span><span class="sxs-lookup"><span data-stu-id="056a7-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="056a7-592">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-593">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-594">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-595">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-595">**Request Body**</span></span>

<span data-ttu-id="056a7-596">nenhum.</span><span class="sxs-lookup"><span data-stu-id="056a7-596">None.</span></span>

<span data-ttu-id="056a7-597">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-597">**Response**</span></span>

<span data-ttu-id="056a7-598">Código de estado: 200 OK é devolvido para uma resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="056a7-599">Consulte o exemplo de Olá JSON no [criando e atualizando um índice](#CreateUpdateIndexExample) para obter um exemplo de Olá de respostas o payload.</span><span class="sxs-lookup"><span data-stu-id="056a7-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="056a7-600">Eliminar o índice</span><span class="sxs-lookup"><span data-stu-id="056a7-600">Delete Index</span></span>
<span data-ttu-id="056a7-601">Olá **eliminar índice** operação remove um índice e os documentos associados do seu serviço da Azure Search.</span><span class="sxs-lookup"><span data-stu-id="056a7-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="056a7-602">Pode obter o nome do índice Olá de dashboard de serviço de Olá no Olá portal do Azure ou de Olá API.</span><span class="sxs-lookup"><span data-stu-id="056a7-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="056a7-603">Consulte [lista índices](#ListIndexes) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="056a7-604">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-604">**Request**</span></span>

<span data-ttu-id="056a7-605">HTTPS é necessário para pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="056a7-606">Olá **eliminar índice** pedido pode ser construído com o método DELETE de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="056a7-607">Olá [nome do índice] no URI de pedido de Olá Especifica qual toodelete de índice da coleção de índices de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="056a7-608">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-609">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-610">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-611">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-611">**Request Headers**</span></span>

<span data-ttu-id="056a7-612">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-613">`api-key`: Necessário.</span><span class="sxs-lookup"><span data-stu-id="056a7-613">`api-key`: Required.</span></span> <span data-ttu-id="056a7-614">Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-615">É um valor de cadeia, o URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="056a7-616">Olá **eliminar índice** pedido tem de incluir um `api-key` cabeçalho definir a chave de administrador tooyour (como chave de consulta tooa oposição ao).</span><span class="sxs-lookup"><span data-stu-id="056a7-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="056a7-617">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-618">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-619">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-620">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-620">**Request Body**</span></span>

<span data-ttu-id="056a7-621">nenhum.</span><span class="sxs-lookup"><span data-stu-id="056a7-621">None.</span></span>

<span data-ttu-id="056a7-622">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-622">**Response**</span></span>

<span data-ttu-id="056a7-623">Código de estado: 204 conteúdo não é devolvido para uma resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="056a7-624">Obter estatísticas de índice</span><span class="sxs-lookup"><span data-stu-id="056a7-624">Get Index Statistics</span></span>
<span data-ttu-id="056a7-625">Olá **obter estatísticas de índice** operação devolve da Azure Search, uma contagem de documentos para o índice atual Olá, mais a utilização do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="056a7-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="056a7-626">Estatísticas de documento contagem e tamanho de armazenamento são recolhidas a cada alguns minutos, não em tempo real.</span><span class="sxs-lookup"><span data-stu-id="056a7-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="056a7-627">Por conseguinte, as estatísticas de Olá devolvidas por esta API podem não refletir alterações causado por operações de indexação recentes.</span><span class="sxs-lookup"><span data-stu-id="056a7-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="056a7-628">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-628">**Request**</span></span>

<span data-ttu-id="056a7-629">HTTPS é necessário para todos os pedidos de serviços.</span><span class="sxs-lookup"><span data-stu-id="056a7-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="056a7-630">Olá **obter estatísticas de índice** pedido pode ser construído com o método GET de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="056a7-631">Olá [nome do índice] no URI de pedido de Olá indica Olá serviço tooreturn índice as estatísticas de índice especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="056a7-632">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-633">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-634">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-635">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-635">**Request Headers**</span></span>

<span data-ttu-id="056a7-636">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-637">`api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-638">É um valor de cadeia, o serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="056a7-639">Olá **obter estatísticas de índice** pedido tem de incluir um `api-key` conjunto tooan chave de administração (como chave de consulta tooa oposição ao).</span><span class="sxs-lookup"><span data-stu-id="056a7-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="056a7-640">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-641">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-642">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-643">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-643">**Request Body**</span></span>

<span data-ttu-id="056a7-644">nenhum.</span><span class="sxs-lookup"><span data-stu-id="056a7-644">None.</span></span>

<span data-ttu-id="056a7-645">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-645">**Response**</span></span>

<span data-ttu-id="056a7-646">Código de estado: 200 OK é devolvido para uma resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="056a7-647">corpo da resposta Olá está a ser Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="056a7-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="056a7-648">Analisador de teste</span><span class="sxs-lookup"><span data-stu-id="056a7-648">Test Analyzer</span></span>
<span data-ttu-id="056a7-649">Olá **analisar API** mostra como um analisador de quebras de texto em tokens.</span><span class="sxs-lookup"><span data-stu-id="056a7-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="056a7-650">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-650">**Request**</span></span>

<span data-ttu-id="056a7-651">HTTPS é necessário para todos os pedidos de serviços.</span><span class="sxs-lookup"><span data-stu-id="056a7-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="056a7-652">Olá **analisar API** pedido pode ser construído com o método POST de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="056a7-653">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-654">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-655">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-656">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-656">**Request Headers**</span></span>

<span data-ttu-id="056a7-657">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-658">`api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-659">É um valor de cadeia, o serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="056a7-660">Olá **analisar API** pedido tem de incluir um `api-key` conjunto tooan chave de administração (como chave de consulta tooa oposição ao).</span><span class="sxs-lookup"><span data-stu-id="056a7-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="056a7-661">Também terá do nome do índice Olá e Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-662">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-663">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-664">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="056a7-665">ou</span><span class="sxs-lookup"><span data-stu-id="056a7-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="056a7-666">Olá `analyzer_name`, `tokenizer_name`, `token_filter_name` e `char_filter_name` necessário toobe nomes válidos de analisadores de predefinidos ou personalizados, tokenizers, filtros de token e filtros de char para o índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="056a7-667">toolearn mais informações sobre o processo de Olá de análise lexical consulte [análise na Azure Search](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="056a7-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="056a7-668">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-668">**Response**</span></span>

<span data-ttu-id="056a7-669">Código de estado: 200 OK é devolvido para uma resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="056a7-670">corpo da resposta Olá está a ser Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="056a7-670">hello response body is in hello following format:</span></span>

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

<span data-ttu-id="056a7-671">**Analisar o exemplo de API**</span><span class="sxs-lookup"><span data-stu-id="056a7-671">**Analyze API example**</span></span>

<span data-ttu-id="056a7-672">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="056a7-673">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-673">**Response**</span></span>

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

## <a name="document-operations"></a><span data-ttu-id="056a7-674">Operações do documento</span><span class="sxs-lookup"><span data-stu-id="056a7-674">Document Operations</span></span>
<span data-ttu-id="056a7-675">Na Azure Search, um índice é armazenado na nuvem de Olá e povoar utilizando documentos JSON que carregar toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="056a7-676">Todos os documentos de Olá que carregar é constituída por corpus Olá dos seus dados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="056a7-677">Documentos contêm campos, algumas das quais são com token em termos de pesquisa que são carregados.</span><span class="sxs-lookup"><span data-stu-id="056a7-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="056a7-678">Olá `/docs` segmento de URL no Olá API da Azure Search representa a coleção de Olá de documentos num índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="056a7-679">Todas as operações executadas numa coleção de Olá como carregar, intercalar, eliminar ou consultar documentos ocorrer no contexto de Olá de um índice único, por isso, Olá URLs para estas operações serão sempre começar a utilizar `/indexes/[index name]/docs` para um nome de índice fornecido.</span><span class="sxs-lookup"><span data-stu-id="056a7-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="056a7-680">O código da aplicação ou tem de gerar JSON documentos tooupload tooAzure pesquisa ou pode utilizar um [indexador](https://msdn.microsoft.com/library/dn946891.aspx) tooload documentos se a origem de dados de Olá é a SQL Database do Azure ou a base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="056a7-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="056a7-681">Normalmente, são povoados índices de um único conjunto de dados que fornecer.</span><span class="sxs-lookup"><span data-stu-id="056a7-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="056a7-682">Deve planear ter um documento para cada item que pretende que o toosearch.</span><span class="sxs-lookup"><span data-stu-id="056a7-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="056a7-683">Uma aplicação de rental filmes pode ter um documento por filmes, uma aplicação storefront pode ter um documento por SKU, uma aplicação online courseware pode ter um documento por decorrer, um firm de pesquisa pode ter um documento para cada documento académico no respetivo repositório e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="056a7-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="056a7-684">Documentos é constituída por um ou mais campos.</span><span class="sxs-lookup"><span data-stu-id="056a7-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="056a7-685">Campos podem conter texto que é atomizado pela pesquisa do Azure em termos de pesquisa, bem como não atomizada ou valores de texto não podem ser utilizados em filtros ou perfis de classificação.</span><span class="sxs-lookup"><span data-stu-id="056a7-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="056a7-686">Olá nomes, tipos de dados e as funcionalidades de pesquisa são suportadas para cada campo são determinadas pelo esquema de índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="056a7-687">Um dos campos de Olá cada esquema de índice tem de ser designado como um ID e cada documento tem de ter um valor para o campo de ID de Olá que identifica exclusivamente esse documento no índice Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="056a7-688">Todos os outros campos de documento são opcionais e serão predefinido tooa um valor nulo se especificado.</span><span class="sxs-lookup"><span data-stu-id="056a7-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="056a7-689">Tenha em atenção que os valores nulos não demorar até espaço no índice de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="056a7-690">Antes de pode carregar documentos, deve já tiver criado o índice de Olá no serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="056a7-691">Consulte [Create Index](#CreateIndex) para obter detalhes sobre neste primeiro passo.</span><span class="sxs-lookup"><span data-stu-id="056a7-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="056a7-692">Adicionar, atualizar, ou eliminar documentos</span><span class="sxs-lookup"><span data-stu-id="056a7-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="056a7-693">Pode carregar, documentos de intercalação, intercalação ou carregamento ou eliminação de um índice especificado utilizando o HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="056a7-694">Para grandes quantidades de atualizações, a criação de batches de documentos (too1000 documentos por lote) ou cerca de 16 MB por lote é recomendada.</span><span class="sxs-lookup"><span data-stu-id="056a7-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="056a7-695">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-695">**Request**</span></span>

<span data-ttu-id="056a7-696">HTTPS é necessário para todos os pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="056a7-697">Pode carregar, documentos de intercalação, intercalação ou carregamento ou eliminação de um índice especificado utilizando o HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="056a7-698">pedido de Olá URI inclui [nome do índice], especificando os documentos de toopost do índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="056a7-699">Só pode publicar o índice de tooone documentos cada vez.</span><span class="sxs-lookup"><span data-stu-id="056a7-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="056a7-700">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-701">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-702">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-703">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-703">**Request Headers**</span></span>

<span data-ttu-id="056a7-704">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-705">`Content-Type`: Necessário.</span><span class="sxs-lookup"><span data-stu-id="056a7-705">`Content-Type`: Required.</span></span> <span data-ttu-id="056a7-706">Defina esta opção demasiado`application/json`</span><span class="sxs-lookup"><span data-stu-id="056a7-706">Set this too`application/json`</span></span>
* <span data-ttu-id="056a7-707">`api-key`: Necessário.</span><span class="sxs-lookup"><span data-stu-id="056a7-707">`api-key`: Required.</span></span> <span data-ttu-id="056a7-708">Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-709">É um valor de cadeia, o serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="056a7-710">Olá **adicionar documentos** pedido tem de incluir um `api-key` cabeçalho definir a chave de administrador tooyour (como chave de consulta tooa oposição ao).</span><span class="sxs-lookup"><span data-stu-id="056a7-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="056a7-711">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-712">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-713">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-714">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-714">**Request Body**</span></span>

<span data-ttu-id="056a7-715">corpo de Olá de pedido de Olá contém um ou mais documentos toobe indexada.</span><span class="sxs-lookup"><span data-stu-id="056a7-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="056a7-716">Documentos são identificados por uma chave exclusiva.</span><span class="sxs-lookup"><span data-stu-id="056a7-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="056a7-717">Cada documento está associado uma ação: carregar, intercalação, mergeOrUpload ou delete.</span><span class="sxs-lookup"><span data-stu-id="056a7-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="056a7-718">Os pedidos de carregamento tem de incluir dados de documento Olá como um conjunto de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="056a7-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

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
> <span data-ttu-id="056a7-719">Chaves de documento só podem conter letras, números, travessões ("-"), carateres de sublinhado ("_") e sinais de igual ("=").</span><span class="sxs-lookup"><span data-stu-id="056a7-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="056a7-720">Para obter mais detalhes, consulte [regras de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="056a7-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="056a7-721">**Ações de documentos**</span><span class="sxs-lookup"><span data-stu-id="056a7-721">**Document Actions**</span></span>

* <span data-ttu-id="056a7-722">`upload`: Uma ação de carregamento é semelhante tooan "upsert" onde o documento de Olá será inserido se for novo e atualizado/substituído se já existir.</span><span class="sxs-lookup"><span data-stu-id="056a7-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="056a7-723">Tenha em atenção de que todos os campos são substituídos no caso de atualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="056a7-724">`merge`: Atualizações intercalação existente documento com Olá especificado campos.</span><span class="sxs-lookup"><span data-stu-id="056a7-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="056a7-725">Se não existir documento Olá, intercalação Olá irá falhar.</span><span class="sxs-lookup"><span data-stu-id="056a7-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="056a7-726">Qualquer campo que especifique numa intercalação irá substituir o campo existente do Olá documento Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="056a7-727">Isto inclui campos do tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="056a7-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="056a7-728">Por exemplo, se hello o documento contém um campo "etiquetas" com o valor `["budget"]` e executar uma intercalação com valor `["economy", "pool"]` para "etiquetas", o valor final do Olá do campo de etiquetas"Olá" será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="056a7-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="056a7-729">Este irá **não** ser `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="056a7-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="056a7-730">`mergeOrUpload`: tem o mesmo comportamento `merge` caso um documento com Olá fornecido chave já exista no índice Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="056a7-731">Se o documento de Olá não existir, tem o mesmo comportamento `upload` com um novo documento.</span><span class="sxs-lookup"><span data-stu-id="056a7-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="056a7-732">`delete`: Eliminar remove o documento especificado Olá desde o índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="056a7-733">Tenha em atenção que quaisquer campos que especificar num `delete` operação que não seja o campo de chave Olá será ignorada.</span><span class="sxs-lookup"><span data-stu-id="056a7-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="056a7-734">Se pretender tooremove um campo individual de um documento, utilize `merge` em vez disso e simplesmente defina o campo de Olá explicitamente demasiado`null`.</span><span class="sxs-lookup"><span data-stu-id="056a7-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="056a7-735">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-735">**Response**</span></span>

<span data-ttu-id="056a7-736">Código de estado 200 (OK) é devolvido para uma resposta com êxito, o que significa que todos os itens têm indexados com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="056a7-737">Esta situação é indicada pelo Olá `status` propriedade que está a ser definida tootrue para todos os itens, bem como Olá `statusCode` propriedade que está a ser definida tooeither 201 (para documentos recentemente carregados) ou 200 (para documentos intercalados ou eliminados):</span><span class="sxs-lookup"><span data-stu-id="056a7-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

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

<span data-ttu-id="056a7-738">Código de estado 207 (estado multi) é devolvido quando pelo menos um item não foi indexado com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="056a7-739">Os itens que não foi indexados têm Olá `status` toofalse de conjunto de campos.</span><span class="sxs-lookup"><span data-stu-id="056a7-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="056a7-740">Olá `errorMessage` e `statusCode` propriedades irão indicar o motivo Olá Olá indexação de erro:</span><span class="sxs-lookup"><span data-stu-id="056a7-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

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

<span data-ttu-id="056a7-741">Olá, a tabela seguinte explica Olá várias por documento códigos de estado que podem ser devolvidos na resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="056a7-742">Tenha em atenção que alguns indicam problemas com o pedido de Olá, enquanto outros indicam condições de erro temporário.</span><span class="sxs-lookup"><span data-stu-id="056a7-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="056a7-743">última dos Olá que deve repetir após um atraso.</span><span class="sxs-lookup"><span data-stu-id="056a7-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="056a7-744">Código de estado</span><span class="sxs-lookup"><span data-stu-id="056a7-744">Status code</span></span></th>
        <th><span data-ttu-id="056a7-745">Significado</span><span class="sxs-lookup"><span data-stu-id="056a7-745">Meaning</span></span></th>
        <th><span data-ttu-id="056a7-746">Repetição</span><span class="sxs-lookup"><span data-stu-id="056a7-746">Retryable</span></span></th>
        <th><span data-ttu-id="056a7-747">Notas</span><span class="sxs-lookup"><span data-stu-id="056a7-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-748">200</span><span class="sxs-lookup"><span data-stu-id="056a7-748">200</span></span></td>
        <td><span data-ttu-id="056a7-749">Documento com êxito foi modificado ou eliminado.</span><span class="sxs-lookup"><span data-stu-id="056a7-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="056a7-750">n/d</span><span class="sxs-lookup"><span data-stu-id="056a7-750">n/a</span></span></td>
        <td><span data-ttu-id="056a7-751">Eliminar operações são <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="056a7-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="056a7-752">Ou seja, mesmo se uma chave de documento não existe no índice Olá, tentar uma operação de eliminação com essa chave resultará num código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="056a7-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-753">201</span><span class="sxs-lookup"><span data-stu-id="056a7-753">201</span></span></td>
        <td><span data-ttu-id="056a7-754">Documento foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="056a7-755">n/d</span><span class="sxs-lookup"><span data-stu-id="056a7-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-756">400</span><span class="sxs-lookup"><span data-stu-id="056a7-756">400</span></span></td>
        <td><span data-ttu-id="056a7-757">Ocorreu um erro no documento de Olá que impediu que está a ser indexado.</span><span class="sxs-lookup"><span data-stu-id="056a7-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="056a7-758">Não</span><span class="sxs-lookup"><span data-stu-id="056a7-758">No</span></span></td>
        <td><span data-ttu-id="056a7-759">mensagem de erro de saudação na resposta Olá indicará que está errado documento Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-760">404</span><span class="sxs-lookup"><span data-stu-id="056a7-760">404</span></span></td>
        <td><span data-ttu-id="056a7-761">Não foi possível intercalar o documento de Olá porque Olá fornecida a chave não existe no índice Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="056a7-762">Não</span><span class="sxs-lookup"><span data-stu-id="056a7-762">No</span></span></td>
        <td><span data-ttu-id="056a7-763">Este erro não ocorrer para carregamentos, uma vez que criarem novos documentos e não ocorre para eliminações por estarem <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="056a7-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-764">409</span><span class="sxs-lookup"><span data-stu-id="056a7-764">409</span></span></td>
        <td><span data-ttu-id="056a7-765">Foi detetado um conflito de versões durante a tentativa de tooindex um documento.</span><span class="sxs-lookup"><span data-stu-id="056a7-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="056a7-766">Sim</span><span class="sxs-lookup"><span data-stu-id="056a7-766">Yes</span></span></td>
        <td><span data-ttu-id="056a7-767">Isto pode acontecer quando está a tentar Olá tooindex mesmo documento mais do que uma vez em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="056a7-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-768">422</span><span class="sxs-lookup"><span data-stu-id="056a7-768">422</span></span></td>
        <td><span data-ttu-id="056a7-769">índice de Olá está temporariamente indisponível porque este foi atualizado com too'true de conjunto de sinalizador Olá 'allowIndexDowntime' '.</span><span class="sxs-lookup"><span data-stu-id="056a7-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="056a7-770">Sim</span><span class="sxs-lookup"><span data-stu-id="056a7-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="056a7-771">503</span><span class="sxs-lookup"><span data-stu-id="056a7-771">503</span></span></td>
        <td><span data-ttu-id="056a7-772">O serviço de pesquisa está temporariamente indisponível, possivelmente devido a carga de tooheavy.</span><span class="sxs-lookup"><span data-stu-id="056a7-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="056a7-773">Sim</span><span class="sxs-lookup"><span data-stu-id="056a7-773">Yes</span></span></td>
        <td><span data-ttu-id="056a7-774">O código deve aguardar antes de repetir neste caso, ou o risco de indisponibilidade do serviço de Olá de prolonging.</span><span class="sxs-lookup"><span data-stu-id="056a7-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="056a7-775">**Tenha em atenção**: se o código de cliente frequentemente encontra uma resposta 207, uma razão possível é a que o sistema de Olá está sob carga.</span><span class="sxs-lookup"><span data-stu-id="056a7-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="056a7-776">Pode confirmar isto verificando Olá `statusCode` propriedade 503.</span><span class="sxs-lookup"><span data-stu-id="056a7-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="056a7-777">Se for este caso de Olá, recomendamos que ***limitação de pedidos de indexação***.</span><span class="sxs-lookup"><span data-stu-id="056a7-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="056a7-778">Caso contrário, se o tráfego de indexação não subside, sistema Olá foi possível iniciar a rejeitar todos os pedidos com 503 erros.</span><span class="sxs-lookup"><span data-stu-id="056a7-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="056a7-779">Código de estado 429 indica que excedeu a quota no número de Olá de documentos por índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="056a7-780">Tem de criar um índice novo ou atualizar para os limites de capacidade superiores.</span><span class="sxs-lookup"><span data-stu-id="056a7-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="056a7-781">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="056a7-781">**Example:**</span></span>

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

## <a name="search-documents"></a><span data-ttu-id="056a7-782">Documentos sobre pesquisa</span><span class="sxs-lookup"><span data-stu-id="056a7-782">Search Documents</span></span>
<span data-ttu-id="056a7-783">A **pesquisa** operação é emitida como um pedido GET ou POST e especifica os parâmetros que forneça critérios Olá para selecionar documentos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="056a7-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="056a7-784">**Quando publicar toouse em vez de obter**</span><span class="sxs-lookup"><span data-stu-id="056a7-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="056a7-785">Quando utiliza HTTP GET Olá de toocall **pesquisa** API, terá de toobe em atenção de que o comprimento do URL de pedido de Olá Olá não pode exceder os 8 KB.</span><span class="sxs-lookup"><span data-stu-id="056a7-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="056a7-786">Isto é normalmente suficiente para a maioria das aplicações.</span><span class="sxs-lookup"><span data-stu-id="056a7-786">This is usually enough for most applications.</span></span> <span data-ttu-id="056a7-787">No entanto, algumas aplicações produzem consultas muito grandes ou expressões de filtro de OData.</span><span class="sxs-lookup"><span data-stu-id="056a7-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="056a7-788">Para estas aplicações, utilizando o HTTP POST é uma melhor opção porque permite maiores filtros e consultas que GET.</span><span class="sxs-lookup"><span data-stu-id="056a7-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="056a7-789">Com o POST, número de Olá de termos de licenciamento ou de cláusulas numa consulta é Olá limitar o fator de tamanho de Olá não da consulta em bruto de Olá, uma vez que o limite de tamanho do pedido de Olá para o POST é aproximadamente 16 MB.</span><span class="sxs-lookup"><span data-stu-id="056a7-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-790">Apesar do limite de tamanho de pedido POST Olá é muito grande, consultas de pesquisa e expressões de filtro não podem ser arbitrariamente complexas.</span><span class="sxs-lookup"><span data-stu-id="056a7-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="056a7-791">Consulte [consulta lucene](https://msdn.microsoft.com/library/mt589323.aspx) e [sintaxe de expressão de OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre limitações de complexidade de consulta e o filtro de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="056a7-792">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-792">**Request**</span></span>

<span data-ttu-id="056a7-793">HTTPS é necessário para pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="056a7-794">Olá **pesquisa** pedido pode ser construído com Olá GET ou métodos POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="056a7-795">URI de pedido de Olá Especifica qual tooquery de índice, para todos os documentos que correspondem aos parâmetros de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="056a7-796">Foram especificados parâmetros na cadeia de consulta Olá no caso de Olá de pedidos GET e no pedido de Olá os pedidos de corpo no caso de Olá da publicação.</span><span class="sxs-lookup"><span data-stu-id="056a7-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="056a7-797">Como melhor prática quando criar pedidos GET, lembre-se demasiado[codificar o URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específicas Olá de parâmetros durante a chamada de REST API diretamente.</span><span class="sxs-lookup"><span data-stu-id="056a7-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="056a7-798">Para **pesquisa** operações, isto inclui:</span><span class="sxs-lookup"><span data-stu-id="056a7-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="056a7-799">Codificação do URL só é recomendada Olá acima parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="056a7-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="056a7-800">Se lhe codificar inadvertidamente URL hello cadeia de consulta completo (tudo após Olá?), irão interromper a pedidos.</span><span class="sxs-lookup"><span data-stu-id="056a7-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="056a7-801">Além disso, a codificação de URL é necessário apenas quando chamar Olá obter a API de REST diretamente utilizando.</span><span class="sxs-lookup"><span data-stu-id="056a7-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="056a7-802">Sem codificação do URL é necessário quando chamar **pesquisa** utilização do POST, ou ao utilizar Olá [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que processa a codificação do URL para si.</span><span class="sxs-lookup"><span data-stu-id="056a7-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="056a7-803"><a name="SearchQueryParameters"></a>
**Parâmetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="056a7-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="056a7-804">**Pesquisa** aceita vários parâmetros que fornecem critérios de consulta e também especificam o comportamento de procura.</span><span class="sxs-lookup"><span data-stu-id="056a7-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="056a7-805">Terá de fornecer estes parâmetros no URL Olá cadeia de consulta ao chamar **pesquisa** via GET e como as propriedades de JSON no corpo do pedido de Olá ao chamar **pesquisa** através de POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="056a7-806">sintaxe de Olá para alguns parâmetros é ligeiramente diferente entre GET e POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="056a7-807">Estas diferenças são assinaladas como aplicável abaixo:</span><span class="sxs-lookup"><span data-stu-id="056a7-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="056a7-808">`search=[string]`(opcional) - Olá toosearch de texto para.</span><span class="sxs-lookup"><span data-stu-id="056a7-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="056a7-809">Todos os `searchable` campos são pesquisados por predefinição, a menos que `searchFields` está especificado.</span><span class="sxs-lookup"><span data-stu-id="056a7-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="056a7-810">Quando pesquisar `searchable` campos, Olá pesquisa próprio texto é com token, pelo que vários termos podem ser separados por espaços em branco (por exemplo: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="056a7-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="056a7-811">Utilize qualquer prazo de toomatch `*` (pode ser útil para consultas de filtro booleano).</span><span class="sxs-lookup"><span data-stu-id="056a7-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="056a7-812">A omissão deste parâmetro tem Olá, mesmo que tenha efeito como defini-la demasiado`*`.</span><span class="sxs-lookup"><span data-stu-id="056a7-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="056a7-813">Consulte [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) para especificações na sintaxe de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="056a7-814">**Tenha em atenção**: resultados Olá, por vezes, podem ser surprising ao consultar sobre `searchable` campos.</span><span class="sxs-lookup"><span data-stu-id="056a7-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="056a7-815">atomizador Olá inclui lógica toohandle casos comuns tooEnglish texto como apostrophes, vírgulas números, etc. Por exemplo, `search=123,456` corresponderá um termo único 123,456 em vez de termos de individuais Olá 123 e 456, uma vez que vírgulas são utilizadas como separadores de milhares de grandes quantidades em inglês.</span><span class="sxs-lookup"><span data-stu-id="056a7-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="056a7-816">Por este motivo, recomendamos que utilize um espaço em branco em vez de termos de tooseparate pontuação no Olá `search` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="056a7-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="056a7-817">`searchMode=any|all`(opcional, será assumida demasiado`any`) - se alguns ou todos os termos de pesquisa de Olá devem corresponder no documento de Olá toocount ordem como uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="056a7-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="056a7-818">`searchFields=[string]`(opcional) - lista de Olá de toosearch de nomes de campo de valores separados por vírgulas para Olá especificado texto.</span><span class="sxs-lookup"><span data-stu-id="056a7-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="056a7-819">Campos de destino devem ser assinalados como `searchable`.</span><span class="sxs-lookup"><span data-stu-id="056a7-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="056a7-820">`queryType=simple|full`(opcional, será assumida demasiado`simple`) - quando o texto de pesquisa demasiado "simples" do conjunto é interpretado utilizando uma linguagem de consulta simples que permite como símbolos +, * e "".</span><span class="sxs-lookup"><span data-stu-id="056a7-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="056a7-821">As consultas são avaliadas em todos os campos pesquisáveis (ou campos indicaram `searchFields`) em cada documento por predefinição.</span><span class="sxs-lookup"><span data-stu-id="056a7-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="056a7-822">Quando o tipo de consulta Olá está definido demasiado`full` texto de pesquisa é interpretado utilizando a linguagem de consulta Lucene do Olá que lhe permite pesquisas específicas do campo e ponderadas.</span><span class="sxs-lookup"><span data-stu-id="056a7-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="056a7-823">Consulte [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) e [consulta Lucene](https://msdn.microsoft.com/library/mt589323.aspx) para especificações no sintaxes de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="056a7-824">Intervalo de pesquisa na Olá Lucene idioma de consulta não é suportado favor $filter que oferece uma funcionalidade semelhante.</span><span class="sxs-lookup"><span data-stu-id="056a7-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="056a7-825">`moreLikeThis=[key]`(opcional) **Importante:** esta funcionalidade só está disponível no `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-826">Esta opção não pode ser utilizada numa consulta que contém o parâmetro de pesquisa de texto Olá, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="056a7-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="056a7-827">Olá `moreLikeThis` parâmetro localiza documentos que são semelhantes toohello documento especificado pela chave do documento Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="056a7-828">Quando é efetuado um pedido de pesquisa com `moreLikeThis`, uma lista dos termos de pesquisa é gerada com base na frequência de Olá e rarity dos termos de documento de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="056a7-829">Os termos encontram-se, em seguida, utilizado toomake Olá pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="056a7-830">Por predefinição, Olá conteúdos de todos os `searchable` campos são considerados a menos que `searchFields` é utilizado toorestrict serão pesquisados os campos.</span><span class="sxs-lookup"><span data-stu-id="056a7-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="056a7-831">`$skip=#`(opcional) - número de Olá de pesquisa resulta tooskip; Não pode ser superior a 100.000.</span><span class="sxs-lookup"><span data-stu-id="056a7-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="056a7-832">Se precisar de documentos tooscan na sequência, mas não é possível utilizar `$skip` devido a limitação de toothis, considere a utilização de `$orderby` numa chave completamente ordenadas e `$filter` com um intervalo de consulta em vez disso.</span><span class="sxs-lookup"><span data-stu-id="056a7-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-833">Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `skip` em vez de `$skip`.</span><span class="sxs-lookup"><span data-stu-id="056a7-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="056a7-834">`$top=#`(opcional) - número de Olá de pesquisa resulta tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="056a7-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="056a7-835">Isto pode ser utilizado em conjunto com `$skip` tooimplement a paginação do lado do cliente dos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-836">Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `top` em vez de `$top`.</span><span class="sxs-lookup"><span data-stu-id="056a7-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="056a7-837">`$count=true|false`(opcional, será assumida demasiado`false`)-Especifica se toofetch Olá contagem total de resultados.</span><span class="sxs-lookup"><span data-stu-id="056a7-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="056a7-838">Esta é a contagem de Olá de todos os documentos que correspondam a Olá `search` e `$filter` parâmetros, a ignorar `$top` e `$skip`.</span><span class="sxs-lookup"><span data-stu-id="056a7-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="056a7-839">Definir este valor demasiado`true` pode ter um impacto no desempenho.</span><span class="sxs-lookup"><span data-stu-id="056a7-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="056a7-840">Tenha em atenção que a contagem de Olá devolvida é uma aproximação do seu.</span><span class="sxs-lookup"><span data-stu-id="056a7-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-841">Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `count` em vez de `$count`.</span><span class="sxs-lookup"><span data-stu-id="056a7-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="056a7-842">`$orderby=[string]`(opcional) - uma lista de expressões de valores separados por vírgulas toosort Olá resultados por.</span><span class="sxs-lookup"><span data-stu-id="056a7-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="056a7-843">Cada expressão pode ser um nome de campo ou uma chamada toohello `geo.distance()` função.</span><span class="sxs-lookup"><span data-stu-id="056a7-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="056a7-844">Cada expressão pode ser seguido `asc` tooindicated ascendente, e `desc` tooindicate descendente.</span><span class="sxs-lookup"><span data-stu-id="056a7-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="056a7-845">é por ordem ascendente predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-845">hello default is ascending order.</span></span> <span data-ttu-id="056a7-846">TIES irão dividir por pontuações de correspondência de Olá de documentos.</span><span class="sxs-lookup"><span data-stu-id="056a7-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="056a7-847">Se não `$orderby` for especificado, sequência de ordenação Olá predefinido é descendente pelo modelo de pontuação de correspondência de documento.</span><span class="sxs-lookup"><span data-stu-id="056a7-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="056a7-848">Há um limite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="056a7-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-849">Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `orderby` em vez de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="056a7-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="056a7-850">`$select=[string]`(opcional) - uma lista de campos de valores separados por vírgulas tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="056a7-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="056a7-851">Se não for indicado, todos os campos marcados como recuperável no esquema Olá estão incluídos.</span><span class="sxs-lookup"><span data-stu-id="056a7-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="056a7-852">Pode também explicitamente pedir todos os campos definindo este parâmetro demasiado`*`.</span><span class="sxs-lookup"><span data-stu-id="056a7-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-853">Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `select` em vez de `$select`.</span><span class="sxs-lookup"><span data-stu-id="056a7-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="056a7-854">`facet=[string]`(zero ou mais) - toofacet um campo pelo.</span><span class="sxs-lookup"><span data-stu-id="056a7-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="056a7-855">Opcionalmente, cadeia Olá pode conter facetamento Olá toocustomize de parâmetros expressado como valores separados por vírgulas `name:value` pares.</span><span class="sxs-lookup"><span data-stu-id="056a7-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="056a7-856">Os parâmetros válidos são:</span><span class="sxs-lookup"><span data-stu-id="056a7-856">Valid parameters are:</span></span>

* <span data-ttu-id="056a7-857">`count`(máximo de número de termos de faceta; predefinição é 10).</span><span class="sxs-lookup"><span data-stu-id="056a7-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="056a7-858">Não existe nenhum máximo, mas valores superiores implicar uma correspondente penalidade de desempenho, especialmente se o campo por facetas Olá contém um grande número de termos exclusivos.</span><span class="sxs-lookup"><span data-stu-id="056a7-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="056a7-859">Por exemplo: `facet=category,count:5` obtém Olá superiores cinco categorias nos resultados de aspeto de restrições.</span><span class="sxs-lookup"><span data-stu-id="056a7-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="056a7-860">**Tenha em atenção**: se hello `count` parâmetro é inferior ao número de Olá dos termos exclusivos, resultados de Olá podem não ser exata.</span><span class="sxs-lookup"><span data-stu-id="056a7-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="056a7-861">Isto acontece devido a forma de toohello consultas facetamento estão distribuídas shards.</span><span class="sxs-lookup"><span data-stu-id="056a7-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="056a7-862">Aumentar `count` geralmente aumenta Olá precisão de contagens de termo Olá, mas um custo de desempenho.</span><span class="sxs-lookup"><span data-stu-id="056a7-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="056a7-863">`sort`(um dos `count` toosort *descendente* por contagem, `-count` toosort *ascendente* por contagem, `value` toosort *ascendente* pelo valor, ou `-value` toosort *descendente* por valor)</span><span class="sxs-lookup"><span data-stu-id="056a7-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="056a7-864">Por exemplo: `facet=category,count:3,sort:count` obtém Olá superiores três categorias nos resultados de aspeto de restrições por ordem descendente por número de Olá de documentos com cada nome de cidade.</span><span class="sxs-lookup"><span data-stu-id="056a7-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="056a7-865">Por exemplo, se Olá superior três categorias são orçamento, hotel e luxo e orçamento tem 5 pedidos, hotel tem 6 e luxo tem 4, Olá registos será por ordem de Olá hotel, orçamento, luxo.</span><span class="sxs-lookup"><span data-stu-id="056a7-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="056a7-866">Por exemplo: `facet=rating,sort:-value` produz registos para todas as classificações possíveis, por ordem descendente por valor.</span><span class="sxs-lookup"><span data-stu-id="056a7-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="056a7-867">Por exemplo, se as classificações de Olá são de 1 too5, registos de Olá irão ser ordenados, 5, 4, 3, 2, 1, independentemente de quantas documentos correspondem a cada classificação.</span><span class="sxs-lookup"><span data-stu-id="056a7-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="056a7-868">`values`(delimitado por pipe numérica ou `Edm.DateTimeOffset` valores especificando um conjunto de valores de entrada do aspeto dinâmico)</span><span class="sxs-lookup"><span data-stu-id="056a7-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="056a7-869">Por exemplo: `facet=baseRate,values:10|20` produz registos três: um para taxa base 0 segurança toobut não incluindo 10, um para 10 cópias de segurança toobut não incluindo 20 e outro para 20 ou superior.</span><span class="sxs-lookup"><span data-stu-id="056a7-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="056a7-870">Por exemplo: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produz dois registos: um para hotéis renovated antes de Fevereiro de 2010 e outro para hotéis renovated Fevereiro partir do dia 1, 2010 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="056a7-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="056a7-871">`interval`(intervalo de número inteiro maior que 0 para números ou `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` para valores de tempo de data)</span><span class="sxs-lookup"><span data-stu-id="056a7-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="056a7-872">Por exemplo: `facet=baseRate,interval:100` produz registos com base nos intervalos de taxa de base do tamanho 100.</span><span class="sxs-lookup"><span data-stu-id="056a7-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="056a7-873">Por exemplo, se forem taxas base todos os entre $60 e $600, será registos para 0-100, 100 200, 200 300, 300 400, 400-500 e 500 600.</span><span class="sxs-lookup"><span data-stu-id="056a7-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="056a7-874">Por exemplo: `facet=lastRenovationDate,interval:year` produz um registo para todos os anos quando foram renovated hotéis.</span><span class="sxs-lookup"><span data-stu-id="056a7-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="056a7-875">`timeoffset`([+-] hh: mm, [+-] hhmm, ou [+-] hh) `timeoffset` é opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="056a7-876">Só pode ser combinado com Olá `interval` opção e apenas quando aplicados tooa campo do tipo `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="056a7-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="056a7-877">valor de Olá Especifica Olá UTC tooaccount desfasamento de tempo para definir limites de tempo.</span><span class="sxs-lookup"><span data-stu-id="056a7-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="056a7-878">Por exemplo: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` utiliza Olá limites do dia que começa em UTC 01:00:00 (meia-noite Olá destino fuso horário)</span><span class="sxs-lookup"><span data-stu-id="056a7-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="056a7-879">**Tenha em atenção**: `count` e `sort` podem ser combinados numa Olá mesmo especificação do aspeto, mas não pode ser combinado com `interval` ou `values`, e `interval` e `values` não podem ser combinados.</span><span class="sxs-lookup"><span data-stu-id="056a7-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="056a7-880">**Tenha em atenção**: facetas de intervalo na data hora são calculadas com base na hora UTC se `timeoffset` não está especificado.</span><span class="sxs-lookup"><span data-stu-id="056a7-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="056a7-881">Por exemplo: para `facet=lastRenovationDate,interval:day`, limites de dia Olá começam às 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="056a7-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="056a7-882">Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `facets` em vez de `facet`.</span><span class="sxs-lookup"><span data-stu-id="056a7-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="056a7-883">Além disso, especificá-la como uma matriz JSON de cadeias, onde cada cadeia é uma expressão de faceta separado.</span><span class="sxs-lookup"><span data-stu-id="056a7-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="056a7-884">`$filter=[string]`(opcional) - uma expressão de pesquisa estruturados na sintaxe de OData padrão.</span><span class="sxs-lookup"><span data-stu-id="056a7-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-885">Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `filter` em vez de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="056a7-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="056a7-886">`highlight=[string]`(opcional) - realça um conjunto de nomes de campos de valores separados por vírgulas utilizada para acessos.</span><span class="sxs-lookup"><span data-stu-id="056a7-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="056a7-887">Apenas `searchable` campos podem ser utilizados para acessos realce.</span><span class="sxs-lookup"><span data-stu-id="056a7-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="056a7-888">`highlightPreTag=[string]`(opcional, será assumida demasiado`<em>`) - uma tag prepends toohit destaques de cadeia.</span><span class="sxs-lookup"><span data-stu-id="056a7-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="056a7-889">Tem de ser definido com `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="056a7-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-890">Quando chamar **pesquisa** utilizar GET, carateres reservados no URL Olá tem de ser codificado por cento (por exemplo, % 23 em vez de #).</span><span class="sxs-lookup"><span data-stu-id="056a7-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="056a7-891">`highlightPostTag=[string]`(opcional, será assumida demasiado`</em>`)-uma tag de cadeia que acrescenta toohit destaques.</span><span class="sxs-lookup"><span data-stu-id="056a7-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="056a7-892">Tem de ser definido com `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="056a7-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-893">Quando chamar **pesquisa** utilizar GET, carateres reservados no URL Olá tem de ser codificado por cento (por exemplo, % 23 em vez de #).</span><span class="sxs-lookup"><span data-stu-id="056a7-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="056a7-894">`scoringProfile=[string]`(opcional) - Olá nome de um tooevaluate de perfil de classificação de corresponder ao pontuações das classificações para documentos correspondentes nos resultados da ordem toosort Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="056a7-895">`scoringParameter=[string]`(zero ou mais) - indica Olá os valores para cada parâmetro definido numa função de classificação (por exemplo, `referencePointParameter`) utilizando o formato de Olá `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="056a7-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="056a7-896">Por exemplo, se o perfil de classificação de Olá define uma função com um parâmetro denominado "mylocation" a opção de cadeia de consulta Olá seria `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="056a7-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="056a7-897">Traço primeiro Olá separa o nome de Olá na lista de valor de Olá, enquanto dash segundo Olá faz parte de Olá o primeiro valor (longitude neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="056a7-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="056a7-898">Para os parâmetros de classificação como etiqueta de os aumentos que podem conter vírgulas, pode terminar quaisquer esses valores na lista de Olá utilizando plicas.</span><span class="sxs-lookup"><span data-stu-id="056a7-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="056a7-899">Se os valores de Olá próprios contenham plicas, pode transformá-los por duplicando.</span><span class="sxs-lookup"><span data-stu-id="056a7-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="056a7-900">Por exemplo, se tiver uma etiqueta os aumentos parâmetro denominado "mytag" e quiser tooboost na tag de Olá valores "Olá, O'Brien" e "Santos", consulta Olá a opção de cadeia seria `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="056a7-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="056a7-901">Tenha em atenção que as aspas são apenas necessários para valores com vírgulas.</span><span class="sxs-lookup"><span data-stu-id="056a7-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-902">Quando chamar **pesquisa** utilização do POST, este parâmetro é denominado `scoringParameters` em vez de `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="056a7-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="056a7-903">Além disso, pode especificá-la como uma matriz JSON de cadeias, onde cada cadeia é um separado `name-values` par.</span><span class="sxs-lookup"><span data-stu-id="056a7-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="056a7-904">`minimumCoverage`(opcional, será assumida too100) - um número entre 0 e 100 que indica a percentagem de Olá do índice de Olá que deve ser abrangida por uma consulta de pesquisa por ordem para Olá consulta toobe reportados como concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="056a7-905">Por predefinição, índice completo Olá tem de estar disponível ou `Search` irá devolver um código de estado HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="056a7-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="056a7-906">Se definir `minimumCoverage` e `Search` for bem sucedida, irá devolver HTTP 200 e incluir um `@search.coverage` valor na resposta Olá que indica a percentagem de Olá do índice de Olá que foi incluído numa consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-907">Definir este valor do parâmetro tooa menor do que 100 pode ser útil para garantir a disponibilidade de pesquisa, mesmo para serviços com apenas uma réplica.</span><span class="sxs-lookup"><span data-stu-id="056a7-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="056a7-908">No entanto, nem todos os documentos correspondentes garantidos toobe presente nos resultados de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="056a7-909">Se devolução de chamada de pesquisa é mais importante tooyour aplicação que a disponibilidade, em seguida, é melhor tooleave `minimumCoverage` no valor predefinido de 100.</span><span class="sxs-lookup"><span data-stu-id="056a7-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="056a7-910">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-911">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-912">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-913">Nota: Para esta operação, Olá `api-version` está especificado como um parâmetro de consulta no URL Olá independentemente se chamar **pesquisa** com GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="056a7-914">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-914">**Request Headers**</span></span>

<span data-ttu-id="056a7-915">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-916">`api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-917">É um valor de cadeia, o URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="056a7-918">Olá **pesquisa** pedido pode especificar uma chave de administrador ou de uma chave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="056a7-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="056a7-919">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-920">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-921">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-922">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-922">**Request Body**</span></span>

<span data-ttu-id="056a7-923">Para o GET: nenhuma.</span><span class="sxs-lookup"><span data-stu-id="056a7-923">For GET: None.</span></span>

<span data-ttu-id="056a7-924">Para o POST:</span><span class="sxs-lookup"><span data-stu-id="056a7-924">For POST:</span></span>

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

<span data-ttu-id="056a7-925">**Continuação de respostas de uma pesquisa parcial**</span><span class="sxs-lookup"><span data-stu-id="056a7-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="056a7-926">Por vezes, pesquisa do Azure não pode devolver que todos os Olá resultados pedidos numa única resposta pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="056a7-927">Isto pode acontecer por diferentes motivos como, por exemplo, quando consulta Olá solicita documentos demasiados especificando não `$top` ou especificando um valor para `$top` que é demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="056a7-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="056a7-928">Nestes casos, a Azure Search incluirá Olá `@odata.nextLink` anotação no corpo de resposta de Olá e também `@search.nextPageParameters` se era um pedido POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="056a7-929">Pode utilizar valores Olá estes tooformulate anotações outra pesquisa pedido tooget Olá seguinte parte da resposta de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="056a7-930">Esta opção é denominada uma ***continuação*** de pedido de pesquisa original Olá e Olá anotações são geralmente denominadas ***tokens de continuação***.</span><span class="sxs-lookup"><span data-stu-id="056a7-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="056a7-931">Consulte [exemplo Olá abaixo](#SearchResponse) para obter detalhes sobre a sintaxe de Olá estes anotações e em que aparecem no corpo da resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="056a7-932">por motivos de Olá por que motivo da Azure Search poderá devolver tokens de continuação são específicos da implementação e assunto do toochange.</span><span class="sxs-lookup"><span data-stu-id="056a7-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="056a7-933">Os clientes robustos devem ser sempre toohandle pronto casos em que são devolvidos menos documentos que o esperado e um token de continuação é incluído toocontinue obter documentos.</span><span class="sxs-lookup"><span data-stu-id="056a7-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="056a7-934">Também em atenção que tem de utilizar Olá mesmo método HTTP como o pedido original de Olá na ordem toocontinue.</span><span class="sxs-lookup"><span data-stu-id="056a7-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="056a7-935">Por exemplo, se enviar um pedido GET, quaisquer pedidos de continuação enviar também tem de utilizar GET (e da mesma forma para o POST).</span><span class="sxs-lookup"><span data-stu-id="056a7-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="056a7-936"><a name="SearchResponse"></a>
**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="056a7-937">Código de estado: 200 OK é devolvido para uma resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-937">Status Code: 200 OK is returned for a successful response.</span></span>

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

<span data-ttu-id="056a7-938">**Exemplos:**</span><span class="sxs-lookup"><span data-stu-id="056a7-938">**Examples:**</span></span>

<span data-ttu-id="056a7-939">Pode encontrar exemplos adicionais no Olá [OData sintaxe de expressão para a Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="056a7-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="056a7-940">Procure Olá descendente do índice ordenado por data.</span><span class="sxs-lookup"><span data-stu-id="056a7-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="056a7-941">GET /indexes/hotels/docs? pesquisa = * & $orderby = lastRenovationDate desc & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-942">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "*", "orderby": "lastRenovationDate desc"}</span><span class="sxs-lookup"><span data-stu-id="056a7-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="056a7-943">Uma pesquisa por facetas pesquisar o índice de Olá e obter as facetas de categorias, classificação, etiquetas, bem como itens com baseRate em intervalos específicos:</span><span class="sxs-lookup"><span data-stu-id="056a7-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="056a7-944">GET /indexes/hotels/docs? pesquisa = teste & aspeto = categoria & aspeto = classificação & aspeto = etiquetas & aspeto = baseRate, valores: 80 | 150 | 220 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-945">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "teste", "facetas": ["categoria", "classificação", "etiquetas", "baseRate, valores: 80 | 150 | 220"]}</span><span class="sxs-lookup"><span data-stu-id="056a7-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="056a7-946">Utilizando um filtro, restringir os resultados da consulta por facetas anterior Olá depois Olá utilizador clica na classificação 3 e a categoria "Hotel":</span><span class="sxs-lookup"><span data-stu-id="056a7-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="056a7-947">GET /indexes/hotels/docs? pesquisa = teste & aspeto = etiquetas & aspeto = baseRate, valores: 80 | 150 | 220 & $filter = classificação eq 3 e categoria eq 'hotel' & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-948">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "teste", "facetas": ["etiquetas", "baseRate, valores: 80 | 150 | 220"], "filtro": "classificação eq 3 e categoria eq"Motel""}</span><span class="sxs-lookup"><span data-stu-id="056a7-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="056a7-949">Numa pesquisa por facetas, defina um limite superior em termos exclusivos devolvidos numa consulta.</span><span class="sxs-lookup"><span data-stu-id="056a7-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="056a7-950">Olá predefinição é 10, mas pode aumentar ou diminuir este valor utilizando Olá `count` parâmetro no Olá `facet` atributo:</span><span class="sxs-lookup"><span data-stu-id="056a7-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="056a7-951">GET /indexes/hotels/docs? pesquisa = teste & aspeto = cidade, contagem: 5 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-952">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "teste", "facetas": ["Cidade, contagem: 5"]}</span><span class="sxs-lookup"><span data-stu-id="056a7-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="056a7-953">Procurar Olá índice dentro de campos específicos; Por exemplo, um campo específicas do idioma:</span><span class="sxs-lookup"><span data-stu-id="056a7-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="056a7-954">GET /indexes/hotels/docs? pesquisa = hôtel & searchFields = description_fr & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-955">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "hôtel", "searchFields": "description_fr"}</span><span class="sxs-lookup"><span data-stu-id="056a7-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="056a7-956">Olá índice através de vários campos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="056a7-957">Por exemplo, pode armazenar e campos pesquisáveis de consulta em vários idiomas, tudo dentro Olá mesmo índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="056a7-958">Se as descrições inglês e francês coexistem na Olá mesmo documento, pode devolver quaisquer ou todas as Olá em resultados de consulta:</span><span class="sxs-lookup"><span data-stu-id="056a7-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="056a7-959">GET /indexes/hotels/docs? pesquisa = átrios & searchFields = descrição, description_fr & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-960">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "átrios", "searchFields": "descrição, description_fr"}</span><span class="sxs-lookup"><span data-stu-id="056a7-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="056a7-961">Tenha em atenção que apenas pode consultar um índice numa altura.</span><span class="sxs-lookup"><span data-stu-id="056a7-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="056a7-962">Não crie vários índices para cada idioma, a menos que planeia tooquery um cada vez.</span><span class="sxs-lookup"><span data-stu-id="056a7-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="056a7-963">A paginação - página de 1ª Olá Get de itens (o tamanho da página é 10):</span><span class="sxs-lookup"><span data-stu-id="056a7-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="056a7-964">GET /indexes/hotels/docs? pesquisa = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-965">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "*", "Ignorar": 0, "superior": 10}</span><span class="sxs-lookup"><span data-stu-id="056a7-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="056a7-966">A paginação - página de 2nd Olá Get de itens (o tamanho da página é 10):</span><span class="sxs-lookup"><span data-stu-id="056a7-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="056a7-967">GET /indexes/hotels/docs? pesquisa = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-968">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "*", "Ignorar": "superior", 10: 10}</span><span class="sxs-lookup"><span data-stu-id="056a7-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="056a7-969">Obter um conjunto específico de campos:</span><span class="sxs-lookup"><span data-stu-id="056a7-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="056a7-970">GET /indexes/hotels/docs? pesquisa = * & $select = hotelName, a descrição e a api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-971">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "*", "select": "hotelName, descrição"}</span><span class="sxs-lookup"><span data-stu-id="056a7-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="056a7-972">Obter documentos correspondente a uma expressão de filtro específico:</span><span class="sxs-lookup"><span data-stu-id="056a7-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="056a7-973">GET /indexes/hotels/docs? $filter = (baseRate ge 60 e baseRate lt 300) ou eq hotelName 'Permaneça Fancy' & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-974">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"filtro": "(baseRate ge 60 e baseRate lt 300) ou hotelName eq 'Fancy mantenha-se'"}</span><span class="sxs-lookup"><span data-stu-id="056a7-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="056a7-975">Índice de pesquisa do Olá e retorno fragmentos com destaques acessos</span><span class="sxs-lookup"><span data-stu-id="056a7-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="056a7-976">GET /indexes/hotels/docs? pesquisa = algo & Realce = descrição & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-977">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "algo", "highlight": "Descrição"}</span><span class="sxs-lookup"><span data-stu-id="056a7-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="056a7-978">Índice de pesquisa do Olá e retorno documentos ordenados do próximo toofarther na direção oposta a uma localização de referência</span><span class="sxs-lookup"><span data-stu-id="056a7-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="056a7-979">GET /indexes/hotels/docs? pesquisa = algo & $orderby=geo.distance (localização, geography'POINT(-122.12315 47.88121)') & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-980">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "algo", "orderby": "geo.distance (localização, geography'POINT(-122.12315 47.88121)')"}</span><span class="sxs-lookup"><span data-stu-id="056a7-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="056a7-981">Pesquisa Olá índice pressuposto de que existe é um perfil de classificação chamado "georreplicação" com duas funções de pontuação de distância, uma definição de um parâmetro denominado "currentLocation" e uma definição de um parâmetro denominado "lastLocation"</span><span class="sxs-lookup"><span data-stu-id="056a7-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="056a7-982">GET /indexes/hotels/docs? pesquisa = algo & scoringProfile = georreplicação & scoringParameter = currentLocation – 122.123,44.77233 & scoringParameter = lastLocation – 121.499,44.2113 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-983">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "algo", "scoringProfile": "georreplicação", "scoringParameters": ["currentLocation – 122.123,44.77233", "lastLocation – 121.499,44.2113"]}</span><span class="sxs-lookup"><span data-stu-id="056a7-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="056a7-984">Localizar documentos no Olá índice utilizando [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="056a7-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="056a7-985">Esta consulta devolve hotéis onde os campos pesquisáveis contenham Olá termos "comfort" e "localização" mas não "hotel":</span><span class="sxs-lookup"><span data-stu-id="056a7-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="056a7-986">GET /indexes/hotels/docs? pesquisa = comfort + localização-hotel & searchMode = all & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="056a7-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="056a7-987">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "comfort + localização-motel", "searchMode": "all"}</span><span class="sxs-lookup"><span data-stu-id="056a7-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="056a7-988">Tenha em atenção a utilização de Olá de `searchMode=all` acima.</span><span class="sxs-lookup"><span data-stu-id="056a7-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="056a7-989">Incluindo este parâmetro substitui a predefinição Olá `searchMode=any`, garantindo que que `-motel` significa "E não" em vez de "Ou NOT".</span><span class="sxs-lookup"><span data-stu-id="056a7-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="056a7-990">Sem `searchMode=all`, obter "Ou NOT" que expande em vez de restringe os resultados da pesquisa e isto pode ser counter-intuitive toosome utilizadores.</span><span class="sxs-lookup"><span data-stu-id="056a7-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="056a7-991">Localizar documentos no Olá índice utilizando [consulta lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="056a7-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="056a7-992">Esta consulta devolve hotéis em que o campo de categoria Olá contém termo Olá "orçamento" e pesquisáveis todos os campos que contém o frase Olá "recentemente renovated".</span><span class="sxs-lookup"><span data-stu-id="056a7-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="056a7-993">Documentos que contém o frase Olá "recentemente renovated" estão ordenados superior, como resultado do valor de aumento Olá termo (3)</span><span class="sxs-lookup"><span data-stu-id="056a7-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="056a7-994">GET /indexes/hotels/docs? pesquisa = categoria: orçamento e \"recentemente renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Preview & querytype = completa</span><span class="sxs-lookup"><span data-stu-id="056a7-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="056a7-995">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"Procurar": "categoria: orçamento e \"recentemente renovated\"^ 3", "queryType": "completa", "searchMode": "all"}</span><span class="sxs-lookup"><span data-stu-id="056a7-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="056a7-996">Documento de pesquisa</span><span class="sxs-lookup"><span data-stu-id="056a7-996">Lookup Document</span></span>
<span data-ttu-id="056a7-997">Olá **pesquisa documento** operação obtém um documento de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="056a7-998">Isto é útil quando um utilizador clica num resultado de pesquisa específica, e pretender toolook segurança detalhes específicos sobre esse documento.</span><span class="sxs-lookup"><span data-stu-id="056a7-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="056a7-999">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-999">**Request**</span></span>

<span data-ttu-id="056a7-1000">HTTPS é necessário para pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="056a7-1001">Olá **pesquisa documento** pedido pode ser construído a forma.</span><span class="sxs-lookup"><span data-stu-id="056a7-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="056a7-1002">Em alternativa, pode utilizar a sintaxe de OData tradicional Olá para pesquisa de chave:</span><span class="sxs-lookup"><span data-stu-id="056a7-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="056a7-1003">pedido de Olá URI inclui um [nome do índice] e [chave], especificando que tooretrieve de documento de que o índice.</span><span class="sxs-lookup"><span data-stu-id="056a7-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="056a7-1004">Só pode obter um documento a uma hora.</span><span class="sxs-lookup"><span data-stu-id="056a7-1004">You can only get one document at a time.</span></span> <span data-ttu-id="056a7-1005">Utilize **pesquisa** tooget vários documentos num único pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="056a7-1006">**Parâmetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="056a7-1006">**Query Parameters**</span></span>

<span data-ttu-id="056a7-1007">`$select=[string]`(opcional) - uma lista de campos de valores separados por vírgulas tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="056a7-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="056a7-1008">Se não especificados ou definido demasiado`*`, todos os campos marcados como recuperável no esquema Olá estão incluídos na projecção de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="056a7-1009">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-1010">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-1011">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-1012">Nota: Para esta operação, Olá `api-version` está especificado como um parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="056a7-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="056a7-1013">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-1013">**Request Headers**</span></span>

<span data-ttu-id="056a7-1014">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-1015">`api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-1016">É um valor de cadeia, o URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="056a7-1017">Olá **pesquisa documento** pedido pode especificar uma chave de administrador ou de uma chave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="056a7-1018">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-1019">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-1020">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-1021">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-1021">**Request Body**</span></span>

<span data-ttu-id="056a7-1022">nenhum.</span><span class="sxs-lookup"><span data-stu-id="056a7-1022">None.</span></span>

<span data-ttu-id="056a7-1023">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-1023">**Response**</span></span>

<span data-ttu-id="056a7-1024">Código de estado: 200 OK é devolvido para uma resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="056a7-1025">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="056a7-1025">**Example**</span></span>

<span data-ttu-id="056a7-1026">Documento de Olá de pesquisa que tenha a chave '2'</span><span class="sxs-lookup"><span data-stu-id="056a7-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="056a7-1027">Documento de Olá de pesquisa que tenha a chave "3" utilizando a sintaxe de OData:</span><span class="sxs-lookup"><span data-stu-id="056a7-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="056a7-1028">Contagem de documentos</span><span class="sxs-lookup"><span data-stu-id="056a7-1028">Count Documents</span></span>
<span data-ttu-id="056a7-1029">Olá **contagem de documentos** operação obtém uma contagem do número de Olá dos documentos num índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="056a7-1030">Olá `$count` sintaxe faz parte de Olá protocolo OData.</span><span class="sxs-lookup"><span data-stu-id="056a7-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="056a7-1031">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-1031">**Request**</span></span>

<span data-ttu-id="056a7-1032">HTTPS é necessário para pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="056a7-1033">Olá **contagem de documentos** pedido pode ser construído com o método GET de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="056a7-1034">Olá [nome do índice] no URI de pedido de Olá indica Olá serviço tooreturn uma contagem de todos os itens na coleção de documentos Olá do índice especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="056a7-1035">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-1036">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-1037">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-1038">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-1038">**Request Headers**</span></span>

<span data-ttu-id="056a7-1039">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional.</span><span class="sxs-lookup"><span data-stu-id="056a7-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="056a7-1040">`Accept`: Este valor tem de ser definido demasiado`text/plain`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="056a7-1041">`api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-1042">É um valor de cadeia, o URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="056a7-1043">Olá **contagem de documentos** pedido pode especificar uma chave de administrador ou de uma chave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="056a7-1044">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-1045">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-1046">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-1047">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-1047">**Request Body**</span></span>

<span data-ttu-id="056a7-1048">nenhum.</span><span class="sxs-lookup"><span data-stu-id="056a7-1048">None.</span></span>

<span data-ttu-id="056a7-1049">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-1049">**Response**</span></span>

<span data-ttu-id="056a7-1050">Código de estado: 200 OK é devolvido para uma resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="056a7-1051">corpo da resposta Olá contém o valor de contagem de Olá como um número inteiro a formatados em texto simples.</span><span class="sxs-lookup"><span data-stu-id="056a7-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="056a7-1052">Sugestões</span><span class="sxs-lookup"><span data-stu-id="056a7-1052">Suggestions</span></span>
<span data-ttu-id="056a7-1053">Olá **sugestões** operação obtém sugestões com base na entrada de uma pesquisa parcial.</span><span class="sxs-lookup"><span data-stu-id="056a7-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="056a7-1054">Este é normalmente utilizado em sugestões antecipada do tooprovide de caixas de pesquisa, como os utilizadores são introduzir termos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="056a7-1055">Sugestão pedidos têm como objetivo em sugerindo documentos de destino, para que Olá sugerida texto pode ser repetido se correspondem a vários documentos candidato Olá mesmo procurar entrada.</span><span class="sxs-lookup"><span data-stu-id="056a7-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="056a7-1056">Pode utilizar `$select` tooretrieve outro campos (incluindo a chave do documento Olá) de documentos para que pode indicar que o documento é origem Olá para cada sugestão.</span><span class="sxs-lookup"><span data-stu-id="056a7-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="056a7-1057">A **sugestões** operação é emitida como um pedido GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="056a7-1058">**Quando publicar toouse em vez de obter**</span><span class="sxs-lookup"><span data-stu-id="056a7-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="056a7-1059">Quando utiliza HTTP GET Olá de toocall **sugestões** API, terá de toobe em atenção de que o comprimento do URL de pedido de Olá Olá não pode exceder os 8 KB.</span><span class="sxs-lookup"><span data-stu-id="056a7-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="056a7-1060">Isto é normalmente suficiente para a maioria das aplicações.</span><span class="sxs-lookup"><span data-stu-id="056a7-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="056a7-1061">No entanto, algumas aplicações produzem consultas muito grande, especificamente expressões de filtro de OData.</span><span class="sxs-lookup"><span data-stu-id="056a7-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="056a7-1062">Para estas aplicações, utilizando o HTTP POST é uma melhor opção porque permite filtros maior do que o GET.</span><span class="sxs-lookup"><span data-stu-id="056a7-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="056a7-1063">Com o POST, número de Olá de cláusulas num filtro de fator restritivo Olá, não Olá tamanho da cadeia de filtro em bruto de Olá, uma vez que o limite de tamanho do pedido de Olá para o POST é aproximadamente 16 MB.</span><span class="sxs-lookup"><span data-stu-id="056a7-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-1064">Apesar do limite de tamanho de pedido POST Olá é muito grande, expressões de filtro não podem ser arbitrariamente complexas.</span><span class="sxs-lookup"><span data-stu-id="056a7-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="056a7-1065">Consulte [sintaxe de expressão de OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre as limitações de complexidade de filtro.</span><span class="sxs-lookup"><span data-stu-id="056a7-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="056a7-1066">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-1066">**Request**</span></span>

<span data-ttu-id="056a7-1067">HTTPS é necessário para pedidos de serviço.</span><span class="sxs-lookup"><span data-stu-id="056a7-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="056a7-1068">Olá **sugestões** pedido pode ser construído com Olá GET ou métodos POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="056a7-1069">URI de pedido de Olá Especifica o nome Olá Olá índice tooquery.</span><span class="sxs-lookup"><span data-stu-id="056a7-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="056a7-1070">Parâmetros, tais como o termo de pesquisa parcialmente entrada de Olá, estão especificados na cadeia de consulta Olá no caso de Olá de pedidos GET e no pedido de Olá os pedidos de corpo no caso de Olá da publicação.</span><span class="sxs-lookup"><span data-stu-id="056a7-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="056a7-1071">Como melhor prática quando criar pedidos GET, lembre-se demasiado[codificar o URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específicas Olá de parâmetros durante a chamada de REST API diretamente.</span><span class="sxs-lookup"><span data-stu-id="056a7-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="056a7-1072">Para **sugestões** operações, isto inclui:</span><span class="sxs-lookup"><span data-stu-id="056a7-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="056a7-1073">Codificação do URL só é recomendada Olá acima parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="056a7-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="056a7-1074">Se lhe codificar inadvertidamente URL hello cadeia de consulta completo (tudo após Olá?), irão interromper a pedidos.</span><span class="sxs-lookup"><span data-stu-id="056a7-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="056a7-1075">Além disso, a codificação de URL é necessário apenas quando chamar Olá obter a API de REST diretamente utilizando.</span><span class="sxs-lookup"><span data-stu-id="056a7-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="056a7-1076">Sem codificação do URL é necessário quando chamar **sugestões** utilização do POST, ou ao utilizar Olá [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que processa a codificação do URL para si.</span><span class="sxs-lookup"><span data-stu-id="056a7-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="056a7-1077">**Parâmetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="056a7-1077">**Query Parameters**</span></span>

<span data-ttu-id="056a7-1078">**Sugestões** aceita vários parâmetros que fornecem critérios de consulta e também especificam o comportamento de procura.</span><span class="sxs-lookup"><span data-stu-id="056a7-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="056a7-1079">Terá de fornecer estes parâmetros no URL Olá cadeia de consulta ao chamar **sugestões** via GET e como as propriedades de JSON no corpo do pedido de Olá ao chamar **sugestões** através de POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="056a7-1080">sintaxe de Olá para alguns parâmetros é ligeiramente diferente entre GET e POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="056a7-1081">Estas diferenças são assinaladas como aplicável abaixo:</span><span class="sxs-lookup"><span data-stu-id="056a7-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="056a7-1082">`search=[string]`-Olá consultas de toosuggest de toouse de texto de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="056a7-1083">Tem de ser, pelo menos, 1 caráter e não mais do que 100 carateres.</span><span class="sxs-lookup"><span data-stu-id="056a7-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="056a7-1084">`highlightPreTag=[string]`(opcional) - uma tag de cadeia que prepends toosearch pedidos.</span><span class="sxs-lookup"><span data-stu-id="056a7-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="056a7-1085">Tem de ser definido com `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-1086">Quando chamar **sugestões** utilizar GET, carateres reservados no URL Olá tem de ser codificado por cento (por exemplo, % 23 em vez de #).</span><span class="sxs-lookup"><span data-stu-id="056a7-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="056a7-1087">`highlightPostTag=[string]`(opcional) - uma tag de cadeia que acrescenta toosearch pedidos.</span><span class="sxs-lookup"><span data-stu-id="056a7-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="056a7-1088">Tem de ser definido com `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-1089">Quando chamar **sugestões** utilizar GET, carateres reservados no URL Olá tem de ser codificado por cento (por exemplo, % 23 em vez de #).</span><span class="sxs-lookup"><span data-stu-id="056a7-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="056a7-1090">`suggesterName=[string]`-nome de Olá do sugestor Olá como especificado no Olá `suggesters` coleção que faz parte da definição do índice Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="056a7-1091">A `suggester` determina os campos são analisados relativamente a termos de sugestões de consulta.</span><span class="sxs-lookup"><span data-stu-id="056a7-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="056a7-1092">Consulte [dos Sugestores](#Suggesters) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="056a7-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="056a7-1093">`fuzzy=[boolean]`(predefinido opcional, = false)-configurar quando o tootrue esta API irá encontrar sugestões, mesmo se existir um caráter substituído ou em falta no texto de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="056a7-1094">Embora Isto proporciona uma melhor experiência em alguns cenários vem num desempenho de custos como sugestão difusa pesquisas são mais lentas e consumam mais recursos.</span><span class="sxs-lookup"><span data-stu-id="056a7-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="056a7-1095">`searchFields=[string]`(opcional) - lista de Olá de toosearch de nomes de campo de valores separados por vírgulas para Olá especificado texto de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="056a7-1096">Campos de destino tem de estar ativados para sugestões.</span><span class="sxs-lookup"><span data-stu-id="056a7-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="056a7-1097">`$top=#`(opcional, predefinição = 5)-Olá diversas tooretrieve de sugestões.</span><span class="sxs-lookup"><span data-stu-id="056a7-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="056a7-1098">Tem de ser um número entre 1 e 100.</span><span class="sxs-lookup"><span data-stu-id="056a7-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-1099">Quando chamar **sugestões** utilização do POST, este parâmetro é denominado `top` em vez de `$top`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="056a7-1100">`$filter=[string]`(opcional) - uma expressão que filtra documentos Olá considerados para sugestões.</span><span class="sxs-lookup"><span data-stu-id="056a7-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-1101">Quando chamar **sugestões** utilização do POST, este parâmetro é denominado `filter` em vez de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="056a7-1102">`$orderby=[string]`(opcional) - uma lista de expressões de valores separados por vírgulas toosort Olá resultados por.</span><span class="sxs-lookup"><span data-stu-id="056a7-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="056a7-1103">Cada expressão pode ser um nome de campo ou uma chamada toohello `geo.distance()` função.</span><span class="sxs-lookup"><span data-stu-id="056a7-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="056a7-1104">Cada expressão pode ser seguido `asc` tooindicated ascendente, e `desc` tooindicate descendente.</span><span class="sxs-lookup"><span data-stu-id="056a7-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="056a7-1105">é por ordem ascendente predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-1105">hello default is ascending order.</span></span> <span data-ttu-id="056a7-1106">Há um limite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-1107">Quando chamar **sugestões** utilização do POST, este parâmetro é denominado `orderby` em vez de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="056a7-1108">`$select=[string]`(opcional) - uma lista de campos de valores separados por vírgulas tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="056a7-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="056a7-1109">Se não for indicado, Olá apenas a chave do documento e o texto de sugestão é devolvido.</span><span class="sxs-lookup"><span data-stu-id="056a7-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="056a7-1110">Pode pedir explicitamente todos os campos definindo este parâmetro demasiado`*`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-1111">Quando chamar **sugestões** utilização do POST, este parâmetro é denominado `select` em vez de `$select`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="056a7-1112">`minimumCoverage`(opcional, será assumida too80) - um número entre 0 e 100 que indica a percentagem de Olá do índice de Olá que deve ser abrangida por uma consulta de sugestões por ordem para Olá consulta toobe reportados como concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="056a7-1113">Por predefinição, pelo menos 80% de índice de Olá tem de estar disponível ou `Suggest` irá devolver um código de estado HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="056a7-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="056a7-1114">Se definir `minimumCoverage` e `Suggest` for bem sucedida, irá devolver HTTP 200 e incluir um `@search.coverage` valor na resposta Olá que indica a percentagem de Olá do índice de Olá que foi incluído numa consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="056a7-1115">Definir este valor do parâmetro tooa menor do que 100 pode ser útil para garantir a disponibilidade de pesquisa, mesmo para serviços com apenas uma réplica.</span><span class="sxs-lookup"><span data-stu-id="056a7-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="056a7-1116">No entanto, nem todas as sugestões correspondentes garantidos toobe presente nos resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="056a7-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="056a7-1117">Se a devolução de chamada é mais importante tooyour aplicação, a disponibilidade, então o respetivo melhores não toolower `minimumCoverage` abaixo o valor predefinido 80.</span><span class="sxs-lookup"><span data-stu-id="056a7-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="056a7-1118">`api-version=[string]`(obrigatório).</span><span class="sxs-lookup"><span data-stu-id="056a7-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="056a7-1119">versão de pré-visualização Olá é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="056a7-1120">Consulte [controlo de versões de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="056a7-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="056a7-1121">Nota: Para esta operação, Olá `api-version` está especificado como um parâmetro de consulta no URL Olá independentemente se chamar **sugestões** com GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="056a7-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="056a7-1122">**Cabeçalhos de pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-1122">**Request Headers**</span></span>

<span data-ttu-id="056a7-1123">Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional</span><span class="sxs-lookup"><span data-stu-id="056a7-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="056a7-1124">`api-key`: Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="056a7-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="056a7-1125">É um valor de cadeia, o URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="056a7-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="056a7-1126">Olá **sugestões** pedido pode especificar uma chave de administrador ou de uma chave de consulta como Olá `api-key`.</span><span class="sxs-lookup"><span data-stu-id="056a7-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="056a7-1127">Também terá de Olá serviço nome tooconstruct Olá URL do pedido.</span><span class="sxs-lookup"><span data-stu-id="056a7-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="056a7-1128">Pode obter o nome do serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056a7-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="056a7-1129">Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.</span><span class="sxs-lookup"><span data-stu-id="056a7-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="056a7-1130">**Corpo do pedido**</span><span class="sxs-lookup"><span data-stu-id="056a7-1130">**Request Body**</span></span>

<span data-ttu-id="056a7-1131">Para o GET: nenhuma.</span><span class="sxs-lookup"><span data-stu-id="056a7-1131">For GET: None.</span></span>

<span data-ttu-id="056a7-1132">Para o POST:</span><span class="sxs-lookup"><span data-stu-id="056a7-1132">For POST:</span></span>

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

<span data-ttu-id="056a7-1133">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="056a7-1133">**Response**</span></span>

<span data-ttu-id="056a7-1134">Código de estado: 200 OK é devolvido para uma resposta com êxito.</span><span class="sxs-lookup"><span data-stu-id="056a7-1134">Status Code: 200 OK is returned for a successful response.</span></span>

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

<span data-ttu-id="056a7-1135">Se a opção de projeção Olá é utilizado tooretrieve campos estiverem incluídas em cada elemento da matriz de Olá:</span><span class="sxs-lookup"><span data-stu-id="056a7-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

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

<span data-ttu-id="056a7-1136">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="056a7-1136">**Example**</span></span>

<span data-ttu-id="056a7-1137">Obter 5 sugestões em que a entrada de uma pesquisa parcial Olá é 'lux'</span><span class="sxs-lookup"><span data-stu-id="056a7-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
