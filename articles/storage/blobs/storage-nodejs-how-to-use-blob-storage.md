---
title: aaaHow toouse Blob storage do Node.js | Microsoft Docs
description: "Armazene dados não estruturados na nuvem de Olá Blob Storage do Azure (armazenamento de objetos)."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="d374c-103">Como toouse Blob storage do Node.js</span><span class="sxs-lookup"><span data-stu-id="d374c-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="d374c-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="d374c-104">Overview</span></span>
<span data-ttu-id="d374c-105">Este artigo mostra como tooperform cenários comuns utilizando o Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d374c-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="d374c-106">Exemplos de Olá são escritos através do Olá Node.js API.</span><span class="sxs-lookup"><span data-stu-id="d374c-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="d374c-107">cenários de Olá abrangidos incluem como tooupload, listar, transferir e eliminar blobs.</span><span class="sxs-lookup"><span data-stu-id="d374c-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="d374c-108">Criar uma aplicação Node.js</span><span class="sxs-lookup"><span data-stu-id="d374c-108">Create a Node.js application</span></span>
<span data-ttu-id="d374c-109">Para obter instruções sobre como toocreate uma aplicação Node.js, consulte [criar uma aplicação de web de Node.js no App Service do Azure], [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) – com o Windows PowerShell, ou [compilar e implementar uma aplicação de web Node.js tooAzure utilizando a Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="d374c-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="d374c-110">Configurar o armazenamento de tooaccess de aplicação</span><span class="sxs-lookup"><span data-stu-id="d374c-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="d374c-111">toouse storage do Azure, terá de Olá SDK de armazenamento do Azure para Node.js, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="d374c-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="d374c-112">Utilizar o Gestor de pacote de nó (NPM) tooobtain Olá pacote</span><span class="sxs-lookup"><span data-stu-id="d374c-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="d374c-113">Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), toonavigate toohello pasta onde criou o seu exemplo aplicação.</span><span class="sxs-lookup"><span data-stu-id="d374c-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="d374c-114">Tipo **npm instalar storage do azure** na janela de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="d374c-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="d374c-115">O resultado do comando de Olá é semelhante toohello seguinte exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="d374c-115">Output from hello command is similar toohello following code example.</span></span>

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="d374c-116">Pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="d374c-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="d374c-117">Dentro dessa pasta, determinar Olá **storage do azure** pacote, que contém as bibliotecas de Olá que necessita de armazenamento tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d374c-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="d374c-118">Importar o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="d374c-118">Import hello package</span></span>
<span data-ttu-id="d374c-119">Utilizar o bloco de notas ou noutro editor de texto, adicionar Olá seguir toohello superior de Olá **server.js** ficheiro da aplicação olá onde pretende toouse armazenamento:</span><span class="sxs-lookup"><span data-stu-id="d374c-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="d374c-120">Configurar uma ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d374c-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="d374c-121">Olá módulo do Azure será lida a variáveis de ambiente de Olá `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY`, ou `AZURE_STORAGE_CONNECTION_STRING`, para as informações necessárias tooconnect tooyour conta de armazenamento Azure.</span><span class="sxs-lookup"><span data-stu-id="d374c-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="d374c-122">Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações da conta Olá ao chamar **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="d374c-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="d374c-123">Para obter um exemplo de definir variáveis de ambiente de Olá na Olá [portal do Azure](https://portal.azure.com) para uma aplicação web do Azure, consulte [através da aplicação de web de Node.js Olá o serviço de tabela do Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="d374c-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="d374c-124">Criar um contentor</span><span class="sxs-lookup"><span data-stu-id="d374c-124">Create a container</span></span>
<span data-ttu-id="d374c-125">Olá **BlobService** objeto permite-lhe trabalhar com blobs e contentores.</span><span class="sxs-lookup"><span data-stu-id="d374c-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="d374c-126">Olá código seguinte cria um **BlobService** objeto.</span><span class="sxs-lookup"><span data-stu-id="d374c-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="d374c-127">Adicione Olá seguinte perto da parte superior Olá **server.js**:</span><span class="sxs-lookup"><span data-stu-id="d374c-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="d374c-128">Pode aceder anonimamente um blob utilizando **createBlobServiceAnonymous** e fornecer o endereço do anfitrião Olá.</span><span class="sxs-lookup"><span data-stu-id="d374c-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="d374c-129">Por exemplo, utilizar `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="d374c-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="d374c-130">toocreate um novo contentor, utilize **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="d374c-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="d374c-131">Olá exemplo de código seguinte cria um novo contentor designado 'mycontainer':</span><span class="sxs-lookup"><span data-stu-id="d374c-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="d374c-132">Se o contentor de Olá é criado recentemente, `result.created` é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="d374c-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="d374c-133">Se já existir um contentor de Olá, `result.created` é falso.</span><span class="sxs-lookup"><span data-stu-id="d374c-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="d374c-134">`response`contém informações sobre a operação de Olá, incluindo Olá ETag informações para o contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="d374c-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="d374c-135">Segurança de contentor</span><span class="sxs-lookup"><span data-stu-id="d374c-135">Container security</span></span>
<span data-ttu-id="d374c-136">Por predefinição, os novos contentores são privados e não podem ser acedidos anonimamente.</span><span class="sxs-lookup"><span data-stu-id="d374c-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="d374c-137">contentor de Olá toomake pública para que possam aceder anonimamente, pode definir o nível de acesso de um contentor Olá demasiado**blob** ou **contentor**.</span><span class="sxs-lookup"><span data-stu-id="d374c-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="d374c-138">**blob** -permite o acesso de leitura anónimo tooblob conteúdo e metadados dentro neste contentor, mas não toocontainer metadados, tais como listar todos os blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="d374c-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="d374c-139">**contentor** -permite o acesso de leitura anónimo tooblob conteúdo e metadados, bem como metadados do contentor</span><span class="sxs-lookup"><span data-stu-id="d374c-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="d374c-140">Olá exemplo de código seguinte demonstra um nível de acesso Olá definição demasiado**blob**:</span><span class="sxs-lookup"><span data-stu-id="d374c-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="d374c-141">Em alternativa, pode modificar o nível de acesso de Olá de um contentor utilizando **setContainerAcl** nível de acesso de Olá toospecify.</span><span class="sxs-lookup"><span data-stu-id="d374c-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="d374c-142">toocontainer ao nível do exemplo alterações Olá acesso de código seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="d374c-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="d374c-143">Olá resultado contém informações sobre a operação de Olá, incluindo Olá atual **ETag** para o contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="d374c-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="d374c-144">Filtros</span><span class="sxs-lookup"><span data-stu-id="d374c-144">Filters</span></span>
<span data-ttu-id="d374c-145">Pode aplicar opcional filtragem operações toooperations efetuada utilizando **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="d374c-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="d374c-146">Operações de filtragem pode incluir registo automaticamente repetir, etc. Os filtros são objetos que implementam um método com assinatura de Olá:</span><span class="sxs-lookup"><span data-stu-id="d374c-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="d374c-147">Depois de efetuar a respetiva pré-processamentos nas opções de pedido de Olá, Olá método necessita toocall "seguinte", transmitir uma chamada de retorno com Olá assinatura os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d374c-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="d374c-148">Esta chamada de retorno e após o processamento Olá returnObject (resposta de hello do servidor de toohello Olá pedido), a chamada de retorno de Olá tem tooeither invocar em seguida, se existir toocontinue outros filtros de processamento ou simplesmente invocar o serviço de Olá finalCallback tooend invocação.</span><span class="sxs-lookup"><span data-stu-id="d374c-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="d374c-149">Dois filtros que implementa lógica de repetição são incluídos com Olá Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="d374c-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="d374c-150">seguinte Olá cria um **BlobService** objeto que utiliza Olá **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="d374c-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d374c-151">Carregar um blob para um contentor</span><span class="sxs-lookup"><span data-stu-id="d374c-151">Upload a blob into a container</span></span>
<span data-ttu-id="d374c-152">Existem três tipos de blobs: blobs de blocos, blobs de páginas e blobs de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="d374c-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="d374c-153">Os blobs de blocos permitem-lhe toomore eficientemente carregar dados de grandes dimensões.</span><span class="sxs-lookup"><span data-stu-id="d374c-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="d374c-154">Acrescentar blobs estão otimizados para operações de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="d374c-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="d374c-155">Os blobs de página estão otimizados para operações de leitura/escrita.</span><span class="sxs-lookup"><span data-stu-id="d374c-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="d374c-156">Para obter mais informações, consulte [compreender os Blobs de blocos, os Blobs de acréscimo e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="d374c-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="d374c-157">Blobs de bloco</span><span class="sxs-lookup"><span data-stu-id="d374c-157">Block blobs</span></span>
<span data-ttu-id="d374c-158">blob de bloco de tooa por dados tooupload, Olá utilize os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d374c-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="d374c-159">**createBlockBlobFromLocalFile** - cria um novo blob de bloco e carrega Olá conteúdo de um ficheiro</span><span class="sxs-lookup"><span data-stu-id="d374c-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="d374c-160">**createBlockBlobFromStream** - cria um novo blob de bloco e carrega o conteúdo de Olá de um fluxo</span><span class="sxs-lookup"><span data-stu-id="d374c-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="d374c-161">**createBlockBlobFromText** - cria um novo blob de bloco e carrega o conteúdo de Olá de uma cadeia</span><span class="sxs-lookup"><span data-stu-id="d374c-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="d374c-162">**createWriteStreamToBlockBlob** -fornece um blob de bloco de tooa de fluxo de escrita</span><span class="sxs-lookup"><span data-stu-id="d374c-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="d374c-163">Olá exemplo de código seguinte carrega conteúdo Olá Olá **test.txt** de ficheiros para **myblob**.</span><span class="sxs-lookup"><span data-stu-id="d374c-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="d374c-164">Olá `result` devolvido por estes métodos contém informações sobre a operação de Olá, tais como Olá **ETag** do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="d374c-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="d374c-165">Blobs de acréscimo</span><span class="sxs-lookup"><span data-stu-id="d374c-165">Append blobs</span></span>
<span data-ttu-id="d374c-166">tooupload dados tooa novo blob de acréscimo, utilize Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="d374c-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="d374c-167">**createAppendBlobFromLocalFile** - cria um novo blob de acréscimo e carrega Olá conteúdo de um ficheiro</span><span class="sxs-lookup"><span data-stu-id="d374c-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="d374c-168">**createAppendBlobFromStream** - cria um novo blob de acréscimo e carrega o conteúdo de Olá de um fluxo</span><span class="sxs-lookup"><span data-stu-id="d374c-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="d374c-169">**createAppendBlobFromText** - cria um novo blob de acréscimo e carrega o conteúdo de Olá de uma cadeia</span><span class="sxs-lookup"><span data-stu-id="d374c-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="d374c-170">**createWriteStreamToNewAppendBlob** - cria um novo blob de acréscimo e, em seguida, fornece uma tooit toowrite de fluxo</span><span class="sxs-lookup"><span data-stu-id="d374c-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="d374c-171">Olá exemplo de código seguinte carrega conteúdo Olá Olá **test.txt** de ficheiros para **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="d374c-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="d374c-172">tooappend existente de tooan um bloco acrescentar blob, Olá utilize os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d374c-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="d374c-173">**appendFromLocalFile** -acrescentar conteúdo Olá de um ficheiro tooan existente Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="d374c-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="d374c-174">**appendFromStream** -acrescentar conteúdo Olá de um fluxo tooan existente Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="d374c-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="d374c-175">**appendFromText** -acrescentar conteúdo Olá de uma cadeia tooan existente Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="d374c-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="d374c-176">**appendBlockFromStream** -acrescentar conteúdo Olá de um fluxo tooan existente Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="d374c-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="d374c-177">**appendBlockFromText** -acrescentar conteúdo Olá de uma cadeia tooan existente Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="d374c-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="d374c-178">appendFromXXX APIs irá efetuar algumas chamadas de servidor desnecessários do lado do cliente validação toofail tooavoid rápida.</span><span class="sxs-lookup"><span data-stu-id="d374c-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="d374c-179">appendBlockFromXXX não.</span><span class="sxs-lookup"><span data-stu-id="d374c-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="d374c-180">Olá exemplo de código seguinte carrega conteúdo Olá Olá **test.txt** de ficheiros para **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="d374c-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="d374c-181">Blobs de páginas</span><span class="sxs-lookup"><span data-stu-id="d374c-181">Page blobs</span></span>
<span data-ttu-id="d374c-182">blob de páginas de tooa por dados tooupload, Olá utilize os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d374c-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="d374c-183">**createPageBlob** -cria um novo blob de página com um comprimento específico</span><span class="sxs-lookup"><span data-stu-id="d374c-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="d374c-184">**createPageBlobFromLocalFile** - cria um novo blob de página e carrega Olá conteúdo de um ficheiro</span><span class="sxs-lookup"><span data-stu-id="d374c-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="d374c-185">**createPageBlobFromStream** - cria um novo blob de página e carrega o conteúdo de Olá de um fluxo</span><span class="sxs-lookup"><span data-stu-id="d374c-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="d374c-186">**createWriteStreamToExistingPageBlob** -fornece um blob de página existente do escrita fluxo tooan</span><span class="sxs-lookup"><span data-stu-id="d374c-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="d374c-187">**createWriteStreamToNewPageBlob** - cria um novo blob de página e, em seguida, fornece uma tooit toowrite de fluxo</span><span class="sxs-lookup"><span data-stu-id="d374c-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="d374c-188">Olá exemplo de código seguinte carrega conteúdo Olá Olá **test.txt** de ficheiros para **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="d374c-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="d374c-189">Os blobs de páginas consistem de 512 bytes 'páginas'.</span><span class="sxs-lookup"><span data-stu-id="d374c-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="d374c-190">Receberá um erro ao carregar dados com um tamanho que não é um múltiplo de 512.</span><span class="sxs-lookup"><span data-stu-id="d374c-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="d374c-191">Lista Olá blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="d374c-191">List hello blobs in a container</span></span>
<span data-ttu-id="d374c-192">os blobs de Olá toolist num contentor, utilize Olá **listBlobsSegmented** método.</span><span class="sxs-lookup"><span data-stu-id="d374c-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="d374c-193">Se gostaria de blobs de tooreturn com um prefixo específico, utilize **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="d374c-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="d374c-194">Olá `result` contém um `entries` coleção, o que é uma matriz de objetos que descrevem cada blob.</span><span class="sxs-lookup"><span data-stu-id="d374c-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="d374c-195">Se não não possível devolver todos os blobs, Olá `result` também fornece um `continuationToken`, que pode ser utilizado como Olá segundo parâmetro tooretrieve entradas adicionais.</span><span class="sxs-lookup"><span data-stu-id="d374c-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="d374c-196">Transferir blobs</span><span class="sxs-lookup"><span data-stu-id="d374c-196">Download blobs</span></span>
<span data-ttu-id="d374c-197">dados toodownload de um blob, utilize o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="d374c-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="d374c-198">**getBlobToLocalFile** -escreve toofile de conteúdo de blob Olá</span><span class="sxs-lookup"><span data-stu-id="d374c-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="d374c-199">**getBlobToStream** -escreve o fluxo de tooa de conteúdo de blob Olá</span><span class="sxs-lookup"><span data-stu-id="d374c-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="d374c-200">**getBlobToText** -escreve conteúdos do blob Olá tooa cadeia</span><span class="sxs-lookup"><span data-stu-id="d374c-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="d374c-201">**createReadStream** -fornece uma tooread fluxo a partir do blob Olá</span><span class="sxs-lookup"><span data-stu-id="d374c-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="d374c-202">Olá exemplo de código seguinte demonstra utilizando **getBlobToStream** conteúdo Olá toodownload Olá **myblob** blob e armazená-las toohello **output.txt** ficheiros utilizando um sequência:</span><span class="sxs-lookup"><span data-stu-id="d374c-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="d374c-203">Olá `result` contém informações sobre blob Olá, incluindo **ETag** informações.</span><span class="sxs-lookup"><span data-stu-id="d374c-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="d374c-204">Eliminar um blob</span><span class="sxs-lookup"><span data-stu-id="d374c-204">Delete a blob</span></span>
<span data-ttu-id="d374c-205">Por fim, toodelete um blob, chamar **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="d374c-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="d374c-206">Olá seguinte exemplo de código elimina Olá blob com o nome **myblob**.</span><span class="sxs-lookup"><span data-stu-id="d374c-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="d374c-207">Acesso simultâneo</span><span class="sxs-lookup"><span data-stu-id="d374c-207">Concurrent access</span></span>
<span data-ttu-id="d374c-208">toosupport acesso simultâneo tooa blob a partir da vários clientes ou de múltiplas instâncias do processo, pode utilizar **ETags** ou **concessões**.</span><span class="sxs-lookup"><span data-stu-id="d374c-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="d374c-209">**ETag** -fornece uma forma toodetect que Olá blob ou contentor foi modificado por outro processo</span><span class="sxs-lookup"><span data-stu-id="d374c-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="d374c-210">**Concessão** - fornece uma forma tooobtain exclusivo, renováveis, operação de escrita ou eliminar o blob de tooa de acesso para um período de tempo</span><span class="sxs-lookup"><span data-stu-id="d374c-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="d374c-211">ETag</span><span class="sxs-lookup"><span data-stu-id="d374c-211">ETag</span></span>
<span data-ttu-id="d374c-212">Utilize ETags se precisar de tooallow vários clientes ou instâncias toowrite toohello bloco Blob de página ou Blob em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="d374c-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="d374c-213">Olá ETag permite-lhe toodetermine se hello contentor ou um blob foi modificada uma vez que inicialmente ler ou criou, permitindo-lhe tooavoid substituir alterações consolidadas por outro processo ou cliente.</span><span class="sxs-lookup"><span data-stu-id="d374c-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="d374c-214">Pode definir condições de ETag utilizando Olá opcional `options.accessConditions` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d374c-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="d374c-215">Olá exemplo de código seguinte apenas carrega Olá **test.txt** ficheiro se blob Olá já existe e tem um valor ETag Olá contido `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="d374c-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="d374c-216">Quando estiver a utilizar ETags, padrão geral Olá é:</span><span class="sxs-lookup"><span data-stu-id="d374c-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="d374c-217">Obter Olá ETag como resultado de Olá de uma operação get, a lista ou a criar.</span><span class="sxs-lookup"><span data-stu-id="d374c-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="d374c-218">Efetuar uma ação, a verificação que Olá valor ETag não foi modificada.</span><span class="sxs-lookup"><span data-stu-id="d374c-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="d374c-219">Se o valor de Olá foi modificado, indica que o se outra instância ou cliente modificadas blob Olá ou contentor, uma vez que obteve valor ETag de Olá.</span><span class="sxs-lookup"><span data-stu-id="d374c-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="d374c-220">Concessão</span><span class="sxs-lookup"><span data-stu-id="d374c-220">Lease</span></span>
<span data-ttu-id="d374c-221">Pode adquirir uma concessão de novo utilizando Olá **acquireLease** método, especificando blob Olá ou contentor que pretende tooobtain uma concessão no.</span><span class="sxs-lookup"><span data-stu-id="d374c-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="d374c-222">Por exemplo, Olá seguinte código adquire uma concessão no **myblob**.</span><span class="sxs-lookup"><span data-stu-id="d374c-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="d374c-223">Operações subsequentes no **myblob** tem de fornecer Olá `options.leaseId` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d374c-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="d374c-224">concessão de Olá ID é devolvido como `result.id` de **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="d374c-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="d374c-225">Por predefinição, a duração da concessão Olá é infinita.</span><span class="sxs-lookup"><span data-stu-id="d374c-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="d374c-226">Pode especificar um período de tempo infinito não (entre 15 e 60 segundos), fornecendo Olá `options.leaseDuration` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d374c-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="d374c-227">utilizar tooremove uma concessão **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="d374c-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="d374c-228">toobreak uma concessão, impedir a outras pessoas, mas a partir de obter uma concessão novo até duração original Olá expirou, utilize **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="d374c-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="d374c-229">Trabalhar com assinaturas de acesso partilhado</span><span class="sxs-lookup"><span data-stu-id="d374c-229">Work with shared access signatures</span></span>
<span data-ttu-id="d374c-230">Assinaturas de acesso partilhado (SAS) são uma tooblobs de acesso granulares de tooprovide de forma segura e contentores sem fornecer o nome da conta de armazenamento ou chaves.</span><span class="sxs-lookup"><span data-stu-id="d374c-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="d374c-231">Assinaturas de acesso partilhado são frequentemente utilizados tooprovide limitada para aceder a dados tooyour, tais como permitir que uma aplicação móvel tooaccess blobs.</span><span class="sxs-lookup"><span data-stu-id="d374c-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="d374c-232">Enquanto pode também autorizar o acesso anónimo tooblobs, assinaturas de acesso partilhado permitem-lhe acesso tooprovide mais controlado, como tem de gerar Olá SAS.</span><span class="sxs-lookup"><span data-stu-id="d374c-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="d374c-233">Uma aplicação como um serviço baseado na nuvem fidedigna gera assinaturas de acesso partilhado com Olá **generateSharedAccessSignature** de Olá **BlobService**e fornece-tooan não fidedigno ou fidedigna por aplicação, tais como uma aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="d374c-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="d374c-234">Acesso partilhado assinaturas são geradas através de uma política, que descreve o início de Olá e datas final durante o qual Olá assinaturas de acesso partilhado são válidas, assim como Olá aceder nível titular de assinaturas de acesso partilhado do toohello concedida.</span><span class="sxs-lookup"><span data-stu-id="d374c-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="d374c-235">Olá exemplo de código seguinte gera uma nova política de acesso partilhado, o que permite Olá as operações de leitura tooperform de marcador de posição de assinaturas de acesso de Olá partilhado **myblob** blob e expira 100 minutos após a hora de Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="d374c-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="d374c-236">Tenha em atenção que as informações do anfitrião Olá têm de ser fornecidos também, conforme necessário, quando marcador de posição de assinaturas de acesso partilhado de Olá tenta contentor de Olá tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d374c-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="d374c-237">Olá, em seguida, a aplicação de cliente utiliza assinaturas de acesso partilhado com **BlobServiceWithSAS** tooperform operações contra blob Olá.</span><span class="sxs-lookup"><span data-stu-id="d374c-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="d374c-238">Olá seguinte obtém as informações **myblob**.</span><span class="sxs-lookup"><span data-stu-id="d374c-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="d374c-239">Uma vez que as assinaturas de acesso partilhado de Olá foram geradas com acesso só de leitura, se for feita uma tentativa de blob de Olá toomodify, será devolvido um erro.</span><span class="sxs-lookup"><span data-stu-id="d374c-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="d374c-240">Lista de controlo de acesso</span><span class="sxs-lookup"><span data-stu-id="d374c-240">Access control lists</span></span>
<span data-ttu-id="d374c-241">Também pode utilizar uma política de acesso do acesso Controlo lista (ACL) tooset Olá para SAS.</span><span class="sxs-lookup"><span data-stu-id="d374c-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="d374c-242">Isto é útil se desejar tooallow vários clientes tooaccess um contentor, mas fornecem as políticas de acesso diferentes para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="d374c-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="d374c-243">Uma ACL é implementada com uma matriz de políticas de acesso, com um ID associado a cada política.</span><span class="sxs-lookup"><span data-stu-id="d374c-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="d374c-244">Olá seguinte exemplo de código define duas políticas, uma para 'user1' e outra para 'Utilizador2':</span><span class="sxs-lookup"><span data-stu-id="d374c-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="d374c-245">Olá seguinte obtém de exemplo de código Olá ACL atual para **mycontainer**e, em seguida, adiciona novas políticas de Olá utilizando **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="d374c-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="d374c-246">Esta abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="d374c-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="d374c-247">Uma vez Olá que ACL é definida, pode, em seguida, criar com base no ID de Olá para uma política de assinaturas de acesso partilhado.</span><span class="sxs-lookup"><span data-stu-id="d374c-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="d374c-248">Olá seguinte exemplo de código cria novas assinaturas de acesso partilhado para 'Utilizador2':</span><span class="sxs-lookup"><span data-stu-id="d374c-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="d374c-249">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d374c-249">Next steps</span></span>
<span data-ttu-id="d374c-250">Para obter mais informações, consulte Olá os seguintes recursos.</span><span class="sxs-lookup"><span data-stu-id="d374c-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="d374c-251">[Storage do azure SDK para o nó a referência da API] [Storage do azure SDK para o nó a referência da API]</span><span class="sxs-lookup"><span data-stu-id="d374c-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="d374c-252">[Blogue da equipa de armazenamento do azure] [Blogue da equipa de armazenamento do azure]</span><span class="sxs-lookup"><span data-stu-id="d374c-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="d374c-253">[SDK de armazenamento do Azure para o nó] [ Azure Storage SDK for Node] repositório no GitHub</span><span class="sxs-lookup"><span data-stu-id="d374c-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="d374c-254">Centro para Programadores do Node.js</span><span class="sxs-lookup"><span data-stu-id="d374c-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="d374c-255">Transferência de dados com Olá utilitário de linha de comandos AzCopy</span><span class="sxs-lookup"><span data-stu-id="d374c-255">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="d374c-256">[Aplicação de web do node.js utilizando Olá serviço de tabela do Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="d374c-256">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="d374c-257">[Criar e implementar uma aplicação de web Node.js tooAzure utilizando a Web Matrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="d374c-257">[Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="d374c-258">[Utilizando Olá REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [portal do Azure]: https://portal.azure.com [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [blogue da equipa de armazenamento do Azure]: http:// blogs.msdn.com/b/windowsazurestorage/ [Storage do Azure SDK para o nó a referência da API]: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="d374c-258">[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
