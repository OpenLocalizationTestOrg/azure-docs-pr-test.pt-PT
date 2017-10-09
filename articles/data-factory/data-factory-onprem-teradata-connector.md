---
title: dados aaaMove Teradata utilizando o Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre o conector Teradata para Olá serviço fábrica de dados que lhe permite mover dados de base de dados Teradata"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="fc9f4-103">Mover dados de Teradata utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="fc9f4-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="fc9f4-104">Este artigo explica como toouse Olá atividade de cópia no Azure Data Factory toomove da base de dados um local Teradata.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="fc9f4-105">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="fc9f4-106">Pode copiar dados de um arquivo de dados do local Teradata dados arquivo tooany suportado sink.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="fc9f4-107">Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="fc9f4-108">Fábrica de dados atualmente suporta apenas mover tooother arquivos de dados de arquivo de dados de um de dados Teradata, mas não para mover dados de noutro arquivo de dados Teradata de tooa de arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fc9f4-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fc9f4-109">Prerequisites</span></span>
<span data-ttu-id="fc9f4-110">Fábrica de dados suporta a ligação origens de Teradata tooon local através de Olá Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="fc9f4-111">Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Data Management Gateway e instruções passo a passo sobre como configurar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="fc9f4-112">É necessário gateway, mesmo se hello Teradata estiver alojada numa VM do IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="fc9f4-113">Pode instalar o gateway de Olá num Olá mesma VM do IaaS como dados de Olá armazenar ou numa VM diferente desde como gateway Olá pode ligar toohello base de dados.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="fc9f4-114">Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="fc9f4-115">Versões suportadas e instalação</span><span class="sxs-lookup"><span data-stu-id="fc9f4-115">Supported versions and installation</span></span>
<span data-ttu-id="fc9f4-116">Para o Data Management Gateway tooconnect toohello base de dados Teradata, terá de tooinstall Olá [fornecedor de dados .NET para Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versão 14 ou acima no Olá mesmo sistema como Olá Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="fc9f4-117">Teradata versão 12 e posterior é suportado.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fc9f4-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="fc9f4-118">Getting started</span></span>
<span data-ttu-id="fc9f4-119">Pode criar um pipeline com uma atividade de cópia move os dados de um arquivo de dados no local Cassandra utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="fc9f4-120">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="fc9f4-121">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="fc9f4-122">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fc9f4-123">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fc9f4-124">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="fc9f4-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="fc9f4-125">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="fc9f4-126">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="fc9f4-127">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="fc9f4-128">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="fc9f4-129">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="fc9f4-130">Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados a partir de um arquivo de dados Teradata no local, consulte [exemplo JSON: copiar dados de Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="fc9f4-131">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine arquivo de dados do Data Factory entidades tooa específico Teradata:</span><span class="sxs-lookup"><span data-stu-id="fc9f4-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fc9f4-132">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="fc9f4-132">Linked service properties</span></span>
<span data-ttu-id="fc9f4-133">Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooTeradata ligado.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="fc9f4-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="fc9f4-134">Property</span></span> | <span data-ttu-id="fc9f4-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="fc9f4-135">Description</span></span> | <span data-ttu-id="fc9f4-136">Necessário</span><span class="sxs-lookup"><span data-stu-id="fc9f4-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc9f4-137">tipo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-137">type</span></span> |<span data-ttu-id="fc9f4-138">a propriedade de tipo Olá tem de ser definida: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="fc9f4-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="fc9f4-139">Sim</span><span class="sxs-lookup"><span data-stu-id="fc9f4-139">Yes</span></span> |
| <span data-ttu-id="fc9f4-140">servidor</span><span class="sxs-lookup"><span data-stu-id="fc9f4-140">server</span></span> |<span data-ttu-id="fc9f4-141">Nome do servidor de Teradata Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="fc9f4-142">Sim</span><span class="sxs-lookup"><span data-stu-id="fc9f4-142">Yes</span></span> |
| <span data-ttu-id="fc9f4-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fc9f4-143">authenticationType</span></span> |<span data-ttu-id="fc9f4-144">Tipo de autenticação utilizado a base de dados Teradata de toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="fc9f4-145">Os valores possíveis são: anónimo, básico e Windows.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="fc9f4-146">Sim</span><span class="sxs-lookup"><span data-stu-id="fc9f4-146">Yes</span></span> |
| <span data-ttu-id="fc9f4-147">o nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="fc9f4-147">username</span></span> |<span data-ttu-id="fc9f4-148">Especifique o nome de utilizador se estiver a utilizar autenticação básica ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="fc9f4-149">Não</span><span class="sxs-lookup"><span data-stu-id="fc9f4-149">No</span></span> |
| <span data-ttu-id="fc9f4-150">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="fc9f4-150">password</span></span> |<span data-ttu-id="fc9f4-151">Especifique a palavra-passe da conta de utilizador de Olá especificado para nome de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="fc9f4-152">Não</span><span class="sxs-lookup"><span data-stu-id="fc9f4-152">No</span></span> |
| <span data-ttu-id="fc9f4-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fc9f4-153">gatewayName</span></span> |<span data-ttu-id="fc9f4-154">Nome do gateway de Olá que Olá serviço Data Factory deve utilizar a base de dados do tooconnect toohello no local Teradata.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="fc9f4-155">Sim</span><span class="sxs-lookup"><span data-stu-id="fc9f4-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="fc9f4-156">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="fc9f4-156">Dataset properties</span></span>
<span data-ttu-id="fc9f4-157">Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fc9f4-158">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fc9f4-159">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="fc9f4-160">Atualmente, existem sem propriedades de tipo suportadas para o conjunto de dados do Olá Teradata.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="fc9f4-161">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-161">Copy activity properties</span></span>
<span data-ttu-id="fc9f4-162">Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fc9f4-163">Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="fc9f4-164">Enquanto, propriedades disponíveis na secção de typeProperties Olá da atividade de Olá variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="fc9f4-165">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="fc9f4-166">Quando a origem de Olá é do tipo **RelationalSource** (que inclui Teradata), Olá seguintes propriedades está disponível no **typeProperties** secção:</span><span class="sxs-lookup"><span data-stu-id="fc9f4-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="fc9f4-167">Propriedade</span><span class="sxs-lookup"><span data-stu-id="fc9f4-167">Property</span></span> | <span data-ttu-id="fc9f4-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="fc9f4-168">Description</span></span> | <span data-ttu-id="fc9f4-169">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="fc9f4-169">Allowed values</span></span> | <span data-ttu-id="fc9f4-170">Necessário</span><span class="sxs-lookup"><span data-stu-id="fc9f4-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc9f4-171">consulta</span><span class="sxs-lookup"><span data-stu-id="fc9f4-171">query</span></span> |<span data-ttu-id="fc9f4-172">Utilize Olá consulta personalizada tooread dados.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="fc9f4-173">Cadeia de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-173">SQL query string.</span></span> <span data-ttu-id="fc9f4-174">Por exemplo: selecionar * de MyTable.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="fc9f4-175">Sim</span><span class="sxs-lookup"><span data-stu-id="fc9f4-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="fc9f4-176">Exemplo JSON: copiar dados de Teradata tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="fc9f4-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="fc9f4-177">Olá exemplo a seguir fornece definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fc9f4-178">Estes mostram como toocopy dados Teradata tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="fc9f4-179">No entanto, os dados podem ser copiado tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="fc9f4-180">exemplo de Olá tem Olá seguintes entidades da fábrica de dados:</span><span class="sxs-lookup"><span data-stu-id="fc9f4-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="fc9f4-181">Um serviço ligado do tipo [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="fc9f4-182">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fc9f4-183">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="fc9f4-184">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fc9f4-185">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fc9f4-186">exemplo de Olá copia dados a partir de um resultado da consulta num blob de tooa de base de dados Teradata a cada hora.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="fc9f4-187">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="fc9f4-188">Como primeiro passo, o programa de configuração Olá o data management gateway.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="fc9f4-189">instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fc9f4-190">**Teradata serviço ligado:**</span><span class="sxs-lookup"><span data-stu-id="fc9f4-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="fc9f4-191">**Serviço ligado do armazenamento de Blobs do Azure:**</span><span class="sxs-lookup"><span data-stu-id="fc9f4-191">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="fc9f4-192">**Conjunto de dados entrado de Teradata:**</span><span class="sxs-lookup"><span data-stu-id="fc9f4-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="fc9f4-193">exemplo de Olá pressupõe que criou uma tabela "MyTable" Teradata e contém uma coluna chamada "timestamp" para dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="fc9f4-194">A definição "external": true informa o serviço do Data Factory Olá nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="fc9f4-195">**Conjunto de dados de saída do Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="fc9f4-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fc9f4-196">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fc9f4-197">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="fc9f4-198">caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="fc9f4-199">**Pipeline com atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="fc9f4-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="fc9f4-200">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun hora a hora.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="fc9f4-201">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="fc9f4-202">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá passado toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="fc9f4-203">Mapeamento de tipos para Teradata</span><span class="sxs-lookup"><span data-stu-id="fc9f4-203">Type mapping for Teradata</span></span>
<span data-ttu-id="fc9f4-204">Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, Olá atividade de cópia executa conversões de tipo automática dos tipos de toosink de tipos de origem com Olá seguir abordagem de passo 2:</span><span class="sxs-lookup"><span data-stu-id="fc9f4-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="fc9f4-205">Converter do tipo de too.NET de tipos de origem nativo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="fc9f4-206">Converter do tipo de sink de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="fc9f4-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="fc9f4-207">Quando move dados tooTeradata, hello mapeamentos seguintes são utilizados nas Teradata tipo too.NET tipo.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="fc9f4-208">Tipo de base de dados Teradata</span><span class="sxs-lookup"><span data-stu-id="fc9f4-208">Teradata Database type</span></span> | <span data-ttu-id="fc9f4-209">Tipo de .NET framework</span><span class="sxs-lookup"><span data-stu-id="fc9f4-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="fc9f4-210">char</span><span class="sxs-lookup"><span data-stu-id="fc9f4-210">Char</span></span> |<span data-ttu-id="fc9f4-211">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-211">String</span></span> |
| <span data-ttu-id="fc9f4-212">CLOB</span><span class="sxs-lookup"><span data-stu-id="fc9f4-212">Clob</span></span> |<span data-ttu-id="fc9f4-213">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-213">String</span></span> |
| <span data-ttu-id="fc9f4-214">Gráfico</span><span class="sxs-lookup"><span data-stu-id="fc9f4-214">Graphic</span></span> |<span data-ttu-id="fc9f4-215">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-215">String</span></span> |
| <span data-ttu-id="fc9f4-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="fc9f4-216">VarChar</span></span> |<span data-ttu-id="fc9f4-217">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-217">String</span></span> |
| <span data-ttu-id="fc9f4-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="fc9f4-218">VarGraphic</span></span> |<span data-ttu-id="fc9f4-219">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-219">String</span></span> |
| <span data-ttu-id="fc9f4-220">Blobs</span><span class="sxs-lookup"><span data-stu-id="fc9f4-220">Blob</span></span> |<span data-ttu-id="fc9f4-221">Byte]</span><span class="sxs-lookup"><span data-stu-id="fc9f4-221">Byte[]</span></span> |
| <span data-ttu-id="fc9f4-222">Bytes</span><span class="sxs-lookup"><span data-stu-id="fc9f4-222">Byte</span></span> |<span data-ttu-id="fc9f4-223">Byte]</span><span class="sxs-lookup"><span data-stu-id="fc9f4-223">Byte[]</span></span> |
| <span data-ttu-id="fc9f4-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="fc9f4-224">VarByte</span></span> |<span data-ttu-id="fc9f4-225">Byte]</span><span class="sxs-lookup"><span data-stu-id="fc9f4-225">Byte[]</span></span> |
| <span data-ttu-id="fc9f4-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="fc9f4-226">BigInt</span></span> |<span data-ttu-id="fc9f4-227">Int64</span><span class="sxs-lookup"><span data-stu-id="fc9f4-227">Int64</span></span> |
| <span data-ttu-id="fc9f4-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="fc9f4-228">ByteInt</span></span> |<span data-ttu-id="fc9f4-229">Int16</span><span class="sxs-lookup"><span data-stu-id="fc9f4-229">Int16</span></span> |
| <span data-ttu-id="fc9f4-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc9f4-230">Decimal</span></span> |<span data-ttu-id="fc9f4-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc9f4-231">Decimal</span></span> |
| <span data-ttu-id="fc9f4-232">duplo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-232">Double</span></span> |<span data-ttu-id="fc9f4-233">duplo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-233">Double</span></span> |
| <span data-ttu-id="fc9f4-234">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="fc9f4-234">Integer</span></span> |<span data-ttu-id="fc9f4-235">Int32</span><span class="sxs-lookup"><span data-stu-id="fc9f4-235">Int32</span></span> |
| <span data-ttu-id="fc9f4-236">Número</span><span class="sxs-lookup"><span data-stu-id="fc9f4-236">Number</span></span> |<span data-ttu-id="fc9f4-237">duplo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-237">Double</span></span> |
| <span data-ttu-id="fc9f4-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="fc9f4-238">SmallInt</span></span> |<span data-ttu-id="fc9f4-239">Int16</span><span class="sxs-lookup"><span data-stu-id="fc9f4-239">Int16</span></span> |
| <span data-ttu-id="fc9f4-240">Data</span><span class="sxs-lookup"><span data-stu-id="fc9f4-240">Date</span></span> |<span data-ttu-id="fc9f4-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="fc9f4-241">DateTime</span></span> |
| <span data-ttu-id="fc9f4-242">Hora</span><span class="sxs-lookup"><span data-stu-id="fc9f4-242">Time</span></span> |<span data-ttu-id="fc9f4-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-243">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-244">Período de tempo com fuso horário</span><span class="sxs-lookup"><span data-stu-id="fc9f4-244">Time With Time Zone</span></span> |<span data-ttu-id="fc9f4-245">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-245">String</span></span> |
| <span data-ttu-id="fc9f4-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="fc9f4-246">Timestamp</span></span> |<span data-ttu-id="fc9f4-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="fc9f4-247">DateTime</span></span> |
| <span data-ttu-id="fc9f4-248">Timestamp com o fuso horário</span><span class="sxs-lookup"><span data-stu-id="fc9f4-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="fc9f4-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="fc9f4-249">DateTimeOffset</span></span> |
| <span data-ttu-id="fc9f4-250">Dia de intervalo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-250">Interval Day</span></span> |<span data-ttu-id="fc9f4-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-251">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-252">Intervalo dia tooHour</span><span class="sxs-lookup"><span data-stu-id="fc9f4-252">Interval Day tooHour</span></span> |<span data-ttu-id="fc9f4-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-253">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-254">Intervalo dia tooMinute</span><span class="sxs-lookup"><span data-stu-id="fc9f4-254">Interval Day tooMinute</span></span> |<span data-ttu-id="fc9f4-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-255">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-256">Intervalo dia tooSecond</span><span class="sxs-lookup"><span data-stu-id="fc9f4-256">Interval Day tooSecond</span></span> |<span data-ttu-id="fc9f4-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-257">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-258">Hora de intervalo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-258">Interval Hour</span></span> |<span data-ttu-id="fc9f4-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-259">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-260">Intervalo hora tooMinute</span><span class="sxs-lookup"><span data-stu-id="fc9f4-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="fc9f4-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-261">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-262">Intervalo hora tooSecond</span><span class="sxs-lookup"><span data-stu-id="fc9f4-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="fc9f4-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-263">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-264">Minuto do intervalo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-264">Interval Minute</span></span> |<span data-ttu-id="fc9f4-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-265">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-266">TooSecond minuto do intervalo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="fc9f4-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-267">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-268">Intervalo segundo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-268">Interval Second</span></span> |<span data-ttu-id="fc9f4-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc9f4-269">TimeSpan</span></span> |
| <span data-ttu-id="fc9f4-270">Intervalo ano</span><span class="sxs-lookup"><span data-stu-id="fc9f4-270">Interval Year</span></span> |<span data-ttu-id="fc9f4-271">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-271">String</span></span> |
| <span data-ttu-id="fc9f4-272">Intervalo ano tooMonth</span><span class="sxs-lookup"><span data-stu-id="fc9f4-272">Interval Year tooMonth</span></span> |<span data-ttu-id="fc9f4-273">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-273">String</span></span> |
| <span data-ttu-id="fc9f4-274">Mês do intervalo</span><span class="sxs-lookup"><span data-stu-id="fc9f4-274">Interval Month</span></span> |<span data-ttu-id="fc9f4-275">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-275">String</span></span> |
| <span data-ttu-id="fc9f4-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="fc9f4-276">Period(Date)</span></span> |<span data-ttu-id="fc9f4-277">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-277">String</span></span> |
| <span data-ttu-id="fc9f4-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="fc9f4-278">Period(Time)</span></span> |<span data-ttu-id="fc9f4-279">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-279">String</span></span> |
| <span data-ttu-id="fc9f4-280">Período (Time com fuso horário)</span><span class="sxs-lookup"><span data-stu-id="fc9f4-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="fc9f4-281">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-281">String</span></span> |
| <span data-ttu-id="fc9f4-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="fc9f4-282">Period(Timestamp)</span></span> |<span data-ttu-id="fc9f4-283">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-283">String</span></span> |
| <span data-ttu-id="fc9f4-284">Período (Timestamp com o fuso horário)</span><span class="sxs-lookup"><span data-stu-id="fc9f4-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="fc9f4-285">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-285">String</span></span> |
| <span data-ttu-id="fc9f4-286">XML</span><span class="sxs-lookup"><span data-stu-id="fc9f4-286">Xml</span></span> |<span data-ttu-id="fc9f4-287">Cadeia</span><span class="sxs-lookup"><span data-stu-id="fc9f4-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="fc9f4-288">Mapear colunas toosink de origem</span><span class="sxs-lookup"><span data-stu-id="fc9f4-288">Map source toosink columns</span></span>
<span data-ttu-id="fc9f4-289">toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="fc9f4-290">Repetíveis leitura a partir de origens relacionais</span><span class="sxs-lookup"><span data-stu-id="fc9f4-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="fc9f4-291">Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="fc9f4-292">No Azure Data Factory, pode voltar a executar um setor manualmente.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fc9f4-293">Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fc9f4-294">Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fc9f4-295">Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fc9f4-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fc9f4-296">Desempenho e a otimização</span><span class="sxs-lookup"><span data-stu-id="fc9f4-296">Performance and Tuning</span></span>
<span data-ttu-id="fc9f4-297">Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.</span><span class="sxs-lookup"><span data-stu-id="fc9f4-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
