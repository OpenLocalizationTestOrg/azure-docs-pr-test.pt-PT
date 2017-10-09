---
title: "índice de tooSearch aaaPush dados utilizando o Data Factory | Microsoft Docs"
description: "Saiba mais sobre como toopush dados tooAzure índice de pesquisa através do Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="0af49-103">Push de índice de pesquisa do Azure tooan dados através da utilização do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0af49-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="0af49-104">Este artigo descreve como o índice de pesquisa de tooAzure de arquivo de dados de toopush do toouse Olá atividade de cópia de dados de origem suportada.</span><span class="sxs-lookup"><span data-stu-id="0af49-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="0af49-105">Arquivos de dados de origem suportada estão listados na coluna de origem de Olá de Olá [suportados origens e sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="0af49-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0af49-106">Este artigo baseia-se Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia e combinações de arquivo de dados suportada.</span><span class="sxs-lookup"><span data-stu-id="0af49-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="0af49-107">Ativar a conectividade</span><span class="sxs-lookup"><span data-stu-id="0af49-107">Enabling connectivity</span></span>
<span data-ttu-id="0af49-108">tooallow serviço Data Factory ligar o arquivo de dados no local tooan, instalar o Data Management Gateway no seu ambiente no local.</span><span class="sxs-lookup"><span data-stu-id="0af49-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="0af49-109">Pode instalar o gateway num Olá mesmo computador que aloja os dados de origem Olá armazenar ou em tooavoid um computador separado competir para recursos com dados Olá arquivo.</span><span class="sxs-lookup"><span data-stu-id="0af49-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="0af49-110">Gateway de gestão de dados liga-se os serviços de toocloud de origens de dados no local de forma segura e gerida.</span><span class="sxs-lookup"><span data-stu-id="0af49-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="0af49-111">Consulte [mover dados entre no local e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter detalhes sobre o Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="0af49-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0af49-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="0af49-112">Getting started</span></span>
<span data-ttu-id="0af49-113">Pode criar um pipeline com uma atividade de cópia que envia dados a partir de um índice de pesquisa de tooAzure de arquivo de dados de origem utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="0af49-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="0af49-114">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="0af49-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="0af49-115">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="0af49-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="0af49-116">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="0af49-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0af49-117">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0af49-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0af49-118">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="0af49-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="0af49-119">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="0af49-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="0af49-120">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="0af49-121">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="0af49-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0af49-122">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="0af49-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="0af49-123">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="0af49-124">Para um exemplo com definições de JSON para entidades do Data Factory do índice de pesquisa utilizados toocopy dados tooAzure, consulte [exemplo JSON: copiar dados de índice de pesquisa no local do SQL Server tooAzure](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="0af49-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="0af49-125">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooAzure índice de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="0af49-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0af49-126">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="0af49-126">Linked service properties</span></span>

<span data-ttu-id="0af49-127">Olá, a tabela seguinte fornece descrições para os elementos JSON que são o serviço de pesquisa do Azure ligado toohello específico.</span><span class="sxs-lookup"><span data-stu-id="0af49-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="0af49-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0af49-128">Property</span></span> | <span data-ttu-id="0af49-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="0af49-129">Description</span></span> | <span data-ttu-id="0af49-130">Necessário</span><span class="sxs-lookup"><span data-stu-id="0af49-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="0af49-131">tipo</span><span class="sxs-lookup"><span data-stu-id="0af49-131">type</span></span> | <span data-ttu-id="0af49-132">a propriedade de tipo Olá tem de ser definida: **azuresearch, uma vez**.</span><span class="sxs-lookup"><span data-stu-id="0af49-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="0af49-133">Sim</span><span class="sxs-lookup"><span data-stu-id="0af49-133">Yes</span></span> |
| <span data-ttu-id="0af49-134">URL</span><span class="sxs-lookup"><span data-stu-id="0af49-134">url</span></span> | <span data-ttu-id="0af49-135">URL para Olá serviço da Azure Search.</span><span class="sxs-lookup"><span data-stu-id="0af49-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="0af49-136">Sim</span><span class="sxs-lookup"><span data-stu-id="0af49-136">Yes</span></span> |
| <span data-ttu-id="0af49-137">key</span><span class="sxs-lookup"><span data-stu-id="0af49-137">key</span></span> | <span data-ttu-id="0af49-138">Chave de administrador para Olá serviço da Azure Search.</span><span class="sxs-lookup"><span data-stu-id="0af49-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="0af49-139">Sim</span><span class="sxs-lookup"><span data-stu-id="0af49-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="0af49-140">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="0af49-140">Dataset properties</span></span>

<span data-ttu-id="0af49-141">Para uma lista completa das secções e as propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0af49-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0af49-142">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="0af49-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="0af49-143">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="0af49-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="0af49-144">secção Olá typeProperties para um conjunto de dados do tipo de Olá **AzureSearchIndex** tem Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="0af49-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="0af49-145">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0af49-145">Property</span></span> | <span data-ttu-id="0af49-146">Descrição</span><span class="sxs-lookup"><span data-stu-id="0af49-146">Description</span></span> | <span data-ttu-id="0af49-147">Necessário</span><span class="sxs-lookup"><span data-stu-id="0af49-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="0af49-148">tipo</span><span class="sxs-lookup"><span data-stu-id="0af49-148">type</span></span> | <span data-ttu-id="0af49-149">a propriedade de tipo Olá tem de ser definida demasiado**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="0af49-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="0af49-150">Sim</span><span class="sxs-lookup"><span data-stu-id="0af49-150">Yes</span></span> |
| <span data-ttu-id="0af49-151">indexName</span><span class="sxs-lookup"><span data-stu-id="0af49-151">indexName</span></span> | <span data-ttu-id="0af49-152">Nome do índice de pesquisa do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="0af49-153">Fábrica de dados não criar o índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="0af49-154">índice de Olá tem de existir na Azure Search.</span><span class="sxs-lookup"><span data-stu-id="0af49-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="0af49-155">Sim</span><span class="sxs-lookup"><span data-stu-id="0af49-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="0af49-156">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0af49-156">Copy activity properties</span></span>
<span data-ttu-id="0af49-157">Para uma lista completa das secções e as propriedades disponíveis para definir as atividades, consulte Olá [Criar pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0af49-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0af49-158">Propriedades, tais como o nome, descrição, entrada e tabelas de saída e várias políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="0af49-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="0af49-159">Enquanto, propriedades disponíveis na secção de typeProperties Olá variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="0af49-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="0af49-160">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="0af49-161">Para a atividade de cópia, quando o sink de Olá é do tipo de Olá **AzureSearchIndexSink**, na secção typeProperties, estão disponível Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="0af49-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="0af49-162">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0af49-162">Property</span></span> | <span data-ttu-id="0af49-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="0af49-163">Description</span></span> | <span data-ttu-id="0af49-164">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0af49-164">Allowed values</span></span> | <span data-ttu-id="0af49-165">Necessário</span><span class="sxs-lookup"><span data-stu-id="0af49-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="0af49-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="0af49-166">WriteBehavior</span></span> | <span data-ttu-id="0af49-167">Especifica se toomerge ou substituir quando um documento já existe no índice Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="0af49-168">Consulte Olá [WriteBehavior propriedade](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="0af49-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="0af49-169">Intercalar (predefinição)</span><span class="sxs-lookup"><span data-stu-id="0af49-169">Merge (default)</span></span><br/><span data-ttu-id="0af49-170">Carregar</span><span class="sxs-lookup"><span data-stu-id="0af49-170">Upload</span></span>| <span data-ttu-id="0af49-171">Não</span><span class="sxs-lookup"><span data-stu-id="0af49-171">No</span></span> |
| <span data-ttu-id="0af49-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="0af49-172">WriteBatchSize</span></span> | <span data-ttu-id="0af49-173">Carrega dados para o índice de pesquisa do Azure Olá quando o tamanho de memória intermédia de Olá atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="0af49-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="0af49-174">Consulte Olá [WriteBatchSize propriedade](#writebatchsize-property) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="0af49-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="0af49-175">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="0af49-175">1 too1,000.</span></span> <span data-ttu-id="0af49-176">Valor predefinido é 1000.</span><span class="sxs-lookup"><span data-stu-id="0af49-176">Default value is 1000.</span></span> | <span data-ttu-id="0af49-177">Não</span><span class="sxs-lookup"><span data-stu-id="0af49-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="0af49-178">Propriedade de WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="0af49-178">WriteBehavior property</span></span>
<span data-ttu-id="0af49-179">AzureSearchSink upserts ao escrever dados.</span><span class="sxs-lookup"><span data-stu-id="0af49-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="0af49-180">Por outras palavras, ao escrever um documento, se a chave do documento Olá já existe no índice de pesquisa do Azure Olá, Azure Search atualizações documento existente Olá, em vez de gerar uma exceção de conflito.</span><span class="sxs-lookup"><span data-stu-id="0af49-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="0af49-181">Olá AzureSearchSink fornece Olá seguir dois upsert comportamentos (utilizando o SDK azuresearch, uma vez):</span><span class="sxs-lookup"><span data-stu-id="0af49-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="0af49-182">**Intercalar**: combinar todas as colunas de Olá documento novo Olá com Olá um existente.</span><span class="sxs-lookup"><span data-stu-id="0af49-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="0af49-183">Para colunas com um valor nulo no documento novo Olá, valor Olá Olá existente um é preservada.</span><span class="sxs-lookup"><span data-stu-id="0af49-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="0af49-184">**Carregar**: substitui o documento novo Olá Olá já existente.</span><span class="sxs-lookup"><span data-stu-id="0af49-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="0af49-185">Para colunas não especificadas no documento novo Olá, o valor de Olá é definido toonull se houver um valor não nulo documento existente Olá, ou não.</span><span class="sxs-lookup"><span data-stu-id="0af49-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="0af49-186">comportamento predefinido de Olá é **intercalar**.</span><span class="sxs-lookup"><span data-stu-id="0af49-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="0af49-187">Propriedade de WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="0af49-187">WriteBatchSize Property</span></span>
<span data-ttu-id="0af49-188">Serviço de pesquisa do Azure suporta documentos de escrita como um lote.</span><span class="sxs-lookup"><span data-stu-id="0af49-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="0af49-189">Um lote pode conter 1 too1, 000 ações.</span><span class="sxs-lookup"><span data-stu-id="0af49-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="0af49-190">Uma ação processa uma operação de intercalação/carregamento do documento tooperform Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="0af49-191">Suporte de tipo de dados</span><span class="sxs-lookup"><span data-stu-id="0af49-191">Data type support</span></span>
<span data-ttu-id="0af49-192">Olá seguinte tabela especifica se um tipo de dados de pesquisa do Azure é suportado ou não.</span><span class="sxs-lookup"><span data-stu-id="0af49-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="0af49-193">Tipo de dados de pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="0af49-193">Azure Search data type</span></span> | <span data-ttu-id="0af49-194">Suportado no receptor de pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="0af49-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="0af49-195">Cadeia</span><span class="sxs-lookup"><span data-stu-id="0af49-195">String</span></span> | <span data-ttu-id="0af49-196">S</span><span class="sxs-lookup"><span data-stu-id="0af49-196">Y</span></span> |
| <span data-ttu-id="0af49-197">Int32</span><span class="sxs-lookup"><span data-stu-id="0af49-197">Int32</span></span> | <span data-ttu-id="0af49-198">S</span><span class="sxs-lookup"><span data-stu-id="0af49-198">Y</span></span> |
| <span data-ttu-id="0af49-199">Int64</span><span class="sxs-lookup"><span data-stu-id="0af49-199">Int64</span></span> | <span data-ttu-id="0af49-200">S</span><span class="sxs-lookup"><span data-stu-id="0af49-200">Y</span></span> |
| <span data-ttu-id="0af49-201">duplo</span><span class="sxs-lookup"><span data-stu-id="0af49-201">Double</span></span> | <span data-ttu-id="0af49-202">S</span><span class="sxs-lookup"><span data-stu-id="0af49-202">Y</span></span> |
| <span data-ttu-id="0af49-203">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="0af49-203">Boolean</span></span> | <span data-ttu-id="0af49-204">S</span><span class="sxs-lookup"><span data-stu-id="0af49-204">Y</span></span> |
| <span data-ttu-id="0af49-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="0af49-205">DataTimeOffset</span></span> | <span data-ttu-id="0af49-206">S</span><span class="sxs-lookup"><span data-stu-id="0af49-206">Y</span></span> |
| <span data-ttu-id="0af49-207">Matriz de cadeia</span><span class="sxs-lookup"><span data-stu-id="0af49-207">String Array</span></span> | <span data-ttu-id="0af49-208">N</span><span class="sxs-lookup"><span data-stu-id="0af49-208">N</span></span> |
| <span data-ttu-id="0af49-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="0af49-209">GeographyPoint</span></span> | <span data-ttu-id="0af49-210">N</span><span class="sxs-lookup"><span data-stu-id="0af49-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="0af49-211">Exemplo JSON: copiar dados de índice de pesquisa de tooAzure de SQL Server no local</span><span class="sxs-lookup"><span data-stu-id="0af49-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="0af49-212">Olá seguinte exemplo mostra:</span><span class="sxs-lookup"><span data-stu-id="0af49-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="0af49-213">Um serviço ligado do tipo [azuresearch, uma vez](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0af49-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="0af49-214">Um serviço ligado do tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0af49-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="0af49-215">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0af49-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="0af49-216">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0af49-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="0af49-217">A [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que utiliza [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) e [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0af49-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="0af49-218">exemplo de Olá copia dados de séries de tempo hora a hora de um índice de pesquisa do Azure do tooan no local do SQL Server da base de dados.</span><span class="sxs-lookup"><span data-stu-id="0af49-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="0af49-219">as propriedades de JSON Olá utilizadas neste exemplo são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="0af49-220">Como primeiro passo, configure o gateway de gestão de dados de Olá no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="0af49-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="0af49-221">instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0af49-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="0af49-222">**Serviço ligado de pesquisa do Azure:**</span><span class="sxs-lookup"><span data-stu-id="0af49-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="0af49-223">**Serviço ligado do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0af49-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="0af49-224">**Conjunto de dados de entrada do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0af49-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="0af49-225">exemplo de Olá pressupõe que criou uma tabela "MyTable" no SQL Server e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="0af49-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="0af49-226">Pode consultar através de várias tabelas na Olá mesma base de dados com um único conjunto de dados, mas uma única tabela tem de ser utilizado para typeProperty tableName de Olá conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="0af49-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="0af49-227">A definição "external": "true" informa serviço Data Factory esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

<span data-ttu-id="0af49-228">**Conjunto de dados de saída de pesquisa do Azure:**</span><span class="sxs-lookup"><span data-stu-id="0af49-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="0af49-229">Olá exemplo cópias dados tooan índice da Azure Search com o nome **produtos**.</span><span class="sxs-lookup"><span data-stu-id="0af49-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="0af49-230">Fábrica de dados não criar o índice de Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="0af49-231">Olá tootest de exemplo, crie um índice com este nome.</span><span class="sxs-lookup"><span data-stu-id="0af49-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="0af49-232">Criar o índice da Azure Search de Olá com Olá mesmo número de colunas que no conjunto de dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="0af49-233">Novas entradas são adicionadas toohello o índice da Azure Search a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0af49-233">New entries are added toohello Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="0af49-234">**Atividade de cópia de um pipeline com a origem SQL e o sink de índice da Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="0af49-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="0af49-235">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0af49-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="0af49-236">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**SqlSource** e **sink** tipo está definido demasiado**AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="0af49-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="0af49-237">consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá passado toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="0af49-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="0af49-238">Se estiver a copiar dados de um arquivo de dados em nuvem na Azure Search, `executionLocation` propriedade é necessária.</span><span class="sxs-lookup"><span data-stu-id="0af49-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="0af49-239">Olá fragmento JSON seguinte mostra as alterações de Olá necessária na atividade de cópia `typeProperties` como exemplo.</span><span class="sxs-lookup"><span data-stu-id="0af49-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="0af49-240">Verifique [copiar dados entre os arquivos de dados de nuvem](data-factory-data-movement-activities.md#global) secção para os valores suportados e obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="0af49-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="0af49-241">Copiar de uma origem de nuvem</span><span class="sxs-lookup"><span data-stu-id="0af49-241">Copy from a cloud source</span></span>
<span data-ttu-id="0af49-242">Se estiver a copiar dados de um arquivo de dados em nuvem na Azure Search, `executionLocation` propriedade é necessária.</span><span class="sxs-lookup"><span data-stu-id="0af49-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="0af49-243">Olá fragmento JSON seguinte mostra as alterações de Olá necessária na atividade de cópia `typeProperties` como exemplo.</span><span class="sxs-lookup"><span data-stu-id="0af49-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="0af49-244">Verifique [copiar dados entre os arquivos de dados de nuvem](data-factory-data-movement-activities.md#global) secção para os valores suportados e obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="0af49-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="0af49-245">Também pode mapear colunas do conjunto de dados de origem toocolumns do conjunto de dados dependente na definição de atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="0af49-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="0af49-246">Para obter mais informações, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="0af49-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0af49-247">Desempenho e otimização</span><span class="sxs-lookup"><span data-stu-id="0af49-247">Performance and tuning</span></span>  
<span data-ttu-id="0af49-248">Consulte Olá [guia Otimização e de desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) e de várias formas toooptimize-lo.</span><span class="sxs-lookup"><span data-stu-id="0af49-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0af49-249">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0af49-249">Next steps</span></span>
<span data-ttu-id="0af49-250">Consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="0af49-250">See hello following articles:</span></span>

* <span data-ttu-id="0af49-251">[Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criar um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0af49-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
