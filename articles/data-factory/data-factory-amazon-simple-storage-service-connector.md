---
title: "dados aaaMove do serviço de armazenamento simples Amazon utilizando o Data Factory | Microsoft Docs"
description: "Saiba mais sobre como dados toomove a partir do serviço de armazenamento simples (S3) do Amazon através da utilização do Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="82f15-103">Mover dados do serviço de armazenamento simples Amazon através da utilização do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="82f15-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="82f15-104">Este artigo explica como toouse Olá atividade de cópia de dados do Azure Data Factory toomove do serviço de armazenamento simples (S3) do Amazon.</span><span class="sxs-lookup"><span data-stu-id="82f15-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="82f15-105">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="82f15-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="82f15-106">Pode copiar dados do arquivo de dados do Amazon S3 tooany suportado sink.</span><span class="sxs-lookup"><span data-stu-id="82f15-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="82f15-107">Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="82f15-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="82f15-108">Fábrica de dados atualmente suporta apenas dados mover de arquivos de dados do Amazon S3 tooother, mas não mover dados de outros dados armazena tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="82f15-109">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="82f15-109">Required permissions</span></span>
<span data-ttu-id="82f15-110">toocopy dados do Amazon S3, certifique-se de que lhe foram concedidas Olá as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="82f15-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="82f15-111">`s3:GetObject`e `s3:GetObjectVersion` para operações de objeto do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="82f15-112">`s3:ListBucket`para operações de registo do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="82f15-113">Se estiver a utilizar o Assistente de cópia do Data Factory, de Olá `s3:ListAllMyBuckets` também é necessário.</span><span class="sxs-lookup"><span data-stu-id="82f15-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="82f15-114">Para obter detalhes sobre a lista completa de Olá Amazon S3 permissões, consulte [especificar permissões numa política](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="82f15-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="82f15-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="82f15-115">Getting started</span></span>
<span data-ttu-id="82f15-116">Pode criar um pipeline com uma atividade de cópia move dados a partir de uma origem de Amazon S3, utilizando ferramentas diferentes ou APIs.</span><span class="sxs-lookup"><span data-stu-id="82f15-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="82f15-117">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="82f15-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="82f15-118">Para instruções rápidas, consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="82f15-119">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="82f15-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="82f15-120">Para instruções passo a passo toocreate um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="82f15-121">Se utilizar ferramentas ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="82f15-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="82f15-122">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="82f15-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="82f15-123">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="82f15-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="82f15-124">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="82f15-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="82f15-125">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="82f15-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="82f15-126">Quando utilizar APIs (exceto .NET API) ou ferramentas, é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="82f15-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="82f15-127">Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de um arquivo de dados do Amazon S3, consulte Olá [exemplo JSON: copiar dados do Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="82f15-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="82f15-128">Para obter detalhes sobre os formatos de ficheiro e compressão suportados para uma atividade de cópia, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="82f15-129">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="82f15-130">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="82f15-130">Linked service properties</span></span>
<span data-ttu-id="82f15-131">Um serviço ligado liga uma fábrica de dados de tooa de arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="82f15-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="82f15-132">Criar um serviço ligado do tipo **AwsAccessKey** toolink tooyour fábrica de dados de arquivo de dados do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="82f15-133">Olá, a tabela seguinte fornece um serviço descrição JSON elementos específico tooAmazon S3 (AwsAccessKey) ligado.</span><span class="sxs-lookup"><span data-stu-id="82f15-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="82f15-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="82f15-134">Property</span></span> | <span data-ttu-id="82f15-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="82f15-135">Description</span></span> | <span data-ttu-id="82f15-136">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="82f15-136">Allowed values</span></span> | <span data-ttu-id="82f15-137">Necessário</span><span class="sxs-lookup"><span data-stu-id="82f15-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82f15-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="82f15-138">accessKeyID</span></span> |<span data-ttu-id="82f15-139">ID da chave de acesso secreta Olá.</span><span class="sxs-lookup"><span data-stu-id="82f15-139">ID of hello secret access key.</span></span> |<span data-ttu-id="82f15-140">Cadeia</span><span class="sxs-lookup"><span data-stu-id="82f15-140">string</span></span> |<span data-ttu-id="82f15-141">Sim</span><span class="sxs-lookup"><span data-stu-id="82f15-141">Yes</span></span> |
| <span data-ttu-id="82f15-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="82f15-142">secretAccessKey</span></span> |<span data-ttu-id="82f15-143">chave de acesso secreta Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="82f15-143">hello secret access key itself.</span></span> |<span data-ttu-id="82f15-144">Cadeia secreta encriptada</span><span class="sxs-lookup"><span data-stu-id="82f15-144">Encrypted secret string</span></span> |<span data-ttu-id="82f15-145">Sim</span><span class="sxs-lookup"><span data-stu-id="82f15-145">Yes</span></span> |

<span data-ttu-id="82f15-146">Segue-se um exemplo:</span><span class="sxs-lookup"><span data-stu-id="82f15-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="82f15-147">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="82f15-147">Dataset properties</span></span>
<span data-ttu-id="82f15-148">toospecify toorepresent um conjunto de dados de entrada os dados no Blob storage do Azure, defina a propriedade de tipo de Olá de conjunto de dados de Olá demasiado**AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="82f15-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="82f15-149">Conjunto Olá **linkedServiceName** propriedade do Olá dataset toohello nome Olá Amazon S3 serviço ligado.</span><span class="sxs-lookup"><span data-stu-id="82f15-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="82f15-150">Para uma lista completa das secções e propriedades disponíveis para definir os conjuntos de dados, consulte [criar conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="82f15-151">As secções, tais como a estrutura, a disponibilidade e a política são semelhantes para todos os tipos de conjunto de dados (por exemplo, SQL database, blob do Azure e tabela do Azure).</span><span class="sxs-lookup"><span data-stu-id="82f15-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="82f15-152">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="82f15-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="82f15-153">Olá **typeProperties** secção para um conjunto de dados do tipo **AmazonS3** (que inclui o conjunto de dados de Olá Amazon S3) tem Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="82f15-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="82f15-154">Propriedade</span><span class="sxs-lookup"><span data-stu-id="82f15-154">Property</span></span> | <span data-ttu-id="82f15-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="82f15-155">Description</span></span> | <span data-ttu-id="82f15-156">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="82f15-156">Allowed values</span></span> | <span data-ttu-id="82f15-157">Necessário</span><span class="sxs-lookup"><span data-stu-id="82f15-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82f15-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="82f15-158">bucketName</span></span> |<span data-ttu-id="82f15-159">nome do registo de Olá S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-159">hello S3 bucket name.</span></span> |<span data-ttu-id="82f15-160">Cadeia</span><span class="sxs-lookup"><span data-stu-id="82f15-160">String</span></span> |<span data-ttu-id="82f15-161">Sim</span><span class="sxs-lookup"><span data-stu-id="82f15-161">Yes</span></span> |
| <span data-ttu-id="82f15-162">key</span><span class="sxs-lookup"><span data-stu-id="82f15-162">key</span></span> |<span data-ttu-id="82f15-163">chave do objeto de Olá S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-163">hello S3 object key.</span></span> |<span data-ttu-id="82f15-164">Cadeia</span><span class="sxs-lookup"><span data-stu-id="82f15-164">String</span></span> |<span data-ttu-id="82f15-165">Não</span><span class="sxs-lookup"><span data-stu-id="82f15-165">No</span></span> |
| <span data-ttu-id="82f15-166">prefixo</span><span class="sxs-lookup"><span data-stu-id="82f15-166">prefix</span></span> |<span data-ttu-id="82f15-167">Prefixo para a chave de objeto Olá S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="82f15-168">Objetos cujas chaves começar a utilizar este prefixo estão selecionados.</span><span class="sxs-lookup"><span data-stu-id="82f15-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="82f15-169">Aplica-se apenas quando o chave está vazia.</span><span class="sxs-lookup"><span data-stu-id="82f15-169">Applies only when key is empty.</span></span> |<span data-ttu-id="82f15-170">Cadeia</span><span class="sxs-lookup"><span data-stu-id="82f15-170">String</span></span> |<span data-ttu-id="82f15-171">Não</span><span class="sxs-lookup"><span data-stu-id="82f15-171">No</span></span> |
| <span data-ttu-id="82f15-172">Versão</span><span class="sxs-lookup"><span data-stu-id="82f15-172">version</span></span> |<span data-ttu-id="82f15-173">versão de Olá do objeto de Olá S3, se o controlo de versões de S3 estiver ativado.</span><span class="sxs-lookup"><span data-stu-id="82f15-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="82f15-174">Cadeia</span><span class="sxs-lookup"><span data-stu-id="82f15-174">String</span></span> |<span data-ttu-id="82f15-175">Não</span><span class="sxs-lookup"><span data-stu-id="82f15-175">No</span></span> |
| <span data-ttu-id="82f15-176">formato</span><span class="sxs-lookup"><span data-stu-id="82f15-176">format</span></span> | <span data-ttu-id="82f15-177">é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="82f15-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="82f15-178">Conjunto Olá **tipo** propriedade em formato tooone destes valores.</span><span class="sxs-lookup"><span data-stu-id="82f15-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="82f15-179">Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc formato](data-factory-supported-file-and-compression-formats.md#orc-format), e [formato Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) secções.</span><span class="sxs-lookup"><span data-stu-id="82f15-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="82f15-180">Se pretender que os ficheiros de toocopy como-entre baseados em ficheiros arquivos de (cópia binário), ignorar Olá formato secção ambas as definições do conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="82f15-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="82f15-181">Não</span><span class="sxs-lookup"><span data-stu-id="82f15-181">No</span></span> | |
| <span data-ttu-id="82f15-182">Compressão</span><span class="sxs-lookup"><span data-stu-id="82f15-182">compression</span></span> | <span data-ttu-id="82f15-183">Especifique o tipo de Olá e nível de compressão de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="82f15-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="82f15-184">os tipos de Olá suportado são: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="82f15-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="82f15-185">níveis de Olá suportado são: **Optimal** e **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="82f15-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="82f15-186">Para obter mais informações, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="82f15-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="82f15-187">Não</span><span class="sxs-lookup"><span data-stu-id="82f15-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="82f15-188">**bucketName + chave** Especifica a localização de Olá do objeto de Olá S3, em que o registo é recipiente-raiz Olá para objetos de S3, e chave é o objeto de toohello S3 Olá caminho completo.</span><span class="sxs-lookup"><span data-stu-id="82f15-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="82f15-189">Conjunto de dados de exemplo com prefixo</span><span class="sxs-lookup"><span data-stu-id="82f15-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="82f15-190">Conjunto de dados de exemplo (com a versão)</span><span class="sxs-lookup"><span data-stu-id="82f15-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="82f15-191">Caminhos de dinâmicos para S3</span><span class="sxs-lookup"><span data-stu-id="82f15-191">Dynamic paths for S3</span></span>
<span data-ttu-id="82f15-192">Olá anterior exemplo utiliza valores fixos para Olá **chave** e **bucketName** propriedades no conjunto de dados de Olá Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="82f15-193">Pode ter o Data Factory calcular estas propriedades dinamicamente em runtime, utilizando variáveis de sistema, tais como SliceStart.</span><span class="sxs-lookup"><span data-stu-id="82f15-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="82f15-194">Pode fazê-lo hello mesmo para Olá **prefixo** propriedade de um conjunto de dados do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="82f15-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="82f15-195">Para obter uma lista de funções suportadas e as variáveis, consulte [funções de Data Factory e variáveis do sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="82f15-196">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="82f15-196">Copy activity properties</span></span>
<span data-ttu-id="82f15-197">Para uma lista completa das secções e propriedades disponíveis para definir as atividades, consulte [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="82f15-198">Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="82f15-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="82f15-199">Propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="82f15-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="82f15-200">Para a atividade de cópia de Olá, propriedades variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="82f15-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="82f15-201">Quando uma origem de atividade de cópia de Olá é do tipo **FileSystemSource** (que inclui o Amazon S3), Olá seguinte propriedade está disponível no **typeProperties** secção:</span><span class="sxs-lookup"><span data-stu-id="82f15-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="82f15-202">Propriedade</span><span class="sxs-lookup"><span data-stu-id="82f15-202">Property</span></span> | <span data-ttu-id="82f15-203">Descrição</span><span class="sxs-lookup"><span data-stu-id="82f15-203">Description</span></span> | <span data-ttu-id="82f15-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="82f15-204">Allowed values</span></span> | <span data-ttu-id="82f15-205">Necessário</span><span class="sxs-lookup"><span data-stu-id="82f15-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82f15-206">Recursiva</span><span class="sxs-lookup"><span data-stu-id="82f15-206">recursive</span></span> |<span data-ttu-id="82f15-207">Especifica se a lista de toorecursively S3 objetos no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="82f15-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="82f15-208">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="82f15-208">true/false</span></span> |<span data-ttu-id="82f15-209">Não</span><span class="sxs-lookup"><span data-stu-id="82f15-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="82f15-210">Exemplo JSON: copiar dados do Amazon S3 tooAzure armazenamento de BLOBs</span><span class="sxs-lookup"><span data-stu-id="82f15-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="82f15-211">Este exemplo mostra como toocopy dados do Amazon S3 tooan Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="82f15-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="82f15-212">No entanto, dados podem ser copiados diretamente demasiado[qualquer um dos Olá sinks que são suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando a atividade de cópia de Olá na fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="82f15-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="82f15-213">exemplo de Olá fornece definições de JSON para Olá seguintes entidades do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="82f15-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="82f15-214">Pode utilizar estes toocreate definições dados de toocopy um pipeline do armazenamento de tooBlob Amazon S3, utilizando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="82f15-215">Um serviço ligado do tipo [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="82f15-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="82f15-216">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="82f15-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="82f15-217">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="82f15-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="82f15-218">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="82f15-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="82f15-219">A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="82f15-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="82f15-220">exemplo de Olá copia dados da Amazon S3 tooan BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="82f15-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="82f15-221">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="82f15-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="82f15-222">Serviço ligado do Amazon S3</span><span class="sxs-lookup"><span data-stu-id="82f15-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="82f15-223">Serviço ligado do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="82f15-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="82f15-224">Conjunto de dados de entrada Amazon S3</span><span class="sxs-lookup"><span data-stu-id="82f15-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="82f15-225">Definição **"external": true** informa o serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="82f15-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="82f15-226">Defina um conjunto de dados de entrada que não é produzido por uma atividade no pipeline de Olá tootrue esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="82f15-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="82f15-227">Conjunto de dados de saída do Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="82f15-227">Azure Blob output dataset</span></span>

<span data-ttu-id="82f15-228">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="82f15-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="82f15-229">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="82f15-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="82f15-230">caminho da pasta Olá utiliza as partes de ano, mês, dia e horas Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="82f15-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="82f15-231">Atividade de cópia de um pipeline com uma origem de Amazon S3 e um receptor de blob</span><span class="sxs-lookup"><span data-stu-id="82f15-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="82f15-232">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída, não sendo toorun agendada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="82f15-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="82f15-233">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**FileSystemSource**, e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="82f15-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="82f15-234">colunas de toomap um toocolumns de conjunto de dados de origem de um conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="82f15-235">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="82f15-235">Next steps</span></span>
<span data-ttu-id="82f15-236">Consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="82f15-236">See hello following articles:</span></span>

* <span data-ttu-id="82f15-237">toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Factory de dados e várias formas toooptimize-lo, consulte Olá [copiar guia Otimização e de desempenho de atividade](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="82f15-238">Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="82f15-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
