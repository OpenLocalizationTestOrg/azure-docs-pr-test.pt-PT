---
title: aaaHow toouse armazenamento de filas do Node.js | Microsoft Docs
description: "Saiba como toouse Olá filas do Azure service toocreate e filas de eliminação e inserção, obterem e eliminar as mensagens. Amostras de escrita no Node.js."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 977e5994c0be1b5d71c60b7479698ccb694ab860
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="7b362-104">Como toouse armazenamento de filas do Node.js</span><span class="sxs-lookup"><span data-stu-id="7b362-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="7b362-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="7b362-105">Overview</span></span>
<span data-ttu-id="7b362-106">Este guia mostra como tooperform cenários comuns utilizando Olá serviço fila do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7b362-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="7b362-107">Exemplos de Olá são escritos utilizando Olá Node.js API.</span><span class="sxs-lookup"><span data-stu-id="7b362-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="7b362-108">Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar e eliminar filas**.</span><span class="sxs-lookup"><span data-stu-id="7b362-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="7b362-109">Criar uma aplicação Node.js</span><span class="sxs-lookup"><span data-stu-id="7b362-109">Create a Node.js Application</span></span>
<span data-ttu-id="7b362-110">Crie uma aplicação Node.js em branco.</span><span class="sxs-lookup"><span data-stu-id="7b362-110">Create a blank Node.js application.</span></span> <span data-ttu-id="7b362-111">Para obter instruções sobre como criar uma aplicação Node.js, consulte [criar uma aplicação web Node.js no App Service do Azure], [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure] utilizando o Windows PowerShell ou [ Criar e implementar uma aplicação de web Node.js tooAzure utilizando a Web Matrix].</span><span class="sxs-lookup"><span data-stu-id="7b362-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="7b362-112">Configurar a sua aplicação tooAccess armazenamento</span><span class="sxs-lookup"><span data-stu-id="7b362-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="7b362-113">toouse storage do Azure, terá de Olá SDK de armazenamento do Azure para Node.js, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="7b362-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="7b362-114">Utilizar o Gestor de pacote de nó (NPM) tooobtain Olá pacote</span><span class="sxs-lookup"><span data-stu-id="7b362-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="7b362-115">Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), navegue até pasta toohello onde criou o seu exemplo de aplicação.</span><span class="sxs-lookup"><span data-stu-id="7b362-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="7b362-116">Tipo **npm instalar storage do azure** na janela de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="7b362-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="7b362-117">O resultado do comando de Olá é semelhante toohello seguinte o exemplo.</span><span class="sxs-lookup"><span data-stu-id="7b362-117">Output from hello command is similar toohello following example.</span></span>
 
    ```
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
    ```

3. <span data-ttu-id="7b362-118">Pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="7b362-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="7b362-119">Dentro dessa pasta encontrará Olá **storage do azure** pacote, que contém as bibliotecas de Olá precisa de aceder ao armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7b362-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="7b362-120">Importar o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="7b362-120">Import hello package</span></span>
<span data-ttu-id="7b362-121">Utilizar o bloco de notas ou noutro editor de texto, adicionar Olá toohello principais a seguir a **server.js** ficheiro da aplicação olá onde pretende toouse armazenamento:</span><span class="sxs-lookup"><span data-stu-id="7b362-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="7b362-122">Configurar uma ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="7b362-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="7b362-123">módulo Olá do azure será lida a variáveis de ambiente de Olá AZURE\_armazenamento\_conta e o AZURE\_armazenamento\_acesso\_chave ou o AZURE\_armazenamento\_ligação \_Cadeia de informações necessárias tooconnect tooyour conta do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b362-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="7b362-124">Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações da conta Olá ao chamar **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="7b362-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="7b362-125">Para obter um exemplo de definir variáveis de ambiente de Olá na Olá [Portal do Azure](https://portal.azure.com) para um Web site do Azure, consulte [através da aplicação de web de Node.js Olá o serviço de tabela do Azure].</span><span class="sxs-lookup"><span data-stu-id="7b362-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="7b362-126">Como: Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="7b362-126">How To: Create a Queue</span></span>
<span data-ttu-id="7b362-127">Olá código seguinte cria um **QueueService** objeto, que permite-lhe toowork com as filas.</span><span class="sxs-lookup"><span data-stu-id="7b362-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="7b362-128">Olá utilize **createQueueIfNotExists** método, que devolve a fila especificada Olá se já existe ou cria uma nova fila com o nome especificado Olá se já existir.</span><span class="sxs-lookup"><span data-stu-id="7b362-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="7b362-129">Se a fila de Olá é criada, `result.created` é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="7b362-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="7b362-130">Se existir a fila de Olá, `result.created` é falso.</span><span class="sxs-lookup"><span data-stu-id="7b362-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="7b362-131">Filtros</span><span class="sxs-lookup"><span data-stu-id="7b362-131">Filters</span></span>
<span data-ttu-id="7b362-132">As operações de filtragem opcionais podem ser aplicados toooperations efetuada utilizando **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="7b362-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="7b362-133">Operações de filtragem pode incluir registo automaticamente repetir, etc. Os filtros são objetos que implementam um método com assinatura de Olá:</span><span class="sxs-lookup"><span data-stu-id="7b362-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="7b362-134">Depois de efetuar a respetiva pré-processamentos nas opções de pedido de Olá, o método de Olá necessita toocall "seguinte" transmitir uma chamada de retorno com Olá assinatura os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7b362-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="7b362-135">Esta chamada de retorno e após o processamento Olá returnObject (resposta de hello do servidor de toohello Olá pedido), a chamada de retorno de Olá tem tooeither invocar em seguida, se existir toocontinue outros filtros de processamento ou simplesmente invocar finalCallback tooend; caso contrário, cópia de segurança Olá invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="7b362-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="7b362-136">Dois filtros que implementa lógica de repetição são incluídos com Olá Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="7b362-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="7b362-137">seguinte Olá cria um **QueueService** objeto que utiliza Olá **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="7b362-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="7b362-138">Como: Introduzir uma mensagem para uma fila</span><span class="sxs-lookup"><span data-stu-id="7b362-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="7b362-139">tooinsert uma mensagem para uma fila, utilize Olá **createMessage** método para criar uma nova mensagem e adicioná-lo toohello fila.</span><span class="sxs-lookup"><span data-stu-id="7b362-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="7b362-140">Como: Pré-visualizar Olá a mensagem seguinte</span><span class="sxs-lookup"><span data-stu-id="7b362-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="7b362-141">Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **peekMessages** método.</span><span class="sxs-lookup"><span data-stu-id="7b362-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="7b362-142">Por predefinição, **peekMessages** observa uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="7b362-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="7b362-143">Olá `result` contém mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b362-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="7b362-144">Utilizar **peekMessages** quando existem não existem mensagens na fila de Olá não devolverá um erro, no entanto, não existem mensagens vai ser devolvidas.</span><span class="sxs-lookup"><span data-stu-id="7b362-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="7b362-145">Como: Anular Olá a mensagem seguinte</span><span class="sxs-lookup"><span data-stu-id="7b362-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="7b362-146">A processar uma mensagem é um processo de duas fases:</span><span class="sxs-lookup"><span data-stu-id="7b362-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="7b362-147">Anular a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b362-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="7b362-148">Elimine a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b362-148">Delete hello message.</span></span>

<span data-ttu-id="7b362-149">utilizar toodequeue uma mensagem, **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="7b362-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="7b362-150">Isto faz com que mensagens hello invisível na fila de Olá, pelo que não existem outros clientes podem processá-los.</span><span class="sxs-lookup"><span data-stu-id="7b362-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="7b362-151">Assim que a aplicação tem de processar uma mensagem, chamar **deleteMessage** toodelete a fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b362-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="7b362-152">Olá seguinte o exemplo obtém uma mensagem, em seguida, elimina-a:</span><span class="sxs-lookup"><span data-stu-id="7b362-152">hello following example gets a message, then deletes it:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> <span data-ttu-id="7b362-153">Por predefinição, uma mensagem apenas está oculto para 30 segundos, após o qual é visível tooother clientes.</span><span class="sxs-lookup"><span data-stu-id="7b362-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="7b362-154">Pode especificar um valor diferente utilizando `options.visibilityTimeout` com **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="7b362-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="7b362-155">Utilizar **getMessages** quando existem não existem mensagens na fila de Olá não devolverá um erro, no entanto, não existem mensagens vai ser devolvidas.</span><span class="sxs-lookup"><span data-stu-id="7b362-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="7b362-156">Como: Alterar Olá conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="7b362-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="7b362-157">Pode alterar o conteúdo de Olá de um mensagem no local na Olá fila utilizando **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="7b362-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="7b362-158">Olá texto Olá de atualizações de exemplo de uma mensagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b362-158">hello following example updates hello text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="7b362-159">Como: Mensagens de opções adicionais para Dequeuing</span><span class="sxs-lookup"><span data-stu-id="7b362-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="7b362-160">Existem duas formas que pode personalizar a obtenção de mensagens numa fila:</span><span class="sxs-lookup"><span data-stu-id="7b362-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="7b362-161">`options.numOfMessages`-Obter um lote de mensagens em fila (cópia de segurança too32.)</span><span class="sxs-lookup"><span data-stu-id="7b362-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="7b362-162">`options.visibilityTimeout`-Defina um tempo de limite de invisibilidade superiores ou inferiores.</span><span class="sxs-lookup"><span data-stu-id="7b362-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="7b362-163">Olá exemplo seguinte utiliza Olá **getMessages** mensagens tooget 15 de método numa chamada.</span><span class="sxs-lookup"><span data-stu-id="7b362-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="7b362-164">Em seguida, processa cada mensagem utilizando um ciclo for.</span><span class="sxs-lookup"><span data-stu-id="7b362-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="7b362-165">Também define minutos toofive de tempo limite de invisibilidade do Olá para todas as mensagens devolvidos por este método.</span><span class="sxs-lookup"><span data-stu-id="7b362-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="7b362-166">Como: Obter Olá comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="7b362-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="7b362-167">Olá **getQueueMetadata** devolve os metadados sobre fila Olá, incluindo o número aproximado de Olá de mensagens a aguardar na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b362-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="7b362-168">Como: Filas de lista</span><span class="sxs-lookup"><span data-stu-id="7b362-168">How To: List Queues</span></span>
<span data-ttu-id="7b362-169">tooretrieve uma lista de filas, utilize **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="7b362-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="7b362-170">tooretrieve uma lista filtrados por um prefixo específico, utilize **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="7b362-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="7b362-171">Se não podem ser devolvidas todas as filas, `result.continuationToken` pode ser utilizada como Olá primeiro parâmetro de **listQueuesSegmented** ou Olá segundo parâmetro de **listQueuesSegmentedWithPrefix** tooretrieve mais resultados.</span><span class="sxs-lookup"><span data-stu-id="7b362-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="7b362-172">Como: Eliminar uma fila</span><span class="sxs-lookup"><span data-stu-id="7b362-172">How To: Delete a Queue</span></span>
<span data-ttu-id="7b362-173">toodelete uma fila e todas as mensagens de Olá nela contidas, chame o **deleteQueue** método no objeto de fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b362-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="7b362-174">tooclear todas as mensagens de uma fila sem eliminá-lo, utilize **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="7b362-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="7b362-175">Como: trabalhar com assinaturas de acesso partilhado</span><span class="sxs-lookup"><span data-stu-id="7b362-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="7b362-176">Assinaturas de acesso partilhado (SAS) são uma tooqueues de acesso granulares tooprovide de forma segura sem fornecer o nome da conta de armazenamento ou chaves.</span><span class="sxs-lookup"><span data-stu-id="7b362-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="7b362-177">SAS são frequentemente utilizados tooprovide limitada para aceder a filas tooyour, tais como permitir que uma aplicação móvel toosubmit mensagens.</span><span class="sxs-lookup"><span data-stu-id="7b362-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="7b362-178">Uma aplicação como um serviço baseado na nuvem fidedigna gera uma SAS utilizando Olá **generateSharedAccessSignature** de Olá **QueueService**e fornece-tooan fidedigna ou fidedigna por aplicação.</span><span class="sxs-lookup"><span data-stu-id="7b362-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="7b362-179">Por exemplo, uma aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="7b362-179">For example, a mobile app.</span></span> <span data-ttu-id="7b362-180">Olá SAS é gerado utilizando uma política, que descreve o início de Olá e datas final durante o qual Olá SAS é válido, bem como Olá marcador de posição SAS de toohello concedida ao nível de acesso.</span><span class="sxs-lookup"><span data-stu-id="7b362-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="7b362-181">Olá seguinte o exemplo gera uma nova política de acesso partilhado, o que permitirá Olá SAS marcador de posição tooadd toohello a fila de mensagens e expira 100 minutos após a hora de Olá que é criado.</span><span class="sxs-lookup"><span data-stu-id="7b362-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

<span data-ttu-id="7b362-182">Tenha em atenção que as informações do anfitrião Olá têm de ser fornecidos também, conforme necessário, quando o marcador de posição do Olá SAS tentativas de fila de Olá tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7b362-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="7b362-183">Olá aplicação cliente, em seguida, utiliza Olá SAS com **QueueServiceWithSAS** tooperform operações em relação a fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b362-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="7b362-184">Olá seguinte o exemplo liga toohello fila e cria uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="7b362-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="7b362-185">Uma vez que hello SAS foi gerado com adicionar acesso, se foi efetuada uma tentativa tooread, atualizar ou eliminar as mensagens, será devolvido um erro.</span><span class="sxs-lookup"><span data-stu-id="7b362-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="7b362-186">Lista de controlo de acesso</span><span class="sxs-lookup"><span data-stu-id="7b362-186">Access control lists</span></span>
<span data-ttu-id="7b362-187">Também pode utilizar uma política de acesso de Olá de tooset de lista de controlo de acesso (ACL) para um SAS.</span><span class="sxs-lookup"><span data-stu-id="7b362-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="7b362-188">Isto é útil se desejar tooallow fila do Olá vários tooaccess de clientes, mas fornecem as políticas de acesso diferentes para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="7b362-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="7b362-189">Uma ACL é implementada com uma matriz de políticas de acesso, com um ID associado a cada política.</span><span class="sxs-lookup"><span data-stu-id="7b362-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="7b362-190">Olá seguinte o exemplo define duas políticas; um para 'user1' e outra para 'Utilizador2':</span><span class="sxs-lookup"><span data-stu-id="7b362-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="7b362-191">Olá seguinte obtém do exemplo Olá ACL atual para **myqueue**, em seguida, adiciona novas políticas de Olá utilizando **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="7b362-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="7b362-192">Esta abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="7b362-192">This approach allows:</span></span>

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="7b362-193">Uma vez Olá que ACL foi definida, pode, em seguida, crie um SAS com base no ID de Olá para uma política.</span><span class="sxs-lookup"><span data-stu-id="7b362-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="7b362-194">Olá seguinte exemplo cria um novo SAS para 'Utilizador2':</span><span class="sxs-lookup"><span data-stu-id="7b362-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="7b362-195">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="7b362-195">Next Steps</span></span>
<span data-ttu-id="7b362-196">Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="7b362-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="7b362-197">Visite Olá [blogue da equipa de armazenamento do Azure][Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="7b362-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="7b362-198">Visite Olá [SDK de armazenamento do Azure para o nó] [ Azure Storage SDK for Node] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="7b362-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[criar uma aplicação web Node.js no App Service do Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[através da aplicação de web de Node.js Olá o serviço de tabela do Azure]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ Criar e implementar uma aplicação de web Node.js tooAzure utilizando a Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
