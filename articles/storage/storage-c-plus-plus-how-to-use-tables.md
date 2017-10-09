---
title: aaaHow toouse armazenamento de tabelas (C++) | Microsoft Docs
description: "Armazene dados estruturados na nuvem de Olá utilizando o Table storage do Azure, um arquivo de dados NoSQL."
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 8eee0031350ab6ff3f76fb288b2f896687aa17a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a><span data-ttu-id="5ecc7-103">Como toouse Table storage do C++</span><span class="sxs-lookup"><span data-stu-id="5ecc7-103">How toouse Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="5ecc7-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="5ecc7-104">Overview</span></span>
<span data-ttu-id="5ecc7-105">Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-105">This guide will show you how tooperform common scenarios by using hello Azure Table storage service.</span></span> <span data-ttu-id="5ecc7-106">Exemplos de Olá são escritos em C++ e utilizar Olá [biblioteca de clientes do Storage do Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="5ecc7-106">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="5ecc7-107">Olá os cenários abrangidos incluem **criar e eliminar uma tabela** e **trabalhar com as entidades da tabela**.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-107">hello scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="5ecc7-108">Destinos neste guia Olá biblioteca de clientes do Storage do Azure para C++ versão 1.0.0 e acima.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-108">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="5ecc7-109">Olá recomendada de versão é biblioteca de clientes de armazenamento 2.2.0, que está disponível através de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="5ecc7-109">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="5ecc7-110">Criar uma aplicação do C++</span><span class="sxs-lookup"><span data-stu-id="5ecc7-110">Create a C++ application</span></span>
<span data-ttu-id="5ecc7-111">Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação de C++.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="5ecc7-112">toodo por isso, terá de tooinstall hello biblioteca de clientes do Storage do Azure para C++ e criar uma conta de armazenamento do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-112">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="5ecc7-113">Olá tooinstall biblioteca de clientes do Storage do Azure para C++, pode utilizar Olá seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="5ecc7-113">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="5ecc7-114">**Linux:** siga as instruções de Olá fornecidas no Olá [biblioteca de clientes do Storage do Azure para o ficheiro Leia-me do C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-114">**Linux:** Follow hello instructions given on hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="5ecc7-115">**Windows:** no Visual Studio, clique em **ferramentas > Gestor de pacotes NuGet > consola do Gestor de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="5ecc7-116">Seguinte Olá de tipo de comando para Olá [consola do Gestor de pacotes NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e prima Enter.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-116">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="5ecc7-117">Pacote de instalação wastorage</span><span class="sxs-lookup"><span data-stu-id="5ecc7-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="5ecc7-118">Configurar a aplicação tooaccess o Table storage</span><span class="sxs-lookup"><span data-stu-id="5ecc7-118">Configure your application tooaccess Table storage</span></span>
<span data-ttu-id="5ecc7-119">Adicione a seguinte Olá incluem parte superior do toohello de declarações do ficheiro de C++ de olá onde pretende que as tabelas de tooaccess APIs de armazenamento do Azure Olá toouse:</span><span class="sxs-lookup"><span data-stu-id="5ecc7-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="5ecc7-120">Configurar uma cadeia de ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecc7-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="5ecc7-121">Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="5ecc7-122">Quando executar uma aplicação de cliente, tem de fornecer cadeia de ligação de armazenamento de Olá Olá seguir o formato.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-122">When running a client application, you must provide hello storage connection string in hello following format.</span></span> <span data-ttu-id="5ecc7-123">Utilize o nome de Olá do seu armazenamento conta e Olá armazenamento chave de acesso de conta de armazenamento Olá listado no Olá [Portal do Azure](https://portal.azure.com) para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-123">Use hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="5ecc7-124">Para obter informações sobre as contas do storage e chaves de acesso, consulte [contas do storage do Azure sobre](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5ecc7-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="5ecc7-125">Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:</span><span class="sxs-lookup"><span data-stu-id="5ecc7-125">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="5ecc7-126">tootest a aplicação no seu computador baseado em Windows local, pode utilizar Olá Azure [emulador do storage](storage-use-emulator.md) que é instalado com Olá [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5ecc7-126">tootest your application in your local Windows-based computer, you can use hello Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="5ecc7-127">emulador do storage Olá é um utilitário que simula Olá tabela, fila e Blob do Azure serviços disponíveis no computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-127">hello storage emulator is a utility that simulates hello Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="5ecc7-128">Olá exemplo seguinte mostra como podem declarar um campo estático toohold Olá ligação cadeia tooyour local emulador do storage:</span><span class="sxs-lookup"><span data-stu-id="5ecc7-128">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="5ecc7-129">toostart Olá emulador do storage do Azure, clique em Olá **iniciar** botão ou prima tecla de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-129">toostart hello Azure storage emulator, click hello **Start** button or press hello Windows key.</span></span> <span data-ttu-id="5ecc7-130">Começa a escrever **emulador do Storage do Azure**e, em seguida, selecione **emulador do Storage do Microsoft Azure** da lista de Olá das aplicações.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="5ecc7-131">Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-131">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="5ecc7-132">Obter a cadeia de ligação</span><span class="sxs-lookup"><span data-stu-id="5ecc7-132">Retrieve your connection string</span></span>
<span data-ttu-id="5ecc7-133">Pode utilizar Olá **cloud_storage_account** classe toorepresent as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-133">You can use hello **cloud_storage_account** class toorepresent your storage account information.</span></span> <span data-ttu-id="5ecc7-134">tooretrieve informações da cadeia de ligação de armazenamento Olá de conta de armazenamento, pode utilizar o método de análise Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-134">tooretrieve your storage account information from hello storage connection string, you can use hello parse method.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="5ecc7-135">Em seguida, obter uma referência tooa **cloud_table_client** classe, que permite-lhe obter objetos de referência para as tabelas e entidades armazenadas no Olá serviço de armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-135">Next, get a reference tooa **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within hello Table storage service.</span></span> <span data-ttu-id="5ecc7-136">Olá código seguinte cria um **cloud_table_client** objeto através da utilização de objeto de conta de armazenamento de Olá vamos obter acima:</span><span class="sxs-lookup"><span data-stu-id="5ecc7-136">hello following code creates a **cloud_table_client** object by using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="5ecc7-137">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="5ecc7-137">Create a table</span></span>
<span data-ttu-id="5ecc7-138">A **cloud_table_client** objeto permite-lhe obter objetos de referência para as tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="5ecc7-139">Olá código seguinte cria um **cloud_table_client** objeto e utiliza-toocreate uma nova tabela.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-139">hello following code creates a **cloud_table_client** object and uses it toocreate a new table.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="5ecc7-140">Adicionar uma tabela de tooa entidade</span><span class="sxs-lookup"><span data-stu-id="5ecc7-140">Add an entity tooa table</span></span>
<span data-ttu-id="5ecc7-141">tooadd uma tabela de tooa de entidade, crie um novo **table_entity** objeto e transmita-demasiado**table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-141">tooadd an entity tooa table, create a new **table_entity** object and pass it too**table_operation::insert_entity**.</span></span> <span data-ttu-id="5ecc7-142">Olá seguinte código utiliza nome próprio do cliente Olá como chave de linha de Olá e o apelido como chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-142">hello following code uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="5ecc7-143">Em conjunto, a partição de uma entidade e a chave de linha de identificar exclusivamente entidade Olá na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-143">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="5ecc7-144">As chaves de partição de entidades com Olá a mesma chave de partição pode ser consultada mais rapidamente do que aqueles com diferentes, mas utilizar várias chaves de partição permite maior escalabilidade da operação paralela.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-144">Entities with hello same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="5ecc7-145">Para obter mais informações, consulte [Microsoft Azure armazenamento desempenho e escalabilidade lista de verificação](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="5ecc7-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="5ecc7-146">Olá código seguinte cria uma nova instância do **table_entity** com algumas toobe de dados de cliente armazenado.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-146">hello following code creates a new instance of **table_entity** with some customer data toobe stored.</span></span> <span data-ttu-id="5ecc7-147">Olá código seguinte chama **table_operation::insert_entity** toocreate um **table_operation** tooinsert uma entidade de objeto para uma tabela e associa Olá nova entidade de tabela com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-147">hello code next calls **table_operation::insert_entity** toocreate a **table_operation** object tooinsert an entity into a table, and associates hello new table entity with it.</span></span> <span data-ttu-id="5ecc7-148">Por fim, Olá código chama Olá executar o método num Olá **cloud_table** objeto.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-148">Finally, hello code calls hello execute method on hello **cloud_table** object.</span></span> <span data-ttu-id="5ecc7-149">E Olá novo **table_operation** envia um pedido toohello tabela serviço tooinsert Olá nova entidade de cliente na tabela de "pessoas" Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-149">And hello new **table_operation** sends a request toohello Table service tooinsert hello new customer entity into hello "people" table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="5ecc7-150">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="5ecc7-150">Insert a batch of entities</span></span>
<span data-ttu-id="5ecc7-151">Pode inserir um lote de entidades toohello serviço tabela numa operação de escrita.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-151">You can insert a batch of entities toohello Table service in one write operation.</span></span> <span data-ttu-id="5ecc7-152">Olá código seguinte cria um **table_batch_operation** de objeto e, em seguida, adiciona três inserir tooit de operações.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-152">hello following code creates a **table_batch_operation** object, and then adds three insert operations tooit.</span></span> <span data-ttu-id="5ecc7-153">Cada operação de inserção é adicionada ao criar um novo objeto de entidade, os respetivos valores, a definição e, em seguida, ao chamar Olá inserir método no Olá **table_batch_operation** operação de inserção de entidade de Olá tooassociate objeto com um novo.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-153">Each insert operation is added by creating a new entity object, setting its values, and then calling hello insert method on hello **table_batch_operation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="5ecc7-154">Em seguida, **cloud_table.execute** é designado por operação de Olá tooexecute.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-154">Then, **cloud_table.execute** is called tooexecute hello operation.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="5ecc7-155">Toonote algumas coisas nas operações de lote:</span><span class="sxs-lookup"><span data-stu-id="5ecc7-155">Some things toonote on batch operations:</span></span>  

* <span data-ttu-id="5ecc7-156">Pode efetuar cópias de segurança too100 insert, eliminar, intercalação, substituir, as operações de inserção ou intercalação e inserir ou substituir em qualquer combinação num batch único.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-156">You can perform up too100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="5ecc7-157">Uma operação em lote pode ter uma operação de obter, se esta é uma operação em lote de Olá apenas Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-157">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>  
* <span data-ttu-id="5ecc7-158">Todas as entidades numa operação batch único tem de ter Olá mesma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-158">All entities in a single batch operation must have hello same partition key.</span></span>  
* <span data-ttu-id="5ecc7-159">Uma operação em lote é limitado tooa payload de dados de 4 MB.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-159">A batch operation is limited tooa 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="5ecc7-160">Obter todas as entidades numa partição</span><span class="sxs-lookup"><span data-stu-id="5ecc7-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="5ecc7-161">tooquery uma tabela para todas as entidades numa partição, utilize um **table_query** objeto.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-161">tooquery a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="5ecc7-162">Olá exemplo de código seguinte especifica um filtro para entidades em que "Santos" é a chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-162">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="5ecc7-163">Este exemplo imprime os campos de Olá de cada entidade na consola de toohello de resultados de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-163">This example prints hello fields of each entity in hello query results toohello console.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="5ecc7-164">consulta de Olá neste exemplo inclui todas as entidades de Olá que correspondem aos critérios de filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-164">hello query in this example brings all hello entities that match hello filter criteria.</span></span> <span data-ttu-id="5ecc7-165">Se tiver tabelas grandes e precisa, muitas vezes, as entidades da tabela toodownload Olá, recomendamos que armazene os dados em blobs de armazenamento do Azure em vez disso.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-165">If you have large tables and need toodownload hello table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="5ecc7-166">Obter um intervalo de entidades numa partição</span><span class="sxs-lookup"><span data-stu-id="5ecc7-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="5ecc7-167">Se não quiser tooquery todas as entidades de Olá numa partição, pode especificar um intervalo através da combinação de filtro de chave de partição de Olá com um filtro de chave de linha.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-167">If you don't want tooquery all hello entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="5ecc7-168">Olá exemplo de código seguinte utiliza dois filtros tooget todas as entidades na partição "Santos", em que a chave de linha de Olá (nome próprio) começa com uma letra anterior ao "E" Olá por letras do alfabeto e, em seguida, imprime os resultados da consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-168">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter earlier than 'E' in hello alphabet and then prints hello query results.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="5ecc7-169">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="5ecc7-169">Retrieve a single entity</span></span>
<span data-ttu-id="5ecc7-170">Pode escrever uma consulta tooretrieve uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-170">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="5ecc7-171">Olá seguinte código utiliza **table_operation::retrieve_entity** cliente de Olá toospecify "Jorge Santos".</span><span class="sxs-lookup"><span data-stu-id="5ecc7-171">hello following code uses **table_operation::retrieve_entity** toospecify hello customer 'Jeff Smith'.</span></span> <span data-ttu-id="5ecc7-172">Este método devolve apenas uma entidade em vez de uma coleção, não sendo hello valor devolvido em **table_result**.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-172">This method returns just one entity, rather than a collection, and hello returned value is in **table_result**.</span></span> <span data-ttu-id="5ecc7-173">A especificação de chaves de partição e da fila numa consulta é Olá tooretrieve da forma mais rápida do serviço de tabela Olá, uma única entidade.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-173">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="5ecc7-174">Substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="5ecc7-174">Replace an entity</span></span>
<span data-ttu-id="5ecc7-175">tooreplace uma entidade, obtê-lo a partir do serviço de tabela Olá, modificar o objecto entidade de Olá e, em seguida, guarde as alterações de Olá fazer uma cópia de serviço de tabela toohello.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-175">tooreplace an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="5ecc7-176">Olá código seguinte altera o endereço de e-mail e o número de telefone de um cliente existente.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-176">hello following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="5ecc7-177">Em vez de chamar **table_operation::insert_entity**, este código utiliza **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="5ecc7-178">Isto faz com que Olá entidade toobe totalmente substituída no servidor de Olá, a menos que a entidade de Olá no servidor de Olá foi alterada desde que foi obtida, caso em que a operação de Olá irá falhar.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-178">This causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="5ecc7-179">Esta falha é tooprevent a aplicação inadvertidamente uma alteração efetuada entre Olá obtenção e atualização por outro componente da aplicação.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-179">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="5ecc7-180">Olá processamento adequado desta falha é tooretrieve Olá entidade novamente, efetuar as alterações (se ainda forem válidas) e, em seguida, executar outra **table_operation::replace_entity** operação.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-180">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="5ecc7-181">secção seguinte Olá irá mostrar como toooverride este comportamento.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-181">hello next section will show you how toooverride this behavior.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="5ecc7-182">Inserir ou substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="5ecc7-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="5ecc7-183">**table_operation::replace_entity** operações falharão se a entidade de Olá tiver sido alterada desde que foi obtida do servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-183">**table_operation::replace_entity** operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="5ecc7-184">Além disso, tem de obter Olá entidade do servidor de Olá primeiro por ordem para **table_operation::replace_entity** toobe com êxito.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-184">Furthermore, you must retrieve hello entity from hello server first in order for **table_operation::replace_entity** toobe successful.</span></span> <span data-ttu-id="5ecc7-185">Por vezes, no entanto, não sabe se a entidade de Olá existe no servidor de Olá e Olá os valores atuais armazenados na mesma são irrelevantes — a atualização deve substituí todos eles.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-185">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="5ecc7-186">tooaccomplish, teria de utilizar um **table_operation::insert_or_replace_entity** operação.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-186">tooaccomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="5ecc7-187">Esta operação insere a entidade de Olá se não existir ou substitui-lo se existir, independentemente de quando foi feita a última atualização da Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-187">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span> <span data-ttu-id="5ecc7-188">No seguinte exemplo de código de Olá, a entidade de cliente Olá para Jorge Santos ainda é obtida, mas é guardada, em seguida, servidor de back-toohello via **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-188">In hello following code example, hello customer entity for Jeff Smith is still retrieved, but it is then saved back toohello server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="5ecc7-189">As atualizações efetuadas toohello entidade entre a operação de obtenção e atualização Olá serão substituídas.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-189">Any updates made toohello entity between hello retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="5ecc7-190">Consultar um subconjunto de propriedades de entidade</span><span class="sxs-lookup"><span data-stu-id="5ecc7-190">Query a subset of entity properties</span></span>
<span data-ttu-id="5ecc7-191">Uma tabela de tooa de consulta pode obter apenas algumas propriedades de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-191">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="5ecc7-192">Olá consulta Olá seguinte código utiliza Olá **table_query::set_select_columns** método tooreturn apenas Olá endereços de e-mail de entidades na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-192">hello query in hello following code uses hello **table_query::set_select_columns** method tooreturn only hello email addresses of entities in hello table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="5ecc7-193">Consultar algumas propriedades de uma entidade é uma operação mais eficiente do que todas as propriedades a obter.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="5ecc7-194">Eliminar uma entidade</span><span class="sxs-lookup"><span data-stu-id="5ecc7-194">Delete an entity</span></span>
<span data-ttu-id="5ecc7-195">Pode facilmente eliminar uma entidade depois de a ter obtido.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="5ecc7-196">Assim que a entidade de Olá é obtida, chamar **table_operation::delete_entity** com Olá toodelete de entidade.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-196">Once hello entity is retrieved, call **table_operation::delete_entity** with hello entity toodelete.</span></span> <span data-ttu-id="5ecc7-197">Em seguida, chame Olá **cloud_table.execute** método.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-197">Then call hello **cloud_table.execute** method.</span></span> <span data-ttu-id="5ecc7-198">Olá código seguinte obtém e elimina uma entidade com uma chave de partição de "Santos" e uma chave de linha de "Jorge".</span><span class="sxs-lookup"><span data-stu-id="5ecc7-198">hello following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="5ecc7-199">Eliminar uma tabela</span><span class="sxs-lookup"><span data-stu-id="5ecc7-199">Delete a table</span></span>
<span data-ttu-id="5ecc7-200">Por fim, Olá seguinte exemplo de código elimina uma tabela a partir de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-200">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="5ecc7-201">Uma tabela que foi eliminada estará indisponível toobe recriada durante um período de tempo após a eliminação de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-201">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="5ecc7-202">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5ecc7-202">Next steps</span></span>
<span data-ttu-id="5ecc7-203">Agora que aprendeu as noções básicas de Olá do table storage, siga estas toolearn ligações mais sobre o Storage do Azure:</span><span class="sxs-lookup"><span data-stu-id="5ecc7-203">Now that you've learned hello basics of table storage, follow these links toolearn more about Azure Storage:</span></span>  

* <span data-ttu-id="5ecc7-204">[Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="5ecc7-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="5ecc7-205">Como toouse Blob storage do C++</span><span class="sxs-lookup"><span data-stu-id="5ecc7-205">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="5ecc7-206">Como toouse armazenamento de filas do C++</span><span class="sxs-lookup"><span data-stu-id="5ecc7-206">How toouse Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="5ecc7-207">Lista de recursos de armazenamento do Azure em C++</span><span class="sxs-lookup"><span data-stu-id="5ecc7-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="5ecc7-208">Biblioteca de clientes do Storage para referência do C++</span><span class="sxs-lookup"><span data-stu-id="5ecc7-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="5ecc7-209">Documentação do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecc7-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
