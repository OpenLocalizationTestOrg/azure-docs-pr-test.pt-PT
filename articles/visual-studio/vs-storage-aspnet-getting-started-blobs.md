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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Introdução ao blob storage do Azure e o Visual Studio ligado serviços (ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Descrição geral

Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs. O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação. O blob storage também é referido tooas armazenamento de objetos.

Este tutorial mostra como toowrite ASP.NET code para alguns cenários comuns utilizando o armazenamento de Blobs do Azure. Os cenários incluem a criação de um contentor de blob, carregar, listar, transferir e eliminar blobs.

##<a name="prerequisites"></a>Pré-requisitos

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Criar um controlador MVC 

1. No Olá **Explorador de soluções**, faça duplo clique **controladores**e, no menu de contexto de Olá, selecione **adicionar -> controlador**.

    ![Adicionar um controlador tooan aplicação ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. No Olá **adicionar andaime** caixa de diálogo, selecione **controlador MVC 5 – vazio**e selecione **adicionar**.

    ![Especifique o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. No Olá **Adicionar controlador** caixa de diálogo, o controlador de Olá nome *BlobsController*e selecione **adicionar**.

    ![Controlador MVC do nome Olá](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Adicione Olá seguinte *utilizando* diretivas toohello `BlobsController.cs` ficheiro:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Criar um contentor de blob

Um contentor do blob é uma hierarquia aninhada de blobs e de pastas. Olá passos seguintes mostram como toocreate um contentor do blob:

> [!NOTE]
> 
> Olá código nesta secção assume que concluiu os passos de Olá na secção de Olá, [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `BlobsController.cs` ficheiro.

1. Adicione um método denominado **CreateBlobContainer** que devolve um **ActionResult**.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro do Olá **CreateBlobContainer** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Utilize Olá seguintes código tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação de configuração de serviço do Azure Olá. (Alterar  *&lt;nome da conta de armazenamento >* nome toohello Olá conta do storage do Azure que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob pretendido de toohello referência. Olá **CloudBlobClient.GetContainerReference** método não faz um pedido para o blob storage. referência de Olá é devolvida se ou não existe de contentor do blob Olá. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Chamar Olá **CloudBlobContainer.CreateIfNotExists** contentor de Olá de toocreate método se ainda não existir. Olá **CloudBlobContainer.CreateIfNotExists** método devolve **verdadeiro** se Olá contentor não existe e é criado com êxito. Caso contrário, **falso** é devolvido.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. Olá atualização **ViewBag** com o nome de Olá do contentor de blob Olá.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **Blobs**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **CreateBlobContainer** para nome da vista Olá e selecione **adicionar**.

1. Abra `CreateBlobContainer.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Executar a aplicação Olá e selecione **criar contentor de Blob** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Criar contentor de blob](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    Como mencionado anteriormente, Olá **CloudBlobContainer.CreateIfNotExists** método devolve **verdadeiro** apenas quando o contentor de Olá não existe e é criado. Por conseguinte, se executar a aplicação Olá quando Olá contentor existe, o método de Olá devolve **falso**. toorun Olá aplicação várias vezes, tem de eliminar o contentor de Olá antes de executar a aplicação Olá novamente. Eliminar contentor de Olá pode ser feito através de Olá **CloudBlobContainer.Delete** método. Também pode eliminar o contentor de Olá utilizando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="upload-a-blob-into-a-blob-container"></a>Carregar um blob para um contentor do blob

Assim que tiver [criou um contentor de blob](#create-a-blob-container), pode carregar ficheiros para esse contentor. Esta secção explica o carregamento de um contentor do blob tooa ficheiro local. Olá passos partem do princípio de que criou um contentor do blob denominado *contentor de BLOBs de teste*. 

> [!NOTE]
> 
> Olá código nesta secção assume que concluiu os passos de Olá na secção de Olá, [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `BlobsController.cs` ficheiro.

1. Adicione um método denominado **UploadBlob** que devolve um **EmptyResult**.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Dentro do Olá **UploadBlob** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob de toohello referência. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Tal como explicado anteriormente, o storage do Azure suporta tipos de blob diferente. tooretrieve um blob de página de tooa de referência, chamada Olá **CloudBlobContainer.GetPageBlobReference** método. tooretrieve um blob de bloco de tooa de referência, chamada Olá **CloudBlobContainer.GetBlockBlobReference** método. Normalmente, o blob de bloco é Olá recomendado toouse de tipo. (Alterar < nome do blob > * toohello nome blob de Olá toogive uma vez carregado.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Depois de ter uma referência de blob, pode carregar qualquer tooit de fluxo de dados, chamando Olá blob o objecto de referência **UploadFromStream** método. Olá **UploadFromStream** método cria blob Olá, se não existir ou substitui-lo se existir. (Alterar  *&lt;carregamento do ficheiro >* tooa totalmente qualificado ficheiro toohello de caminho que pretende tooupload.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **Blobs**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Executar a aplicação Olá e selecione **carregar blob**.  
  
Olá secção - [listar Olá blobs num contentor de blob](#list-the-blobs-in-a-blob-container) -ilustra como Olá toolist blobs num contentor de blob.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Lista Olá blobs num contentor de blob

Esta secção ilustra como Olá toolist blobs num contentor de blob. código de exemplo de Olá referencia Olá *contentor de BLOBs de teste* criou na secção de Olá, [criar um contentor de blob](#create-a-blob-container).

> [!NOTE]
> 
> Olá código nesta secção assume que concluiu os passos de Olá na secção de Olá, [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `BlobsController.cs` ficheiro.

1. Adicione um método denominado **ListBlobs** que devolve um **ActionResult**.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro do Olá **ListBlobs** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob de toohello referência. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. os blobs de Olá toolist num contentor de BLOBs, utilize Olá **CloudBlobContainer.ListBlobs** método. Olá **CloudBlobContainer.ListBlobs** método devolve um **IListBlobItem** objeto que converter tooa **CloudBlockBlob**, **CloudPageBlob**, ou **CloudBlobDirectory** objeto. Olá fragmento de código seguinte enumera todos os Olá blobs no contentor do blob. Cada blob está converter toohello adequado o objeto com base no respetivo tipo e o respetivo nome (ou URI no caso de Olá de um **CloudBlobDirectory**) está adicionada tooa lista.

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

    Na adição tooblobs, contentores de blob podem conter diretórios. Vamos imaginar que tem um contentor do blob denominado *contentor de BLOBs de teste* com Olá hierarquia os seguintes:

        foo.png
        dir1/bar.png
        dir2/baz.png

    Utilizar Olá anterior exemplo de código, Olá **blobs** lista de cadeias contém seguinte de toohello semelhante valores:

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    Como pode ver, a lista de Olá inclui apenas Olá nível superior entidades; Olá não aninhado aqueles (*bar.png* e *baz.png*). toolist Olá todas as entidades dentro de um contentor de blob, tem de chamar Olá **CloudBlobContainer.ListBlobs** método e passar **verdadeiro** para Olá **useFlatBlobListing** parâmetro.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    Olá definição **useFlatBlobListing** parâmetro demasiado**verdadeiro** devolve uma lista não hierárquica de todas as entidades no contentor de blob Olá e gera Olá os seguintes resultados:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **Blobs**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **ListBlobs** para nome da vista Olá e selecione **adicionar**.

1. Abra `ListBlobs.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

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

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Executar a aplicação Olá e selecione **listar blobs** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Lista de blob](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Transferir blobs

Esta secção ilustra como toodownload um blob e a manter-toolocal armazenamento ou leitura Olá do conteúdo numa cadeia. código de exemplo de Olá referencia Olá *contentor de BLOBs de teste* criou na secção de Olá, [criar um contentor de blob](#create-a-blob-container).

1. Abra Olá `BlobsController.cs` ficheiro.

1. Adicione um método denominado **DownloadBlob** que devolve um **ActionResult**.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Dentro do Olá **DownloadBlob** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob de toohello referência. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. A obtenção de um objeto de referência de blob chamando **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference** método. (Alterar  *&lt;nome do blob >* toohello nome do blob Olá estiver a transferir.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload um blob, utilize Olá **CloudBlockBlob.DownloadToStream** ou **CloudPageBlob.DownloadToStream** método, dependendo do tipo de blob Olá. Olá seguinte fragmento de código utiliza Olá **CloudBlockBlob.DownloadToStream** tootransfer método fluxo de tooa de conteúdo de um blob de objeto que é persistente, em seguida, ficheiro local tooa: (alteração  *&lt;nome de ficheiro local >* toohello totalmente qualificado representando de nome de ficheiro onde pretende que o blob Olá transferido.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Executar a aplicação Olá e selecione **transferir BLOBs** blob de Olá toodownload. blob Olá especificado no Olá **CloudBlobContainer.GetBlockBlobReference** chamada de método transfere localização toohello especificou nas Olá **File.OpenWrite** chamada de método. 

## <a name="delete-blobs"></a>Eliminar blobs

Olá passos seguintes mostram como toodelete um blob:

> [!NOTE]
> 
> Olá código nesta secção assume que concluiu os passos de Olá na secção de Olá, [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `BlobsController.cs` ficheiro.

1. Adicione um método denominado **DeleteBlob** que devolve um **ActionResult**.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. Obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obter um **CloudBlobClient** objeto representa um cliente do serviço blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contentor do blob de toohello referência. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. A obtenção de um objeto de referência de blob chamando **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference** método. (Alterar  *&lt;nome do blob >* toohello nome do blob Olá serão eliminados.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Executar a aplicação Olá e selecione **eliminar BLOBs** blob de Olá toodelete especificado no Olá **CloudBlobContainer.GetBlockBlobReference** chamada de método. 

## <a name="next-steps"></a>Passos seguintes
Ver mais toolearn de guias de funcionalidades sobre as opções adicionais para armazenar dados no Azure.

  * [Introdução ao table storage do Azure e o Visual Studio ligado serviços (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
  * [Introdução ao armazenamento de filas do Azure e o Visual Studio ligado serviços (ASP.NET)](vs-storage-aspnet-getting-started-queues.md)
