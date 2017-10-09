---
title: dados aaaMove Redshift Amazon utilizando o Data Factory | Microsoft Docs
description: Saiba mais sobre como dados toomove Redshift Amazon utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="50278-103">Mover dados de Redshift de Amazon utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="50278-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="50278-104">Este artigo explica como toouse Olá atividade de cópia em dados do Azure Data Factory toomove Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="50278-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="50278-105">artigo de Olá baseia-se Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="50278-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="50278-106">Pode copiar dados do arquivo de dados do Amazon Redshift tooany suportado sink.</span><span class="sxs-lookup"><span data-stu-id="50278-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="50278-107">Para obter uma lista dos arquivos de dados suportados como sinks pela atividade de cópia de Olá, consulte [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="50278-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="50278-108">Atualmente, a fábrica de dados suporta mover dados de arquivos de dados do Amazon Redshift tooother, mas não para mover dados de outra tooAmazon de arquivos de dados Redshift.</span><span class="sxs-lookup"><span data-stu-id="50278-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50278-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="50278-109">Prerequisites</span></span>
* <span data-ttu-id="50278-110">Se estiver a mover dados tooan arquivo de dados no local, instale [Data Management Gateway](data-factory-data-management-gateway.md) numa máquina no local.</span><span class="sxs-lookup"><span data-stu-id="50278-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="50278-111">Em seguida, conceder Data Management Gateway (endereço IP da utilização da máquina de Olá) Olá tooAmazon Redshift cluster de acesso.</span><span class="sxs-lookup"><span data-stu-id="50278-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="50278-112">Consulte [cluster de toohello de acesso de autorizar](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="50278-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="50278-113">Se estiver a mover o arquivo de dados do Azure de tooan de dados, consulte o artigo [intervalos de IP de centro de dados do Azure](https://www.microsoft.com/download/details.aspx?id=41653) para endereço de IP de computação de Olá e intervalos de SQL Server utilizados pelo Olá centros de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="50278-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="50278-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="50278-114">Getting started</span></span>
<span data-ttu-id="50278-115">Pode criar um pipeline com uma atividade de cópia move dados a partir de uma origem de Amazon Redshift utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="50278-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="50278-116">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="50278-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="50278-117">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="50278-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="50278-118">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="50278-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="50278-119">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="50278-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="50278-120">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="50278-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="50278-121">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="50278-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="50278-122">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="50278-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="50278-123">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="50278-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="50278-124">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="50278-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="50278-125">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="50278-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="50278-126">Para um exemplo com definições de JSON para entidades do Data Factory que os dados de um arquivo de dados do Amazon Redshift toocopy utilizadas, consulte [exemplo JSON: copiar dados do Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="50278-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="50278-127">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooAmazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="50278-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="50278-128">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="50278-128">Linked service properties</span></span>
<span data-ttu-id="50278-129">Olá, a tabela seguinte fornece uma descrição para JSON elementos específico tooAmazon serviço Redshift ligado.</span><span class="sxs-lookup"><span data-stu-id="50278-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="50278-130">Propriedade</span><span class="sxs-lookup"><span data-stu-id="50278-130">Property</span></span> | <span data-ttu-id="50278-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="50278-131">Description</span></span> | <span data-ttu-id="50278-132">Necessário</span><span class="sxs-lookup"><span data-stu-id="50278-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50278-133">tipo</span><span class="sxs-lookup"><span data-stu-id="50278-133">type</span></span> |<span data-ttu-id="50278-134">a propriedade de tipo Olá tem de ser definida: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="50278-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="50278-135">Sim</span><span class="sxs-lookup"><span data-stu-id="50278-135">Yes</span></span> |
| <span data-ttu-id="50278-136">servidor</span><span class="sxs-lookup"><span data-stu-id="50278-136">server</span></span> |<span data-ttu-id="50278-137">Nome anfitrião ou endereço IP do servidor de Amazon Redshift Olá.</span><span class="sxs-lookup"><span data-stu-id="50278-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="50278-138">Sim</span><span class="sxs-lookup"><span data-stu-id="50278-138">Yes</span></span> |
| <span data-ttu-id="50278-139">porta</span><span class="sxs-lookup"><span data-stu-id="50278-139">port</span></span> |<span data-ttu-id="50278-140">número de Olá de porta TCP de Olá Olá Amazon Redshift servidor utiliza toolisten para ligações de cliente.</span><span class="sxs-lookup"><span data-stu-id="50278-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="50278-141">Valor predefinido não,: 5439</span><span class="sxs-lookup"><span data-stu-id="50278-141">No, default value: 5439</span></span> |
| <span data-ttu-id="50278-142">base de dados</span><span class="sxs-lookup"><span data-stu-id="50278-142">database</span></span> |<span data-ttu-id="50278-143">Nome da base de dados do Olá Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="50278-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="50278-144">Sim</span><span class="sxs-lookup"><span data-stu-id="50278-144">Yes</span></span> |
| <span data-ttu-id="50278-145">o nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="50278-145">username</span></span> |<span data-ttu-id="50278-146">Nome de utilizador que tenha a base de dados do access toohello.</span><span class="sxs-lookup"><span data-stu-id="50278-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="50278-147">Sim</span><span class="sxs-lookup"><span data-stu-id="50278-147">Yes</span></span> |
| <span data-ttu-id="50278-148">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="50278-148">password</span></span> |<span data-ttu-id="50278-149">Palavra-passe da conta de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="50278-149">Password for hello user account.</span></span> |<span data-ttu-id="50278-150">Sim</span><span class="sxs-lookup"><span data-stu-id="50278-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="50278-151">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="50278-151">Dataset properties</span></span>
<span data-ttu-id="50278-152">Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="50278-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="50278-153">As secções, tais como a estrutura, a disponibilidade e a política são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="50278-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="50278-154">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="50278-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="50278-155">Fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="50278-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="50278-156">Olá typeProperties secção para o conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados do Amazon Redshift) tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="50278-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="50278-157">Propriedade</span><span class="sxs-lookup"><span data-stu-id="50278-157">Property</span></span> | <span data-ttu-id="50278-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="50278-158">Description</span></span> | <span data-ttu-id="50278-159">Necessário</span><span class="sxs-lookup"><span data-stu-id="50278-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50278-160">tableName</span><span class="sxs-lookup"><span data-stu-id="50278-160">tableName</span></span> |<span data-ttu-id="50278-161">Nome da tabela de Olá na base de dados do Amazon Redshift Olá pelo serviço ligado refere-se.</span><span class="sxs-lookup"><span data-stu-id="50278-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="50278-162">Não (se **consulta** de **RelationalSource** especificado)</span><span class="sxs-lookup"><span data-stu-id="50278-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="50278-163">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="50278-163">Copy activity properties</span></span>
<span data-ttu-id="50278-164">Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="50278-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="50278-165">Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="50278-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="50278-166">Enquanto, propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="50278-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="50278-167">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="50278-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="50278-168">Quando a origem da atividade de cópia é do tipo **RelationalSource** (que inclui o Amazon Redshift), na secção typeProperties, estão disponível Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="50278-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="50278-169">Propriedade</span><span class="sxs-lookup"><span data-stu-id="50278-169">Property</span></span> | <span data-ttu-id="50278-170">Descrição</span><span class="sxs-lookup"><span data-stu-id="50278-170">Description</span></span> | <span data-ttu-id="50278-171">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="50278-171">Allowed values</span></span> | <span data-ttu-id="50278-172">Necessário</span><span class="sxs-lookup"><span data-stu-id="50278-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="50278-173">consulta</span><span class="sxs-lookup"><span data-stu-id="50278-173">query</span></span> |<span data-ttu-id="50278-174">Utilize Olá consulta personalizada tooread dados.</span><span class="sxs-lookup"><span data-stu-id="50278-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="50278-175">Cadeia de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="50278-175">SQL query string.</span></span> <span data-ttu-id="50278-176">Por exemplo: selecionar * de MyTable.</span><span class="sxs-lookup"><span data-stu-id="50278-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="50278-177">Não (se **tableName** de **dataset** especificado)</span><span class="sxs-lookup"><span data-stu-id="50278-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="50278-178">Exemplo JSON: copiar dados do Amazon Redshift tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="50278-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="50278-179">Este exemplo mostra como toocopy dados a partir de um Redshift Amazon da base de dados tooan Blob Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="50278-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="50278-180">No entanto, os dados podem ser copiados **diretamente** tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="50278-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="50278-181">exemplo de Olá tem Olá seguintes entidades da fábrica de dados:</span><span class="sxs-lookup"><span data-stu-id="50278-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="50278-182">Um serviço ligado do tipo [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="50278-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="50278-183">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="50278-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="50278-184">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="50278-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="50278-185">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="50278-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="50278-186">A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="50278-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="50278-187">exemplo de Olá copia dados a partir num resultado de consulta Amazon Redshift tooa blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="50278-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="50278-188">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="50278-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="50278-189">**Serviço ligado do Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="50278-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="50278-190">**Serviço ligado do Storage do Azure:**</span><span class="sxs-lookup"><span data-stu-id="50278-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="50278-191">**Conjunto de dados entrado de Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="50278-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="50278-192">Definição `"external": true` informa o serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="50278-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="50278-193">Defina um conjunto de dados de entrada que não é produzido por uma atividade no pipeline de Olá tootrue esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="50278-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="50278-194">**Conjunto de dados de saída do Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="50278-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="50278-195">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="50278-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="50278-196">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="50278-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="50278-197">caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="50278-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="50278-198">**Atividade de cópia de um pipeline com a origem de Azure Redshift (RelationalSource) e o sink de Blob:**</span><span class="sxs-lookup"><span data-stu-id="50278-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="50278-199">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora.</span><span class="sxs-lookup"><span data-stu-id="50278-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="50278-200">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="50278-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="50278-201">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá passado toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="50278-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="50278-202">Mapeamento de tipo para o Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="50278-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="50278-203">Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá abordagem de dois passos a seguir:</span><span class="sxs-lookup"><span data-stu-id="50278-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="50278-204">Converter do tipo de too.NET de tipos de origem nativo</span><span class="sxs-lookup"><span data-stu-id="50278-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="50278-205">Converter do tipo de sink de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="50278-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="50278-206">Quando move dados tooAmazon Redshift, Olá seguintes mapeamentos é utilizada de tipos de too.NET Amazon Redshift tipos.</span><span class="sxs-lookup"><span data-stu-id="50278-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="50278-207">Tipo de Redshift Amazon</span><span class="sxs-lookup"><span data-stu-id="50278-207">Amazon Redshift Type</span></span> | <span data-ttu-id="50278-208">.NET com base em tipo</span><span class="sxs-lookup"><span data-stu-id="50278-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="50278-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="50278-209">SMALLINT</span></span> |<span data-ttu-id="50278-210">Int16</span><span class="sxs-lookup"><span data-stu-id="50278-210">Int16</span></span> |
| <span data-ttu-id="50278-211">NÚMERO INTEIRO</span><span class="sxs-lookup"><span data-stu-id="50278-211">INTEGER</span></span> |<span data-ttu-id="50278-212">Int32</span><span class="sxs-lookup"><span data-stu-id="50278-212">Int32</span></span> |
| <span data-ttu-id="50278-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="50278-213">BIGINT</span></span> |<span data-ttu-id="50278-214">Int64</span><span class="sxs-lookup"><span data-stu-id="50278-214">Int64</span></span> |
| <span data-ttu-id="50278-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="50278-215">DECIMAL</span></span> |<span data-ttu-id="50278-216">Decimal</span><span class="sxs-lookup"><span data-stu-id="50278-216">Decimal</span></span> |
| <span data-ttu-id="50278-217">REAL</span><span class="sxs-lookup"><span data-stu-id="50278-217">REAL</span></span> |<span data-ttu-id="50278-218">Único</span><span class="sxs-lookup"><span data-stu-id="50278-218">Single</span></span> |
| <span data-ttu-id="50278-219">PRECISÃO DUPLA</span><span class="sxs-lookup"><span data-stu-id="50278-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="50278-220">duplo</span><span class="sxs-lookup"><span data-stu-id="50278-220">Double</span></span> |
| <span data-ttu-id="50278-221">VALOR BOOLEANO</span><span class="sxs-lookup"><span data-stu-id="50278-221">BOOLEAN</span></span> |<span data-ttu-id="50278-222">Cadeia</span><span class="sxs-lookup"><span data-stu-id="50278-222">String</span></span> |
| <span data-ttu-id="50278-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="50278-223">CHAR</span></span> |<span data-ttu-id="50278-224">Cadeia</span><span class="sxs-lookup"><span data-stu-id="50278-224">String</span></span> |
| <span data-ttu-id="50278-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="50278-225">VARCHAR</span></span> |<span data-ttu-id="50278-226">Cadeia</span><span class="sxs-lookup"><span data-stu-id="50278-226">String</span></span> |
| <span data-ttu-id="50278-227">DATA</span><span class="sxs-lookup"><span data-stu-id="50278-227">DATE</span></span> |<span data-ttu-id="50278-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="50278-228">DateTime</span></span> |
| <span data-ttu-id="50278-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="50278-229">TIMESTAMP</span></span> |<span data-ttu-id="50278-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="50278-230">DateTime</span></span> |
| <span data-ttu-id="50278-231">TEXTO</span><span class="sxs-lookup"><span data-stu-id="50278-231">TEXT</span></span> |<span data-ttu-id="50278-232">Cadeia</span><span class="sxs-lookup"><span data-stu-id="50278-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="50278-233">Mapear colunas toosink de origem</span><span class="sxs-lookup"><span data-stu-id="50278-233">Map source toosink columns</span></span>
<span data-ttu-id="50278-234">toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="50278-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="50278-235">Repetíveis leitura a partir de origens relacionais</span><span class="sxs-lookup"><span data-stu-id="50278-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="50278-236">Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="50278-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="50278-237">No Azure Data Factory, pode voltar a executar um setor manualmente.</span><span class="sxs-lookup"><span data-stu-id="50278-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="50278-238">Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="50278-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="50278-239">Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado.</span><span class="sxs-lookup"><span data-stu-id="50278-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="50278-240">Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="50278-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="50278-241">Desempenho e a otimização</span><span class="sxs-lookup"><span data-stu-id="50278-241">Performance and Tuning</span></span>
<span data-ttu-id="50278-242">Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.</span><span class="sxs-lookup"><span data-stu-id="50278-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50278-243">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="50278-243">Next Steps</span></span>
<span data-ttu-id="50278-244">Consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="50278-244">See hello following articles:</span></span>

* <span data-ttu-id="50278-245">[Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criar um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="50278-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
