---
title: aaaHow toouse table storage do PHP | Microsoft Docs
description: "Saiba como toouse Olá serviço tabela toocreate do PHP e eliminar tabela e consulta Olá tabela, eliminação e inserção."
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 1e1036118e208280b4c205da7d7eea61e79359c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a><span data-ttu-id="2cbc7-103">Como toouse tabela storage do PHP</span><span class="sxs-lookup"><span data-stu-id="2cbc7-103">How toouse table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="2cbc7-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="2cbc7-104">Overview</span></span>
<span data-ttu-id="2cbc7-105">Este guia mostra como tooperform cenários comuns utilizando Olá o serviço de Azure Table.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="2cbc7-106">Exemplos de Olá são escritos no PHP e utilizam Olá [Azure SDK para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="2cbc7-106">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="2cbc7-107">Olá os cenários abrangidos incluem **criar e eliminar uma tabela e inserir, eliminar e consultar entidades numa tabela**.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-107">hello scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="2cbc7-108">Para obter mais informações sobre Olá serviço tabela do Azure, consulte Olá [passos](#next-steps) secção.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-108">For more information on hello Azure Table service, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="2cbc7-109">Criar uma aplicação PHP</span><span class="sxs-lookup"><span data-stu-id="2cbc7-109">Create a PHP application</span></span>
<span data-ttu-id="2cbc7-110">Olá, só é o requisito para criar uma aplicação PHP que acede ao serviço de Azure Table Olá Olá de referência de classes no Olá Azure SDK para PHP a partir de dentro do seu código.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-110">hello only requirement for creating a PHP application that accesses hello Azure Table service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="2cbc7-111">Pode utilizar qualquer toocreate de ferramentas de desenvolvimento da aplicação, incluindo o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="2cbc7-112">Neste guia, pode utiliza as funcionalidades do serviço de tabela que podem ser chamadas de dentro de uma aplicação PHP localmente, ou no código em execução dentro de uma função da web do Azure, a função de trabalho ou o Web site.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="2cbc7-113">Obter Olá bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="2cbc7-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a><span data-ttu-id="2cbc7-114">Configurar o serviço de tabela do aplicação tooaccess Olá</span><span class="sxs-lookup"><span data-stu-id="2cbc7-114">Configure your application tooaccess hello Table service</span></span>
<span data-ttu-id="2cbc7-115">toouse Olá Azure Table APIs de serviço, tem de:</span><span class="sxs-lookup"><span data-stu-id="2cbc7-115">toouse hello Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="2cbc7-116">Ficheiro de Carregador automático de Olá de referência utilizando Olá [require_once] [ require_once] declaração, e</span><span class="sxs-lookup"><span data-stu-id="2cbc7-116">Reference hello autoloader file using hello [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="2cbc7-117">Referência a quaisquer classes que poderá utilizar.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-117">Reference any classes you might use.</span></span>

<span data-ttu-id="2cbc7-118">Olá exemplo seguinte mostra como tooinclude Olá Carregador automático de ficheiros e referência Olá **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="2cbc7-119">Exemplos de Olá neste artigo partem do princípio de que instalou Olá bibliotecas de cliente do PHP do Azure através do compositor.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-119">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="2cbc7-120">Se instalou manualmente bibliotecas Olá, terá de tooreference Olá <code>WindowsAzure.php</code> Carregador automático ficheiros.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-120">If you installed hello libraries manually, you need tooreference hello <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="2cbc7-121">Nos exemplos de Olá abaixo, Olá `require_once` instrução sempre é apresentada, mas apenas Olá classes necessárias para tooexecute de exemplo de Olá são referenciadas.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-121">In hello examples below, hello `require_once` statement is always shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="2cbc7-122">Configurar uma ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2cbc7-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="2cbc7-123">um cliente do serviço de Azure Table tooinstantiate, tem de ter uma cadeia de ligação válido.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-123">tooinstantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="2cbc7-124">formato de Olá para Olá cadeia de ligação de serviço tabela é:</span><span class="sxs-lookup"><span data-stu-id="2cbc7-124">hello format for hello Table service connection string is:</span></span>

<span data-ttu-id="2cbc7-125">Para aceder a um serviço em direto:</span><span class="sxs-lookup"><span data-stu-id="2cbc7-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="2cbc7-126">Para aceder ao armazenamento de emulador de Olá:</span><span class="sxs-lookup"><span data-stu-id="2cbc7-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="2cbc7-127">toocreate qualquer cliente de serviço do Azure, terá de toouse Olá **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="2cbc7-128">Pode:</span><span class="sxs-lookup"><span data-stu-id="2cbc7-128">You can:</span></span>

* <span data-ttu-id="2cbc7-129">passar ligação Olá cadeia diretamente tooit ou</span><span class="sxs-lookup"><span data-stu-id="2cbc7-129">pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="2cbc7-130">utilizar Olá **CloudConfigurationManager (CCM)** toocheck externo várias origens para a cadeia de ligação de Olá:</span><span class="sxs-lookup"><span data-stu-id="2cbc7-130">use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="2cbc7-131">Por predefinição, este inclui suporte para uma origem externa - variáveis de ambientais</span><span class="sxs-lookup"><span data-stu-id="2cbc7-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="2cbc7-132">Pode adicionar novas origens expandindo Olá **ConnectionStringSource** classe</span><span class="sxs-lookup"><span data-stu-id="2cbc7-132">you can add new sources by extending hello **ConnectionStringSource** class</span></span>

<span data-ttu-id="2cbc7-133">Para obter exemplos Olá aqui descritos, cadeia de ligação de Olá será transmitida diretamente.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="2cbc7-134">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="2cbc7-134">Create a table</span></span>
<span data-ttu-id="2cbc7-135">A **TableRestProxy** objeto permite-lhe criar uma tabela com Olá **createTable** método.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-135">A **TableRestProxy** object lets you create a table with hello **createTable** method.</span></span> <span data-ttu-id="2cbc7-136">Ao criar uma tabela, pode definir o tempo limite do serviço de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-136">When creating a table, you can set hello Table service timeout.</span></span> <span data-ttu-id="2cbc7-137">(Para obter mais informações sobre o tempo limite do serviço de tabela Olá, consulte [tempos limite de definição para operações de serviço tabela][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="2cbc7-137">(For more information about hello Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

<span data-ttu-id="2cbc7-138">Para informações sobre restrições de nomes de tabela, consulte [Olá compreender o modelo de dados do serviço tabela][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="2cbc7-138">For information about restrictions on table names, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="2cbc7-139">Adicionar uma tabela de tooa entidade</span><span class="sxs-lookup"><span data-stu-id="2cbc7-139">Add an entity tooa table</span></span>
<span data-ttu-id="2cbc7-140">tooadd uma tabela de tooa de entidade, crie um novo **entidade** objeto e transmita-demasiado**TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-140">tooadd an entity tooa table, create a new **Entity** object and pass it too**TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="2cbc7-141">Tenha em atenção que quando criar uma entidade, terá de especificar um `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="2cbc7-142">Estas são Olá identificadores exclusivos para uma entidade e são valores que podem ser consultados muito mais rapidamente do que outras propriedades de entidade.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-142">These are hello unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="2cbc7-143">Olá sistema utiliza `PartitionKey` tooautomatically distribuir entidades da tabela de Olá através de vários nós de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-143">hello system uses `PartitionKey` tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="2cbc7-144">Entidades com Olá mesmo `PartitionKey` são armazenadas no Olá mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-144">Entities with hello same `PartitionKey` are stored on hello same node.</span></span> <span data-ttu-id="2cbc7-145">(Várias entidades armazenadas no Olá mesmo nó de efetuar as operações melhor do que em entidades armazenadas em nós diferentes.) Olá `RowKey` é Olá ID exclusivo de uma entidade dentro de uma partição.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-145">(Operations on multiple entities stored on hello same node perform better than on entities stored across different nodes.) hello `RowKey` is hello unique ID of an entity within a partition.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

<span data-ttu-id="2cbc7-146">Para obter informações sobre as propriedades de tabela e tipos, consulte [Olá compreender o modelo de dados do serviço tabela][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="2cbc7-146">For information about Table properties and types, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="2cbc7-147">Olá **TableRestProxy** classe fornece dois métodos alternativos para inserir entidades: **insertOrMergeEntity** e **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-147">hello **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="2cbc7-148">toouse destes métodos, crie um novo **entidade** e transmita-o como um método de tooeither do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-148">toouse these methods, create a new **Entity** and pass it as a parameter tooeither method.</span></span> <span data-ttu-id="2cbc7-149">Cada método irá inserir a entidade de Olá se não existir.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-149">Each method will insert hello entity if it does not exist.</span></span> <span data-ttu-id="2cbc7-150">Se já existir uma entidade de Olá, **insertOrMergeEntity** atualiza os valores de propriedade se já existem propriedades de Olá e adiciona novas propriedades se não existir, enquanto **insertOrReplaceEntity** completamente substitui uma entidade existente.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-150">If hello entity already exists, **insertOrMergeEntity** updates property values if hello properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="2cbc7-151">Olá seguinte exemplo mostra como toouse **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-151">hello following example shows how toouse **insertOrMergeEntity**.</span></span> <span data-ttu-id="2cbc7-152">Se Olá entidade com `PartitionKey` "tasksSeattle" e `RowKey` "1" ainda não existir, será inserido.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-152">If hello entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="2cbc7-153">No entanto, se anteriormente tiver sido introduzida (conforme ilustrado no exemplo Olá acima), Olá `DueDate` propriedade serão atualizados e Olá `Status` propriedade será adicionada.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-153">However, if it has previously been inserted (as shown in hello example above), hello `DueDate` property will be updated, and hello `Status` property will be added.</span></span> <span data-ttu-id="2cbc7-154">Olá `Description` e `Location` propriedades também são atualizadas, mas com valores que efetivamente deixe-os inalterado.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-154">hello `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="2cbc7-155">Se estas duas propriedades última não foram adicionadas, conforme mostrado no exemplo Olá, mas existiam na entidade de destino Olá, os respetivos valores existentes permanecerá inalterados.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-155">If these latter two properties were not added as shown in hello example, but existed on hello target entity, their existing values would remain unchanged.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="2cbc7-156">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="2cbc7-156">Retrieve a single entity</span></span>
<span data-ttu-id="2cbc7-157">Olá **TableRestProxy -> getEntity** método permite-lhe tooretrieve uma entidade única através de consultas para o respetivo `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-157">hello **TableRestProxy->getEntity** method allows you tooretrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="2cbc7-158">Exemplo de Olá abaixo, Olá chave de partição `tasksSeattle` e a chave de linha `1` são transmitidos toohello **getEntity** método.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-158">In hello example below, hello partition key `tasksSeattle` and row key `1` are passed toohello **getEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="2cbc7-159">Obter todas as entidades numa partição</span><span class="sxs-lookup"><span data-stu-id="2cbc7-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="2cbc7-160">Consultas de entidade são construídas utilizando filtros (para obter mais informações, consulte [consultar tabelas e entidades][filters]).</span><span class="sxs-lookup"><span data-stu-id="2cbc7-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="2cbc7-161">tooretrieve todas as entidades numa partição, utilize o filtro de Olá "PartitionKey eq *partition_name*".</span><span class="sxs-lookup"><span data-stu-id="2cbc7-161">tooretrieve all entities in partition, use hello filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="2cbc7-162">Olá seguinte exemplo mostra como tooretrieve todas as entidades numa Olá `tasksSeattle` partição transferindo toohello um filtro **queryEntities** método.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-162">hello following example shows how tooretrieve all entities in hello `tasksSeattle` partition by passing a filter toohello **queryEntities** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="2cbc7-163">Obter um subconjunto de entidades numa partição</span><span class="sxs-lookup"><span data-stu-id="2cbc7-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="2cbc7-164">Olá mesmo padrão utilizado no exemplo anterior Olá pode ser utilizado tooretrieve qualquer subconjunto de entidades numa partição.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-164">hello same pattern used in hello previous example can be used tooretrieve any subset of entities in a partition.</span></span> <span data-ttu-id="2cbc7-165">subconjunto de Olá de entidades é possível obter são determinados pelo filtro de Olá utilizar (para obter mais informações, consulte [consultar tabelas e entidades][filters]) .hello seguinte exemplo mostra como toouse tooretrieve um filtro todas as entidades com um específico `Location` e um `DueDate` menor do que uma data especificada.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-165">hello subset of entities you retrieve are determined by hello filter you use (for more information, see [Querying Tables and Entities][filters]).hello following example shows how toouse a filter tooretrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="2cbc7-166">Obter um subconjunto de propriedades de entidade</span><span class="sxs-lookup"><span data-stu-id="2cbc7-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="2cbc7-167">Uma consulta pode obter um subconjunto de propriedades de entidade.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="2cbc7-168">Esta técnica, denominada *projecção*, reduz a largura de banda e pode melhorar o desempenho de consulta, especialmente para entidades grandes.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="2cbc7-169">obter de uma propriedade toobe toospecify, transmitir Olá nome de Olá propriedade toohello **consulta -> addSelectField** método.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-169">toospecify a property toobe retrieved, pass hello name of hello property toohello **Query->addSelectField** method.</span></span> <span data-ttu-id="2cbc7-170">Pode chamar este método tooadd várias vezes mais propriedades.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-170">You can call this method multiple times tooadd more properties.</span></span> <span data-ttu-id="2cbc7-171">Depois de executar **TableRestProxy -> queryEntities**, Olá devolvido entidades só terão de propriedades de Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-171">After executing **TableRestProxy->queryEntities**, hello returned entities will only have hello selected properties.</span></span> <span data-ttu-id="2cbc7-172">(Se quiser tooreturn um subconjunto de entidades de tabela, utilize um filtro conforme mostrado nas consultas Olá acima.)</span><span class="sxs-lookup"><span data-stu-id="2cbc7-172">(If you want tooreturn a subset of Table entities, use a filter as shown in hello queries above.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="2cbc7-173">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="2cbc7-173">Update an entity</span></span>
<span data-ttu-id="2cbc7-174">Uma entidade existente pode ser atualizada utilizando Olá **entidade -> setProperty** e **entidade -> addProperty** métodos na entidade Olá e, em seguida, chamar **TableRestProxy -> updateEntity** .</span><span class="sxs-lookup"><span data-stu-id="2cbc7-174">An existing entity can be updated by using hello **Entity->setProperty** and **Entity->addProperty** methods on hello entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="2cbc7-175">Olá exemplo seguinte obtém uma entidade, modifica uma propriedade, remove outra propriedade e adiciona uma nova propriedade.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-175">hello following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="2cbc7-176">Tenha em atenção que pode remover uma propriedade de definir o respetivo valor demasiado**nulo**.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-176">Note that you can remove a property by setting its value too**null**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="2cbc7-177">Eliminar uma entidade</span><span class="sxs-lookup"><span data-stu-id="2cbc7-177">Delete an entity</span></span>
<span data-ttu-id="2cbc7-178">toodelete uma entidade, transmitir o nome da tabela de Olá e entidade Olá `PartitionKey` e `RowKey` toohello **TableRestProxy -> deleteEntity** método.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-178">toodelete an entity, pass hello table name, and hello entity's `PartitionKey` and `RowKey` toohello **TableRestProxy->deleteEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="2cbc7-179">Tenha em atenção para verificações de simultaneidade, pode definir Olá Etag para um toobe entidade eliminada utilizando Olá **DeleteEntityOptions -> setEtag** Olá método e transmitir **DeleteEntityOptions** objeto demasiado**deleteEntity** como um parâmetro quarto.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-179">Note that for concurrency checks, you can set hello Etag for an entity toobe deleted by using hello **DeleteEntityOptions->setEtag** method and passing hello **DeleteEntityOptions** object too**deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="2cbc7-180">Operações de tabela do batch</span><span class="sxs-lookup"><span data-stu-id="2cbc7-180">Batch table operations</span></span>
<span data-ttu-id="2cbc7-181">Olá **TableRestProxy -> batch** método permite-lhe tooexecute várias operações num único pedido.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-181">hello **TableRestProxy->batch** method allows you tooexecute multiple operations in a single request.</span></span> <span data-ttu-id="2cbc7-182">Olá padrão aqui envolve adicionar operações demasiado**BatchRequest** objeto e, em seguida, passou Olá **BatchRequest** objeto toohello **TableRestProxy -> batch** método.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-182">hello pattern here involves adding operations too**BatchRequest** object and then passing hello **BatchRequest** object toohello **TableRestProxy->batch** method.</span></span> <span data-ttu-id="2cbc7-183">tooadd tooa uma operação **BatchRequest** objeto, pode chamar qualquer um dos Olá várias vezes os métodos seguintes:</span><span class="sxs-lookup"><span data-stu-id="2cbc7-183">tooadd an operation tooa **BatchRequest** object, you can call any of hello following methods multiple times:</span></span>

* <span data-ttu-id="2cbc7-184">**addInsertEntity** (adiciona uma operação insertEntity)</span><span class="sxs-lookup"><span data-stu-id="2cbc7-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="2cbc7-185">**addUpdateEntity** (adiciona uma operação updateEntity)</span><span class="sxs-lookup"><span data-stu-id="2cbc7-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="2cbc7-186">**addMergeEntity** (adiciona uma operação mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="2cbc7-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="2cbc7-187">**addInsertOrReplaceEntity** (adiciona uma operação insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="2cbc7-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="2cbc7-188">**addInsertOrMergeEntity** (adiciona uma operação insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="2cbc7-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="2cbc7-189">**addDeleteEntity** (adiciona uma operação deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="2cbc7-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="2cbc7-190">Olá seguinte exemplo mostra como tooexecute **insertEntity** e **deleteEntity** operações num único pedido:</span><span class="sxs-lookup"><span data-stu-id="2cbc7-190">hello following example shows how tooexecute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="2cbc7-191">Para obter mais informações sobre a criação de batches de operações da tabela, consulte [efetuar transações de grupo de entidade][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="2cbc7-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="2cbc7-192">Eliminar uma tabela</span><span class="sxs-lookup"><span data-stu-id="2cbc7-192">Delete a table</span></span>
<span data-ttu-id="2cbc7-193">Por fim, toodelete uma tabela, transmitir toohello de nome de tabela Olá **TableRestProxy -> deleteTable** método.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-193">Finally, toodelete a table, pass hello table name toohello **TableRestProxy->deleteTable** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="2cbc7-194">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2cbc7-194">Next steps</span></span>
<span data-ttu-id="2cbc7-195">Agora que aprendeu as noções básicas de Olá de Olá serviço tabela do Azure, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-195">Now that you've learned hello basics of hello Azure Table service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="2cbc7-196">[Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="2cbc7-197">[Centro para programadores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="2cbc7-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
