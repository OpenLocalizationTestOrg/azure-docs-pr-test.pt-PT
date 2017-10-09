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
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>Introdução ao Armazenamento de filas do Azure através do .NET
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Descrição geral
O armazenamento de Filas do Azure fornece um serviço de mensagens na nuvem entre componentes da aplicação. Ao conceber aplicações para o dimensionamento, os componentes da aplicação, muitas vezes, são desacoplados para um dimensionamento independente. Armazenamento de filas fornece mensagens assíncrono para comunicação entre componentes da aplicação, se estiverem a executar na nuvem de Olá, no ambiente de trabalho Olá, num servidor no local ou num dispositivo móvel. O Armazenamento de filas também suporta a gestão das tarefas assíncronas e a criação de fluxos de trabalho do processo.

### <a name="about-this-tutorial"></a>Acerca deste tutorial
Este tutorial mostra como código de toowrite .NET para alguns cenários comuns utilizando o armazenamento de filas do Azure. Os cenários abrangidos incluem criar e eliminar filas e adicionar, ler e eliminar mensagens de filas.

**Estimado tempo toocomplete:** 45 minutos

**Pré-requisitos:**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Biblioteca de Clientes do Armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gestor de Configuração do Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Uma [Conta do Storage do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Adicionar com diretivas
Adicione Olá seguinte `using` diretivas toohello parte superior Olá `Program.cs` ficheiro:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Analisar cadeia de ligação de Olá
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Crie hello do cliente do serviço fila
Olá **CloudQueueClient** classe permite-lhe tooretrieve filas armazenadas no armazenamento de filas. Segue-se o cliente do serviço Olá toocreate unidirecional:

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Agora, está pronto toowrite código que lê dados de e escreve tooQueue o armazenamento de dados.

## <a name="create-a-queue"></a>Criar uma fila
Este exemplo mostra como toocreate uma fila se já existir:

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

## <a name="insert-a-message-into-a-queue"></a>Introduzir uma mensagem numa fila
tooinsert uma mensagem numa fila existente, primeiro crie um novo **CloudQueueMessage**. Em seguida, chame Olá **AddMessage** método. É possível criar uma **CloudQueueMessage** a partir de uma cadeia (no formato UTF-8) ou uma matriz de **bytes**. Eis o código que cria uma fila (se não existir) e a mensagem de saudação inserções "Olá, mundo":

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

## <a name="peek-at-hello-next-message"></a>Pré-visualizar a mensagem seguinte Olá
Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **PeekMessage** método.

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

## <a name="change-hello-contents-of-a-queued-message"></a>Alterar Olá conteúdo de uma mensagem em fila
Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá. Se a mensagem representa uma tarefa de trabalho, pode utilizar esta funcionalidade tooupdate o estado de tarefa de trabalho de Olá. Olá seguinte código atualiza a mensagem da fila de saudação com novos conteúdos e conjuntos Olá tooextend de tempo limite de visibilidade 60 segundos. Isto guarda Olá estado do trabalho associado à mensagem de saudação e atribui o cliente de Olá toocontinue minuto outra mensagem de saudação a trabalhar. Pode utilizar esta técnica tootrack com vários passos os fluxos de trabalho na fila de mensagens, sem ter toostart através de Olá início se falhar um passo de processamento devido a falha de toohardware ou software. Normalmente, também manteria uma contagem de tentativas e se hello mensagem for repetida mais do que  *n*  vezes, deveria eliminá-la. Esta ação protege contra uma mensagem que aciona um erro da aplicação sempre que é processada.

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

## <a name="de-queue-hello-next-message"></a>Anular a fila a mensagem seguinte Olá
O código remove uma mensagem da fila em dois passos. Quando chamar **GetMessage**, obterá a mensagem seguinte Olá numa fila. Uma mensagem devolvida por **GetMessage** torna-se invisível tooany outro código de leitura de mensagens desta fila. Por predefinição, esta mensagem permanece invisível durante 30 segundos. toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **DeleteMessage**. Este processo de dois passos da remoção de uma mensagem garante que se o código de falha tooprocess que pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá a mesma mensagem e tente novamente. As chamadas de código **DeleteMessage** imediatamente após a mensagem de saudação foi processada.

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

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Utilizar o padrão Async-Await com APIs de Armazenamento de filas comuns
Este exemplo mostra como o padrão Olá toouse Async-Await com APIs de armazenamento de filas comuns. exemplo de Olá chama a versão assíncrona de Olá de cada uma das Olá fornecido métodos, conforme indicado pelo Olá *Async* sufixo de cada método. Quando é utilizado um método async, Olá async-await padrão suspende a execução local até Olá chamada seja concluída. Este comportamento permite Olá atual thread toodo outro trabalho, o que ajuda a evitar congestionamentos de desempenho e melhora Olá capacidade de resposta global da sua aplicação. Para obter mais detalhes sobre como utilizar o padrão Async-Await no .NET de Olá consulte [Async e -Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Tirar maior partido das opções adicionais para remover as mensagens da fila
Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila.
Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32). Segundo, pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem. seguinte Olá código de exemplo utiliza o **GetMessages** mensagens de tooget 20 método numa chamada. Em seguida, processa cada mensagem através de um ciclo **foreach**. Também define minutos toofive de tempo limite de invisibilidade do Olá para cada mensagem. Tenha em atenção que Olá 5 minutos inicia para todas as mensagens com Olá mesmo tempo, pelo que, depois de 5 minutos passaram desde a chamada de Olá demasiado**GetMessages**, as mensagens que não tenham sido eliminadas ficarão visíveis novamente.

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

## <a name="get-hello-queue-length"></a>Obter o comprimento da fila Olá
Pode obter uma estimativa do número de Olá de mensagens numa fila. O **FetchAttributes** método pede o serviço de fila de Olá para obter os atributos de fila de Olá, incluindo a contagem de mensagens hello. Olá **ApproximateMessageCount** propriedade devolve Olá último valor obtido pelo **FetchAttributes** método, sem chamar o serviço de fila de Olá.

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

## <a name="delete-a-queue"></a>Eliminar uma fila
toodelete uma fila e todas as mensagens de Olá nela contidas, chame o **eliminar** método no objeto de fila de Olá.

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
    

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.

* Consulte Olá documentação de referência do serviço de fila para obter detalhes completos sobre as APIs disponíveis:
  * [Storage Client Library for .NET reference (Referência da Biblioteca de Clientes do Armazenamento para .NET)](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [REST API reference (Referência da API REST)](http://msdn.microsoft.com/library/azure/dd179355)
* Saiba como código de Olá toosimplify escrever toowork com armazenamento do Azure utilizando Olá [SDK de WebJobs do Azure](../../app-service-web/websites-dotnet-webjobs-sdk.md).
* Ver mais toolearn de guias de funcionalidades sobre as opções adicionais para armazenar dados no Azure.
  * [Introdução ao Table storage do Azure através do .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore estruturados dados.
  * [Introdução ao Blob storage do Azure através do .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore dados não estruturados.
  * [Ligar tooSQL da base de dados, utilizando o .NET (c#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore de dados relacionais.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
