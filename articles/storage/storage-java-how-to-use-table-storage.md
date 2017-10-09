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
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="fa9fa-103">Como toouse Table storage do Java</span><span class="sxs-lookup"><span data-stu-id="fa9fa-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="fa9fa-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="fa9fa-104">Overview</span></span>
<span data-ttu-id="fa9fa-105">Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="fa9fa-106">Exemplos de Olá são escritos em Java e utilizar Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="fa9fa-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="fa9fa-107">Olá os cenários abrangidos incluem **criar**, **listagem**, e **eliminar** tabelas, bem como **inserir**,  **consultar**, **modificar**, e **eliminar** entidades numa tabela.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="fa9fa-108">Para obter mais informações sobre as tabelas, consulte Olá [passos](#Next-Steps) secção.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="fa9fa-109">Nota: Um SDK está disponível para programadores que estiver a utilizar o armazenamento do Azure em dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="fa9fa-110">Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="fa9fa-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="fa9fa-111">Criar uma aplicação Java</span><span class="sxs-lookup"><span data-stu-id="fa9fa-111">Create a Java application</span></span>
<span data-ttu-id="fa9fa-112">Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação Java localmente ou numa código em execução numa função da web ou função de trabalho no Azure.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="fa9fa-113">toodo por isso, terá de tooinstall Olá Kit de desenvolvimento Java (JDK) e criar uma conta de armazenamento do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="fa9fa-114">Assim que tiver feito, terá de tooverify que o seu sistema de desenvolvimento cumpre os requisitos mínimos de Olá e dependências que são apresentadas nas Olá [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="fa9fa-115">Se o seu sistema cumpre os requisitos, pode seguir Olá as instruções para transferir e instalar Olá bibliotecas de armazenamento do Azure para Java no seu sistema desse repositório.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="fa9fa-116">Depois de concluir essas tarefas, será capaz de toocreate uma aplicação de Java que utiliza os exemplos de Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="fa9fa-117">Configurar o armazenamento de tabelas de tooaccess de aplicação</span><span class="sxs-lookup"><span data-stu-id="fa9fa-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="fa9fa-118">Adicione Olá importação instruções toohello superior do ficheiro de Java olá onde pretende que as tabelas armazenamento toouse Microsoft Azure APIs tooaccess os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fa9fa-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="fa9fa-119">Configurar uma cadeia de ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="fa9fa-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="fa9fa-120">Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="fa9fa-121">Quando em execução numa aplicação de cliente, tem de fornecer uma cadeia de ligação de armazenamento Olá no Olá seguir o formato, utilizando o nome de Olá da sua conta de armazenamento e Olá chave de acesso primária para a conta de armazenamento de Olá listada no Olá [portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="fa9fa-122">Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:</span><span class="sxs-lookup"><span data-stu-id="fa9fa-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="fa9fa-123">Na execução aplicação dentro de uma função no Microsoft Azure, esta cadeia pode ser armazenada no ficheiro de configuração de serviço Olá, *serviceconfiguration. Cscfg*e pode ser acedido com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="fa9fa-124">Eis um exemplo de obter a cadeia de ligação de Olá de um **definição** elemento com o nome *StorageConnectionString* no ficheiro de configuração do serviço de Olá:</span><span class="sxs-lookup"><span data-stu-id="fa9fa-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="fa9fa-125">Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="fa9fa-126">Como: criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="fa9fa-126">How to: Create a table</span></span>
<span data-ttu-id="fa9fa-127">A **CloudTableClient** objeto permite-lhe obter objetos de referência para as tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="fa9fa-128">Olá código seguinte cria um **CloudTableClient** objeto e utiliza-toocreate um novo **CloudTable** objecto que representa uma tabela com o nome "as pessoas".</span><span class="sxs-lookup"><span data-stu-id="fa9fa-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="fa9fa-129">(Nota: existem formas adicionais toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** no Olá [referência do SDK do Azure armazenamento cliente].)</span><span class="sxs-lookup"><span data-stu-id="fa9fa-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

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

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="fa9fa-130">Como: listar as tabelas de Olá</span><span class="sxs-lookup"><span data-stu-id="fa9fa-130">How to: List hello tables</span></span>
<span data-ttu-id="fa9fa-131">tooget uma lista de tabelas, chamada Olá **CloudTableClient.listTables()** método tooretrieve uma iterable lista de nomes de tabela.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

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

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="fa9fa-132">Como: adicionar uma tabela de tooa entidade</span><span class="sxs-lookup"><span data-stu-id="fa9fa-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="fa9fa-133">As entidades mapeiam objetos tooJava através de uma classe personalizada implementar **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="fa9fa-134">Para sua comodidade, Olá **TableServiceEntity** classe implementa **TableEntity** e utiliza as propriedades da toomap de reflexão toogetter e um setter métodos com o nome para Olá propriedades.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="fa9fa-135">em primeiro lugar, tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de Olá de entidade.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="fa9fa-136">Olá código seguinte define uma classe de entidade que utiliza o nome próprio do cliente Olá como chave de linha de Olá e o apelido como chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="fa9fa-137">Em conjunto, a partição de uma entidade e a chave de linha de identificar exclusivamente entidade Olá na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="fa9fa-138">Entidades com Olá a mesma chave de partição pode ser consultada mais rapidamente do que as chaves de partição diferentes.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="fa9fa-139">As operações de tabela que envolvem entidades requerem um **TableOperation** objeto.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="fa9fa-140">Este objeto define Olá operação toobe efetuada numa entidade, que pode ser executada com um **CloudTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="fa9fa-141">Olá código seguinte cria uma nova instância do Olá **CustomerEntity** classe com algumas toobe de dados de cliente armazenado.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="fa9fa-142">Olá código seguinte chama **TableOperation.insertOrReplace** toocreate um **TableOperation** tooinsert uma entidade de objeto para uma tabela e associa novos Olá **CustomerEntity**com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="fa9fa-143">Por fim, Olá chama Olá **executar** método no Olá **CloudTable** objeto, especifica a tabela de "pessoas" Olá e Olá novo **TableOperation**, que, em seguida, envia um toohello armazenamento serviço tooinsert Olá nova entidade de cliente na tabela de "pessoas" Olá, ou um pedido de substituir entidade Olá se já existir.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

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

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="fa9fa-144">Como: Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="fa9fa-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="fa9fa-145">Pode inserir um lote de serviço do entidades toohello tabela numa operação de escrita.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="fa9fa-146">Olá código seguinte cria um **TableBatchOperation** objeto, em seguida, adiciona três inserir tooit de operações.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="fa9fa-147">Cada operação de inserção é adicionada ao criar um novo objeto de entidade, os respetivos valores a definição e, em seguida, ao chamar Olá **inserir** método no Olá **TableBatchOperation** objeto de entidade de Olá tooassociate com um novo a operação de inserção.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="fa9fa-148">Em seguida, Olá código chama **executar** no Olá **CloudTable** objeto, especificar a tabela de "pessoas" Olá e Olá **TableBatchOperation** objeto, o que envia o lote de Olá da tabela serviço de armazenamento do toohello Operations num único pedido.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

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

<span data-ttu-id="fa9fa-149">Toonote algumas coisas nas operações de lote:</span><span class="sxs-lookup"><span data-stu-id="fa9fa-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="fa9fa-150">Pode efetuar cópias de segurança too100 insert, delete, intercalação, substituir, insert ou intercalação e inserir ou substituir as operações em qualquer combinação de um único lote.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="fa9fa-151">Uma operação em lote pode ter uma operação de obter, se esta é uma operação em lote de Olá apenas Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="fa9fa-152">Todas as entidades numa operação batch único tem de ter Olá mesma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="fa9fa-153">Uma operação em lote é limitado tooa payload de dados de 4MB.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="fa9fa-154">Como: obter todas as entidades numa partição</span><span class="sxs-lookup"><span data-stu-id="fa9fa-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="fa9fa-155">tooquery uma tabela para entidades numa partição, pode utilizar um **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="fa9fa-156">Chamar **TableQuery.from** toocreate uma consulta numa determinada tabela que devolve um tipo de resultado especificado.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="fa9fa-157">Olá código seguinte especifica um filtro para entidades em que "Santos" é a chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="fa9fa-158">**TableQuery.generateFilterCondition** é um método de programa auxiliar toocreate filtros para consultas.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="fa9fa-159">Chamar **onde** numa referência de Olá devolvida pelo Olá **TableQuery.from** consulta de toohello do método tooapply Olá filtro.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="fa9fa-160">Quando Olá é executar a consulta com uma chamada demasiado**executar** no Olá **CloudTable** objeto devolve um **Iterator** com Olá **CustomerEntity**especificado do tipo de resultado.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="fa9fa-161">Em seguida, pode utilizar Olá **Iterator** devolvida uma para cada ciclo tooconsume Olá obter os resultados.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="fa9fa-162">Este código imprime os campos de Olá de cada entidade na consola de toohello de resultados de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="fa9fa-163">Como: obter um intervalo de entidades numa partição</span><span class="sxs-lookup"><span data-stu-id="fa9fa-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="fa9fa-164">Se não quiser tooquery todas as entidades de Olá numa partição, pode especificar um intervalo através da utilização de operadores de comparação num filtro.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="fa9fa-165">Olá seguir combina código dois filtros tooget todas as entidades numa partição "Santos" em que a chave de linha de Olá (nome próprio) começa com uma letra segurança too'E' no Olá por letras do alfabeto.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="fa9fa-166">Em seguida, imprime os resultados da consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-166">Then it prints hello query results.</span></span> <span data-ttu-id="fa9fa-167">Se utilizar a tabela de toohello adicionado Olá entidades no batch Olá inserir a secção deste guia, apenas duas entidades são devolvidas desta vez (Bernardo e Denise Santos); Jorge Santos não está incluído.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="fa9fa-168">Como: obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="fa9fa-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="fa9fa-169">Pode escrever uma consulta tooretrieve uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="fa9fa-170">chamadas de código seguinte Olá **TableOperation.retrieve** com partição linha de chave e os parâmetros de chave toospecify Olá cliente "Jorge Santos", em vez de criar um **TableQuery** e utilizar Olá toodo de filtros mesma coisa.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="fa9fa-171">Quando executada, Olá obter operação devolve apenas uma entidade em vez de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="fa9fa-172">Olá **getResultAsType** método casts tipo toohello de resultado de Olá do destino da atribuição de Olá, um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="fa9fa-173">Se este tipo não é compatível com o tipo de Olá especificado para a consulta de Olá, será emitida uma exceção.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="fa9fa-174">Se nenhuma entidade tem uma partição exata e a chave de linha corresponder, é devolvido um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="fa9fa-175">A especificação de chaves de partição e da fila numa consulta é Olá tooretrieve da forma mais rápida do serviço de tabela Olá, uma única entidade.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

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

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="fa9fa-176">Como: modificar uma entidade</span><span class="sxs-lookup"><span data-stu-id="fa9fa-176">How to: Modify an entity</span></span>
<span data-ttu-id="fa9fa-177">toomodify uma entidade, obtê-lo a partir do serviço de tabela Olá, se o objeto de entidade toohello alterações e guardar alterações de Olá toohello back-serviço de tabela com uma operação de substituição ou intercalação.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="fa9fa-178">Olá código seguinte altera o número de telefone de um cliente existente.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="fa9fa-179">Em vez de chamar **TableOperation.insert** , como fizemos tooinsert, este código chama **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="fa9fa-180">Olá **Cloudtable** método chama o serviço de tabela Olá e entidade Olá é substituída, a menos que outra aplicação alterado-la no tempo de Olá, uma vez que esta aplicação obtido.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="fa9fa-181">Quando isso acontece, é emitida uma exceção e a entidade Olá tem de ter obtida, modificar e guardar novamente.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="fa9fa-182">Neste padrão de repetição de simultaneidade otimista é comum num sistema de armazenamento distribuído.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

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

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="fa9fa-183">Como: consultar um subconjunto de propriedades de entidade</span><span class="sxs-lookup"><span data-stu-id="fa9fa-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="fa9fa-184">Uma tabela de tooa de consulta pode obter apenas algumas propriedades de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="fa9fa-185">Esta técnica, denominada projeção, reduz a largura de banda e pode melhorar o desempenho da consulta, especialmente para entidades grandes.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="fa9fa-186">Olá consulta Olá seguinte código utiliza Olá **selecione** método tooreturn apenas Olá endereços de e-mail de entidades na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="fa9fa-187">Olá os resultados são projetados para uma coleção de **cadeia** com a ajuda de Olá de um **EntityResolver**, que does Olá conversão do tipo entidades Olá devolvido do servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="fa9fa-188">Pode saber mais sobre a projeção na [tabelas do Azure: Upsert e da projeção da consulta][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="fa9fa-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="fa9fa-189">Tenha em atenção que projeção não é suportada no emulador de armazenamento local Olá, pelo que este código é executado apenas quando utilizar uma conta de serviço de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

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

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="fa9fa-190">Como: inserir ou substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="fa9fa-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="fa9fa-191">Muitas vezes, pretende tooadd uma tabela de tooa entidade sem saberem se já existir na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="fa9fa-192">Uma operação de inserção ou substituir permite-lhe toomake único pedido que irá inserir a entidade de Olá se não existir ou substitua Olá existente um caso.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="fa9fa-193">Criar nos exemplos anteriores, hello seguinte código insere ou substitui entidade Olá para "Walter Harp".</span><span class="sxs-lookup"><span data-stu-id="fa9fa-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="fa9fa-194">Depois de criar uma nova entidade, este código chama Olá **TableOperation.insertOrReplace** método.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="fa9fa-195">Este código, em seguida, chama **executar** no Olá **CloudTable** objeto com a inserção de tabela e Olá Olá ou operação de tabela como parâmetros de Olá de substituição.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="fa9fa-196">tooupdate só fazem parte de uma entidade Olá **TableOperation.insertOrMerge** método pode ser utilizado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="fa9fa-197">Tenha em atenção que inserir ou substituir não é suportada no emulador de armazenamento local Olá, pelo que este código é executado apenas quando utilizar uma conta de serviço de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="fa9fa-198">Pode saber mais sobre inserir ou substituir e a inserção ou intercalação deste [tabelas do Azure: Upsert e da projeção da consulta][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="fa9fa-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

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

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="fa9fa-199">Como: eliminar uma entidade</span><span class="sxs-lookup"><span data-stu-id="fa9fa-199">How to: Delete an entity</span></span>
<span data-ttu-id="fa9fa-200">Pode facilmente eliminar uma entidade depois de a ter obtido.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="fa9fa-201">Assim que a entidade de Olá é obtida, chamar **TableOperation.delete** com Olá toodelete de entidade.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="fa9fa-202">Em seguida, chame **executar** no Olá **CloudTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="fa9fa-203">Olá seguinte código obtém e elimina uma entidade de cliente.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-203">hello following code retrieves and deletes a customer entity.</span></span>

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

## <a name="how-to-delete-a-table"></a><span data-ttu-id="fa9fa-204">Como: eliminar uma tabela</span><span class="sxs-lookup"><span data-stu-id="fa9fa-204">How to: Delete a table</span></span>
<span data-ttu-id="fa9fa-205">Por fim, hello seguinte código elimina uma tabela a partir de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="fa9fa-206">Uma tabela que foi eliminada estará indisponível toobe recriada durante um período de tempo após a eliminação de Olá, normalmente, menos de forty segundos.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fa9fa-207">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fa9fa-207">Next steps</span></span>

* <span data-ttu-id="fa9fa-208">[Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="fa9fa-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="fa9fa-209">[Armazenamento do Azure SDK para Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="fa9fa-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="fa9fa-210">[Referência do SDK de cliente de armazenamento do Azure][referência do SDK do Azure armazenamento cliente]</span><span class="sxs-lookup"><span data-stu-id="fa9fa-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="fa9fa-211">[API REST do Storage do Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="fa9fa-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="fa9fa-212">[Blogue da equipa do Storage do Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="fa9fa-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="fa9fa-213">Para obter mais informações, consulte também Olá [Centro de programadores Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="fa9fa-213">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência do SDK do Azure armazenamento cliente]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
