---
title: aaaDevelop para o File storage do Azure com o Java | Microsoft Docs
description: "Saiba como aplicações de Java toodevelop e serviços que utilizam toostore de armazenamento de ficheiros do Azure de ficheiros de dados."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="b92b2-103">Desenvolver para o File storage do Azure com Java</span><span class="sxs-lookup"><span data-stu-id="b92b2-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="b92b2-104">Acerca deste tutorial</span><span class="sxs-lookup"><span data-stu-id="b92b2-104">About this tutorial</span></span>
<span data-ttu-id="b92b2-105">Este tutorial demonstrar Noções básicas de Olá da utilização de aplicações do Java toodevelop ou serviços que utilizam dados de ficheiros de toostore de armazenamento de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="b92b2-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="b92b2-106">Neste tutorial, iremos criar uma aplicação de consola simples e Mostrar como tooperform ações básicas com o storage do Java e ficheiros do Azure:</span><span class="sxs-lookup"><span data-stu-id="b92b2-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="b92b2-107">Criar e eliminar as partilhas de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="b92b2-108">Criar e eliminar diretórios</span><span class="sxs-lookup"><span data-stu-id="b92b2-108">Create and delete directories</span></span>
* <span data-ttu-id="b92b2-109">Enumerar ficheiros e diretórios numa partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="b92b2-110">Carregar, transferir e eliminar um ficheiro</span><span class="sxs-lookup"><span data-stu-id="b92b2-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="b92b2-111">Porque o File storage do Azure pode ser acedido através de SMB, é possível toowrite aplicações simples que aceder à partilha de ficheiros do Azure Olá utilizar Olá padrão e/s de Java classes.</span><span class="sxs-lookup"><span data-stu-id="b92b2-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="b92b2-112">Este artigo descreve como toowrite aplicações que utilizam Olá SDK de Java do Azure armazenamento, que utiliza Olá [File storage do Azure REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure armazenamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="b92b2-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="b92b2-113">Criar uma aplicação Java</span><span class="sxs-lookup"><span data-stu-id="b92b2-113">Create a Java application</span></span>
<span data-ttu-id="b92b2-114">amostras de Olá toobuild, terá de Olá Kit de desenvolvimento Java (JDK) e Olá [SDK de armazenamento do Azure para Java] [-].</span><span class="sxs-lookup"><span data-stu-id="b92b2-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="b92b2-115">Deve também criou uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b92b2-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="b92b2-116">Configurar a sua aplicação toouse File storage do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="b92b2-117">Olá toouse storage do Azure APIs, adicionar Olá seguir parte superior do toohello de declaração do ficheiro de Java de olá onde pretende tooaccess Olá armazenamento serviço.</span><span class="sxs-lookup"><span data-stu-id="b92b2-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="b92b2-118">Configurar uma cadeia de ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="b92b2-119">toouse File storage do Azure, terá de tooconnect tooyour conta de armazenamento Azure.</span><span class="sxs-lookup"><span data-stu-id="b92b2-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="b92b2-120">Olá primeiro passo seria tooconfigure uma cadeia de ligação que iremos utilizar conta de armazenamento de tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b92b2-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="b92b2-121">Vamos definir um toodo variável estática que.</span><span class="sxs-lookup"><span data-stu-id="b92b2-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="b92b2-122">Substitua os valores reais Olá para a sua conta de armazenamento your_storage_account_name e your_storage_account_key.</span><span class="sxs-lookup"><span data-stu-id="b92b2-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="b92b2-123">Ligar tooan conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="b92b2-124">conta de armazenamento de tooyour tooconnect, terá de toouse Olá **CloudStorageAccount** objeto, transmitir um tooits de cadeia de ligação **analisar** método.</span><span class="sxs-lookup"><span data-stu-id="b92b2-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="b92b2-125">**CloudStorageAccount.parse** gera um InvalidKeyException, pelo que terá tooput-lo dentro de um catch/tente bloquear.</span><span class="sxs-lookup"><span data-stu-id="b92b2-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="b92b2-126">Criar uma partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-126">Create an Azure File share</span></span>
<span data-ttu-id="b92b2-127">Todos os ficheiros e diretórios no File storage do Azure residem num contentor chamado um **partilha**.</span><span class="sxs-lookup"><span data-stu-id="b92b2-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="b92b2-128">A conta do storage pode ter o mesmo partilhas que permite a capacidade de conta.</span><span class="sxs-lookup"><span data-stu-id="b92b2-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="b92b2-129">partilha de tooa tooobtain acesso e o respetivo conteúdo, terá de toouse um cliente de armazenamento de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="b92b2-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="b92b2-130">Utilizando o cliente de armazenamento de ficheiros do Azure de Olá, em seguida, pode obter uma partilha de tooa de referência.</span><span class="sxs-lookup"><span data-stu-id="b92b2-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="b92b2-131">tooactually criar partilha de Olá, utilize Olá **createIfNotExists** método de Olá CloudFileShare objeto.</span><span class="sxs-lookup"><span data-stu-id="b92b2-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="b92b2-132">Neste momento, **partilhar** contém uma partilha de tooa referência denominada **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="b92b2-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="b92b2-133">Eliminar uma partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-133">Delete an Azure File share</span></span>
<span data-ttu-id="b92b2-134">Eliminar uma partilha é feito ao chamar Olá **deleteIfExists** método num objeto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="b92b2-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="b92b2-135">Eis o código de exemplo que suporta que.</span><span class="sxs-lookup"><span data-stu-id="b92b2-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="b92b2-136">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="b92b2-136">Create a directory</span></span>
<span data-ttu-id="b92b2-137">Também pode organizar armazenamento colocando os ficheiros secundárias diretórios em vez de ter todos eles no diretório de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="b92b2-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="b92b2-138">File storage do Azure permite-lhe toocreate como permitem muito diretórios como será a conta.</span><span class="sxs-lookup"><span data-stu-id="b92b2-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="b92b2-139">código de Olá abaixo irá criar um subdiretório com o nome **sampledir** no diretório de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="b92b2-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="b92b2-140">Eliminar um diretório</span><span class="sxs-lookup"><span data-stu-id="b92b2-140">Delete a directory</span></span>
<span data-ttu-id="b92b2-141">Eliminar um diretório é uma tarefa bastante simple, embora deve ser salientado que não é possível eliminar um diretório que contiver ficheiros ou outros diretórios.</span><span class="sxs-lookup"><span data-stu-id="b92b2-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="b92b2-142">Enumerar ficheiros e diretórios numa partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="b92b2-143">Obter uma lista de ficheiros e diretórios dentro de uma partilha facilmente é feito chamando **listFilesAndDirectories** numa referência CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="b92b2-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="b92b2-144">método de Olá devolve uma lista de objetos de ListFileItem que pode iterar.</span><span class="sxs-lookup"><span data-stu-id="b92b2-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="b92b2-145">Por exemplo, hello código seguinte irá listar ficheiros e diretórios dentro do diretório de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="b92b2-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="b92b2-146">Carregar um ficheiro</span><span class="sxs-lookup"><span data-stu-id="b92b2-146">Upload a file</span></span>
<span data-ttu-id="b92b2-147">Um ficheiro de Azure partilha contém em Olá muito menos, um diretório de raiz, onde podem residir os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="b92b2-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="b92b2-148">Nesta secção, irá aprender como tooupload um ficheiro a partir do armazenamento local para Olá raiz do diretório de uma partilha.</span><span class="sxs-lookup"><span data-stu-id="b92b2-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="b92b2-149">Olá primeiro passo para carregar um ficheiro é tooobtain um diretório de toohello de referência onde deve residir.</span><span class="sxs-lookup"><span data-stu-id="b92b2-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="b92b2-150">Pode fazê-lo ao chamar Olá **getRootDirectoryReference** método do objeto de partilha de Olá.</span><span class="sxs-lookup"><span data-stu-id="b92b2-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="b92b2-151">Agora que tem um diretório de raiz de toohello de referência da partilha de Olá, pode carregar um ficheiro no mesmo utilizando Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="b92b2-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="b92b2-152">Transferir um ficheiro</span><span class="sxs-lookup"><span data-stu-id="b92b2-152">Download a file</span></span>
<span data-ttu-id="b92b2-153">Uma das Olá induzirem mais frequentes operações que irá executar contra File storage do Azure é ficheiros toodownload.</span><span class="sxs-lookup"><span data-stu-id="b92b2-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="b92b2-154">No seguinte exemplo de Olá, código de Olá transfere SampleFile.txt e apresenta o respetivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="b92b2-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="b92b2-155">Eliminar um ficheiro</span><span class="sxs-lookup"><span data-stu-id="b92b2-155">Delete a file</span></span>
<span data-ttu-id="b92b2-156">Há outra operação de armazenamento de ficheiros do Azure comum é a eliminação de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="b92b2-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="b92b2-157">Olá seguinte código elimina um ficheiro denominado SampleFile.txt armazenados dentro de um diretório com o nome **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="b92b2-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="b92b2-158">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b92b2-158">Next steps</span></span>
<span data-ttu-id="b92b2-159">Se quiser toolearn mais informações sobre outras APIs de armazenamento do Azure, siga estas ligações.</span><span class="sxs-lookup"><span data-stu-id="b92b2-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="b92b2-160">Centro de Programadores do Java</span><span class="sxs-lookup"><span data-stu-id="b92b2-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="b92b2-161">Armazenamento do Azure SDK para Java</span><span class="sxs-lookup"><span data-stu-id="b92b2-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="b92b2-162">Armazenamento do Azure SDK para Android</span><span class="sxs-lookup"><span data-stu-id="b92b2-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="b92b2-163">Referência do SDK de cliente de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="b92b2-164">API REST dos Serviços do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="b92b2-165">Blogue da Equipa de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b92b2-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="b92b2-166">Transferência de dados com o utilitário de linha de comandos do AzCopy Olá</span><span class="sxs-lookup"><span data-stu-id="b92b2-166">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)
