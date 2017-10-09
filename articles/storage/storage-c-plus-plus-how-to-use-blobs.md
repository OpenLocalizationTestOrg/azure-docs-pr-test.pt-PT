---
title: aaaHow toouse blob storage (armazenamento de objeto) do C++ | Microsoft Docs
description: "Armazene dados não estruturados na nuvem de Olá Blob Storage do Azure (armazenamento de objetos)."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="1e2f9-103">Como toouse Blob Storage do C++</span><span class="sxs-lookup"><span data-stu-id="1e2f9-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="1e2f9-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="1e2f9-104">Overview</span></span>
<span data-ttu-id="1e2f9-105">Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="1e2f9-106">O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="1e2f9-107">O blob storage também é referido tooas armazenamento de objetos.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="1e2f9-108">Este guia demonstrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="1e2f9-109">Exemplos de Olá são escritos em C++ e utilizar Olá [biblioteca de clientes do Storage do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="1e2f9-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="1e2f9-110">Olá os cenários abrangidos incluem **carregar**, **listagem**, **transferir**, e **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="1e2f9-111">Destinos neste guia Olá biblioteca de clientes do Storage do Azure para C++ versão 1.0.0 e acima.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="1e2f9-112">Olá recomendada de versão é biblioteca de clientes de armazenamento 2.2.0, que está disponível através de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="1e2f9-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="1e2f9-113">Criar uma aplicação do C++</span><span class="sxs-lookup"><span data-stu-id="1e2f9-113">Create a C++ application</span></span>
<span data-ttu-id="1e2f9-114">Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação de C++.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="1e2f9-115">toodo por isso, terá de tooinstall hello biblioteca de clientes do Storage do Azure para C++ e criar uma conta de armazenamento do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="1e2f9-116">Olá tooinstall biblioteca de clientes do Storage do Azure para C++, pode utilizar Olá seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="1e2f9-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="1e2f9-117">**Linux:** siga as instruções de Olá indicadas na Olá [biblioteca de clientes do Storage do Azure para o ficheiro Leia-me do C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="1e2f9-118">**Windows:** no Visual Studio, clique em **ferramentas > Gestor de pacotes NuGet > consola do Gestor de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="1e2f9-119">Seguinte Olá de tipo de comando para Olá [consola do Gestor de pacotes NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e prima **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="1e2f9-120">Pacote de instalação wastorage</span><span class="sxs-lookup"><span data-stu-id="1e2f9-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="1e2f9-121">Configurar o seu tooaccess aplicações armazenamento de BLOBs</span><span class="sxs-lookup"><span data-stu-id="1e2f9-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="1e2f9-122">Adicione a seguinte Olá incluem parte superior do toohello de declarações do ficheiro de C++ de olá onde pretende que os blobs storage do Azure toouse Olá APIs tooaccess:</span><span class="sxs-lookup"><span data-stu-id="1e2f9-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="1e2f9-123">Configurar uma cadeia de ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="1e2f9-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="1e2f9-124">Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="1e2f9-125">Quando em execução numa aplicação de cliente, tem de fornecer cadeia de ligação de armazenamento de Olá Olá seguir o formato, utilizando o nome de Olá do seu armazenamento conta e Olá armazenamento chave de acesso da conta de armazenamento de Olá listada no Olá [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="1e2f9-126">Para obter informações sobre as contas do storage e chaves de acesso, consulte [sobre contas de armazenamento do Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1e2f9-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="1e2f9-127">Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:</span><span class="sxs-lookup"><span data-stu-id="1e2f9-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="1e2f9-128">tootest a aplicação no seu computador local do Windows, pode utilizar Olá Microsoft Azure [emulador do storage](storage-use-emulator.md) que é instalado com Olá [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1e2f9-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="1e2f9-129">emulador do storage Olá é um utilitário que simula Olá tabela, fila e Blob serviços disponíveis no Azure no seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="1e2f9-130">Olá exemplo seguinte mostra como podem declarar um campo estático toohold Olá ligação cadeia tooyour local emulador do storage:</span><span class="sxs-lookup"><span data-stu-id="1e2f9-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="1e2f9-131">emulador do storage do Azure de toostart Olá, selecione Olá **iniciar** Olá botão ou prima **Windows** chave.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="1e2f9-132">Começa a escrever **emulador do Storage do Azure**e selecione **emulador do Storage do Microsoft Azure** da lista de Olá das aplicações.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="1e2f9-133">Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="1e2f9-134">Obter a cadeia de ligação</span><span class="sxs-lookup"><span data-stu-id="1e2f9-134">Retrieve your connection string</span></span>
<span data-ttu-id="1e2f9-135">Pode utilizar Olá **cloud_storage_account** classe toorepresent informações da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="1e2f9-136">tooretrieve informações da cadeia de ligação de armazenamento Olá de conta de armazenamento, pode utilizar Olá **analisar** método.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="1e2f9-137">Em seguida, obter uma referência tooa **cloud_blob_client** como permite-lhe tooretrieve objetos que representam a contentores e blobs armazenados no Olá serviço de armazenamento de BLOBs de classe.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="1e2f9-138">Olá código seguinte cria um **cloud_blob_client** objeto utilizando o objeto de conta de armazenamento de Olá vamos obter acima:</span><span class="sxs-lookup"><span data-stu-id="1e2f9-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="1e2f9-139">Como: criar um contentor</span><span class="sxs-lookup"><span data-stu-id="1e2f9-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="1e2f9-140">Este exemplo mostra como toocreate um contentor se já existir:</span><span class="sxs-lookup"><span data-stu-id="1e2f9-140">This example shows how toocreate a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="1e2f9-141">Por predefinição, Olá novo contentor é privado e tem de especificar os blobs de toodownload chave de acesso de armazenamento deste contentor.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="1e2f9-142">Se pretender que os ficheiros de Olá toomake (blobs) dentro de Olá contentor disponíveis tooeveryone, pode definir Olá contentor toobe público utilizando Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="1e2f9-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="1e2f9-143">Qualquer pessoa na Internet de Olá pode ver os blobs num contentor público, mas pode modificar ou eliminá-los apenas se tiver a chave de acesso adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="1e2f9-144">Como: carregar um blob para um contentor</span><span class="sxs-lookup"><span data-stu-id="1e2f9-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="1e2f9-145">O Blob Storage do Azure suporta blobs de blocos e blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="1e2f9-146">Na maioria dos casos de Olá, o blob de bloco é Olá recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="1e2f9-147">tooupload um blob de blocos do ficheiro tooa, obtenha uma referência de contentor e utilizá-lo tooget uma referência de blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="1e2f9-148">Depois de ter uma referência de blob, pode carregar qualquer fluxo de dados tooit ao chamar Olá **upload_from_stream** método.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="1e2f9-149">Esta operação irá criar blob Olá se que não exista, ou substituí-lo se existir.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="1e2f9-150">Olá seguinte exemplo mostra como tooupload um blob para um contentor e parte do princípio de que contentor Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="1e2f9-151">Em alternativa, pode utilizar Olá **upload_from_file** tooupload método um blob de bloco de tooa do ficheiro.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="1e2f9-152">Como: listar Olá blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="1e2f9-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="1e2f9-153">os blobs de Olá toolist num contentor, obtenha primeiro uma referência de contentor.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="1e2f9-154">Em seguida, pode utilizar um contentor Olá **list_blobs** blobs do método tooretrieve Olá e/ou os diretórios dentro do mesmo.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="1e2f9-155">tooaccess Olá conjunto avançado de propriedades e métodos de um **list_blob_item**, tem de chamar Olá **list_blob_item.as_blob** método tooget um **cloud_blob** objeto, ou Olá **list_blob.as_directory** método tooget um objeto de cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="1e2f9-156">Olá código seguinte demonstra como tooretrieve e de saída Olá URI de cada item no Olá **contentor my exemplo** contentor:</span><span class="sxs-lookup"><span data-stu-id="1e2f9-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="1e2f9-157">Para obter mais detalhes sobre operações de listagem, consulte [lista de recursos de armazenamento do Azure em C++](storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="1e2f9-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="1e2f9-158">Como: Transferir blobs</span><span class="sxs-lookup"><span data-stu-id="1e2f9-158">How to: Download blobs</span></span>
<span data-ttu-id="1e2f9-159">toodownload blobs, obtenha primeiro uma referência de blob e, em seguida, chame Olá **download_to_stream** método.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="1e2f9-160">Olá exemplo seguinte utiliza Olá **download_to_stream** método tootransfer Olá blob conteúdo tooa objeto de fluxo, em seguida, pode manter tooa de ficheiros local.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="1e2f9-161">Em alternativa, pode utilizar Olá **download_to_file** método toodownload Olá conteúdo de um blob tooa ficheiro.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="1e2f9-162">Além disso, também pode utilizar Olá **download_text** método toodownload Olá conteúdo um blob como uma cadeia de texto.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="1e2f9-163">Como: eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="1e2f9-163">How to: Delete blobs</span></span>
<span data-ttu-id="1e2f9-164">toodelete um blob, obtenha primeiro uma referência de blob e, em seguida, chame Olá **delete_blob** método.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="1e2f9-165">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1e2f9-165">Next steps</span></span>
<span data-ttu-id="1e2f9-166">Agora que aprendeu Olá Noções básicas do blob storage, siga estas toolearn ligações mais sobre o Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e2f9-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="1e2f9-167">Como toouse armazenamento de filas do C++</span><span class="sxs-lookup"><span data-stu-id="1e2f9-167">How toouse Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="1e2f9-168">Como toouse Table Storage do C++</span><span class="sxs-lookup"><span data-stu-id="1e2f9-168">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="1e2f9-169">Recursos de armazenamento do Azure de lista em C++</span><span class="sxs-lookup"><span data-stu-id="1e2f9-169">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="1e2f9-170">Biblioteca de clientes do Storage para referência do C++</span><span class="sxs-lookup"><span data-stu-id="1e2f9-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="1e2f9-171">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="1e2f9-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="1e2f9-172">Transferência de dados com Olá utilitário de linha de comandos AzCopy</span><span class="sxs-lookup"><span data-stu-id="1e2f9-172">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)

