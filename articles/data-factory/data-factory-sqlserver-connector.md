---
title: aaaMove tooand de dados do SQL Server | Microsoft Docs
description: "Saiba mais sobre como dados toomove da SQL Server da base de dados que está no local ou numa VM do Azure utilizando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="0cd43-103">Mover tooand de dados do SQL Server no local ou no IaaS (VM do Azure) utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0cd43-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="0cd43-104">Este artigo explica como toouse Olá atividade de cópia de dados de toomove do Azure Data Factory para/de uma base de dados do SQL Server no local.</span><span class="sxs-lookup"><span data-stu-id="0cd43-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="0cd43-105">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="0cd43-106">Cenários suportados</span><span class="sxs-lookup"><span data-stu-id="0cd43-106">Supported scenarios</span></span>
<span data-ttu-id="0cd43-107">Pode copiar dados **de uma base de dados do SQL Server** toohello seguir arquivos de dados:</span><span class="sxs-lookup"><span data-stu-id="0cd43-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="0cd43-108">Pode copiar dados de Olá seguir arquivos de dados **base de dados do SQL Server tooa**:</span><span class="sxs-lookup"><span data-stu-id="0cd43-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="0cd43-109">Versões suportadas do SQL Server</span><span class="sxs-lookup"><span data-stu-id="0cd43-109">Supported SQL Server versions</span></span>
<span data-ttu-id="0cd43-110">Este suporte de conector do SQL Server copiar dados a partir de / toohello seguintes versões de instância alojado no local ou no IaaS do Azure utilizando a autenticação do SQL Server e a autenticação do Windows: SQL Server 2016, o SQL Server 2014, o SQL Server 2012, o SQL Server 2008 R2, o SQL Server Server 2008, o SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="0cd43-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="0cd43-111">Ativar a conectividade</span><span class="sxs-lookup"><span data-stu-id="0cd43-111">Enabling connectivity</span></span>
<span data-ttu-id="0cd43-112">conceitos de Olá e passos necessários para estabelecer a ligação com SQL Server alojado no local ou no IaaS do Azure VMs (infraestrutura-como-um-serviço) são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="0cd43-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="0cd43-113">Em ambos os casos, terá de toouse Data Management Gateway para a conectividade.</span><span class="sxs-lookup"><span data-stu-id="0cd43-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="0cd43-114">Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Data Management Gateway e instruções passo a passo sobre como configurar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="0cd43-115">Configurar uma instância de gateway é um pré-requisito para a ligação com o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cd43-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="0cd43-116">Enquanto pode instalar o gateway no Olá mesmo no local instância VM de nuvem ou máquina como hello do SQL Server para um melhor desempenho, recomendamos que instalar em computadores separados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="0cd43-117">A existência de gateway Olá e o SQL Server em máquinas separadas reduz a contenção de recursos.</span><span class="sxs-lookup"><span data-stu-id="0cd43-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0cd43-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="0cd43-118">Getting started</span></span>
<span data-ttu-id="0cd43-119">Pode criar um pipeline com uma atividade de cópia move os dados de/para uma base de dados do SQL Server no local utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="0cd43-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="0cd43-120">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="0cd43-121">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="0cd43-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="0cd43-122">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0cd43-123">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0cd43-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0cd43-124">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="0cd43-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="0cd43-125">Criar um **fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-125">Create a **data factory**.</span></span> <span data-ttu-id="0cd43-126">Uma fábrica de dados pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="0cd43-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="0cd43-127">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="0cd43-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="0cd43-128">Por exemplo, se estiver a copiar dados de um tooan de base de dados do SQL Server blob storage do Azure, pode cria dois serviços ligados toolink a base de dados do SQL Server e a fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd43-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="0cd43-129">Para o serviço ligado as propriedades da base de dados de servidor de tooSQL específico, consulte [ligado propriedades do serviço](#linked-service-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="0cd43-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="0cd43-130">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="0cd43-131">Exemplo de Olá mencionado no passo último Olá, crie uma tabela SQL do conjunto de dados toospecify Olá na base de dados do SQL Server que contém dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="0cd43-132">Crie outro conjunto de dados toospecify Olá o contentor de BLOBs e pasta de Olá que contém dados Olá copiados Olá base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cd43-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="0cd43-133">Para o conjunto de dados as propriedades da base de dados de servidor de tooSQL específico, consulte [propriedades do dataset](#dataset-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="0cd43-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="0cd43-134">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="0cd43-135">Exemplo de Olá mencionado anteriormente, que utilizar SqlSource como uma origem e BlobSink como um sink para atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="0cd43-136">Da mesma forma, se estiver a copiar a partir do Blob Storage do Azure tooSQL base de dados do servidor, utilizar BlobSource e SqlSink na atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="0cd43-137">Para copiar atividade propriedades tooSQL específica da base de dados do servidor, consulte [copiar propriedades da atividade](#copy-activity-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="0cd43-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="0cd43-138">Para obter detalhes sobre como toouse um arquivo de dados como uma origem ou de um receptor de mensagens em fila, clique em ligação Olá na secção anterior do Olá para o arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="0cd43-139">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="0cd43-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="0cd43-140">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="0cd43-141">Para exemplos com definições de JSON para entidades do Data Factory que são utilizados toocopy dados para/de uma base de dados do SQL Server no local, consulte [exemplos JSON](#json-examples-for-copying-data-from-and-to-sql-server) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="0cd43-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="0cd43-142">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooSQL servidor:</span><span class="sxs-lookup"><span data-stu-id="0cd43-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="0cd43-143">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="0cd43-143">Linked service properties</span></span>
<span data-ttu-id="0cd43-144">Criar um serviço ligado do tipo **OnPremisesSqlServer** toolink uma fábrica de dados no local do SQL Server da base de dados tooa.</span><span class="sxs-lookup"><span data-stu-id="0cd43-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="0cd43-145">Olá, a tabela seguinte fornece uma descrição do serviço ligado do SQL Server do JSON elementos local tooon específico.</span><span class="sxs-lookup"><span data-stu-id="0cd43-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="0cd43-146">Olá, a tabela seguinte fornece uma descrição para JSON elementos específico tooSQL serviço de servidor ligado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="0cd43-147">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0cd43-147">Property</span></span> | <span data-ttu-id="0cd43-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cd43-148">Description</span></span> | <span data-ttu-id="0cd43-149">Necessário</span><span class="sxs-lookup"><span data-stu-id="0cd43-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0cd43-150">tipo</span><span class="sxs-lookup"><span data-stu-id="0cd43-150">type</span></span> |<span data-ttu-id="0cd43-151">a propriedade de tipo Olá deve ser definida como: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="0cd43-152">Sim</span><span class="sxs-lookup"><span data-stu-id="0cd43-152">Yes</span></span> |
| <span data-ttu-id="0cd43-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="0cd43-153">connectionString</span></span> |<span data-ttu-id="0cd43-154">Especifique as informações de connectionString necessárias tooconnect toohello no local do SQL Server da base de dados utilizando a autenticação SQL ou autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="0cd43-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="0cd43-155">Sim</span><span class="sxs-lookup"><span data-stu-id="0cd43-155">Yes</span></span> |
| <span data-ttu-id="0cd43-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0cd43-156">gatewayName</span></span> |<span data-ttu-id="0cd43-157">Nome do gateway de Olá que Olá serviço Data Factory deve utilizar tooconnect toohello no local do SQL Server da base de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="0cd43-158">Sim</span><span class="sxs-lookup"><span data-stu-id="0cd43-158">Yes</span></span> |
| <span data-ttu-id="0cd43-159">o nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="0cd43-159">username</span></span> |<span data-ttu-id="0cd43-160">Especifique o nome de utilizador se estiver a utilizar a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="0cd43-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="0cd43-161">Exemplo: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="0cd43-162">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-162">No</span></span> |
| <span data-ttu-id="0cd43-163">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="0cd43-163">password</span></span> |<span data-ttu-id="0cd43-164">Especifique a palavra-passe da conta de utilizador de Olá especificado para nome de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0cd43-165">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-165">No</span></span> |

<span data-ttu-id="0cd43-166">Pode encriptar as credenciais utilizando Olá **New-AzureRmDataFactoryEncryptValue** cmdlet e utilizá-los na cadeia de ligação de Olá, conforme mostrado no seguinte exemplo de Olá (**EncryptedCredential** propriedade):</span><span class="sxs-lookup"><span data-stu-id="0cd43-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="0cd43-167">Amostras</span><span class="sxs-lookup"><span data-stu-id="0cd43-167">Samples</span></span>
<span data-ttu-id="0cd43-168">**JSON para utilizar a autenticação do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0cd43-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="0cd43-169">**JSON para utilizar a autenticação do Windows**</span><span class="sxs-lookup"><span data-stu-id="0cd43-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="0cd43-170">O Data Management Gateway será representar Olá especificado utilizador conta tooconnect toohello no local do SQL Server base de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="0cd43-171">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="0cd43-171">Dataset properties</span></span>
<span data-ttu-id="0cd43-172">Nos exemplos de Olá, utilizou um conjunto de dados do tipo **SqlServerTable** toorepresent uma tabela numa base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cd43-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="0cd43-173">Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0cd43-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0cd43-174">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL Server, BLOBs do Azure, a tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="0cd43-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0cd43-175">secção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="0cd43-176">Olá **typeProperties** secção Olá conjunto de dados do tipo **SqlServerTable** tem Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="0cd43-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="0cd43-177">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0cd43-177">Property</span></span> | <span data-ttu-id="0cd43-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cd43-178">Description</span></span> | <span data-ttu-id="0cd43-179">Necessário</span><span class="sxs-lookup"><span data-stu-id="0cd43-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0cd43-180">tableName</span><span class="sxs-lookup"><span data-stu-id="0cd43-180">tableName</span></span> |<span data-ttu-id="0cd43-181">Nome da tabela de Olá ou vista na instância de base de dados do SQL Server Olá pelo serviço ligado referenciada.</span><span class="sxs-lookup"><span data-stu-id="0cd43-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="0cd43-182">Sim</span><span class="sxs-lookup"><span data-stu-id="0cd43-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="0cd43-183">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0cd43-183">Copy activity properties</span></span>
<span data-ttu-id="0cd43-184">Se estiver a mover dados de uma base de dados do SQL Server, definir o tipo de origem Olá na atividade de cópia de Olá demasiado**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="0cd43-185">Da mesma forma, se estiver a mover dados tooa do SQL Server da base de dados, definir o tipo de sink Olá na atividade de cópia de Olá demasiado**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="0cd43-186">Esta secção fornece uma lista de propriedades suportadas por SqlSource e SqlSink.</span><span class="sxs-lookup"><span data-stu-id="0cd43-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="0cd43-187">Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0cd43-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0cd43-188">Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="0cd43-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="0cd43-189">Olá atividade de cópia demora apenas uma entrada e produz saída de apenas um.</span><span class="sxs-lookup"><span data-stu-id="0cd43-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="0cd43-190">Enquanto, propriedades disponíveis na secção de typeProperties Olá da atividade de Olá variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="0cd43-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="0cd43-191">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="0cd43-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="0cd43-192">SqlSource</span></span>
<span data-ttu-id="0cd43-193">Quando a origem de uma atividade de cópia é do tipo **SqlSource**, Olá seguintes propriedades está disponível no **typeProperties** secção:</span><span class="sxs-lookup"><span data-stu-id="0cd43-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="0cd43-194">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0cd43-194">Property</span></span> | <span data-ttu-id="0cd43-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cd43-195">Description</span></span> | <span data-ttu-id="0cd43-196">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0cd43-196">Allowed values</span></span> | <span data-ttu-id="0cd43-197">Necessário</span><span class="sxs-lookup"><span data-stu-id="0cd43-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0cd43-198">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="0cd43-198">sqlReaderQuery</span></span> |<span data-ttu-id="0cd43-199">Utilize Olá consulta personalizada tooread dados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0cd43-200">Cadeia de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="0cd43-200">SQL query string.</span></span> <span data-ttu-id="0cd43-201">Por exemplo: selecionar * de MyTable.</span><span class="sxs-lookup"><span data-stu-id="0cd43-201">For example: select * from MyTable.</span></span> <span data-ttu-id="0cd43-202">Pode referenciar várias tabelas da base de dados de Olá referenciada pelo conjunto de dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="0cd43-203">Se não for especificado, Olá instrução de SQL que é executada: selecione a partir de MyTable.</span><span class="sxs-lookup"><span data-stu-id="0cd43-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="0cd43-204">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-204">No</span></span> |
| <span data-ttu-id="0cd43-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="0cd43-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="0cd43-206">Nome da Olá armazenado procedimento que lê dados a partir da tabela de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="0cd43-207">Nome do Olá procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-207">Name of hello stored procedure.</span></span> <span data-ttu-id="0cd43-208">Olá última instrução de SQL tem de ser uma instrução SELECT no procedimento de Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="0cd43-209">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-209">No</span></span> |
| <span data-ttu-id="0cd43-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="0cd43-210">storedProcedureParameters</span></span> |<span data-ttu-id="0cd43-211">Parâmetros para Olá procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="0cd43-212">Pares nome/valor.</span><span class="sxs-lookup"><span data-stu-id="0cd43-212">Name/value pairs.</span></span> <span data-ttu-id="0cd43-213">Nomes e maiúsculas e minúsculas de parâmetros têm de corresponder nomes Olá e maiúsculas e minúsculas de parâmetros de procedimento armazenado de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="0cd43-214">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-214">No</span></span> |

<span data-ttu-id="0cd43-215">Se hello **sqlReaderQuery** especificado para Olá SqlSource, hello atividade de cópia executa esta consulta contra Olá base de dados do SQL Server origem tooget Olá de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="0cd43-216">Em alternativa, pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado recebe parâmetros).</span><span class="sxs-lookup"><span data-stu-id="0cd43-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="0cd43-217">Se não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas Olá definidas na secção de estrutura de Olá são utilizado toobuild toorun uma consulta select contra Olá base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cd43-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="0cd43-218">Se a definição do conjunto de dados de Olá não tem uma estrutura de Olá, todas as colunas são selecionadas da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="0cd43-219">Quando utiliza **sqlReaderStoredProcedureName**, terá ainda de toospecify um valor para Olá **tableName** propriedade no conjunto de dados Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="0cd43-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="0cd43-220">Não existem nenhum validações executadas apesar desta tabela.</span><span class="sxs-lookup"><span data-stu-id="0cd43-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="0cd43-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="0cd43-221">SqlSink</span></span>
<span data-ttu-id="0cd43-222">**SqlSink** suporta Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="0cd43-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="0cd43-223">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0cd43-223">Property</span></span> | <span data-ttu-id="0cd43-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cd43-224">Description</span></span> | <span data-ttu-id="0cd43-225">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0cd43-225">Allowed values</span></span> | <span data-ttu-id="0cd43-226">Necessário</span><span class="sxs-lookup"><span data-stu-id="0cd43-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0cd43-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0cd43-227">writeBatchTimeout</span></span> |<span data-ttu-id="0cd43-228">De tempo de espera para toocomplete de operação de inserção de lote Olá antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="0cd43-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="0cd43-229">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0cd43-229">timespan</span></span><br/><br/> <span data-ttu-id="0cd43-230">Exemplo: "00: 30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="0cd43-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="0cd43-231">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-231">No</span></span> |
| <span data-ttu-id="0cd43-232">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="0cd43-232">writeBatchSize</span></span> |<span data-ttu-id="0cd43-233">Insere dados na tabela SQL Olá quando o tamanho de memória intermédia de Olá atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="0cd43-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="0cd43-234">Número inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="0cd43-234">Integer (number of rows)</span></span> |<span data-ttu-id="0cd43-235">Não (predefinição: 10000)</span><span class="sxs-lookup"><span data-stu-id="0cd43-235">No (default: 10000)</span></span> |
| <span data-ttu-id="0cd43-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="0cd43-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="0cd43-237">Especifique a consulta para a atividade de cópia tooexecute, de modo a que os dados de um setor específico é limpa.</span><span class="sxs-lookup"><span data-stu-id="0cd43-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="0cd43-238">Para obter mais informações, consulte [cópia repetíveis](#repeatable-copy) secção.</span><span class="sxs-lookup"><span data-stu-id="0cd43-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="0cd43-239">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="0cd43-239">A query statement.</span></span> |<span data-ttu-id="0cd43-240">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-240">No</span></span> |
| <span data-ttu-id="0cd43-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="0cd43-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="0cd43-242">Especifique o nome de coluna para toofill de atividade de cópia com o identificador de setor automaticamente gerado, que é utilizado tooclean dos dados de um setor específico quando voltar a executar.</span><span class="sxs-lookup"><span data-stu-id="0cd43-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="0cd43-243">Para obter mais informações, consulte [cópia repetíveis](#repeatable-copy) secção.</span><span class="sxs-lookup"><span data-stu-id="0cd43-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="0cd43-244">Nome da coluna de uma coluna com o tipo de dados de binary(32).</span><span class="sxs-lookup"><span data-stu-id="0cd43-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="0cd43-245">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-245">No</span></span> |
| <span data-ttu-id="0cd43-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="0cd43-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="0cd43-247">Nome do Olá procedimento armazenado dados upserts (inserções/atualizações) na tabela de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="0cd43-248">Nome do Olá procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="0cd43-249">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-249">No</span></span> |
| <span data-ttu-id="0cd43-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="0cd43-250">storedProcedureParameters</span></span> |<span data-ttu-id="0cd43-251">Parâmetros para Olá procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="0cd43-252">Pares nome/valor.</span><span class="sxs-lookup"><span data-stu-id="0cd43-252">Name/value pairs.</span></span> <span data-ttu-id="0cd43-253">Nomes e maiúsculas e minúsculas de parâmetros têm de corresponder nomes Olá e maiúsculas e minúsculas de parâmetros de procedimento armazenado de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="0cd43-254">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-254">No</span></span> |
| <span data-ttu-id="0cd43-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="0cd43-255">sqlWriterTableType</span></span> |<span data-ttu-id="0cd43-256">Especifique toobe de nome de tipo de tabela utilizado no procedimento de Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="0cd43-257">Atividade de cópia disponibiliza uma dados Olá a ser movidos numa tabela temporária com este tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="0cd43-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="0cd43-258">Código do procedimento armazenado, em seguida, pode intercalar dados de Olá a ser copiados com dados existentes.</span><span class="sxs-lookup"><span data-stu-id="0cd43-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="0cd43-259">Um nome de tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="0cd43-259">A table type name.</span></span> |<span data-ttu-id="0cd43-260">Não</span><span class="sxs-lookup"><span data-stu-id="0cd43-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="0cd43-261">Exemplos JSON para copiar dados e tooSQL servidor</span><span class="sxs-lookup"><span data-stu-id="0cd43-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="0cd43-262">Olá exemplos seguintes fornecem definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0cd43-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0cd43-263">Olá, os seguintes exemplos mostram como toocopy tooand de dados do SQL Server e o armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd43-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="0cd43-264">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das origens tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0cd43-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="0cd43-265">Exemplo: Copiar dados do SQL Server tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="0cd43-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="0cd43-266">Olá seguinte exemplo mostra:</span><span class="sxs-lookup"><span data-stu-id="0cd43-266">hello following sample shows:</span></span>

1. <span data-ttu-id="0cd43-267">Um serviço ligado do tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="0cd43-268">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0cd43-269">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="0cd43-270">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0cd43-271">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0cd43-272">exemplo de Olá copia dados de séries de tempo de um tooan de tabela do SQL Server BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0cd43-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="0cd43-273">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="0cd43-274">Como primeiro passo, o programa de configuração Olá o data management gateway.</span><span class="sxs-lookup"><span data-stu-id="0cd43-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="0cd43-275">instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0cd43-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="0cd43-276">**Serviço ligado do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0cd43-276">**SQL Server linked service**</span></span>
```json
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
<span data-ttu-id="0cd43-277">**Serviço de ligado do armazenamento de Blobs do Azure**</span><span class="sxs-lookup"><span data-stu-id="0cd43-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="0cd43-278">**Conjunto de dados de entrada do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0cd43-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="0cd43-279">exemplo de Olá pressupõe que criou uma tabela "MyTable" no SQL Server e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="0cd43-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="0cd43-280">Pode consultar através de várias tabelas na Olá mesma base de dados com um único conjunto de dados, mas uma única tabela tem de ser utilizado para typeProperty tableName de Olá conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="0cd43-281">A definição "external": "true" informa serviço Data Factory esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "SqlServerInput",
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
<span data-ttu-id="0cd43-282">**Conjunto de dados de saída de Blobs do Azure**</span><span class="sxs-lookup"><span data-stu-id="0cd43-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="0cd43-283">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="0cd43-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0cd43-284">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="0cd43-285">caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="0cd43-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
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
<span data-ttu-id="0cd43-286">**Pipeline com atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="0cd43-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="0cd43-287">pipeline de Olá contém uma atividade de cópia que está configurado toouse estes conjuntos de dados de entrada e de saída e toorun agendada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0cd43-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="0cd43-288">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**SqlSource** e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="0cd43-289">consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá passado toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="0cd43-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
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
<span data-ttu-id="0cd43-290">Neste exemplo, **sqlReaderQuery** especificado para Olá SqlSource.</span><span class="sxs-lookup"><span data-stu-id="0cd43-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="0cd43-291">Olá atividade de cópia executa esta consulta contra Olá base de dados do SQL Server origem tooget Olá de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="0cd43-292">Em alternativa, pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado recebe parâmetros).</span><span class="sxs-lookup"><span data-stu-id="0cd43-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="0cd43-293">Olá sqlReaderQuery pode fazer referência a várias tabelas na base de dados de Olá referenciada pelo conjunto de dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="0cd43-294">Não é limitado tooonly tabela de Olá definida como Olá typeProperty tableName de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="0cd43-295">Se não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas Olá definidas na secção de estrutura de Olá são utilizado toobuild toorun uma consulta select contra Olá base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cd43-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="0cd43-296">Se a definição do conjunto de dados de Olá não tem uma estrutura de Olá, todas as colunas são selecionadas da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="0cd43-297">Consulte Olá [origem Sql](#sqlsource) secção e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para Olá obter lista de propriedades suportadas por SqlSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="0cd43-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="0cd43-298">Exemplo: Copiar dados de Blobs do Azure tooSQL servidor</span><span class="sxs-lookup"><span data-stu-id="0cd43-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="0cd43-299">Olá seguinte exemplo mostra:</span><span class="sxs-lookup"><span data-stu-id="0cd43-299">hello following sample shows:</span></span>

1. <span data-ttu-id="0cd43-300">serviço do tipo de ligado a Olá [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="0cd43-301">serviço do tipo de ligado a Olá [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0cd43-302">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="0cd43-303">Uma saída [dataset](data-factory-create-datasets.md) do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0cd43-304">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="0cd43-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="0cd43-305">exemplo de Olá copia dados de séries de tempo de uma tabela de SQL Server do blob do Azure tooa a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0cd43-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="0cd43-306">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="0cd43-307">**Serviço ligado do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0cd43-307">**SQL Server linked service**</span></span>

```json
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
<span data-ttu-id="0cd43-308">**Serviço de ligado do armazenamento de Blobs do Azure**</span><span class="sxs-lookup"><span data-stu-id="0cd43-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="0cd43-309">**Conjunto de dados de entrada Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="0cd43-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="0cd43-310">Dados são captados um blob de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="0cd43-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0cd43-311">Olá pasta caminho e nome de ficheiro para o blob Olá dinamicamente são avaliados com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="0cd43-312">caminho da pasta Olá utiliza ano, mês e parte de dia da hora de início de Olá e nome de ficheiro utiliza a parte de hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="0cd43-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="0cd43-313">"external": "true" definição informa o serviço do Data Factory Olá, esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
<span data-ttu-id="0cd43-314">**Conjunto de dados de saída de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0cd43-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="0cd43-315">exemplo de Olá copia a tabela de tooa de dados com o nome "MyTable" no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cd43-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="0cd43-316">Criar tabela Olá no SQL Server com Olá o mesmo número de colunas como esperado Olá Blob CSV ficheiro toocontain.</span><span class="sxs-lookup"><span data-stu-id="0cd43-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="0cd43-317">Novas linhas são adicionadas toohello tabela cada hora.</span><span class="sxs-lookup"><span data-stu-id="0cd43-317">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
<span data-ttu-id="0cd43-318">**Pipeline com atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="0cd43-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="0cd43-319">pipeline de Olá contém uma atividade de cópia que está configurado toouse estes conjuntos de dados de entrada e de saída e toorun agendada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0cd43-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="0cd43-320">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**BlobSource** e **sink** tipo está definido demasiado**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="0cd43-321">Resolução de problemas de ligação</span><span class="sxs-lookup"><span data-stu-id="0cd43-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="0cd43-322">Configure as ligações remotas de tooaccept do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cd43-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="0cd43-323">Iniciar **SQL Server Management Studio**, faça duplo clique **servidor**e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="0cd43-324">Selecione **ligações** partir da lista de Olá e verificação **servidor do permitir ligações remotas toohello**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![Ativar ligações remotas](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="0cd43-326">Consulte [configurar o acesso remoto de Olá opção de configuração do servidor](https://msdn.microsoft.com/library/ms191464.aspx) para obter passos detalhados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="0cd43-327">Iniciar **Gestor de configuração do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="0cd43-328">Expanda **configuração de rede do SQL Server** para Olá instância pretende e selecione **protocolos para MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="0cd43-329">Deverá ver protocolos no painel direito Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="0cd43-330">Ative TCP/IP clicando **TCP/IP** e clicando em **ativar**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Ative TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="0cd43-332">Consulte [ativar ou desativar um protocolo de rede do servidor](https://msdn.microsoft.com/library/ms191294.aspx) para obter detalhes e alternativas formas de ativar o protocolo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="0cd43-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="0cd43-333">Na mesma janela de Olá, faça duplo clique **TCP/IP** toolaunch **propriedades de TCP/IP** janela.</span><span class="sxs-lookup"><span data-stu-id="0cd43-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="0cd43-334">Comutador toohello **endereços IP** separador. Desloque para baixo toosee **IPAll** secção.</span><span class="sxs-lookup"><span data-stu-id="0cd43-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="0cd43-335">Tome nota dos Olá * * a porta TCP * * (predefinição é **1433**).</span><span class="sxs-lookup"><span data-stu-id="0cd43-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="0cd43-336">Criar um **regra de Firewall do Windows de Olá** no Olá máquina tooallow tráfego de entrada através desta porta.</span><span class="sxs-lookup"><span data-stu-id="0cd43-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="0cd43-337">**Verificar ligação**: tooconnect toohello SQL Server com o nome completamente qualificado, utilize o SQL Server Management Studio de um computador diferente.</span><span class="sxs-lookup"><span data-stu-id="0cd43-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="0cd43-338">Por exemplo: "<machine>.<domain>. Corp.<company>empresa>.com, 1433. "</span><span class="sxs-lookup"><span data-stu-id="0cd43-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="0cd43-339">Consulte [mover dados entre origens no local e nuvem de Olá com o Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obter informações detalhadas.</span><span class="sxs-lookup"><span data-stu-id="0cd43-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="0cd43-340">Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.</span><span class="sxs-lookup"><span data-stu-id="0cd43-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="0cd43-341">Colunas de identidade na base de dados de destino de Olá</span><span class="sxs-lookup"><span data-stu-id="0cd43-341">Identity columns in hello target database</span></span>
<span data-ttu-id="0cd43-342">Esta secção fornece um exemplo que copia dados a partir de uma tabela de origem com a tabela de destino não identidade coluna tooa com uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="0cd43-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="0cd43-343">**Tabela de origem:**</span><span class="sxs-lookup"><span data-stu-id="0cd43-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="0cd43-344">**Tabela de destino:**</span><span class="sxs-lookup"><span data-stu-id="0cd43-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="0cd43-345">Tenha em atenção de que a tabela de destino que Olá tem uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="0cd43-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="0cd43-346">**Definição de JSON do conjunto de dados de origem**</span><span class="sxs-lookup"><span data-stu-id="0cd43-346">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="0cd43-347">**Definição de JSON do conjunto de dados de destino**</span><span class="sxs-lookup"><span data-stu-id="0cd43-347">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="0cd43-348">Tenha em atenção que, como a tabela de origem e destino têm esquemas diferentes (o destino tem uma coluna adicional com a identidade).</span><span class="sxs-lookup"><span data-stu-id="0cd43-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="0cd43-349">Neste cenário, terá de toospecify **estrutura** propriedade na definição do conjunto de dados de Olá destino, que não inclui a coluna de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd43-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="0cd43-350">Invocar um procedimento armazenado do sink do SQL Server</span><span class="sxs-lookup"><span data-stu-id="0cd43-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="0cd43-351">Consulte [invocar um procedimento armazenado para sink do SQL Server na atividade de cópia](data-factory-invoke-stored-procedure-from-copy-activity.md) artigo para obter um exemplo de invocar um procedimento armazenado do sink do SQL Server numa atividade de cópia de um pipeline.</span><span class="sxs-lookup"><span data-stu-id="0cd43-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="0cd43-352">Mapeamento de tipos para o SQL server</span><span class="sxs-lookup"><span data-stu-id="0cd43-352">Type mapping for SQL server</span></span>
<span data-ttu-id="0cd43-353">Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, Olá atividade de cópia executa conversões de tipo automática dos tipos de toosink de tipos de origem com Olá seguir abordagem de passo 2:</span><span class="sxs-lookup"><span data-stu-id="0cd43-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="0cd43-354">Converter do tipo de too.NET de tipos de origem nativo</span><span class="sxs-lookup"><span data-stu-id="0cd43-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="0cd43-355">Converter do tipo de sink de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="0cd43-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="0cd43-356">Quando mover dados demasiado & do SQL server, Olá mapeamentos seguintes são utilizados do tipo de too.NET do tipo SQL e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="0cd43-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="0cd43-357">o mapeamento de Olá é igual ao hello mapeamento do tipo de dados do SQL Server para ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="0cd43-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="0cd43-358">Tipo de motor de base de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="0cd43-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="0cd43-359">Tipo de .NET framework</span><span class="sxs-lookup"><span data-stu-id="0cd43-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="0cd43-360">bigint</span><span class="sxs-lookup"><span data-stu-id="0cd43-360">bigint</span></span> |<span data-ttu-id="0cd43-361">Int64</span><span class="sxs-lookup"><span data-stu-id="0cd43-361">Int64</span></span> |
| <span data-ttu-id="0cd43-362">Binário</span><span class="sxs-lookup"><span data-stu-id="0cd43-362">binary</span></span> |<span data-ttu-id="0cd43-363">Byte]</span><span class="sxs-lookup"><span data-stu-id="0cd43-363">Byte[]</span></span> |
| <span data-ttu-id="0cd43-364">bits</span><span class="sxs-lookup"><span data-stu-id="0cd43-364">bit</span></span> |<span data-ttu-id="0cd43-365">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="0cd43-365">Boolean</span></span> |
| <span data-ttu-id="0cd43-366">char</span><span class="sxs-lookup"><span data-stu-id="0cd43-366">char</span></span> |<span data-ttu-id="0cd43-367">Cadeia, Char []</span><span class="sxs-lookup"><span data-stu-id="0cd43-367">String, Char[]</span></span> |
| <span data-ttu-id="0cd43-368">Data</span><span class="sxs-lookup"><span data-stu-id="0cd43-368">date</span></span> |<span data-ttu-id="0cd43-369">DateTime</span><span class="sxs-lookup"><span data-stu-id="0cd43-369">DateTime</span></span> |
| <span data-ttu-id="0cd43-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="0cd43-370">Datetime</span></span> |<span data-ttu-id="0cd43-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="0cd43-371">DateTime</span></span> |
| <span data-ttu-id="0cd43-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="0cd43-372">datetime2</span></span> |<span data-ttu-id="0cd43-373">DateTime</span><span class="sxs-lookup"><span data-stu-id="0cd43-373">DateTime</span></span> |
| <span data-ttu-id="0cd43-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="0cd43-374">Datetimeoffset</span></span> |<span data-ttu-id="0cd43-375">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="0cd43-375">DateTimeOffset</span></span> |
| <span data-ttu-id="0cd43-376">Decimal</span><span class="sxs-lookup"><span data-stu-id="0cd43-376">Decimal</span></span> |<span data-ttu-id="0cd43-377">Decimal</span><span class="sxs-lookup"><span data-stu-id="0cd43-377">Decimal</span></span> |
| <span data-ttu-id="0cd43-378">Atributo FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="0cd43-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="0cd43-379">Byte]</span><span class="sxs-lookup"><span data-stu-id="0cd43-379">Byte[]</span></span> |
| <span data-ttu-id="0cd43-380">Número de vírgula flutuante</span><span class="sxs-lookup"><span data-stu-id="0cd43-380">Float</span></span> |<span data-ttu-id="0cd43-381">duplo</span><span class="sxs-lookup"><span data-stu-id="0cd43-381">Double</span></span> |
| <span data-ttu-id="0cd43-382">Imagem</span><span class="sxs-lookup"><span data-stu-id="0cd43-382">image</span></span> |<span data-ttu-id="0cd43-383">Byte]</span><span class="sxs-lookup"><span data-stu-id="0cd43-383">Byte[]</span></span> |
| <span data-ttu-id="0cd43-384">Int</span><span class="sxs-lookup"><span data-stu-id="0cd43-384">int</span></span> |<span data-ttu-id="0cd43-385">Int32</span><span class="sxs-lookup"><span data-stu-id="0cd43-385">Int32</span></span> |
| <span data-ttu-id="0cd43-386">dinheiro</span><span class="sxs-lookup"><span data-stu-id="0cd43-386">money</span></span> |<span data-ttu-id="0cd43-387">Decimal</span><span class="sxs-lookup"><span data-stu-id="0cd43-387">Decimal</span></span> |
| <span data-ttu-id="0cd43-388">nchar</span><span class="sxs-lookup"><span data-stu-id="0cd43-388">nchar</span></span> |<span data-ttu-id="0cd43-389">Cadeia, Char []</span><span class="sxs-lookup"><span data-stu-id="0cd43-389">String, Char[]</span></span> |
| <span data-ttu-id="0cd43-390">ntext</span><span class="sxs-lookup"><span data-stu-id="0cd43-390">ntext</span></span> |<span data-ttu-id="0cd43-391">Cadeia, Char []</span><span class="sxs-lookup"><span data-stu-id="0cd43-391">String, Char[]</span></span> |
| <span data-ttu-id="0cd43-392">um valor numérico</span><span class="sxs-lookup"><span data-stu-id="0cd43-392">numeric</span></span> |<span data-ttu-id="0cd43-393">Decimal</span><span class="sxs-lookup"><span data-stu-id="0cd43-393">Decimal</span></span> |
| <span data-ttu-id="0cd43-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="0cd43-394">nvarchar</span></span> |<span data-ttu-id="0cd43-395">Cadeia, Char []</span><span class="sxs-lookup"><span data-stu-id="0cd43-395">String, Char[]</span></span> |
| <span data-ttu-id="0cd43-396">real</span><span class="sxs-lookup"><span data-stu-id="0cd43-396">real</span></span> |<span data-ttu-id="0cd43-397">Único</span><span class="sxs-lookup"><span data-stu-id="0cd43-397">Single</span></span> |
| <span data-ttu-id="0cd43-398">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="0cd43-398">rowversion</span></span> |<span data-ttu-id="0cd43-399">Byte]</span><span class="sxs-lookup"><span data-stu-id="0cd43-399">Byte[]</span></span> |
| <span data-ttu-id="0cd43-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="0cd43-400">smalldatetime</span></span> |<span data-ttu-id="0cd43-401">DateTime</span><span class="sxs-lookup"><span data-stu-id="0cd43-401">DateTime</span></span> |
| <span data-ttu-id="0cd43-402">smallint</span><span class="sxs-lookup"><span data-stu-id="0cd43-402">smallint</span></span> |<span data-ttu-id="0cd43-403">Int16</span><span class="sxs-lookup"><span data-stu-id="0cd43-403">Int16</span></span> |
| <span data-ttu-id="0cd43-404">em smallmoney</span><span class="sxs-lookup"><span data-stu-id="0cd43-404">smallmoney</span></span> |<span data-ttu-id="0cd43-405">Decimal</span><span class="sxs-lookup"><span data-stu-id="0cd43-405">Decimal</span></span> |
| <span data-ttu-id="0cd43-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="0cd43-406">sql_variant</span></span> |<span data-ttu-id="0cd43-407">Objeto *</span><span class="sxs-lookup"><span data-stu-id="0cd43-407">Object *</span></span> |
| <span data-ttu-id="0cd43-408">Texto</span><span class="sxs-lookup"><span data-stu-id="0cd43-408">text</span></span> |<span data-ttu-id="0cd43-409">Cadeia, Char []</span><span class="sxs-lookup"><span data-stu-id="0cd43-409">String, Char[]</span></span> |
| <span data-ttu-id="0cd43-410">hora</span><span class="sxs-lookup"><span data-stu-id="0cd43-410">time</span></span> |<span data-ttu-id="0cd43-411">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0cd43-411">TimeSpan</span></span> |
| <span data-ttu-id="0cd43-412">carimbo de data/hora</span><span class="sxs-lookup"><span data-stu-id="0cd43-412">timestamp</span></span> |<span data-ttu-id="0cd43-413">Byte]</span><span class="sxs-lookup"><span data-stu-id="0cd43-413">Byte[]</span></span> |
| <span data-ttu-id="0cd43-414">tinyint</span><span class="sxs-lookup"><span data-stu-id="0cd43-414">tinyint</span></span> |<span data-ttu-id="0cd43-415">Bytes</span><span class="sxs-lookup"><span data-stu-id="0cd43-415">Byte</span></span> |
| <span data-ttu-id="0cd43-416">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="0cd43-416">uniqueidentifier</span></span> |<span data-ttu-id="0cd43-417">GUID</span><span class="sxs-lookup"><span data-stu-id="0cd43-417">Guid</span></span> |
| <span data-ttu-id="0cd43-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="0cd43-418">varbinary</span></span> |<span data-ttu-id="0cd43-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="0cd43-419">Byte[]</span></span> |
| <span data-ttu-id="0cd43-420">varchar</span><span class="sxs-lookup"><span data-stu-id="0cd43-420">varchar</span></span> |<span data-ttu-id="0cd43-421">Cadeia, Char []</span><span class="sxs-lookup"><span data-stu-id="0cd43-421">String, Char[]</span></span> |
| <span data-ttu-id="0cd43-422">xml</span><span class="sxs-lookup"><span data-stu-id="0cd43-422">xml</span></span> |<span data-ttu-id="0cd43-423">XML</span><span class="sxs-lookup"><span data-stu-id="0cd43-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="0cd43-424">Mapeamento de colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="0cd43-424">Mapping source toosink columns</span></span>
<span data-ttu-id="0cd43-425">colunas de toomap toocolumns de conjunto de dados de origem do conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="0cd43-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="0cd43-426">Cópia repetíveis</span><span class="sxs-lookup"><span data-stu-id="0cd43-426">Repeatable copy</span></span>
<span data-ttu-id="0cd43-427">Quando copiar dados tooSQL base de dados do servidor, a atividade de cópia de Olá acrescenta tabela do sink de toohello de dados por predefinição.</span><span class="sxs-lookup"><span data-stu-id="0cd43-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="0cd43-428">em vez disso, consulte tooperform um UPSERT [escrita repetíveis tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artigo.</span><span class="sxs-lookup"><span data-stu-id="0cd43-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="0cd43-429">Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="0cd43-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="0cd43-430">No Azure Data Factory, pode voltar a executar um setor manualmente.</span><span class="sxs-lookup"><span data-stu-id="0cd43-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="0cd43-431">Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="0cd43-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="0cd43-432">Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado.</span><span class="sxs-lookup"><span data-stu-id="0cd43-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="0cd43-433">Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="0cd43-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0cd43-434">Desempenho e a otimização</span><span class="sxs-lookup"><span data-stu-id="0cd43-434">Performance and Tuning</span></span>
<span data-ttu-id="0cd43-435">Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.</span><span class="sxs-lookup"><span data-stu-id="0cd43-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
