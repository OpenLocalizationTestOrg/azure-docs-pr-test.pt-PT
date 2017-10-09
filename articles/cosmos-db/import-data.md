---
title: "ferramenta de migração de aaaDatabase para a base de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como toouse Olá abrir origem Azure Cosmos DB dados migração ferramentas tooimport dados tooAzure Cosmos DB de várias origens, incluindo ficheiros MongoDB, SQL Server, Table storage, Amazon DynamoDB, CSV e JSON. Conversão de tooJSON CSV."
keywords: "toojson csv, as ferramentas de migração de base de dados, converter csv toojson"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="fdd8b-105">Como tooimport dados na base de dados do Azure Cosmos para Olá API do DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="fdd8b-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="fdd8b-106">Este tutorial fornece instruções sobre como utilizar Olá BD do Azure Cosmos: ferramenta de migração de dados de API do DocumentDB, que pode importar dados a partir de várias origens, incluindo ficheiros JSON, CSV ficheiros, SQL Server, o MongoDB, o Table storage do Azure, Amazon DynamoDB e DocumentDB do Azure Cosmos DB Coleções de API para coleções para utilizam com a base de dados do Azure Cosmos e Olá API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="fdd8b-107">Também pode ser utilizada a ferramenta de migração de dados de Olá quando migrar a partir de uma única partição coleção tooa partição multi coleção Olá API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="fdd8b-108">ferramenta de migração de dados de Olá só funciona quando a importação de dados na base de dados do Azure Cosmos para utilizam com Olá API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="fdd8b-109">Importar dados para utilização com Olá API de tabela ou Graph API não é suportado neste momento.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="fdd8b-110">dados de tooimport para utilização com Olá API do MongoDB, consulte [BD do Azure Cosmos: como dados de toomigrate para Olá MongoDB API?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="fdd8b-111">Este tutorial abrange Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fdd8b-112">Instalar a ferramenta de migração de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="fdd8b-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="fdd8b-113">Importar dados a partir de origens de dados diferentes</span><span class="sxs-lookup"><span data-stu-id="fdd8b-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="fdd8b-114">Exportação de base de dados do Azure Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="fdd8b-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="fdd8b-115"><a id="Prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fdd8b-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="fdd8b-116">Antes de seguir as instruções de Olá neste artigo, certifique-se de que tem o seguinte Olá instalado:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="fdd8b-117">[O Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ou superior.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="fdd8b-118"><a id="Overviewl"></a>Descrição geral da ferramenta de migração de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="fdd8b-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="fdd8b-119">ferramenta de migração de dados de Olá é uma solução de código aberto que importa dados tooAzure Cosmos BD a partir de uma variedade de origens, incluindo:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="fdd8b-120">Ficheiros JSON</span><span class="sxs-lookup"><span data-stu-id="fdd8b-120">JSON files</span></span>
* <span data-ttu-id="fdd8b-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="fdd8b-121">MongoDB</span></span>
* <span data-ttu-id="fdd8b-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="fdd8b-122">SQL Server</span></span>
* <span data-ttu-id="fdd8b-123">Ficheiros CSV</span><span class="sxs-lookup"><span data-stu-id="fdd8b-123">CSV files</span></span>
* <span data-ttu-id="fdd8b-124">Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="fdd8b-124">Azure Table storage</span></span>
* <span data-ttu-id="fdd8b-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="fdd8b-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="fdd8b-126">HBase</span><span class="sxs-lookup"><span data-stu-id="fdd8b-126">HBase</span></span>
* <span data-ttu-id="fdd8b-127">Coleções do Cosmos BD do Azure</span><span class="sxs-lookup"><span data-stu-id="fdd8b-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="fdd8b-128">Enquanto a ferramenta de importação de Olá inclui uma interface gráfica (dtui.exe), também pode ser controlada Olá linha de comandos (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="fdd8b-129">Na verdade, há um comando de Olá associado toooutput opção depois de configurar uma importação através de Olá IU.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="fdd8b-130">Pode ser transformadas a tabela de origem de dados (por exemplo, SQL Server ou ficheiros CSV) que podem ser criadas relações hierárquicas (subdocuments) durante a importação.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="fdd8b-131">Manter toolearn de ler mais sobre as opções de origem, tooimport de linhas de comandos de exemplo de cada origem, as opções de destino e visualizar os resultados de importar.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="fdd8b-132"><a id="Install"></a>Instalar a ferramenta de migração de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="fdd8b-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="fdd8b-133">código de origem da ferramenta de migração de Olá está disponível no GitHub em [este repositório](https://github.com/azure/azure-documentdb-datamigrationtool) e está disponível a partir de uma versão de compilados [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="fdd8b-134">Pode compilar solução Olá ou simplesmente transferir e extrair o diretório de tooa versão compilada Olá à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="fdd8b-135">Em seguida, execute um:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-135">Then run either:</span></span>

* <span data-ttu-id="fdd8b-136">**Dtui.exe**: versão de interface gráfica da ferramenta de Olá</span><span class="sxs-lookup"><span data-stu-id="fdd8b-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="fdd8b-137">**DT.exe**: versão de linha de comandos da ferramenta de Olá</span><span class="sxs-lookup"><span data-stu-id="fdd8b-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="fdd8b-138">Importar dados</span><span class="sxs-lookup"><span data-stu-id="fdd8b-138">Import data</span></span>

<span data-ttu-id="fdd8b-139">Assim que instalou a ferramenta de Olá, é tooimport tempo os dados.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="fdd8b-140">Que tipo de dados pretende tooimport?</span><span class="sxs-lookup"><span data-stu-id="fdd8b-140">What kind of data do you want tooimport?</span></span>

* [<span data-ttu-id="fdd8b-141">Ficheiros JSON</span><span class="sxs-lookup"><span data-stu-id="fdd8b-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="fdd8b-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="fdd8b-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="fdd8b-143">Ficheiros de exportação do MongoDB</span><span class="sxs-lookup"><span data-stu-id="fdd8b-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="fdd8b-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="fdd8b-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="fdd8b-145">Ficheiros CSV</span><span class="sxs-lookup"><span data-stu-id="fdd8b-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="fdd8b-146">Armazenamento de tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="fdd8b-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="fdd8b-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="fdd8b-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="fdd8b-148">Blob</span><span class="sxs-lookup"><span data-stu-id="fdd8b-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="fdd8b-149">Coleções do Cosmos BD do Azure</span><span class="sxs-lookup"><span data-stu-id="fdd8b-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="fdd8b-150">HBase</span><span class="sxs-lookup"><span data-stu-id="fdd8b-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="fdd8b-151">Importação de em massa do Cosmos BD do Azure</span><span class="sxs-lookup"><span data-stu-id="fdd8b-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="fdd8b-152">Importação de registo sequenciais Cosmos BD do Azure</span><span class="sxs-lookup"><span data-stu-id="fdd8b-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="fdd8b-153"><a id="JSON"></a>ficheiros JSON tooimport</span><span class="sxs-lookup"><span data-stu-id="fdd8b-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="fdd8b-154">Olá opção de importador de origem de ficheiro JSON permite-lhe tooimport um ou mais ficheiros JSON único documento ou ficheiros JSON que contém cada uma matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="fdd8b-155">Ao adicionar pastas que contêm tooimport de ficheiros JSON, tiver opção Olá recursivamente a procurar ficheiros em subpastas.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![Opções de origem de ficheiro de captura de ecrã de JSON - ferramentas de migração de bases de dados](./media/import-data/jsonsource.png)

<span data-ttu-id="fdd8b-157">Seguem-se alguns ficheiros JSON de tooimport de amostras de linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-157">Here are some command line samples tooimport JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="fdd8b-158"><a id="MongoDB"></a>tooimport do MongoDB</span><span class="sxs-lookup"><span data-stu-id="fdd8b-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdd8b-159">Se estiver a importar conta de base de dados do Azure Cosmos tooan com suporte para o MongoDB, siga estes [instruções](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="fdd8b-160">Olá opção de importador de origem do MongoDB permite-lhe tooimport de uma coleção de MongoDB individuais e, opcionalmente, filtrar documentos através de uma consulta e/ou modificar a estrutura de documento Olá através da utilização de uma projecção.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![Opções de origem de captura de ecrã do MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="fdd8b-162">cadeia de ligação de Olá está no formato de MongoDB padrão Olá:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="fdd8b-163">Utilize Olá verifique comando tooensure que Olá instância do MongoDB especificada no campo de cadeia de ligação de Olá pode ser acedido.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="fdd8b-164">Introduza o nome de Olá da coleção de Olá partir da qual os dados serão importados.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="fdd8b-165">Opcionalmente, pode especificar ou fornecer um ficheiro para uma consulta (por exemplo, {pop: {$gt: 5000}}) e/ou projecção (por exemplo, {loc:0}) tooboth filtro e forma Olá dados toobe importado.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="fdd8b-166">Seguem-se algumas tooimport de amostras de linha de comandos do MongoDB:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="fdd8b-167"><a id="MongoDBExport"></a>ficheiros de exportação do MongoDB tooimport</span><span class="sxs-lookup"><span data-stu-id="fdd8b-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdd8b-168">Se estiver a importar conta de base de dados do Azure Cosmos tooan com suporte para o MongoDB, siga estes [instruções](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="fdd8b-169">Olá os opção do importador de origem do ficheiro JSON do MongoDB exportação permite-lhe tooimport um ou mais ficheiros JSON produzidos do utilitário de mongoexport Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![Opções de origem de exportação de captura de ecrã do MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="fdd8b-171">Ao adicionar pastas que contêm ficheiros JSON de exportação de MongoDB para importação, terá de opção de Olá de recursivamente a procurar ficheiros em subpastas.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="fdd8b-172">Eis um tooimport de exemplo de linha de comandos da exportação do MongoDB ficheiros JSON:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="fdd8b-173"><a id="SQL"></a>tooimport do SQL Server</span><span class="sxs-lookup"><span data-stu-id="fdd8b-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="fdd8b-174">Olá opção de importador de origem SQL permite-lhe tooimport de uma base de dados individuais do SQL Server e, opcionalmente, filtrar Olá registos toobe importado utilizando uma consulta.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="fdd8b-175">Além disso, pode modificar a estrutura de documento Olá, especificando um separador de aninhamento (mais informações sobre as que dentro de momentos).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Opções de origem de captura de ecrã do SQL Server - as ferramentas de migração de base de dados](./media/import-data/sqlexportsource.png)

<span data-ttu-id="fdd8b-177">formato de Olá Olá da cadeia de ligação é o formato de cadeia de ligação do Olá padrão SQL.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="fdd8b-178">Utilize Olá verifique comando tooensure que Olá instância do SQL Server especificada no campo de cadeia de ligação de Olá pode ser acedido.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="fdd8b-179">Olá aninhamento de propriedade de separador é utilizado toocreate hierárquica relações (secundárias documentos) durante a importação.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="fdd8b-180">Considere Olá seguinte consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-180">Consider hello following SQL query:</span></span>

<span data-ttu-id="fdd8b-181">*Selecione CAST (BusinessEntityID AS varchar) como Id, o nome, AddressType como [Address.AddressType], AddressLine1 como [Address.AddressLine1], cidade como [Address.Location.City], StateProvinceName como [Address.Location.StateProvinceName], PostalCode como [ Address.PostalCode] CountryRegionName como [Address.CountryRegionName] do Sales.vStoreWithAddresses onde AddressType = 'Sede'*</span><span class="sxs-lookup"><span data-stu-id="fdd8b-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="fdd8b-182">Que devolve Olá os seguintes resultados (parciais):</span><span class="sxs-lookup"><span data-stu-id="fdd8b-182">Which returns hello following (partial) results:</span></span>

![Resultados da consulta de captura de ecrã do SQL Server](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="fdd8b-184">Tenha em atenção os aliases de Olá como Address.AddressType e Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="fdd8b-185">Ao especificar um separador de aninhamento de '.', ferramenta de importação de Olá cria endereço e Address.Location subdocuments durante Olá importar.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="fdd8b-186">Eis um exemplo de um documento do BD Azure Cosmos resultante:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="fdd8b-187">*{"id": "956", "Name": "Melhorar vendas e serviço de", "Endereço": {"AddressType": "Main Office", "AddressLine1": "#500 75 O'Connor Rua", "Localização": {"Cidade": "Ottawa", "StateProvinceName": "Ontario"}, "PostalCode": "K4B 1S2", "CountryRegionName": " Canadá"}}*</span><span class="sxs-lookup"><span data-stu-id="fdd8b-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="fdd8b-188">Seguem-se algumas tooimport de amostras de linha de comandos do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="fdd8b-189"><a id="CSV"></a>ficheiros CSV tooimport e converter CSV tooJSON</span><span class="sxs-lookup"><span data-stu-id="fdd8b-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="fdd8b-190">Olá opção de importador de origem de ficheiro CSV permite-lhe tooimport um ou mais ficheiros CSV.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="fdd8b-191">Ao adicionar pastas que contêm ficheiros CSV para importar, tiver opção Olá recursivamente a procurar ficheiros em subpastas.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![Opções de origem de captura de ecrã do CSV - tooJSON CSV](media/import-data/csvsource.png)

<span data-ttu-id="fdd8b-193">Origem SQL toohello semelhante, Olá aninhamento propriedade separador estar toocreate utilizados hierárquica relações (secundárias documentos) durante a importação.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="fdd8b-194">Considere Olá seguinte linha de cabeçalho CSV e linhas de dados:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-194">Consider hello following CSV header row and data rows:</span></span>

![Registos de exemplo de captura de ecrã do CSV - tooJSON CSV](./media/import-data/csvsample.png)

<span data-ttu-id="fdd8b-196">Tenha em atenção os aliases de Olá como DomainInfo.Domain_Name e RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="fdd8b-197">Ao especificar um separador de aninhamento de '.', a ferramenta de importação de Olá criará DomainInfo e RedirectInfo subdocuments durante Olá importar.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="fdd8b-198">Eis um exemplo de um documento do BD Azure Cosmos resultante:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="fdd8b-199">*{"DomainInfo": {"Nome_domínio": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"},"Agência Federal":"Conferência administrativa de Olá dos Estados Unidos","RedirectInfo": {"Redirecionar":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*</span><span class="sxs-lookup"><span data-stu-id="fdd8b-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="fdd8b-200">ferramenta de importação de Olá tentará informações de tipo tooinfer por valores unquoted ficheiros CSV (delimitado por aspas valores sempre são tratados como cadeias).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="fdd8b-201">Tipos são identificados num Olá seguinte ordem: número, datetime, booleano.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="fdd8b-202">Existem dois outro toonote coisas sobre importação de CSV:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="fdd8b-203">Por predefinição, valores unquoted sempre são recortados para separadores e espaços, enquanto os valores entre aspas são preservados como-é.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="fdd8b-204">Este comportamento pode ser substituído por Olá que cortar quoted valores caixa de verificação ou Olá /s.TrimQuoted linha de comandos opção.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="fdd8b-205">Por predefinição, um nulo unquoted é tratado como um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="fdd8b-206">Este comportamento pode ser substituído (ou seja, processe um unquoted nulo como uma cadeia "null") com Olá Treat unquoted nulo como caixa de verificação ou Olá /s.NoUnquotedNulls linha de comandos a opção de cadeia.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="fdd8b-207">Eis um exemplo de linha de comandos para importação de CSV:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="fdd8b-208"><a id="AzureTableSource"></a>tooimport do Table storage do Azure</span><span class="sxs-lookup"><span data-stu-id="fdd8b-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="fdd8b-209">Olá opção do importador de origem de armazenamento de tabelas do Azure permite-lhe tooimport de uma tabela de armazenamento de tabelas do Azure individual e, opcionalmente, filtrar Olá tabela entidades toobe importado.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="fdd8b-210">Tenha em atenção que não é possível utilizar dados de armazenamento de Azure Table ferramenta tooimport Olá migração de dados na base de dados do Azure Cosmos para utilização com Olá API de tabela.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="fdd8b-211">Importar apenas tooAzure Cosmos DB para utilização com Olá API do DocumentDB é suportado neste momento.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Opções de origem do armazenamento de captura de ecrã de tabelas do Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="fdd8b-213">formato de Olá do Olá cadeia de ligação de armazenamento de tabelas do Azure é:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="fdd8b-214">Utilize Olá verifique comando tooensure que Olá instância de armazenamento de tabelas do Azure especificada no campo de cadeia de ligação de Olá pode ser acedido.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="fdd8b-215">Introduza o nome de Olá de Olá Azure tabela a partir da qual os dados serão importados.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="fdd8b-216">Opcionalmente, pode especificar um [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="fdd8b-217">Olá opção do importador de origem de armazenamento de tabelas do Azure tem Olá seguintes opções adicionais:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="fdd8b-218">Incluir campos internos</span><span class="sxs-lookup"><span data-stu-id="fdd8b-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="fdd8b-219">-Incluem todos os campos internos (PartitionKey, RowKey e Timestamp)</span><span class="sxs-lookup"><span data-stu-id="fdd8b-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="fdd8b-220">Nenhum - excluir todos os campos internos</span><span class="sxs-lookup"><span data-stu-id="fdd8b-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="fdd8b-221">RowKey - incluir apenas o campo de RowKey Olá</span><span class="sxs-lookup"><span data-stu-id="fdd8b-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="fdd8b-222">Selecionar colunas</span><span class="sxs-lookup"><span data-stu-id="fdd8b-222">Select Columns</span></span>
   1. <span data-ttu-id="fdd8b-223">Os filtros de armazenamento do Azure tabela não suportam projeções.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="fdd8b-224">Se pretender que as propriedades de entidade de Azure Table específicas do tooonly importação, adicioná-los toohello lista de colunas selecionadas.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="fdd8b-225">Todas as outras propriedades de entidade serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="fdd8b-226">Eis um tooimport de exemplo de linha de comandos do Table storage do Azure:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="fdd8b-227"><a id="DynamoDBSource"></a>tooimport da Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="fdd8b-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="fdd8b-228">Olá opção de importador de origem do Amazon DynamoDB permite-lhe tooimport de uma tabela de Amazon DynamoDB individuais e, opcionalmente, filtrar Olá entidades toobe importado.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="fdd8b-229">Vários modelos são fornecidos para que configurar uma importação é tão simples quanto possível.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Opções de origem de captura de ecrã da Amazon DynamoDB - ferramentas de migração de bases de dados](./media/import-data/dynamodbsource1.png)

![Opções de origem de captura de ecrã da Amazon DynamoDB - ferramentas de migração de bases de dados](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="fdd8b-232">formato de Olá do Olá Amazon DynamoDB cadeia de ligação é:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="fdd8b-233">Utilize Olá verifique comando tooensure que Olá instância Amazon DynamoDB especificada no campo de cadeia de ligação de Olá pode ser acedido.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="fdd8b-234">Eis um tooimport de exemplo de linha de comandos do Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="fdd8b-235"><a id="BlobImport"></a>ficheiros de tooimport do Blob storage do Azure</span><span class="sxs-lookup"><span data-stu-id="fdd8b-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="fdd8b-236">Olá ficheiro JSON, ficheiro de exportação do MongoDB e as opções do importador de origem de ficheiro do CSV permitem-lhe tooimport um ou mais ficheiros do Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="fdd8b-237">Depois de especificar um URL do contentor de Blob e a chave da conta, forneça uma expressão regular tooselect Olá ficheiros tooimport.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Opções de origem do ficheiro de captura de ecrã do Blob](./media/import-data/blobsource.png)

<span data-ttu-id="fdd8b-239">Segue-se a linha de comandos exemplo tooimport JSON os ficheiros do armazenamento de Blobs do Azure:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="fdd8b-240"><a id="DocumentDBSource"></a>tooimport de uma coleção de API de DocumentDB do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fdd8b-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="fdd8b-241">Olá opção de importador de origem de BD do Cosmos Azure permite-lhe tooimport dados a partir de uma ou mais coleções da base de dados do Azure Cosmos e, opcionalmente, filtrar documentos através de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Opções de origem de BD do Cosmos captura de ecrã do Azure](./media/import-data/documentdbsource.png)

<span data-ttu-id="fdd8b-243">formato de Olá do Olá cadeia de ligação de base de dados do Azure Cosmos é:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="fdd8b-244">Olá cadeia de ligação de conta de base de dados do Azure Cosmos pode ser obtido a partir do painel de chaves de Olá de Olá portal do Azure, conforme descrito em [como toomanage uma conta de base de dados do Azure Cosmos](manage-account.md); no entanto, o nome de Olá da base de dados de Olá tem toohello toobe anexado cadeia de ligação no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="fdd8b-245">Utilize Olá verifique comando tooensure que Olá instância de base de dados do Azure Cosmos especificada no campo de cadeia de ligação de Olá pode ser acedido.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="fdd8b-246">tooimport de uma única coleção da base de dados do Azure Cosmos, introduza o nome de Olá da coleção de Olá partir da qual os dados serão importados.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="fdd8b-247">tooimport de várias coleções de BD do Cosmos do Azure, forneça uma expressão regular toomatch um ou mais nomes de coleção (por exemplo, collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="fdd8b-248">Opcionalmente, pode especificar, ou fornecer um ficheiro para um filtro de tooboth de consulta e formam Olá dados toobe importado.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="fdd8b-249">Uma vez que o campo de coleção de Olá aceita expressões regulares, se estiver a importar a partir de uma única coleção cujo nome contém carateres de expressão regular, em seguida, esses carateres tem de ser escape em conformidade.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="fdd8b-250">Olá opção de importador de origem de base de dados do Azure Cosmos tem seguinte Olá opções avançadas:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="fdd8b-251">Incluir campos internos: Especifica se pretende ou não tooinclude Azure Cosmos DB documento das propriedades do sistema no Olá exportar (por exemplo, _ts, _rid).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="fdd8b-252">Número de tentativas em caso de falha: Especifica Olá diversas vezes tooretry Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="fdd8b-253">Intervalo de repetição: Especifica quanto toowait entre repetir Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="fdd8b-254">Modo de ligação: Especifica toouse de modo de ligação de Olá com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="fdd8b-255">opções disponíveis Olá são DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="fdd8b-256">modos de ligação direta Olá são mais rápida, enquanto o modo de gateway de Olá é firewall mais amigável como o utiliza apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Origem de captura de ecrã da BD do Cosmos Azure opções avançadas](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="fdd8b-258">modo de tooconnection de predefinições de ferramenta DirectTcp de importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="fdd8b-259">Se ocorrerem problemas de firewall, alternar modo tooconnection Gateway, porque requer apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="fdd8b-260">Seguem-se algumas tooimport de amostras de linha de comandos da base de dados do Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="fdd8b-261">Olá ferramenta de importação de dados do Azure Cosmos DB também suporta a importação de dados de Olá [emulador de BD do Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="fdd8b-262">Ao importar dados a partir de um emulador local, definir ponto final de Olá demasiado`https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="fdd8b-263"><a id="HBaseSource"></a>tooimport do HBase</span><span class="sxs-lookup"><span data-stu-id="fdd8b-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="fdd8b-264">Olá opção de importador de origem do HBase permite-lhe tooimport dados a partir de uma tabela de HBase e, opcionalmente, filtrar dados Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="fdd8b-265">Vários modelos são fornecidos para que configurar uma importação é tão simples quanto possível.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Opções de origem de captura de ecrã do HBase](./media/import-data/hbasesource1.png)

![Opções de origem de captura de ecrã do HBase](./media/import-data/hbasesource2.png)

<span data-ttu-id="fdd8b-268">formato de Olá do Olá HBase Stargate cadeia de ligação é:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="fdd8b-269">Utilize Olá verifique comando tooensure que Olá instância HBase especificada no campo de cadeia de ligação de Olá pode ser acedido.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="fdd8b-270">Eis um tooimport de exemplo de linha de comandos do HBase:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="fdd8b-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (importar em massa)</span><span class="sxs-lookup"><span data-stu-id="fdd8b-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="fdd8b-272">importador de em massa de BD do Azure Cosmos Olá permite-lhe tooimport de qualquer uma das opções de origem disponível Olá, utilizando um procedimento de BD do Cosmos Azure armazenados para uma eficiência.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="fdd8b-273">Olá ferramenta suporta a importação tooone particionado em único base de dados do Azure Cosmos coleção, bem como a importação na qual os dados estão particionados em várias coleções de base de dados do Azure Cosmos particionado em único.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="fdd8b-274">Para obter mais informações sobre a criação de partições de dados, consulte [divisão em partições e o dimensionamento do BD Azure Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="fdd8b-275">ferramenta de Olá irá criar, executar e, em seguida, elimine o procedimento armazenado de Olá do Olá destino collection(s).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Opções de em massa de BD do Cosmos captura de ecrã do Azure](./media/import-data/documentdbbulk.png)

<span data-ttu-id="fdd8b-277">formato de Olá do Olá cadeia de ligação de base de dados do Azure Cosmos é:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="fdd8b-278">Olá cadeia de ligação de conta de base de dados do Azure Cosmos pode ser obtido a partir do painel de chaves de Olá de Olá portal do Azure, conforme descrito em [como toomanage uma conta de base de dados do Azure Cosmos](manage-account.md); no entanto, o nome de Olá da base de dados de Olá tem toohello toobe anexado cadeia de ligação no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="fdd8b-279">Utilize Olá verifique comando tooensure que Olá instância de base de dados do Azure Cosmos especificada no campo de cadeia de ligação de Olá pode ser acedido.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="fdd8b-280">tooimport tooa única coleção, introduza o nome de Olá de Olá coleção toowhich dados serão importados e clique no botão Adicionar de Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="fdd8b-281">tooimport toomultiple coleções, introduza o nome de cada coleção individualmente ou utilizar Olá seguindo a sintaxe toospecify várias coleções: *collection_prefix*[iniciar índice - índice de fim].</span><span class="sxs-lookup"><span data-stu-id="fdd8b-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="fdd8b-282">Ao especificar várias coleções através da sintaxe acima mencionados Olá, tenha em atenção Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="fdd8b-283">São suportados apenas número inteiro intervalo padrões de nome.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="fdd8b-284">Por exemplo, especificar a coleção [0-3] irá produzir Olá seguintes coleções: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="fdd8b-285">Pode utilizar uma sintaxe abreviada: recolha [3] irá emitir o mesmo conjunto de coleções mencionado no passo 1.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="fdd8b-286">Pode ser fornecida mais do que uma substituição.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-286">More than one substitution can be provided.</span></span> <span data-ttu-id="fdd8b-287">Por exemplo, a coleção [0-1], [0-9] irá gerar 20 nomes de colecção com líderes zeros (collection01,.. 02,... 03).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="fdd8b-288">Depois de Olá coleção nomes foram especificadas, escolhe o débito pretendido Olá Olá collection(s) (400 RUs too10 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="fdd8b-289">Para melhor desempenho de importação, escolha um maior débito.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="fdd8b-290">Para obter mais informações sobre os níveis de desempenho, consulte [níveis de desempenho na base de dados do Azure Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fdd8b-291">definição de débito de desempenho de Olá só se aplica toocollection criação.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="fdd8b-292">Se Olá especificado coleção já existe, o débito não será modificado.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="fdd8b-293">Quando importar coleções toomultiple, a ferramenta de importação de Olá suporta fragmentação de hash com base.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="fdd8b-294">Neste cenário, especifique a propriedade de documento Olá desejar toouse como Olá chave de partição (se a chave de partição for deixada em branco, documentos será a aleatoriamente em coleções de destino Olá).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="fdd8b-295">Opcionalmente, pode especificar o campo na origem de importação de Olá deve ser utilizado como Olá propriedade de id do documento de base de dados do Azure Cosmos durante a importação de Olá (tenha em atenção que se documentos não contêm esta propriedade, em seguida, Olá importação ferramenta irá gerar um GUID como valor de propriedade de id de Olá).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="fdd8b-296">Existem várias opções avançadas de disponíveis durante a importação.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="fdd8b-297">Em primeiro lugar, enquanto a ferramenta de Olá inclui um volume de predefinição importar procedimento armazenado (BulkInsert.js), pode optar por toospecify seu próprio procedimento de importação armazenado:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Opção de sproc de inserção de em massa de BD do Cosmos captura de ecrã do Azure](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="fdd8b-299">Além disso, ao importar os tipos de data (por exemplo, a partir de SQL Server ou o MongoDB), pode escolher entre três opções de importação:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Opções de importação do BD do Cosmos captura de ecrã do Azure data hora](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="fdd8b-301">Cadeia: Manter como um valor de cadeia</span><span class="sxs-lookup"><span data-stu-id="fdd8b-301">String: Persist as a string value</span></span>
* <span data-ttu-id="fdd8b-302">Época: Manter como um valor de número de época</span><span class="sxs-lookup"><span data-stu-id="fdd8b-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="fdd8b-303">Ambas: Manter a cadeia e valores numéricos época.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="fdd8b-304">Esta opção irá criar um subdocument, por exemplo: "date_joined": {"Valor": "2013-10-21T21:17:25.2410000Z", "época": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="fdd8b-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="fdd8b-305">importador de em massa de BD do Azure Cosmos Olá tem seguinte de Olá adicionais opções avançadas:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="fdd8b-306">Tamanho do lote: Olá ferramenta predefinições tooa tamanho do lote de 50.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="fdd8b-307">Se Olá documentos toobe importado é grande, considere reduzir o tamanho do lote Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="fdd8b-308">Por outro lado, se Olá documentos toobe importado é pequeno, considere aumentar o tamanho do lote Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="fdd8b-309">Tamanho máximo de Script (bytes): a ferramenta de Olá predefinições tooa tamanho de script máximo de 512KB</span><span class="sxs-lookup"><span data-stu-id="fdd8b-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="fdd8b-310">Desative a geração de Id automática: Se toobe cada documento importada contém um campo de id, em seguida, selecionar esta opção pode aumentar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="fdd8b-311">Falta um campo de id exclusivo de documentos não serão importados.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="fdd8b-312">Atualização existente documentos: Olá ferramenta predefinições toonot substituir os documentos existentes com conflitos de id.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="fdd8b-313">A seleção desta opção permitirá a substituir os documentos existentes com ID correspondentes.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="fdd8b-314">Esta funcionalidade é útil para migrações de dados agendada que atualizam documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="fdd8b-315">Número de tentativas em caso de falha: Especifica Olá diversas vezes tooretry Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="fdd8b-316">Intervalo de repetição: Especifica quanto toowait entre repetir Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="fdd8b-317">Modo de ligação: Especifica toouse de modo de ligação de Olá com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="fdd8b-318">opções disponíveis Olá são DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="fdd8b-319">modos de ligação direta Olá são mais rápida, enquanto o modo de gateway de Olá é firewall mais amigável como o utiliza apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Importação em volume de captura de ecrã da BD do Cosmos Azure opções avançadas](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="fdd8b-321">modo de tooconnection de predefinições de ferramenta DirectTcp de importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="fdd8b-322">Se ocorrerem problemas de firewall, alternar modo tooconnection Gateway, porque requer apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="fdd8b-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (sequencial de registo de importação)</span><span class="sxs-lookup"><span data-stu-id="fdd8b-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="fdd8b-324">importador de sequencial de registo de base de dados do Azure Cosmos Olá permite-lhe tooimport de qualquer uma das opções de origem disponível Olá numa base de registo ao registo.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="fdd8b-325">Poderá escolher esta opção se estiver a importar tooan coleção existente que atingiu a quota de procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="fdd8b-326">Olá ferramenta suporta a importação tooa única coleção de base de dados do Azure Cosmos (partição única e várias partição), bem como a importação em dados estão particionados em várias coleções de partição única e/ou partição multi da BD do Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="fdd8b-327">Para obter mais informações sobre a criação de partições de dados, consulte [divisão em partições e o dimensionamento do BD Azure Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Opções de importação de registos sequencial de BD do Cosmos captura de ecrã do Azure](./media/import-data/documentdbsequential.png)

<span data-ttu-id="fdd8b-329">formato de Olá do Olá cadeia de ligação de base de dados do Azure Cosmos é:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="fdd8b-330">Olá cadeia de ligação de conta de base de dados do Azure Cosmos pode ser obtido a partir do painel de chaves de Olá de Olá portal do Azure, conforme descrito em [como toomanage uma conta de base de dados do Azure Cosmos](manage-account.md); no entanto, o nome de Olá da base de dados de Olá tem toohello toobe anexado cadeia de ligação no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="fdd8b-331">Utilize Olá verifique comando tooensure que Olá instância de base de dados do Azure Cosmos especificada no campo de cadeia de ligação de Olá pode ser acedido.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="fdd8b-332">tooimport tooa única coleção, introduza o nome de Olá de Olá coleção toowhich dados serão importados e clique no botão Adicionar de Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="fdd8b-333">tooimport toomultiple coleções, introduza o nome de cada coleção individualmente ou utilizar Olá seguindo a sintaxe toospecify várias coleções: *collection_prefix*[iniciar índice - índice de fim].</span><span class="sxs-lookup"><span data-stu-id="fdd8b-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="fdd8b-334">Ao especificar várias coleções através da sintaxe acima mencionados Olá, tenha em atenção Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="fdd8b-335">São suportados apenas número inteiro intervalo padrões de nome.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="fdd8b-336">Por exemplo, especificar a coleção [0-3] irá produzir Olá seguintes coleções: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="fdd8b-337">Pode utilizar uma sintaxe abreviada: recolha [3] irá emitir o mesmo conjunto de coleções mencionado no passo 1.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="fdd8b-338">Pode ser fornecida mais do que uma substituição.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-338">More than one substitution can be provided.</span></span> <span data-ttu-id="fdd8b-339">Por exemplo, a coleção [0-1], [0-9] irá gerar 20 nomes de colecção com líderes zeros (collection01,.. 02,... 03).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="fdd8b-340">Depois de Olá coleção nomes foram especificadas, escolhe o débito pretendido Olá Olá collection(s) (400 RUs too250 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="fdd8b-341">Para melhor desempenho de importação, escolha um maior débito.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="fdd8b-342">Para obter mais informações sobre os níveis de desempenho, consulte [níveis de desempenho na base de dados do Azure Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="fdd8b-343">Importar qualquer toocollections com débito > 10 000 RUs necessitarão de uma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="fdd8b-344">Se optar por toohave mais do que 250 000 RUs, terá de toofile um pedido no toohave portal Olá aumenta a sua conta.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="fdd8b-345">definição de débito de Olá só se aplica toocollection criação.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="fdd8b-346">Se Olá especificado coleção já existe, o débito não será modificado.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="fdd8b-347">Quando importar coleções toomultiple, a ferramenta de importação de Olá suporta fragmentação de hash com base.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="fdd8b-348">Neste cenário, especifique a propriedade de documento Olá desejar toouse como Olá chave de partição (se a chave de partição for deixada em branco, documentos será a aleatoriamente em coleções de destino Olá).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="fdd8b-349">Opcionalmente, pode especificar o campo na origem de importação de Olá deve ser utilizado como Olá propriedade de id do documento de base de dados do Azure Cosmos durante a importação de Olá (tenha em atenção que se documentos não contêm esta propriedade, em seguida, Olá importação ferramenta irá gerar um GUID como valor de propriedade de id de Olá).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="fdd8b-350">Existem várias opções avançadas de disponíveis durante a importação.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="fdd8b-351">Em primeiro lugar, ao importar os tipos de data (por exemplo, a partir de SQL Server ou o MongoDB), pode escolher entre três opções de importação:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Opções de importação do BD do Cosmos captura de ecrã do Azure data hora](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="fdd8b-353">Cadeia: Manter como um valor de cadeia</span><span class="sxs-lookup"><span data-stu-id="fdd8b-353">String: Persist as a string value</span></span>
* <span data-ttu-id="fdd8b-354">Época: Manter como um valor de número de época</span><span class="sxs-lookup"><span data-stu-id="fdd8b-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="fdd8b-355">Ambas: Manter a cadeia e valores numéricos época.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="fdd8b-356">Esta opção irá criar um subdocument, por exemplo: "date_joined": {"Valor": "2013-10-21T21:17:25.2410000Z", "época": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="fdd8b-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="fdd8b-357">Olá Azure Cosmos DB - importador sequencial de registo tem o seguinte de Olá adicionais opções avançadas:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="fdd8b-358">Número de pedidos paralelos: ferramenta Olá predefinições pedidos paralelas too2.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="fdd8b-359">Se Olá documentos toobe importado é pequeno, considere aumentar o número de Olá de pedidos paralelos.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="fdd8b-360">Tenha em atenção que o se este número é gerado muito, Olá importação pode ter a limitação.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="fdd8b-361">Desative a geração de Id automática: Se toobe cada documento importada contém um campo de id, em seguida, selecionar esta opção pode aumentar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="fdd8b-362">Falta um campo de id exclusivo de documentos não serão importados.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="fdd8b-363">Atualização existente documentos: Olá ferramenta predefinições toonot substituir os documentos existentes com conflitos de id.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="fdd8b-364">A seleção desta opção permitirá a substituir os documentos existentes com ID correspondentes.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="fdd8b-365">Esta funcionalidade é útil para migrações de dados agendada que atualizam documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="fdd8b-366">Número de tentativas em caso de falha: Especifica Olá diversas vezes tooretry Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="fdd8b-367">Intervalo de repetição: Especifica quanto toowait entre repetir Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="fdd8b-368">Modo de ligação: Especifica toouse de modo de ligação de Olá com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="fdd8b-369">opções disponíveis Olá são DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="fdd8b-370">modos de ligação direta Olá são mais rápida, enquanto o modo de gateway de Olá é firewall mais amigável como o utiliza apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Importação de registo sequencial de captura de ecrã da BD do Cosmos Azure opções avançadas](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="fdd8b-372">modo de tooconnection de predefinições de ferramenta DirectTcp de importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="fdd8b-373">Se ocorrerem problemas de firewall, alternar modo tooconnection Gateway, porque requer apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="fdd8b-374"><a id="IndexingPolicy"></a>Especificar uma política de indexação ao criar a base de dados do Azure Cosmos coleções</span><span class="sxs-lookup"><span data-stu-id="fdd8b-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="fdd8b-375">Ao permitir a migração de Olá coleções de toocreate ferramenta durante a importação, pode especificar a política de indexação Olá de coleções de Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="fdd8b-376">No Olá avançadas secção Opções de importação de em massa de BD do Azure Cosmos Olá e opções de registo do Azure Cosmos DB sequenciais, navegue até toohello secção de política de indexação.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Captura de ecrã do Cosmos DB indexação política Azure opções avançadas](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="fdd8b-378">Utilizar Olá opção da política de indexação avançada, pode selecionar um ficheiro de política de indexação, manualmente introduza uma política de indexação ou selecione um conjunto de modelos predefinidos (clicando com o botão direito na caixa de texto de política de indexação de Olá).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="fdd8b-379">os modelos de política de Olá Olá ferramenta fornece são:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="fdd8b-380">A predefinição.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-380">Default.</span></span> <span data-ttu-id="fdd8b-381">Esta política é melhor quando estiver a efetuar consultas de igualdade em relação a cadeias e utilizar ORDER BY, intervalo e consultas de igualdade para números.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="fdd8b-382">Esta política tem uma tolerância de armazenamento de índice inferior ao intervalo.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="fdd8b-383">Intervalo.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-383">Range.</span></span> <span data-ttu-id="fdd8b-384">Esta política é melhor que utilizar consultas de ORDER BY, intervalo e igualdade no ambos números e scripts.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="fdd8b-385">Esta política tem uma tolerância de armazenamento de índice mais alta que predefinido ou Hash.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Captura de ecrã do Cosmos DB indexação política Azure opções avançadas](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="fdd8b-387">Se não especificar uma política de indexação, em seguida, Olá predefinido política será aplicada.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="fdd8b-388">Para obter mais informações sobre as políticas de indexação, consulte [Azure Cosmos DB indexação políticas](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="fdd8b-389">Ficheiro de exportação de tooJSON</span><span class="sxs-lookup"><span data-stu-id="fdd8b-389">Export tooJSON file</span></span>
<span data-ttu-id="fdd8b-390">exportador de JSON de BD do Azure Cosmos Olá permite-lhe tooexport qualquer um dos Olá origem disponível opções tooa ficheiro JSON que contém uma matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="fdd8b-391">ferramenta de Olá irá processar a exportação de Olá para si, ou pode escolher o comando de migração do tooview Olá resultante e execute o comando de Olá por si.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="fdd8b-392">ficheiro JSON resultante Olá pode ser armazenado localmente ou no Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Opção de exportação de ficheiros local de captura de ecrã do Azure Cosmos DB JSON](./media/import-data/jsontarget.png)

![Opção de exportação de armazenamento de captura de ecrã do Blob do Azure Cosmos DB JSON do Azure](./media/import-data/jsontarget2.png)

<span data-ttu-id="fdd8b-395">Pode optar por Olá tooprettify resultante JSON, que irá aumentar o tamanho de Olá documento resultante Olá enquanto efetuar Olá contents humanos mais legível.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="fdd8b-396">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="fdd8b-396">Advanced configuration</span></span>
<span data-ttu-id="fdd8b-397">No ecrã de configuração avançada de Olá, especifique a localização de Olá dos toowhich de ficheiro de registo de Olá que gostaria de quaisquer erros de escrita.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="fdd8b-398">Olá seguintes regras aplicam-se a página de toothis:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="fdd8b-399">Se não for fornecido um nome de ficheiro, serão devolvidos todos os erros na página de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="fdd8b-400">Se não for fornecido um nome de ficheiro sem um diretório, em seguida, o ficheiro de Olá será criado (ou substituído) no diretório de ambiente atual Olá.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="fdd8b-401">Se selecionar um existente ficheiro, em seguida, o ficheiro de Olá serão substituídas, não existe nenhuma opção de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="fdd8b-402">Em seguida, escolha se todos os toolog, crítico, ou não existem mensagens de erro.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="fdd8b-403">Por fim, decida frequência Olá na mensagem de transferência de ecrã será atualizada com o progresso da mesma.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="fdd8b-404">Confirme as definições de importação e a linha de comandos de vista</span><span class="sxs-lookup"><span data-stu-id="fdd8b-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="fdd8b-405">Depois de especificar as informações da origem, informações de destino e configuração avançada, reveja o resumo de migração de Olá e, opcionalmente, vista/copiar Olá resultante comandos de migração (copiar comandos de Olá é útil tooautomate operações de importação):</span><span class="sxs-lookup"><span data-stu-id="fdd8b-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![Captura de ecrã do ecrã de resumo](./media/import-data/summary.png)
   
    ![Captura de ecrã do ecrã de resumo](./media/import-data/summarycommand.png)
2. <span data-ttu-id="fdd8b-408">Quando estiver satisfeito com as opções de origem e de destino, clique em **importação**.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="fdd8b-409">tempo decorrido de Olá, contagem transferida e informações da falha (se não fornecer um nome de ficheiro na configuração avançada Olá) irão atualizar como importar Olá está em curso.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="fdd8b-410">Depois de concluído, pode exportar resultados de Olá (por exemplo, toodeal com eventuais falhas de importação).</span><span class="sxs-lookup"><span data-stu-id="fdd8b-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Opção de exportação de captura de ecrã do Azure Cosmos DB JSON](./media/import-data/viewresults.png)
3. <span data-ttu-id="fdd8b-412">Também pode iniciar uma importação novo, mantendo Olá as definições existentes (por exemplo, escolha de informações, de origem e de destino de cadeia de ligação, etc.) ou repor todos os valores.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Opção de exportação de captura de ecrã do Azure Cosmos DB JSON](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="fdd8b-414">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fdd8b-414">Next steps</span></span>

<span data-ttu-id="fdd8b-415">Neste tutorial, fez seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="fdd8b-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fdd8b-416">Instalar ferramenta de migração de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="fdd8b-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="fdd8b-417">Dados importados a partir de origens de dados diferentes</span><span class="sxs-lookup"><span data-stu-id="fdd8b-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="fdd8b-418">Exportado a partir da base de dados do Azure Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="fdd8b-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="fdd8b-419">Agora pode prosseguir toohello próximo tutorial e obter informações como dados de tooquery utilizando a BD do Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd8b-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="fdd8b-420">Como tooquery dados?</span><span class="sxs-lookup"><span data-stu-id="fdd8b-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
