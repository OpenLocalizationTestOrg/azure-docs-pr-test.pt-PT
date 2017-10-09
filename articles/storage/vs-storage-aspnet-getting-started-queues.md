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
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="6e975-103">Introdução ao armazenamento de filas do Azure e o Visual Studio ligado serviços (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="6e975-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="6e975-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="6e975-104">Overview</span></span>

<span data-ttu-id="6e975-105">Armazenamento de filas do Azure fornece processamento de mensagens entre componentes da aplicação de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6e975-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="6e975-106">Ao conceber aplicações para o dimensionamento, os componentes da aplicação, muitas vezes, são desacoplados para um dimensionamento independente.</span><span class="sxs-lookup"><span data-stu-id="6e975-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="6e975-107">Armazenamento de filas fornece mensagens assíncrono para comunicação entre componentes da aplicação, se estiverem a executar na nuvem de Olá, no ambiente de trabalho Olá, num servidor no local ou num dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="6e975-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="6e975-108">O Armazenamento de filas também suporta a gestão das tarefas assíncronas e a criação de fluxos de trabalho do processo.</span><span class="sxs-lookup"><span data-stu-id="6e975-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="6e975-109">Este tutorial mostra como toowrite ASP.NET code para alguns cenários comuns utilizando entidades de armazenamento de filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e975-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="6e975-110">Estes cenários incluem tarefas comuns, tais como criar uma fila do Azure, adicionar, modificar, ler e remoção de fila de mensagens.</span><span class="sxs-lookup"><span data-stu-id="6e975-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="6e975-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6e975-111">Prerequisites</span></span>

* [<span data-ttu-id="6e975-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e975-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="6e975-113">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="6e975-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="6e975-114">Criar um controlador MVC</span><span class="sxs-lookup"><span data-stu-id="6e975-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="6e975-115">No Olá **Explorador de soluções**, faça duplo clique **controladores**e, no menu de contexto de Olá, selecione **adicionar -> controlador**.</span><span class="sxs-lookup"><span data-stu-id="6e975-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Adicionar um controlador tooan aplicação ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="6e975-117">No Olá **adicionar andaime** caixa de diálogo, selecione **controlador MVC 5 – vazio**e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e975-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especifique o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="6e975-119">No Olá **Adicionar controlador** caixa de diálogo, o controlador de Olá nome *QueuesController*e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e975-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Controlador MVC do nome Olá](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="6e975-121">Adicione Olá seguinte *utilizando* diretivas toohello `QueuesController.cs` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="6e975-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="6e975-122">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="6e975-122">Create a queue</span></span>

<span data-ttu-id="6e975-123">Olá passos seguintes mostram como toocreate uma fila:</span><span class="sxs-lookup"><span data-stu-id="6e975-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6e975-124">Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6e975-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6e975-125">Abra Olá `QueuesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6e975-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="6e975-126">Adicione um método denominado **CreateQueue** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6e975-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6e975-127">Dentro do Olá **CreateQueue** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6e975-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6e975-128">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="6e975-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6e975-129">Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="6e975-130">Obter um **CloudQueue** objeto que representa um nome de fila pretendida do toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="6e975-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="6e975-131">Olá **CloudQueueClient.GetQueueReference** método não faz um pedido de armazenamento de filas.</span><span class="sxs-lookup"><span data-stu-id="6e975-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="6e975-132">referência de Olá é devolvida se ou não existe Olá fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6e975-133">Chamar Olá **CloudQueue.CreateIfNotExists** fila de Olá de toocreate método se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="6e975-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="6e975-134">Olá **CloudQueue.CreateIfNotExists** método devolve **verdadeiro** se Olá fila não existe e é criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="6e975-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="6e975-135">Caso contrário, **falso** é devolvido.</span><span class="sxs-lookup"><span data-stu-id="6e975-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="6e975-136">Olá atualização **ViewBag** com o nome de Olá da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e975-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="6e975-137">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="6e975-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6e975-138">No Olá **Adicionar vista** caixa de diálogo, introduza **CreateQueue** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e975-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6e975-139">Abra `CreateQueue.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="6e975-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="6e975-140">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6e975-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6e975-141">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6e975-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="6e975-142">Executar a aplicação Olá e selecione **criar fila** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e975-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![Criar fila](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="6e975-144">Como mencionado anteriormente, Olá **CloudQueue.CreateIfNotExists** método devolve **verdadeiro** apenas quando a fila de Olá não existe e é criada.</span><span class="sxs-lookup"><span data-stu-id="6e975-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="6e975-145">Por conseguinte, se executar a aplicação Olá quando existe Olá fila, o método de Olá devolve **falso**.</span><span class="sxs-lookup"><span data-stu-id="6e975-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="6e975-146">aplicação de Olá toorun várias vezes, terá de eliminar Olá fila antes de executar novamente a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="6e975-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="6e975-147">A eliminar filas de Olá podem ser feita através de Olá **CloudQueue.Delete** método.</span><span class="sxs-lookup"><span data-stu-id="6e975-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="6e975-148">Também pode eliminar a fila de Olá utilizando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="6e975-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="6e975-149">Adicionar uma fila de tooa de mensagens</span><span class="sxs-lookup"><span data-stu-id="6e975-149">Add a message tooa queue</span></span>

<span data-ttu-id="6e975-150">Assim que tiver [criou uma fila](#create-a-queue), pode adicionar toothat a fila de mensagens.</span><span class="sxs-lookup"><span data-stu-id="6e975-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="6e975-151">Esta secção explica como adicionar uma fila de tooa mensagens *teste fila*.</span><span class="sxs-lookup"><span data-stu-id="6e975-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="6e975-152">Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6e975-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6e975-153">Abra Olá `QueuesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6e975-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6e975-154">Adicione um método denominado **AddMessage** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6e975-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6e975-155">Dentro do Olá **AddMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6e975-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6e975-156">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="6e975-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6e975-157">Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6e975-158">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="6e975-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6e975-159">Criar Olá **CloudQueueMessage** objeto que representa a mensagem de saudação pretende tooadd toohello fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="6e975-160">A **CloudQueueMessage** objeto pode ser criado a partir de uma cadeia (no formato UTF-8) ou uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="6e975-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="6e975-161">Chamar Olá **CloudQueue.AddMessage** fila do método tooadd Olá messaged toohello.</span><span class="sxs-lookup"><span data-stu-id="6e975-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="6e975-162">Crie e defina alguns **ViewBag** propriedades para apresentação na vista de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e975-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="6e975-163">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="6e975-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6e975-164">No Olá **Adicionar vista** caixa de diálogo, introduza **AddMessage** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e975-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6e975-165">Abra `AddMessage.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="6e975-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="6e975-166">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6e975-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6e975-167">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6e975-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="6e975-168">Executar a aplicação Olá e selecione **Adicionar mensagem** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e975-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![Adicionar mensagem](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="6e975-170">Olá duas secções - [ler uma mensagem numa fila sem a remover](#read-a-message-from-a-queue-without-removing-it) e [leitura e remover uma mensagem numa fila](#read-and-remove-a-message-from-a-queue) -ilustrar como tooread mensagens numa fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="6e975-171">Ler uma mensagem numa fila sem a remover</span><span class="sxs-lookup"><span data-stu-id="6e975-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="6e975-172">Esta secção ilustra como toopeek uma mensagem em fila (leitura primeira mensagem de saudação sem a remover).</span><span class="sxs-lookup"><span data-stu-id="6e975-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="6e975-173">Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6e975-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6e975-174">Abra Olá `QueuesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6e975-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6e975-175">Adicione um método denominado **PeekMessage** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6e975-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6e975-176">Dentro do Olá **PeekMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6e975-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6e975-177">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="6e975-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6e975-178">Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6e975-179">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="6e975-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6e975-180">Chamar Olá **CloudQueue.PeekMessage** método tooread Olá primeira mensagem Olá fila sem a remover da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e975-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="6e975-181">Olá atualização **ViewBag** com dois valores: nome da fila Olá e mensagem de saudação foi lido.</span><span class="sxs-lookup"><span data-stu-id="6e975-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="6e975-182">Olá **CloudQueueMessage** objeto expõe duas propriedades para obter o valor do objeto de Olá: **CloudQueueMessage.AsBytes** e **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="6e975-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="6e975-183">**AsString** (utilizada neste exemplo) devolve uma cadeia, enquanto **AsBytes** devolve uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="6e975-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="6e975-184">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="6e975-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6e975-185">No Olá **Adicionar vista** caixa de diálogo, introduza **PeekMessage** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e975-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6e975-186">Abra `PeekMessage.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="6e975-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="6e975-187">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6e975-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6e975-188">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6e975-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="6e975-189">Executar a aplicação Olá e selecione **observar mensagem** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e975-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![Observar mensagem](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="6e975-191">Ler e remover uma mensagem a partir de uma fila</span><span class="sxs-lookup"><span data-stu-id="6e975-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="6e975-192">Nesta secção, saiba como tooread e remover uma mensagem numa fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="6e975-193">Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6e975-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6e975-194">Abra Olá `QueuesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6e975-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6e975-195">Adicione um método denominado **ReadMessage** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6e975-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6e975-196">Dentro do Olá **ReadMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6e975-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6e975-197">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="6e975-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6e975-198">Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6e975-199">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="6e975-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6e975-200">Chamar Olá **CloudQueue.GetMessage** método tooread Olá primeira mensagem Olá fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="6e975-201">Olá **CloudQueue.GetMessage** método torna Olá mensagem invisível para 30 segundos (por predefinição) tooany outro mensagens de leitura para que nenhum outro código pode modificar ou eliminar a mensagem de saudação durante o processamento de código.</span><span class="sxs-lookup"><span data-stu-id="6e975-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="6e975-202">quantidade de Olá toochange de mensagem de saudação do tempo é invisível, modifique Olá **visibilityTimeout** parâmetro a ser transmitido toohello **CloudQueue.GetMessage** método.</span><span class="sxs-lookup"><span data-stu-id="6e975-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="6e975-203">Chamar Olá **CloudQueueMessage.Delete** mensagem de saudação do método toodelete da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e975-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="6e975-204">Olá atualização **ViewBag** com Olá mensagem eliminados e Olá nome da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e975-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="6e975-205">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="6e975-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6e975-206">No Olá **Adicionar vista** caixa de diálogo, introduza **ReadMessage** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e975-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6e975-207">Abra `ReadMessage.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="6e975-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="6e975-208">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6e975-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6e975-209">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6e975-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="6e975-210">Executar a aplicação Olá e selecione **mensagens de leitura/eliminar** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e975-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![Ler e eliminar a mensagem](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="6e975-212">Obter o comprimento da fila Olá</span><span class="sxs-lookup"><span data-stu-id="6e975-212">Get hello queue length</span></span>

<span data-ttu-id="6e975-213">Esta secção ilustra como tooget Olá comprimento da fila (número de mensagens em fila).</span><span class="sxs-lookup"><span data-stu-id="6e975-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="6e975-214">Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6e975-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6e975-215">Abra Olá `QueuesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6e975-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6e975-216">Adicione um método denominado **GetQueueLength** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6e975-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6e975-217">Dentro do Olá **ReadMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6e975-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6e975-218">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="6e975-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6e975-219">Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6e975-220">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="6e975-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6e975-221">Chamar Olá **CloudQueue.FetchAttributes** atributos da fila do método tooretrieve Olá (incluindo o respetivo comprimento).</span><span class="sxs-lookup"><span data-stu-id="6e975-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="6e975-222">Olá acesso **CloudQueue.ApproximateMessageCount** comprimento da fila de propriedade, tooget Olá.</span><span class="sxs-lookup"><span data-stu-id="6e975-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="6e975-223">Olá atualização **ViewBag** com nome Olá Olá fila e o comprimento.</span><span class="sxs-lookup"><span data-stu-id="6e975-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="6e975-224">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="6e975-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6e975-225">No Olá **Adicionar vista** caixa de diálogo, introduza **GetQueueLength** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e975-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6e975-226">Abra `GetQueueLengthMessage.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="6e975-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="6e975-227">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6e975-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6e975-228">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6e975-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="6e975-229">Executar a aplicação Olá e selecione **obter o comprimento da fila** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e975-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Obter o comprimento da fila](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="6e975-231">Eliminar uma fila</span><span class="sxs-lookup"><span data-stu-id="6e975-231">Delete a queue</span></span>
<span data-ttu-id="6e975-232">Esta secção ilustra como toodelete uma fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="6e975-233">Esta secção assume que concluiu as fases de Olá [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6e975-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6e975-234">Abra Olá `QueuesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6e975-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6e975-235">Adicione um método denominado **DeleteQueue** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6e975-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6e975-236">Dentro do Olá **DeleteQueue** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6e975-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6e975-237">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="6e975-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6e975-238">Obter um **CloudQueueClient** objeto representa um cliente do serviço fila.</span><span class="sxs-lookup"><span data-stu-id="6e975-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6e975-239">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="6e975-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6e975-240">Chamar Olá **CloudQueue.Delete** fila Olá toodelete de método representada pelo Olá **CloudQueue** objeto.</span><span class="sxs-lookup"><span data-stu-id="6e975-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="6e975-241">Olá atualização **ViewBag** com nome Olá Olá fila e o comprimento.</span><span class="sxs-lookup"><span data-stu-id="6e975-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="6e975-242">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **filas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="6e975-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6e975-243">No Olá **Adicionar vista** caixa de diálogo, introduza **DeleteQueue** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e975-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6e975-244">Abra `DeleteQueue.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="6e975-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="6e975-245">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6e975-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6e975-246">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6e975-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="6e975-247">Executar a aplicação Olá e selecione **obter o comprimento da fila** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e975-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Eliminar a fila](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="6e975-249">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6e975-249">Next steps</span></span>
<span data-ttu-id="6e975-250">Ver mais toolearn de guias de funcionalidades sobre as opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="6e975-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="6e975-251">Introdução ao blob storage do Azure e o Visual Studio ligado serviços (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="6e975-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="6e975-252">Introdução ao table storage do Azure e o Visual Studio ligado serviços (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="6e975-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
