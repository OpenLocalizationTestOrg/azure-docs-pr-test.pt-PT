---
title: aaaCopy tooand de dados do Azure Data Lake Store | Microsoft Docs
description: Saiba como toocopy tooand dados do Data Lake Store utilizando o Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="5bf60-103">Copiar tooand de dados do Data Lake Store utilizando o Data Factory</span><span class="sxs-lookup"><span data-stu-id="5bf60-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="5bf60-104">Este artigo explica como toouse atividade de cópia no Azure Data Factory toomove dados tooand do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5bf60-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="5bf60-105">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, uma descrição geral do movimento de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="5bf60-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="5bf60-106">Cenários suportados</span><span class="sxs-lookup"><span data-stu-id="5bf60-106">Supported scenarios</span></span>
<span data-ttu-id="5bf60-107">Pode copiar dados **do Azure Data Lake Store** toohello seguir arquivos de dados:</span><span class="sxs-lookup"><span data-stu-id="5bf60-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="5bf60-108">Pode copiar dados de Olá seguir arquivos de dados **tooAzure Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="5bf60-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="5bf60-109">Crie uma conta de Data Lake Store antes de criar um pipeline com atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="5bf60-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="5bf60-110">Para obter mais informações, consulte [introdução ao Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5bf60-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="5bf60-111">Tipos de autenticação suportados</span><span class="sxs-lookup"><span data-stu-id="5bf60-111">Supported authentication types</span></span>
<span data-ttu-id="5bf60-112">conector do Data Lake Store Olá suporta estes tipos de autenticação:</span><span class="sxs-lookup"><span data-stu-id="5bf60-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="5bf60-113">Autenticação do principal de serviço</span><span class="sxs-lookup"><span data-stu-id="5bf60-113">Service principal authentication</span></span>
* <span data-ttu-id="5bf60-114">Autenticação de credencial (OAuth) do utilizador</span><span class="sxs-lookup"><span data-stu-id="5bf60-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="5bf60-115">Recomendamos que utilize autenticação principal de serviço, especialmente para uma cópia de dados agendada.</span><span class="sxs-lookup"><span data-stu-id="5bf60-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="5bf60-116">Comportamento de expiração do token pode ocorrer com autenticação de credenciais do utilizador.</span><span class="sxs-lookup"><span data-stu-id="5bf60-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="5bf60-117">Para detalhes de configuração, consulte Olá [ligado propriedades do serviço](#linked-service-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="5bf60-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="5bf60-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="5bf60-118">Get started</span></span>
<span data-ttu-id="5bf60-119">Pode criar um pipeline com uma atividade de cópia move os dados para/de um Azure Data Lake Store utilizando APIs/ferramentas diferentes.</span><span class="sxs-lookup"><span data-stu-id="5bf60-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="5bf60-120">Olá toocreate da forma mais fácil um dados toocopy do pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="5bf60-121">Para um tutorial sobre como criar um pipeline utilizando Olá Assistente para copiar, consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="5bf60-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="5bf60-122">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5bf60-123">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="5bf60-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="5bf60-124">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="5bf60-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="5bf60-125">Criar um **fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-125">Create a **data factory**.</span></span> <span data-ttu-id="5bf60-126">Uma fábrica de dados pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="5bf60-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="5bf60-127">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="5bf60-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="5bf60-128">Por exemplo, se estiver a copiar dados de um tooan de armazenamento de Blobs do Azure do Azure Data Lake Store, criar dois serviços ligados toolink a conta de armazenamento do Azure e a fábrica de dados do Azure Data Lake store tooyour.</span><span class="sxs-lookup"><span data-stu-id="5bf60-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="5bf60-129">As propriedades de serviço ligado que são específica tooAzure Data Lake Store, consulte [ligado propriedades do serviço](#linked-service-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="5bf60-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="5bf60-130">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="5bf60-131">Exemplo de Olá mencionado no passo último Olá, criar um contentor de blob do conjunto de dados toospecify Olá e a pasta que contém dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="5bf60-132">Além disso, crie outro conjunto de dados toospecify Olá ficheiros e pastas caminho no Olá Data Lake store que contém dados Olá copiados Olá do armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="5bf60-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="5bf60-133">As propriedades do conjunto de dados que são específica tooAzure Data Lake Store, consulte [propriedades do dataset](#dataset-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="5bf60-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="5bf60-134">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="5bf60-135">Exemplo de Olá mencionado anteriormente, que utilizar BlobSource como uma origem e AzureDataLakeStoreSink como um sink para atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="5bf60-136">Da mesma forma, se estiver a copiar no Blob Storage do Azure Data Lake Store tooAzure, utilizar AzureDataLakeStoreSource e BlobSink na atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="5bf60-137">Para as propriedades da atividade de cópia que são específica tooAzure Data Lake Store, consulte [copiar propriedades da atividade](#copy-activity-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="5bf60-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="5bf60-138">Para obter detalhes sobre como toouse um arquivo de dados como uma origem ou de um receptor de mensagens em fila, clique em ligação Olá na secção anterior do Olá para o arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="5bf60-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="5bf60-139">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="5bf60-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="5bf60-140">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="5bf60-141">Para exemplos com definições de JSON para entidades do Data Factory que são utilizados toocopy dados para/de um Azure Data Lake Store, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="5bf60-142">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizado toodefine Data Factory entidades específicas tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5bf60-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5bf60-143">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="5bf60-143">Linked service properties</span></span>
<span data-ttu-id="5bf60-144">Um serviço ligado liga uma fábrica de dados de tooa de arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="5bf60-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="5bf60-145">Criar um serviço ligado do tipo **AzureDataLakeStore** toolink a fábrica de dados de tooyour de dados do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5bf60-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="5bf60-146">Olá, a tabela seguinte descreve JSON elementos específicos tooData Lake Store ligado serviços.</span><span class="sxs-lookup"><span data-stu-id="5bf60-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="5bf60-147">Pode escolher entre o principal de serviço e a autenticação de credenciais do utilizador.</span><span class="sxs-lookup"><span data-stu-id="5bf60-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="5bf60-148">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5bf60-148">Property</span></span> | <span data-ttu-id="5bf60-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bf60-149">Description</span></span> | <span data-ttu-id="5bf60-150">Necessário</span><span class="sxs-lookup"><span data-stu-id="5bf60-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5bf60-151">**tipo**</span><span class="sxs-lookup"><span data-stu-id="5bf60-151">**type**</span></span> | <span data-ttu-id="5bf60-152">a propriedade de tipo Olá tem de ser definida demasiado**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="5bf60-153">Sim</span><span class="sxs-lookup"><span data-stu-id="5bf60-153">Yes</span></span> |
| <span data-ttu-id="5bf60-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="5bf60-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="5bf60-155">Informações sobre Olá conta do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5bf60-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="5bf60-156">Estas informações demora um dos seguintes formatos de Olá: `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="5bf60-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="5bf60-157">Sim</span><span class="sxs-lookup"><span data-stu-id="5bf60-157">Yes</span></span> |
| <span data-ttu-id="5bf60-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="5bf60-158">**subscriptionId**</span></span> | <span data-ttu-id="5bf60-159">Olá de toowhich de ID de subscrição do Azure conta do Data Lake Store pertence.</span><span class="sxs-lookup"><span data-stu-id="5bf60-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="5bf60-160">Obrigatório para sink</span><span class="sxs-lookup"><span data-stu-id="5bf60-160">Required for sink</span></span> |
| <span data-ttu-id="5bf60-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="5bf60-161">**resourceGroupName**</span></span> | <span data-ttu-id="5bf60-162">Olá de toowhich de nome do recurso do Azure grupo conta de Data Lake Store pertence.</span><span class="sxs-lookup"><span data-stu-id="5bf60-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="5bf60-163">Obrigatório para sink</span><span class="sxs-lookup"><span data-stu-id="5bf60-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="5bf60-164">Autenticação principal de serviço (recomendada)</span><span class="sxs-lookup"><span data-stu-id="5bf60-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="5bf60-165">toouse a autenticação principal de serviço, registar uma entidade de aplicação no Azure Active Directory (Azure AD) e conceda-Olá aceder tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5bf60-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="5bf60-166">Para obter passos detalhados, consulte [autenticação de serviço a serviço](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="5bf60-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="5bf60-167">Tome nota dos Olá valores, que utiliza os seguintes toodefine Olá serviço ligado:</span><span class="sxs-lookup"><span data-stu-id="5bf60-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="5bf60-168">ID da aplicação</span><span class="sxs-lookup"><span data-stu-id="5bf60-168">Application ID</span></span>
* <span data-ttu-id="5bf60-169">Chave da aplicação</span><span class="sxs-lookup"><span data-stu-id="5bf60-169">Application key</span></span> 
* <span data-ttu-id="5bf60-170">ID do inquilino</span><span class="sxs-lookup"><span data-stu-id="5bf60-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bf60-171">Se estiver a utilizar pipelines de dados do Olá Assistente para copiar tooauthor, certifique-se de que conceda principal de serviço Olá, pelo menos, um **leitor** função no controlo de acesso (gestão de identidades e acessos) para a conta de Data Lake Store Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="5bf60-172">Além disso, conceder, pelo menos, o principal de serviço Olá **leitura + executar** raiz de Data Lake Store para tooyour de permissão ("/") e os respectivos valores secundários.</span><span class="sxs-lookup"><span data-stu-id="5bf60-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="5bf60-173">Caso contrário, poderá ver a mensagem de saudação "Olá credenciais fornecidas são inválidas."</span><span class="sxs-lookup"><span data-stu-id="5bf60-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="5bf60-174">Depois de criar ou atualizar um principal de serviço no Azure AD, pode demorar alguns minutos para Olá alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="5bf60-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="5bf60-175">Certifique-se de principal de serviço Olá e configurações de lista (ACL) de controlo de acesso de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5bf60-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="5bf60-176">Se continuar a ver a mensagem de saudação "Olá credenciais fornecidas são inválidas", aguarde e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="5bf60-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="5bf60-177">Utilize autenticação principal de serviço, especificando Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="5bf60-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="5bf60-178">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5bf60-178">Property</span></span> | <span data-ttu-id="5bf60-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bf60-179">Description</span></span> | <span data-ttu-id="5bf60-180">Necessário</span><span class="sxs-lookup"><span data-stu-id="5bf60-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5bf60-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="5bf60-181">**servicePrincipalId**</span></span> | <span data-ttu-id="5bf60-182">Especifique o ID de cliente. da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="5bf60-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="5bf60-183">Sim</span><span class="sxs-lookup"><span data-stu-id="5bf60-183">Yes</span></span> |
| <span data-ttu-id="5bf60-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="5bf60-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="5bf60-185">Especifique a chave da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-185">Specify hello application's key.</span></span> | <span data-ttu-id="5bf60-186">Sim</span><span class="sxs-lookup"><span data-stu-id="5bf60-186">Yes</span></span> |
| <span data-ttu-id="5bf60-187">**inquilino**</span><span class="sxs-lookup"><span data-stu-id="5bf60-187">**tenant**</span></span> | <span data-ttu-id="5bf60-188">Especifique as informações de inquilinos Olá (nome ou o inquilino ID de domínio) em que reside a aplicação.</span><span class="sxs-lookup"><span data-stu-id="5bf60-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="5bf60-189">Pode obtê-lo por hovering rato Olá no canto superior direito de Olá de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bf60-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="5bf60-190">Sim</span><span class="sxs-lookup"><span data-stu-id="5bf60-190">Yes</span></span> |

<span data-ttu-id="5bf60-191">**Exemplo: Autenticação principal do serviço**</span><span class="sxs-lookup"><span data-stu-id="5bf60-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="5bf60-192">Autenticação de credenciais de utilizador</span><span class="sxs-lookup"><span data-stu-id="5bf60-192">User credential authentication</span></span>
<span data-ttu-id="5bf60-193">Em alternativa, pode utilizar toocopy de autenticação de credenciais de utilizador do ou tooData Lake Store, especificando Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="5bf60-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="5bf60-194">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5bf60-194">Property</span></span> | <span data-ttu-id="5bf60-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bf60-195">Description</span></span> | <span data-ttu-id="5bf60-196">Necessário</span><span class="sxs-lookup"><span data-stu-id="5bf60-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5bf60-197">**autorização**</span><span class="sxs-lookup"><span data-stu-id="5bf60-197">**authorization**</span></span> | <span data-ttu-id="5bf60-198">Clique em Olá **autorizar** clique no botão no Olá Editor do Data Factory e introduza as credenciais que atribui a propriedade de toothis do URL de autorização do Olá gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5bf60-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="5bf60-199">Sim</span><span class="sxs-lookup"><span data-stu-id="5bf60-199">Yes</span></span> |
| <span data-ttu-id="5bf60-200">**ID de sessão**</span><span class="sxs-lookup"><span data-stu-id="5bf60-200">**sessionId**</span></span> | <span data-ttu-id="5bf60-201">ID de sessão OAuth a partir de sessão de autorização do OAuth Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="5bf60-202">Cada ID de sessão é exclusivo e pode ser utilizado apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="5bf60-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="5bf60-203">Esta definição é gerada automaticamente quando utiliza Olá Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5bf60-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="5bf60-204">Sim</span><span class="sxs-lookup"><span data-stu-id="5bf60-204">Yes</span></span> |

<span data-ttu-id="5bf60-205">**Exemplo: Autenticação de credenciais de utilizador**</span><span class="sxs-lookup"><span data-stu-id="5bf60-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="5bf60-206">Expiração do token</span><span class="sxs-lookup"><span data-stu-id="5bf60-206">Token expiration</span></span>
<span data-ttu-id="5bf60-207">Olá, código de autorização que geram utilizando Olá **autorizar** botão expira após um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="5bf60-208">Olá seguir mensagem significa que esse token de autenticação Olá expirou:</span><span class="sxs-lookup"><span data-stu-id="5bf60-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="5bf60-209">Erro de operação de credencial: invalid_grant - AADSTS70002: erro ao validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="5bf60-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="5bf60-210">AADSTS70008: Olá fornecido a concessão de acesso expirado ou revogado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="5bf60-211">ID de rastreio: ID de correlação d18629e8-af88-43c5-88e3-d8419eb1fca1: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="5bf60-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="5bf60-212">Olá tabela seguinte mostra tempos de expiração de Olá de diferentes tipos de contas de utilizador:</span><span class="sxs-lookup"><span data-stu-id="5bf60-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="5bf60-213">Tipo de utilizador</span><span class="sxs-lookup"><span data-stu-id="5bf60-213">User type</span></span> | <span data-ttu-id="5bf60-214">Expira após</span><span class="sxs-lookup"><span data-stu-id="5bf60-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="5bf60-215">Contas de utilizador *não* geridas pelo Azure Active Directory (por exemplo, @hotmail.com ou @live.com)</span><span class="sxs-lookup"><span data-stu-id="5bf60-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="5bf60-216">12 horas</span><span class="sxs-lookup"><span data-stu-id="5bf60-216">12 hours</span></span> |
| <span data-ttu-id="5bf60-217">Contas de utilizadores geridas pelo Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bf60-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="5bf60-218">nos últimos 14 dias após o último setor de Olá executar</span><span class="sxs-lookup"><span data-stu-id="5bf60-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="5bf60-219">90 dias, se um setor com base num serviço ligado com base em OAuth é executado, pelo menos, uma vez a cada 14 dias</span><span class="sxs-lookup"><span data-stu-id="5bf60-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="5bf60-220">Se alterar a palavra-passe antes da hora de expiração do token de Olá, token Olá expira imediatamente.</span><span class="sxs-lookup"><span data-stu-id="5bf60-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="5bf60-221">Verá a mensagem de saudação mencionada anteriormente nesta secção.</span><span class="sxs-lookup"><span data-stu-id="5bf60-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="5bf60-222">Pode voltar a autorizar a conta de Olá utilizando Olá **autorizar** botão quando o token de Olá expira tooredeploy Olá serviço ligado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="5bf60-223">Também pode gerar valores para Olá **sessionId** e **autorização** Olá propriedades através de programação utilizando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="5bf60-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="5bf60-224">Para obter detalhes sobre as classes de fábrica de dados de Olá utilizados no código Olá, consulte Olá [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [ Classe de AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tópicos.</span><span class="sxs-lookup"><span data-stu-id="5bf60-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="5bf60-225">Adicionar uma referência tooversion `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` para Olá `WindowsFormsWebAuthenticationDialog` classe utilizado no código Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="5bf60-226">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="5bf60-226">Dataset properties</span></span>
<span data-ttu-id="5bf60-227">toospecify dados de entrada de toorepresent um conjunto de dados num arquivo Data Lake, definir Olá **tipo** propriedade de conjunto de dados de Olá demasiado**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="5bf60-228">Conjunto Olá **linkedServiceName** serviço ligado de propriedade do Olá dataset toohello nome Olá Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5bf60-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="5bf60-229">Para obter uma lista completa de secções JSON e propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5bf60-230">Secções de um conjunto de dados em JSON, tais como **estrutura**, **disponibilidade**, e **política**, são semelhantes para todos os tipos de conjunto de dados (SQL database do Azure, BLOBs do Azure e a tabela do Azure, para exemplo).</span><span class="sxs-lookup"><span data-stu-id="5bf60-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="5bf60-231">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações como a localização e o formato dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="5bf60-232">Olá **typeProperties** secção para um conjunto de dados do tipo **AzureDataLakeStore** contém Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="5bf60-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="5bf60-233">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5bf60-233">Property</span></span> | <span data-ttu-id="5bf60-234">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bf60-234">Description</span></span> | <span data-ttu-id="5bf60-235">Necessário</span><span class="sxs-lookup"><span data-stu-id="5bf60-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5bf60-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="5bf60-236">**folderPath**</span></span> |<span data-ttu-id="5bf60-237">Contentor de toohello caminho e a pasta no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5bf60-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="5bf60-238">Sim</span><span class="sxs-lookup"><span data-stu-id="5bf60-238">Yes</span></span> |
| <span data-ttu-id="5bf60-239">**nome de ficheiro**</span><span class="sxs-lookup"><span data-stu-id="5bf60-239">**fileName**</span></span> |<span data-ttu-id="5bf60-240">Nome do ficheiro de Olá no Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5bf60-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="5bf60-241">Olá **fileName** propriedade é opcional e maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5bf60-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="5bf60-242">Se especificar **fileName**, atividade Olá (incluindo cópia) funciona num ficheiro específico Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="5bf60-243">Quando **fileName** não for especificado, cópia inclui todos os ficheiros no **folderPath** no conjunto de dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="5bf60-244">Quando **fileName** não está especificado para um conjunto de dados de saída e **preserveHierarchy** não foram especificadas no receptor de atividade, nome de Olá do ficheiro de Olá gerado está num formato de Olá dados. _GUID_. txt '.</span><span class="sxs-lookup"><span data-stu-id="5bf60-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="5bf60-245">Por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="5bf60-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="5bf60-246">Não</span><span class="sxs-lookup"><span data-stu-id="5bf60-246">No</span></span> |
| <span data-ttu-id="5bf60-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="5bf60-247">**partitionedBy**</span></span> |<span data-ttu-id="5bf60-248">Olá **partitionedBy** propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="5bf60-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="5bf60-249">Pode utilizá-lo toospecify um dinâmico caminho e nome de ficheiro de dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="5bf60-250">Por exemplo, **folderPath** podem ser parametrizadas para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="5bf60-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="5bf60-251">Para obter detalhes e exemplos, consulte [Olá partitionedBy propriedade](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="5bf60-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="5bf60-252">Não</span><span class="sxs-lookup"><span data-stu-id="5bf60-252">No</span></span> |
| <span data-ttu-id="5bf60-253">**formato**</span><span class="sxs-lookup"><span data-stu-id="5bf60-253">**format**</span></span> | <span data-ttu-id="5bf60-254">é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, e  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="5bf60-255">Conjunto Olá **tipo** propriedade **formato** tooone destes valores.</span><span class="sxs-lookup"><span data-stu-id="5bf60-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="5bf60-256">Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) secções Olá [formatos de ficheiro e compressão suportados pelo Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="5bf60-257">Se pretender que os ficheiros de toocopy "como-é" entre arquivos baseados em ficheiros (cópia binário), ignorar Olá `format` secção em ambas as definições do conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="5bf60-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="5bf60-258">Não</span><span class="sxs-lookup"><span data-stu-id="5bf60-258">No</span></span> |
| <span data-ttu-id="5bf60-259">**compressão**</span><span class="sxs-lookup"><span data-stu-id="5bf60-259">**compression**</span></span> | <span data-ttu-id="5bf60-260">Especifique o tipo de Olá e nível de compressão de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="5bf60-261">Tipos suportados são **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="5bf60-262">Níveis suportados são **Optimal** e **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="5bf60-263">Para obter mais informações, consulte [formatos de ficheiro e compressão suportados pelo Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="5bf60-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="5bf60-264">Não</span><span class="sxs-lookup"><span data-stu-id="5bf60-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="5bf60-265">propriedade de partitionedBy Olá</span><span class="sxs-lookup"><span data-stu-id="5bf60-265">hello partitionedBy property</span></span>
<span data-ttu-id="5bf60-266">Pode especificar dinâmica **folderPath** e **fileName** propriedades para dados de séries de tempo com Olá **partitionedBy** propriedade, funções de fábrica de dados e do sistema variáveis.</span><span class="sxs-lookup"><span data-stu-id="5bf60-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="5bf60-267">Para obter mais informações, consulte Olá [do Azure Data Factory - as funções e variáveis do sistema](data-factory-functions-variables.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="5bf60-268">No seguinte exemplo, de Olá `{Slice}` é substituído pelo valor Olá da variável de sistema do Data Factory Olá `SliceStart` no formato de Olá especificado (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="5bf60-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="5bf60-269">nome de Olá `SliceStart` refere-se a hora de início do setor Olá toohello.</span><span class="sxs-lookup"><span data-stu-id="5bf60-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="5bf60-270">Olá `folderPath` propriedade é diferente para cada setor, como em `wikidatagateway/wikisampledataout/2014100103` ou `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="5bf60-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="5bf60-271">No Olá seguinte exemplo, Olá ano, mês, dia e tempo de `SliceStart` são extraídos em separado variáveis que são utilizadas por Olá `folderPath` e `fileName` propriedades:</span><span class="sxs-lookup"><span data-stu-id="5bf60-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
```JSON
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
<span data-ttu-id="5bf60-272">Para obter mais detalhes sobre conjuntos de dados de séries de tempo, agendar e setores, consulte Olá [conjuntos de dados no Azure Data Factory](data-factory-create-datasets.md) e [Data Factory agendamento e execução](data-factory-scheduling-and-execution.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="5bf60-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="5bf60-273">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="5bf60-273">Copy activity properties</span></span>
<span data-ttu-id="5bf60-274">Para uma lista completa das secções e propriedades disponíveis para definir as atividades, consulte Olá [Criar pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5bf60-275">Propriedades, tais como o nome, descrição e de saída, tabelas e política estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="5bf60-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="5bf60-276">Olá propriedades disponíveis nos Olá **typeProperties** secção de uma atividade variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="5bf60-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="5bf60-277">Para uma atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="5bf60-278">**AzureDataLakeStoreSource** suporta Olá seguinte propriedade no Olá **typeProperties** secção:</span><span class="sxs-lookup"><span data-stu-id="5bf60-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="5bf60-279">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5bf60-279">Property</span></span> | <span data-ttu-id="5bf60-280">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bf60-280">Description</span></span> | <span data-ttu-id="5bf60-281">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="5bf60-281">Allowed values</span></span> | <span data-ttu-id="5bf60-282">Necessário</span><span class="sxs-lookup"><span data-stu-id="5bf60-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5bf60-283">**recursiva**</span><span class="sxs-lookup"><span data-stu-id="5bf60-283">**recursive**</span></span> |<span data-ttu-id="5bf60-284">Indica se Olá é ler dados recursivamente subpastas Olá ou apenas a pasta especificada Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="5bf60-285">TRUE (valor predefinido), False</span><span class="sxs-lookup"><span data-stu-id="5bf60-285">True (default value), False</span></span> |<span data-ttu-id="5bf60-286">Não</span><span class="sxs-lookup"><span data-stu-id="5bf60-286">No</span></span> |


<span data-ttu-id="5bf60-287">**AzureDataLakeStoreSink** suporta Olá seguintes propriedades no Olá **typeProperties** secção:</span><span class="sxs-lookup"><span data-stu-id="5bf60-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="5bf60-288">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5bf60-288">Property</span></span> | <span data-ttu-id="5bf60-289">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bf60-289">Description</span></span> | <span data-ttu-id="5bf60-290">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="5bf60-290">Allowed values</span></span> | <span data-ttu-id="5bf60-291">Necessário</span><span class="sxs-lookup"><span data-stu-id="5bf60-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5bf60-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="5bf60-292">**copyBehavior**</span></span> |<span data-ttu-id="5bf60-293">Especifica o comportamento de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="5bf60-294"><b>PreserveHierarchy</b>: preserva a hierarquia de ficheiros de Olá na pasta de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="5bf60-295">o caminho relativo Olá da pasta de toosource do ficheiro de origem é idêntico toohello caminho relativo de tootarget da pasta do ficheiro de destino.</span><span class="sxs-lookup"><span data-stu-id="5bf60-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="5bf60-296"><b>FlattenHierarchy</b>: todos os ficheiros da pasta de origem Olá são criados no nível de primeiro Olá da pasta de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="5bf60-297">ficheiros do destino de Olá são criados com nomes gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5bf60-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="5bf60-298"><b>MergeFiles</b>: une todos os ficheiros a partir do ficheiro de tooone da pasta de origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="5bf60-299">Se hello nome de ficheiro ou blob for especificado, Olá ficheiro intercalado é Olá especificado nome.</span><span class="sxs-lookup"><span data-stu-id="5bf60-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="5bf60-300">Caso contrário, o nome de ficheiro Olá é gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5bf60-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="5bf60-301">Não</span><span class="sxs-lookup"><span data-stu-id="5bf60-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="5bf60-302">Exemplos de recursiva e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="5bf60-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="5bf60-303">Esta secção descreve o comportamento resultante de Olá de operação de cópia de Olá para diferentes combinações de valores recursiva e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="5bf60-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="5bf60-304">Recursiva</span><span class="sxs-lookup"><span data-stu-id="5bf60-304">recursive</span></span> | <span data-ttu-id="5bf60-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="5bf60-305">copyBehavior</span></span> | <span data-ttu-id="5bf60-306">Comportamento resultante</span><span class="sxs-lookup"><span data-stu-id="5bf60-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5bf60-307">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="5bf60-307">true</span></span> |<span data-ttu-id="5bf60-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="5bf60-308">preserveHierarchy</span></span> |<span data-ttu-id="5bf60-309">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5bf60-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="5bf60-310">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-310">Folder1</span></span><br/><span data-ttu-id="5bf60-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5bf60-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5bf60-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5bf60-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5bf60-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5bf60-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5bf60-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5bf60-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5bf60-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5bf60-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5bf60-317">pasta de destino Olá Pasta1 é criada com Olá mesmo estrutura como origem Olá</span><span class="sxs-lookup"><span data-stu-id="5bf60-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="5bf60-318">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-318">Folder1</span></span><br/><span data-ttu-id="5bf60-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5bf60-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5bf60-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5bf60-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5bf60-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5bf60-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5bf60-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5bf60-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5bf60-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="5bf60-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="5bf60-325">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="5bf60-325">true</span></span> |<span data-ttu-id="5bf60-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="5bf60-326">flattenHierarchy</span></span> |<span data-ttu-id="5bf60-327">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5bf60-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="5bf60-328">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-328">Folder1</span></span><br/><span data-ttu-id="5bf60-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5bf60-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5bf60-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5bf60-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5bf60-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5bf60-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5bf60-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5bf60-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5bf60-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5bf60-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5bf60-335">destino de Olá Pasta1 é criado com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5bf60-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="5bf60-336">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-336">Folder1</span></span><br/><span data-ttu-id="5bf60-337">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="5bf60-338">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="5bf60-339">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File3</span><span class="sxs-lookup"><span data-stu-id="5bf60-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="5bf60-340">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File4</span><span class="sxs-lookup"><span data-stu-id="5bf60-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="5bf60-341">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File5</span><span class="sxs-lookup"><span data-stu-id="5bf60-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="5bf60-342">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="5bf60-342">true</span></span> |<span data-ttu-id="5bf60-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="5bf60-343">mergeFiles</span></span> |<span data-ttu-id="5bf60-344">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5bf60-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="5bf60-345">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-345">Folder1</span></span><br/><span data-ttu-id="5bf60-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5bf60-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5bf60-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5bf60-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5bf60-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5bf60-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5bf60-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5bf60-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5bf60-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5bf60-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5bf60-352">destino de Olá Pasta1 é criado com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5bf60-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="5bf60-353">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-353">Folder1</span></span><br/><span data-ttu-id="5bf60-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + ficheiro 5 é intercalado conteúdo para um ficheiro com nome de ficheiro gerado automaticamente</span><span class="sxs-lookup"><span data-stu-id="5bf60-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="5bf60-355">FALSO</span><span class="sxs-lookup"><span data-stu-id="5bf60-355">false</span></span> |<span data-ttu-id="5bf60-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="5bf60-356">preserveHierarchy</span></span> |<span data-ttu-id="5bf60-357">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5bf60-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="5bf60-358">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-358">Folder1</span></span><br/><span data-ttu-id="5bf60-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5bf60-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5bf60-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5bf60-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5bf60-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5bf60-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5bf60-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5bf60-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5bf60-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5bf60-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5bf60-365">pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura</span><span class="sxs-lookup"><span data-stu-id="5bf60-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="5bf60-366">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-366">Folder1</span></span><br/><span data-ttu-id="5bf60-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5bf60-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="5bf60-369">Não Subfolder1 com File3, File4 e File5 captado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="5bf60-370">FALSO</span><span class="sxs-lookup"><span data-stu-id="5bf60-370">false</span></span> |<span data-ttu-id="5bf60-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="5bf60-371">flattenHierarchy</span></span> |<span data-ttu-id="5bf60-372">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5bf60-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="5bf60-373">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-373">Folder1</span></span><br/><span data-ttu-id="5bf60-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5bf60-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5bf60-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5bf60-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5bf60-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5bf60-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5bf60-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5bf60-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5bf60-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5bf60-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5bf60-380">pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura</span><span class="sxs-lookup"><span data-stu-id="5bf60-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="5bf60-381">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-381">Folder1</span></span><br/><span data-ttu-id="5bf60-382">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="5bf60-383">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="5bf60-384">Não Subfolder1 com File3, File4 e File5 captado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="5bf60-385">FALSO</span><span class="sxs-lookup"><span data-stu-id="5bf60-385">false</span></span> |<span data-ttu-id="5bf60-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="5bf60-386">mergeFiles</span></span> |<span data-ttu-id="5bf60-387">Para uma pasta de origem Pasta1 com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5bf60-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="5bf60-388">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-388">Folder1</span></span><br/><span data-ttu-id="5bf60-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5bf60-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5bf60-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5bf60-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5bf60-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5bf60-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5bf60-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5bf60-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5bf60-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5bf60-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5bf60-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5bf60-395">pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura</span><span class="sxs-lookup"><span data-stu-id="5bf60-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="5bf60-396">Pasta1</span><span class="sxs-lookup"><span data-stu-id="5bf60-396">Folder1</span></span><br/><span data-ttu-id="5bf60-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 conteúdos são intercalados para um ficheiro com nome de ficheiro gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5bf60-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="5bf60-398">nome gerado automaticamente para File1</span><span class="sxs-lookup"><span data-stu-id="5bf60-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="5bf60-399">Não Subfolder1 com File3, File4 e File5 captado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="5bf60-400">Formatos de ficheiro e compressão suportados</span><span class="sxs-lookup"><span data-stu-id="5bf60-400">Supported file and compression formats</span></span>
<span data-ttu-id="5bf60-401">Para obter mais informações, consulte Olá [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="5bf60-402">Exemplos JSON para copiar dados tooand do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5bf60-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="5bf60-403">Olá exemplos a seguir fornece definições JSON de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="5bf60-404">Pode utilizar estes toocreate de definições de exemplo um pipeline com Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5bf60-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5bf60-405">Olá exemplos mostram como toocopy tooand de dados do armazenamento do Data Lake Store e BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bf60-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="5bf60-406">No entanto, os dados podem ser copiados _diretamente_ de qualquer um dos Olá origens tooany de sinks Olá suportado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="5bf60-407">Para obter mais informações, consulte a secção de Olá "arquivos de dados suportadas e formatos" em Olá [mover dados utilizando a atividade de cópia](data-factory-data-movement-activities.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="5bf60-408">Exemplo: Copiar dados de tooAzure do Blob Storage do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5bf60-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="5bf60-409">Mostra o código de exemplo de Olá nesta secção:</span><span class="sxs-lookup"><span data-stu-id="5bf60-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="5bf60-410">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5bf60-411">Um serviço ligado do tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="5bf60-412">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5bf60-413">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="5bf60-414">A [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que utiliza [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="5bf60-415">Olá exemplos mostram como séries de tempo dados a partir do Blob Storage do Azure são copiado tooData Lake Store a cada hora.</span><span class="sxs-lookup"><span data-stu-id="5bf60-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="5bf60-416">**Serviço ligado do Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="5bf60-416">**Azure Storage linked service**</span></span>

```JSON
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

<span data-ttu-id="5bf60-417">**Serviço ligado do Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="5bf60-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="5bf60-418">Para detalhes de configuração, consulte Olá [ligado propriedades do serviço](#linked-service-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="5bf60-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="5bf60-419">**Conjunto de dados de entrada do blobs do Azure**</span><span class="sxs-lookup"><span data-stu-id="5bf60-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="5bf60-420">No seguinte exemplo de Olá, dados são captados um blob de novo a cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="5bf60-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="5bf60-421">Olá pasta caminho e nome de ficheiro para o blob Olá dinamicamente são avaliados com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="5bf60-422">caminho da pasta Olá utiliza Olá ano, mês e parte do dia Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="5bf60-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="5bf60-423">nome de ficheiro Olá utiliza hora Olá parte Olá a hora de início.</span><span class="sxs-lookup"><span data-stu-id="5bf60-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="5bf60-424">Olá `"external": true` definição informa o serviço do Data Factory Olá nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="5bf60-425">**Conjunto de dados de saída do Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="5bf60-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="5bf60-426">Olá arquivo de Lake de tooData de dados de cópias de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5bf60-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="5bf60-427">Novos dados são copiados tooData Lake Store a cada hora.</span><span class="sxs-lookup"><span data-stu-id="5bf60-427">New data is copied tooData Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="5bf60-428">**Atividade de cópia de um pipeline com uma origem de blob e um receptor de Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="5bf60-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="5bf60-429">No seguinte exemplo de Olá, pipeline Olá contém uma atividade de cópia está configurada toouse Olá conjuntos de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="5bf60-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="5bf60-430">atividade de cópia de Olá é agendada toorun a cada hora.</span><span class="sxs-lookup"><span data-stu-id="5bf60-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="5bf60-431">No pipeline de Olá definição JSON, Olá `source` tipo está definido demasiado`BlobSource`e Olá `sink` tipo está definido demasiado`AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="5bf60-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="5bf60-432">Exemplo: Copiar dados do Azure Data Lake Store tooan BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="5bf60-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="5bf60-433">Mostra o código de exemplo de Olá nesta secção:</span><span class="sxs-lookup"><span data-stu-id="5bf60-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="5bf60-434">Um serviço ligado do tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="5bf60-435">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5bf60-436">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="5bf60-437">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5bf60-438">A [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que utiliza [AzureDataLakeStoreSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5bf60-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5bf60-439">código de Olá copia dados de séries de tempo da Data Lake Store tooan BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="5bf60-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="5bf60-440">**Serviço ligado do Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="5bf60-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="5bf60-441">Para detalhes de configuração, consulte Olá [ligado propriedades do serviço](#linked-service-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="5bf60-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="5bf60-442">**Serviço ligado do Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="5bf60-442">**Azure Storage linked service**</span></span>

```JSON
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
<span data-ttu-id="5bf60-443">**Conjunto de dados de entrada do Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="5bf60-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="5bf60-444">Neste exemplo, definição `"external"` demasiado`true` informa o serviço do Data Factory Olá nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf60-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
<span data-ttu-id="5bf60-445">**Conjunto de dados de saída do blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="5bf60-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="5bf60-446">No seguinte exemplo de Olá, são escritos dados no blob tooa de novo a cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="5bf60-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="5bf60-447">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="5bf60-448">caminho da pasta Olá utiliza Olá ano, mês, dia e parte horas Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="5bf60-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="5bf60-449">**Uma atividade de cópia num pipeline com uma origem de Azure Data Lake Store e um receptor de blob**</span><span class="sxs-lookup"><span data-stu-id="5bf60-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="5bf60-450">No seguinte exemplo de Olá, pipeline Olá contém uma atividade de cópia está configurada toouse Olá conjuntos de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="5bf60-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="5bf60-451">atividade de cópia de Olá é agendada toorun a cada hora.</span><span class="sxs-lookup"><span data-stu-id="5bf60-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="5bf60-452">No pipeline de Olá definição JSON, Olá `source` tipo está definido demasiado`AzureDataLakeStoreSource`e Olá `sink` tipo está definido demasiado`BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="5bf60-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

<span data-ttu-id="5bf60-453">Na definição de atividade de cópia de Olá, também pode mapear colunas de Olá toocolumns de conjunto de dados de origem no conjunto de dados do Olá sink.</span><span class="sxs-lookup"><span data-stu-id="5bf60-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="5bf60-454">Para obter mais informações, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5bf60-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5bf60-455">Desempenho e otimização</span><span class="sxs-lookup"><span data-stu-id="5bf60-455">Performance and tuning</span></span>
<span data-ttu-id="5bf60-456">toolearn sobre fatores Olá que afetam o desempenho de atividade de cópia e como toooptimize-lo, consulte Olá [guia Otimização e de desempenho de atividade de cópia](data-factory-copy-activity-performance.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
