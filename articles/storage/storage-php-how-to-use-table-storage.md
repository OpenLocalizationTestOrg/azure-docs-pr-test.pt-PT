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
# <a name="how-toouse-table-storage-from-php"></a>Como toouse tabela storage do PHP
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Descrição geral
Este guia mostra como tooperform cenários comuns utilizando Olá o serviço de Azure Table. Exemplos de Olá são escritos no PHP e utilizam Olá [Azure SDK para PHP][download]. Olá os cenários abrangidos incluem **criar e eliminar uma tabela e inserir, eliminar e consultar entidades numa tabela**. Para obter mais informações sobre Olá serviço tabela do Azure, consulte Olá [passos](#next-steps) secção.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Criar uma aplicação PHP
Olá, só é o requisito para criar uma aplicação PHP que acede ao serviço de Azure Table Olá Olá de referência de classes no Olá Azure SDK para PHP a partir de dentro do seu código. Pode utilizar qualquer toocreate de ferramentas de desenvolvimento da aplicação, incluindo o bloco de notas.

Neste guia, pode utiliza as funcionalidades do serviço de tabela que podem ser chamadas de dentro de uma aplicação PHP localmente, ou no código em execução dentro de uma função da web do Azure, a função de trabalho ou o Web site.

## <a name="get-hello-azure-client-libraries"></a>Obter Olá bibliotecas de cliente do Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>Configurar o serviço de tabela do aplicação tooaccess Olá
toouse Olá Azure Table APIs de serviço, tem de:

1. Ficheiro de Carregador automático de Olá de referência utilizando Olá [require_once] [ require_once] declaração, e
2. Referência a quaisquer classes que poderá utilizar.

Olá exemplo seguinte mostra como tooinclude Olá Carregador automático de ficheiros e referência Olá **ServicesBuilder** classe.

> [!NOTE]
> Exemplos de Olá neste artigo partem do princípio de que instalou Olá bibliotecas de cliente do PHP do Azure através do compositor. Se instalou manualmente bibliotecas Olá, terá de tooreference Olá <code>WindowsAzure.php</code> Carregador automático ficheiros.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Nos exemplos de Olá abaixo, Olá `require_once` instrução sempre é apresentada, mas apenas Olá classes necessárias para tooexecute de exemplo de Olá são referenciadas.

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma ligação de armazenamento do Azure
um cliente do serviço de Azure Table tooinstantiate, tem de ter uma cadeia de ligação válido. formato de Olá para Olá cadeia de ligação de serviço tabela é:

Para aceder a um serviço em direto:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Para aceder ao armazenamento de emulador de Olá:

```php
UseDevelopmentStorage=true
```

toocreate qualquer cliente de serviço do Azure, terá de toouse Olá **ServicesBuilder** classe. Pode:

* passar ligação Olá cadeia diretamente tooit ou
* utilizar Olá **CloudConfigurationManager (CCM)** toocheck externo várias origens para a cadeia de ligação de Olá:
  * Por predefinição, este inclui suporte para uma origem externa - variáveis de ambientais
  * Pode adicionar novas origens expandindo Olá **ConnectionStringSource** classe

Para obter exemplos Olá aqui descritos, cadeia de ligação de Olá será transmitida diretamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Criar uma tabela
A **TableRestProxy** objeto permite-lhe criar uma tabela com Olá **createTable** método. Ao criar uma tabela, pode definir o tempo limite do serviço de tabela Olá. (Para obter mais informações sobre o tempo limite do serviço de tabela Olá, consulte [tempos limite de definição para operações de serviço tabela][table-service-timeouts].)

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

Para informações sobre restrições de nomes de tabela, consulte [Olá compreender o modelo de dados do serviço tabela][table-data-model].

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de tooa entidade
tooadd uma tabela de tooa de entidade, crie um novo **entidade** objeto e transmita-demasiado**TableRestProxy -> insertEntity**. Tenha em atenção que quando criar uma entidade, terá de especificar um `PartitionKey` e `RowKey`. Estas são Olá identificadores exclusivos para uma entidade e são valores que podem ser consultados muito mais rapidamente do que outras propriedades de entidade. Olá sistema utiliza `PartitionKey` tooautomatically distribuir entidades da tabela de Olá através de vários nós de armazenamento. Entidades com Olá mesmo `PartitionKey` são armazenadas no Olá mesmo nó. (Várias entidades armazenadas no Olá mesmo nó de efetuar as operações melhor do que em entidades armazenadas em nós diferentes.) Olá `RowKey` é Olá ID exclusivo de uma entidade dentro de uma partição.

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

Para obter informações sobre as propriedades de tabela e tipos, consulte [Olá compreender o modelo de dados do serviço tabela][table-data-model].

Olá **TableRestProxy** classe fornece dois métodos alternativos para inserir entidades: **insertOrMergeEntity** e **insertOrReplaceEntity**. toouse destes métodos, crie um novo **entidade** e transmita-o como um método de tooeither do parâmetro. Cada método irá inserir a entidade de Olá se não existir. Se já existir uma entidade de Olá, **insertOrMergeEntity** atualiza os valores de propriedade se já existem propriedades de Olá e adiciona novas propriedades se não existir, enquanto **insertOrReplaceEntity** completamente substitui uma entidade existente. Olá seguinte exemplo mostra como toouse **insertOrMergeEntity**. Se Olá entidade com `PartitionKey` "tasksSeattle" e `RowKey` "1" ainda não existir, será inserido. No entanto, se anteriormente tiver sido introduzida (conforme ilustrado no exemplo Olá acima), Olá `DueDate` propriedade serão atualizados e Olá `Status` propriedade será adicionada. Olá `Description` e `Location` propriedades também são atualizadas, mas com valores que efetivamente deixe-os inalterado. Se estas duas propriedades última não foram adicionadas, conforme mostrado no exemplo Olá, mas existiam na entidade de destino Olá, os respetivos valores existentes permanecerá inalterados.

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

## <a name="retrieve-a-single-entity"></a>Obter uma única entidade
Olá **TableRestProxy -> getEntity** método permite-lhe tooretrieve uma entidade única através de consultas para o respetivo `PartitionKey` e `RowKey`. Exemplo de Olá abaixo, Olá chave de partição `tasksSeattle` e a chave de linha `1` são transmitidos toohello **getEntity** método.

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

## <a name="retrieve-all-entities-in-a-partition"></a>Obter todas as entidades numa partição
Consultas de entidade são construídas utilizando filtros (para obter mais informações, consulte [consultar tabelas e entidades][filters]). tooretrieve todas as entidades numa partição, utilize o filtro de Olá "PartitionKey eq *partition_name*". Olá seguinte exemplo mostra como tooretrieve todas as entidades numa Olá `tasksSeattle` partição transferindo toohello um filtro **queryEntities** método.

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>Obter um subconjunto de entidades numa partição
Olá mesmo padrão utilizado no exemplo anterior Olá pode ser utilizado tooretrieve qualquer subconjunto de entidades numa partição. subconjunto de Olá de entidades é possível obter são determinados pelo filtro de Olá utilizar (para obter mais informações, consulte [consultar tabelas e entidades][filters]) .hello seguinte exemplo mostra como toouse tooretrieve um filtro todas as entidades com um específico `Location` e um `DueDate` menor do que uma data especificada.

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

## <a name="retrieve-a-subset-of-entity-properties"></a>Obter um subconjunto de propriedades de entidade
Uma consulta pode obter um subconjunto de propriedades de entidade. Esta técnica, denominada *projecção*, reduz a largura de banda e pode melhorar o desempenho de consulta, especialmente para entidades grandes. obter de uma propriedade toobe toospecify, transmitir Olá nome de Olá propriedade toohello **consulta -> addSelectField** método. Pode chamar este método tooadd várias vezes mais propriedades. Depois de executar **TableRestProxy -> queryEntities**, Olá devolvido entidades só terão de propriedades de Olá selecionado. (Se quiser tooreturn um subconjunto de entidades de tabela, utilize um filtro conforme mostrado nas consultas Olá acima.)

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

## <a name="update-an-entity"></a>Atualizar uma entidade
Uma entidade existente pode ser atualizada utilizando Olá **entidade -> setProperty** e **entidade -> addProperty** métodos na entidade Olá e, em seguida, chamar **TableRestProxy -> updateEntity** . Olá exemplo seguinte obtém uma entidade, modifica uma propriedade, remove outra propriedade e adiciona uma nova propriedade. Tenha em atenção que pode remover uma propriedade de definir o respetivo valor demasiado**nulo**.

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

## <a name="delete-an-entity"></a>Eliminar uma entidade
toodelete uma entidade, transmitir o nome da tabela de Olá e entidade Olá `PartitionKey` e `RowKey` toohello **TableRestProxy -> deleteEntity** método.

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

Tenha em atenção para verificações de simultaneidade, pode definir Olá Etag para um toobe entidade eliminada utilizando Olá **DeleteEntityOptions -> setEtag** Olá método e transmitir **DeleteEntityOptions** objeto demasiado**deleteEntity** como um parâmetro quarto.

## <a name="batch-table-operations"></a>Operações de tabela do batch
Olá **TableRestProxy -> batch** método permite-lhe tooexecute várias operações num único pedido. Olá padrão aqui envolve adicionar operações demasiado**BatchRequest** objeto e, em seguida, passou Olá **BatchRequest** objeto toohello **TableRestProxy -> batch** método. tooadd tooa uma operação **BatchRequest** objeto, pode chamar qualquer um dos Olá várias vezes os métodos seguintes:

* **addInsertEntity** (adiciona uma operação insertEntity)
* **addUpdateEntity** (adiciona uma operação updateEntity)
* **addMergeEntity** (adiciona uma operação mergeEntity)
* **addInsertOrReplaceEntity** (adiciona uma operação insertOrReplaceEntity)
* **addInsertOrMergeEntity** (adiciona uma operação insertOrMergeEntity)
* **addDeleteEntity** (adiciona uma operação deleteEntity)

Olá seguinte exemplo mostra como tooexecute **insertEntity** e **deleteEntity** operações num único pedido:

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

Para obter mais informações sobre a criação de batches de operações da tabela, consulte [efetuar transações de grupo de entidade][entity-group-transactions].

## <a name="delete-a-table"></a>Eliminar uma tabela
Por fim, toodelete uma tabela, transmitir toohello de nome de tabela Olá **TableRestProxy -> deleteTable** método.

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

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá de Olá serviço tabela do Azure, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.

* [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.

* [Centro para programadores do PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
