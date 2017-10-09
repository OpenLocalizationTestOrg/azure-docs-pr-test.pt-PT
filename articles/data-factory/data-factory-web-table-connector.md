---
title: "aaaMove dados da tabela da Web através do Azure Data Factory | Microsoft Docs"
description: "Saiba mais sobre como toomove dados de uma tabela de uma Web página utilizando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="a5da6-103">Mover dados de uma origem de tabela Web utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a5da6-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="a5da6-104">Este artigo descreve como toouse Olá atividade de cópia em dados do Azure Data Factory toomove a partir de uma tabela na tooa página Web suportado o arquivo de dados do sink.</span><span class="sxs-lookup"><span data-stu-id="a5da6-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="a5da6-105">Este artigo baseia-se Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo que apresenta uma descrição geral do movimento de dados com a lista de atividade e Olá de cópia de arquivos de dados suportados como sinks/origens.</span><span class="sxs-lookup"><span data-stu-id="a5da6-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="a5da6-106">Fábrica de dados suporta atualmente só armazena mover dados a partir de um tooother de dados de tabela da Web, mas não mover dados de outros dados armazena o destino de tabela tooa Web.</span><span class="sxs-lookup"><span data-stu-id="a5da6-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5da6-107">Este conector Web atualmente suporta apenas extrair conteúdo da tabela de uma página HTML.</span><span class="sxs-lookup"><span data-stu-id="a5da6-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="a5da6-108">utilizar tooretrieve dados a partir de um ponto final de HTTP/s, [conetor HTTP](data-factory-http-connector.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="a5da6-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a5da6-109">Introdução</span><span class="sxs-lookup"><span data-stu-id="a5da6-109">Getting started</span></span>
<span data-ttu-id="a5da6-110">Pode criar um pipeline com uma atividade de cópia move os dados de um arquivo de dados no local Cassandra utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="a5da6-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="a5da6-111">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="a5da6-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a5da6-112">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="a5da6-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="a5da6-113">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="a5da6-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a5da6-114">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="a5da6-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a5da6-115">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="a5da6-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="a5da6-116">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="a5da6-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a5da6-117">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="a5da6-118">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="a5da6-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a5da6-119">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="a5da6-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a5da6-120">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="a5da6-121">Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de uma tabela de web, consulte [exemplo JSON: copiar dados da tabela de Web tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="a5da6-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a5da6-122">Olá seguintes secções fornece detalhes sobre as propriedades JSON que estão a tabela de Web do toodefine utilizados Data Factory entidades tooa específico:</span><span class="sxs-lookup"><span data-stu-id="a5da6-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a5da6-123">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="a5da6-123">Linked service properties</span></span>
<span data-ttu-id="a5da6-124">Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooWeb ligado.</span><span class="sxs-lookup"><span data-stu-id="a5da6-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="a5da6-125">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a5da6-125">Property</span></span> | <span data-ttu-id="a5da6-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="a5da6-126">Description</span></span> | <span data-ttu-id="a5da6-127">Necessário</span><span class="sxs-lookup"><span data-stu-id="a5da6-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a5da6-128">tipo</span><span class="sxs-lookup"><span data-stu-id="a5da6-128">type</span></span> |<span data-ttu-id="a5da6-129">a propriedade de tipo Olá tem de ser definida: **Web**</span><span class="sxs-lookup"><span data-stu-id="a5da6-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="a5da6-130">Sim</span><span class="sxs-lookup"><span data-stu-id="a5da6-130">Yes</span></span> |
| <span data-ttu-id="a5da6-131">Url</span><span class="sxs-lookup"><span data-stu-id="a5da6-131">Url</span></span> |<span data-ttu-id="a5da6-132">Origem do URL toohello Web</span><span class="sxs-lookup"><span data-stu-id="a5da6-132">URL toohello Web source</span></span> |<span data-ttu-id="a5da6-133">Sim</span><span class="sxs-lookup"><span data-stu-id="a5da6-133">Yes</span></span> |
| <span data-ttu-id="a5da6-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a5da6-134">authenticationType</span></span> |<span data-ttu-id="a5da6-135">Anónimo.</span><span class="sxs-lookup"><span data-stu-id="a5da6-135">Anonymous.</span></span> |<span data-ttu-id="a5da6-136">Sim</span><span class="sxs-lookup"><span data-stu-id="a5da6-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="a5da6-137">Autenticação anónima</span><span class="sxs-lookup"><span data-stu-id="a5da6-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a5da6-138">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="a5da6-138">Dataset properties</span></span>
<span data-ttu-id="a5da6-139">Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="a5da6-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a5da6-140">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="a5da6-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a5da6-141">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a5da6-142">Olá typeProperties secção para o conjunto de dados do tipo **WebTable** tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="a5da6-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="a5da6-143">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a5da6-143">Property</span></span> | <span data-ttu-id="a5da6-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="a5da6-144">Description</span></span> | <span data-ttu-id="a5da6-145">Necessário</span><span class="sxs-lookup"><span data-stu-id="a5da6-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a5da6-146">tipo</span><span class="sxs-lookup"><span data-stu-id="a5da6-146">type</span></span> |<span data-ttu-id="a5da6-147">Tipo de conjunto de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-147">type of hello dataset.</span></span> <span data-ttu-id="a5da6-148">tem de ser definido demasiado**WebTable**</span><span class="sxs-lookup"><span data-stu-id="a5da6-148">must be set too**WebTable**</span></span> |<span data-ttu-id="a5da6-149">Sim</span><span class="sxs-lookup"><span data-stu-id="a5da6-149">Yes</span></span> |
| <span data-ttu-id="a5da6-150">Caminho</span><span class="sxs-lookup"><span data-stu-id="a5da6-150">path</span></span> |<span data-ttu-id="a5da6-151">Um relativo recurso de toohello do URL, que contém Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="a5da6-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="a5da6-152">Não.</span><span class="sxs-lookup"><span data-stu-id="a5da6-152">No.</span></span> <span data-ttu-id="a5da6-153">Quando o caminho não for especificado, é utilizada apenas Olá URL especificado na definição de serviço Olá ligado.</span><span class="sxs-lookup"><span data-stu-id="a5da6-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="a5da6-154">Índice</span><span class="sxs-lookup"><span data-stu-id="a5da6-154">index</span></span> |<span data-ttu-id="a5da6-155">índice de Olá da tabela de Olá no recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="a5da6-156">Consulte [Get índice de uma tabela numa página HTML](#get-index-of-a-table-in-an-html-page) secção para o índice de toogetting passos de uma tabela numa página HTML.</span><span class="sxs-lookup"><span data-stu-id="a5da6-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="a5da6-157">Sim</span><span class="sxs-lookup"><span data-stu-id="a5da6-157">Yes</span></span> |

<span data-ttu-id="a5da6-158">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="a5da6-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="a5da6-159">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="a5da6-159">Copy activity properties</span></span>
<span data-ttu-id="a5da6-160">Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="a5da6-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a5da6-161">Propriedades, tais como o nome, descrição e de saída, tabelas e política estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="a5da6-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="a5da6-162">Enquanto, propriedades disponíveis na secção de typeProperties Olá da atividade de Olá variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="a5da6-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a5da6-163">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a5da6-164">Atualmente, quando a origem de Olá na atividade de cópia é do tipo **WebSource**, sem propriedades adicionais são suportadas.</span><span class="sxs-lookup"><span data-stu-id="a5da6-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="a5da6-165">Exemplo JSON: copiar dados da tabela de Web tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="a5da6-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="a5da6-166">Olá seguinte exemplo mostra:</span><span class="sxs-lookup"><span data-stu-id="a5da6-166">hello following sample shows:</span></span>

1. <span data-ttu-id="a5da6-167">Um serviço ligado do tipo [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a5da6-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="a5da6-168">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a5da6-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a5da6-169">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a5da6-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="a5da6-170">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a5da6-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a5da6-171">A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [WebSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a5da6-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a5da6-172">exemplo de Olá copia dados a partir um tooan de tabela Web BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="a5da6-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="a5da6-173">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a5da6-174">Olá seguinte exemplo mostra como os dados de toocopy de um tooan de tabela de Web do Azure blob.</span><span class="sxs-lookup"><span data-stu-id="a5da6-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="a5da6-175">No entanto, é possível copiar dados diretamente tooany de Olá sinks Olá declarado no [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo utilizando Olá atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a5da6-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="a5da6-176">**Serviço ligado do Web** este exemplo utiliza Olá Web ligado serviço com a autenticação anónima.</span><span class="sxs-lookup"><span data-stu-id="a5da6-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="a5da6-177">Consulte [Web serviço ligado](#linked-service-properties) secção para diferentes tipos de autenticação, pode utilizar.</span><span class="sxs-lookup"><span data-stu-id="a5da6-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="a5da6-178">**Serviço ligado do Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="a5da6-178">**Azure Storage linked service**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="a5da6-179">**Conjunto de dados de entrada WebTable** definição **externo** demasiado**verdadeiro** informa o serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="a5da6-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="a5da6-180">Consulte [Get índice de uma tabela numa página HTML](#get-index-of-a-table-in-an-html-page) secção para o índice de toogetting passos de uma tabela numa página HTML.</span><span class="sxs-lookup"><span data-stu-id="a5da6-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="a5da6-181">**Conjunto de dados de saída de Blobs do Azure**</span><span class="sxs-lookup"><span data-stu-id="a5da6-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="a5da6-182">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="a5da6-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="a5da6-183">**Pipeline com atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="a5da6-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="a5da6-184">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora.</span><span class="sxs-lookup"><span data-stu-id="a5da6-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a5da6-185">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**WebSource** e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a5da6-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="a5da6-186">Consulte [propriedades do tipo WebSource](#copy-activity-type-properties) para Olá obter lista de propriedades suportadas por Olá WebSource.</span><span class="sxs-lookup"><span data-stu-id="a5da6-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="a5da6-187">Obter o índice de uma tabela de uma página HTML</span><span class="sxs-lookup"><span data-stu-id="a5da6-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="a5da6-188">Iniciar **Excel 2016** e um comutador toohello **dados** separador.</span><span class="sxs-lookup"><span data-stu-id="a5da6-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="a5da6-189">Clique em **nova consulta** na barra de ferramentas Olá, ponto demasiado**de outras origens** e clique em **da Web**.</span><span class="sxs-lookup"><span data-stu-id="a5da6-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Menu de consulta de energia](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="a5da6-191">No Olá **da Web** caixa de diálogo, introduza **URL** que pretende utilizar no ligado JSON do serviço (por exemplo: https://en.wikipedia.org/wiki/), juntamente com o caminho tem de especificar Olá conjunto de dados (por exemplo: AFI % 27s_100_Years... 100_Movies) e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5da6-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Caixa de diálogo Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="a5da6-193">URL utilizado neste exemplo: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="a5da6-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="a5da6-194">Se vir **conteúdo acesso Web** caixa de diálogo, o direito de Olá selecione **URL**, **autenticação**e clique em **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a5da6-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Aceder à caixa de diálogo de conteúdo Web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="a5da6-196">Clique num **tabela** item no conteúdo toosee de vista de árvore do Olá da tabela de Olá e, em seguida, clique em **editar** botão na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![Caixa de diálogo do navegador](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="a5da6-198">No Olá **Editor de consultas** janela, clique em **avançadas Editor** botão na barra de ferramentas Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![Botão Avançadas do Editor](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="a5da6-200">Na caixa de diálogo Editor avançadas de Olá, Olá número junto demasiado "Origem" é o índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5da6-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![Avançadas Editor - índice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="a5da6-202">Se estiver a utilizar o Excel 2013, utilize [Microsoft Power Query para Excel](https://www.microsoft.com/download/details.aspx?id=39379) índice de Olá tooget.</span><span class="sxs-lookup"><span data-stu-id="a5da6-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="a5da6-203">Consulte [Connect tooa web página](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a5da6-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="a5da6-204">passos de Olá são semelhantes, se estiver a utilizar [Microsoft Power BI para ambiente de trabalho](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="a5da6-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="a5da6-205">colunas de toomap toocolumns de conjunto de dados de origem do conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a5da6-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a5da6-206">Desempenho e a otimização</span><span class="sxs-lookup"><span data-stu-id="a5da6-206">Performance and Tuning</span></span>
<span data-ttu-id="a5da6-207">Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.</span><span class="sxs-lookup"><span data-stu-id="a5da6-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
