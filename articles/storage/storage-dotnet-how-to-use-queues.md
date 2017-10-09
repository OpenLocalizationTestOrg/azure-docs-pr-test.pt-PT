---
title: "aaaGet começar a utilizar armazenamento de filas do Azure através do .NET | Microsoft Docs"
description: "As Filas do Azure fornecem um serviço de mensagens fiável e assíncrono entre componentes da aplicação. Na nuvem permite mensagens tooscale de componentes da aplicação independentemente."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 36bbb40189a301cddbc2ded92d0623fa5e093eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="adce3-104">Introdução ao Armazenamento de filas do Azure através do .NET</span><span class="sxs-lookup"><span data-stu-id="adce3-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="adce3-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="adce3-105">Overview</span></span>
<span data-ttu-id="adce3-106">O armazenamento de Filas do Azure fornece um serviço de mensagens na nuvem entre componentes da aplicação.</span><span class="sxs-lookup"><span data-stu-id="adce3-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="adce3-107">Ao conceber aplicações para o dimensionamento, os componentes da aplicação, muitas vezes, são desacoplados para um dimensionamento independente.</span><span class="sxs-lookup"><span data-stu-id="adce3-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="adce3-108">Armazenamento de filas fornece mensagens assíncrono para comunicação entre componentes da aplicação, se estiverem a executar na nuvem de Olá, no ambiente de trabalho Olá, num servidor no local ou num dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="adce3-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="adce3-109">O Armazenamento de filas também suporta a gestão das tarefas assíncronas e a criação de fluxos de trabalho do processo.</span><span class="sxs-lookup"><span data-stu-id="adce3-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="adce3-110">Acerca deste tutorial</span><span class="sxs-lookup"><span data-stu-id="adce3-110">About this tutorial</span></span>
<span data-ttu-id="adce3-111">Este tutorial mostra como código de toowrite .NET para alguns cenários comuns utilizando o armazenamento de filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="adce3-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="adce3-112">Os cenários abrangidos incluem criar e eliminar filas e adicionar, ler e eliminar mensagens de filas.</span><span class="sxs-lookup"><span data-stu-id="adce3-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="adce3-113">**Estimado tempo toocomplete:** 45 minutos</span><span class="sxs-lookup"><span data-stu-id="adce3-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="adce3-114">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="adce3-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="adce3-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="adce3-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="adce3-116">Biblioteca de Clientes do Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="adce3-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="adce3-117">Gestor de Configuração do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="adce3-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="adce3-118">Uma [Conta do Storage do Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="adce3-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="adce3-119">Adicionar com diretivas</span><span class="sxs-lookup"><span data-stu-id="adce3-119">Add using directives</span></span>
<span data-ttu-id="adce3-120">Adicione Olá seguinte `using` diretivas toohello parte superior Olá `Program.cs` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="adce3-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="adce3-121">Analisar cadeia de ligação de Olá</span><span class="sxs-lookup"><span data-stu-id="adce3-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="adce3-122">Crie hello do cliente do serviço fila</span><span class="sxs-lookup"><span data-stu-id="adce3-122">Create hello Queue service client</span></span>
<span data-ttu-id="adce3-123">Olá **CloudQueueClient** classe permite-lhe tooretrieve filas armazenadas no armazenamento de filas.</span><span class="sxs-lookup"><span data-stu-id="adce3-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="adce3-124">Segue-se o cliente do serviço Olá toocreate unidirecional:</span><span class="sxs-lookup"><span data-stu-id="adce3-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="adce3-125">Agora, está pronto toowrite código que lê dados de e escreve tooQueue o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="adce3-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="adce3-126">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="adce3-126">Create a queue</span></span>
<span data-ttu-id="adce3-127">Este exemplo mostra como toocreate uma fila se já existir:</span><span class="sxs-lookup"><span data-stu-id="adce3-127">This example shows how toocreate a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="adce3-128">Introduzir uma mensagem numa fila</span><span class="sxs-lookup"><span data-stu-id="adce3-128">Insert a message into a queue</span></span>
<span data-ttu-id="adce3-129">tooinsert uma mensagem numa fila existente, primeiro crie um novo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="adce3-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="adce3-130">Em seguida, chame Olá **AddMessage** método.</span><span class="sxs-lookup"><span data-stu-id="adce3-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="adce3-131">É possível criar uma **CloudQueueMessage** a partir de uma cadeia (no formato UTF-8) ou uma matriz de **bytes**.</span><span class="sxs-lookup"><span data-stu-id="adce3-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="adce3-132">Eis o código que cria uma fila (se não existir) e a mensagem de saudação inserções "Olá, mundo":</span><span class="sxs-lookup"><span data-stu-id="adce3-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="adce3-133">Pré-visualizar a mensagem seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="adce3-133">Peek at hello next message</span></span>
<span data-ttu-id="adce3-134">Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **PeekMessage** método.</span><span class="sxs-lookup"><span data-stu-id="adce3-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="adce3-135">Alterar Olá conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="adce3-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="adce3-136">Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="adce3-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="adce3-137">Se a mensagem representa uma tarefa de trabalho, pode utilizar esta funcionalidade tooupdate o estado de tarefa de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="adce3-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="adce3-138">Olá seguinte código atualiza a mensagem da fila de saudação com novos conteúdos e conjuntos Olá tooextend de tempo limite de visibilidade 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="adce3-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="adce3-139">Isto guarda Olá estado do trabalho associado à mensagem de saudação e atribui o cliente de Olá toocontinue minuto outra mensagem de saudação a trabalhar.</span><span class="sxs-lookup"><span data-stu-id="adce3-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="adce3-140">Pode utilizar esta técnica tootrack com vários passos os fluxos de trabalho na fila de mensagens, sem ter toostart através de Olá início se falhar um passo de processamento devido a falha de toohardware ou software.</span><span class="sxs-lookup"><span data-stu-id="adce3-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="adce3-141">Normalmente, também manteria uma contagem de tentativas e se hello mensagem for repetida mais do que  *n*  vezes, deveria eliminá-la.</span><span class="sxs-lookup"><span data-stu-id="adce3-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="adce3-142">Esta ação protege contra uma mensagem que aciona um erro da aplicação sempre que é processada.</span><span class="sxs-lookup"><span data-stu-id="adce3-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="adce3-143">Anular a fila a mensagem seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="adce3-143">De-queue hello next message</span></span>
<span data-ttu-id="adce3-144">O código remove uma mensagem da fila em dois passos.</span><span class="sxs-lookup"><span data-stu-id="adce3-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="adce3-145">Quando chamar **GetMessage**, obterá a mensagem seguinte Olá numa fila.</span><span class="sxs-lookup"><span data-stu-id="adce3-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="adce3-146">Uma mensagem devolvida por **GetMessage** torna-se invisível tooany outro código de leitura de mensagens desta fila.</span><span class="sxs-lookup"><span data-stu-id="adce3-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="adce3-147">Por predefinição, esta mensagem permanece invisível durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="adce3-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="adce3-148">toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="adce3-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="adce3-149">Este processo de dois passos da remoção de uma mensagem garante que se o código de falha tooprocess que pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="adce3-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="adce3-150">As chamadas de código **DeleteMessage** imediatamente após a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="adce3-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="adce3-151">Utilizar o padrão Async-Await com APIs de Armazenamento de filas comuns</span><span class="sxs-lookup"><span data-stu-id="adce3-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="adce3-152">Este exemplo mostra como o padrão Olá toouse Async-Await com APIs de armazenamento de filas comuns.</span><span class="sxs-lookup"><span data-stu-id="adce3-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="adce3-153">exemplo de Olá chama a versão assíncrona de Olá de cada uma das Olá fornecido métodos, conforme indicado pelo Olá *Async* sufixo de cada método.</span><span class="sxs-lookup"><span data-stu-id="adce3-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="adce3-154">Quando é utilizado um método async, Olá async-await padrão suspende a execução local até Olá chamada seja concluída.</span><span class="sxs-lookup"><span data-stu-id="adce3-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="adce3-155">Este comportamento permite Olá atual thread toodo outro trabalho, o que ajuda a evitar congestionamentos de desempenho e melhora Olá capacidade de resposta global da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="adce3-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="adce3-156">Para obter mais detalhes sobre como utilizar o padrão Async-Await no .NET de Olá consulte [Async e -Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="adce3-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="adce3-157">Tirar maior partido das opções adicionais para remover as mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="adce3-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="adce3-158">Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila.</span><span class="sxs-lookup"><span data-stu-id="adce3-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="adce3-159">Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32).</span><span class="sxs-lookup"><span data-stu-id="adce3-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="adce3-160">Segundo, pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="adce3-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="adce3-161">seguinte Olá código de exemplo utiliza o **GetMessages** mensagens de tooget 20 método numa chamada.</span><span class="sxs-lookup"><span data-stu-id="adce3-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="adce3-162">Em seguida, processa cada mensagem através de um ciclo **foreach**.</span><span class="sxs-lookup"><span data-stu-id="adce3-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="adce3-163">Também define minutos toofive de tempo limite de invisibilidade do Olá para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="adce3-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="adce3-164">Tenha em atenção que Olá 5 minutos inicia para todas as mensagens com Olá mesmo tempo, pelo que, depois de 5 minutos passaram desde a chamada de Olá demasiado**GetMessages**, as mensagens que não tenham sido eliminadas ficarão visíveis novamente.</span><span class="sxs-lookup"><span data-stu-id="adce3-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a><span data-ttu-id="adce3-165">Obter o comprimento da fila Olá</span><span class="sxs-lookup"><span data-stu-id="adce3-165">Get hello queue length</span></span>
<span data-ttu-id="adce3-166">Pode obter uma estimativa do número de Olá de mensagens numa fila.</span><span class="sxs-lookup"><span data-stu-id="adce3-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="adce3-167">O **FetchAttributes** método pede o serviço de fila de Olá para obter os atributos de fila de Olá, incluindo a contagem de mensagens hello.</span><span class="sxs-lookup"><span data-stu-id="adce3-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="adce3-168">Olá **ApproximateMessageCount** propriedade devolve Olá último valor obtido pelo **FetchAttributes** método, sem chamar o serviço de fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="adce3-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="adce3-169">Eliminar uma fila</span><span class="sxs-lookup"><span data-stu-id="adce3-169">Delete a queue</span></span>
<span data-ttu-id="adce3-170">toodelete uma fila e todas as mensagens de Olá nela contidas, chame o **eliminar** método no objeto de fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="adce3-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="adce3-171">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="adce3-171">Next steps</span></span>
<span data-ttu-id="adce3-172">Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="adce3-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="adce3-173">Consulte Olá documentação de referência do serviço de fila para obter detalhes completos sobre as APIs disponíveis:</span><span class="sxs-lookup"><span data-stu-id="adce3-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="adce3-174">Storage Client Library for .NET reference (Referência da Biblioteca de Clientes do Armazenamento para .NET)</span><span class="sxs-lookup"><span data-stu-id="adce3-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="adce3-175">REST API reference (Referência da API REST)</span><span class="sxs-lookup"><span data-stu-id="adce3-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="adce3-176">Saiba como código de Olá toosimplify escrever toowork com armazenamento do Azure utilizando Olá [SDK de WebJobs do Azure](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="adce3-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="adce3-177">Ver mais toolearn de guias de funcionalidades sobre as opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="adce3-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="adce3-178">[Introdução ao Table storage do Azure através do .NET](storage-dotnet-how-to-use-tables.md) toostore estruturados dados.</span><span class="sxs-lookup"><span data-stu-id="adce3-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) toostore structured data.</span></span>
  * <span data-ttu-id="adce3-179">[Introdução ao Blob storage do Azure através do .NET](storage-dotnet-how-to-use-blobs.md) toostore dados não estruturados.</span><span class="sxs-lookup"><span data-stu-id="adce3-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="adce3-180">[Ligar tooSQL da base de dados, utilizando o .NET (c#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore de dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="adce3-180">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
