---
title: "aaaGet iniciado com o Blob storage do Azure (armazenamento de objetos) através do .NET | Microsoft Docs"
description: "Armazene dados não estruturados na nuvem de Olá Blob Storage do Azure (armazenamento de objetos)."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 9b675ac073e7e901fe1afe54f7bfea12eefbf3ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="a292c-103">Introdução ao Blob Storage do Azure através do .NET</span><span class="sxs-lookup"><span data-stu-id="a292c-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="a292c-104">Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="a292c-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="a292c-105">O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação.</span><span class="sxs-lookup"><span data-stu-id="a292c-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="a292c-106">O blob storage também é referido tooas armazenamento de objetos.</span><span class="sxs-lookup"><span data-stu-id="a292c-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="a292c-107">Acerca deste tutorial</span><span class="sxs-lookup"><span data-stu-id="a292c-107">About this tutorial</span></span>
<span data-ttu-id="a292c-108">Este tutorial mostra como código de toowrite .NET para alguns cenários comuns utilizando o Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="a292c-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="a292c-109">Os cenários abrangidos incluem carregar, listar, transferir e eliminar blobs.</span><span class="sxs-lookup"><span data-stu-id="a292c-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="a292c-110">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="a292c-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="a292c-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a292c-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="a292c-112">Biblioteca de Clientes do Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="a292c-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="a292c-113">Gestor de Configuração do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="a292c-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="a292c-114">Uma [Conta do Storage do Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="a292c-114">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="a292c-115">Mais exemplos</span><span class="sxs-lookup"><span data-stu-id="a292c-115">More samples</span></span>
<span data-ttu-id="a292c-116">Para obter exemplos adicionais que utilizam o Armazenamento de Blobs, veja [Introdução ao Armazenamento de Blobs do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="a292c-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="a292c-117">Pode transferir a aplicação de exemplo de Olá e executá-la ou procurar Olá código no GitHub.</span><span class="sxs-lookup"><span data-stu-id="a292c-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="a292c-118">Adicionar com diretivas</span><span class="sxs-lookup"><span data-stu-id="a292c-118">Add using directives</span></span>
<span data-ttu-id="a292c-119">Adicione Olá seguinte **utilizando** diretivas toohello parte superior Olá `Program.cs` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="a292c-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="a292c-120">Analisar cadeia de ligação de Olá</span><span class="sxs-lookup"><span data-stu-id="a292c-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="a292c-121">Crie hello do cliente do serviço Blob</span><span class="sxs-lookup"><span data-stu-id="a292c-121">Create hello Blob service client</span></span>
<span data-ttu-id="a292c-122">Olá **CloudBlobClient** classe permite-lhe tooretrieve contentores e blobs armazenados no Blob storage.</span><span class="sxs-lookup"><span data-stu-id="a292c-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="a292c-123">Segue-se o cliente do serviço Olá toocreate unidirecional:</span><span class="sxs-lookup"><span data-stu-id="a292c-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="a292c-124">Agora, está pronto toowrite código que lê dados de e escreve tooBlob o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="a292c-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="a292c-125">Criar um contentor</span><span class="sxs-lookup"><span data-stu-id="a292c-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="a292c-126">Este exemplo mostra como toocreate um contentor se já existir:</span><span class="sxs-lookup"><span data-stu-id="a292c-126">This example shows how toocreate a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="a292c-127">Por predefinição, o novo contentor de Olá é privado, o que significa que terá de especificar os blobs de toodownload chave de acesso de armazenamento deste contentor.</span><span class="sxs-lookup"><span data-stu-id="a292c-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="a292c-128">Se pretender que os ficheiros de Olá toomake dentro Olá contentor disponíveis tooeveryone, pode definir Olá contentor toobe público utilizando Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="a292c-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="a292c-129">Qualquer pessoa na Internet de Olá pode ver os blobs num contentor público.</span><span class="sxs-lookup"><span data-stu-id="a292c-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="a292c-130">No entanto, pode modificar ou eliminá-los apenas se tiver a chave de acesso da conta adequada de Olá ou uma assinatura de acesso partilhado.</span><span class="sxs-lookup"><span data-stu-id="a292c-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="a292c-131">Carregar um blob para um contentor</span><span class="sxs-lookup"><span data-stu-id="a292c-131">Upload a blob into a container</span></span>
<span data-ttu-id="a292c-132">O Blob Storage do Azure suporta blobs de blocos e blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="a292c-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="a292c-133">Na maioria dos casos, o blob de bloco é Olá recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="a292c-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="a292c-134">tooupload um blob de blocos do ficheiro tooa, obtenha uma referência de contentor e utilizá-lo tooget uma referência de blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="a292c-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="a292c-135">Depois de ter uma referência de blob, pode carregar qualquer fluxo de dados tooit ao chamar Olá **UploadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="a292c-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="a292c-136">Esta operação cria blob Olá se anteriormente não existir ou substitui-lo se existir.</span><span class="sxs-lookup"><span data-stu-id="a292c-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="a292c-137">Olá seguinte exemplo mostra como tooupload um blob para um contentor e parte do princípio de que contentor Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="a292c-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="a292c-138">Lista Olá blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="a292c-138">List hello blobs in a container</span></span>
<span data-ttu-id="a292c-139">os blobs de Olá toolist num contentor, obtenha primeiro uma referência de contentor.</span><span class="sxs-lookup"><span data-stu-id="a292c-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="a292c-140">Em seguida, pode utilizar um contentor Olá **ListBlobs** blobs do método tooretrieve Olá e/ou os diretórios dentro do mesmo.</span><span class="sxs-lookup"><span data-stu-id="a292c-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="a292c-141">tooaccess Olá conjunto avançado de propriedades e métodos de um **IListBlobItem**, tem de o transmitir-tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="a292c-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="a292c-142">Se o tipo de Olá for desconhecido, pode utilizar o toodetermine de verificação de um tipo que toocast para.</span><span class="sxs-lookup"><span data-stu-id="a292c-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="a292c-143">Olá código seguinte demonstra como tooretrieve e de saída Olá URI de cada item no Olá _fotografias_ contentor:</span><span class="sxs-lookup"><span data-stu-id="a292c-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
{
    if (item.GetType() == typeof(CloudBlockBlob))
    {
        CloudBlockBlob blob = (CloudBlockBlob)item;

        Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

    }
    else if (item.GetType() == typeof(CloudPageBlob))
    {
        CloudPageBlob pageBlob = (CloudPageBlob)item;

        Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

    }
    else if (item.GetType() == typeof(CloudBlobDirectory))
    {
        CloudBlobDirectory directory = (CloudBlobDirectory)item;

        Console.WriteLine("Directory: {0}", directory.Uri);
    }
}
```

<span data-ttu-id="a292c-144">Ao incluir informações do caminho nos nomes de blobs, pode criar uma estrutura de diretório virtual que pode organizar e percorrer tal como faria com um sistema de ficheiros tradicional.</span><span class="sxs-lookup"><span data-stu-id="a292c-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="a292c-145">estrutura de diretórios Olá é virtual Olá apenas – apenas recursos disponíveis no Blob storage são contentores e blobs.</span><span class="sxs-lookup"><span data-stu-id="a292c-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="a292c-146">No entanto, biblioteca de clientes do storage Olá oferece um **CloudBlobDirectory** diretório virtual do toorefer tooa de objeto e simplificar o processo de Olá de trabalhar com blobs que se encontram organizados desta forma.</span><span class="sxs-lookup"><span data-stu-id="a292c-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="a292c-147">Por exemplo, considere o seguinte conjunto de blobs de blocos num contentor com o nome de Olá *fotografias*:</span><span class="sxs-lookup"><span data-stu-id="a292c-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

<span data-ttu-id="a292c-148">Quando chamar **ListBlobs** no Olá *fotografias* contentor (tal como no Olá precedente fragmento de código), é devolvida uma lista hierárquica.</span><span class="sxs-lookup"><span data-stu-id="a292c-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="a292c-149">Esta contém os **CloudBlobDirectory** e **CloudBlockBlob** objetos, que representam os diretórios de Olá e os blobs no contentor de Olá, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="a292c-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="a292c-150">saída resultante Olá tem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a292c-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="a292c-151">Opcionalmente, pode definir Olá **UseFlatBlobListing** parâmetro de Olá **ListBlobs** método **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="a292c-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="a292c-152">Neste caso, todos os BLOBs no contentor de Olá é devolvido como uma **CloudBlockBlob** objeto.</span><span class="sxs-lookup"><span data-stu-id="a292c-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="a292c-153">Olá chamada demasiado**ListBlobs** tooreturn uma lista não hierárquica tem o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="a292c-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="a292c-154">e resultados de Olá tem o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="a292c-154">and hello results look like this:</span></span>

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a><span data-ttu-id="a292c-155">Transferir blobs</span><span class="sxs-lookup"><span data-stu-id="a292c-155">Download blobs</span></span>
<span data-ttu-id="a292c-156">toodownload blobs, obtenha primeiro uma referência de blob e, em seguida, chame Olá **DownloadToStream** método.</span><span class="sxs-lookup"><span data-stu-id="a292c-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="a292c-157">Olá exemplo seguinte utiliza Olá **DownloadToStream** método tootransfer Olá blob conteúdo tooa objeto de fluxo, em seguida, pode manter tooa de ficheiros local.</span><span class="sxs-lookup"><span data-stu-id="a292c-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="a292c-158">Também pode utilizar Olá **DownloadToStream** método toodownload Olá conteúdo um blob como uma cadeia de texto.</span><span class="sxs-lookup"><span data-stu-id="a292c-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="a292c-159">Eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="a292c-159">Delete blobs</span></span>
<span data-ttu-id="a292c-160">toodelete um blob, obtenha primeiro uma referência de blob e, em seguida, chame o **eliminar** método.</span><span class="sxs-lookup"><span data-stu-id="a292c-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="a292c-161">Listar blobs em páginas de forma assíncrona</span><span class="sxs-lookup"><span data-stu-id="a292c-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="a292c-162">Se está a listar um grande número de blobs ou pretende que o número de Olá toocontrol de resultados devolvido numa operação de listagem, pode listar os blobs em páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="a292c-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="a292c-163">Este exemplo mostra como tooreturn resulta nas páginas de forma assíncrona, para que a execução não fique bloqueada enquanto espera tooreturn um grande conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="a292c-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="a292c-164">Este exemplo mostra uma lista de BLOBs não hierárquica, mas também pode criar uma lista hierárquica ao definir Olá _useFlatBlobListing_ parâmetro de Olá **ListBlobsSegmentedAsync** too_false_ de método.</span><span class="sxs-lookup"><span data-stu-id="a292c-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="a292c-165">Uma vez que o método de exemplo de Olá chama um método assíncrono, tem de ser precedido pela Olá _async_ palavra-chave e tem de devolver um **tarefas** objeto.</span><span class="sxs-lookup"><span data-stu-id="a292c-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="a292c-166">Olá await palavra-chave especificada para Olá **ListBlobsSegmentedAsync** método suspende a execução do método de exemplo de Olá até concluir a tarefa de listagem Olá.</span><span class="sxs-lookup"><span data-stu-id="a292c-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="a292c-167">Blob de acréscimo tooan de escrita</span><span class="sxs-lookup"><span data-stu-id="a292c-167">Writing tooan append blob</span></span>
<span data-ttu-id="a292c-168">Um blob de acréscimo está otimizado para operações de acréscimo, como o registo.</span><span class="sxs-lookup"><span data-stu-id="a292c-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="a292c-169">Como um blob de blocos, um blob de acréscimo é composto por blocos, mas quando adicionar um novo blob de acréscimo tooan de bloco, é sempre toohello anexado final do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="a292c-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="a292c-170">Não é possível atualizar ou eliminar um bloco existente num blob de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="a292c-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="a292c-171">o bloco de Olá IDs para um blob de acréscimo não são expostos como acontece para um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="a292c-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="a292c-172">Cada bloco num blob de acréscimo pode ter um tamanho diferente, cópia de segurança tooa máximo de 4 MB, e um blob de acréscimo pode incluir um máximo de 50 000 blocos.</span><span class="sxs-lookup"><span data-stu-id="a292c-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="a292c-173">Consequentemente, o tamanho máximo do Olá de um blob de acréscimo é ligeiramente superior a 195 GB (4 MB X 50 000 blocos).</span><span class="sxs-lookup"><span data-stu-id="a292c-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="a292c-174">exemplo de Olá abaixo cria um novo blob de acréscimo e acrescenta alguns dados tooit, simulando uma operação de registo simples.</span><span class="sxs-lookup"><span data-stu-id="a292c-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="a292c-175">Consulte [compreender os Blobs de blocos, Blobs de páginas e os Blobs de acréscimo](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) para obter mais informações sobre as diferenças de Olá entre tipos de Olá três de blobs.</span><span class="sxs-lookup"><span data-stu-id="a292c-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="a292c-176">Gerir a segurança dos blobs</span><span class="sxs-lookup"><span data-stu-id="a292c-176">Managing security for blobs</span></span>
<span data-ttu-id="a292c-177">Por predefinição, armazenamento do Azure mantém os seus dados seguros ao limitar acesso toohello proprietário da conta, que está na posse das chaves de acesso de conta Olá.</span><span class="sxs-lookup"><span data-stu-id="a292c-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="a292c-178">Quando precisar de dados de BLOBs de tooshare na sua conta de armazenamento, é importante toodo Sim sem comprometer a segurança de Olá das suas chaves de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="a292c-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="a292c-179">Além disso, pode encriptar tooensure de dados de BLOBs que estes estão seguros durante a transmissão Olá e no Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="a292c-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="a292c-180">Controlar o acesso tooblob dados</span><span class="sxs-lookup"><span data-stu-id="a292c-180">Controlling access tooblob data</span></span>
<span data-ttu-id="a292c-181">Por predefinição, dados de BLOBs de Olá na sua conta do storage são o proprietário da conta toostorage apenas acessíveis.</span><span class="sxs-lookup"><span data-stu-id="a292c-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="a292c-182">Autenticar pedidos para o Blob storage requer a chave de acesso da conta de Olá por predefinição.</span><span class="sxs-lookup"><span data-stu-id="a292c-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="a292c-183">No entanto, pode ser útil toomake determinados utilizadores tooother disponíveis de dados de Blobs.</span><span class="sxs-lookup"><span data-stu-id="a292c-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="a292c-184">Tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="a292c-184">You have two options:</span></span>

* <span data-ttu-id="a292c-185">**Acesso anónimo:** pode tornar um contentor ou os respetivos blobs publicamente disponíveis para acesso anónimo.</span><span class="sxs-lookup"><span data-stu-id="a292c-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="a292c-186">Consulte [gerir o acesso de leitura anónimo toocontainers e blobs](storage-manage-access-to-resources.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a292c-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="a292c-187">**Assinaturas de acesso partilhado:** pode fornecer aos clientes uma assinatura de acesso partilhado (SAS), que concede acesso delegado tooa recursos na sua conta de armazenamento, com as permissões que especificar e durante um intervalo que especificou.</span><span class="sxs-lookup"><span data-stu-id="a292c-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="a292c-188">Veja [Utilizar Assinaturas de Acesso Partilhado (SAS)](storage-dotnet-shared-access-signature-part-1.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a292c-188">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="a292c-189">Encriptar dados de blobs</span><span class="sxs-lookup"><span data-stu-id="a292c-189">Encrypting blob data</span></span>
<span data-ttu-id="a292c-190">Armazenamento do Azure suporta a encriptação de dados de BLOBs cliente Olá e no servidor de Olá:</span><span class="sxs-lookup"><span data-stu-id="a292c-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="a292c-191">**Encriptação do lado do cliente:** Olá biblioteca de clientes de armazenamento para .NET suporta a encriptação de dados dentro de aplicações de cliente antes de carregar tooAzure armazenamento e a desencriptação de dados ao transferir toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="a292c-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="a292c-192">biblioteca de Olá também suporta a integração com o Cofre de chaves do Azure para a gestão de chaves de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a292c-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="a292c-193">Consulte [Encriptação do Lado do Cliente com .NET para o Armazenamento do Microsoft Azure](storage-client-side-encryption.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a292c-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) for more information.</span></span> <span data-ttu-id="a292c-194">Consulte também [Tutorial: encriptar e desencriptar blobs no Armazenamento do Microsoft Azure com o Cofre de Chaves do Azure](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="a292c-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="a292c-195">**Encriptação do lado do servidor**: agora, o Storage do Azure suporta a encriptação do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="a292c-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="a292c-196">Consulte [Encriptação do Serviço do Storage do Azure para Dados Inativos (Pré-visualização)](storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="a292c-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a292c-197">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a292c-197">Next steps</span></span>
<span data-ttu-id="a292c-198">Agora que aprendeu Olá Noções básicas do Blob storage, siga estas toolearn ligações mais.</span><span class="sxs-lookup"><span data-stu-id="a292c-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="a292c-199">Explorador de Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a292c-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="a292c-200">[Explorador de armazenamento do Azure (MASE) da Microsoft](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="a292c-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="a292c-201">Exemplos de Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="a292c-201">Blob storage samples</span></span>
* [<span data-ttu-id="a292c-202">Introdução ao Armazenamento de Blobs do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="a292c-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="a292c-203">Referência do Blob Storage</span><span class="sxs-lookup"><span data-stu-id="a292c-203">Blob storage reference</span></span>
* [<span data-ttu-id="a292c-204">Referência da Biblioteca de Clientes do Storage para o .NET</span><span class="sxs-lookup"><span data-stu-id="a292c-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="a292c-205">Referência da API REST</span><span class="sxs-lookup"><span data-stu-id="a292c-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="a292c-206">Guias conceptuais</span><span class="sxs-lookup"><span data-stu-id="a292c-206">Conceptual guides</span></span>
* [<span data-ttu-id="a292c-207">Transferência de dados com Olá utilitário de linha de comandos AzCopy</span><span class="sxs-lookup"><span data-stu-id="a292c-207">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="a292c-208">Introdução ao Armazenamento de ficheiros do .NET</span><span class="sxs-lookup"><span data-stu-id="a292c-208">Get started with File storage for .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="a292c-209">Como o armazenamento com Olá SDK de WebJobs de BLOBs de toouse do Azure</span><span class="sxs-lookup"><span data-stu-id="a292c-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
