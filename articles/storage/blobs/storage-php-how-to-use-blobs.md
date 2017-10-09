---
title: aaaHow toouse blob storage (armazenamento de objeto) do PHP | Microsoft Docs
description: "Armazene dados não estruturados na nuvem de Olá Blob Storage do Azure (armazenamento de objetos)."
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 2e77415519b38007652e3ea372da531b3a97c5d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="913c5-103">Como toouse blob storage do PHP</span><span class="sxs-lookup"><span data-stu-id="913c5-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="913c5-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="913c5-104">Overview</span></span>
<span data-ttu-id="913c5-105">Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="913c5-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="913c5-106">O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação.</span><span class="sxs-lookup"><span data-stu-id="913c5-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="913c5-107">O blob storage também é referido tooas armazenamento de objetos.</span><span class="sxs-lookup"><span data-stu-id="913c5-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="913c5-108">Este guia mostra como tooperform cenários comuns utilizando Olá Azure serviço blob.</span><span class="sxs-lookup"><span data-stu-id="913c5-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="913c5-109">Exemplos de Olá são escritos no PHP e utilizam Olá [Azure SDK para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="913c5-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="913c5-110">Olá os cenários abrangidos incluem **carregar**, **listagem**, **transferir**, e **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="913c5-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="913c5-111">Para obter mais informações sobre os blobs, consulte Olá [passos](#next-steps) secção.</span><span class="sxs-lookup"><span data-stu-id="913c5-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="913c5-112">Criar uma aplicação PHP</span><span class="sxs-lookup"><span data-stu-id="913c5-112">Create a PHP application</span></span>
<span data-ttu-id="913c5-113">Olá, só é o requisito para criar uma aplicação PHP que acede ao serviço de Blobs do Azure Olá Olá de referência de classes no Olá Azure SDK para PHP a partir de dentro do seu código.</span><span class="sxs-lookup"><span data-stu-id="913c5-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="913c5-114">Pode utilizar qualquer toocreate de ferramentas de desenvolvimento da aplicação, incluindo o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="913c5-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="913c5-115">Neste guia, utilize as funcionalidades do serviço, que podem ser chamadas dentro de uma aplicação PHP localmente ou numa código em execução dentro de uma função da web do Azure, a função de trabalho ou o Web site.</span><span class="sxs-lookup"><span data-stu-id="913c5-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="913c5-116">Obter Olá bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="913c5-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="913c5-117">Configurar o serviço do blob tooaccess Olá sua aplicação</span><span class="sxs-lookup"><span data-stu-id="913c5-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="913c5-118">toouse Olá BLOBs do Azure APIs de serviço, tem de:</span><span class="sxs-lookup"><span data-stu-id="913c5-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="913c5-119">Ficheiro de Carregador automático de Olá de referência utilizando Olá [require_once] declaração, e</span><span class="sxs-lookup"><span data-stu-id="913c5-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="913c5-120">Referência a quaisquer classes que poderá utilizar.</span><span class="sxs-lookup"><span data-stu-id="913c5-120">Reference any classes you might use.</span></span>

<span data-ttu-id="913c5-121">Olá exemplo seguinte mostra como tooinclude Olá Carregador automático de ficheiros e referência Olá **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="913c5-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="913c5-122">Exemplos de Olá neste artigo partem do princípio de que instalou Olá bibliotecas de cliente do PHP do Azure através do compositor.</span><span class="sxs-lookup"><span data-stu-id="913c5-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="913c5-123">Se instalou manualmente bibliotecas Olá, terá de tooreference Olá `WindowsAzure.php` Carregador automático ficheiros.</span><span class="sxs-lookup"><span data-stu-id="913c5-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="913c5-124">Nos exemplos de Olá abaixo, Olá `require_once` instrução será sempre apresentada, mas apenas Olá classes necessárias para tooexecute de exemplo de Olá são referenciadas.</span><span class="sxs-lookup"><span data-stu-id="913c5-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="913c5-125">Configurar uma ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="913c5-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="913c5-126">tooinstantiate um cliente do serviço blob do Azure, tem de ter uma cadeia de ligação válido.</span><span class="sxs-lookup"><span data-stu-id="913c5-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="913c5-127">formato de Olá para a cadeia de ligação de serviço de blob Olá é:</span><span class="sxs-lookup"><span data-stu-id="913c5-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="913c5-128">Para aceder a um serviço em direto:</span><span class="sxs-lookup"><span data-stu-id="913c5-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="913c5-129">Para aceder ao emulador do storage Olá:</span><span class="sxs-lookup"><span data-stu-id="913c5-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="913c5-130">toocreate qualquer cliente de serviço do Azure, terá de toouse Olá **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="913c5-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="913c5-131">Pode:</span><span class="sxs-lookup"><span data-stu-id="913c5-131">You can:</span></span>

* <span data-ttu-id="913c5-132">passar ligação Olá cadeia diretamente tooit ou</span><span class="sxs-lookup"><span data-stu-id="913c5-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="913c5-133">utilizar Olá **CloudConfigurationManager (CCM)** toocheck externo várias origens para a cadeia de ligação de Olá:</span><span class="sxs-lookup"><span data-stu-id="913c5-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="913c5-134">Por predefinição, este inclui suporte para uma origem externa - variáveis de ambientais.</span><span class="sxs-lookup"><span data-stu-id="913c5-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="913c5-135">Pode adicionar novas origens expandindo Olá **ConnectionStringSource** classe.</span><span class="sxs-lookup"><span data-stu-id="913c5-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="913c5-136">Para obter exemplos Olá aqui descritos, cadeia de ligação de Olá será transmitida diretamente.</span><span class="sxs-lookup"><span data-stu-id="913c5-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="913c5-137">Criar um contentor</span><span class="sxs-lookup"><span data-stu-id="913c5-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="913c5-138">A **BlobRestProxy** objeto permite-lhe criar um contentor do blob com Olá **createContainer** método.</span><span class="sxs-lookup"><span data-stu-id="913c5-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="913c5-139">Ao criar um contentor, pode definir as opções no contentor de Olá, mas fazê-lo, por isso, não é necessário.</span><span class="sxs-lookup"><span data-stu-id="913c5-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="913c5-140">(o exemplo de Olá abaixo mostra como contentor de Olá tooset acesso (ACL) de lista de controlo e de metadados do contentor.)</span><span class="sxs-lookup"><span data-stu-id="913c5-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="913c5-141">Chamar **setPublicAccess (PublicAccessType::CONTAINER\_e\_BLOBS)** torna Olá contentor e BLOBs de dados acessíveis via pedidos anónimos.</span><span class="sxs-lookup"><span data-stu-id="913c5-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="913c5-142">Chamar **setPublicAccess(PublicAccessType::BLOBS_ONLY)** faz com que apenas acessíveis através de pedidos anónimos de dados de Blobs.</span><span class="sxs-lookup"><span data-stu-id="913c5-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="913c5-143">Para mais informações sobre as ACLs do contentor, consulte [conjunto contentor ACL (REST API)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="913c5-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="913c5-144">Para obter mais informações sobre códigos de erro do serviço Blob, consulte [códigos de erro do serviço Blob][error-codes].</span><span class="sxs-lookup"><span data-stu-id="913c5-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="913c5-145">Carregar um blob para um contentor</span><span class="sxs-lookup"><span data-stu-id="913c5-145">Upload a blob into a container</span></span>
<span data-ttu-id="913c5-146">tooupload um ficheiro como um blob, utilize Olá **BlobRestProxy -> createBlockBlob** método.</span><span class="sxs-lookup"><span data-stu-id="913c5-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="913c5-147">Esta operação cria blob Olá se não existir ou substitui-lo se existir.</span><span class="sxs-lookup"><span data-stu-id="913c5-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="913c5-148">Olá exemplo de código abaixo parte do princípio que contentor Olá já foi criado e utiliza [fopen] [ fopen] ficheiro de Olá tooopen como uma transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="913c5-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="913c5-149">Tenha em atenção que Olá anterior exemplo carrega um blob como uma transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="913c5-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="913c5-150">No entanto, também pode ser carregado um blob como uma cadeia a utilizar, por exemplo, Olá [ficheiro\_obter\_conteúdo] [ file_get_contents] função.</span><span class="sxs-lookup"><span data-stu-id="913c5-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="913c5-151">toodo este utilizando o exemplo anterior Olá, alterar `$content = fopen("c:\myfile.txt", "r");` demasiado`$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="913c5-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="913c5-152">Lista Olá blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="913c5-152">List hello blobs in a container</span></span>
<span data-ttu-id="913c5-153">os blobs de Olá toolist num contentor, utilize Olá **BlobRestProxy -> listBlobs** método com um **foreach** cíclicas tooloop através de um resultado Olá.</span><span class="sxs-lookup"><span data-stu-id="913c5-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="913c5-154">Olá código seguinte mostra nome Olá de cada blob como saída num contentor e respetivo browser de toohello URI.</span><span class="sxs-lookup"><span data-stu-id="913c5-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a><span data-ttu-id="913c5-155">Transferir um blob</span><span class="sxs-lookup"><span data-stu-id="913c5-155">Download a blob</span></span>
<span data-ttu-id="913c5-156">toodownload um blob, chamada Olá **BlobRestProxy -> getBlob** método, em seguida, chamada Olá **getContentStream** método no Olá resultante **GetBlobResult** objeto.</span><span class="sxs-lookup"><span data-stu-id="913c5-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="913c5-157">Tenha em atenção que exemplo Olá acima obtém um blob como um recurso de fluxo (comportamento predefinido de Olá).</span><span class="sxs-lookup"><span data-stu-id="913c5-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="913c5-158">No entanto, pode utilizar Olá [fluxo\_obter\_conteúdo] [ stream-get-contents] Olá tooconvert de função devolveu a cadeia de tooa de fluxo.</span><span class="sxs-lookup"><span data-stu-id="913c5-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="913c5-159">Eliminar um blob</span><span class="sxs-lookup"><span data-stu-id="913c5-159">Delete a blob</span></span>
<span data-ttu-id="913c5-160">toodelete um blob, transmitir o nome de contentor Olá e nome do blob demasiado**BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="913c5-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="913c5-161">Eliminar um contentor do blob</span><span class="sxs-lookup"><span data-stu-id="913c5-161">Delete a blob container</span></span>
<span data-ttu-id="913c5-162">Por fim, toodelete um contentor de blob, transmitir o nome de contentor Olá demasiado**BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="913c5-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="913c5-163">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="913c5-163">Next steps</span></span>
<span data-ttu-id="913c5-164">Agora que aprendeu as noções básicas de Olá de Olá serviço blob do Azure, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="913c5-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="913c5-165">Visite Olá [blogue da equipa do Storage do Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="913c5-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="913c5-166">Consulte Olá [exemplo de blob de bloco PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="913c5-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="913c5-167">Consulte Olá [exemplo de blob de página do PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="913c5-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="913c5-168">Transferência de dados com o utilitário de linha de comandos do AzCopy Olá</span><span class="sxs-lookup"><span data-stu-id="913c5-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="913c5-169">Para obter mais informações, consulte também Olá [Centro para programadores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="913c5-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
