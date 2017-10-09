---
title: aaaHow toouse Azure Table Storage do Ruby | Microsoft Docs
description: "Armazene dados estruturados na nuvem de Olá utilizando o Table storage do Azure, um arquivo de dados NoSQL."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="87684-103">Como toouse Azure Table Storage do Ruby</span><span class="sxs-lookup"><span data-stu-id="87684-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="87684-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="87684-104">Overview</span></span>
<span data-ttu-id="87684-105">Este guia mostra como tooperform cenários comuns utilizando Olá o serviço de Azure Table.</span><span class="sxs-lookup"><span data-stu-id="87684-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="87684-106">Exemplos de Olá são escritos utilizando Olá Ruby API.</span><span class="sxs-lookup"><span data-stu-id="87684-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="87684-107">Olá os cenários abrangidos incluem **criar e eliminar uma tabela, a inserir e consultar entidades numa tabela**.</span><span class="sxs-lookup"><span data-stu-id="87684-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="87684-108">Criar uma aplicação Ruby</span><span class="sxs-lookup"><span data-stu-id="87684-108">Create a Ruby application</span></span>
<span data-ttu-id="87684-109">Para obter instruções sobre como toocreate uma aplicação Ruby, consulte [Ruby na aplicação Rails Web numa VM do Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="87684-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="87684-110">Configurar o armazenamento de tooaccess de aplicação</span><span class="sxs-lookup"><span data-stu-id="87684-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="87684-111">toouse Storage do Azure, terá de toodownload e utilize Olá Ruby pacote do azure que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de armazenamento REST Olá.</span><span class="sxs-lookup"><span data-stu-id="87684-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="87684-112">Utilize o pacote de Olá RubyGems tooobtain</span><span class="sxs-lookup"><span data-stu-id="87684-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="87684-113">Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="87684-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="87684-114">Tipo **azure de instalação gem** gem do Olá comando janela tooinstall Olá e dependências.</span><span class="sxs-lookup"><span data-stu-id="87684-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="87684-115">Importar o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="87684-115">Import hello package</span></span>
<span data-ttu-id="87684-116">Utilize o editor de texto favorito, adicione Olá toohello superior de Olá Ruby ficheiro onde pretende toouse armazenamento os seguintes:</span><span class="sxs-lookup"><span data-stu-id="87684-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="87684-117">Configurar uma ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="87684-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="87684-118">Olá módulo do azure será lida a variáveis de ambiente de Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_acesso\_chave**para obter informações de conta de armazenamento do Azure tooconnect tooyour necessário.</span><span class="sxs-lookup"><span data-stu-id="87684-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="87684-119">Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações de conta de Olá antes de utilizar **Azure::TableService** com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="87684-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="87684-120">tooobtain estes valores de um clássico ou do armazenamento do Resource Manager conta no Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="87684-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="87684-121">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87684-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="87684-122">Navegue toohello conta de armazenamento que pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="87684-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="87684-123">No painel de definições de Olá no Olá direito, clique em **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="87684-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="87684-124">Olá acesso painel chaves que aparece, verá a chave de acesso de Olá 1 e 2 a chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="87684-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="87684-125">Pode utilizar qualquer um destes.</span><span class="sxs-lookup"><span data-stu-id="87684-125">You can use either of these.</span></span>
5. <span data-ttu-id="87684-126">Clique em Olá cópia ícone toocopy Olá toohello chave da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="87684-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="87684-127">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="87684-127">Create a table</span></span>
<span data-ttu-id="87684-128">Olá **Azure::TableService** objeto permite-lhe trabalhar com tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="87684-128">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="87684-129">toocreate uma tabela, utilize Olá **criar\_table()** método.</span><span class="sxs-lookup"><span data-stu-id="87684-129">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="87684-130">Olá exemplo seguinte cria uma tabela ou impressões Olá erro se existir alguma.</span><span class="sxs-lookup"><span data-stu-id="87684-130">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="87684-131">Adicionar uma tabela de tooa entidade</span><span class="sxs-lookup"><span data-stu-id="87684-131">Add an entity tooa table</span></span>
<span data-ttu-id="87684-132">tooadd uma entidade, primeiro crie um objeto de hash, que define as propriedades de entidade.</span><span class="sxs-lookup"><span data-stu-id="87684-132">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="87684-133">Tenha em atenção que para cada entidade tem de especificar um **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="87684-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="87684-134">Estas são Olá identificadores exclusivos da sua entidades e são valores que podem ser consultados muito mais rapidamente do que as outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="87684-134">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="87684-135">Storage do Azure utiliza **PartitionKey** tooautomatically distribuir entidades da tabela de Olá através de vários nós de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="87684-135">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="87684-136">Entidades com Olá mesmo **PartitionKey** são armazenadas no Olá mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="87684-136">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="87684-137">Olá **RowKey** é Olá da entidade de Olá dentro de partição Olá pertence a um ID exclusivo.</span><span class="sxs-lookup"><span data-stu-id="87684-137">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="87684-138">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="87684-138">Update an entity</span></span>
<span data-ttu-id="87684-139">Existem vários métodos tooupdate de disponível uma entidade existente:</span><span class="sxs-lookup"><span data-stu-id="87684-139">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="87684-140">**Atualizar\_entity():** atualizar uma entidade existente, substituindo-lo.</span><span class="sxs-lookup"><span data-stu-id="87684-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="87684-141">**intercalação\_entity():** atualiza uma entidade existente, a intercalação novos valores de propriedade na entidade existente Olá.</span><span class="sxs-lookup"><span data-stu-id="87684-141">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="87684-142">**Inserir\_ou\_intercalação\_entity():** atualiza uma entidade existente, substituindo-lo.</span><span class="sxs-lookup"><span data-stu-id="87684-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="87684-143">Se nenhuma entidade de existir, será inserido um novo:</span><span class="sxs-lookup"><span data-stu-id="87684-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="87684-144">**Inserir\_ou\_substituir\_entity():** atualiza uma entidade existente, a intercalação novos valores de propriedade na entidade existente Olá.</span><span class="sxs-lookup"><span data-stu-id="87684-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="87684-145">Se nenhuma entidade de existir, será inserido um novo.</span><span class="sxs-lookup"><span data-stu-id="87684-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="87684-146">Olá exemplo seguinte demonstra a atualizar uma entidade utilizando **atualizar\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="87684-146">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="87684-147">Com **atualizar\_entity()** e **intercalação\_entity()**, se a entidade de Olá que estão a atualizar não existir, a operação de atualização de Olá irá falhar.</span><span class="sxs-lookup"><span data-stu-id="87684-147">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="87684-148">Por conseguinte, se desejar toostore uma entidade, independentemente de já existir, deve em vez disso, utilizar **inserir\_ou\_substituir\_entity()** ou **inserir\_ou \_intercalação\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="87684-148">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="87684-149">Trabalhar com grupos de entidades</span><span class="sxs-lookup"><span data-stu-id="87684-149">Work with groups of entities</span></span>
<span data-ttu-id="87684-150">Por vezes, faz sentido toosubmit várias operações em conjunto no tooensure batch atomic processados pelo servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="87684-150">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="87684-151">tooaccomplish que, primeiro crie um **Batch** de objeto e, em seguida, utilizar Olá **executar\_batch()** método no **TableService**.</span><span class="sxs-lookup"><span data-stu-id="87684-151">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="87684-152">Olá exemplo seguinte demonstra submeter duas entidades com RowKey 2 e 3 num batch.</span><span class="sxs-lookup"><span data-stu-id="87684-152">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="87684-153">Tenha em atenção que só funciona para entidades com Olá PartitionKey mesmo.</span><span class="sxs-lookup"><span data-stu-id="87684-153">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="87684-154">Consulta de uma entidade</span><span class="sxs-lookup"><span data-stu-id="87684-154">Query for an entity</span></span>
<span data-ttu-id="87684-155">tooquery uma entidade numa tabela, utilize Olá **obter\_entity()** método, transferindo o nome da tabela Olá, **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="87684-155">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="87684-156">Consulta de um conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="87684-156">Query a set of entities</span></span>
<span data-ttu-id="87684-157">tooquery um conjunto de entidades numa tabela, crie um objeto de hash de consulta e utilize Olá **consulta\_entities()** método.</span><span class="sxs-lookup"><span data-stu-id="87684-157">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="87684-158">Olá exemplo seguinte demonstra obter todas as entidades de Olá com Olá mesmo **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="87684-158">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="87684-159">Se o conjunto de resultados de Olá é demasiado grande para uma única consulta tooreturn, um token de continuação será devolvido que pode utilizar as páginas subsequentes tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="87684-159">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="87684-160">Consultar um subconjunto de propriedades de entidade</span><span class="sxs-lookup"><span data-stu-id="87684-160">Query a subset of entity properties</span></span>
<span data-ttu-id="87684-161">Uma tabela de tooa de consulta pode obter apenas algumas propriedades de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="87684-161">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="87684-162">Esta técnica, denominada "projeção", reduz a largura de banda e pode melhorar o desempenho de consulta, especialmente para entidades grandes.</span><span class="sxs-lookup"><span data-stu-id="87684-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="87684-163">Cláusula de seleção de Olá de utilização e os nomes de Olá de passagem de Olá propriedades gostaria toobring através de toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="87684-163">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="87684-164">Eliminar uma entidade</span><span class="sxs-lookup"><span data-stu-id="87684-164">Delete an entity</span></span>
<span data-ttu-id="87684-165">toodelete uma entidade, utilize Olá **eliminar\_entity()** método.</span><span class="sxs-lookup"><span data-stu-id="87684-165">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="87684-166">É necessário toopass no nome de Olá da tabela de Olá que contém a entidade de Olá, Olá PartitionKey e RowKey da entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="87684-166">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="87684-167">Eliminar uma tabela</span><span class="sxs-lookup"><span data-stu-id="87684-167">Delete a table</span></span>
<span data-ttu-id="87684-168">toodelete uma tabela, utilize Olá **eliminar\_table()** método e passar no nome de Olá da Olá pretende toodelete de tabela.</span><span class="sxs-lookup"><span data-stu-id="87684-168">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="87684-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="87684-169">Next steps</span></span>

* <span data-ttu-id="87684-170">[Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="87684-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="87684-171">[Azure SDK para Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repositório no GitHub</span><span class="sxs-lookup"><span data-stu-id="87684-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

