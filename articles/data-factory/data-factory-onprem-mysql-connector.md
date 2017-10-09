---
title: dados aaaMove MySQL utilizando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como dados toomove MySQL da base de dados utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="846b5-103">Mover dados de MySQL utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="846b5-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="846b5-104">Este artigo explica como toouse Olá atividade de cópia em dados do Azure Data Factory toomove a partir de uma base de dados MySQL no local.</span><span class="sxs-lookup"><span data-stu-id="846b5-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="846b5-105">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="846b5-106">Pode copiar dados de um arquivo de dados do local MySQL dados arquivo tooany suportado sink.</span><span class="sxs-lookup"><span data-stu-id="846b5-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="846b5-107">Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="846b5-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="846b5-108">Fábrica de dados atualmente suporta apenas mover tooother arquivos de dados de arquivo de dados de um de dados MySQL, mas não para mover dados de noutro arquivo de dados MySQL de tooan de arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="846b5-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="846b5-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="846b5-109">Prerequisites</span></span>
<span data-ttu-id="846b5-110">Serviço de fábrica de dados suporta origens de MySQL tooon local ao ligar utilizando Olá Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="846b5-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="846b5-111">Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Data Management Gateway e instruções passo a passo sobre como configurar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="846b5-112">É necessário gateway, mesmo se a base de dados MySQL Olá estiver alojada numa máquina virtual IaaS do Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="846b5-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="846b5-113">Pode instalar o gateway de Olá num Olá mesma VM como dados de Olá armazenar ou numa VM diferente desde como gateway Olá pode ligar toohello base de dados.</span><span class="sxs-lookup"><span data-stu-id="846b5-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="846b5-114">Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.</span><span class="sxs-lookup"><span data-stu-id="846b5-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="846b5-115">Versões suportadas e instalação</span><span class="sxs-lookup"><span data-stu-id="846b5-115">Supported versions and installation</span></span>
<span data-ttu-id="846b5-116">Para o Data Management Gateway tooconnect toohello base de dados MySQL, terá de tooinstall Olá [MySQL conector/Net para Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versão 6.6.5 ou superior) Olá no mesmo sistema como Olá Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="846b5-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="846b5-117">O MySQL versão 5.1 e posterior é suportado.</span><span class="sxs-lookup"><span data-stu-id="846b5-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="846b5-118">Se clicar em erro "Autenticação falhou porque a parte remota de Olá fechou fluxo de transporte Olá.", considere tooupgrade Olá versão de toohigher MySQL conector/Net.</span><span class="sxs-lookup"><span data-stu-id="846b5-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="846b5-119">Introdução</span><span class="sxs-lookup"><span data-stu-id="846b5-119">Getting started</span></span>
<span data-ttu-id="846b5-120">Pode criar um pipeline com uma atividade de cópia move os dados de um arquivo de dados no local Cassandra utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="846b5-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="846b5-121">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="846b5-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="846b5-122">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="846b5-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="846b5-123">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="846b5-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="846b5-124">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="846b5-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="846b5-125">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="846b5-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="846b5-126">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="846b5-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="846b5-127">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="846b5-128">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="846b5-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="846b5-129">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="846b5-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="846b5-130">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="846b5-131">Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados a partir de um arquivo de dados MySQL no local, consulte [exemplo JSON: copiar dados de MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="846b5-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="846b5-132">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine arquivo de dados do Data Factory entidades tooa específico MySQL:</span><span class="sxs-lookup"><span data-stu-id="846b5-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="846b5-133">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="846b5-133">Linked service properties</span></span>
<span data-ttu-id="846b5-134">Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooMySQL ligado.</span><span class="sxs-lookup"><span data-stu-id="846b5-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="846b5-135">Propriedade</span><span class="sxs-lookup"><span data-stu-id="846b5-135">Property</span></span> | <span data-ttu-id="846b5-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="846b5-136">Description</span></span> | <span data-ttu-id="846b5-137">Necessário</span><span class="sxs-lookup"><span data-stu-id="846b5-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="846b5-138">tipo</span><span class="sxs-lookup"><span data-stu-id="846b5-138">type</span></span> |<span data-ttu-id="846b5-139">a propriedade de tipo Olá tem de ser definida: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="846b5-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="846b5-140">Sim</span><span class="sxs-lookup"><span data-stu-id="846b5-140">Yes</span></span> |
| <span data-ttu-id="846b5-141">servidor</span><span class="sxs-lookup"><span data-stu-id="846b5-141">server</span></span> |<span data-ttu-id="846b5-142">Nome do servidor do Olá MySQL.</span><span class="sxs-lookup"><span data-stu-id="846b5-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="846b5-143">Sim</span><span class="sxs-lookup"><span data-stu-id="846b5-143">Yes</span></span> |
| <span data-ttu-id="846b5-144">base de dados</span><span class="sxs-lookup"><span data-stu-id="846b5-144">database</span></span> |<span data-ttu-id="846b5-145">Nome da base de dados MySQL Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="846b5-146">Sim</span><span class="sxs-lookup"><span data-stu-id="846b5-146">Yes</span></span> |
| <span data-ttu-id="846b5-147">Esquema</span><span class="sxs-lookup"><span data-stu-id="846b5-147">schema</span></span> |<span data-ttu-id="846b5-148">Nome do esquema de Olá na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="846b5-149">Não</span><span class="sxs-lookup"><span data-stu-id="846b5-149">No</span></span> |
| <span data-ttu-id="846b5-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="846b5-150">authenticationType</span></span> |<span data-ttu-id="846b5-151">Tipo de autenticação utilizado toohello tooconnect de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="846b5-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="846b5-152">Os valores possíveis são: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="846b5-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="846b5-153">Sim</span><span class="sxs-lookup"><span data-stu-id="846b5-153">Yes</span></span> |
| <span data-ttu-id="846b5-154">o nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="846b5-154">username</span></span> |<span data-ttu-id="846b5-155">Especifique a base de dados do utilizador nome tooconnect toohello MySQL.</span><span class="sxs-lookup"><span data-stu-id="846b5-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="846b5-156">Sim</span><span class="sxs-lookup"><span data-stu-id="846b5-156">Yes</span></span> |
| <span data-ttu-id="846b5-157">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="846b5-157">password</span></span> |<span data-ttu-id="846b5-158">Especifique a palavra-passe da conta de utilizador de Olá que especificou.</span><span class="sxs-lookup"><span data-stu-id="846b5-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="846b5-159">Sim</span><span class="sxs-lookup"><span data-stu-id="846b5-159">Yes</span></span> |
| <span data-ttu-id="846b5-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="846b5-160">gatewayName</span></span> |<span data-ttu-id="846b5-161">Nome do gateway de Olá que Olá serviço Data Factory deve utilizar tooconnect toohello no local de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="846b5-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="846b5-162">Sim</span><span class="sxs-lookup"><span data-stu-id="846b5-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="846b5-163">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="846b5-163">Dataset properties</span></span>
<span data-ttu-id="846b5-164">Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="846b5-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="846b5-165">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="846b5-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="846b5-166">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="846b5-167">Olá typeProperties secção para o conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados MySQL) tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="846b5-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="846b5-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="846b5-168">Property</span></span> | <span data-ttu-id="846b5-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="846b5-169">Description</span></span> | <span data-ttu-id="846b5-170">Necessário</span><span class="sxs-lookup"><span data-stu-id="846b5-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="846b5-171">tableName</span><span class="sxs-lookup"><span data-stu-id="846b5-171">tableName</span></span> |<span data-ttu-id="846b5-172">Nome da tabela de Olá na instância de base de dados MySQL que o serviço ligado de Olá referenciada.</span><span class="sxs-lookup"><span data-stu-id="846b5-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="846b5-173">Não (se **consulta** de **RelationalSource** especificado)</span><span class="sxs-lookup"><span data-stu-id="846b5-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="846b5-174">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="846b5-174">Copy activity properties</span></span>
<span data-ttu-id="846b5-175">Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="846b5-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="846b5-176">Propriedades, tais como o nome, descrição, tabelas de entrada e de saída, são as políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="846b5-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="846b5-177">Enquanto, propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="846b5-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="846b5-178">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="846b5-179">Quando a origem de atividade de cópia é do tipo **RelationalSource** (que inclui o MySQL), na secção typeProperties, estão disponível Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="846b5-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="846b5-180">Propriedade</span><span class="sxs-lookup"><span data-stu-id="846b5-180">Property</span></span> | <span data-ttu-id="846b5-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="846b5-181">Description</span></span> | <span data-ttu-id="846b5-182">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="846b5-182">Allowed values</span></span> | <span data-ttu-id="846b5-183">Necessário</span><span class="sxs-lookup"><span data-stu-id="846b5-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="846b5-184">consulta</span><span class="sxs-lookup"><span data-stu-id="846b5-184">query</span></span> |<span data-ttu-id="846b5-185">Utilize Olá consulta personalizada tooread dados.</span><span class="sxs-lookup"><span data-stu-id="846b5-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="846b5-186">Cadeia de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="846b5-186">SQL query string.</span></span> <span data-ttu-id="846b5-187">Por exemplo: selecionar * de MyTable.</span><span class="sxs-lookup"><span data-stu-id="846b5-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="846b5-188">Não (se **tableName** de **dataset** especificado)</span><span class="sxs-lookup"><span data-stu-id="846b5-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="846b5-189">Exemplo JSON: copiar dados de MySQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="846b5-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="846b5-190">Neste exemplo fornece definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="846b5-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="846b5-191">Mostra como toocopy dados a partir de um MySQL no local da base de dados tooan Blob Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="846b5-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="846b5-192">No entanto, os dados podem ser copiado tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="846b5-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="846b5-193">Este exemplo fornece fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="846b5-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="846b5-194">Não inclui instruções passo a passo para criar a fábrica de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="846b5-195">Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="846b5-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="846b5-196">exemplo de Olá tem Olá seguintes entidades da fábrica de dados:</span><span class="sxs-lookup"><span data-stu-id="846b5-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="846b5-197">Um serviço ligado do tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="846b5-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="846b5-198">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="846b5-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="846b5-199">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="846b5-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="846b5-200">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="846b5-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="846b5-201">A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="846b5-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="846b5-202">exemplo de Olá copia dados a partir de um resultado da consulta num blob de tooa de base de dados MySQL hora a hora.</span><span class="sxs-lookup"><span data-stu-id="846b5-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="846b5-203">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="846b5-204">Como primeiro passo, o programa de configuração Olá o data management gateway.</span><span class="sxs-lookup"><span data-stu-id="846b5-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="846b5-205">instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="846b5-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="846b5-206">**Serviço ligado do MySQL:**</span><span class="sxs-lookup"><span data-stu-id="846b5-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="846b5-207">**Serviço ligado do Storage do Azure:**</span><span class="sxs-lookup"><span data-stu-id="846b5-207">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="846b5-208">**Conjunto de dados entrado de MySQL:**</span><span class="sxs-lookup"><span data-stu-id="846b5-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="846b5-209">exemplo de Olá pressupõe que criou uma tabela "MyTable" MySQL e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="846b5-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="846b5-210">A definição "external": "true" informa serviço do Data Factory Olá nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="846b5-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
            "typeProperties": {},
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

<span data-ttu-id="846b5-211">**Conjunto de dados de saída do Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="846b5-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="846b5-212">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="846b5-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="846b5-213">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="846b5-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="846b5-214">caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="846b5-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="846b5-215">**Pipeline com atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="846b5-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="846b5-216">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora.</span><span class="sxs-lookup"><span data-stu-id="846b5-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="846b5-217">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="846b5-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="846b5-218">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá passado toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="846b5-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
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
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="846b5-219">Mapeamento de tipo para o MySQL</span><span class="sxs-lookup"><span data-stu-id="846b5-219">Type mapping for MySQL</span></span>
<span data-ttu-id="846b5-220">Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá abordagem de dois passos a seguir:</span><span class="sxs-lookup"><span data-stu-id="846b5-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="846b5-221">Converter do tipo de too.NET de tipos de origem nativo</span><span class="sxs-lookup"><span data-stu-id="846b5-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="846b5-222">Converter do tipo de sink de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="846b5-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="846b5-223">Quando move dados tooMySQL, Olá mapeamentos seguintes são utilizados dos tipos de too.NET de tipos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="846b5-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="846b5-224">Tipo de base de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="846b5-224">MySQL Database type</span></span> | <span data-ttu-id="846b5-225">Tipo de .NET framework</span><span class="sxs-lookup"><span data-stu-id="846b5-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="846b5-226">bigint não assinado</span><span class="sxs-lookup"><span data-stu-id="846b5-226">bigint unsigned</span></span> |<span data-ttu-id="846b5-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="846b5-227">Decimal</span></span> |
| <span data-ttu-id="846b5-228">bigint</span><span class="sxs-lookup"><span data-stu-id="846b5-228">bigint</span></span> |<span data-ttu-id="846b5-229">Int64</span><span class="sxs-lookup"><span data-stu-id="846b5-229">Int64</span></span> |
| <span data-ttu-id="846b5-230">bits</span><span class="sxs-lookup"><span data-stu-id="846b5-230">bit</span></span> |<span data-ttu-id="846b5-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="846b5-231">Decimal</span></span> |
| <span data-ttu-id="846b5-232">blob</span><span class="sxs-lookup"><span data-stu-id="846b5-232">blob</span></span> |<span data-ttu-id="846b5-233">Byte]</span><span class="sxs-lookup"><span data-stu-id="846b5-233">Byte[]</span></span> |
| <span data-ttu-id="846b5-234">bool</span><span class="sxs-lookup"><span data-stu-id="846b5-234">bool</span></span> |<span data-ttu-id="846b5-235">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="846b5-235">Boolean</span></span> |
| <span data-ttu-id="846b5-236">char</span><span class="sxs-lookup"><span data-stu-id="846b5-236">char</span></span> |<span data-ttu-id="846b5-237">Cadeia</span><span class="sxs-lookup"><span data-stu-id="846b5-237">String</span></span> |
| <span data-ttu-id="846b5-238">Data</span><span class="sxs-lookup"><span data-stu-id="846b5-238">date</span></span> |<span data-ttu-id="846b5-239">DateTime</span><span class="sxs-lookup"><span data-stu-id="846b5-239">Datetime</span></span> |
| <span data-ttu-id="846b5-240">DateTime</span><span class="sxs-lookup"><span data-stu-id="846b5-240">datetime</span></span> |<span data-ttu-id="846b5-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="846b5-241">Datetime</span></span> |
| <span data-ttu-id="846b5-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="846b5-242">decimal</span></span> |<span data-ttu-id="846b5-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="846b5-243">Decimal</span></span> |
| <span data-ttu-id="846b5-244">precisão dupla</span><span class="sxs-lookup"><span data-stu-id="846b5-244">double precision</span></span> |<span data-ttu-id="846b5-245">duplo</span><span class="sxs-lookup"><span data-stu-id="846b5-245">Double</span></span> |
| <span data-ttu-id="846b5-246">duplo</span><span class="sxs-lookup"><span data-stu-id="846b5-246">double</span></span> |<span data-ttu-id="846b5-247">duplo</span><span class="sxs-lookup"><span data-stu-id="846b5-247">Double</span></span> |
| <span data-ttu-id="846b5-248">Enum</span><span class="sxs-lookup"><span data-stu-id="846b5-248">enum</span></span> |<span data-ttu-id="846b5-249">Cadeia</span><span class="sxs-lookup"><span data-stu-id="846b5-249">String</span></span> |
| <span data-ttu-id="846b5-250">Número de vírgula flutuante</span><span class="sxs-lookup"><span data-stu-id="846b5-250">float</span></span> |<span data-ttu-id="846b5-251">Único</span><span class="sxs-lookup"><span data-stu-id="846b5-251">Single</span></span> |
| <span data-ttu-id="846b5-252">Int não assinado</span><span class="sxs-lookup"><span data-stu-id="846b5-252">int unsigned</span></span> |<span data-ttu-id="846b5-253">Int64</span><span class="sxs-lookup"><span data-stu-id="846b5-253">Int64</span></span> |
| <span data-ttu-id="846b5-254">Int</span><span class="sxs-lookup"><span data-stu-id="846b5-254">int</span></span> |<span data-ttu-id="846b5-255">Int32</span><span class="sxs-lookup"><span data-stu-id="846b5-255">Int32</span></span> |
| <span data-ttu-id="846b5-256">número inteiro sem sinal</span><span class="sxs-lookup"><span data-stu-id="846b5-256">integer unsigned</span></span> |<span data-ttu-id="846b5-257">Int64</span><span class="sxs-lookup"><span data-stu-id="846b5-257">Int64</span></span> |
| <span data-ttu-id="846b5-258">número inteiro</span><span class="sxs-lookup"><span data-stu-id="846b5-258">integer</span></span> |<span data-ttu-id="846b5-259">Int32</span><span class="sxs-lookup"><span data-stu-id="846b5-259">Int32</span></span> |
| <span data-ttu-id="846b5-260">varbinary longo</span><span class="sxs-lookup"><span data-stu-id="846b5-260">long varbinary</span></span> |<span data-ttu-id="846b5-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="846b5-261">Byte[]</span></span> |
| <span data-ttu-id="846b5-262">varchar longo</span><span class="sxs-lookup"><span data-stu-id="846b5-262">long varchar</span></span> |<span data-ttu-id="846b5-263">Cadeia</span><span class="sxs-lookup"><span data-stu-id="846b5-263">String</span></span> |
| <span data-ttu-id="846b5-264">longblob</span><span class="sxs-lookup"><span data-stu-id="846b5-264">longblob</span></span> |<span data-ttu-id="846b5-265">Byte]</span><span class="sxs-lookup"><span data-stu-id="846b5-265">Byte[]</span></span> |
| <span data-ttu-id="846b5-266">LONGTEXT</span><span class="sxs-lookup"><span data-stu-id="846b5-266">longtext</span></span> |<span data-ttu-id="846b5-267">Cadeia</span><span class="sxs-lookup"><span data-stu-id="846b5-267">String</span></span> |
| <span data-ttu-id="846b5-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="846b5-268">mediumblob</span></span> |<span data-ttu-id="846b5-269">Byte]</span><span class="sxs-lookup"><span data-stu-id="846b5-269">Byte[]</span></span> |
| <span data-ttu-id="846b5-270">mediumint não assinado</span><span class="sxs-lookup"><span data-stu-id="846b5-270">mediumint unsigned</span></span> |<span data-ttu-id="846b5-271">Int64</span><span class="sxs-lookup"><span data-stu-id="846b5-271">Int64</span></span> |
| <span data-ttu-id="846b5-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="846b5-272">mediumint</span></span> |<span data-ttu-id="846b5-273">Int32</span><span class="sxs-lookup"><span data-stu-id="846b5-273">Int32</span></span> |
| <span data-ttu-id="846b5-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="846b5-274">mediumtext</span></span> |<span data-ttu-id="846b5-275">Cadeia</span><span class="sxs-lookup"><span data-stu-id="846b5-275">String</span></span> |
| <span data-ttu-id="846b5-276">um valor numérico</span><span class="sxs-lookup"><span data-stu-id="846b5-276">numeric</span></span> |<span data-ttu-id="846b5-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="846b5-277">Decimal</span></span> |
| <span data-ttu-id="846b5-278">real</span><span class="sxs-lookup"><span data-stu-id="846b5-278">real</span></span> |<span data-ttu-id="846b5-279">duplo</span><span class="sxs-lookup"><span data-stu-id="846b5-279">Double</span></span> |
| <span data-ttu-id="846b5-280">definir</span><span class="sxs-lookup"><span data-stu-id="846b5-280">set</span></span> |<span data-ttu-id="846b5-281">Cadeia</span><span class="sxs-lookup"><span data-stu-id="846b5-281">String</span></span> |
| <span data-ttu-id="846b5-282">smallint não assinado</span><span class="sxs-lookup"><span data-stu-id="846b5-282">smallint unsigned</span></span> |<span data-ttu-id="846b5-283">Int32</span><span class="sxs-lookup"><span data-stu-id="846b5-283">Int32</span></span> |
| <span data-ttu-id="846b5-284">smallint</span><span class="sxs-lookup"><span data-stu-id="846b5-284">smallint</span></span> |<span data-ttu-id="846b5-285">Int16</span><span class="sxs-lookup"><span data-stu-id="846b5-285">Int16</span></span> |
| <span data-ttu-id="846b5-286">Texto</span><span class="sxs-lookup"><span data-stu-id="846b5-286">text</span></span> |<span data-ttu-id="846b5-287">Cadeia</span><span class="sxs-lookup"><span data-stu-id="846b5-287">String</span></span> |
| <span data-ttu-id="846b5-288">hora</span><span class="sxs-lookup"><span data-stu-id="846b5-288">time</span></span> |<span data-ttu-id="846b5-289">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="846b5-289">TimeSpan</span></span> |
| <span data-ttu-id="846b5-290">carimbo de data/hora</span><span class="sxs-lookup"><span data-stu-id="846b5-290">timestamp</span></span> |<span data-ttu-id="846b5-291">DateTime</span><span class="sxs-lookup"><span data-stu-id="846b5-291">Datetime</span></span> |
| <span data-ttu-id="846b5-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="846b5-292">tinyblob</span></span> |<span data-ttu-id="846b5-293">Byte]</span><span class="sxs-lookup"><span data-stu-id="846b5-293">Byte[]</span></span> |
| <span data-ttu-id="846b5-294">tinyint não assinado</span><span class="sxs-lookup"><span data-stu-id="846b5-294">tinyint unsigned</span></span> |<span data-ttu-id="846b5-295">Int16</span><span class="sxs-lookup"><span data-stu-id="846b5-295">Int16</span></span> |
| <span data-ttu-id="846b5-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="846b5-296">tinyint</span></span> |<span data-ttu-id="846b5-297">Int16</span><span class="sxs-lookup"><span data-stu-id="846b5-297">Int16</span></span> |
| <span data-ttu-id="846b5-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="846b5-298">tinytext</span></span> |<span data-ttu-id="846b5-299">Cadeia</span><span class="sxs-lookup"><span data-stu-id="846b5-299">String</span></span> |
| <span data-ttu-id="846b5-300">varchar</span><span class="sxs-lookup"><span data-stu-id="846b5-300">varchar</span></span> |<span data-ttu-id="846b5-301">Cadeia</span><span class="sxs-lookup"><span data-stu-id="846b5-301">String</span></span> |
| <span data-ttu-id="846b5-302">ano</span><span class="sxs-lookup"><span data-stu-id="846b5-302">year</span></span> |<span data-ttu-id="846b5-303">Int</span><span class="sxs-lookup"><span data-stu-id="846b5-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="846b5-304">Mapear colunas toosink de origem</span><span class="sxs-lookup"><span data-stu-id="846b5-304">Map source toosink columns</span></span>
<span data-ttu-id="846b5-305">toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="846b5-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="846b5-306">Repetíveis leitura a partir de origens relacionais</span><span class="sxs-lookup"><span data-stu-id="846b5-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="846b5-307">Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="846b5-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="846b5-308">No Azure Data Factory, pode voltar a executar um setor manualmente.</span><span class="sxs-lookup"><span data-stu-id="846b5-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="846b5-309">Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="846b5-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="846b5-310">Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado.</span><span class="sxs-lookup"><span data-stu-id="846b5-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="846b5-311">Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="846b5-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="846b5-312">Desempenho e a otimização</span><span class="sxs-lookup"><span data-stu-id="846b5-312">Performance and Tuning</span></span>
<span data-ttu-id="846b5-313">Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.</span><span class="sxs-lookup"><span data-stu-id="846b5-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
