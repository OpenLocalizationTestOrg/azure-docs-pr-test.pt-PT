---
title: aaaHow toouse Table storage do Java | Microsoft Docs
description: "Armazene dados estruturados na nuvem de Olá utilizando o Table storage do Azure, um arquivo de dados NoSQL."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f72cac3fc10cf0aef74780b84c515d93d715d787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a>Como toouse Table storage do Java
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Descrição geral
Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de tabelas do Azure. Exemplos de Olá são escritos em Java e utilizar Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java]. Olá os cenários abrangidos incluem **criar**, **listagem**, e **eliminar** tabelas, bem como **inserir**,  **consultar**, **modificar**, e **eliminar** entidades numa tabela. Para obter mais informações sobre as tabelas, consulte Olá [passos](#Next-Steps) secção.

Nota: Um SDK está disponível para programadores que estiver a utilizar o armazenamento do Azure em dispositivos Android. Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Criar uma aplicação Java
Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação Java localmente ou numa código em execução numa função da web ou função de trabalho no Azure.

toodo por isso, terá de tooinstall Olá Kit de desenvolvimento Java (JDK) e criar uma conta de armazenamento do Azure na sua subscrição do Azure. Assim que tiver feito, terá de tooverify que o seu sistema de desenvolvimento cumpre os requisitos mínimos de Olá e dependências que são apresentadas nas Olá [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub. Se o seu sistema cumpre os requisitos, pode seguir Olá as instruções para transferir e instalar Olá bibliotecas de armazenamento do Azure para Java no seu sistema desse repositório. Depois de concluir essas tarefas, será capaz de toocreate uma aplicação de Java que utiliza os exemplos de Olá neste artigo.

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurar o armazenamento de tabelas de tooaccess de aplicação
Adicione Olá importação instruções toohello superior do ficheiro de Java olá onde pretende que as tabelas armazenamento toouse Microsoft Azure APIs tooaccess os seguintes:

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurar uma cadeia de ligação de armazenamento do Azure
Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados. Quando em execução numa aplicação de cliente, tem de fornecer uma cadeia de ligação de armazenamento Olá no Olá seguir o formato, utilizando o nome de Olá da sua conta de armazenamento e Olá chave de acesso primária para a conta de armazenamento de Olá listada no Olá [portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores. Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Na execução aplicação dentro de uma função no Microsoft Azure, esta cadeia pode ser armazenada no ficheiro de configuração de serviço Olá, *serviceconfiguration. Cscfg*e pode ser acedido com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método. Eis um exemplo de obter a cadeia de ligação de Olá de um **definição** elemento com o nome *StorageConnectionString* no ficheiro de configuração do serviço de Olá:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.

## <a name="how-to-create-a-table"></a>Como: criar uma tabela
A **CloudTableClient** objeto permite-lhe obter objetos de referência para as tabelas e entidades. Olá código seguinte cria um **CloudTableClient** objeto e utiliza-toocreate um novo **CloudTable** objecto que representa uma tabela com o nome "as pessoas". (Nota: existem formas adicionais toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** no Olá [referência do SDK do Azure armazenamento cliente].)

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a>Como: listar as tabelas de Olá
tooget uma lista de tabelas, chamada Olá **CloudTableClient.listTables()** método tooretrieve uma iterable lista de nomes de tabela.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a>Como: adicionar uma tabela de tooa entidade
As entidades mapeiam objetos tooJava através de uma classe personalizada implementar **TableEntity**. Para sua comodidade, Olá **TableServiceEntity** classe implementa **TableEntity** e utiliza as propriedades da toomap de reflexão toogetter e um setter métodos com o nome para Olá propriedades. em primeiro lugar, tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de Olá de entidade. Olá código seguinte define uma classe de entidade que utiliza o nome próprio do cliente Olá como chave de linha de Olá e o apelido como chave de partição Olá. Em conjunto, a partição de uma entidade e a chave de linha de identificar exclusivamente entidade Olá na tabela de Olá. Entidades com Olá a mesma chave de partição pode ser consultada mais rapidamente do que as chaves de partição diferentes.

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

As operações de tabela que envolvem entidades requerem um **TableOperation** objeto. Este objeto define Olá operação toobe efetuada numa entidade, que pode ser executada com um **CloudTable** objeto. Olá código seguinte cria uma nova instância do Olá **CustomerEntity** classe com algumas toobe de dados de cliente armazenado. Olá código seguinte chama **TableOperation.insertOrReplace** toocreate um **TableOperation** tooinsert uma entidade de objeto para uma tabela e associa novos Olá **CustomerEntity**com o mesmo. Por fim, Olá chama Olá **executar** método no Olá **CloudTable** objeto, especifica a tabela de "pessoas" Olá e Olá novo **TableOperation**, que, em seguida, envia um toohello armazenamento serviço tooinsert Olá nova entidade de cliente na tabela de "pessoas" Olá, ou um pedido de substituir entidade Olá se já existir.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a>Como: Inserir um lote de entidades
Pode inserir um lote de serviço do entidades toohello tabela numa operação de escrita. Olá código seguinte cria um **TableBatchOperation** objeto, em seguida, adiciona três inserir tooit de operações. Cada operação de inserção é adicionada ao criar um novo objeto de entidade, os respetivos valores a definição e, em seguida, ao chamar Olá **inserir** método no Olá **TableBatchOperation** objeto de entidade de Olá tooassociate com um novo a operação de inserção. Em seguida, Olá código chama **executar** no Olá **CloudTable** objeto, especificar a tabela de "pessoas" Olá e Olá **TableBatchOperation** objeto, o que envia o lote de Olá da tabela serviço de armazenamento do toohello Operations num único pedido.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Toonote algumas coisas nas operações de lote:

* Pode efetuar cópias de segurança too100 insert, delete, intercalação, substituir, insert ou intercalação e inserir ou substituir as operações em qualquer combinação de um único lote.
* Uma operação em lote pode ter uma operação de obter, se esta é uma operação em lote de Olá apenas Olá.
* Todas as entidades numa operação batch único tem de ter Olá mesma chave de partição.
* Uma operação em lote é limitado tooa payload de dados de 4MB.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Como: obter todas as entidades numa partição
tooquery uma tabela para entidades numa partição, pode utilizar um **TableQuery**. Chamar **TableQuery.from** toocreate uma consulta numa determinada tabela que devolve um tipo de resultado especificado. Olá código seguinte especifica um filtro para entidades em que "Santos" é a chave de partição Olá. **TableQuery.generateFilterCondition** é um método de programa auxiliar toocreate filtros para consultas. Chamar **onde** numa referência de Olá devolvida pelo Olá **TableQuery.from** consulta de toohello do método tooapply Olá filtro. Quando Olá é executar a consulta com uma chamada demasiado**executar** no Olá **CloudTable** objeto devolve um **Iterator** com Olá **CustomerEntity**especificado do tipo de resultado. Em seguida, pode utilizar Olá **Iterator** devolvida uma para cada ciclo tooconsume Olá obter os resultados. Este código imprime os campos de Olá de cada entidade na consola de toohello de resultados de consulta Olá.

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Como: obter um intervalo de entidades numa partição
Se não quiser tooquery todas as entidades de Olá numa partição, pode especificar um intervalo através da utilização de operadores de comparação num filtro. Olá seguir combina código dois filtros tooget todas as entidades numa partição "Santos" em que a chave de linha de Olá (nome próprio) começa com uma letra segurança too'E' no Olá por letras do alfabeto. Em seguida, imprime os resultados da consulta Olá. Se utilizar a tabela de toohello adicionado Olá entidades no batch Olá inserir a secção deste guia, apenas duas entidades são devolvidas desta vez (Bernardo e Denise Santos); Jorge Santos não está incluído.

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a>Como: obter uma única entidade
Pode escrever uma consulta tooretrieve uma entidade única e específica. chamadas de código seguinte Olá **TableOperation.retrieve** com partição linha de chave e os parâmetros de chave toospecify Olá cliente "Jorge Santos", em vez de criar um **TableQuery** e utilizar Olá toodo de filtros mesma coisa. Quando executada, Olá obter operação devolve apenas uma entidade em vez de uma coleção. Olá **getResultAsType** método casts tipo toohello de resultado de Olá do destino da atribuição de Olá, um **CustomerEntity** objeto. Se este tipo não é compatível com o tipo de Olá especificado para a consulta de Olá, será emitida uma exceção. Se nenhuma entidade tem uma partição exata e a chave de linha corresponder, é devolvido um valor nulo. A especificação de chaves de partição e da fila numa consulta é Olá tooretrieve da forma mais rápida do serviço de tabela Olá, uma única entidade.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a>Como: modificar uma entidade
toomodify uma entidade, obtê-lo a partir do serviço de tabela Olá, se o objeto de entidade toohello alterações e guardar alterações de Olá toohello back-serviço de tabela com uma operação de substituição ou intercalação. Olá código seguinte altera o número de telefone de um cliente existente. Em vez de chamar **TableOperation.insert** , como fizemos tooinsert, este código chama **TableOperation.replace**. Olá **Cloudtable** método chama o serviço de tabela Olá e entidade Olá é substituída, a menos que outra aplicação alterado-la no tempo de Olá, uma vez que esta aplicação obtido. Quando isso acontece, é emitida uma exceção e a entidade Olá tem de ter obtida, modificar e guardar novamente. Neste padrão de repetição de simultaneidade otimista é comum num sistema de armazenamento distribuído.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a>Como: consultar um subconjunto de propriedades de entidade
Uma tabela de tooa de consulta pode obter apenas algumas propriedades de uma entidade. Esta técnica, denominada projeção, reduz a largura de banda e pode melhorar o desempenho da consulta, especialmente para entidades grandes. Olá consulta Olá seguinte código utiliza Olá **selecione** método tooreturn apenas Olá endereços de e-mail de entidades na tabela de Olá. Olá os resultados são projetados para uma coleção de **cadeia** com a ajuda de Olá de um **EntityResolver**, que does Olá conversão do tipo entidades Olá devolvido do servidor de Olá. Pode saber mais sobre a projeção na [tabelas do Azure: Upsert e da projeção da consulta][Azure Tables: Introducing Upsert and Query Projection]. Tenha em atenção que projeção não é suportada no emulador de armazenamento local Olá, pelo que este código é executado apenas quando utilizar uma conta de serviço de tabela Olá.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a>Como: inserir ou substituir uma entidade
Muitas vezes, pretende tooadd uma tabela de tooa entidade sem saberem se já existir na tabela de Olá. Uma operação de inserção ou substituir permite-lhe toomake único pedido que irá inserir a entidade de Olá se não existir ou substitua Olá existente um caso. Criar nos exemplos anteriores, hello seguinte código insere ou substitui entidade Olá para "Walter Harp". Depois de criar uma nova entidade, este código chama Olá **TableOperation.insertOrReplace** método. Este código, em seguida, chama **executar** no Olá **CloudTable** objeto com a inserção de tabela e Olá Olá ou operação de tabela como parâmetros de Olá de substituição. tooupdate só fazem parte de uma entidade Olá **TableOperation.insertOrMerge** método pode ser utilizado em vez disso. Tenha em atenção que inserir ou substituir não é suportada no emulador de armazenamento local Olá, pelo que este código é executado apenas quando utilizar uma conta de serviço de tabela Olá. Pode saber mais sobre inserir ou substituir e a inserção ou intercalação deste [tabelas do Azure: Upsert e da projeção da consulta][Azure Tables: Introducing Upsert and Query Projection].

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a>Como: eliminar uma entidade
Pode facilmente eliminar uma entidade depois de a ter obtido. Assim que a entidade de Olá é obtida, chamar **TableOperation.delete** com Olá toodelete de entidade. Em seguida, chame **executar** no Olá **CloudTable** objeto. Olá seguinte código obtém e elimina uma entidade de cliente.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a>Como: eliminar uma tabela
Por fim, hello seguinte código elimina uma tabela a partir de uma conta de armazenamento. Uma tabela que foi eliminada estará indisponível toobe recriada durante um período de tempo após a eliminação de Olá, normalmente, menos de forty segundos.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a>Passos seguintes

* [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.
* [Armazenamento do Azure SDK para Java][Azure Storage SDK for Java]
* [Referência do SDK de cliente de armazenamento do Azure][referência do SDK do Azure armazenamento cliente]
* [API REST do Storage do Azure][Azure Storage REST API]
* [Blogue da equipa do Storage do Azure][Azure Storage Team Blog]

Para obter mais informações, consulte também Olá [Centro de programadores Java](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência do SDK do Azure armazenamento cliente]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
