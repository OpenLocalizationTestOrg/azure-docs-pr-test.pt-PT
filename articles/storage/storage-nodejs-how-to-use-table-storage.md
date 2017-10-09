---
title: aaaHow toouse Table storage do Azure do Node.js | Microsoft Docs
description: "Armazene dados estruturados na nuvem de Olá utilizando o Table storage do Azure, um arquivo de dados NoSQL."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="06815-103">Como toouse Table storage do Azure do Node.js</span><span class="sxs-lookup"><span data-stu-id="06815-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="06815-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="06815-104">Overview</span></span>
<span data-ttu-id="06815-105">Este tópico mostra como tooperform cenários comuns utilizando Olá tabelas do Azure service numa aplicação Node.js.</span><span class="sxs-lookup"><span data-stu-id="06815-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="06815-106">Exemplos de código Olá neste tópico partem do princípio de que já tem uma aplicação Node.js.</span><span class="sxs-lookup"><span data-stu-id="06815-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="06815-107">Para obter informações sobre como toocreate uma aplicação Node.js no Azure, consulte qualquer um dos seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="06815-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="06815-108">Criar uma aplicação web Node.js no App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="06815-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="06815-109">Criar e implementar uma aplicação de web Node.js tooAzure com o WebMatrix</span><span class="sxs-lookup"><span data-stu-id="06815-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="06815-110">[Criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (através do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="06815-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="06815-111">Configurar a sua aplicação tooaccess Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="06815-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="06815-112">toouse Storage do Azure, terá de Olá SDK de armazenamento do Azure para Node.js, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="06815-113">Utilizar o Gestor de pacote de nó (NPM) tooinstall Olá pacote</span><span class="sxs-lookup"><span data-stu-id="06815-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="06815-114">Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix) e navegue pasta toohello onde criou a aplicação.</span><span class="sxs-lookup"><span data-stu-id="06815-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="06815-115">Tipo **npm instalar storage do azure** na janela de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="06815-116">O resultado do comando de Olá é semelhante toohello seguinte o exemplo.</span><span class="sxs-lookup"><span data-stu-id="06815-116">Output from hello command is similar toohello following example.</span></span>

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
3. <span data-ttu-id="06815-117">Pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="06815-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="06815-118">Dentro dessa pasta encontrará Olá **storage do azure** pacote, que contém as bibliotecas de Olá necessita de armazenamento tooaccess.</span><span class="sxs-lookup"><span data-stu-id="06815-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="06815-119">Importar o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="06815-119">Import hello package</span></span>
<span data-ttu-id="06815-120">Adicionar Olá seguinte código toohello parte superior Olá **server.js** ficheiros na sua aplicação:</span><span class="sxs-lookup"><span data-stu-id="06815-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="06815-121">Configurar uma ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="06815-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="06815-122">módulo Olá do azure será lida a variáveis de ambiente de Olá AZURE\_armazenamento\_conta e o AZURE\_armazenamento\_acesso\_chave ou o AZURE\_armazenamento\_ligação \_Cadeia de informações necessárias tooconnect tooyour conta do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="06815-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="06815-123">Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações da conta Olá ao chamar **TableService**.</span><span class="sxs-lookup"><span data-stu-id="06815-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="06815-124">Para obter um exemplo de definir variáveis de ambiente de Olá na Olá [portal do Azure](https://portal.azure.com) para um Web site do Azure, consulte [através da aplicação de web de Node.js Olá o serviço de tabela do Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="06815-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="06815-125">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="06815-125">Create a table</span></span>
<span data-ttu-id="06815-126">Olá código seguinte cria um **TableService** objeto e utiliza-toocreate uma nova tabela.</span><span class="sxs-lookup"><span data-stu-id="06815-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="06815-127">Adicione Olá seguinte perto da parte superior Olá **server.js**.</span><span class="sxs-lookup"><span data-stu-id="06815-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="06815-128">Olá chamada demasiado**createTableIfNotExists** criará uma nova tabela com o nome especificado Olá se já existir.</span><span class="sxs-lookup"><span data-stu-id="06815-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="06815-129">Olá exemplo seguinte cria uma nova tabela com o nome 'mytable' se já existir:</span><span class="sxs-lookup"><span data-stu-id="06815-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="06815-130">Olá `result.created` será `true` se for criada uma nova tabela, e `false` se Olá tabela já existe.</span><span class="sxs-lookup"><span data-stu-id="06815-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="06815-131">Olá `response` contêm informações sobre o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="06815-132">Filtros</span><span class="sxs-lookup"><span data-stu-id="06815-132">Filters</span></span>
<span data-ttu-id="06815-133">As operações de filtragem opcionais podem ser aplicados toooperations efetuada utilizando **TableService**.</span><span class="sxs-lookup"><span data-stu-id="06815-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="06815-134">Operações de filtragem pode incluir registo automaticamente repetir, etc. Os filtros são objetos que implementam um método com assinatura de Olá:</span><span class="sxs-lookup"><span data-stu-id="06815-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="06815-135">Depois de efetuar a respetiva pré-processamentos nas opções de pedido de Olá, Olá método necessita toocall "seguinte", transmitir uma chamada de retorno com Olá assinatura os seguintes:</span><span class="sxs-lookup"><span data-stu-id="06815-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="06815-136">Esta chamada de retorno e após o processamento Olá returnObject (resposta de hello do servidor de toohello Olá pedido), a chamada de retorno de Olá tem tooeither invocar em seguida, se existir toocontinue outros filtros de processamento ou simplesmente invocar finalCallback; caso contrário, tooend Olá invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="06815-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="06815-137">Dois filtros que implementa lógica de repetição são incluídos com Olá Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="06815-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="06815-138">seguinte Olá cria um **TableService** objeto que utiliza Olá **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="06815-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="06815-139">Adicionar uma tabela de tooa entidade</span><span class="sxs-lookup"><span data-stu-id="06815-139">Add an entity tooa table</span></span>
<span data-ttu-id="06815-140">tooadd uma entidade, primeiro crie um objeto que define as propriedades de entidade.</span><span class="sxs-lookup"><span data-stu-id="06815-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="06815-141">Todas as entidades tem de conter um **PartitionKey** e **RowKey**, que são identificadores exclusivos para a entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="06815-142">**PartitionKey** -determina partição Olá entidade Olá armazenados no</span><span class="sxs-lookup"><span data-stu-id="06815-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="06815-143">**RowKey** - exclusivamente identifica entidade Olá dentro de partição Olá</span><span class="sxs-lookup"><span data-stu-id="06815-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="06815-144">Ambos **PartitionKey** e **RowKey** tem de ser valores de cadeia.</span><span class="sxs-lookup"><span data-stu-id="06815-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="06815-145">Para obter mais informações, consulte [Olá compreender o modelo de dados do serviço tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="06815-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="06815-146">Olá segue-se um exemplo de definir uma entidade.</span><span class="sxs-lookup"><span data-stu-id="06815-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="06815-147">Tenha em atenção que **dueDate** está definido como um tipo de **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="06815-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="06815-148">Tipo de Olá especificação é opcional e tipos irão ser inferidos se não for especificados.</span><span class="sxs-lookup"><span data-stu-id="06815-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="06815-149">Há também um **Timestamp** campo para cada registo, o que é definido pelo Azure quando uma entidade é inserida ou atualizada.</span><span class="sxs-lookup"><span data-stu-id="06815-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="06815-150">Também pode utilizar Olá **entityGenerator** toocreate entidades.</span><span class="sxs-lookup"><span data-stu-id="06815-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="06815-151">Olá exemplo seguinte cria Olá mesma entidade de tarefas utilizando Olá **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="06815-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="06815-152">tooadd uma tabela de tooyour de entidade, transmitir toohello de objeto de entidade Olá **insertEntity** método.</span><span class="sxs-lookup"><span data-stu-id="06815-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="06815-153">Se a operação de Olá for bem-sucedida, `result` irá conter Olá [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) de Olá inserir o registo e `response` contêm informações sobre a operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="06815-154">Exemplo de resposta:</span><span class="sxs-lookup"><span data-stu-id="06815-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="06815-155">Por predefinição, **insertEntity** não devolve entidades Olá inserido como parte da Olá `response` informações.</span><span class="sxs-lookup"><span data-stu-id="06815-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="06815-156">Se planear efetuar outras operações nesta entidade ou informações de Olá toocache assim o desejar, pode ser útil toohave devolvido como parte da Olá `result`.</span><span class="sxs-lookup"><span data-stu-id="06815-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="06815-157">Pode fazê-lo ao ativar **echoContent** da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="06815-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="06815-158">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="06815-158">Update an entity</span></span>
<span data-ttu-id="06815-159">Existem vários métodos tooupdate de disponível uma entidade existente:</span><span class="sxs-lookup"><span data-stu-id="06815-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="06815-160">**replaceEntity** -atualizações de uma entidade existente, substituindo-la</span><span class="sxs-lookup"><span data-stu-id="06815-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="06815-161">**mergeEntity** -atualiza uma entidade existente, a intercalação novos valores de propriedade na entidade existente Olá</span><span class="sxs-lookup"><span data-stu-id="06815-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="06815-162">**insertOrReplaceEntity** -atualizações de uma entidade existente, substituindo-lo.</span><span class="sxs-lookup"><span data-stu-id="06815-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="06815-163">Se nenhuma entidade de existir, será inserido um novo</span><span class="sxs-lookup"><span data-stu-id="06815-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="06815-164">**insertOrMergeEntity** -atualiza uma entidade existente, a intercalação novos valores de propriedade para Olá existente.</span><span class="sxs-lookup"><span data-stu-id="06815-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="06815-165">Se nenhuma entidade de existir, será inserido um novo</span><span class="sxs-lookup"><span data-stu-id="06815-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="06815-166">Olá exemplo seguinte demonstra a atualizar uma entidade utilizando **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="06815-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="06815-167">Por predefinição, ao atualizar uma entidade não verifica toosee se dados Olá a ser atualizados anteriormente foi modificados por outro processo.</span><span class="sxs-lookup"><span data-stu-id="06815-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="06815-168">atualizações em simultâneo toosupport:</span><span class="sxs-lookup"><span data-stu-id="06815-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="06815-169">Obter Olá ETag do objeto de Olá a ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="06815-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="06815-170">Este é devolvido como parte da Olá `response` em nenhuma operação relacionada com entidade e podem ser recuperadas por meio `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="06815-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="06815-171">Quando efetuar uma operação de atualização numa entidade, adicionar Olá ETag obter as informações anteriormente toohello nova entidade.</span><span class="sxs-lookup"><span data-stu-id="06815-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="06815-172">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="06815-172">For example:</span></span>
>
>       <span data-ttu-id="06815-173">entity2 .etag ['.metadata'] = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="06815-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="06815-174">Efetue a operação de atualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-174">Perform hello update operation.</span></span> <span data-ttu-id="06815-175">Se a entidade de Olá foi modificada desde que obtida valor ETag de Olá, tais como outra instância da sua aplicação, um `error` vai ser devolvido a indicar que a condição de atualização de Olá especificada num pedido de Olá não foi cumprida.</span><span class="sxs-lookup"><span data-stu-id="06815-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="06815-176">Com **replaceEntity** e **mergeEntity**, se não existir entidade Olá que está a ser atualizada, em seguida, a operação de atualização de Olá irá falhar.</span><span class="sxs-lookup"><span data-stu-id="06815-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="06815-177">Por conseguinte, se desejar toostore uma entidade, independentemente de já existir, utilize **insertOrReplaceEntity** ou **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="06815-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="06815-178">Olá `result` para atualização bem sucedida operações irão conter Olá **Etag** de Olá atualizado entidade.</span><span class="sxs-lookup"><span data-stu-id="06815-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="06815-179">Trabalhar com grupos de entidades</span><span class="sxs-lookup"><span data-stu-id="06815-179">Work with groups of entities</span></span>
<span data-ttu-id="06815-180">Por vezes, faz sentido toosubmit várias operações em conjunto no tooensure batch atomic processados pelo servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="06815-181">tooaccomplish que, utilize Olá **TableBatch** toocreate um lote de classe e, em seguida, utilize Olá **executeBatch** método **TableService** tooperform Olá em lotes operações.</span><span class="sxs-lookup"><span data-stu-id="06815-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="06815-182">Olá seguinte exemplo mostra como submeter duas entidades no batch:</span><span class="sxs-lookup"><span data-stu-id="06815-182">hello following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="06815-183">Para operações de lote com êxito, `result` irá conter informações para cada operação no lote de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="06815-184">Trabalhar com operações em lote</span><span class="sxs-lookup"><span data-stu-id="06815-184">Work with batched operations</span></span>
<span data-ttu-id="06815-185">Operações adicionado tooa batch pode ser inspecionado visualizando Olá `operations` propriedade.</span><span class="sxs-lookup"><span data-stu-id="06815-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="06815-186">Também pode utilizar Olá toowork de métodos com operações os seguintes:</span><span class="sxs-lookup"><span data-stu-id="06815-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="06815-187">**Limpar** -limpa todas as operações do batch</span><span class="sxs-lookup"><span data-stu-id="06815-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="06815-188">**getOperations** -obtém uma operação do batch Olá</span><span class="sxs-lookup"><span data-stu-id="06815-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="06815-189">**hasOperations** -devolve true se o batch Olá contém operações</span><span class="sxs-lookup"><span data-stu-id="06815-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="06815-190">**removeOperations** -remove uma operação</span><span class="sxs-lookup"><span data-stu-id="06815-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="06815-191">**tamanho** -devolve Olá número de operações em lote de Olá</span><span class="sxs-lookup"><span data-stu-id="06815-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="06815-192">Obter uma entidade pela chave</span><span class="sxs-lookup"><span data-stu-id="06815-192">Retrieve an entity by key</span></span>
<span data-ttu-id="06815-193">tooreturn uma entidade específica com base no Olá **PartitionKey** e **RowKey**, utilize Olá **retrieveEntity** método.</span><span class="sxs-lookup"><span data-stu-id="06815-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="06815-194">Assim que esta operação for concluída, `result` irá conter a entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="06815-195">Consulta de um conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="06815-195">Query a set of entities</span></span>
<span data-ttu-id="06815-196">tooquery uma tabela, utilize Olá **TableQuery** objeto toobuild se uma expressão de consulta utilizando Olá cláusulas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="06815-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="06815-197">**Selecione** -Olá campos toobe devolvidas da consulta de Olá</span><span class="sxs-lookup"><span data-stu-id="06815-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="06815-198">**onde** - hello onde cláusula</span><span class="sxs-lookup"><span data-stu-id="06815-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="06815-199">**e** - um `and` onde condição</span><span class="sxs-lookup"><span data-stu-id="06815-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="06815-200">**ou** - um `or` onde condição</span><span class="sxs-lookup"><span data-stu-id="06815-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="06815-201">**parte superior** -Olá número de itens toofetch</span><span class="sxs-lookup"><span data-stu-id="06815-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="06815-202">Olá exemplo seguinte cria uma consulta que irá devolver Olá superiores cinco itens com uma PartitionKey 'hometasks'.</span><span class="sxs-lookup"><span data-stu-id="06815-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="06815-203">Uma vez que **selecione** não for utilizado, serão devolvidos todos os campos.</span><span class="sxs-lookup"><span data-stu-id="06815-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="06815-204">consulta de Olá tooperform contra uma tabela, utilize **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="06815-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="06815-205">Olá exemplo seguinte utiliza este entidades tooreturn de consulta de 'mytable'.</span><span class="sxs-lookup"><span data-stu-id="06815-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="06815-206">Se tiver êxito, `result.entries` irá conter uma matriz de entidades que correspondem à consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="06815-207">Se a consulta de Olá foi tooreturn não é possível todas as entidades, `result.continuationToken` será não -*nulo* e pode ser utilizado como Olá terceiro parâmetro de **queryEntities** tooretrieve mais resultados.</span><span class="sxs-lookup"><span data-stu-id="06815-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="06815-208">Para consulta inicial Olá, utilize *nulo* para o terceiro parâmetro de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="06815-209">Consultar um subconjunto de propriedades de entidade</span><span class="sxs-lookup"><span data-stu-id="06815-209">Query a subset of entity properties</span></span>
<span data-ttu-id="06815-210">Uma tabela de tooa de consulta pode obter alguns campos de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="06815-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="06815-211">Isto reduz a largura de banda e pode melhorar o desempenho de consulta, especialmente para entidades grandes.</span><span class="sxs-lookup"><span data-stu-id="06815-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="06815-212">Olá utilize **selecione** cláusula e passar nomes Olá de Olá campos toobe devolvido.</span><span class="sxs-lookup"><span data-stu-id="06815-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="06815-213">Por exemplo, hello seguinte consulta devolverá apenas Olá **Descrição** e **dueDate** campos.</span><span class="sxs-lookup"><span data-stu-id="06815-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="06815-214">Eliminar uma entidade</span><span class="sxs-lookup"><span data-stu-id="06815-214">Delete an entity</span></span>
<span data-ttu-id="06815-215">Pode eliminar uma entidade com as chaves de partição e linha.</span><span class="sxs-lookup"><span data-stu-id="06815-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="06815-216">Neste exemplo, Olá **task1** objeto contém Olá **RowKey** e **PartitionKey** valores de Olá toobe de entidade eliminada.</span><span class="sxs-lookup"><span data-stu-id="06815-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="06815-217">Em seguida, é transmitido um objeto de Olá toohello **deleteEntity** método.</span><span class="sxs-lookup"><span data-stu-id="06815-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="06815-218">Considere utilizar ETags quando a eliminação de itens, tooensure Olá item não foi modificada por outro processo.</span><span class="sxs-lookup"><span data-stu-id="06815-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="06815-219">Consulte [atualizar uma entidade](#update-an-entity) para obter informações sobre como utilizar ETags.</span><span class="sxs-lookup"><span data-stu-id="06815-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="06815-220">Eliminar uma tabela</span><span class="sxs-lookup"><span data-stu-id="06815-220">Delete a table</span></span>
<span data-ttu-id="06815-221">Olá seguinte código elimina uma tabela a partir de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="06815-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="06815-222">Se não tiver a certeza se existe a tabela de Olá, utilize **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="06815-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="06815-223">Utilize tokens de continuação</span><span class="sxs-lookup"><span data-stu-id="06815-223">Use continuation tokens</span></span>
<span data-ttu-id="06815-224">Quando estiver a consultar tabelas para grandes quantidades de resultados, procure os tokens de continuação.</span><span class="sxs-lookup"><span data-stu-id="06815-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="06815-225">Poderão estar disponíveis para a consulta que poderá Note que o se não criar toorecognize quando existe um token de continuação grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="06815-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="06815-226">resultados de Olá objeto devolvido durante a consulta de conjuntos de entidades um `continuationToken` propriedade quando tal um token está presente.</span><span class="sxs-lookup"><span data-stu-id="06815-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="06815-227">Em seguida, pode utilizar este quando efetuar uma toomove toocontinue de consulta em entidades de partição e a tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="06815-228">Ao consultar, poderá ser fornecido um parâmetro de continuationToken entre a instância de objeto da consulta de Olá e função de chamada de retorno de Olá:</span><span class="sxs-lookup"><span data-stu-id="06815-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="06815-229">Se inspecionar Olá `continuationToken` objeto, encontrará propriedades, tais como `nextPartitionKey`, `nextRowKey` e `targetLocation`, que pode ser utilizado tooiterate através de todos os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="06815-230">Também é um exemplo de continuação no repositório de Node.js de armazenamento do Azure Olá no GitHub.</span><span class="sxs-lookup"><span data-stu-id="06815-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="06815-231">Procure `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="06815-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="06815-232">Trabalhar com assinaturas de acesso partilhado</span><span class="sxs-lookup"><span data-stu-id="06815-232">Work with shared access signatures</span></span>
<span data-ttu-id="06815-233">Assinaturas de acesso partilhado (SAS) são uma tootables de acesso granulares tooprovide de forma segura sem fornecer o nome da conta de armazenamento ou chaves.</span><span class="sxs-lookup"><span data-stu-id="06815-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="06815-234">SAS são frequentemente utilizados tooprovide limitada para aceder a dados tooyour, tais como permitir que uma aplicação móvel tooquery registos.</span><span class="sxs-lookup"><span data-stu-id="06815-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="06815-235">Uma aplicação como um serviço baseado na nuvem fidedigna gera uma SAS utilizando Olá **generateSharedAccessSignature** de Olá **TableService**e fornece-tooan fidedigna ou fidedigna por aplicação Por exemplo, uma aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="06815-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="06815-236">Olá SAS é gerado utilizando uma política, que descreve o início de Olá e datas final durante o qual Olá SAS é válido, bem como Olá marcador de posição SAS de toohello concedida ao nível de acesso.</span><span class="sxs-lookup"><span data-stu-id="06815-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="06815-237">Olá exemplo seguinte gera uma nova política de acesso partilhado, o que permitirá Olá tabela Olá do SAS marcador de posição tooquery ('r') e expira 100 minutos após a hora de Olá que é criado.</span><span class="sxs-lookup"><span data-stu-id="06815-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="06815-238">Tenha em atenção que as informações do anfitrião Olá têm de ser fornecidos também, conforme necessário, quando o marcador de posição do Olá SAS tenta tabela de Olá tooaccess.</span><span class="sxs-lookup"><span data-stu-id="06815-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="06815-239">Olá aplicação cliente, em seguida, utiliza Olá SAS com **TableServiceWithSAS** tooperform operações relativamente à tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="06815-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="06815-240">seguinte o exemplo de Olá liga toohello tabela e executa uma consulta.</span><span class="sxs-lookup"><span data-stu-id="06815-240">hello following example connects toohello table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

<span data-ttu-id="06815-241">Uma vez que hello SAS foi gerado com acesso de consulta apenas, se foi efetuada uma tentativa tooinsert, atualizar ou eliminar entidades, será devolvido um erro.</span><span class="sxs-lookup"><span data-stu-id="06815-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="06815-242">Listas de controlo de acesso</span><span class="sxs-lookup"><span data-stu-id="06815-242">Access Control Lists</span></span>
<span data-ttu-id="06815-243">Também pode utilizar uma política de acesso de Olá de tooset de lista de controlo de acesso (ACL) para um SAS.</span><span class="sxs-lookup"><span data-stu-id="06815-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="06815-244">Isto é útil se desejar tooallow tabela do Olá vários tooaccess de clientes, mas fornecem as políticas de acesso diferentes para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="06815-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="06815-245">Uma ACL é implementada com uma matriz de políticas de acesso, com um ID associado a cada política.</span><span class="sxs-lookup"><span data-stu-id="06815-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="06815-246">Olá seguinte o exemplo define duas políticas, uma para 'user1' e outra para 'Utilizador2':</span><span class="sxs-lookup"><span data-stu-id="06815-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="06815-247">Olá seguinte obtém do exemplo Olá ACL atual para Olá **hometasks** tabela e, em seguida, adiciona novas políticas de Olá utilizando **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="06815-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="06815-248">Esta abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="06815-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="06815-249">Uma vez Olá que ACL foi definida, pode, em seguida, crie um SAS com base no ID de Olá para uma política.</span><span class="sxs-lookup"><span data-stu-id="06815-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="06815-250">Olá seguinte exemplo cria um novo SAS para 'Utilizador2':</span><span class="sxs-lookup"><span data-stu-id="06815-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="06815-251">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="06815-251">Next steps</span></span>
<span data-ttu-id="06815-252">Para obter mais informações, consulte Olá os seguintes recursos.</span><span class="sxs-lookup"><span data-stu-id="06815-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="06815-253">[Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="06815-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="06815-254">[SDK de armazenamento do Azure para o nó](https://github.com/Azure/azure-storage-node) repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="06815-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="06815-255">Centro para Programadores do Node.js</span><span class="sxs-lookup"><span data-stu-id="06815-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="06815-256">Criar e implementar uma tooan de aplicação Node.js Web site do Azure</span><span class="sxs-lookup"><span data-stu-id="06815-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
