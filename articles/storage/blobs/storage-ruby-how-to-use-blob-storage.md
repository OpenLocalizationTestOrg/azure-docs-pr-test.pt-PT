---
title: aaaHow toouse (armazenamento de objeto) do Blob storage do Ruby | Microsoft Docs
description: "Armazene dados não estruturados na nuvem de Olá Blob Storage do Azure (armazenamento de objetos)."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a>Como toouse Blob storage do Ruby
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Descrição geral
Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs. O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação. O blob storage também é referido tooas armazenamento de objetos.

Este guia irá mostrar como tooperform cenários comuns utilizando o Blob storage. Exemplos de Olá são escritos utilizando Olá Ruby API. Olá os cenários abrangidos incluem **carregar, listar, transferir,** e **eliminar** blobs.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Criar uma aplicação Ruby
Crie uma aplicação Ruby. Para obter instruções, consulte [Ruby na aplicação Rails Web numa VM do Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)

## <a name="configure-your-application-tooaccess-storage"></a>Configurar o armazenamento de tooaccess de aplicação
toouse Storage do Azure, terá de toodownload e utilize Olá Ruby pacote do azure, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utilize o pacote de Olá RubyGems tooobtain
1. Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix).
2. Escreva "gem instalar azure" gem do Olá comando janela tooinstall Olá e as dependências.

### <a name="import-hello-package"></a>Importar o pacote de Olá
Utilizar o editor de texto favorito, adicione Olá toohello superior de Olá Ruby ficheiro onde pretende toouse armazenamento os seguintes:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma ligação de armazenamento do Azure
módulo Olá do azure será lida a variáveis de ambiente de Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_ACCESS_KEY** para as informações necessárias tooconnect tooyour conta de armazenamento Azure. Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações de conta de Olá antes de utilizar **Azure::Blob::BlobService** com Olá seguinte código:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain estes valores de um clássico ou do armazenamento do Resource Manager conta no Olá portal do Azure:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Navegue toohello conta de armazenamento que pretende toouse.
3. No painel de definições de Olá no Olá direito, clique em **chaves de acesso**.
4. Olá acesso painel chaves que aparece, verá a chave de acesso de Olá 1 e 2 a chave de acesso. Pode utilizar qualquer um destes.
5. Clique em Olá cópia ícone toocopy Olá toohello chave da área de transferência.

## <a name="create-a-container"></a>Criar um contentor
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Olá **Azure::Blob::BlobService** objeto permite-lhe trabalhar com blobs e contentores. toocreate um contentor, utilize Olá **criar\_container()** método.

Olá exemplo de código seguinte cria um contentor ou imprime erro Olá, se existir alguma.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Se pretender que os ficheiros de Olá toomake no contentor de Olá públicas, pode definir permissões do contentor de Olá.

Apenas pode modificar Olá <strong>criar\_container()</strong> chamada toopass Olá **: pública\_acesso\_nível** opção:

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

Os valores válidos para Olá **: pública\_acesso\_nível** opção são:

* **blob:** Especifica público acesso de leitura de blobs. Dados de BLOBs dentro deste contentor podem ser lidos através do pedido anónimo, mas não estão disponíveis dados de contentor. Os clientes não é possível enumerar os blobs no contentor de Olá através do pedido anónimo.
* **contentor:** Especifica completa público acesso de leitura de dados de blob e o contentor. Os clientes podem enumerar os blobs no contentor de Olá através do pedido anónimo, mas não é possível enumerar os contentores na conta do storage Olá.

Em alternativa, pode modificar o nível de acesso público Olá de um contentor utilizando **definir\_contentor\_acl()** ao nível do método toospecify Olá acesso público.

Olá seguinte exemplo de código alterações Olá nível de acesso público demasiado**contentor**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob para um contentor
blob de conteúdo tooa tooupload, utilize Olá **criar\_bloco\_blob()** blob do método toocreate Olá, utilize um ficheiro ou de cadeia como o conteúdo de blob Olá Olá.

Olá seguinte código carrega o ficheiro de Olá **test.png** como um novo blob com o nome "-blob de imagem" no contentor de Olá.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>Lista Olá blobs num contentor
utilizar contentores de Olá toolist **list_containers()** método.
Utilize blobs de Olá toolist num contentor, **lista\_blobs()** método.

Isto produz Olá urls de todos os blobs Olá em todos os contentores de Olá para a conta de Olá.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Transferir blobs
toodownload blobs, utilize Olá **obter\_blob()** conteúdo do método tooretrieve Olá.

Olá exemplo de código seguinte demonstra utilizando **obter\_blob()** toodownload Olá conteúdo de "-blob de imagem" e escrevem-tooa de ficheiros local.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>Eliminar um Blob
Por fim, toodelete um blob, utilize Olá **eliminar\_blob()** método. Olá exemplo de código seguinte demonstra como toodelete um blob.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>Passos seguintes
toolearn sobre as tarefas de armazenamento mais complexas, siga estas ligações:

* [Blogue da Equipa de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Azure SDK para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repositório no GitHub
* [Transferência de dados com o utilitário de linha de comandos do AzCopy Olá](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

