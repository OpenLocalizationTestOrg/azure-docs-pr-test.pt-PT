---
title: dados de aaaMove de origens de OData | Microsoft Docs
description: Saiba mais sobre como origens utilizando o Azure Data Factory de dados de toomove de OData.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="a2a4f-103">Mover dados de origem do OData utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a2a4f-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="a2a4f-104">Este artigo explica como toouse Olá atividade de cópia em dados do Azure Data Factory toomove a partir de uma origem de OData.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="a2a4f-105">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="a2a4f-106">Pode copiar dados de um arquivo de dados do OData origem tooany suportado sink.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="a2a4f-107">Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a2a4f-108">Fábrica de dados atualmente suporta apenas mover armazena os dados a partir de uma origem de OData tooother dados, mas não para mover dados de outros dados armazena tooan OData origem.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="a2a4f-109">Versões suportadas e tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="a2a4f-109">Supported versions and authentication types</span></span>
<span data-ttu-id="a2a4f-110">Este conector de OData suporta a versão de OData 3.0 e 4.0 e pode copiar dados a partir de ambos os cloud OData e origens de OData no local.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="a2a4f-111">Para Olá esta última opção, terá de tooinstall Olá Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="a2a4f-112">Consulte [mover dados entre no local e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter detalhes sobre o Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="a2a4f-113">Abaixo autenticação são suportados tipos:</span><span class="sxs-lookup"><span data-stu-id="a2a4f-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="a2a4f-114">tooaccess **nuvem** feed de OData, pode utilizar anónimo, básico (nome de utilizador e palavra-passe), ou do Azure Active Directory baseado em autenticação OAuth.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="a2a4f-115">tooaccess **no local** feed de OData, pode utilizar anónimo, básico (nome de utilizador e palavra-passe), ou a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a2a4f-116">Introdução</span><span class="sxs-lookup"><span data-stu-id="a2a4f-116">Getting started</span></span>
<span data-ttu-id="a2a4f-117">Pode criar um pipeline com uma atividade de cópia move dados a partir de uma origem de OData utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="a2a4f-118">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a2a4f-119">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="a2a4f-120">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a2a4f-121">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a2a4f-122">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="a2a4f-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="a2a4f-123">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a2a4f-124">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="a2a4f-125">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a2a4f-126">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a2a4f-127">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="a2a4f-128">Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de uma origem de OData, consulte [exemplo JSON: copiar dados de OData origem tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a2a4f-129">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades tooOData específico origem:</span><span class="sxs-lookup"><span data-stu-id="a2a4f-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a2a4f-130">Propriedades do serviço ligadas</span><span class="sxs-lookup"><span data-stu-id="a2a4f-130">Linked Service properties</span></span>
<span data-ttu-id="a2a4f-131">Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooOData ligado.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="a2a4f-132">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a2a4f-132">Property</span></span> | <span data-ttu-id="a2a4f-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="a2a4f-133">Description</span></span> | <span data-ttu-id="a2a4f-134">Necessário</span><span class="sxs-lookup"><span data-stu-id="a2a4f-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a2a4f-135">tipo</span><span class="sxs-lookup"><span data-stu-id="a2a4f-135">type</span></span> |<span data-ttu-id="a2a4f-136">a propriedade de tipo Olá tem de ser definida: **OData**</span><span class="sxs-lookup"><span data-stu-id="a2a4f-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="a2a4f-137">Sim</span><span class="sxs-lookup"><span data-stu-id="a2a4f-137">Yes</span></span> |
| <span data-ttu-id="a2a4f-138">URL</span><span class="sxs-lookup"><span data-stu-id="a2a4f-138">url</span></span> |<span data-ttu-id="a2a4f-139">URL de Olá serviço OData.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-139">Url of hello OData service.</span></span> |<span data-ttu-id="a2a4f-140">Sim</span><span class="sxs-lookup"><span data-stu-id="a2a4f-140">Yes</span></span> |
| <span data-ttu-id="a2a4f-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a2a4f-141">authenticationType</span></span> |<span data-ttu-id="a2a4f-142">Tipo de autenticação utilizado tooconnect toohello OData origem.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="a2a4f-143">Para a nuvem OData, os valores possíveis são anónimo, básico e OAuth (tenha em atenção o suporte do Azure Data Factory atualmente, apenas do Azure Active Directory com base em OAuth).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="a2a4f-144">De OData no local, os valores possíveis são anónimo, básico e Windows.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="a2a4f-145">Sim</span><span class="sxs-lookup"><span data-stu-id="a2a4f-145">Yes</span></span> |
| <span data-ttu-id="a2a4f-146">o nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="a2a4f-146">username</span></span> |<span data-ttu-id="a2a4f-147">Especifique o nome de utilizador se estiver a utilizar autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="a2a4f-148">Sim (apenas se estiver a utilizar autenticação básica)</span><span class="sxs-lookup"><span data-stu-id="a2a4f-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="a2a4f-149">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="a2a4f-149">password</span></span> |<span data-ttu-id="a2a4f-150">Especifique a palavra-passe da conta de utilizador de Olá especificado para nome de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="a2a4f-151">Sim (apenas se estiver a utilizar autenticação básica)</span><span class="sxs-lookup"><span data-stu-id="a2a4f-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="a2a4f-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="a2a4f-152">authorizedCredential</span></span> |<span data-ttu-id="a2a4f-153">Se estiver a utilizar o OAuth, clique em **autorizar** button hello Assistente de cópia do Data Factory ou Editor e introduza as credenciais, em seguida, o valor desta propriedade Olá será gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="a2a4f-154">Sim (apenas se estiver a utilizar autenticação OAuth)</span><span class="sxs-lookup"><span data-stu-id="a2a4f-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="a2a4f-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a2a4f-155">gatewayName</span></span> |<span data-ttu-id="a2a4f-156">Nome do gateway de Olá que Olá serviço Data Factory deve utilizar o serviço OData do tooconnect toohello no local.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="a2a4f-157">Especifique apenas se estiver a copiar dados a partir da origem de OData no local.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="a2a4f-158">Não</span><span class="sxs-lookup"><span data-stu-id="a2a4f-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="a2a4f-159">Utilizar a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="a2a4f-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="a2a4f-160">Autenticação anónima</span><span class="sxs-lookup"><span data-stu-id="a2a4f-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="a2a4f-161">Através da autenticação do Windows aceder à origem de OData no local</span><span class="sxs-lookup"><span data-stu-id="a2a4f-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="a2a4f-162">Utilizando a autenticação do OAuth de nuvem ao aceder à origem de OData</span><span class="sxs-lookup"><span data-stu-id="a2a4f-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a2a4f-163">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="a2a4f-163">Dataset properties</span></span>
<span data-ttu-id="a2a4f-164">Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a2a4f-165">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a2a4f-166">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a2a4f-167">Olá typeProperties secção para o conjunto de dados do tipo **ODataResource** (que inclui o conjunto de dados do OData) tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="a2a4f-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="a2a4f-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a2a4f-168">Property</span></span> | <span data-ttu-id="a2a4f-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="a2a4f-169">Description</span></span> | <span data-ttu-id="a2a4f-170">Necessário</span><span class="sxs-lookup"><span data-stu-id="a2a4f-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a2a4f-171">Caminho</span><span class="sxs-lookup"><span data-stu-id="a2a4f-171">path</span></span> |<span data-ttu-id="a2a4f-172">Caminho toohello recursos de OData</span><span class="sxs-lookup"><span data-stu-id="a2a4f-172">Path toohello OData resource</span></span> |<span data-ttu-id="a2a4f-173">Não</span><span class="sxs-lookup"><span data-stu-id="a2a4f-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="a2a4f-174">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="a2a4f-174">Copy activity properties</span></span>
<span data-ttu-id="a2a4f-175">Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a2a4f-176">Propriedades, tais como o nome, descrição e de saída, tabelas e política estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="a2a4f-177">As propriedades disponíveis na secção de typeProperties Olá da atividade de Olá no Olá por outro lado variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="a2a4f-178">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a2a4f-179">Quando a origem é do tipo **RelationalSource** (que inclui OData) na secção typeProperties, estão disponível Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="a2a4f-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="a2a4f-180">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a2a4f-180">Property</span></span> | <span data-ttu-id="a2a4f-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="a2a4f-181">Description</span></span> | <span data-ttu-id="a2a4f-182">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a2a4f-182">Example</span></span> | <span data-ttu-id="a2a4f-183">Necessário</span><span class="sxs-lookup"><span data-stu-id="a2a4f-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a2a4f-184">consulta</span><span class="sxs-lookup"><span data-stu-id="a2a4f-184">query</span></span> |<span data-ttu-id="a2a4f-185">Utilize Olá consulta personalizada tooread dados.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="a2a4f-186">"? $select = o nome, descrição & $top = 5"</span><span class="sxs-lookup"><span data-stu-id="a2a4f-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="a2a4f-187">Não</span><span class="sxs-lookup"><span data-stu-id="a2a4f-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="a2a4f-188">Mapeamento de tipos de OData</span><span class="sxs-lookup"><span data-stu-id="a2a4f-188">Type Mapping for OData</span></span>
<span data-ttu-id="a2a4f-189">Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá abordagem de dois passos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="a2a4f-190">Converter do tipo de too.NET de tipos de origem nativo</span><span class="sxs-lookup"><span data-stu-id="a2a4f-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="a2a4f-191">Converter do tipo de sink de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="a2a4f-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="a2a4f-192">Quando mover dados de OData, hello mapeamentos seguintes são utilizados do tipo de too.NET de tipos de OData.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="a2a4f-193">Tipo de dados de OData</span><span class="sxs-lookup"><span data-stu-id="a2a4f-193">OData Data Type</span></span> | <span data-ttu-id="a2a4f-194">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="a2a4f-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="a2a4f-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="a2a4f-195">Edm.Binary</span></span> |<span data-ttu-id="a2a4f-196">Byte]</span><span class="sxs-lookup"><span data-stu-id="a2a4f-196">Byte[]</span></span> |
| <span data-ttu-id="a2a4f-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="a2a4f-197">Edm.Boolean</span></span> |<span data-ttu-id="a2a4f-198">bool</span><span class="sxs-lookup"><span data-stu-id="a2a4f-198">Bool</span></span> |
| <span data-ttu-id="a2a4f-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="a2a4f-199">Edm.Byte</span></span> |<span data-ttu-id="a2a4f-200">Byte]</span><span class="sxs-lookup"><span data-stu-id="a2a4f-200">Byte[]</span></span> |
| <span data-ttu-id="a2a4f-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="a2a4f-201">Edm.DateTime</span></span> |<span data-ttu-id="a2a4f-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="a2a4f-202">DateTime</span></span> |
| <span data-ttu-id="a2a4f-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="a2a4f-203">Edm.Decimal</span></span> |<span data-ttu-id="a2a4f-204">Decimal</span><span class="sxs-lookup"><span data-stu-id="a2a4f-204">Decimal</span></span> |
| <span data-ttu-id="a2a4f-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="a2a4f-205">Edm.Double</span></span> |<span data-ttu-id="a2a4f-206">duplo</span><span class="sxs-lookup"><span data-stu-id="a2a4f-206">Double</span></span> |
| <span data-ttu-id="a2a4f-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="a2a4f-207">Edm.Single</span></span> |<span data-ttu-id="a2a4f-208">Único</span><span class="sxs-lookup"><span data-stu-id="a2a4f-208">Single</span></span> |
| <span data-ttu-id="a2a4f-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="a2a4f-209">Edm.Guid</span></span> |<span data-ttu-id="a2a4f-210">GUID</span><span class="sxs-lookup"><span data-stu-id="a2a4f-210">Guid</span></span> |
| <span data-ttu-id="a2a4f-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="a2a4f-211">Edm.Int16</span></span> |<span data-ttu-id="a2a4f-212">Int16</span><span class="sxs-lookup"><span data-stu-id="a2a4f-212">Int16</span></span> |
| <span data-ttu-id="a2a4f-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="a2a4f-213">Edm.Int32</span></span> |<span data-ttu-id="a2a4f-214">Int32</span><span class="sxs-lookup"><span data-stu-id="a2a4f-214">Int32</span></span> |
| <span data-ttu-id="a2a4f-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="a2a4f-215">Edm.Int64</span></span> |<span data-ttu-id="a2a4f-216">Int64</span><span class="sxs-lookup"><span data-stu-id="a2a4f-216">Int64</span></span> |
| <span data-ttu-id="a2a4f-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="a2a4f-217">Edm.SByte</span></span> |<span data-ttu-id="a2a4f-218">Int16</span><span class="sxs-lookup"><span data-stu-id="a2a4f-218">Int16</span></span> |
| <span data-ttu-id="a2a4f-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="a2a4f-219">Edm.String</span></span> |<span data-ttu-id="a2a4f-220">Cadeia</span><span class="sxs-lookup"><span data-stu-id="a2a4f-220">String</span></span> |
| <span data-ttu-id="a2a4f-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="a2a4f-221">Edm.Time</span></span> |<span data-ttu-id="a2a4f-222">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a2a4f-222">TimeSpan</span></span> |
| <span data-ttu-id="a2a4f-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="a2a4f-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="a2a4f-224">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="a2a4f-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="a2a4f-225">Por exemplo, tipos de dados complexos de OData objeto não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="a2a4f-226">Exemplo JSON: copiar dados de OData origem tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="a2a4f-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="a2a4f-227">Neste exemplo fornece definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a2a4f-228">Estes mostram como tooan Blob Storage do Azure da origem de dados de toocopy de OData.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="a2a4f-229">No entanto, os dados podem ser copiado tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="a2a4f-230">exemplo de Olá tem Olá seguintes entidades do Data Factory:</span><span class="sxs-lookup"><span data-stu-id="a2a4f-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="a2a4f-231">Um serviço ligado do tipo [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="a2a4f-232">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a2a4f-233">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="a2a4f-234">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a2a4f-235">A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a2a4f-236">exemplo de Olá copia dados da consulta em relação a um tooan de origem OData BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="a2a4f-237">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a2a4f-238">**Serviço ligado de OData:** neste exemplo Olá, utiliza a autenticação anónima.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="a2a4f-239">Consulte [serviço ligado de OData](#linked-service-properties) secção para diferentes tipos de autenticação, pode utilizar.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="a2a4f-240">**Serviço ligado do Storage do Azure:**</span><span class="sxs-lookup"><span data-stu-id="a2a4f-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="a2a4f-241">**Conjunto de dados entrado de OData:**</span><span class="sxs-lookup"><span data-stu-id="a2a4f-241">**OData input dataset:**</span></span>

<span data-ttu-id="a2a4f-242">A definição "external": "true" informa serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="a2a4f-243">Especificar **caminho** no conjunto de dados de Olá definição é opcional.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="a2a4f-244">**Conjunto de dados de saída do Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="a2a4f-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a2a4f-245">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a2a4f-246">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a2a4f-247">caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="a2a4f-248">**Atividade de cópia num pipeline com a origem de OData e o sink de Blob:**</span><span class="sxs-lookup"><span data-stu-id="a2a4f-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="a2a4f-249">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a2a4f-250">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="a2a4f-251">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona os dados (mais recentes) mais recentes de Olá a partir da origem de OData Olá.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="a2a4f-252">Especificar **consulta** no pipeline de Olá definição é opcional.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="a2a4f-253">Olá **URL** é que o serviço do Data Factory Olá utiliza dados tooretrieve: URL especificado no Olá serviço ligado (obrigatório) + caminho especificado no conjunto de dados Olá (opcional) + consultar no pipeline de Olá (opcional).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="a2a4f-254">Mapeamento de tipos de OData</span><span class="sxs-lookup"><span data-stu-id="a2a4f-254">Type mapping for OData</span></span>
<span data-ttu-id="a2a4f-255">Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá seguir abordagem de passo 2:</span><span class="sxs-lookup"><span data-stu-id="a2a4f-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="a2a4f-256">Converter do tipo de too.NET de tipos de origem nativo</span><span class="sxs-lookup"><span data-stu-id="a2a4f-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="a2a4f-257">Converter do tipo de sink de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="a2a4f-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="a2a4f-258">Quando mover dados de arquivos de dados de OData, tipos de dados de OData são tipos de too.NET mapeada.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="a2a4f-259">Mapear colunas toosink de origem</span><span class="sxs-lookup"><span data-stu-id="a2a4f-259">Map source toosink columns</span></span>
<span data-ttu-id="a2a4f-260">toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="a2a4f-261">Repetíveis leitura a partir de origens relacionais</span><span class="sxs-lookup"><span data-stu-id="a2a4f-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="a2a4f-262">Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="a2a4f-263">No Azure Data Factory, pode voltar a executar um setor manualmente.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a2a4f-264">Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a2a4f-265">Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a2a4f-266">Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="a2a4f-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a2a4f-267">Desempenho e a otimização</span><span class="sxs-lookup"><span data-stu-id="a2a4f-267">Performance and Tuning</span></span>
<span data-ttu-id="a2a4f-268">Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.</span><span class="sxs-lookup"><span data-stu-id="a2a4f-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
