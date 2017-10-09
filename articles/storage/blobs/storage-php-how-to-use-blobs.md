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
# <a name="how-toouse-blob-storage-from-php"></a>Como toouse blob storage do PHP
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Descrição geral
Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs. O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação. O blob storage também é referido tooas armazenamento de objetos.

Este guia mostra como tooperform cenários comuns utilizando Olá Azure serviço blob. Exemplos de Olá são escritos no PHP e utilizam Olá [Azure SDK para PHP][download]. Olá os cenários abrangidos incluem **carregar**, **listagem**, **transferir**, e **eliminar** blobs. Para obter mais informações sobre os blobs, consulte Olá [passos](#next-steps) secção.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Criar uma aplicação PHP
Olá, só é o requisito para criar uma aplicação PHP que acede ao serviço de Blobs do Azure Olá Olá de referência de classes no Olá Azure SDK para PHP a partir de dentro do seu código. Pode utilizar qualquer toocreate de ferramentas de desenvolvimento da aplicação, incluindo o bloco de notas.

Neste guia, utilize as funcionalidades do serviço, que podem ser chamadas dentro de uma aplicação PHP localmente ou numa código em execução dentro de uma função da web do Azure, a função de trabalho ou o Web site.

## <a name="get-hello-azure-client-libraries"></a>Obter Olá bibliotecas de cliente do Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>Configurar o serviço do blob tooaccess Olá sua aplicação
toouse Olá BLOBs do Azure APIs de serviço, tem de:

1. Ficheiro de Carregador automático de Olá de referência utilizando Olá [require_once] declaração, e
2. Referência a quaisquer classes que poderá utilizar.

Olá exemplo seguinte mostra como tooinclude Olá Carregador automático de ficheiros e referência Olá **ServicesBuilder** classe.

> [!NOTE]
> Exemplos de Olá neste artigo partem do princípio de que instalou Olá bibliotecas de cliente do PHP do Azure através do compositor. Se instalou manualmente bibliotecas Olá, terá de tooreference Olá `WindowsAzure.php` Carregador automático ficheiros.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Nos exemplos de Olá abaixo, Olá `require_once` instrução será sempre apresentada, mas apenas Olá classes necessárias para tooexecute de exemplo de Olá são referenciadas.

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma ligação de armazenamento do Azure
tooinstantiate um cliente do serviço blob do Azure, tem de ter uma cadeia de ligação válido. formato de Olá para a cadeia de ligação de serviço de blob Olá é:

Para aceder a um serviço em direto:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Para aceder ao emulador do storage Olá:

```php
UseDevelopmentStorage=true
```

toocreate qualquer cliente de serviço do Azure, terá de toouse Olá **ServicesBuilder** classe. Pode:

* passar ligação Olá cadeia diretamente tooit ou
* utilizar Olá **CloudConfigurationManager (CCM)** toocheck externo várias origens para a cadeia de ligação de Olá:
  * Por predefinição, este inclui suporte para uma origem externa - variáveis de ambientais.
  * Pode adicionar novas origens expandindo Olá **ConnectionStringSource** classe.

Para obter exemplos Olá aqui descritos, cadeia de ligação de Olá será transmitida diretamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>Criar um contentor
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

A **BlobRestProxy** objeto permite-lhe criar um contentor do blob com Olá **createContainer** método. Ao criar um contentor, pode definir as opções no contentor de Olá, mas fazê-lo, por isso, não é necessário. (o exemplo de Olá abaixo mostra como contentor de Olá tooset acesso (ACL) de lista de controlo e de metadados do contentor.)

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

Chamar **setPublicAccess (PublicAccessType::CONTAINER\_e\_BLOBS)** torna Olá contentor e BLOBs de dados acessíveis via pedidos anónimos. Chamar **setPublicAccess(PublicAccessType::BLOBS_ONLY)** faz com que apenas acessíveis através de pedidos anónimos de dados de Blobs. Para mais informações sobre as ACLs do contentor, consulte [conjunto contentor ACL (REST API)][container-acl].

Para obter mais informações sobre códigos de erro do serviço Blob, consulte [códigos de erro do serviço Blob][error-codes].

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob para um contentor
tooupload um ficheiro como um blob, utilize Olá **BlobRestProxy -> createBlockBlob** método. Esta operação cria blob Olá se não existir ou substitui-lo se existir. Olá exemplo de código abaixo parte do princípio que contentor Olá já foi criado e utiliza [fopen] [ fopen] ficheiro de Olá tooopen como uma transmissão em fluxo.

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

Tenha em atenção que Olá anterior exemplo carrega um blob como uma transmissão em fluxo. No entanto, também pode ser carregado um blob como uma cadeia a utilizar, por exemplo, Olá [ficheiro\_obter\_conteúdo] [ file_get_contents] função. toodo este utilizando o exemplo anterior Olá, alterar `$content = fopen("c:\myfile.txt", "r");` demasiado`$content = file_get_contents("c:\myfile.txt");`.

## <a name="list-hello-blobs-in-a-container"></a>Lista Olá blobs num contentor
os blobs de Olá toolist num contentor, utilize Olá **BlobRestProxy -> listBlobs** método com um **foreach** cíclicas tooloop através de um resultado Olá. Olá código seguinte mostra nome Olá de cada blob como saída num contentor e respetivo browser de toohello URI.

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

## <a name="download-a-blob"></a>Transferir um blob
toodownload um blob, chamada Olá **BlobRestProxy -> getBlob** método, em seguida, chamada Olá **getContentStream** método no Olá resultante **GetBlobResult** objeto.

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

Tenha em atenção que exemplo Olá acima obtém um blob como um recurso de fluxo (comportamento predefinido de Olá). No entanto, pode utilizar Olá [fluxo\_obter\_conteúdo] [ stream-get-contents] Olá tooconvert de função devolveu a cadeia de tooa de fluxo.

## <a name="delete-a-blob"></a>Eliminar um blob
toodelete um blob, transmitir o nome de contentor Olá e nome do blob demasiado**BlobRestProxy -> deleteBlob**.

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

## <a name="delete-a-blob-container"></a>Eliminar um contentor do blob
Por fim, toodelete um contentor de blob, transmitir o nome de contentor Olá demasiado**BlobRestProxy -> deleteContainer**.

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

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá de Olá serviço blob do Azure, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.

* Visite Olá [blogue da equipa do Storage do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Consulte Olá [exemplo de blob de bloco PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).
* Consulte Olá [exemplo de blob de página do PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).
* [Transferência de dados com o utilitário de linha de comandos do AzCopy Olá](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

Para obter mais informações, consulte também Olá [Centro para programadores do PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
