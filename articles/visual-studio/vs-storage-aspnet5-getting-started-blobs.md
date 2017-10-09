---
title: "aaaGet começar a utilizar o blob storage e o Visual Studio serviços ligados (ASP.NET Core) | Microsoft Docs"
description: "Como tooget iniciado utilizando o Blob storage do Azure num projeto Visual Studio ASP.NET Core depois de criar uma conta de armazenamento com o Visual Studio ligada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="e531c-103">Introdução ao Blob do Azure Visual Studio e de armazenamento ligado serviços (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="e531c-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="e531c-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="e531c-104">Overview</span></span>
<span data-ttu-id="e531c-105">Este artigo descreve como tooget iniciado utilizando o Blob storage do Azure no Visual Studio depois de ter criado ou referenciada uma conta de armazenamento do Azure num projeto ASP.NET Core, utilizando a caixa de diálogo do Olá Visual Studio adicionar ligado serviços.</span><span class="sxs-lookup"><span data-stu-id="e531c-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="e531c-106">Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e531c-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="e531c-107">Um blob único pode ser qualquer dimensão.</span><span class="sxs-lookup"><span data-stu-id="e531c-107">A single blob can be any size.</span></span> <span data-ttu-id="e531c-108">Os BLOBs podem ser coisas como imagens, ficheiros de áudio e vídeos, dados não processados e ficheiros do documento.</span><span class="sxs-lookup"><span data-stu-id="e531c-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="e531c-109">Este artigo descreve como tooget ao blob storage depois de criar uma conta de armazenamento do Azure utilizando Olá Visual Studio **adicionar serviços ligados** diálogo num projeto ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e531c-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="e531c-110">Tal como em direto de ficheiros em pastas, blobs de armazenamento em direto nos contentores.</span><span class="sxs-lookup"><span data-stu-id="e531c-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="e531c-111">Depois de ter criado um armazenamento, crie um ou mais contentores no armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="e531c-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="e531c-112">Por exemplo, um armazenamento chamado "Scrapbook", pode criar contentores no armazenamento de Olá chamado imagens de toostore "imagens" e outra denominada "áudio" toostore ficheiros áudio.</span><span class="sxs-lookup"><span data-stu-id="e531c-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="e531c-113">Depois de criar contentores de Olá, pode carregar blob individuais toothem de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="e531c-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="e531c-114">Consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) para obter mais informações sobre manipular programaticamente os blobs.</span><span class="sxs-lookup"><span data-stu-id="e531c-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="e531c-115">Contentores de BLOBs de acesso no código</span><span class="sxs-lookup"><span data-stu-id="e531c-115">Access blob containers in code</span></span>
<span data-ttu-id="e531c-116">tooprogrammatically aceder aos blobs em projetos de ASP.NET Core, terá de Olá tooadd seguintes itens, se não estiverem já presentes.</span><span class="sxs-lookup"><span data-stu-id="e531c-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="e531c-117">Adicione Olá seguir superior toohello de declarações de espaço de nomes do código de qualquer ficheiro c# em que pretende acesso tooprogrammatically storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="e531c-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="e531c-118">Obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e531c-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="e531c-119">Utilize Olá tooget de código a seguir a cadeia de ligação de armazenamento e as informações da configuração de serviço do Azure Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e531c-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="e531c-120">**Nota:** utilize todas Olá acima código à frente do código Olá Olá secções a seguir.</span><span class="sxs-lookup"><span data-stu-id="e531c-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="e531c-121">Utilize um **CloudBlobClient** objeto tooget um **CloudBlobContainer** referência tooan existente num contentor na sua conta do storage.</span><span class="sxs-lookup"><span data-stu-id="e531c-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="e531c-122">Criar um contentor no código</span><span class="sxs-lookup"><span data-stu-id="e531c-122">Create a container in code</span></span>
<span data-ttu-id="e531c-123">Também pode utilizar Olá **CloudBlobClient** toocreate um contentor na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e531c-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="e531c-124">Tudo o que precisa toodo é demasiado tooadd uma chamada**CreateIfNotExistsAsync** como Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="e531c-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="e531c-125">**Nota:** Olá APIs que efetuar chamadas tooAzure armazenamento em ASP.NET Core são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="e531c-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="e531c-126">Consulte [programação assíncrona com Async-Await](http://msdn.microsoft.com/library/hh191443.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e531c-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="e531c-127">código de Olá abaixo parte do princípio de métodos de programação assíncrona estão a ser utilizados.</span><span class="sxs-lookup"><span data-stu-id="e531c-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="e531c-128">toomake Olá ficheiros Olá contentor disponíveis tooeveryone, pode definir Olá contentor toobe público utilizando Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="e531c-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="e531c-129">Carregar um blob para um contentor</span><span class="sxs-lookup"><span data-stu-id="e531c-129">Upload a blob into a container</span></span>
<span data-ttu-id="e531c-130">tooupload um ficheiro de BLOBs num contentor, obtenha uma referência de contentor e utilizá-lo tooget uma referência de blob.</span><span class="sxs-lookup"><span data-stu-id="e531c-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="e531c-131">Depois de ter uma referência de blob, pode carregar qualquer fluxo de dados tooit ao chamar Olá **UploadFromStreamAsync** método.</span><span class="sxs-lookup"><span data-stu-id="e531c-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="e531c-132">Esta operação cria blob Olá se não estiver lá, ou substitui-lo se existir.</span><span class="sxs-lookup"><span data-stu-id="e531c-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="e531c-133">Olá seguinte exemplo mostra como tooupload um blob para um contentor e parte do princípio de que contentor Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="e531c-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="e531c-134">Lista Olá blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="e531c-134">List hello blobs in a container</span></span>
<span data-ttu-id="e531c-135">os blobs de Olá toolist num contentor, obtenha primeiro uma referência de contentor.</span><span class="sxs-lookup"><span data-stu-id="e531c-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="e531c-136">Em seguida, pode chamar do contentor de Olá **ListBlobsSegmentedAsync** blobs do método tooretrieve Olá e/ou os diretórios dentro do mesmo.</span><span class="sxs-lookup"><span data-stu-id="e531c-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="e531c-137">tooaccess Olá conjunto avançado de propriedades e métodos de um **IListBlobItem**, tem de o transmitir-tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="e531c-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="e531c-138">Se não souber blob Olá escreva, pode utilizar um toodetermine de verificação do tipo que toocast para.</span><span class="sxs-lookup"><span data-stu-id="e531c-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="e531c-139">Olá seguinte código demonstra como tooretrieve e de saída Olá URI de cada item no contentor.</span><span class="sxs-lookup"><span data-stu-id="e531c-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

<span data-ttu-id="e531c-140">Existem outras formas toolist Olá conteúdo um contentor do blob.</span><span class="sxs-lookup"><span data-stu-id="e531c-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="e531c-141">Consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e531c-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="e531c-142">Transferir um blob</span><span class="sxs-lookup"><span data-stu-id="e531c-142">Download a blob</span></span>
<span data-ttu-id="e531c-143">toodownload um blob, obtenha primeiro um blob de toohello de referência e, em seguida, chame Olá **DownloadToStreamAsync** método.</span><span class="sxs-lookup"><span data-stu-id="e531c-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="e531c-144">Olá exemplo seguinte utiliza Olá **DownloadToStreamAsync** método tootransfer Olá blob conteúdo tooa objeto de fluxo que, em seguida, pode guardar como um ficheiro local.</span><span class="sxs-lookup"><span data-stu-id="e531c-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="e531c-145">Existem outras formas toosave blobs como ficheiros.</span><span class="sxs-lookup"><span data-stu-id="e531c-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="e531c-146">Consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e531c-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="e531c-147">Eliminar um blob</span><span class="sxs-lookup"><span data-stu-id="e531c-147">Delete a blob</span></span>
<span data-ttu-id="e531c-148">toodelete um blob, obtenha primeiro um blob de toohello de referência e, em seguida, chame Olá **DeleteAsync** método.</span><span class="sxs-lookup"><span data-stu-id="e531c-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="e531c-149">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e531c-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

