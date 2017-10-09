---
title: "aaaGet começar a utilizar o blob storage e o Visual Studio serviços ligados (Serviços de cloud) | Microsoft Docs"
description: "Como tooget iniciado utilizando o armazenamento de Blobs do Azure num projeto de serviço em nuvem no Visual Studio depois de ligar tooa conta de armazenamento com o Visual Studio ligada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="2a08c-103">Introdução ao Blob Storage do Azure e o Visual Studio ligado serviços (projetos de serviços de nuvem)</span><span class="sxs-lookup"><span data-stu-id="2a08c-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="2a08c-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="2a08c-104">Overview</span></span>
<span data-ttu-id="2a08c-105">Este artigo descreve como tooget começar a utilizar armazenamento de Blobs do Azure após a criação ou referenciada uma conta de armazenamento do Azure utilizando Olá Visual Studio **adicionar serviços ligados** projeto dos serviços de caixa de diálogo numa nuvem Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a08c-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="2a08c-106">Vamos mostrar-lhe como tooaccess e criar contentores de BLOBs e que as tarefas comuns tooperform como carregar, listar e transferir os blobs.</span><span class="sxs-lookup"><span data-stu-id="2a08c-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="2a08c-107">Exemplos de Olá são escritos no C\# e utilizar Olá [biblioteca do cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a08c-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="2a08c-108">Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2a08c-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="2a08c-109">Um blob único pode ser qualquer dimensão.</span><span class="sxs-lookup"><span data-stu-id="2a08c-109">A single blob can be any size.</span></span> <span data-ttu-id="2a08c-110">Os BLOBs podem ser coisas como imagens, ficheiros de áudio e vídeos, dados não processados e ficheiros do documento.</span><span class="sxs-lookup"><span data-stu-id="2a08c-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="2a08c-111">Tal como em direto de ficheiros em pastas, blobs de armazenamento em direto nos contentores.</span><span class="sxs-lookup"><span data-stu-id="2a08c-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="2a08c-112">Depois de ter criado um armazenamento, crie um ou mais contentores no armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a08c-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="2a08c-113">Por exemplo, um armazenamento chamado "Scrapbook", pode criar contentores no armazenamento de Olá chamado imagens de toostore "imagens" e outra denominada "áudio" toostore ficheiros áudio.</span><span class="sxs-lookup"><span data-stu-id="2a08c-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="2a08c-114">Depois de criar contentores de Olá, pode carregar blob individuais toothem de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="2a08c-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="2a08c-115">Para obter mais informações sobre manipular programaticamente os blobs, consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="2a08c-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="2a08c-116">Para obter informações gerais sobre o Storage do Azure, consulte [documentação do Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="2a08c-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="2a08c-117">Para obter informações gerais sobre os Cloud Services do Azure, consulte [documentação dos serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="2a08c-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="2a08c-118">Para obter mais informações sobre a programação de aplicações ASP.NET, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="2a08c-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="2a08c-119">Contentores de BLOBs de acesso no código</span><span class="sxs-lookup"><span data-stu-id="2a08c-119">Access blob containers in code</span></span>
<span data-ttu-id="2a08c-120">tooprogrammatically aceder aos blobs em projetos de serviço em nuvem, terá de Olá tooadd seguintes itens, se não estiverem já presentes.</span><span class="sxs-lookup"><span data-stu-id="2a08c-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="2a08c-121">Adicione Olá seguir superior toohello de declarações de espaço de nomes do código de qualquer ficheiro c# no qual pretende tooprogrammatically acesso Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a08c-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="2a08c-122">Obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2a08c-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a08c-123">Olá de utilização seguintes código tooget Olá a cadeia de ligação de armazenamento e as informações da configuração de serviço do Azure Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2a08c-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="2a08c-124">Obter um **CloudBlobClient** tooreference um contentor existente na sua conta de armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="2a08c-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="2a08c-125">Obter um **CloudBlobContainer** objeto tooreference um contentor de blob específico.</span><span class="sxs-lookup"><span data-stu-id="2a08c-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="2a08c-126">Utilize todas código Olá mostrado no procedimento anterior do Olá à frente do código Olá mostrado Olá secções a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a08c-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="2a08c-127">Criar um contentor no código</span><span class="sxs-lookup"><span data-stu-id="2a08c-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="2a08c-128">Algumas APIs que efetuar chamadas de saída tooAzure armazenamento no ASP.NET são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="2a08c-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="2a08c-129">Consulte [programação assíncrona com Async-Await](http://msdn.microsoft.com/library/hh191443.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="2a08c-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="2a08c-130">código de Olá no seguinte exemplo de Olá parte do princípio de que está a utilizar métodos assíncronos de programação.</span><span class="sxs-lookup"><span data-stu-id="2a08c-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="2a08c-131">toocreate um contentor na sua conta de armazenamento, tudo o que precisa toodo é adicionar uma chamada demasiado**CreateIfNotExistsAsync** como Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="2a08c-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="2a08c-132">toomake Olá ficheiros Olá contentor disponíveis tooeveryone, pode definir Olá contentor toobe público utilizando Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="2a08c-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="2a08c-133">Qualquer pessoa na Internet de Olá pode ver os blobs num contentor público, mas pode modificar ou eliminá-los apenas se tiver a chave de acesso adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="2a08c-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="2a08c-134">Carregar um blob para um contentor</span><span class="sxs-lookup"><span data-stu-id="2a08c-134">Upload a blob into a container</span></span>
<span data-ttu-id="2a08c-135">Storage do Azure suporta blobs de blocos e blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="2a08c-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="2a08c-136">Na maioria dos casos de Olá, o blob de bloco é Olá recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="2a08c-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="2a08c-137">tooupload um blob de blocos do ficheiro tooa, obtenha uma referência de contentor e utilizá-lo tooget uma referência de blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="2a08c-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="2a08c-138">Depois de ter uma referência de blob, pode carregar qualquer fluxo de dados tooit ao chamar Olá **UploadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="2a08c-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="2a08c-139">Esta operação cria blob Olá se anteriormente não existir ou substitui-lo se existir.</span><span class="sxs-lookup"><span data-stu-id="2a08c-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="2a08c-140">Olá seguinte exemplo mostra como tooupload um blob para um contentor e parte do princípio de que contentor Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="2a08c-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="2a08c-141">Lista Olá blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="2a08c-141">List hello blobs in a container</span></span>
<span data-ttu-id="2a08c-142">os blobs de Olá toolist num contentor, obtenha primeiro uma referência de contentor.</span><span class="sxs-lookup"><span data-stu-id="2a08c-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="2a08c-143">Em seguida, pode utilizar um contentor Olá **ListBlobs** blobs do método tooretrieve Olá e/ou os diretórios dentro do mesmo.</span><span class="sxs-lookup"><span data-stu-id="2a08c-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="2a08c-144">tooaccess Olá conjunto avançado de propriedades e métodos de um **IListBlobItem**, tem de o transmitir-tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="2a08c-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="2a08c-145">Se o tipo de Olá for desconhecido, pode utilizar o toodetermine de verificação de um tipo que toocast para.</span><span class="sxs-lookup"><span data-stu-id="2a08c-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="2a08c-146">Olá código seguinte demonstra como tooretrieve e de saída Olá URI de cada item no Olá **fotografias** contentor:</span><span class="sxs-lookup"><span data-stu-id="2a08c-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

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

<span data-ttu-id="2a08c-147">Conforme mostrado no exemplo de código anterior Olá, serviço de blob Olá tem o conceito de Olá de diretórios contentores, bem.</span><span class="sxs-lookup"><span data-stu-id="2a08c-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="2a08c-148">Isto é, de modo a que pode organizar os blobs numa estrutura mais semelhantes a pasta.</span><span class="sxs-lookup"><span data-stu-id="2a08c-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="2a08c-149">Por exemplo, considere o seguinte conjunto de blobs de blocos num contentor com o nome de Olá **fotografias**:</span><span class="sxs-lookup"><span data-stu-id="2a08c-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="2a08c-150">Quando chamar **ListBlobs** no contentor de Olá (tal como no exemplo anterior Olá), contém a coleção de Olá devolvida **CloudBlobDirectory** e **CloudBlockBlob** objetos que representam os diretórios de Olá e os blobs contidos no nível superior Olá.</span><span class="sxs-lookup"><span data-stu-id="2a08c-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="2a08c-151">Olá o resultado resultante é:</span><span class="sxs-lookup"><span data-stu-id="2a08c-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="2a08c-152">Opcionalmente, pode definir Olá **UseFlatBlobListing** parâmetro de Olá **ListBlobs** método **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="2a08c-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="2a08c-153">Isto resulta em todos os BLOBs que está a ser devolvido como uma **CloudBlockBlob**, independentemente do diretório.</span><span class="sxs-lookup"><span data-stu-id="2a08c-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="2a08c-154">Segue-se a chamada de Olá demasiado**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="2a08c-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="2a08c-155">e Eis resultados Olá:</span><span class="sxs-lookup"><span data-stu-id="2a08c-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="2a08c-156">Para obter mais informações, consulte [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a08c-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="2a08c-157">Transferir blobs</span><span class="sxs-lookup"><span data-stu-id="2a08c-157">Download blobs</span></span>
<span data-ttu-id="2a08c-158">toodownload blobs, obtenha primeiro uma referência de blob e, em seguida, chame Olá **DownloadToStream** método.</span><span class="sxs-lookup"><span data-stu-id="2a08c-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="2a08c-159">Olá exemplo seguinte utiliza Olá **DownloadToStream** método tootransfer Olá blob conteúdo tooa objeto de fluxo, em seguida, pode manter tooa de ficheiros local.</span><span class="sxs-lookup"><span data-stu-id="2a08c-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="2a08c-160">Também pode utilizar Olá **DownloadToStream** método toodownload Olá conteúdo um blob como uma cadeia de texto.</span><span class="sxs-lookup"><span data-stu-id="2a08c-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="2a08c-161">Eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="2a08c-161">Delete blobs</span></span>
<span data-ttu-id="2a08c-162">toodelete um blob, obtenha primeiro uma referência de blob e, em seguida, chame o **eliminar** método.</span><span class="sxs-lookup"><span data-stu-id="2a08c-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="2a08c-163">Listar blobs em páginas de forma assíncrona</span><span class="sxs-lookup"><span data-stu-id="2a08c-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="2a08c-164">Se está a listar um grande número de blobs ou pretende que o número de Olá toocontrol de resultados devolvido numa operação de listagem, pode listar os blobs em páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="2a08c-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="2a08c-165">Este exemplo mostra como tooreturn resulta nas páginas de forma assíncrona, para que a execução não fique bloqueada enquanto espera tooreturn um grande conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="2a08c-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="2a08c-166">Este exemplo mostra uma lista de BLOBs não hierárquica, mas também pode criar uma lista hierárquica ao definir Olá **useFlatBlobListing** parâmetro de Olá **ListBlobsSegmentedAsync** método demasiado **FALSO**.</span><span class="sxs-lookup"><span data-stu-id="2a08c-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="2a08c-167">Uma vez que o método de exemplo de Olá chama um método assíncrono, tem de ser precedido pela Olá **async** palavra-chave e tem de devolver um **tarefas** objeto.</span><span class="sxs-lookup"><span data-stu-id="2a08c-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="2a08c-168">Olá await palavra-chave especificada para Olá **ListBlobsSegmentedAsync** método suspende a execução do método de exemplo de Olá até concluir a tarefa de listagem Olá.</span><span class="sxs-lookup"><span data-stu-id="2a08c-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="2a08c-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2a08c-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

