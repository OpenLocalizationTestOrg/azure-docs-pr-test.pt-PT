---
title: "aaaGet começar a utilizar armazenamento de Blobs do Azure e o Visual Studio ligado serviços (ASP.NET) | Microsoft Docs"
description: Como tooget iniciado a utilizar o armazenamento de Blobs do Azure num projeto ASP.NET no Visual Studio depois de se ligar a conta de armazenamento de tooa utilizando o Visual Studio ligado Services
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="80910-103">Introdução ao blob storage do Azure e o Visual Studio ligado serviços (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="80910-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="80910-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="80910-104">Overview</span></span>

<span data-ttu-id="80910-105">Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="80910-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="80910-106">O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação.</span><span class="sxs-lookup"><span data-stu-id="80910-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="80910-107">O blob storage também é referido tooas armazenamento de objetos.</span><span class="sxs-lookup"><span data-stu-id="80910-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="80910-108">Este tutorial mostra como toowrite ASP.NET code para alguns cenários comuns utilizando o armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="80910-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="80910-109">Os cenários incluem a criação de um contentor de blob, carregar, listar, transferir e eliminar blobs.</span><span class="sxs-lookup"><span data-stu-id="80910-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="80910-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80910-110">Prerequisites</span></span>

* [<span data-ttu-id="80910-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="80910-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="80910-112">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="80910-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="80910-113">Criar um controlador MVC</span><span class="sxs-lookup"><span data-stu-id="80910-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="80910-114">No Olá **Explorador de soluções**, faça duplo clique **controladores**e, no menu de contexto de Olá, selecione **adicionar -> controlador**.</span><span class="sxs-lookup"><span data-stu-id="80910-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Adicionar um controlador tooan aplicação ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="80910-116">No Olá **adicionar andaime** caixa de diálogo, selecione **controlador MVC 5 – vazio**e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="80910-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especifique o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="80910-118">No Olá **Adicionar controlador** caixa de diálogo, o controlador de Olá nome *BlobsController*e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="80910-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Controlador MVC do nome Olá](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="80910-120">Adicione Olá seguinte *utilizando* diretivas toohello `BlobsController.cs` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="80910-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="80910-121">Criar um contentor de blob</span><span class="sxs-lookup"><span data-stu-id="80910-121">Create a blob container</span></span>

<span data-ttu-id="80910-122">Um contentor do blob é uma hierarquia aninhada de blobs e de pastas.</span><span class="sxs-lookup"><span data-stu-id="80910-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="80910-123">Olá passos seguintes mostram como toocreate um contentor do blob:</span><span class="sxs-lookup"><span data-stu-id="80910-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="80910-124">Olá código nesta secção assume que concluiu os passos de Olá na secção de Olá, [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="80910-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="80910-125">Abra Olá `BlobsController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="80910-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="80910-126">Adicione um método denominado **CreateBlobContainer** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="80910-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="80910-127">Dentro do Olá **CreateBlobContainer** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="80910-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="80910-128">Utilize Olá seguintes código tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação de configuração de serviço do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="80910-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="80910-129">(Alterar  *&lt;nome da conta de armazenamento >* nome toohello Olá conta do storage do Azure que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="80910-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="80910-130">Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.</span><span class="sxs-lookup"><span data-stu-id="80910-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="80910-131">Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob pretendido de toohello referência.</span><span class="sxs-lookup"><span data-stu-id="80910-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="80910-132">Olá **CloudBlobClient.GetContainerReference** método não faz um pedido para o blob storage.</span><span class="sxs-lookup"><span data-stu-id="80910-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="80910-133">referência de Olá é devolvida se ou não existe de contentor do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="80910-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="80910-134">Chamar Olá **CloudBlobContainer.CreateIfNotExists** contentor de Olá de toocreate método se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="80910-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="80910-135">Olá **CloudBlobContainer.CreateIfNotExists** método devolve **verdadeiro** se Olá contentor não existe e é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="80910-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="80910-136">Caso contrário, **falso** é devolvido.</span><span class="sxs-lookup"><span data-stu-id="80910-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="80910-137">Olá atualização **ViewBag** com o nome de Olá do contentor de blob Olá.</span><span class="sxs-lookup"><span data-stu-id="80910-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="80910-138">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **Blobs**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="80910-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="80910-139">No Olá **Adicionar vista** caixa de diálogo, introduza **CreateBlobContainer** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="80910-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="80910-140">Abra `CreateBlobContainer.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="80910-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="80910-141">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="80910-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="80910-142">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="80910-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="80910-143">Executar a aplicação Olá e selecione **criar contentor de Blob** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="80910-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![Criar contentor de blob](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="80910-145">Como mencionado anteriormente, Olá **CloudBlobContainer.CreateIfNotExists** método devolve **verdadeiro** apenas quando o contentor de Olá não existe e é criado.</span><span class="sxs-lookup"><span data-stu-id="80910-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="80910-146">Por conseguinte, se executar a aplicação Olá quando Olá contentor existe, o método de Olá devolve **falso**.</span><span class="sxs-lookup"><span data-stu-id="80910-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="80910-147">toorun Olá aplicação várias vezes, tem de eliminar o contentor de Olá antes de executar a aplicação Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="80910-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="80910-148">Eliminar contentor de Olá pode ser feito através de Olá **CloudBlobContainer.Delete** método.</span><span class="sxs-lookup"><span data-stu-id="80910-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="80910-149">Também pode eliminar o contentor de Olá utilizando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="80910-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="80910-150">Carregar um blob para um contentor do blob</span><span class="sxs-lookup"><span data-stu-id="80910-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="80910-151">Assim que tiver [criou um contentor de blob](#create-a-blob-container), pode carregar ficheiros para esse contentor.</span><span class="sxs-lookup"><span data-stu-id="80910-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="80910-152">Esta secção explica o carregamento de um contentor do blob tooa ficheiro local.</span><span class="sxs-lookup"><span data-stu-id="80910-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="80910-153">Olá passos partem do princípio de que criou um contentor do blob denominado *contentor de BLOBs de teste*.</span><span class="sxs-lookup"><span data-stu-id="80910-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="80910-154">Olá código nesta secção assume que concluiu os passos de Olá na secção de Olá, [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="80910-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="80910-155">Abra Olá `BlobsController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="80910-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="80910-156">Adicione um método denominado **UploadBlob** que devolve um **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="80910-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="80910-157">Dentro do Olá **UploadBlob** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="80910-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="80910-158">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="80910-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="80910-159">Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.</span><span class="sxs-lookup"><span data-stu-id="80910-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="80910-160">Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob de toohello referência.</span><span class="sxs-lookup"><span data-stu-id="80910-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="80910-161">Tal como explicado anteriormente, o storage do Azure suporta tipos de blob diferente.</span><span class="sxs-lookup"><span data-stu-id="80910-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="80910-162">tooretrieve um blob de página de tooa de referência, chamada Olá **CloudBlobContainer.GetPageBlobReference** método.</span><span class="sxs-lookup"><span data-stu-id="80910-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="80910-163">tooretrieve um blob de bloco de tooa de referência, chamada Olá **CloudBlobContainer.GetBlockBlobReference** método.</span><span class="sxs-lookup"><span data-stu-id="80910-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="80910-164">Normalmente, o blob de bloco é Olá recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="80910-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="80910-165">(Alterar < nome do blob > * toohello nome blob de Olá toogive uma vez carregado.)</span><span class="sxs-lookup"><span data-stu-id="80910-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="80910-166">Depois de ter uma referência de blob, pode carregar qualquer tooit de fluxo de dados, chamando Olá blob o objecto de referência **UploadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="80910-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="80910-167">Olá **UploadFromStream** método cria blob Olá, se não existir ou substitui-lo se existir.</span><span class="sxs-lookup"><span data-stu-id="80910-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="80910-168">(Alterar  *&lt;carregamento do ficheiro >* tooa totalmente qualificado ficheiro toohello de caminho que pretende tooupload.)</span><span class="sxs-lookup"><span data-stu-id="80910-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="80910-169">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **Blobs**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="80910-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="80910-170">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="80910-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="80910-171">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="80910-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="80910-172">Executar a aplicação Olá e selecione **carregar blob**.</span><span class="sxs-lookup"><span data-stu-id="80910-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="80910-173">Olá secção - [listar Olá blobs num contentor de blob](#list-the-blobs-in-a-blob-container) -ilustra como Olá toolist blobs num contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="80910-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="80910-174">Lista Olá blobs num contentor de blob</span><span class="sxs-lookup"><span data-stu-id="80910-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="80910-175">Esta secção ilustra como Olá toolist blobs num contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="80910-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="80910-176">código de exemplo de Olá referencia Olá *contentor de BLOBs de teste* criou na secção de Olá, [criar um contentor de blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="80910-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="80910-177">Olá código nesta secção assume que concluiu os passos de Olá na secção de Olá, [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="80910-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="80910-178">Abra Olá `BlobsController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="80910-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="80910-179">Adicione um método denominado **ListBlobs** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="80910-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="80910-180">Dentro do Olá **ListBlobs** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="80910-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="80910-181">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="80910-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="80910-182">Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.</span><span class="sxs-lookup"><span data-stu-id="80910-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="80910-183">Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob de toohello referência.</span><span class="sxs-lookup"><span data-stu-id="80910-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="80910-184">os blobs de Olá toolist num contentor de BLOBs, utilize Olá **CloudBlobContainer.ListBlobs** método.</span><span class="sxs-lookup"><span data-stu-id="80910-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="80910-185">Olá **CloudBlobContainer.ListBlobs** método devolve um **IListBlobItem** objeto que converter tooa **CloudBlockBlob**, **CloudPageBlob**, ou **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="80910-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="80910-186">Olá fragmento de código seguinte enumera todos os Olá blobs no contentor do blob.</span><span class="sxs-lookup"><span data-stu-id="80910-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="80910-187">Cada blob está converter toohello adequado o objeto com base no respetivo tipo e o respetivo nome (ou URI no caso de Olá de um **CloudBlobDirectory**) está adicionada tooa lista.</span><span class="sxs-lookup"><span data-stu-id="80910-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="80910-188">Na adição tooblobs, contentores de blob podem conter diretórios.</span><span class="sxs-lookup"><span data-stu-id="80910-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="80910-189">Vamos imaginar que tem um contentor do blob denominado *contentor de BLOBs de teste* com Olá hierarquia os seguintes:</span><span class="sxs-lookup"><span data-stu-id="80910-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="80910-190">Utilizar Olá anterior exemplo de código, Olá **blobs** lista de cadeias contém seguinte de toohello semelhante valores:</span><span class="sxs-lookup"><span data-stu-id="80910-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="80910-191">Como pode ver, a lista de Olá inclui apenas Olá nível superior entidades; Olá não aninhado aqueles (*bar.png* e *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="80910-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="80910-192">toolist Olá todas as entidades dentro de um contentor de blob, tem de chamar Olá **CloudBlobContainer.ListBlobs** método e passar **verdadeiro** para Olá **useFlatBlobListing** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="80910-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="80910-193">Olá definição **useFlatBlobListing** parâmetro demasiado**verdadeiro** devolve uma lista não hierárquica de todas as entidades no contentor de blob Olá e gera Olá os seguintes resultados:</span><span class="sxs-lookup"><span data-stu-id="80910-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="80910-194">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **Blobs**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="80910-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="80910-195">No Olá **Adicionar vista** caixa de diálogo, introduza **ListBlobs** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="80910-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="80910-196">Abra `ListBlobs.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="80910-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="80910-197">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="80910-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="80910-198">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="80910-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="80910-199">Executar a aplicação Olá e selecione **listar blobs** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="80910-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![Lista de blob](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="80910-201">Transferir blobs</span><span class="sxs-lookup"><span data-stu-id="80910-201">Download blobs</span></span>

<span data-ttu-id="80910-202">Esta secção ilustra como toodownload um blob e a manter-toolocal armazenamento ou leitura Olá do conteúdo numa cadeia.</span><span class="sxs-lookup"><span data-stu-id="80910-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="80910-203">código de exemplo de Olá referencia Olá *contentor de BLOBs de teste* criou na secção de Olá, [criar um contentor de blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="80910-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="80910-204">Abra Olá `BlobsController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="80910-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="80910-205">Adicione um método denominado **DownloadBlob** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="80910-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="80910-206">Dentro do Olá **DownloadBlob** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="80910-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="80910-207">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="80910-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="80910-208">Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.</span><span class="sxs-lookup"><span data-stu-id="80910-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="80910-209">Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob de toohello referência.</span><span class="sxs-lookup"><span data-stu-id="80910-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="80910-210">A obtenção de um objeto de referência de blob chamando **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference** método.</span><span class="sxs-lookup"><span data-stu-id="80910-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="80910-211">(Alterar  *&lt;nome do blob >* toohello nome do blob Olá estiver a transferir.)</span><span class="sxs-lookup"><span data-stu-id="80910-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="80910-212">toodownload um blob, utilize Olá **CloudBlockBlob.DownloadToStream** ou **CloudPageBlob.DownloadToStream** método, dependendo do tipo de blob Olá.</span><span class="sxs-lookup"><span data-stu-id="80910-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="80910-213">Olá seguinte fragmento de código utiliza Olá **CloudBlockBlob.DownloadToStream** tootransfer método fluxo de tooa de conteúdo de um blob de objeto que é persistente, em seguida, ficheiro local tooa: (alteração  *&lt;nome de ficheiro local >* toohello totalmente qualificado representando de nome de ficheiro onde pretende que o blob Olá transferido.)</span><span class="sxs-lookup"><span data-stu-id="80910-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="80910-214">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="80910-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="80910-215">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="80910-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="80910-216">Executar a aplicação Olá e selecione **transferir BLOBs** blob de Olá toodownload.</span><span class="sxs-lookup"><span data-stu-id="80910-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="80910-217">blob Olá especificado no Olá **CloudBlobContainer.GetBlockBlobReference** chamada de método transfere localização toohello especificou nas Olá **File.OpenWrite** chamada de método.</span><span class="sxs-lookup"><span data-stu-id="80910-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="80910-218">Eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="80910-218">Delete blobs</span></span>

<span data-ttu-id="80910-219">Olá passos seguintes mostram como toodelete um blob:</span><span class="sxs-lookup"><span data-stu-id="80910-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="80910-220">Olá código nesta secção assume que concluiu os passos de Olá na secção de Olá, [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="80910-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="80910-221">Abra Olá `BlobsController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="80910-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="80910-222">Adicione um método denominado **DeleteBlob** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="80910-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="80910-223">Obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="80910-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="80910-224">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="80910-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="80910-225">Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.</span><span class="sxs-lookup"><span data-stu-id="80910-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="80910-226">Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob de toohello referência.</span><span class="sxs-lookup"><span data-stu-id="80910-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="80910-227">A obtenção de um objeto de referência de blob chamando **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference** método.</span><span class="sxs-lookup"><span data-stu-id="80910-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="80910-228">(Alterar  *&lt;nome do blob >* toohello nome do blob Olá serão eliminados.)</span><span class="sxs-lookup"><span data-stu-id="80910-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="80910-229">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="80910-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="80910-230">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="80910-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="80910-231">Executar a aplicação Olá e selecione **eliminar BLOBs** blob de Olá toodelete especificado no Olá **CloudBlobContainer.GetBlockBlobReference** chamada de método.</span><span class="sxs-lookup"><span data-stu-id="80910-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="80910-232">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="80910-232">Next steps</span></span>
<span data-ttu-id="80910-233">Ver mais toolearn de guias de funcionalidades sobre as opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="80910-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="80910-234">Introdução ao table storage do Azure e o Visual Studio ligado serviços (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="80910-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="80910-235">Introdução ao armazenamento de filas do Azure e o Visual Studio ligado serviços (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="80910-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)
