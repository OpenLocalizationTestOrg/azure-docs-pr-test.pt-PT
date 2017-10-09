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
# <a name="how-toouse-blob-storage-from-c"></a>Como toouse Blob Storage do C++
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Descrição geral
Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs. O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação. O blob storage também é referido tooas armazenamento de objetos.

Este guia demonstrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de Blobs do Azure. Exemplos de Olá são escritos em C++ e utilizar Olá [biblioteca de clientes do Storage do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Olá os cenários abrangidos incluem **carregar**, **listagem**, **transferir**, e **eliminar** blobs.  

> [!NOTE]
> Destinos neste guia Olá biblioteca de clientes do Storage do Azure para C++ versão 1.0.0 e acima. Olá recomendada de versão é biblioteca de clientes de armazenamento 2.2.0, que está disponível através de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Criar uma aplicação do C++
Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação de C++.  

toodo por isso, terá de tooinstall hello biblioteca de clientes do Storage do Azure para C++ e criar uma conta de armazenamento do Azure na sua subscrição do Azure.   

Olá tooinstall biblioteca de clientes do Storage do Azure para C++, pode utilizar Olá seguintes métodos:

* **Linux:** siga as instruções de Olá indicadas na Olá [biblioteca de clientes do Storage do Azure para o ficheiro Leia-me do C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.  
* **Windows:** no Visual Studio, clique em **ferramentas > Gestor de pacotes NuGet > consola do Gestor de pacotes**. Seguinte Olá de tipo de comando para Olá [consola do Gestor de pacotes NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e prima **ENTER**.  
  
     Pacote de instalação wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>Configurar o seu tooaccess aplicações armazenamento de BLOBs
Adicione a seguinte Olá incluem parte superior do toohello de declarações do ficheiro de C++ de olá onde pretende que os blobs storage do Azure toouse Olá APIs tooaccess:  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Configurar uma cadeia de ligação de armazenamento do Azure
Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados. Quando em execução numa aplicação de cliente, tem de fornecer cadeia de ligação de armazenamento de Olá Olá seguir o formato, utilizando o nome de Olá do seu armazenamento conta e Olá armazenamento chave de acesso da conta de armazenamento de Olá listada no Olá [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores. Para obter informações sobre as contas do storage e chaves de acesso, consulte [sobre contas de armazenamento do Azure](storage-create-storage-account.md). Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest a aplicação no seu computador local do Windows, pode utilizar Olá Microsoft Azure [emulador do storage](storage-use-emulator.md) que é instalado com Olá [Azure SDK](https://azure.microsoft.com/downloads/). emulador do storage Olá é um utilitário que simula Olá tabela, fila e Blob serviços disponíveis no Azure no seu computador de desenvolvimento local. Olá exemplo seguinte mostra como podem declarar um campo estático toohold Olá ligação cadeia tooyour local emulador do storage:

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

emulador do storage do Azure de toostart Olá, selecione Olá **iniciar** Olá botão ou prima **Windows** chave. Começa a escrever **emulador do Storage do Azure**e selecione **emulador do Storage do Microsoft Azure** da lista de Olá das aplicações.  

Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.  

## <a name="retrieve-your-connection-string"></a>Obter a cadeia de ligação
Pode utilizar Olá **cloud_storage_account** classe toorepresent informações da sua conta de armazenamento. tooretrieve informações da cadeia de ligação de armazenamento Olá de conta de armazenamento, pode utilizar Olá **analisar** método.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Em seguida, obter uma referência tooa **cloud_blob_client** como permite-lhe tooretrieve objetos que representam a contentores e blobs armazenados no Olá serviço de armazenamento de BLOBs de classe. Olá código seguinte cria um **cloud_blob_client** objeto utilizando o objeto de conta de armazenamento de Olá vamos obter acima:  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>Como: criar um contentor
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Este exemplo mostra como toocreate um contentor se já existir:  

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

Por predefinição, Olá novo contentor é privado e tem de especificar os blobs de toodownload chave de acesso de armazenamento deste contentor. Se pretender que os ficheiros de Olá toomake (blobs) dentro de Olá contentor disponíveis tooeveryone, pode definir Olá contentor toobe público utilizando Olá seguinte código:  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Qualquer pessoa na Internet de Olá pode ver os blobs num contentor público, mas pode modificar ou eliminá-los apenas se tiver a chave de acesso adequadas Olá.  

## <a name="how-to-upload-a-blob-into-a-container"></a>Como: carregar um blob para um contentor
O Blob Storage do Azure suporta blobs de blocos e blobs de páginas. Na maioria dos casos de Olá, o blob de bloco é Olá recomendado toouse de tipo.  

tooupload um blob de blocos do ficheiro tooa, obtenha uma referência de contentor e utilizá-lo tooget uma referência de blob de bloco. Depois de ter uma referência de blob, pode carregar qualquer fluxo de dados tooit ao chamar Olá **upload_from_stream** método. Esta operação irá criar blob Olá se que não exista, ou substituí-lo se existir. Olá seguinte exemplo mostra como tooupload um blob para um contentor e parte do princípio de que contentor Olá já foi criado.  

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

Em alternativa, pode utilizar Olá **upload_from_file** tooupload método um blob de bloco de tooa do ficheiro.

## <a name="how-to-list-hello-blobs-in-a-container"></a>Como: listar Olá blobs num contentor
os blobs de Olá toolist num contentor, obtenha primeiro uma referência de contentor. Em seguida, pode utilizar um contentor Olá **list_blobs** blobs do método tooretrieve Olá e/ou os diretórios dentro do mesmo. tooaccess Olá conjunto avançado de propriedades e métodos de um **list_blob_item**, tem de chamar Olá **list_blob_item.as_blob** método tooget um **cloud_blob** objeto, ou Olá **list_blob.as_directory** método tooget um objeto de cloud_blob_directory. Olá código seguinte demonstra como tooretrieve e de saída Olá URI de cada item no Olá **contentor my exemplo** contentor:

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

Para obter mais detalhes sobre operações de listagem, consulte [lista de recursos de armazenamento do Azure em C++](storage-c-plus-plus-enumeration.md).

## <a name="how-to-download-blobs"></a>Como: Transferir blobs
toodownload blobs, obtenha primeiro uma referência de blob e, em seguida, chame Olá **download_to_stream** método. Olá exemplo seguinte utiliza Olá **download_to_stream** método tootransfer Olá blob conteúdo tooa objeto de fluxo, em seguida, pode manter tooa de ficheiros local.  

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

Em alternativa, pode utilizar Olá **download_to_file** método toodownload Olá conteúdo de um blob tooa ficheiro.
Além disso, também pode utilizar Olá **download_text** método toodownload Olá conteúdo um blob como uma cadeia de texto.  

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

## <a name="how-to-delete-blobs"></a>Como: eliminar blobs
toodelete um blob, obtenha primeiro uma referência de blob e, em seguida, chame Olá **delete_blob** método.  

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

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu Olá Noções básicas do blob storage, siga estas toolearn ligações mais sobre o Storage do Azure.  

* [Como toouse armazenamento de filas do C++](storage-c-plus-plus-how-to-use-queues.md)
* [Como toouse Table Storage do C++](storage-c-plus-plus-how-to-use-tables.md)
* [Recursos de armazenamento do Azure de lista em C++](storage-c-plus-plus-enumeration.md)
* [Biblioteca de clientes do Storage para referência do C++](http://azure.github.io/azure-storage-cpp)
* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Transferência de dados com Olá utilitário de linha de comandos AzCopy](storage-use-azcopy.md)

