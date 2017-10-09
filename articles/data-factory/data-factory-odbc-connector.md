---
title: dados de aaaMove de arquivos de dados ODBC | Microsoft Docs
description: Saiba mais sobre como dados de toomove dos dados ODBC armazena utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="d5bb5-103">Mover dados de ODBC os arquivos de dados utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5bb5-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="d5bb5-104">Este artigo explica como armazenar toouse Olá atividade de cópia de dados de toomove do Azure Data Factory de dados ODBC no local.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="d5bb5-105">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="d5bb5-106">Pode copiar dados de um arquivo de dados do ODBC dados arquivo tooany suportado sink.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="d5bb5-107">Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d5bb5-108">Fábrica de dados atualmente suporta apenas mover tooother arquivos de dados de arquivo de dados de dados de ODBC, mas não para mover dados do arquivo de dados ODBC outros dados arquivos tooan.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="d5bb5-109">Ativar a conectividade</span><span class="sxs-lookup"><span data-stu-id="d5bb5-109">Enabling connectivity</span></span>
<span data-ttu-id="d5bb5-110">Serviço de fábrica de dados suporta origens ODBC tooon local ao ligar utilizando Olá Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="d5bb5-111">Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Data Management Gateway e instruções passo a passo sobre como configurar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="d5bb5-112">Utilize o arquivo de dados ODBC tooconnect tooan Olá gateway mesmo esteja alojado numa VM do IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="d5bb5-113">Pode instalar o gateway de Olá num Olá mesmo no local do computador ou Olá VM do Azure como arquivo de dados ODBC Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="d5bb5-114">No entanto, recomendamos que instale o gateway de Olá num máquina/Azure separado IaaS VM tooavoid contenção de recursos e para um melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="d5bb5-115">Quando instalar o gateway de Olá num computador separado, máquina Olá deve ser capaz de tooaccess máquina de Olá com o arquivo de dados ODBC Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="d5bb5-116">Para além dos Olá Data Management Gateway, tem também o controlador ODBC do tooinstall Olá Olá arquivo de dados no computador do gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="d5bb5-117">Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d5bb5-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="d5bb5-118">Getting started</span></span>
<span data-ttu-id="d5bb5-119">Pode criar um pipeline com uma atividade de cópia move os dados de um arquivo de dados ODBC utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="d5bb5-120">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d5bb5-121">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="d5bb5-122">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d5bb5-123">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d5bb5-124">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="d5bb5-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="d5bb5-125">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="d5bb5-126">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="d5bb5-127">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d5bb5-128">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d5bb5-129">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="d5bb5-130">Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de um arquivo de dados ODBC, consulte [exemplo JSON: arquivo de dados de cópia de dados de ODBC tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d5bb5-131">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são o arquivo de dados do toodefine utilizados Data Factory entidades tooODBC específico:</span><span class="sxs-lookup"><span data-stu-id="d5bb5-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d5bb5-132">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="d5bb5-132">Linked service properties</span></span>
<span data-ttu-id="d5bb5-133">Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooODBC ligado.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="d5bb5-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d5bb5-134">Property</span></span> | <span data-ttu-id="d5bb5-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="d5bb5-135">Description</span></span> | <span data-ttu-id="d5bb5-136">Necessário</span><span class="sxs-lookup"><span data-stu-id="d5bb5-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5bb5-137">tipo</span><span class="sxs-lookup"><span data-stu-id="d5bb5-137">type</span></span> |<span data-ttu-id="d5bb5-138">a propriedade de tipo Olá tem de ser definida: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="d5bb5-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="d5bb5-139">Sim</span><span class="sxs-lookup"><span data-stu-id="d5bb5-139">Yes</span></span> |
| <span data-ttu-id="d5bb5-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="d5bb5-140">connectionString</span></span> |<span data-ttu-id="d5bb5-141">parte de credencial de acesso não de Olá da cadeia de ligação de Olá e opcional encriptada credencial.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="d5bb5-142">Veja exemplos na Olá seguintes secções:</span><span class="sxs-lookup"><span data-stu-id="d5bb5-142">See examples in hello following sections.</span></span> |<span data-ttu-id="d5bb5-143">Sim</span><span class="sxs-lookup"><span data-stu-id="d5bb5-143">Yes</span></span> |
| <span data-ttu-id="d5bb5-144">credencial</span><span class="sxs-lookup"><span data-stu-id="d5bb5-144">credential</span></span> |<span data-ttu-id="d5bb5-145">parte de credencial de acesso de Olá Olá da cadeia de ligação especificada no formato do valor da propriedade do controlador específico.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="d5bb5-146">Exemplo: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; ".</span><span class="sxs-lookup"><span data-stu-id="d5bb5-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="d5bb5-147">Não</span><span class="sxs-lookup"><span data-stu-id="d5bb5-147">No</span></span> |
| <span data-ttu-id="d5bb5-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d5bb5-148">authenticationType</span></span> |<span data-ttu-id="d5bb5-149">Tipo de autenticação utilizado tooconnect toohello arquivo de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="d5bb5-150">Os valores possíveis são: básico e anónimos.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="d5bb5-151">Sim</span><span class="sxs-lookup"><span data-stu-id="d5bb5-151">Yes</span></span> |
| <span data-ttu-id="d5bb5-152">o nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="d5bb5-152">username</span></span> |<span data-ttu-id="d5bb5-153">Especifique o nome de utilizador se estiver a utilizar autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="d5bb5-154">Não</span><span class="sxs-lookup"><span data-stu-id="d5bb5-154">No</span></span> |
| <span data-ttu-id="d5bb5-155">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="d5bb5-155">password</span></span> |<span data-ttu-id="d5bb5-156">Especifique a palavra-passe da conta de utilizador de Olá especificado para nome de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d5bb5-157">Não</span><span class="sxs-lookup"><span data-stu-id="d5bb5-157">No</span></span> |
| <span data-ttu-id="d5bb5-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d5bb5-158">gatewayName</span></span> |<span data-ttu-id="d5bb5-159">Nome do gateway de Olá que Olá serviço Data Factory deve utilizar o arquivo de dados ODBC do tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="d5bb5-160">Sim</span><span class="sxs-lookup"><span data-stu-id="d5bb5-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="d5bb5-161">Utilizar a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="d5bb5-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="d5bb5-162">Utilizar a autenticação básica com credenciais encriptado</span><span class="sxs-lookup"><span data-stu-id="d5bb5-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="d5bb5-163">Pode encriptar as credenciais de Olá utilizando Olá [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versão do Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 ou anterior versão da Olá O Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="d5bb5-164">Autenticação anónima</span><span class="sxs-lookup"><span data-stu-id="d5bb5-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="d5bb5-165">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="d5bb5-165">Dataset properties</span></span>
<span data-ttu-id="d5bb5-166">Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d5bb5-167">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d5bb5-168">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="d5bb5-169">Olá typeProperties secção para o conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados ODBC) tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="d5bb5-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="d5bb5-170">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d5bb5-170">Property</span></span> | <span data-ttu-id="d5bb5-171">Descrição</span><span class="sxs-lookup"><span data-stu-id="d5bb5-171">Description</span></span> | <span data-ttu-id="d5bb5-172">Necessário</span><span class="sxs-lookup"><span data-stu-id="d5bb5-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5bb5-173">tableName</span><span class="sxs-lookup"><span data-stu-id="d5bb5-173">tableName</span></span> |<span data-ttu-id="d5bb5-174">Nome da tabela de Olá no arquivo de dados ODBC Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="d5bb5-175">Sim</span><span class="sxs-lookup"><span data-stu-id="d5bb5-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d5bb5-176">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="d5bb5-176">Copy activity properties</span></span>
<span data-ttu-id="d5bb5-177">Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d5bb5-178">Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="d5bb5-179">Propriedades disponíveis nos Olá **typeProperties** secção de atividades de Olá em Olá por outro lado variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="d5bb5-180">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="d5bb5-181">Na atividade de cópia, quando a origem é do tipo **RelationalSource** (que inclui ODBC), na secção typeProperties, estão disponível Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="d5bb5-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d5bb5-182">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d5bb5-182">Property</span></span> | <span data-ttu-id="d5bb5-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="d5bb5-183">Description</span></span> | <span data-ttu-id="d5bb5-184">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="d5bb5-184">Allowed values</span></span> | <span data-ttu-id="d5bb5-185">Necessário</span><span class="sxs-lookup"><span data-stu-id="d5bb5-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5bb5-186">consulta</span><span class="sxs-lookup"><span data-stu-id="d5bb5-186">query</span></span> |<span data-ttu-id="d5bb5-187">Utilize Olá consulta personalizada tooread dados.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d5bb5-188">Cadeia de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-188">SQL query string.</span></span> <span data-ttu-id="d5bb5-189">Por exemplo: selecionar * de MyTable.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="d5bb5-190">Sim</span><span class="sxs-lookup"><span data-stu-id="d5bb5-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="d5bb5-191">Exemplo JSON: arquivo de dados de cópia de dados de ODBC tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="d5bb5-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="d5bb5-192">Neste exemplo fornece definições de JSON que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d5bb5-193">Mostra como tooan Blob Storage do Azure da origem de dados de toocopy de um ODBC.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="d5bb5-194">No entanto, os dados podem ser copiado tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="d5bb5-195">exemplo de Olá tem Olá seguintes entidades da fábrica de dados:</span><span class="sxs-lookup"><span data-stu-id="d5bb5-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="d5bb5-196">Um serviço ligado do tipo [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="d5bb5-197">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d5bb5-198">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="d5bb5-199">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d5bb5-200">A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d5bb5-201">exemplo de Olá copia dados a partir num resultado de consulta um blob de tooa do arquivo de dados ODBC a cada hora.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="d5bb5-202">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d5bb5-203">Como primeiro passo, configure Olá o data management gateway.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="d5bb5-204">instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="d5bb5-205">**Serviço ligado de ODBC** este exemplo utiliza Olá autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="d5bb5-206">Consulte [serviço ligado de ODBC](#linked-service-properties) secção para diferentes tipos de autenticação, pode utilizar.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="d5bb5-207">**Serviço ligado do Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="d5bb5-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="d5bb5-208">**Conjunto de dados de entrada de ODBC**</span><span class="sxs-lookup"><span data-stu-id="d5bb5-208">**ODBC input dataset**</span></span>

<span data-ttu-id="d5bb5-209">exemplo de Olá pressupõe que criou uma tabela "MyTable" numa base de dados ODBC e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="d5bb5-210">A definição "external": "true" informa serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

<span data-ttu-id="d5bb5-211">**Conjunto de dados de saída de Blobs do Azure**</span><span class="sxs-lookup"><span data-stu-id="d5bb5-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="d5bb5-212">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d5bb5-213">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d5bb5-214">caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="d5bb5-215">**Atividade de cópia de um pipeline com a origem ODBC (RelationalSource) e o sink de Blob (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="d5bb5-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="d5bb5-216">pipeline de Olá contém uma atividade de cópia que está configurado toouse estes conjuntos de dados de entrada e de saída e toorun agendada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d5bb5-217">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="d5bb5-218">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá passado toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
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
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="d5bb5-219">Mapeamento de tipos para ODBC</span><span class="sxs-lookup"><span data-stu-id="d5bb5-219">Type mapping for ODBC</span></span>
<span data-ttu-id="d5bb5-220">Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá abordagem de dois passos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5bb5-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="d5bb5-221">Converter do tipo de too.NET de tipos de origem nativo</span><span class="sxs-lookup"><span data-stu-id="d5bb5-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="d5bb5-222">Converter do tipo de sink de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="d5bb5-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="d5bb5-223">Quando mover dados de arquivos de dados ODBC, tipos de dados ODBC são tipos de too.NET mapeada tal como mencionado na Olá [mapeamentos de tipos de dados de ODBC](https://msdn.microsoft.com/library/cc668763.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="d5bb5-224">Mapear colunas toosink de origem</span><span class="sxs-lookup"><span data-stu-id="d5bb5-224">Map source toosink columns</span></span>
<span data-ttu-id="d5bb5-225">toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d5bb5-226">Repetíveis leitura a partir de origens relacionais</span><span class="sxs-lookup"><span data-stu-id="d5bb5-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="d5bb5-227">Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="d5bb5-228">No Azure Data Factory, pode voltar a executar um setor manualmente.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d5bb5-229">Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d5bb5-230">Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d5bb5-231">Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="d5bb5-232">Arquivo de GE Historian</span><span class="sxs-lookup"><span data-stu-id="d5bb5-232">GE Historian store</span></span>
<span data-ttu-id="d5bb5-233">Criar um toolink de serviço ligado de ODBC um [GE Proficy Historian (agora GE Historian)](http://www.geautomation.com/products/proficy-historian) tooan fábrica de dados do Azure do arquivo de dados conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="d5bb5-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="d5bb5-234">Instalar o Data Management Gateway numa máquina no local e registar o gateway de Olá com o portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="d5bb5-235">gateway de Olá instalado no seu computador no local utiliza o controlador ODBC Olá para GE Historian tooconnect toohello arquivo de dados de GE Historian.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="d5bb5-236">Por conseguinte, instale o controlador de Olá se não estiver já instalado no computador do gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="d5bb5-237">Consulte [ativar conectividade](#enabling-connectivity) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="d5bb5-238">Antes de utilizar Olá GE Historian armazenar numa solução de fábrica de dados, verifique se o gateway de Olá pode ligar toohello arquivo de dados com as instruções na secção seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="d5bb5-239">Artigo de Olá de leitura a partir do início de Olá para uma descrição geral detalhada da utilização de dados de ODBC armazena como arquivos de dados de origem de uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="d5bb5-240">Resolver problemas de conectividade</span><span class="sxs-lookup"><span data-stu-id="d5bb5-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="d5bb5-241">problemas de ligação de tootroubleshoot, utilize Olá **diagnóstico** separador de **Gestor de configuração do Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="d5bb5-242">Iniciar **Gestor de configuração do Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="d5bb5-243">Pode optar por executar "C:\Program Files\Microsoft Data gestão Gateway\1.0\Shared\ConfigManager.exe" diretamente (ou) pesquisa para **Gateway** toofind uma ligação demasiado**Microsoft Data Management Gateway** aplicação conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![Gateway de pesquisa](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="d5bb5-245">Comutador toohello **diagnóstico** separador.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-245">Switch toohello **Diagnostics** tab.</span></span>

    ![Diagnóstico do gateway](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="d5bb5-247">Selecione Olá **tipo** de dados armazenar (serviço ligado).</span><span class="sxs-lookup"><span data-stu-id="d5bb5-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="d5bb5-248">Especifique **autenticação** e introduza **credenciais** (ou) introduza **cadeia de ligação** que é o arquivo de dados de toohello tooconnect utilizados.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="d5bb5-249">Clique em **Testar ligação** o arquivo de dados do tootest Olá ligação toohello.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d5bb5-250">Desempenho e a otimização</span><span class="sxs-lookup"><span data-stu-id="d5bb5-250">Performance and Tuning</span></span>
<span data-ttu-id="d5bb5-251">Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.</span><span class="sxs-lookup"><span data-stu-id="d5bb5-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
