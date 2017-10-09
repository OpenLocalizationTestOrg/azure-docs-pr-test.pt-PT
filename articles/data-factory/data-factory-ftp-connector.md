---
title: dados de aaaMove de um servidor FTP utilizando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como dados de toomove de um servidor FTP utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="41d17-103">Mover dados de um servidor de FTP utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="41d17-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="41d17-104">Este artigo explica como toouse Olá atividade de cópia de dados do Azure Data Factory toomove de um servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="41d17-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="41d17-105">Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="41d17-106">Pode copiar dados de um arquivo de dados de receptor de tooany suportado de servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="41d17-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="41d17-107">Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="41d17-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="41d17-108">Fábrica de dados suporta atualmente só armazena dados movimento de dados de tooother do servidor de FTP, mas não mover dados de outros dados armazena servidor tooan FTP.</span><span class="sxs-lookup"><span data-stu-id="41d17-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="41d17-109">Suporta tanto no local e na nuvem servidores FTP.</span><span class="sxs-lookup"><span data-stu-id="41d17-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="41d17-110">atividade de cópia de Olá não eliminar o ficheiro de origem Olá depois de estes destino toohello copiados com êxito.</span><span class="sxs-lookup"><span data-stu-id="41d17-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="41d17-111">Se precisar de ficheiro de origem do toodelete Olá depois de uma cópia com êxito, crie um ficheiro de Olá toodelete atividade personalizada e utilize a atividade de Olá no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="41d17-112">Ativar a conectividade</span><span class="sxs-lookup"><span data-stu-id="41d17-112">Enable connectivity</span></span>
<span data-ttu-id="41d17-113">Se estiver a mover dados a partir de um **no local** arquivo de dados na nuvem de tooa de servidor FTP (por exemplo, a tooAzure armazenamento de BLOBs), instalar e utilizar o Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="41d17-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="41d17-114">Olá Data Management Gateway é um agente de cliente que está instalado no seu computador local e permite recurso da nuvem serviços tooconnect tooan no local.</span><span class="sxs-lookup"><span data-stu-id="41d17-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="41d17-115">Para obter mais informações, consulte [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="41d17-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="41d17-116">Para obter instruções passo a passo sobre como configurar o gateway de Olá e utilizá-lo, consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="41d17-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="41d17-117">Utilizar Olá gateway tooconnect tooan FTP server, mesmo que esteja servidor Olá numa infraestrutura do Azure como uma máquina virtual (VM) do serviço (IaaS).</span><span class="sxs-lookup"><span data-stu-id="41d17-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="41d17-118">É possível tooinstall gateway de Olá Olá mesmo no local da máquina ou VM do IaaS como hello do servidor de FTP.</span><span class="sxs-lookup"><span data-stu-id="41d17-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="41d17-119">No entanto, recomendamos que instale o gateway de Olá num computador separado ou contenção de recursos do VM do IaaS tooavoid e para um melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="41d17-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="41d17-120">Quando instalar o gateway de Olá num computador separado, máquina Olá deve ser o servidor de FTP possam tooaccess Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="41d17-121">Introdução</span><span class="sxs-lookup"><span data-stu-id="41d17-121">Get started</span></span>
<span data-ttu-id="41d17-122">Pode criar um pipeline com uma atividade de cópia move dados a partir de uma origem FTP utilizando ferramentas diferentes ou APIs.</span><span class="sxs-lookup"><span data-stu-id="41d17-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="41d17-123">Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente de cópia do Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="41d17-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="41d17-124">Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para instruções rápidas.</span><span class="sxs-lookup"><span data-stu-id="41d17-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="41d17-125">Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **PowerShell**, **modelo Azure Resource Manager**, **.NET API**, e **REST API**.</span><span class="sxs-lookup"><span data-stu-id="41d17-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="41d17-126">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="41d17-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="41d17-127">Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:</span><span class="sxs-lookup"><span data-stu-id="41d17-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="41d17-128">Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.</span><span class="sxs-lookup"><span data-stu-id="41d17-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="41d17-129">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="41d17-130">Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="41d17-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="41d17-131">Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="41d17-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="41d17-132">Quando utilizar APIs (exceto .NET API) ou ferramentas, é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="41d17-133">Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de um arquivo de dados do FTP, consulte Olá [exemplo JSON: copiar dados de blob de tooAzure do servidor FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) secção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="41d17-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="41d17-134">Para obter detalhes sobre toouse de formatos de ficheiro e compressão suportado, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="41d17-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="41d17-135">Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine entidades de fábrica de dados tooFTP específico.</span><span class="sxs-lookup"><span data-stu-id="41d17-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="41d17-136">Propriedades de serviço ligado</span><span class="sxs-lookup"><span data-stu-id="41d17-136">Linked service properties</span></span>
<span data-ttu-id="41d17-137">Olá, a tabela seguinte descreve o serviço FTP ligado JSON elementos tooan específico.</span><span class="sxs-lookup"><span data-stu-id="41d17-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="41d17-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="41d17-138">Property</span></span> | <span data-ttu-id="41d17-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="41d17-139">Description</span></span> | <span data-ttu-id="41d17-140">Necessário</span><span class="sxs-lookup"><span data-stu-id="41d17-140">Required</span></span> | <span data-ttu-id="41d17-141">Predefinição</span><span class="sxs-lookup"><span data-stu-id="41d17-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="41d17-142">tipo</span><span class="sxs-lookup"><span data-stu-id="41d17-142">type</span></span> |<span data-ttu-id="41d17-143">Defina este tooFtpServer.</span><span class="sxs-lookup"><span data-stu-id="41d17-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="41d17-144">Sim</span><span class="sxs-lookup"><span data-stu-id="41d17-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="41d17-145">anfitrião</span><span class="sxs-lookup"><span data-stu-id="41d17-145">host</span></span> |<span data-ttu-id="41d17-146">Especifique o nome de Olá ou endereço IP do servidor FTP Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="41d17-147">Sim</span><span class="sxs-lookup"><span data-stu-id="41d17-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="41d17-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="41d17-148">authenticationType</span></span> |<span data-ttu-id="41d17-149">Especifique o tipo de autenticação de Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-149">Specify hello authentication type.</span></span> |<span data-ttu-id="41d17-150">Sim</span><span class="sxs-lookup"><span data-stu-id="41d17-150">Yes</span></span> |<span data-ttu-id="41d17-151">Anónimo, básico</span><span class="sxs-lookup"><span data-stu-id="41d17-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="41d17-152">o nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="41d17-152">username</span></span> |<span data-ttu-id="41d17-153">Especificar utilizador Olá com o servidor de FTP toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="41d17-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="41d17-154">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-154">No</span></span> |&nbsp; |
| <span data-ttu-id="41d17-155">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="41d17-155">password</span></span> |<span data-ttu-id="41d17-156">Especifique Olá palavra-passe do utilizador Olá (nome de utilizador).</span><span class="sxs-lookup"><span data-stu-id="41d17-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="41d17-157">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-157">No</span></span> |&nbsp; |
| <span data-ttu-id="41d17-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="41d17-158">encryptedCredential</span></span> |<span data-ttu-id="41d17-159">Especifica Olá encriptado credencial tooaccess Olá FTP servidor.</span><span class="sxs-lookup"><span data-stu-id="41d17-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="41d17-160">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-160">No</span></span> |&nbsp; |
| <span data-ttu-id="41d17-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="41d17-161">gatewayName</span></span> |<span data-ttu-id="41d17-162">Especifique o nome de Olá do gateway de Olá no servidor FTP do Data Management Gateway tooconnect tooan no local.</span><span class="sxs-lookup"><span data-stu-id="41d17-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="41d17-163">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-163">No</span></span> |&nbsp; |
| <span data-ttu-id="41d17-164">porta</span><span class="sxs-lookup"><span data-stu-id="41d17-164">port</span></span> |<span data-ttu-id="41d17-165">Especifique a porta de Olá no qual Olá FTP servidor está a escutar.</span><span class="sxs-lookup"><span data-stu-id="41d17-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="41d17-166">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-166">No</span></span> |<span data-ttu-id="41d17-167">21</span><span class="sxs-lookup"><span data-stu-id="41d17-167">21</span></span> |
| <span data-ttu-id="41d17-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="41d17-168">enableSsl</span></span> |<span data-ttu-id="41d17-169">Especifique se toouse FTP através de um canal SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="41d17-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="41d17-170">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-170">No</span></span> |<span data-ttu-id="41d17-171">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="41d17-171">true</span></span> |
| <span data-ttu-id="41d17-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="41d17-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="41d17-173">Especifique se o servidor tooenable SSL certificado validação quando estiver a utilizar FTP através do canal SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="41d17-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="41d17-174">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-174">No</span></span> |<span data-ttu-id="41d17-175">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="41d17-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="41d17-176">Utilize a autenticação anónima</span><span class="sxs-lookup"><span data-stu-id="41d17-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="41d17-177">Utilize o nome de utilizador e palavra-passe em texto simples para a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="41d17-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="41d17-178">Utilizar porta, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="41d17-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="41d17-179">Utilizar encryptedCredential para autenticação e de gateway</span><span class="sxs-lookup"><span data-stu-id="41d17-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="41d17-180">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="41d17-180">Dataset properties</span></span>
<span data-ttu-id="41d17-181">Para uma lista completa das secções e propriedades disponíveis para definir os conjuntos de dados, consulte [criar conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="41d17-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="41d17-182">As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="41d17-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="41d17-183">Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="41d17-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="41d17-184">Fornece informações que é o tipo de conjunto de toohello específico.</span><span class="sxs-lookup"><span data-stu-id="41d17-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="41d17-185">Olá **typeProperties** secção para um conjunto de dados do tipo **FileShare** tem Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="41d17-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="41d17-186">Propriedade</span><span class="sxs-lookup"><span data-stu-id="41d17-186">Property</span></span> | <span data-ttu-id="41d17-187">Descrição</span><span class="sxs-lookup"><span data-stu-id="41d17-187">Description</span></span> | <span data-ttu-id="41d17-188">Necessário</span><span class="sxs-lookup"><span data-stu-id="41d17-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41d17-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="41d17-189">folderPath</span></span> |<span data-ttu-id="41d17-190">Pasta de toohello Subcaminho.</span><span class="sxs-lookup"><span data-stu-id="41d17-190">Subpath toohello folder.</span></span> <span data-ttu-id="41d17-191">Utilize o caráter de escape ' \ ' para carateres especiais na cadeia de Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="41d17-192">Consulte [exemplo ligado definições de serviço e o conjunto de dados](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="41d17-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="41d17-193">Pode combinar esta propriedade com **partitionBy** toohave caminhos de pastas com base no setor começar e terminar tempos de data.</span><span class="sxs-lookup"><span data-stu-id="41d17-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="41d17-194">Sim</span><span class="sxs-lookup"><span data-stu-id="41d17-194">Yes</span></span> |
| <span data-ttu-id="41d17-195">fileName</span><span class="sxs-lookup"><span data-stu-id="41d17-195">fileName</span></span> |<span data-ttu-id="41d17-196">Especifique o nome de Olá do ficheiro de Olá no Olá **folderPath** se quiser Olá tabela toorefer tooa específico ficheiro na pasta Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="41d17-197">Se não for especificado qualquer valor para esta propriedade, tabela Olá pontos tooall ficheiros na pasta Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="41d17-198">Quando **fileName** não está especificado para um conjunto de dados de saída, Olá do ficheiro de Olá gerado está a ser Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="41d17-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="41d17-199">Dados. <Guid>. txt (exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="41d17-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="41d17-200">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-200">No</span></span> |
| <span data-ttu-id="41d17-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="41d17-201">fileFilter</span></span> |<span data-ttu-id="41d17-202">Especifique um tooselect toobe utilizado de filtro um subconjunto de ficheiros no Olá **folderPath**, em vez de todos os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="41d17-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="41d17-203">Valores permitidos são: `*` (vários carateres) e `?` (único caráter).</span><span class="sxs-lookup"><span data-stu-id="41d17-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="41d17-204">Exemplo 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="41d17-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="41d17-205">Exemplo 2:`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="41d17-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="41d17-206">**fileFilter** se aplica a um conjunto de dados de partilha de ficheiros de entrada.</span><span class="sxs-lookup"><span data-stu-id="41d17-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="41d17-207">Esta propriedade não é suportada com distribuído ficheiro sistema Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="41d17-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="41d17-208">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-208">No</span></span> |
| <span data-ttu-id="41d17-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="41d17-209">partitionedBy</span></span> |<span data-ttu-id="41d17-210">Utilizado toospecify um dinâmico **folderPath** e **fileName** para dados de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="41d17-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="41d17-211">Por exemplo, pode especificar um **folderPath** que é parametrizada para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="41d17-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="41d17-212">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-212">No</span></span> |
| <span data-ttu-id="41d17-213">formato</span><span class="sxs-lookup"><span data-stu-id="41d17-213">format</span></span> | <span data-ttu-id="41d17-214">é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="41d17-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="41d17-215">Conjunto Olá **tipo** propriedade em formato tooone destes valores.</span><span class="sxs-lookup"><span data-stu-id="41d17-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="41d17-216">Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc formato](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) secções.</span><span class="sxs-lookup"><span data-stu-id="41d17-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="41d17-217">Se pretender que os ficheiros de toocopy conforme forem entre arquivos baseados em ficheiros (cópia binário), ignore a secção de formato de Olá em ambas as definições do conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="41d17-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="41d17-218">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-218">No</span></span> |
| <span data-ttu-id="41d17-219">Compressão</span><span class="sxs-lookup"><span data-stu-id="41d17-219">compression</span></span> | <span data-ttu-id="41d17-220">Especifique o tipo de Olá e nível de compressão de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="41d17-221">Tipos suportados são **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**, e níveis suportados são **Optimal** e **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="41d17-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="41d17-222">Para obter mais informações, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="41d17-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="41d17-223">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-223">No</span></span> |
| <span data-ttu-id="41d17-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="41d17-224">useBinaryTransfer</span></span> |<span data-ttu-id="41d17-225">Especifique se binário de Olá toouse modo de transferência.</span><span class="sxs-lookup"><span data-stu-id="41d17-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="41d17-226">valores de Olá forem verdadeiros para o modo binário (este é o valor predefinido de Olá) ou FALSO para ASCII.</span><span class="sxs-lookup"><span data-stu-id="41d17-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="41d17-227">Esta propriedade só pode ser utilizada quando hello tipo de serviço ligado associado é do tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="41d17-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="41d17-228">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="41d17-229">**nome de ficheiro** e **fileFilter** não podem ser utilizados em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="41d17-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="41d17-230">Utilize a propriedade de partionedBy Olá</span><span class="sxs-lookup"><span data-stu-id="41d17-230">Use hello partionedBy property</span></span>
<span data-ttu-id="41d17-231">Tal como mencionado na secção anterior Olá, pode especificar um dinâmico **folderPath** e **fileName** para dados de séries de tempo com Olá **partitionedBy** propriedade.</span><span class="sxs-lookup"><span data-stu-id="41d17-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="41d17-232">toolearn sobre conjuntos de dados de séries de tempo, agendar e setores, consulte [criar conjuntos de dados](data-factory-create-datasets.md), [agendamento e execução](data-factory-scheduling-and-execution.md), e [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="41d17-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="41d17-233">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="41d17-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="41d17-234">Neste exemplo, {setor} é substituído pelo valor Olá da variável de sistema do Data Factory SliceStart, no Olá Formatar especificado (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="41d17-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="41d17-235">Olá SliceStart refere-se a hora de toostart do setor Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="41d17-236">caminho da pasta Olá é diferente para cada setor.</span><span class="sxs-lookup"><span data-stu-id="41d17-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="41d17-237">(Por exemplo, wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104)</span><span class="sxs-lookup"><span data-stu-id="41d17-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="41d17-238">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="41d17-238">Sample 2</span></span>

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
<span data-ttu-id="41d17-239">Neste exemplo, são extraídos Olá ano, mês, dia e hora do SliceStart em separado variáveis que são utilizadas por Olá **folderPath** e **fileName** propriedades.</span><span class="sxs-lookup"><span data-stu-id="41d17-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="41d17-240">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="41d17-240">Copy activity properties</span></span>
<span data-ttu-id="41d17-241">Para uma lista completa das secções e propriedades disponíveis para definir as atividades, consulte [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="41d17-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="41d17-242">Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="41d17-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="41d17-243">Propriedades disponíveis nos Olá **typeProperties** secção Olá atividade, no Olá por outro lado, variar de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="41d17-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="41d17-244">Para a atividade de cópia de Olá, propriedades do tipo Olá variam consoante os tipos de origens e sinks Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="41d17-245">Na atividade de cópia, quando a origem de Olá é do tipo **FileSystemSource**, Olá seguinte propriedade está disponível no **typeProperties** secção:</span><span class="sxs-lookup"><span data-stu-id="41d17-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="41d17-246">Propriedade</span><span class="sxs-lookup"><span data-stu-id="41d17-246">Property</span></span> | <span data-ttu-id="41d17-247">Descrição</span><span class="sxs-lookup"><span data-stu-id="41d17-247">Description</span></span> | <span data-ttu-id="41d17-248">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="41d17-248">Allowed values</span></span> | <span data-ttu-id="41d17-249">Necessário</span><span class="sxs-lookup"><span data-stu-id="41d17-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="41d17-250">Recursiva</span><span class="sxs-lookup"><span data-stu-id="41d17-250">recursive</span></span> |<span data-ttu-id="41d17-251">Indica se Olá é ler dados em modo recursivo de subpastas hello, ou apenas a partir da pasta especificada Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="41d17-252">TRUE, False (predefinição)</span><span class="sxs-lookup"><span data-stu-id="41d17-252">True, False (default)</span></span> |<span data-ttu-id="41d17-253">Não</span><span class="sxs-lookup"><span data-stu-id="41d17-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="41d17-254">Exemplo JSON: copiar dados do servidor FTP tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="41d17-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="41d17-255">Este exemplo mostra como toocopy dados a partir de um tooAzure de servidor FTP armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="41d17-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="41d17-256">No entanto, é possível copiar dados diretamente tooany de Olá sinks Olá declarado no [arquivos de dados e formatos suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats), utilizando a atividade de cópia de Olá na fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="41d17-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="41d17-257">Olá exemplos seguintes fornecem definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="41d17-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="41d17-258">Um serviço ligado do tipo [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="41d17-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="41d17-259">Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="41d17-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="41d17-260">Uma entrada [dataset](data-factory-create-datasets.md) do tipo [partilha de ficheiros](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="41d17-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="41d17-261">Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="41d17-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="41d17-262">A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="41d17-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="41d17-263">exemplo de Olá copia dados a partir de um tooan de servidor FTP BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="41d17-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="41d17-264">Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="41d17-265">Serviço ligado de FTP</span><span class="sxs-lookup"><span data-stu-id="41d17-265">FTP linked service</span></span>

<span data-ttu-id="41d17-266">Este exemplo utiliza a autenticação básica, com o nome de utilizador de Olá e a palavra-passe em texto simples.</span><span class="sxs-lookup"><span data-stu-id="41d17-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="41d17-267">Também pode utilizar um dos Olá seguintes formas:</span><span class="sxs-lookup"><span data-stu-id="41d17-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="41d17-268">Autenticação anónima</span><span class="sxs-lookup"><span data-stu-id="41d17-268">Anonymous authentication</span></span>
* <span data-ttu-id="41d17-269">Autenticação básica com credenciais encriptado</span><span class="sxs-lookup"><span data-stu-id="41d17-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="41d17-270">FTP por SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="41d17-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="41d17-271">Consulte Olá [serviço ligado de FTP](#linked-service-properties) secção para diferentes tipos de autenticação, pode utilizar.</span><span class="sxs-lookup"><span data-stu-id="41d17-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="41d17-272">Serviço ligado do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="41d17-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="41d17-273">Conjunto de dados de entrada de FTP</span><span class="sxs-lookup"><span data-stu-id="41d17-273">FTP input dataset</span></span>

<span data-ttu-id="41d17-274">Este conjunto de dados refere-se a pasta de toohello FTP `mysharedfolder` e ficheiro `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="41d17-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="41d17-275">Olá pipeline cópias Olá toohello o destino de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="41d17-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="41d17-276">Definição **externo** demasiado**verdadeiro** informa o serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="41d17-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="41d17-277">Conjunto de dados de saída do Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="41d17-277">Azure Blob output dataset</span></span>

<span data-ttu-id="41d17-278">São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="41d17-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="41d17-279">caminho da pasta Olá para BLOBs Olá é avaliado dinamicamente, com base na hora de início de Olá do setor de Olá que está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="41d17-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="41d17-280">caminho da pasta Olá utiliza as partes de ano, mês, dia e horas Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="41d17-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="41d17-281">Uma atividade de cópia num pipeline com o sink de origem e de blob do sistema de ficheiros</span><span class="sxs-lookup"><span data-stu-id="41d17-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="41d17-282">Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída, não sendo toorun agendada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="41d17-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="41d17-283">No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**FileSystemSource**e Olá **sink** tipo está definido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="41d17-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="41d17-284">colunas de toomap toocolumns de conjunto de dados de origem do conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="41d17-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41d17-285">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="41d17-285">Next steps</span></span>
<span data-ttu-id="41d17-286">Consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="41d17-286">See hello following articles:</span></span>

* <span data-ttu-id="41d17-287">toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Factory de dados e várias formas toooptimize-lo, consulte Olá [copiar guia Otimização e de desempenho de atividade](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="41d17-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="41d17-288">Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="41d17-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
