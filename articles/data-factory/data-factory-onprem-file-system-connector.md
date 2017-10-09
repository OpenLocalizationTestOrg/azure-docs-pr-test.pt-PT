---
title: dados aaaCopy para/de um sistema de ficheiros utilizando o Azure Data Factory | Microsoft Docs
description: Saiba como toocopy tooand de dados de um sistema de ficheiros no local utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="c19a4-103">Copiar tooand de dados a partir de um sistema de ficheiros no local utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c19a4-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="c19a4-104">Este artigo explica como toouse Olá atividade de cópia de dados de toocopy do Azure Data Factory para/de um sistema de ficheiros no local.</span><span class="sxs-lookup"><span data-stu-id="c19a4-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="c19a4-105">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="c19a4-106">Cenários suportados</span><span class="sxs-lookup"><span data-stu-id="c19a4-106">Supported scenarios</span></span>
<span data-ttu-id="c19a4-107">Pode copiar dados **de um sistema de ficheiros no local** toohello seguir arquivos de dados:</span><span class="sxs-lookup"><span data-stu-id="c19a4-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="c19a4-108">Pode copiar dados de Olá seguir arquivos de dados **tooan no local o sistema de ficheiros**:</span><span class="sxs-lookup"><span data-stu-id="c19a4-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="c19a4-109">Atividade de cópia não eliminar o ficheiro de origem Olá depois de estes destino toohello copiados com êxito.</span><span class="sxs-lookup"><span data-stu-id="c19a4-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="c19a4-110">Se precisar de ficheiro de origem do toodelete Olá depois de uma cópia com êxito, crie um ficheiro de Olá toodelete atividade personalizada e utilize a atividade Olá no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="c19a4-111">Ativar a conectividade</span><span class="sxs-lookup"><span data-stu-id="c19a4-111">Enabling connectivity</span></span>
<span data-ttu-id="c19a4-112">Fábrica de dados suporta tooand ligação de um sistema de ficheiros no local através de **Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="c19a4-113">Tem de instalar Olá Data Management Gateway no seu ambiente no local para Olá Data Factory service tooconnect tooany suportados no local arquivo de dados, incluindo o sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="c19a4-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="c19a4-114">toolearn sobre o Data Management Gateway e para obter instruções passo a passo sobre como configurar o gateway de Olá, consulte [mover dados entre origens no local e nuvem de Olá com o Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="c19a4-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="c19a4-115">Para além do Data Management Gateway, não existem outros ficheiros binários tem toobe instalado toocommunicate tooand de um sistema de ficheiros no local.</span><span class="sxs-lookup"><span data-stu-id="c19a4-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="c19a4-116">Tem de instalar e utilizar Olá Data Management Gateway, mesmo que esteja sistema de ficheiros de Olá na VM do IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="c19a4-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="c19a4-117">Para obter informações detalhadas sobre o gateway de Olá, consulte [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c19a4-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="c19a4-118">instalar toouse uma partilha de ficheiros do Linux, [Samba](https://www.samba.org/) no seu servidor Linux e instalar o Data Management Gateway num servidor do Windows.</span><span class="sxs-lookup"><span data-stu-id="c19a4-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="c19a4-119">Instalar o Data Management Gateway num servidor Linux não é suportada.</span><span class="sxs-lookup"><span data-stu-id="c19a4-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c19a4-120">Introdução</span><span class="sxs-lookup"><span data-stu-id="c19a4-120">Getting started</span></span>
<span data-ttu-id="c19a4-121">Pode criar um pipeline com uma atividade de cópia move os dados do sistema de ficheiros utilizando ferramentas diferentes/APIs.</span><span class="sxs-lookup"><span data-stu-id="c19a4-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="c19a4-122">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="c19a4-123">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="c19a4-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="c19a4-124">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c19a4-125">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="c19a4-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="c19a4-126">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="c19a4-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="c19a4-127">Criar um **fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-127">Create a **data factory**.</span></span> <span data-ttu-id="c19a4-128">Uma fábrica de dados pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="c19a4-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="c19a4-129">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="c19a4-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="c19a4-130">Por exemplo, se estiver a copiar dados de um sistema de ficheiros no local de tooan de armazenamento de Blobs do Azure, pode cria dois serviços ligados toolink o sistema de ficheiros no local e a fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c19a4-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="c19a4-131">As propriedades de serviço ligado que são de sistema de ficheiros no local tooan específicos, consulte [ligado propriedades do serviço](#linked-service-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="c19a4-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="c19a4-132">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="c19a4-133">Exemplo de Olá mencionado no passo último Olá, criar um contentor de blob do conjunto de dados toospecify Olá e a pasta que contém dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="c19a4-134">Além disso, crie outro conjunto de dados toospecify Olá ficheiros e pastas nome (opcional) no seu sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="c19a4-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="c19a4-135">Para obter propriedades de conjunto de dados que são específico tooon local o sistema de ficheiros, consulte [propriedades do dataset](#dataset-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="c19a4-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="c19a4-136">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="c19a4-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="c19a4-137">Exemplo de Olá mencionado anteriormente, que utilizar BlobSource como uma origem e FileSystemSink como um sink para atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="c19a4-138">Da mesma forma, se estiver a copiar tooAzure de sistema de ficheiros no local o Blob Storage, utilizar FileSystemSource e BlobSink na atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="c19a4-139">Para obter as propriedades da atividade de cópia são específico tooon local o sistema de ficheiros, consulte [copiar propriedades da atividade](#copy-activity-properties) secção.</span><span class="sxs-lookup"><span data-stu-id="c19a4-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="c19a4-140">Para obter detalhes sobre como toouse um arquivo de dados como uma origem ou de um receptor de mensagens em fila, clique em ligação Olá na secção anterior do Olá para o arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="c19a4-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="c19a4-141">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="c19a4-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="c19a4-142">Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="c19a4-143">Para exemplos com definições de JSON para entidades do Data Factory que são utilizados toocopy dados para/de um sistema de ficheiros, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-file-system) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="c19a4-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="c19a4-144">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades toofile específico sistema:</span><span class="sxs-lookup"><span data-stu-id="c19a4-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c19a4-145">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="c19a4-145">Linked service properties</span></span>
<span data-ttu-id="c19a4-146">Pode ligar uma fábrica de dados do Azure de tooan de sistema de ficheiros no local com Olá **local no servidor de ficheiros** serviço ligado.</span><span class="sxs-lookup"><span data-stu-id="c19a4-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="c19a4-147">Olá, a tabela seguinte fornece descrições para os elementos JSON que são específica toohello serviço servidor de ficheiros no local ligada.</span><span class="sxs-lookup"><span data-stu-id="c19a4-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="c19a4-148">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c19a4-148">Property</span></span> | <span data-ttu-id="c19a4-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="c19a4-149">Description</span></span> | <span data-ttu-id="c19a4-150">Necessário</span><span class="sxs-lookup"><span data-stu-id="c19a4-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c19a4-151">tipo</span><span class="sxs-lookup"><span data-stu-id="c19a4-151">type</span></span> |<span data-ttu-id="c19a4-152">Certifique-se de que a propriedade de tipo Olá está definida demasiado**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="c19a4-153">Sim</span><span class="sxs-lookup"><span data-stu-id="c19a4-153">Yes</span></span> |
| <span data-ttu-id="c19a4-154">anfitrião</span><span class="sxs-lookup"><span data-stu-id="c19a4-154">host</span></span> |<span data-ttu-id="c19a4-155">Especifica o caminho da raiz da pasta de Olá que pretende que o toocopy Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="c19a4-156">Utilize o caráter de escape Olá ' \ ' para carateres especiais na cadeia de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="c19a4-157">Consulte [exemplo ligado definições de serviço e o conjunto de dados](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="c19a4-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="c19a4-158">Sim</span><span class="sxs-lookup"><span data-stu-id="c19a4-158">Yes</span></span> |
| <span data-ttu-id="c19a4-159">ID de utilizador</span><span class="sxs-lookup"><span data-stu-id="c19a4-159">userid</span></span> |<span data-ttu-id="c19a4-160">Especificar Olá ID de utilizador de Olá que tem acesso toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="c19a4-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="c19a4-161">Não (se optar por encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="c19a4-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="c19a4-162">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="c19a4-162">password</span></span> |<span data-ttu-id="c19a4-163">Especifique Olá palavra-passe do utilizador Olá (userid).</span><span class="sxs-lookup"><span data-stu-id="c19a4-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="c19a4-164">Não (se optar por encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c19a4-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="c19a4-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c19a4-165">encryptedCredential</span></span> |<span data-ttu-id="c19a4-166">Especifique as credenciais de Olá encriptado que pode obter executando o cmdlet Olá AzureRmDataFactoryEncryptValue de novo.</span><span class="sxs-lookup"><span data-stu-id="c19a4-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="c19a4-167">Não (se optar por toospecify ID de utilizador e palavra-passe em texto simples)</span><span class="sxs-lookup"><span data-stu-id="c19a4-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="c19a4-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c19a4-168">gatewayName</span></span> |<span data-ttu-id="c19a4-169">Especifica o nome de Olá do gateway de Olá que fábrica de dados deve utilizar o servidor de ficheiros do tooconnect toohello no local.</span><span class="sxs-lookup"><span data-stu-id="c19a4-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="c19a4-170">Sim</span><span class="sxs-lookup"><span data-stu-id="c19a4-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="c19a4-171">Serviço ligado e definições do conjunto de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="c19a4-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="c19a4-172">Cenário</span><span class="sxs-lookup"><span data-stu-id="c19a4-172">Scenario</span></span> | <span data-ttu-id="c19a4-173">Na definição de serviço ligado do anfitrião</span><span class="sxs-lookup"><span data-stu-id="c19a4-173">Host in linked service definition</span></span> | <span data-ttu-id="c19a4-174">folderPath na definição do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="c19a4-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c19a4-175">Pasta local no computador do Data Management Gateway:</span><span class="sxs-lookup"><span data-stu-id="c19a4-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="c19a4-176">Exemplos: D:\\ \* ou D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="c19a4-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="c19a4-177">D:\\ \\ (para o Data Management Gateway 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="c19a4-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="c19a4-178">localhost (para versões anteriores a 2.0 do Data Management Gateway)</span><span class="sxs-lookup"><span data-stu-id="c19a4-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="c19a4-179">. \\ \\ ou pasta\\\\subpasta (para o Data Management Gateway 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="c19a4-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="c19a4-180">D:\\ \\ ou d:\\\\pasta\\\\subpasta (para a versão do gateway abaixo 2.0)</span><span class="sxs-lookup"><span data-stu-id="c19a4-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="c19a4-181">Pasta partilhada remota:</span><span class="sxs-lookup"><span data-stu-id="c19a4-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="c19a4-182">Exemplos: \\ \\myserver\\partilhar\\ \* ou \\ \\myserver\\partilhar\\pasta\\subpasta\\*</span><span class="sxs-lookup"><span data-stu-id="c19a4-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="c19a4-183">\\\\\\\\MyServer\\\\partilhar</span><span class="sxs-lookup"><span data-stu-id="c19a4-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="c19a4-184">. \\ \\ ou pasta\\\\subpasta</span><span class="sxs-lookup"><span data-stu-id="c19a4-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="c19a4-185">Exemplo: Utilizar o nome de utilizador e palavra-passe em texto simples</span><span class="sxs-lookup"><span data-stu-id="c19a4-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="c19a4-186">Exemplo: Utilizar encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="c19a4-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c19a4-187">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="c19a4-187">Dataset properties</span></span>
<span data-ttu-id="c19a4-188">Para uma lista completa das secções e as propriedades disponíveis para definir os conjuntos de dados, consulte [criar conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="c19a4-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="c19a4-189">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="c19a4-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="c19a4-190">secção de typeProperties Olá é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="c19a4-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="c19a4-191">Fornece informações como localização de Olá e o formato dos dados de Olá no arquivo de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="c19a4-192">Olá typeProperties secção Olá conjunto de dados do tipo **FileShare** tem Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c19a4-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="c19a4-193">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c19a4-193">Property</span></span> | <span data-ttu-id="c19a4-194">Descrição</span><span class="sxs-lookup"><span data-stu-id="c19a4-194">Description</span></span> | <span data-ttu-id="c19a4-195">Necessário</span><span class="sxs-lookup"><span data-stu-id="c19a4-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c19a4-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="c19a4-196">folderPath</span></span> |<span data-ttu-id="c19a4-197">Especifica Olá Subcaminho toohello pasta.</span><span class="sxs-lookup"><span data-stu-id="c19a4-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="c19a4-198">Utilize o caráter de escape Olá ' \' para carateres especiais na cadeia de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="c19a4-199">Consulte [exemplo ligado definições de serviço e o conjunto de dados](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="c19a4-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="c19a4-200">Pode combinar esta propriedade com **partitionBy** toohave caminhos de pastas com base no setor início/fim tempos de data.</span><span class="sxs-lookup"><span data-stu-id="c19a4-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="c19a4-201">Sim</span><span class="sxs-lookup"><span data-stu-id="c19a4-201">Yes</span></span> |
| <span data-ttu-id="c19a4-202">fileName</span><span class="sxs-lookup"><span data-stu-id="c19a4-202">fileName</span></span> |<span data-ttu-id="c19a4-203">Especifique o nome de Olá do ficheiro de Olá no Olá **folderPath** se quiser Olá tabela toorefer tooa específico ficheiro na pasta Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="c19a4-204">Se não for especificado qualquer valor para esta propriedade, tabela Olá pontos tooall ficheiros na pasta Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="c19a4-205">Quando **fileName** não está especificado para um conjunto de dados de saída e **preserveHierarchy** não foram especificadas no receptor de atividade, Olá do ficheiro de Olá gerado está a ser Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="c19a4-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="c19a4-206">`Data.<Guid>.txt`(Exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="c19a4-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="c19a4-207">Não</span><span class="sxs-lookup"><span data-stu-id="c19a4-207">No</span></span> |
| <span data-ttu-id="c19a4-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="c19a4-208">fileFilter</span></span> |<span data-ttu-id="c19a4-209">Especifique um filtro toobe utilizada tooselect um subconjunto de ficheiros em folderPath Olá em vez de todos os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="c19a4-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="c19a4-210">Valores permitidos são: `*` (vários carateres) e `?` (único caráter).</span><span class="sxs-lookup"><span data-stu-id="c19a4-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="c19a4-211">Exemplo 1: "fileFilter": "*. log"</span><span class="sxs-lookup"><span data-stu-id="c19a4-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="c19a4-212">Exemplo 2: "fileFilter": 2014 - 1-?. txt"</span><span class="sxs-lookup"><span data-stu-id="c19a4-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="c19a4-213">Tenha em atenção que fileFilter se aplica a um conjunto de dados de partilha de ficheiros de entrada.</span><span class="sxs-lookup"><span data-stu-id="c19a4-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="c19a4-214">Não</span><span class="sxs-lookup"><span data-stu-id="c19a4-214">No</span></span> |
| <span data-ttu-id="c19a4-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="c19a4-215">partitionedBy</span></span> |<span data-ttu-id="c19a4-216">Pode utilizar partitionedBy toospecify folderPath/fileName dinâmico para dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="c19a4-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="c19a4-217">Um exemplo é folderPath parametrizada para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="c19a4-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="c19a4-218">Não</span><span class="sxs-lookup"><span data-stu-id="c19a4-218">No</span></span> |
| <span data-ttu-id="c19a4-219">formato</span><span class="sxs-lookup"><span data-stu-id="c19a4-219">format</span></span> | <span data-ttu-id="c19a4-220">é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c19a4-221">Conjunto Olá **tipo** propriedade em formato tooone destes valores.</span><span class="sxs-lookup"><span data-stu-id="c19a4-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="c19a4-222">Para obter mais informações, consulte [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc formato](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato](data-factory-supported-file-and-compression-formats.md#parquet-format) secções.</span><span class="sxs-lookup"><span data-stu-id="c19a4-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="c19a4-223">Se quiser demasiado**copiar ficheiros como-é** entre arquivos baseados em ficheiros (cópia binário), ignorar a secção de formato Olá em ambas as definições do conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="c19a4-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="c19a4-224">Não</span><span class="sxs-lookup"><span data-stu-id="c19a4-224">No</span></span> |
| <span data-ttu-id="c19a4-225">Compressão</span><span class="sxs-lookup"><span data-stu-id="c19a4-225">compression</span></span> | <span data-ttu-id="c19a4-226">Especifique o tipo de Olá e nível de compressão de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="c19a4-227">Tipos suportados são: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="c19a4-228">Níveis suportados são: **Optimal** e **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c19a4-229">consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="c19a4-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c19a4-230">Não</span><span class="sxs-lookup"><span data-stu-id="c19a4-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="c19a4-231">Não é possível utilizar fileName e fileFilter em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="c19a4-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="c19a4-232">Utilizar a propriedade partitionedBy</span><span class="sxs-lookup"><span data-stu-id="c19a4-232">Using partitionedBy property</span></span>
<span data-ttu-id="c19a4-233">Tal como mencionado na secção anterior Olá, pode especificar um folderPath dinâmica e o nome de ficheiro de dados de séries de tempo com Olá **partitionedBy** propriedade, [funções de Data Factory e variáveis do sistema Olá](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c19a4-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="c19a4-234">Consulte mais detalhes em conjuntos de dados de séries de tempo, agendar e setores, de toounderstand [criar conjuntos de dados](data-factory-create-datasets.md), [agendamento e execução](data-factory-scheduling-and-execution.md), e [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c19a4-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="c19a4-235">Exemplo 1:</span><span class="sxs-lookup"><span data-stu-id="c19a4-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="c19a4-236">Neste exemplo, {setor} é substituído pelo valor Olá de Olá fábrica de dados de variável de sistema SliceStart no formato de Olá (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="c19a4-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="c19a4-237">SliceStart refere-se a hora de toostart do setor Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="c19a4-238">Olá folderPath é diferente para cada setor.</span><span class="sxs-lookup"><span data-stu-id="c19a4-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="c19a4-239">Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="c19a4-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="c19a4-240">Exemplo 2:</span><span class="sxs-lookup"><span data-stu-id="c19a4-240">Sample 2:</span></span>

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

<span data-ttu-id="c19a4-241">Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos para variáveis separadas que utilizam propriedades de Olá folderPath e nome de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="c19a4-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c19a4-242">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="c19a4-242">Copy activity properties</span></span>
<span data-ttu-id="c19a4-243">Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="c19a4-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c19a4-244">Propriedades, tais como o nome, descrição e de saída, conjuntos de dados e as políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="c19a4-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="c19a4-245">Enquanto, propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="c19a4-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="c19a4-246">Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="c19a4-247">Se estiver a mover dados de um sistema de ficheiros no local, definir o tipo de origem Olá na atividade de cópia de Olá demasiado**FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="c19a4-248">Da mesma forma, se estiver a mover dados tooan sistema de ficheiros no local, defina o tipo de sink Olá na atividade de cópia de Olá demasiado**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="c19a4-249">Esta secção fornece uma lista de propriedades suportadas por FileSystemSource e FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="c19a4-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="c19a4-250">**FileSystemSource** suporta Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c19a4-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="c19a4-251">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c19a4-251">Property</span></span> | <span data-ttu-id="c19a4-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="c19a4-252">Description</span></span> | <span data-ttu-id="c19a4-253">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="c19a4-253">Allowed values</span></span> | <span data-ttu-id="c19a4-254">Necessário</span><span class="sxs-lookup"><span data-stu-id="c19a4-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c19a4-255">Recursiva</span><span class="sxs-lookup"><span data-stu-id="c19a4-255">recursive</span></span> |<span data-ttu-id="c19a4-256">Indica se Olá é ler dados recursivamente subpastas Olá ou apenas a pasta especificada Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="c19a4-257">TRUE, False (predefinição)</span><span class="sxs-lookup"><span data-stu-id="c19a4-257">True, False (default)</span></span> |<span data-ttu-id="c19a4-258">Não</span><span class="sxs-lookup"><span data-stu-id="c19a4-258">No</span></span> |

<span data-ttu-id="c19a4-259">**FileSystemSink** suporta Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c19a4-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="c19a4-260">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c19a4-260">Property</span></span> | <span data-ttu-id="c19a4-261">Descrição</span><span class="sxs-lookup"><span data-stu-id="c19a4-261">Description</span></span> | <span data-ttu-id="c19a4-262">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="c19a4-262">Allowed values</span></span> | <span data-ttu-id="c19a4-263">Necessário</span><span class="sxs-lookup"><span data-stu-id="c19a4-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c19a4-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="c19a4-264">copyBehavior</span></span> |<span data-ttu-id="c19a4-265">Define o comportamento de cópia de Olá quando a origem de Olá é BlobSource ou sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="c19a4-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="c19a4-266">**PreserveHierarchy:** preserva a hierarquia de ficheiros de Olá na pasta de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="c19a4-267">Ou seja, o caminho da pasta de origem do Olá origem ficheiro toohello relativo Olá é Olá, mesmo que o caminho da pasta de destino do toohello no ficheiro de destino do Olá relativo Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="c19a4-268">**FlattenHierarchy:** todos os ficheiros da pasta de origem Olá são criados no nível de primeiro Olá da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="c19a4-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="c19a4-269">ficheiros do destino de Olá são criados com um nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c19a4-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="c19a4-270">**MergeFiles:** une todos os ficheiros a partir do ficheiro de tooone da pasta de origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="c19a4-271">Se for especificado o nome de blob/nome de ficheiro Olá, Olá ficheiro intercalado é Olá especificado nome.</span><span class="sxs-lookup"><span data-stu-id="c19a4-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="c19a4-272">Caso contrário, é um nome de ficheiro gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c19a4-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="c19a4-273">Não</span><span class="sxs-lookup"><span data-stu-id="c19a4-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="c19a4-274">Exemplos de recursiva e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="c19a4-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="c19a4-275">Esta secção descreve o comportamento resultante de Olá de operação de cópia de Olá para diferentes combinações de valores para Olá recursiva e copyBehavior propriedades.</span><span class="sxs-lookup"><span data-stu-id="c19a4-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="c19a4-276">valor de recursiva</span><span class="sxs-lookup"><span data-stu-id="c19a4-276">recursive value</span></span> | <span data-ttu-id="c19a4-277">valor de copyBehavior</span><span class="sxs-lookup"><span data-stu-id="c19a4-277">copyBehavior value</span></span> | <span data-ttu-id="c19a4-278">Comportamento resultante</span><span class="sxs-lookup"><span data-stu-id="c19a4-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c19a4-279">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="c19a4-279">true</span></span> |<span data-ttu-id="c19a4-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="c19a4-280">preserveHierarchy</span></span> |<span data-ttu-id="c19a4-281">Para uma pasta de origem Pasta1 com Olá seguir a estrutura de</span><span class="sxs-lookup"><span data-stu-id="c19a4-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c19a4-282">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-282">Folder1</span></span><br/><span data-ttu-id="c19a4-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c19a4-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c19a4-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c19a4-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c19a4-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="c19a4-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c19a4-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c19a4-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c19a4-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c19a4-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c19a4-289">pasta de destino Olá Pasta1 é criada com Olá mesmo estrutura como origem Olá:</span><span class="sxs-lookup"><span data-stu-id="c19a4-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="c19a4-290">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-290">Folder1</span></span><br/><span data-ttu-id="c19a4-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c19a4-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c19a4-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c19a4-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c19a4-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="c19a4-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c19a4-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c19a4-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c19a4-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c19a4-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="c19a4-297">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="c19a4-297">true</span></span> |<span data-ttu-id="c19a4-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="c19a4-298">flattenHierarchy</span></span> |<span data-ttu-id="c19a4-299">Para uma pasta de origem Pasta1 com Olá seguir a estrutura de</span><span class="sxs-lookup"><span data-stu-id="c19a4-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c19a4-300">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-300">Folder1</span></span><br/><span data-ttu-id="c19a4-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c19a4-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c19a4-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c19a4-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c19a4-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="c19a4-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c19a4-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c19a4-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c19a4-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c19a4-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c19a4-307">destino de Olá Pasta1 é criado com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="c19a4-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="c19a4-308">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-308">Folder1</span></span><br/><span data-ttu-id="c19a4-309">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="c19a4-310">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="c19a4-311">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File3</span><span class="sxs-lookup"><span data-stu-id="c19a4-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="c19a4-312">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File4</span><span class="sxs-lookup"><span data-stu-id="c19a4-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="c19a4-313">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File5</span><span class="sxs-lookup"><span data-stu-id="c19a4-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="c19a4-314">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="c19a4-314">true</span></span> |<span data-ttu-id="c19a4-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="c19a4-315">mergeFiles</span></span> |<span data-ttu-id="c19a4-316">Para uma pasta de origem Pasta1 com Olá seguir a estrutura de</span><span class="sxs-lookup"><span data-stu-id="c19a4-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c19a4-317">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-317">Folder1</span></span><br/><span data-ttu-id="c19a4-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c19a4-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c19a4-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c19a4-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c19a4-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="c19a4-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c19a4-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c19a4-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c19a4-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c19a4-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c19a4-324">destino de Olá Pasta1 é criado com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="c19a4-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="c19a4-325">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-325">Folder1</span></span><br/><span data-ttu-id="c19a4-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + ficheiro 5 é intercalado conteúdo para um ficheiro com um nome de ficheiro gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c19a4-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="c19a4-327">FALSO</span><span class="sxs-lookup"><span data-stu-id="c19a4-327">false</span></span> |<span data-ttu-id="c19a4-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="c19a4-328">preserveHierarchy</span></span> |<span data-ttu-id="c19a4-329">Para uma pasta de origem Pasta1 com Olá seguir a estrutura de</span><span class="sxs-lookup"><span data-stu-id="c19a4-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c19a4-330">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-330">Folder1</span></span><br/><span data-ttu-id="c19a4-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c19a4-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c19a4-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c19a4-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c19a4-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="c19a4-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c19a4-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c19a4-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c19a4-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c19a4-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c19a4-337">pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="c19a4-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="c19a4-338">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-338">Folder1</span></span><br/><span data-ttu-id="c19a4-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c19a4-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="c19a4-341">Não é escolhido Subfolder1 com File3, File4 e File5.</span><span class="sxs-lookup"><span data-stu-id="c19a4-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="c19a4-342">FALSO</span><span class="sxs-lookup"><span data-stu-id="c19a4-342">false</span></span> |<span data-ttu-id="c19a4-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="c19a4-343">flattenHierarchy</span></span> |<span data-ttu-id="c19a4-344">Para uma pasta de origem Pasta1 com Olá seguir a estrutura de</span><span class="sxs-lookup"><span data-stu-id="c19a4-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c19a4-345">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-345">Folder1</span></span><br/><span data-ttu-id="c19a4-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c19a4-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c19a4-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c19a4-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c19a4-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="c19a4-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c19a4-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c19a4-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c19a4-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c19a4-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c19a4-352">pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="c19a4-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="c19a4-353">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-353">Folder1</span></span><br/><span data-ttu-id="c19a4-354">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="c19a4-355">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="c19a4-356">Não é escolhido Subfolder1 com File3, File4 e File5.</span><span class="sxs-lookup"><span data-stu-id="c19a4-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="c19a4-357">FALSO</span><span class="sxs-lookup"><span data-stu-id="c19a4-357">false</span></span> |<span data-ttu-id="c19a4-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="c19a4-358">mergeFiles</span></span> |<span data-ttu-id="c19a4-359">Para uma pasta de origem Pasta1 com Olá seguir a estrutura de</span><span class="sxs-lookup"><span data-stu-id="c19a4-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c19a4-360">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-360">Folder1</span></span><br/><span data-ttu-id="c19a4-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c19a4-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="c19a4-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c19a4-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c19a4-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c19a4-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="c19a4-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c19a4-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c19a4-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c19a4-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c19a4-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c19a4-367">pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="c19a4-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="c19a4-368">Pasta1</span><span class="sxs-lookup"><span data-stu-id="c19a4-368">Folder1</span></span><br/><span data-ttu-id="c19a4-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 conteúdos são intercalados para um ficheiro com um nome de ficheiro gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c19a4-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="c19a4-370">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para File1</span><span class="sxs-lookup"><span data-stu-id="c19a4-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="c19a4-371">Não é escolhido Subfolder1 com File3, File4 e File5.</span><span class="sxs-lookup"><span data-stu-id="c19a4-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="c19a4-372">Formatos de ficheiro e compressão suportados</span><span class="sxs-lookup"><span data-stu-id="c19a4-372">Supported file and compression formats</span></span>
<span data-ttu-id="c19a4-373">Consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo em detalhes.</span><span class="sxs-lookup"><span data-stu-id="c19a4-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="c19a4-374">Exemplos JSON para copiar dados tooand do sistema de ficheiros</span><span class="sxs-lookup"><span data-stu-id="c19a4-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="c19a4-375">Olá exemplos seguintes fornecem definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c19a4-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c19a4-376">Estes mostram como toocopy tooand de dados de um sistema de ficheiros no local e o armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c19a4-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="c19a4-377">No entanto, pode copiar dados *diretamente* de qualquer um dos Olá origens tooany de Olá sinks listado no [suportados origens e sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando a atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c19a4-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="c19a4-378">Exemplo: Copiar dados de um tooAzure de sistema de ficheiros local no armazenamento de BLOBs</span><span class="sxs-lookup"><span data-stu-id="c19a4-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="c19a4-379">Este exemplo mostra como toocopy dados a partir de um tooAzure de sistema de ficheiros local no armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="c19a4-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="c19a4-380">exemplo de Olá tem Olá seguintes entidades do Data Factory:</span><span class="sxs-lookup"><span data-stu-id="c19a4-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="c19a4-381">Um serviço ligado do tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c19a4-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="c19a4-382">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c19a4-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="c19a4-383">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c19a4-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="c19a4-384">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c19a4-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="c19a4-385">A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c19a4-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c19a4-386">Olá exemplo a seguir copia dados de séries de tempo de um tooAzure de sistema de ficheiros local no armazenamento de BLOBs a cada hora.</span><span class="sxs-lookup"><span data-stu-id="c19a4-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="c19a4-387">Propriedades JSON Olá que são utilizadas nestes exemplos são descritas nas secções de Olá após amostras Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="c19a4-388">Como primeiro passo, configurar o Data Management Gateway de acordo com as instruções de Olá em [mover dados entre origens no local e nuvem de Olá com o Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="c19a4-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="c19a4-389">**Serviço ligado do servidor de ficheiros no local:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="c19a4-390">Recomendamos que utilize Olá **encryptedCredential** propriedade em vez disso, Olá **userid** e **palavra-passe** propriedades.</span><span class="sxs-lookup"><span data-stu-id="c19a4-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="c19a4-391">Consulte [serviço ligado do servidor de ficheiros](#linked-service-properties) para obter detalhes sobre este serviço ligado.</span><span class="sxs-lookup"><span data-stu-id="c19a4-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="c19a4-392">**Serviço ligado do Storage do Azure:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="c19a4-393">**Conjunto de dados de entrada de sistema de ficheiros no local:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="c19a4-394">Dados são captados um novo ficheiro de cada hora.</span><span class="sxs-lookup"><span data-stu-id="c19a4-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="c19a4-395">Olá folderPath e propriedades de nome de ficheiro são determinadas com base na hora de início de Olá do setor Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="c19a4-396">Definição `"external": "true"` informa fábrica de dados, esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="c19a4-397">**Conjunto de dados de saída do Blob storage do Azure:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="c19a4-398">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="c19a4-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c19a4-399">caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="c19a4-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="c19a4-400">caminho da pasta Olá utiliza as partes de ano, mês, dia e hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="c19a4-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="c19a4-401">**Uma atividade de cópia num pipeline com a origem de sistema de ficheiros e o sink de Blob:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="c19a4-402">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída, não sendo toorun agendada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="c19a4-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="c19a4-403">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**FileSystemSource**, e **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="c19a4-404">Exemplo: Copiar dados de sistema de ficheiros no local do SQL Database do Azure tooan</span><span class="sxs-lookup"><span data-stu-id="c19a4-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="c19a4-405">Olá seguinte exemplo mostra:</span><span class="sxs-lookup"><span data-stu-id="c19a4-405">hello following sample shows:</span></span>

* <span data-ttu-id="c19a4-406">Um serviço ligado do tipo [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c19a4-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="c19a4-407">Um serviço ligado do tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c19a4-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="c19a4-408">Um conjunto de dados de entrada do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c19a4-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="c19a4-409">Um conjunto de dados de saída do tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c19a4-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="c19a4-410">Um pipeline com uma atividade de cópia que utiliza [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) e [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c19a4-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="c19a4-411">exemplo de Olá copia dados de séries de tempo de um sistema de ficheiros no local do SQL do Azure tabela tooan a cada hora.</span><span class="sxs-lookup"><span data-stu-id="c19a4-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="c19a4-412">Propriedades JSON Olá que são utilizadas nestes exemplos são descritas nas secções após amostras Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="c19a4-413">**Serviço ligado do SQL Database do Azure:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-413">**Azure SQL Database linked service:**</span></span>

```JSON
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

<span data-ttu-id="c19a4-414">**Serviço ligado do servidor de ficheiros no local:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="c19a4-415">Recomendamos que utilize Olá **encryptedCredential** propriedade em vez de utilizar Olá **userid** e **palavra-passe** propriedades.</span><span class="sxs-lookup"><span data-stu-id="c19a4-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="c19a4-416">Consulte [serviço ligado do sistema de ficheiros](#linked-service-properties) para obter detalhes sobre este serviço ligado.</span><span class="sxs-lookup"><span data-stu-id="c19a4-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="c19a4-417">**Conjunto de dados de entrada SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="c19a4-418">exemplo de Olá pressupõe que criou uma tabela "MyTable" no SQL do Azure e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="c19a4-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="c19a4-419">Definição ``“external”: ”true”`` informa fábrica de dados, esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
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

<span data-ttu-id="c19a4-420">**Conjunto de dados de saída de sistema de ficheiros no local:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="c19a4-421">Os dados são copiados tooa novo ficheiro a cada hora.</span><span class="sxs-lookup"><span data-stu-id="c19a4-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="c19a4-422">Olá folderPath e nome de ficheiro de blob Olá são determinados com base na hora de início de Olá do setor Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="c19a4-423">**Uma atividade de cópia num pipeline com a origem SQL e o sink de sistema de ficheiros:**</span><span class="sxs-lookup"><span data-stu-id="c19a4-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="c19a4-424">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída, não sendo toorun agendada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="c19a4-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="c19a4-425">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**SqlSource**e Olá **sink** tipo está definido demasiado**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="c19a4-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="c19a4-426">consulta SQL Olá especificado para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá passado toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="c19a4-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="c19a4-427">Também pode mapear colunas do conjunto de dados de origem toocolumns do conjunto de dados dependente na definição de atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="c19a4-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="c19a4-428">Para obter mais informações, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c19a4-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c19a4-429">Desempenho e otimização</span><span class="sxs-lookup"><span data-stu-id="c19a4-429">Performance and tuning</span></span>
 <span data-ttu-id="c19a4-430">toolearn sobre chave factors desse desempenho de Olá impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo, consulte Olá [guia Otimização e de desempenho de atividade de cópia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="c19a4-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
