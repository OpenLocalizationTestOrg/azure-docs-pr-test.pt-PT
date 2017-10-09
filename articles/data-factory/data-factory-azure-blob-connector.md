---
title: dados aaaCopy para/de Blob Storage do Azure | Microsoft Docs
description: 'Saiba como toocopy blob dados no Azure Data Factory. Utilizar o nosso exemplo: como toocopy tooand de dados do Blob Storage do Azure e SQL Database do Azure.'
keywords: "dados de BLOBs, cópia de Blobs do azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="6346b-105">Copiar dados tooor do armazenamento de Blobs do Azure utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6346b-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="6346b-106">Este artigo explica como toouse Olá atividade de cópia no Azure Data Factory toocopy dados tooand do Blob Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="6346b-107">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="6346b-108">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="6346b-108">Overview</span></span>
<span data-ttu-id="6346b-109">Pode copiar dados de qualquer origem suportada armazenam tooAzure armazenamento de BLOBs ou a partir dos dados do Blob Storage do Azure tooany suportado sink armazenam dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="6346b-110">Olá tabela seguinte fornece uma lista de arquivos de dados suportada como origens ou sinks pela atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="6346b-111">Por exemplo, pode mover dados **de** uma base de dados do SQL Server ou uma base de dados SQL do Azure **para** um armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="6346b-112">E, pode copiar dados **de** blob storage do Azure **para** um Azure SQL Data Warehouse ou uma coleção de BD do Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="6346b-113">Cenários suportados</span><span class="sxs-lookup"><span data-stu-id="6346b-113">Supported scenarios</span></span>
<span data-ttu-id="6346b-114">Pode copiar dados **do Blob Storage do Azure** toohello seguir arquivos de dados:</span><span class="sxs-lookup"><span data-stu-id="6346b-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="6346b-115">Pode copiar dados de Olá seguir arquivos de dados **tooAzure Blob Storage**:</span><span class="sxs-lookup"><span data-stu-id="6346b-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="6346b-116">Atividade de cópia suporta a cópia de dados de / tooboth Storage do Azure para fins gerais contas de acesso frequente e/esporádico armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="6346b-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="6346b-117">atividade de Olá suporta **ler a partir de blocos, acrescentar ou blobs de páginas**, mas suporta **escrita de blobs de blocos tooonly**.</span><span class="sxs-lookup"><span data-stu-id="6346b-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="6346b-118">Armazenamento Premium do Azure não é suportado como um sink porque esteja associada a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="6346b-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="6346b-119">Atividade de cópia não elimina dados de origem Olá após Olá dados com êxito são copiada toohello destino.</span><span class="sxs-lookup"><span data-stu-id="6346b-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="6346b-120">Se precisar de dados de origem toodelete depois de uma cópia com êxito, crie um [atividade personalizada](data-factory-use-custom-activities.md) toodelete Olá dados e utilize a atividade de Olá no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="6346b-121">Por exemplo, consulte Olá [eliminar BLOBs ou pasta de exemplo no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="6346b-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="6346b-122">Introdução</span><span class="sxs-lookup"><span data-stu-id="6346b-122">Get started</span></span>
<span data-ttu-id="6346b-123">Pode criar um pipeline com uma atividade de cópia move os dados de/para um armazenamento de Blobs do Azure utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="6346b-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="6346b-124">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="6346b-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6346b-125">Este artigo tem um [instruções](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) para criar um dados toocopy do pipeline de um tooanother de localização de armazenamento de Blobs do Azure a localização de armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="6346b-126">Para um tutorial sobre a criação de um dado de toocopy do pipeline de uma base de dados SQL de tooAzure do Blob Storage do Azure, consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6346b-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="6346b-127">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="6346b-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6346b-128">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="6346b-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="6346b-129">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="6346b-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="6346b-130">Criar um **fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="6346b-130">Create a **data factory**.</span></span> <span data-ttu-id="6346b-131">Uma fábrica de dados pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="6346b-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="6346b-132">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="6346b-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="6346b-133">Por exemplo, se estiver a copiar dados de uma base de dados de SQL do Azure de tooan de armazenamento do BLOBs do Azure, pode cria dois serviços ligados toolink a conta de armazenamento do Azure e a fábrica de dados de tooyour de base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="6346b-134">As propriedades de serviço ligado que são específica tooAzure Blob Storage, consulte [ligado propriedades do serviço](#linked-service-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="6346b-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="6346b-135">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="6346b-136">Exemplo de Olá mencionado no passo último Olá, criar um contentor de blob do conjunto de dados toospecify Olá e a pasta que contém dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="6346b-137">Além disso, crie outra tabela do conjunto de dados toospecify Olá SQL na base de dados do SQL do Azure Olá que contém dados Olá copiados Olá do armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="6346b-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="6346b-138">As propriedades do conjunto de dados que são específica tooAzure Blob Storage, consulte [propriedades do dataset](#dataset-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="6346b-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="6346b-139">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="6346b-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="6346b-140">Exemplo de Olá mencionado anteriormente, que utilizar BlobSource como uma origem e SqlSink como um sink para atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="6346b-141">Da mesma forma, se estiver a copiar a partir da base de dados do Azure SQL tooAzure armazenamento de BLOBs, utilizar SqlSource e BlobSink na atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="6346b-142">Para as propriedades da atividade de cópia que são específica tooAzure Blob Storage, consulte [copiar propriedades da atividade](#copy-activity-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="6346b-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="6346b-143">Para obter detalhes sobre como toouse um arquivo de dados como uma origem ou de um receptor de mensagens em fila, clique em ligação Olá na secção anterior do Olá para o arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="6346b-144">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="6346b-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6346b-145">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6346b-146">Para exemplos com definições de JSON para entidades do Data Factory que são utilizados toocopy dados para/de um Blob Storage do Azure, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6346b-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="6346b-147">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="6346b-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6346b-148">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="6346b-148">Linked service properties</span></span>
<span data-ttu-id="6346b-149">Existem dois tipos de serviços ligados, pode utilizar toolink um Azure data factory de tooan do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="6346b-150">São: **AzureStorage** serviço ligado e **AzureStorageSas** serviço ligado.</span><span class="sxs-lookup"><span data-stu-id="6346b-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="6346b-151">Olá serviço ligado do Storage do Azure fornece fábrica de dados de Olá com acesso global toohello Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="6346b-152">Enquanto, Olá Azure armazenamento SAS (assinatura de acesso partilhado) ligado serviço fornece fábrica de dados de Olá com acesso restrito/vínculo de tempo toohello Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="6346b-153">Não existem não existem outras diferenças entre esses dois serviços ligados.</span><span class="sxs-lookup"><span data-stu-id="6346b-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="6346b-154">Escolha um serviço Olá ligado que se adapta às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="6346b-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="6346b-155">Olá secções seguintes fornecem mais detalhes sobre estes dois serviços ligados.</span><span class="sxs-lookup"><span data-stu-id="6346b-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="6346b-156">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6346b-156">Dataset properties</span></span>
<span data-ttu-id="6346b-157">toospecify toorepresent um conjunto de dados dados de entrada ou saídos num armazenamento de Blobs do Azure, pode definir a propriedade de tipo Olá de Olá conjunto de dados: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="6346b-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="6346b-158">Conjunto Olá **linkedServiceName** serviço ligado de propriedade do Olá dataset toohello nome Olá Storage do Azure ou SAS de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="6346b-159">Propriedades de tipo Olá do conjunto de dados de Olá especificar Olá **contentor do blob** e Olá **pasta** no armazenamento de BLOBs de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="6346b-160">Para obter uma lista completa de secções JSON & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6346b-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6346b-161">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="6346b-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6346b-162">Fábrica de dados suporta Olá os seguintes valores do tipo compatível com CLS .NET com base para fornecer informações sobre o tipo de "estrutura" para origens de dados de esquema no leitura como BLOBs do Azure: Int16, Int32, Int64, único, Double, Decimal, Byte [] e String, booleano, Datetime, e Guid Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="6346b-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="6346b-163">Fábrica de dados efetua automaticamente conversões de tipo ao mover o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="6346b-164">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá, etc., formato de dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="6346b-165">Olá typeProperties secção para o conjunto de dados do tipo **AzureBlob** dataset tem Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="6346b-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="6346b-166">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6346b-166">Property</span></span> | <span data-ttu-id="6346b-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="6346b-167">Description</span></span> | <span data-ttu-id="6346b-168">Necessário</span><span class="sxs-lookup"><span data-stu-id="6346b-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6346b-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="6346b-169">folderPath</span></span> |<span data-ttu-id="6346b-170">Contentor de toohello caminho e a pasta no armazenamento de BLOBs de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="6346b-171">Exemplo: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="6346b-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="6346b-172">Sim</span><span class="sxs-lookup"><span data-stu-id="6346b-172">Yes</span></span> |
| <span data-ttu-id="6346b-173">fileName</span><span class="sxs-lookup"><span data-stu-id="6346b-173">fileName</span></span> |<span data-ttu-id="6346b-174">Nome do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-174">Name of hello blob.</span></span> <span data-ttu-id="6346b-175">nome de ficheiro é opcional e maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6346b-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="6346b-176">Se especificar um nome de ficheiro, Olá atividade (incluindo cópia) funciona no Olá Blob específico.</span><span class="sxs-lookup"><span data-stu-id="6346b-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="6346b-177">Quando o nome de ficheiro não for especificado, cópia inclui todos os Blobs no folderPath Olá para conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="6346b-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="6346b-178">Quando **fileName** não está especificado para um conjunto de dados de saída e **preserveHierarchy** não foram especificadas no receptor de atividade, nome de Olá do ficheiro de Olá gerado seria no Olá segue este formato: Data.<Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="6346b-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="6346b-179">Não</span><span class="sxs-lookup"><span data-stu-id="6346b-179">No</span></span> |
| <span data-ttu-id="6346b-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6346b-180">partitionedBy</span></span> |<span data-ttu-id="6346b-181">partitionedBy propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="6346b-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="6346b-182">Pode utilizar-toospecify um folderPath dinâmica e nome de ficheiro de dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="6346b-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="6346b-183">Por exemplo, folderPath pode ser parametrizada para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="6346b-184">Consulte Olá [utilizando a secção de propriedade partitionedBy](#using-partitionedBy-property) para obter detalhes e exemplos.</span><span class="sxs-lookup"><span data-stu-id="6346b-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="6346b-185">Não</span><span class="sxs-lookup"><span data-stu-id="6346b-185">No</span></span> |
| <span data-ttu-id="6346b-186">formato</span><span class="sxs-lookup"><span data-stu-id="6346b-186">format</span></span> | <span data-ttu-id="6346b-187">é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="6346b-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6346b-188">Conjunto Olá **tipo** propriedade em formato tooone destes valores.</span><span class="sxs-lookup"><span data-stu-id="6346b-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="6346b-189">Para obter mais informações, consulte [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc formato](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato](data-factory-supported-file-and-compression-formats.md#parquet-format) secções.</span><span class="sxs-lookup"><span data-stu-id="6346b-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6346b-190">Se quiser demasiado**copiar ficheiros como-é** entre arquivos baseados em ficheiros (cópia binário), ignorar a secção de formato Olá em ambas as definições do conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="6346b-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6346b-191">Não</span><span class="sxs-lookup"><span data-stu-id="6346b-191">No</span></span> |
| <span data-ttu-id="6346b-192">Compressão</span><span class="sxs-lookup"><span data-stu-id="6346b-192">compression</span></span> | <span data-ttu-id="6346b-193">Especifique o tipo de Olá e nível de compressão de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="6346b-194">Tipos suportados são: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="6346b-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="6346b-195">Níveis suportados são: **Optimal** e **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="6346b-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6346b-196">Para obter mais informações, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="6346b-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6346b-197">Não</span><span class="sxs-lookup"><span data-stu-id="6346b-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="6346b-198">Utilizar a propriedade partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6346b-198">Using partitionedBy property</span></span>
<span data-ttu-id="6346b-199">Tal como mencionado na secção anterior Olá, pode especificar um folderPath dinâmica e o nome de ficheiro de dados de séries de tempo com Olá **partitionedBy** propriedade, [funções de Data Factory e variáveis do sistema Olá](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="6346b-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="6346b-200">Para obter mais informações sobre conjuntos de dados de séries de tempo, agendar e setores, consulte [criar conjuntos de dados](data-factory-create-datasets.md) e [agendamento e execução](data-factory-scheduling-and-execution.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="6346b-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="6346b-201">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="6346b-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="6346b-202">Neste exemplo, {setor} é substituído pelo valor da Olá da variável de sistema do Data Factory SliceStart no formato de Olá (YYYYMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="6346b-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="6346b-203">Olá SliceStart refere-se a hora de toostart do setor Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="6346b-204">Olá folderPath é diferente para cada setor.</span><span class="sxs-lookup"><span data-stu-id="6346b-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="6346b-205">Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="6346b-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="6346b-206">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="6346b-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="6346b-207">Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em separado variáveis que são utilizadas pelas propriedades folderPath e nome de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6346b-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="6346b-208">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="6346b-208">Copy activity properties</span></span>
<span data-ttu-id="6346b-209">Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6346b-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6346b-210">Propriedades, tais como o nome, descrição e de saída, conjuntos de dados e as políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="6346b-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="6346b-211">Enquanto, propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="6346b-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="6346b-212">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="6346b-213">Se estiver a mover dados de um Blob Storage do Azure, definir o tipo de origem Olá na atividade de cópia de Olá demasiado**BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="6346b-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="6346b-214">Da mesma forma, se estiver a mover dados tooan Blob Storage do Azure, definir o tipo de sink Olá na atividade de cópia de Olá demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6346b-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="6346b-215">Esta secção fornece uma lista de propriedades suportadas por BlobSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="6346b-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="6346b-216">**BlobSource** suporta Olá seguintes propriedades no Olá **typeProperties** secção:</span><span class="sxs-lookup"><span data-stu-id="6346b-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="6346b-217">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6346b-217">Property</span></span> | <span data-ttu-id="6346b-218">Descrição</span><span class="sxs-lookup"><span data-stu-id="6346b-218">Description</span></span> | <span data-ttu-id="6346b-219">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="6346b-219">Allowed values</span></span> | <span data-ttu-id="6346b-220">Necessário</span><span class="sxs-lookup"><span data-stu-id="6346b-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6346b-221">Recursiva</span><span class="sxs-lookup"><span data-stu-id="6346b-221">recursive</span></span> |<span data-ttu-id="6346b-222">Indica se Olá é ler dados recursivamente subpastas Olá ou apenas a pasta especificada Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="6346b-223">TRUE (valor predefinido), False</span><span class="sxs-lookup"><span data-stu-id="6346b-223">True (default value), False</span></span> |<span data-ttu-id="6346b-224">Não</span><span class="sxs-lookup"><span data-stu-id="6346b-224">No</span></span> |

<span data-ttu-id="6346b-225">**BlobSink** suporta as seguintes propriedades de Olá **typeProperties** secção:</span><span class="sxs-lookup"><span data-stu-id="6346b-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="6346b-226">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6346b-226">Property</span></span> | <span data-ttu-id="6346b-227">Descrição</span><span class="sxs-lookup"><span data-stu-id="6346b-227">Description</span></span> | <span data-ttu-id="6346b-228">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="6346b-228">Allowed values</span></span> | <span data-ttu-id="6346b-229">Necessário</span><span class="sxs-lookup"><span data-stu-id="6346b-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6346b-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6346b-230">copyBehavior</span></span> |<span data-ttu-id="6346b-231">Define o comportamento de cópia de Olá quando a origem de Olá é BlobSource ou sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="6346b-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="6346b-232"><b>PreserveHierarchy</b>: preserva Olá hierarquia de ficheiros na pasta de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="6346b-233">o caminho relativo Olá da pasta de toosource do ficheiro de origem é idêntico toohello caminho relativo de tootarget da pasta do ficheiro de destino.</span><span class="sxs-lookup"><span data-stu-id="6346b-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="6346b-234"><b>FlattenHierarchy</b>: todos os ficheiros da pasta de origem Olá estão em Olá primeiro níveis da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="6346b-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="6346b-235">os ficheiros de destino Olá ter nome automaticamente gerado.</span><span class="sxs-lookup"><span data-stu-id="6346b-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="6346b-236"><b>MergeFiles</b>: une todos os ficheiros a partir do ficheiro de tooone da pasta de origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="6346b-237">Se Olá nome de ficheiro/Blob for especificado, o nome de ficheiro intercalada de Olá seria o nome especificado Olá; caso contrário, seria nome de ficheiro gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6346b-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="6346b-238">Não</span><span class="sxs-lookup"><span data-stu-id="6346b-238">No</span></span> |

<span data-ttu-id="6346b-239">**BlobSource** também suporta estas duas propriedades para compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="6346b-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="6346b-240">**treatEmptyAsNull**: Especifica se uma cadeia nula ou vazia tootreat como um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="6346b-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="6346b-241">**skipHeaderLineCount** -Especifica o número de linhas tem de ser ignoradas.</span><span class="sxs-lookup"><span data-stu-id="6346b-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="6346b-242">É aplicável apenas ao conjunto de dados de entrada está a utilizar TextFormat.</span><span class="sxs-lookup"><span data-stu-id="6346b-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="6346b-243">Da mesma forma, **BlobSink** suporta Olá seguinte propriedade para compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="6346b-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="6346b-244">**blobWriterAddHeader**: Especifica se tooadd um cabeçalho de definições da coluna ao escrever tooan conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="6346b-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="6346b-245">Olá suporte agora de conjuntos de dados seguintes propriedades que implementam Olá a mesma funcionalidade: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="6346b-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="6346b-246">Olá tabela seguinte fornece orientações sobre como utilizar propriedades de novo conjunto de dados Olá em vez destas propriedades de origem/sink do blob.</span><span class="sxs-lookup"><span data-stu-id="6346b-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="6346b-247">Propriedade da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="6346b-247">Copy Activity property</span></span> | <span data-ttu-id="6346b-248">Propriedade de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6346b-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="6346b-249">skipHeaderLineCount no BlobSource</span><span class="sxs-lookup"><span data-stu-id="6346b-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="6346b-250">skipLineCount e firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="6346b-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="6346b-251">As linhas são ignoradas pela primeira vez e, em seguida, a primeira linha de Olá é lido como um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="6346b-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="6346b-252">treatEmptyAsNull no BlobSource</span><span class="sxs-lookup"><span data-stu-id="6346b-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="6346b-253">treatEmptyAsNull no conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="6346b-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="6346b-254">blobWriterAddHeader no BlobSink</span><span class="sxs-lookup"><span data-stu-id="6346b-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="6346b-255">firstRowAsHeader no conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="6346b-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="6346b-256">Consulte [especificando TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) secção para obter informações detalhadas sobre estas propriedades.</span><span class="sxs-lookup"><span data-stu-id="6346b-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="6346b-257">Exemplos de recursiva e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6346b-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="6346b-258">Esta secção descreve o comportamento resultante de Olá de operação de cópia de Olá para diferentes combinações de valores recursiva e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="6346b-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="6346b-259">Recursiva</span><span class="sxs-lookup"><span data-stu-id="6346b-259">recursive</span></span> | <span data-ttu-id="6346b-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6346b-260">copyBehavior</span></span> | <span data-ttu-id="6346b-261">Comportamento resultante</span><span class="sxs-lookup"><span data-stu-id="6346b-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6346b-262">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="6346b-262">true</span></span> |<span data-ttu-id="6346b-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="6346b-263">preserveHierarchy</span></span> |<span data-ttu-id="6346b-264">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="6346b-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="6346b-265">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-265">Folder1</span></span><br/><span data-ttu-id="6346b-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="6346b-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6346b-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="6346b-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6346b-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6346b-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6346b-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="6346b-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6346b-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6346b-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6346b-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6346b-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6346b-272">pasta de destino Olá Pasta1 é criada com Olá mesmo estrutura como origem Olá</span><span class="sxs-lookup"><span data-stu-id="6346b-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="6346b-273">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-273">Folder1</span></span><br/><span data-ttu-id="6346b-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="6346b-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6346b-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="6346b-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6346b-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6346b-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6346b-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="6346b-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6346b-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6346b-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6346b-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="6346b-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="6346b-280">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="6346b-280">true</span></span> |<span data-ttu-id="6346b-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="6346b-281">flattenHierarchy</span></span> |<span data-ttu-id="6346b-282">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="6346b-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="6346b-283">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-283">Folder1</span></span><br/><span data-ttu-id="6346b-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="6346b-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6346b-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="6346b-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6346b-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6346b-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6346b-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="6346b-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6346b-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6346b-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6346b-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6346b-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6346b-290">destino de Olá Pasta1 é criado com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="6346b-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="6346b-291">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-291">Folder1</span></span><br/><span data-ttu-id="6346b-292">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1</span><span class="sxs-lookup"><span data-stu-id="6346b-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="6346b-293">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2</span><span class="sxs-lookup"><span data-stu-id="6346b-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="6346b-294">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File3</span><span class="sxs-lookup"><span data-stu-id="6346b-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="6346b-295">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File4</span><span class="sxs-lookup"><span data-stu-id="6346b-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="6346b-296">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File5</span><span class="sxs-lookup"><span data-stu-id="6346b-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="6346b-297">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="6346b-297">true</span></span> |<span data-ttu-id="6346b-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="6346b-298">mergeFiles</span></span> |<span data-ttu-id="6346b-299">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="6346b-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="6346b-300">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-300">Folder1</span></span><br/><span data-ttu-id="6346b-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="6346b-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6346b-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="6346b-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6346b-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6346b-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6346b-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="6346b-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6346b-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6346b-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6346b-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6346b-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6346b-307">destino de Olá Pasta1 é criado com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="6346b-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="6346b-308">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-308">Folder1</span></span><br/><span data-ttu-id="6346b-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + ficheiro 5 é intercalado conteúdo para um ficheiro com nome de ficheiro gerado automaticamente</span><span class="sxs-lookup"><span data-stu-id="6346b-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="6346b-310">FALSO</span><span class="sxs-lookup"><span data-stu-id="6346b-310">false</span></span> |<span data-ttu-id="6346b-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="6346b-311">preserveHierarchy</span></span> |<span data-ttu-id="6346b-312">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="6346b-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="6346b-313">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-313">Folder1</span></span><br/><span data-ttu-id="6346b-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="6346b-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6346b-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="6346b-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6346b-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6346b-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6346b-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="6346b-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6346b-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6346b-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6346b-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6346b-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6346b-320">pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura</span><span class="sxs-lookup"><span data-stu-id="6346b-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="6346b-321">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-321">Folder1</span></span><br/><span data-ttu-id="6346b-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="6346b-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6346b-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="6346b-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="6346b-324">Não Subfolder1 com File3, File4 e File5 captado.</span><span class="sxs-lookup"><span data-stu-id="6346b-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="6346b-325">FALSO</span><span class="sxs-lookup"><span data-stu-id="6346b-325">false</span></span> |<span data-ttu-id="6346b-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="6346b-326">flattenHierarchy</span></span> |<span data-ttu-id="6346b-327">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="6346b-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="6346b-328">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-328">Folder1</span></span><br/><span data-ttu-id="6346b-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="6346b-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6346b-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="6346b-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6346b-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6346b-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6346b-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="6346b-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6346b-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6346b-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6346b-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6346b-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6346b-335">pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura</span><span class="sxs-lookup"><span data-stu-id="6346b-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="6346b-336">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-336">Folder1</span></span><br/><span data-ttu-id="6346b-337">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1</span><span class="sxs-lookup"><span data-stu-id="6346b-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="6346b-338">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2</span><span class="sxs-lookup"><span data-stu-id="6346b-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="6346b-339">Não Subfolder1 com File3, File4 e File5 captado.</span><span class="sxs-lookup"><span data-stu-id="6346b-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="6346b-340">FALSO</span><span class="sxs-lookup"><span data-stu-id="6346b-340">false</span></span> |<span data-ttu-id="6346b-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="6346b-341">mergeFiles</span></span> |<span data-ttu-id="6346b-342">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="6346b-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="6346b-343">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-343">Folder1</span></span><br/><span data-ttu-id="6346b-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="6346b-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6346b-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="6346b-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6346b-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6346b-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6346b-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="6346b-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6346b-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6346b-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6346b-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6346b-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6346b-350">pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura</span><span class="sxs-lookup"><span data-stu-id="6346b-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="6346b-351">Pasta1</span><span class="sxs-lookup"><span data-stu-id="6346b-351">Folder1</span></span><br/><span data-ttu-id="6346b-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 conteúdos são intercalados para um ficheiro com nome de ficheiro gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6346b-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="6346b-353">nome gerado automaticamente para File1</span><span class="sxs-lookup"><span data-stu-id="6346b-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="6346b-354">Não Subfolder1 com File3, File4 e File5 captado.</span><span class="sxs-lookup"><span data-stu-id="6346b-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="6346b-355">EXPLICAÇÃO passo a passo: Dados Assistente de cópia de utilização toocopy para/de armazenamento de BLOBs</span><span class="sxs-lookup"><span data-stu-id="6346b-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="6346b-356">Vamos ver como o armazenamento de BLOBs de tooquickly copiar dados para / do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="6346b-357">Nestas instruções, armazena os dados de origem e destino do tipo: Blob Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="6346b-358">Olá pipeline nestas instruções copia dados a partir de uma pasta de tooanother nas Olá mesmo contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="6346b-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="6346b-359">Estas instruções se tooshow intencionalmente simple que as definições ou propriedades quando utilizar o armazenamento de Blob como uma origem ou o sink.</span><span class="sxs-lookup"><span data-stu-id="6346b-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="6346b-360">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6346b-360">Prerequisites</span></span>
1. <span data-ttu-id="6346b-361">Criar um para fins gerais **conta do Storage do Azure** se ainda não tiver um.</span><span class="sxs-lookup"><span data-stu-id="6346b-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="6346b-362">Utilizar o armazenamento de BLOBs de Olá como ambos **origem** e **destino** armazenam dados nestas instruções.</span><span class="sxs-lookup"><span data-stu-id="6346b-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="6346b-363">Se não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo para passos toocreate um.</span><span class="sxs-lookup"><span data-stu-id="6346b-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="6346b-364">Criar um contentor do blob denominado **adfblobconnector** na conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="6346b-365">Crie uma pasta denominada **entrada** no Olá **adfblobconnector** contentor.</span><span class="sxs-lookup"><span data-stu-id="6346b-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="6346b-366">Crie um ficheiro denominado **emp.txt** com Olá seguir conteúdo e carregá-la toohello **entrada** pasta utilizando ferramentas como [Explorador de armazenamento do Azure](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="6346b-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="6346b-367">Criar fábrica de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="6346b-367">Create hello data factory</span></span>
1. <span data-ttu-id="6346b-368">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6346b-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6346b-369">Clique em **+ novo** no canto superior esquerdo de Olá, clique em **Intelligence + análise**e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="6346b-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="6346b-370">No Olá **nova fábrica de dados** painel:</span><span class="sxs-lookup"><span data-stu-id="6346b-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="6346b-371">Introduza **ADFBlobConnectorDF** para Olá **nome**.</span><span class="sxs-lookup"><span data-stu-id="6346b-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="6346b-372">nome de Olá do Olá do Azure data factory deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="6346b-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="6346b-373">Se receber o erro de Olá: `*Data factory name “ADFBlobConnectorDF” is not available`, altere o nome de Olá do Olá data factory (por exemplo, yournameADFBlobConnectorDF) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="6346b-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="6346b-374">Veja o tópico [Data Factory – Naming Rules (Data Factory – Regras de Nomenclatura)](data-factory-naming-rules.md) para obter as regras de nomenclatura dos artefactos do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6346b-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="6346b-375">Selecione a sua **subscrição** do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="6346b-376">Para o grupo de recursos, selecione **utilização existente** tooselect um recurso grupo (ou existente) selecione **criar nova** tooenter um nome para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6346b-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="6346b-377">Selecione um **localização** Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="6346b-378">Selecione **Pin toodashboard** caixa de verificação na parte inferior de Olá do painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="6346b-379">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6346b-379">Click **Create**.</span></span>
3. <span data-ttu-id="6346b-380">Depois de concluída a criação de Olá, consulte Olá **Data Factory** painel conforme mostrado no Olá seguinte imagem: ![home page da fábrica de dados](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="6346b-381">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="6346b-381">Copy Wizard</span></span>
1. <span data-ttu-id="6346b-382">Na home page da Olá fábrica de dados, clique em Olá **copiar dados [pré-visualização]** mosaico toolaunch **Assistente de cópia de dados** num separador separado.</span><span class="sxs-lookup"><span data-stu-id="6346b-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="6346b-383">Se vir esse browser da web Olá é bloqueada no "A autorizar …", desative/desmarque **bloquear cookies de terceiros e dados do site** definição (ou) mantenha-a ativada e crie uma exceção para **login.microsoftonline.com**e, em seguida, tente iniciar novamente o Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="6346b-384">No Olá **propriedades** página:</span><span class="sxs-lookup"><span data-stu-id="6346b-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="6346b-385">Introduza **CopyPipeline** para **nome da tarefa**.</span><span class="sxs-lookup"><span data-stu-id="6346b-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="6346b-386">nome da tarefa Olá é o nome de Olá do pipeline de Olá na fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="6346b-387">Introduza um **Descrição** tarefa Olá (opcional).</span><span class="sxs-lookup"><span data-stu-id="6346b-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="6346b-388">Para **cadência de tarefas ou agenda de tarefas**, manter Olá **regularmente executado numa agenda** opção.</span><span class="sxs-lookup"><span data-stu-id="6346b-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="6346b-389">Se pretender toorun esta tarefa apenas uma vez em vez de ser executado repetidamente numa agenda, selecione **executar agora uma vez**.</span><span class="sxs-lookup"><span data-stu-id="6346b-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="6346b-390">Se selecionar, **executar agora uma vez** opção, uma [pipeline Monouso](data-factory-create-pipelines.md#onetime-pipeline) é criado.</span><span class="sxs-lookup"><span data-stu-id="6346b-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="6346b-391">Manter Olá para **periódica padrão**.</span><span class="sxs-lookup"><span data-stu-id="6346b-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="6346b-392">Esta tarefa é executada diariamente entre Olá começar e termina horas especificar no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="6346b-393">Olá alteração **data hora de início** demasiado**21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="6346b-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="6346b-394">Olá alteração **data hora de fim** demasiado**25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="6346b-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="6346b-395">Poderá pretender data de Olá tootype em vez de navegar pelas calendário Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="6346b-396">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6346b-396">Click **Next**.</span></span>
      <span data-ttu-id="6346b-397">![Ferramenta copiar – página de propriedades](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="6346b-398">No Olá **arquivo de dados de origem** página, clique em **Blob Storage do Azure** mosaico.</span><span class="sxs-lookup"><span data-stu-id="6346b-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="6346b-399">Utiliza este arquivo de dados de origem do página toospecify Olá Olá tarefa de cópia.</span><span class="sxs-lookup"><span data-stu-id="6346b-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="6346b-400">Pode utilizar um serviço ligado do arquivo de dados existente (ou) especificar um novo arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="6346b-401">serviço ligado de toouse existente, deverá selecionar **de serviços ligados existentes** e selecione Olá serviço ligado correto.</span><span class="sxs-lookup"><span data-stu-id="6346b-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="6346b-402">![Ferramenta copiar – página do arquivo de dados de origem](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="6346b-403">No Olá **especificar conta de armazenamento de Blobs do Azure Olá** página:</span><span class="sxs-lookup"><span data-stu-id="6346b-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="6346b-404">Mantenha o nome de Olá gerado automaticamente para **nome da ligação**.</span><span class="sxs-lookup"><span data-stu-id="6346b-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="6346b-405">nome da ligação Olá é o nome de Olá do serviço de Olá ligado do tipo: armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="6346b-406">Confirme que a opção **A partir de subscrições do Azure** está selecionada para o **Método de seleção de contas**.</span><span class="sxs-lookup"><span data-stu-id="6346b-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="6346b-407">Selecione a sua subscrição do Azure ou manter **Selecionar tudo** para **subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="6346b-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="6346b-408">Selecione um **conta do storage do Azure** de Olá contas disponível na subscrição Olá selecionado de lista de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="6346b-409">Pode também escolher tooenter as definições de conta de armazenamento manualmente selecionando **introduzir manualmente** opção para Olá **método de seleção de contas**.</span><span class="sxs-lookup"><span data-stu-id="6346b-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="6346b-410">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6346b-410">Click **Next**.</span></span> 
      <span data-ttu-id="6346b-411">![Ferramenta copiar – especificar a conta de armazenamento de Blobs do Azure Olá](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="6346b-412">No **pasta ou ficheiro de entrada escolha Olá** página:</span><span class="sxs-lookup"><span data-stu-id="6346b-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="6346b-413">Faça duplo clique em **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="6346b-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="6346b-414">Selecione **entrada**e clique em **escolha**.</span><span class="sxs-lookup"><span data-stu-id="6346b-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="6346b-415">Nestas instruções, selecionar pasta de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="6346b-416">Pode também selecionar Olá emp.txt ficheiro na pasta Olá em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6346b-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="6346b-417">![Ferramenta copiar – escolha a pasta ou ficheiro de entrada Olá](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="6346b-418">No Olá **pasta ou ficheiro de entrada escolha Olá** página:</span><span class="sxs-lookup"><span data-stu-id="6346b-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="6346b-419">Confirme que Olá **ficheiro ou pasta** estiver definido demasiado**adfblobconnector/entrada**.</span><span class="sxs-lookup"><span data-stu-id="6346b-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="6346b-420">Se forem ficheiros Olá em subpastas, por exemplo, 2017/04/01, 2017/04/02 e assim sucessivamente, introduza adfblobconnector/valor / {year} / {month} / {day} para o ficheiro ou pasta.</span><span class="sxs-lookup"><span data-stu-id="6346b-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="6346b-421">Quando prime SEPARADOR fora de caixa de texto Olá, será apresentada três formatos de tooselect na lista pendente (AAAA) de ano, mês (MM) e dia (dd).</span><span class="sxs-lookup"><span data-stu-id="6346b-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="6346b-422">Não defina **copiar recursivamente ficheiro**.</span><span class="sxs-lookup"><span data-stu-id="6346b-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="6346b-423">Selecione este passam de toorecursively opção através de pastas para ficheiros toobe toohello copiados de destino.</span><span class="sxs-lookup"><span data-stu-id="6346b-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="6346b-424">Não Olá **cópia binária** opção.</span><span class="sxs-lookup"><span data-stu-id="6346b-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="6346b-425">Selecione esta opção tooperform uma cópia binária do destino de toohello do ficheiro de origem.</span><span class="sxs-lookup"><span data-stu-id="6346b-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="6346b-426">Não selecione para estas instruções para que possa ver mais opções em páginas seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="6346b-427">Confirme que Olá **tipo de compressão** estiver definido demasiado**nenhum**.</span><span class="sxs-lookup"><span data-stu-id="6346b-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="6346b-428">Selecione um valor para esta opção se os ficheiros de origem são comprimidos dos formatos de Olá suportado.</span><span class="sxs-lookup"><span data-stu-id="6346b-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="6346b-429">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6346b-429">Click **Next**.</span></span>
    <span data-ttu-id="6346b-430">![Ferramenta copiar – escolha a pasta ou ficheiro de entrada Olá](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="6346b-431">No Olá **definições do formato de ficheiro** página, verá os delimitadores Olá e esquema de Olá que é detetada automaticamente pelo Assistente de Olá ao analisar o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="6346b-432">Confirmar Olá seguintes opções: uma.</span><span class="sxs-lookup"><span data-stu-id="6346b-432">Confirm hello following options: a.</span></span> <span data-ttu-id="6346b-433">Olá **formato de ficheiro** estiver definido demasiado**formato de texto**.</span><span class="sxs-lookup"><span data-stu-id="6346b-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="6346b-434">Pode ver todos os formatos de Olá suportado Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="6346b-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="6346b-435">Por exemplo: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="6346b-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="6346b-436">b.</span><span class="sxs-lookup"><span data-stu-id="6346b-436">b.</span></span> <span data-ttu-id="6346b-437">Olá **delimitador de coluna** estiver definido demasiado`Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="6346b-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="6346b-438">Pode ver Olá outros delimitadores de coluna suportados pela fábrica de dados no Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="6346b-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="6346b-439">Também pode especificar um delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="6346b-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="6346b-440">c.</span><span class="sxs-lookup"><span data-stu-id="6346b-440">c.</span></span> <span data-ttu-id="6346b-441">Olá **delimitador de linha** estiver definido demasiado`Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="6346b-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="6346b-442">Pode ver Olá outros delimitadores de linha suportados pela fábrica de dados no Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="6346b-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="6346b-443">Também pode especificar um delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="6346b-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="6346b-444">d.</span><span class="sxs-lookup"><span data-stu-id="6346b-444">d.</span></span> <span data-ttu-id="6346b-445">Olá **ignorar a contagem de linha** estiver definido demasiado**0**.</span><span class="sxs-lookup"><span data-stu-id="6346b-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="6346b-446">Se pretender que alguns toobe de linhas ignorado, Olá parte superior do ficheiro de Olá, introduza o número de Olá aqui.</span><span class="sxs-lookup"><span data-stu-id="6346b-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="6346b-447">e.</span><span class="sxs-lookup"><span data-stu-id="6346b-447">e.</span></span>  <span data-ttu-id="6346b-448">Olá **primeira linha de dados contém nomes de colunas** não está definido.</span><span class="sxs-lookup"><span data-stu-id="6346b-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="6346b-449">Se os ficheiros de origem Olá contém nomes de colunas na primeira linha de Olá, selecione esta opção.</span><span class="sxs-lookup"><span data-stu-id="6346b-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="6346b-450">f.</span><span class="sxs-lookup"><span data-stu-id="6346b-450">f.</span></span> <span data-ttu-id="6346b-451">Olá **tratar o valor de coluna vazia como null** opção estiver definida.</span><span class="sxs-lookup"><span data-stu-id="6346b-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="6346b-452">Expanda **definições avançadas** toosee avançadas opção disponível.</span><span class="sxs-lookup"><span data-stu-id="6346b-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="6346b-453">Em Olá parte inferior da página Olá, consulte Olá **pré-visualização** dos dados a partir do ficheiro de emp.txt Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="6346b-454">Clique em **esquema** separador no esquema do Olá inferior toosee Olá nesse assistente de cópia de Olá inferido observando dados Olá no ficheiro de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="6346b-455">Clique em **seguinte** depois de analisar os delimitadores Olá e pré-visualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="6346b-456">![Ferramenta copiar – definições do formato de ficheiro](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="6346b-457">No Olá **página do arquivo de dados de destino**, selecione **Blob Storage do Azure**e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6346b-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="6346b-458">Olá Blob Storage do Azure está a utilizar como ambos os arquivos de dados de Olá origem e de destino, esta explicação passo a passo.</span><span class="sxs-lookup"><span data-stu-id="6346b-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="6346b-459">![Ferramenta copiar – arquivo de dados de destino selecione](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="6346b-460">No **especificar conta de armazenamento de Blobs do Azure Olá** página:</span><span class="sxs-lookup"><span data-stu-id="6346b-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="6346b-461">Introduza **AzureStorageLinkedService** para Olá **nome da ligação** campo.</span><span class="sxs-lookup"><span data-stu-id="6346b-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="6346b-462">Confirme que a opção **A partir de subscrições do Azure** está selecionada para o **Método de seleção de contas**.</span><span class="sxs-lookup"><span data-stu-id="6346b-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="6346b-463">Selecione a sua **subscrição** do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="6346b-464">Selecione a sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="6346b-465">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6346b-465">Click **Next**.</span></span>     
10. <span data-ttu-id="6346b-466">No Olá **Olá de escolha de saída do ficheiro ou pasta** página:</span><span class="sxs-lookup"><span data-stu-id="6346b-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="6346b-467">Especifique **caminho da pasta** como **adfblobconnector/saída / {year} / {month} / {day}**.</span><span class="sxs-lookup"><span data-stu-id="6346b-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="6346b-468">Introduza **SEPARADOR**.</span><span class="sxs-lookup"><span data-stu-id="6346b-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="6346b-469">Para Olá **ano**, selecione **aaaa**.</span><span class="sxs-lookup"><span data-stu-id="6346b-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="6346b-470">Para Olá **mês**, confirme que está definido demasiado**MM**.</span><span class="sxs-lookup"><span data-stu-id="6346b-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="6346b-471">Para Olá **dia**, confirme que está definido demasiado**dd**.</span><span class="sxs-lookup"><span data-stu-id="6346b-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="6346b-472">Confirme que Olá **tipo de compressão** estiver definido demasiado**nenhum**.</span><span class="sxs-lookup"><span data-stu-id="6346b-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="6346b-473">Confirme que Olá **copiar comportamento** estiver definido demasiado**intercalar ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="6346b-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="6346b-474">Se o ficheiro com Olá já existe mesmo nome de saída Olá, hello novo conteúdo é adicionado toohello mesmo ficheiro no fim de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="6346b-475">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6346b-475">Click **Next**.</span></span>
    <span data-ttu-id="6346b-476">![Ferramenta copiar – escolha a pasta ou ficheiro de saída](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="6346b-477">No Olá **definições do formato de ficheiro** , reveja as definições de Olá e, em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6346b-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="6346b-478">Uma das opções adicionais Olá aqui é tooadd um ficheiro de saída de toohello do cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="6346b-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="6346b-479">Se selecionar esta opção, uma linha de cabeçalho é adicionada com nomes de colunas de Olá do esquema de Olá da origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="6346b-480">Pode mudar o nome de Olá nomes predefinidos das colunas ao visualizar o esquema de Olá para a origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="6346b-481">Por exemplo, pode alterar Olá primeira coluna tooFirst nome e a segunda coluna tooLast nome.</span><span class="sxs-lookup"><span data-stu-id="6346b-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="6346b-482">Em seguida, o ficheiro de saída Olá é gerado com um cabeçalho com estes nomes como nomes de colunas.</span><span class="sxs-lookup"><span data-stu-id="6346b-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="6346b-483">![Ferramenta copiar – definições do formato de ficheiro de destino](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="6346b-484">No Olá **definições de desempenho** página, confirme que **nuvem unidades** e **paralela cópias** estão definidas demasiado**automática**e clique em seguinte.</span><span class="sxs-lookup"><span data-stu-id="6346b-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="6346b-485">Para obter detalhes sobre estas definições, consulte [copiar guia Otimização e de desempenho de atividade](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="6346b-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="6346b-486">![Ferramenta copiar – definições de desempenho](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="6346b-487">No Olá **resumo** página, reveja as definições de todos os (propriedades da tarefa, as definições de origem e de destino e as definições de cópia) e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6346b-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="6346b-488">![Ferramenta copiar – página de resumo](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="6346b-489">Reveja as informações na Olá **resumo** página e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="6346b-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="6346b-490">Assistente de Olá cria dois serviços ligados, dois conjuntos de dados (entrada e saída) e um pipeline na fábrica de dados de Olá (a partir de onde foi iniciado Olá Assistente para copiar).</span><span class="sxs-lookup"><span data-stu-id="6346b-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="6346b-491">![Ferramenta copiar – página de implementação](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="6346b-492">Monitorizar o pipeline Olá (tarefa de cópia)</span><span class="sxs-lookup"><span data-stu-id="6346b-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="6346b-493">Clique em ligação Olá `Click here toomonitor copy pipeline` no Olá **implementação** página.</span><span class="sxs-lookup"><span data-stu-id="6346b-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="6346b-494">Deverá ver Olá **monitorizar e gerir aplicações** num separador separado.  ![Monitorizar e gerir aplicações](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="6346b-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="6346b-495">Olá alteração **iniciar** tempo na parte superior do Olá demasiado`04/19/2017` e **final** demasiado tempo`04/27/2017`e, em seguida, clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="6346b-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="6346b-496">Deverá ver cinco janelas de atividade do Olá **ATIVIDADE WINDOWS** lista.</span><span class="sxs-lookup"><span data-stu-id="6346b-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="6346b-497">Olá **WindowStart** vezes devem abranger todos os dias da hora de fim do pipeline início toopipeline.</span><span class="sxs-lookup"><span data-stu-id="6346b-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="6346b-498">Clique em **atualizar** botão para Olá **ATIVIDADE WINDOWS** lista algumas horas até ver estado Olá de todas as janelas de atividade de Olá está definida tooReady.</span><span class="sxs-lookup"><span data-stu-id="6346b-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="6346b-499">Agora, certifique-se de que os ficheiros de saída Olá são gerados na pasta de saída de Olá do contentor de adfblobconnector.</span><span class="sxs-lookup"><span data-stu-id="6346b-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="6346b-500">Deverá ver Olá seguir a estrutura de pastas na pasta de saída Olá:</span><span class="sxs-lookup"><span data-stu-id="6346b-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="6346b-501">Para obter informações detalhadas sobre como monitorizar e gerir as fábricas de dados, consulte [monitorizar e gerir o pipeline do Data Factory](data-factory-monitor-manage-app.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6346b-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="6346b-502">Entidades da fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="6346b-502">Data Factory entities</span></span>
<span data-ttu-id="6346b-503">Agora, mude o separador de back-toohello com Olá home page da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="6346b-504">Tenha em atenção que existem dois serviços ligados, dois conjuntos de dados e um pipeline na fábrica de dados agora.</span><span class="sxs-lookup"><span data-stu-id="6346b-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Página inicial de fábrica de dados com entidades](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="6346b-506">Clique em **autor e implementar** toolaunch Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6346b-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Editor do Data Factory](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="6346b-508">Deverá ver Olá seguintes entidades do Data Factory na fábrica de dados:</span><span class="sxs-lookup"><span data-stu-id="6346b-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="6346b-509">Dois serviços ligados.</span><span class="sxs-lookup"><span data-stu-id="6346b-509">Two linked services.</span></span> <span data-ttu-id="6346b-510">Uma para a origem de Olá e Olá outro para o destino de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="6346b-511">Ambos os serviços de Olá ligado Consulte toohello mesma conta de armazenamento do Azure esta explicação passo a passo.</span><span class="sxs-lookup"><span data-stu-id="6346b-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="6346b-512">Dois conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-512">Two datasets.</span></span> <span data-ttu-id="6346b-513">Um conjunto de dados de entrada e um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="6346b-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="6346b-514">Nestas instruções, ambos utilizam Olá mesmo contentor de blob mas Consulte toodifferent pastas (entrada e saída).</span><span class="sxs-lookup"><span data-stu-id="6346b-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="6346b-515">Um pipeline.</span><span class="sxs-lookup"><span data-stu-id="6346b-515">A pipeline.</span></span> <span data-ttu-id="6346b-516">pipeline de Olá contém uma atividade de cópia que utiliza uma origem de blob e um blob sink toocopy de dados de um tooanother de localização de blob do Azure a localização de blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="6346b-517">Olá secções seguintes fornecem mais informações sobre estas entidades.</span><span class="sxs-lookup"><span data-stu-id="6346b-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="6346b-518">Serviços ligados</span><span class="sxs-lookup"><span data-stu-id="6346b-518">Linked services</span></span>
<span data-ttu-id="6346b-519">Deverá ver dois serviços ligados.</span><span class="sxs-lookup"><span data-stu-id="6346b-519">You should see two linked services.</span></span> <span data-ttu-id="6346b-520">Uma para a origem de Olá e Olá outro para o destino de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="6346b-521">Esta explicação passo a passo, o aspeto ambas as definições Olá mesmo, exceto para os nomes de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="6346b-522">Olá **tipo** de Olá serviço ligado está definido demasiado**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="6346b-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="6346b-523">A propriedade mais importante da definição de serviço ligado de Olá está Olá **connectionString**, que é utilizado pelo Data Factory tooconnect tooyour conta de armazenamento do Azure no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="6346b-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="6346b-524">Ignore a propriedade de hubName Olá na definição de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="6346b-525">Serviço de ligado do armazenamento de BLOBs de origem</span><span class="sxs-lookup"><span data-stu-id="6346b-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="6346b-526">Serviço de ligado do armazenamento de BLOBs de destino</span><span class="sxs-lookup"><span data-stu-id="6346b-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="6346b-527">Para mais informações sobre o serviço ligado do Storage do Azure, consulte [ligado propriedades do serviço](#linked-service-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="6346b-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="6346b-528">Conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="6346b-528">Datasets</span></span>
<span data-ttu-id="6346b-529">Existem dois conjuntos de dados: um conjunto de dados de entrada e um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="6346b-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="6346b-530">tipo de Olá de Olá conjunto de dados está definido demasiado**AzureBlob** para ambos.</span><span class="sxs-lookup"><span data-stu-id="6346b-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="6346b-531">conjunto de dados de entrada Olá pontos toohello **entrada** pasta de Olá **adfblobconnector** contentor do blob.</span><span class="sxs-lookup"><span data-stu-id="6346b-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="6346b-532">Olá **externo** for definida demasiado**verdadeiro** deste conjunto de dados como Olá dados não é produzidos pelo pipeline Olá com atividade de cópia de Olá que demora este conjunto de dados como entrada.</span><span class="sxs-lookup"><span data-stu-id="6346b-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="6346b-533">Olá toohello de pontos de conjunto de dados de saída **saída** pasta de Olá mesmo contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="6346b-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="6346b-534">Olá conjunto de dados de saída também utiliza Olá ano, mês e dia Olá **SliceStart** toodynamically variável sistema avaliar caminho Olá para o ficheiro de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="6346b-535">Para obter uma lista de funções e variáveis do sistema suportadas pela fábrica de dados, consulte [funções de Data Factory e variáveis do sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="6346b-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="6346b-536">Olá **externo** for definida demasiado**falso** (valor predefinido) porque este conjunto de dados é produzido pelo pipeline Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="6346b-537">Para obter mais informações sobre as propriedades suportadas pelo conjunto de dados de Blobs do Azure, consulte [propriedades do Dataset](#dataset-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="6346b-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="6346b-538">Conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="6346b-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="6346b-539">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="6346b-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="6346b-540">Pipeline</span><span class="sxs-lookup"><span data-stu-id="6346b-540">Pipeline</span></span>
<span data-ttu-id="6346b-541">pipeline de Olá tem apenas uma atividade.</span><span class="sxs-lookup"><span data-stu-id="6346b-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="6346b-542">Olá **tipo** de Olá atividade está definida demasiado**cópia**.</span><span class="sxs-lookup"><span data-stu-id="6346b-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="6346b-543">Nas propriedades do tipo de Olá para a atividade de Olá, existem duas secções, um para a origem e Olá outro para sink.</span><span class="sxs-lookup"><span data-stu-id="6346b-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="6346b-544">tipo de origem Olá estiver definido demasiado**BlobSource** como atividade Olá copia dados do armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="6346b-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="6346b-545">Olá o tipo de sink estiver definido demasiado**BlobSink** como atividade Olá copiar o blob storage tooa dados.</span><span class="sxs-lookup"><span data-stu-id="6346b-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="6346b-546">atividade de cópia de Olá aceita InputDataset z4y como comentários de Olá e OutputDataset-z4y como saída Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="6346b-547">Para obter mais informações sobre propriedades suportadas por BlobSource e BlobSink, consulte [copiar propriedades da atividade](#copy-activity-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="6346b-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="6346b-548">Exemplos JSON para copiar dados tooand do armazenamento de BLOBs</span><span class="sxs-lookup"><span data-stu-id="6346b-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="6346b-549">Olá exemplos seguintes fornecem definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6346b-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6346b-550">Estes mostram como toocopy tooand de dados do Blob Storage do Azure e SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="6346b-551">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das origens tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6346b-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="6346b-552">Exemplo JSON: Copiar dados de armazenamento de BLOBs tooSQL da base de dados</span><span class="sxs-lookup"><span data-stu-id="6346b-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="6346b-553">Olá seguinte exemplo mostra:</span><span class="sxs-lookup"><span data-stu-id="6346b-553">hello following sample shows:</span></span>

1. <span data-ttu-id="6346b-554">Um serviço ligado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6346b-555">Um serviço ligado do tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="6346b-556">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="6346b-557">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6346b-558">A [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que utiliza [BlobSource](#copy-activity-properties) e [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6346b-559">exemplo de Olá copia dados de séries de tempo de uma tabela de SQL do Azure do blob do Azure tooan hora a hora.</span><span class="sxs-lookup"><span data-stu-id="6346b-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="6346b-560">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6346b-561">**Serviço ligado SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6346b-561">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="6346b-562">**Serviço ligado do Storage do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6346b-562">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="6346b-563">O Azure Data Factory suportam dois tipos de serviços de armazenamento do Azure ligado: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="6346b-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="6346b-564">Para Olá primeiro, especifique a cadeia de ligação de Olá que incluem a chave de conta Olá e para Olá posteriormente, um, especificar Olá Uri de assinatura de acesso partilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="6346b-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="6346b-565">Consulte [serviços ligados](#linked-service-properties) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="6346b-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="6346b-566">**Conjunto de dados de entrada Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6346b-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="6346b-567">Dados são captados um blob de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="6346b-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6346b-568">Olá pasta caminho e nome de ficheiro para o blob Olá dinamicamente são avaliados com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="6346b-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6346b-569">caminho da pasta Olá utiliza ano, mês e parte de dia da hora de início de Olá e nome de ficheiro utiliza a parte de hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="6346b-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="6346b-570">"external": "true" definição informa fábrica de dados nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="6346b-571">**Conjunto de dados de saída do SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6346b-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="6346b-572">exemplo de Olá copia a tabela de tooa de dados com o nome "MyTable" numa base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="6346b-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="6346b-573">Criar tabela Olá na base de dados SQL do Azure com Olá o mesmo número de colunas como esperado Olá Blob CSV ficheiro toocontain.</span><span class="sxs-lookup"><span data-stu-id="6346b-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="6346b-574">Novas linhas são adicionadas toohello tabela cada hora.</span><span class="sxs-lookup"><span data-stu-id="6346b-574">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="6346b-575">**Uma atividade de cópia num pipeline com a origem de Blob e o sink do SQL Server:**</span><span class="sxs-lookup"><span data-stu-id="6346b-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="6346b-576">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora.</span><span class="sxs-lookup"><span data-stu-id="6346b-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6346b-577">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**BlobSource** e **sink** tipo está definido demasiado**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="6346b-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="6346b-578">Exemplo JSON: Copiar dados de SQL do Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="6346b-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="6346b-579">Olá seguinte exemplo mostra:</span><span class="sxs-lookup"><span data-stu-id="6346b-579">hello following sample shows:</span></span>

1. <span data-ttu-id="6346b-580">Um serviço ligado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6346b-581">Um serviço ligado do tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="6346b-582">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6346b-583">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="6346b-584">A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) e [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6346b-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="6346b-585">exemplo de Olá copia dados de séries de tempo de um tooan de tabela SQL do Azure blob do Azure numa base horária.</span><span class="sxs-lookup"><span data-stu-id="6346b-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="6346b-586">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6346b-587">**Serviço ligado SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6346b-587">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="6346b-588">**Serviço ligado do Storage do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6346b-588">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="6346b-589">O Azure Data Factory suportam dois tipos de serviços de armazenamento do Azure ligado: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="6346b-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="6346b-590">Para Olá primeiro, especifique a cadeia de ligação de Olá que incluem a chave de conta Olá e para Olá posteriormente, um, especificar Olá Uri de assinatura de acesso partilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="6346b-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="6346b-591">Consulte [serviços ligados](#linked-service-properties) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="6346b-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="6346b-592">**Conjunto de dados de entrada SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6346b-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="6346b-593">exemplo de Olá pressupõe que criou uma tabela "MyTable" SQL do Azure e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="6346b-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="6346b-594">A definição "external": "true" informa serviço Data Factory nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="6346b-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="6346b-595">**Conjunto de dados de saída do Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6346b-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6346b-596">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="6346b-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6346b-597">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="6346b-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6346b-598">caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="6346b-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="6346b-599">**Uma atividade de cópia num pipeline com a origem SQL e o sink de Blob:**</span><span class="sxs-lookup"><span data-stu-id="6346b-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="6346b-600">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora.</span><span class="sxs-lookup"><span data-stu-id="6346b-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6346b-601">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**SqlSource** e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6346b-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="6346b-602">consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá passado toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="6346b-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

> [!NOTE]
> <span data-ttu-id="6346b-603">colunas de toomap toocolumns de conjunto de dados de origem do conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6346b-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6346b-604">Desempenho e a otimização</span><span class="sxs-lookup"><span data-stu-id="6346b-604">Performance and Tuning</span></span>
<span data-ttu-id="6346b-605">Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.</span><span class="sxs-lookup"><span data-stu-id="6346b-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
