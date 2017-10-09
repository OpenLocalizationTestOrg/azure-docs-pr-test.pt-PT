---
title: "aaaGet começar a utilizar o armazenamento de filas do Azure e o Visual Studio ligado serviços (ASP.NET) | Microsoft Docs"
description: Como tooget iniciado utilizando o armazenamento de filas do Azure num projeto ASP.NET no Visual Studio depois de se ligar a conta de armazenamento de tooa utilizando o Visual Studio ligado Services
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: a9d6ecb1e8d61d75f59658d0ea3fa63d26fd7354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Introdução ao armazenamento de filas do Azure e o Visual Studio ligado serviços (ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Descrição geral

Armazenamento de filas do Azure fornece processamento de mensagens entre componentes da aplicação de nuvem. Ao conceber aplicações para o dimensionamento, os componentes da aplicação, muitas vezes, são desacoplados para um dimensionamento independente. Armazenamento de filas fornece mensagens assíncrono para comunicação entre componentes da aplicação, se estiverem a executar na nuvem de Olá, no ambiente de trabalho Olá, num servidor no local ou num dispositivo móvel. O Armazenamento de filas também suporta a gestão das tarefas assíncronas e a criação de fluxos de trabalho do processo.

Este tutorial mostra como toowrite ASP.NET code para alguns cenários comuns utilizando entidades de armazenamento de filas do Azure. Estes cenários incluem tarefas comuns, tais como criar uma fila do Azure, adicionar, modificar, ler e remoção de fila de mensagens.

##<a name="prerequisites"></a>Pré-requisitos

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Conta de armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Criar um controlador MVC 

1. No Olá **Explorador de soluções**, faça duplo clique **controladores**e, no menu de contexto de Olá, selecione **adicionar -> controlador**.

    ![Adicionar um controlador tooan aplicação ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. No Olá **adicionar andaime** caixa de diálogo, selecione **controlador MVC 5 – vazio**e selecione **adicionar**.

    ![Especifique o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. No Olá **Adicionar controlador** caixa de diálogo, o controlador de Olá nome *QueuesController*e selecione **adicionar**.

    ![Controlador MVC do nome Olá](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Adicione Olá seguinte *utilizando* diretivas toohello `QueuesController.cs` ficheiro:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>Criar uma fila

Olá passos seguintes mostram como toocreate uma fila:

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `QueuesController.cs` ficheiro. 

1. Adicione um método denominado **CreateQueue** que devolve um **ActionResult**.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro do Olá **CreateQueue** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. Obter um **CloudQueue** objeto que representa um nome de fila pretendida do toohello de referência. Olá **CloudQueueClient.GetQueueReference** método não faz um pedido de armazenamento de filas. referência de Olá é devolvida se ou não existe Olá fila. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar Olá **CloudQueue.CreateIfNotExists** fila de Olá de toocreate método se ainda não existir. Olá **CloudQueue.CreateIfNotExists** método devolve **verdadeiro** se Olá fila não existe e é criada com êxito. Caso contrário, **falso** é devolvido.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. Olá atualização **ViewBag** com o nome de Olá da fila de Olá.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **CreateQueue** para nome da vista Olá e selecione **adicionar**.

1. Abra `CreateQueue.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Executar a aplicação Olá e selecione **criar fila** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Criar fila](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    Como mencionado anteriormente, Olá **CloudQueue.CreateIfNotExists** método devolve **verdadeiro** apenas quando a fila de Olá não existe e é criada. Por conseguinte, se executar a aplicação Olá quando existe Olá fila, o método de Olá devolve **falso**. aplicação de Olá toorun várias vezes, terá de eliminar Olá fila antes de executar novamente a aplicação Olá. A eliminar filas de Olá podem ser feita através de Olá **CloudQueue.Delete** método. Também pode eliminar a fila de Olá utilizando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-a-message-tooa-queue"></a>Adicionar uma fila de tooa de mensagens

Assim que tiver [criou uma fila](#create-a-queue), pode adicionar toothat a fila de mensagens. Esta secção explica como adicionar uma fila de tooa mensagens *teste fila*. 

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `QueuesController.cs` ficheiro.

1. Adicione um método denominado **AddMessage** que devolve um **ActionResult**.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro do Olá **AddMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Criar Olá **CloudQueueMessage** objeto que representa a mensagem de saudação pretende tooadd toohello fila. A **CloudQueueMessage** objeto pode ser criado a partir de uma cadeia (no formato UTF-8) ou uma matriz de bytes.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Chamar Olá **CloudQueue.AddMessage** fila do método tooadd Olá messaged toohello.

    ```csharp
    queue.AddMessage(message);
    ```

1. Crie e defina alguns **ViewBag** propriedades para apresentação na vista de Olá.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **AddMessage** para nome da vista Olá e selecione **adicionar**.

1. Abra `AddMessage.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Executar a aplicação Olá e selecione **Adicionar mensagem** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Adicionar mensagem](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

Olá duas secções - [ler uma mensagem numa fila sem a remover](#read-a-message-from-a-queue-without-removing-it) e [leitura e remover uma mensagem numa fila](#read-and-remove-a-message-from-a-queue) -ilustrar como tooread mensagens numa fila.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>Ler uma mensagem numa fila sem a remover

Esta secção ilustra como toopeek uma mensagem em fila (leitura primeira mensagem de saudação sem a remover).  

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `QueuesController.cs` ficheiro.

1. Adicione um método denominado **PeekMessage** que devolve um **ActionResult**.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro do Olá **PeekMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar Olá **CloudQueue.PeekMessage** método tooread Olá primeira mensagem Olá fila sem a remover da fila de Olá. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. Olá atualização **ViewBag** com dois valores: nome da fila Olá e mensagem de saudação foi lido. Olá **CloudQueueMessage** objeto expõe duas propriedades para obter o valor do objeto de Olá: **CloudQueueMessage.AsBytes** e **CloudQueueMessage.AsString**. **AsString** (utilizada neste exemplo) devolve uma cadeia, enquanto **AsBytes** devolve uma matriz de bytes.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **PeekMessage** para nome da vista Olá e selecione **adicionar**.

1. Abra `PeekMessage.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Executar a aplicação Olá e selecione **observar mensagem** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Observar mensagem](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>Ler e remover uma mensagem a partir de uma fila

Nesta secção, saiba como tooread e remover uma mensagem numa fila.   

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `QueuesController.cs` ficheiro.

1. Adicione um método denominado **ReadMessage** que devolve um **ActionResult**.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro do Olá **ReadMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar Olá **CloudQueue.GetMessage** método tooread Olá primeira mensagem Olá fila. Olá **CloudQueue.GetMessage** método torna Olá mensagem invisível para 30 segundos (por predefinição) tooany outro mensagens de leitura para que nenhum outro código pode modificar ou eliminar a mensagem de saudação durante o processamento de código. quantidade de Olá toochange de mensagem de saudação do tempo é invisível, modifique Olá **visibilityTimeout** parâmetro a ser transmitido toohello **CloudQueue.GetMessage** método.

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Chamar Olá **CloudQueueMessage.Delete** mensagem de saudação do método toodelete da fila de Olá.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. Olá atualização **ViewBag** com Olá mensagem eliminados e Olá nome da fila de Olá.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **ReadMessage** para nome da vista Olá e selecione **adicionar**.

1. Abra `ReadMessage.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Executar a aplicação Olá e selecione **mensagens de leitura/eliminar** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Ler e eliminar a mensagem](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Obter o comprimento da fila Olá

Esta secção ilustra como tooget Olá comprimento da fila (número de mensagens em fila). 

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `QueuesController.cs` ficheiro.

1. Adicione um método denominado **GetQueueLength** que devolve um **ActionResult**.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro do Olá **ReadMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar Olá **CloudQueue.FetchAttributes** atributos da fila do método tooretrieve Olá (incluindo o respetivo comprimento). 

    ```csharp
    queue.FetchAttributes();
    ```

6. Olá acesso **CloudQueue.ApproximateMessageCount** comprimento da fila de propriedade, tooget Olá.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. Olá atualização **ViewBag** com nome Olá Olá fila e o comprimento.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **GetQueueLength** para nome da vista Olá e selecione **adicionar**.

1. Abra `GetQueueLengthMessage.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Executar a aplicação Olá e selecione **obter o comprimento da fila** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Obter o comprimento da fila](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>Eliminar uma fila
Esta secção ilustra como toodelete uma fila. 

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `QueuesController.cs` ficheiro.

1. Adicione um método denominado **DeleteQueue** que devolve um **ActionResult**.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro do Olá **DeleteQueue** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar Olá **CloudQueue.Delete** fila Olá toodelete de método representada pelo Olá **CloudQueue** objeto.

    ```csharp
    queue.Delete();
    ```

1. Olá atualização **ViewBag** com nome Olá Olá fila e o comprimento.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **DeleteQueue** para nome da vista Olá e selecione **adicionar**.

1. Abra `DeleteQueue.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Executar a aplicação Olá e selecione **obter o comprimento da fila** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Eliminar a fila](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>Passos seguintes
Ver mais toolearn de guias de funcionalidades sobre as opções adicionais para armazenar dados no Azure.

  * [Introdução ao blob storage do Azure e o Visual Studio ligado serviços (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Introdução ao table storage do Azure e o Visual Studio ligado serviços (ASP.NET)](./vs-storage-aspnet-getting-started-tables.md)
