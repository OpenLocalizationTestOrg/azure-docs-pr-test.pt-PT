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
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="3fb17-103">Como toouse Blob storage do Ruby</span><span class="sxs-lookup"><span data-stu-id="3fb17-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="3fb17-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="3fb17-104">Overview</span></span>
<span data-ttu-id="3fb17-105">Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="3fb17-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="3fb17-106">O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação.</span><span class="sxs-lookup"><span data-stu-id="3fb17-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="3fb17-107">O blob storage também é referido tooas armazenamento de objetos.</span><span class="sxs-lookup"><span data-stu-id="3fb17-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="3fb17-108">Este guia irá mostrar como tooperform cenários comuns utilizando o Blob storage.</span><span class="sxs-lookup"><span data-stu-id="3fb17-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="3fb17-109">Exemplos de Olá são escritos utilizando Olá Ruby API.</span><span class="sxs-lookup"><span data-stu-id="3fb17-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="3fb17-110">Olá os cenários abrangidos incluem **carregar, listar, transferir,** e **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="3fb17-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="3fb17-111">Criar uma aplicação Ruby</span><span class="sxs-lookup"><span data-stu-id="3fb17-111">Create a Ruby application</span></span>
<span data-ttu-id="3fb17-112">Crie uma aplicação Ruby.</span><span class="sxs-lookup"><span data-stu-id="3fb17-112">Create a Ruby application.</span></span> <span data-ttu-id="3fb17-113">Para obter instruções, consulte [Ruby na aplicação Rails Web numa VM do Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="3fb17-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="3fb17-114">Configurar o armazenamento de tooaccess de aplicação</span><span class="sxs-lookup"><span data-stu-id="3fb17-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="3fb17-115">toouse Storage do Azure, terá de toodownload e utilize Olá Ruby pacote do azure, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="3fb17-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="3fb17-116">Utilize o pacote de Olá RubyGems tooobtain</span><span class="sxs-lookup"><span data-stu-id="3fb17-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="3fb17-117">Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="3fb17-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="3fb17-118">Escreva "gem instalar azure" gem do Olá comando janela tooinstall Olá e as dependências.</span><span class="sxs-lookup"><span data-stu-id="3fb17-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="3fb17-119">Importar o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="3fb17-119">Import hello package</span></span>
<span data-ttu-id="3fb17-120">Utilizar o editor de texto favorito, adicione Olá toohello superior de Olá Ruby ficheiro onde pretende toouse armazenamento os seguintes:</span><span class="sxs-lookup"><span data-stu-id="3fb17-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="3fb17-121">Configurar uma ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3fb17-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="3fb17-122">módulo Olá do azure será lida a variáveis de ambiente de Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_ACCESS_KEY** para as informações necessárias tooconnect tooyour conta de armazenamento Azure.</span><span class="sxs-lookup"><span data-stu-id="3fb17-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="3fb17-123">Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações de conta de Olá antes de utilizar **Azure::Blob::BlobService** com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="3fb17-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="3fb17-124">tooobtain estes valores de um clássico ou do armazenamento do Resource Manager conta no Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="3fb17-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="3fb17-125">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3fb17-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3fb17-126">Navegue toohello conta de armazenamento que pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="3fb17-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="3fb17-127">No painel de definições de Olá no Olá direito, clique em **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="3fb17-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="3fb17-128">Olá acesso painel chaves que aparece, verá a chave de acesso de Olá 1 e 2 a chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="3fb17-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="3fb17-129">Pode utilizar qualquer um destes.</span><span class="sxs-lookup"><span data-stu-id="3fb17-129">You can use either of these.</span></span>
5. <span data-ttu-id="3fb17-130">Clique em Olá cópia ícone toocopy Olá toohello chave da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="3fb17-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="3fb17-131">Criar um contentor</span><span class="sxs-lookup"><span data-stu-id="3fb17-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="3fb17-132">Olá **Azure::Blob::BlobService** objeto permite-lhe trabalhar com blobs e contentores.</span><span class="sxs-lookup"><span data-stu-id="3fb17-132">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="3fb17-133">toocreate um contentor, utilize Olá **criar\_container()** método.</span><span class="sxs-lookup"><span data-stu-id="3fb17-133">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="3fb17-134">Olá exemplo de código seguinte cria um contentor ou imprime erro Olá, se existir alguma.</span><span class="sxs-lookup"><span data-stu-id="3fb17-134">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="3fb17-135">Se pretender que os ficheiros de Olá toomake no contentor de Olá públicas, pode definir permissões do contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="3fb17-135">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="3fb17-136">Apenas pode modificar Olá <strong>criar\_container()</strong> chamada toopass Olá **: pública\_acesso\_nível** opção:</span><span class="sxs-lookup"><span data-stu-id="3fb17-136">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="3fb17-137">Os valores válidos para Olá **: pública\_acesso\_nível** opção são:</span><span class="sxs-lookup"><span data-stu-id="3fb17-137">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="3fb17-138">**blob:** Especifica público acesso de leitura de blobs.</span><span class="sxs-lookup"><span data-stu-id="3fb17-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="3fb17-139">Dados de BLOBs dentro deste contentor podem ser lidos através do pedido anónimo, mas não estão disponíveis dados de contentor.</span><span class="sxs-lookup"><span data-stu-id="3fb17-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="3fb17-140">Os clientes não é possível enumerar os blobs no contentor de Olá através do pedido anónimo.</span><span class="sxs-lookup"><span data-stu-id="3fb17-140">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="3fb17-141">**contentor:** Especifica completa público acesso de leitura de dados de blob e o contentor.</span><span class="sxs-lookup"><span data-stu-id="3fb17-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="3fb17-142">Os clientes podem enumerar os blobs no contentor de Olá através do pedido anónimo, mas não é possível enumerar os contentores na conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="3fb17-142">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="3fb17-143">Em alternativa, pode modificar o nível de acesso público Olá de um contentor utilizando **definir\_contentor\_acl()** ao nível do método toospecify Olá acesso público.</span><span class="sxs-lookup"><span data-stu-id="3fb17-143">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="3fb17-144">Olá seguinte exemplo de código alterações Olá nível de acesso público demasiado**contentor**:</span><span class="sxs-lookup"><span data-stu-id="3fb17-144">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="3fb17-145">Carregar um blob para um contentor</span><span class="sxs-lookup"><span data-stu-id="3fb17-145">Upload a blob into a container</span></span>
<span data-ttu-id="3fb17-146">blob de conteúdo tooa tooupload, utilize Olá **criar\_bloco\_blob()** blob do método toocreate Olá, utilize um ficheiro ou de cadeia como o conteúdo de blob Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="3fb17-146">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="3fb17-147">Olá seguinte código carrega o ficheiro de Olá **test.png** como um novo blob com o nome "-blob de imagem" no contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="3fb17-147">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="3fb17-148">Lista Olá blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="3fb17-148">List hello blobs in a container</span></span>
<span data-ttu-id="3fb17-149">utilizar contentores de Olá toolist **list_containers()** método.</span><span class="sxs-lookup"><span data-stu-id="3fb17-149">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="3fb17-150">Utilize blobs de Olá toolist num contentor, **lista\_blobs()** método.</span><span class="sxs-lookup"><span data-stu-id="3fb17-150">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="3fb17-151">Isto produz Olá urls de todos os blobs Olá em todos os contentores de Olá para a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="3fb17-151">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="3fb17-152">Transferir blobs</span><span class="sxs-lookup"><span data-stu-id="3fb17-152">Download blobs</span></span>
<span data-ttu-id="3fb17-153">toodownload blobs, utilize Olá **obter\_blob()** conteúdo do método tooretrieve Olá.</span><span class="sxs-lookup"><span data-stu-id="3fb17-153">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="3fb17-154">Olá exemplo de código seguinte demonstra utilizando **obter\_blob()** toodownload Olá conteúdo de "-blob de imagem" e escrevem-tooa de ficheiros local.</span><span class="sxs-lookup"><span data-stu-id="3fb17-154">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="3fb17-155">Eliminar um Blob</span><span class="sxs-lookup"><span data-stu-id="3fb17-155">Delete a Blob</span></span>
<span data-ttu-id="3fb17-156">Por fim, toodelete um blob, utilize Olá **eliminar\_blob()** método.</span><span class="sxs-lookup"><span data-stu-id="3fb17-156">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="3fb17-157">Olá exemplo de código seguinte demonstra como toodelete um blob.</span><span class="sxs-lookup"><span data-stu-id="3fb17-157">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="3fb17-158">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3fb17-158">Next steps</span></span>
<span data-ttu-id="3fb17-159">toolearn sobre as tarefas de armazenamento mais complexas, siga estas ligações:</span><span class="sxs-lookup"><span data-stu-id="3fb17-159">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="3fb17-160">Blogue da Equipa de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3fb17-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="3fb17-161">[Azure SDK para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repositório no GitHub</span><span class="sxs-lookup"><span data-stu-id="3fb17-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="3fb17-162">Transferência de dados com o utilitário de linha de comandos do AzCopy Olá</span><span class="sxs-lookup"><span data-stu-id="3fb17-162">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

