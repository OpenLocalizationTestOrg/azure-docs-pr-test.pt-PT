---
title: "aaaGet começar a utilizar o table storage e o Visual Studio serviços ligados (Serviços de cloud) | Microsoft Docs"
description: "Como tooget iniciado utilizando o Table storage do Azure num projeto de serviço em nuvem no Visual Studio depois de ligar tooa conta de armazenamento com o Visual Studio ligada a serviços"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: efb16953e05764cb162cbdae4d0eab57f781682d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="18c17-103">Introdução ao table storage do Azure e o Visual Studio ligado serviços (projetos de serviços de nuvem)</span><span class="sxs-lookup"><span data-stu-id="18c17-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="18c17-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="18c17-104">Overview</span></span>
<span data-ttu-id="18c17-105">Este artigo descreve como tooget iniciado utilizando o table storage do Azure no Visual Studio depois de ter criado ou referenciada uma conta de armazenamento do Azure num projeto de serviços em nuvem utilizando Olá Visual Studio **adicionar serviços ligados** caixa de diálogo .</span><span class="sxs-lookup"><span data-stu-id="18c17-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="18c17-106">Olá **adicionar serviços ligados** operação instala tooaccess de pacotes de NuGet adequado do Olá storage do Azure no seu projeto e adiciona a cadeia de ligação de Olá para hello armazenamento conta tooyour ficheiros de configuração do projeto.</span><span class="sxs-lookup"><span data-stu-id="18c17-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="18c17-107">Olá serviço de armazenamento de tabelas do Azure permite-lhe toostore grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="18c17-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="18c17-108">o serviço de Olá é um arquivo de dados NoSQL que aceita chamadas autenticadas de dentro e fora Olá em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="18c17-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="18c17-109">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="18c17-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="18c17-110">tooget iniciado, terá primeiro toocreate uma tabela na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="18c17-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="18c17-111">Vamos mostrar-lhe como toocreate um Azure uma tabela no código, e também como tabela básico tooperform e operações de entidade, tais como adicionar, modificar, ler e ao ler a tabela entidades.</span><span class="sxs-lookup"><span data-stu-id="18c17-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="18c17-112">Exemplos de Olá são escritos no C\# código e utilizar Olá [biblioteca de clientes de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="18c17-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="18c17-113">**Nota:** algumas das Olá APIs que efetuar chamadas o tooAzure storage são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="18c17-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="18c17-114">Consulte [programação assíncrona com Async-Await](http://msdn.microsoft.com/library/hh191443.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="18c17-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="18c17-115">código de Olá abaixo parte do princípio de métodos de programação assíncrona estão a ser utilizados.</span><span class="sxs-lookup"><span data-stu-id="18c17-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="18c17-116">Consulte [introdução ao Table storage do Azure através do .NET](storage-dotnet-how-to-use-tables.md) para obter mais informações sobre manipular programaticamente tabelas.</span><span class="sxs-lookup"><span data-stu-id="18c17-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="18c17-117">Consulte [documentação do Storage](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="18c17-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="18c17-118">Consulte [documentação dos serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="18c17-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="18c17-119">Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre a programação de aplicações do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="18c17-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="18c17-120">Tabelas de acesso no código</span><span class="sxs-lookup"><span data-stu-id="18c17-120">Access tables in code</span></span>
<span data-ttu-id="18c17-121">tabelas tooaccess projetos do serviço em nuvem, terá de Olá tooinclude os seguintes itens tooany c# os ficheiros de origem que acedem ao table storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="18c17-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="18c17-122">Certifique-se de declarações de espaço de nomes de Olá, Olá parte superior do ficheiro de Olá c# incluem estes **utilizando** instruções.</span><span class="sxs-lookup"><span data-stu-id="18c17-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="18c17-123">Obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="18c17-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="18c17-124">Utilize Olá seguintes código tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação de configuração de serviço do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="18c17-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="18c17-125">Utilize todas Olá acima código à frente do código Olá Olá exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="18c17-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="18c17-126">Obter um **CloudTableClient** objetos de tabela de Olá tooreference na sua conta de armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="18c17-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="18c17-127">Obter um **CloudTable** objeto tooreference uma tabela específica e entidades de referência.</span><span class="sxs-lookup"><span data-stu-id="18c17-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="18c17-128">Criar uma tabela no código</span><span class="sxs-lookup"><span data-stu-id="18c17-128">Create a table in code</span></span>
<span data-ttu-id="18c17-129">Olá toocreate tabela do Azure, basta adicionar uma chamada demasiado**CreateIfNotExistsAsync** toohello depois um **CloudTable** conforme descrito na secção de "Acesso as tabelas no código" Olá de objeto.</span><span class="sxs-lookup"><span data-stu-id="18c17-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="18c17-130">Adicionar uma tabela de tooa entidade</span><span class="sxs-lookup"><span data-stu-id="18c17-130">Add an entity tooa table</span></span>
<span data-ttu-id="18c17-131">tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de Olá de entidade.</span><span class="sxs-lookup"><span data-stu-id="18c17-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="18c17-132">Olá código seguinte define uma classe de entidade chamada **CustomerEntity** que utiliza Olá nome do próprio do cliente como chave de linha de Olá e apelido Olá como chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="18c17-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }

        public string PhoneNumber { get; set; }
    }

<span data-ttu-id="18c17-133">Operações da tabela que envolvem entidades são efetuadas utilizando Olá **CloudTable** objeto que criou anteriormente no "Tabelas de acesso no código."</span><span class="sxs-lookup"><span data-stu-id="18c17-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="18c17-134">Olá **TableOperation** objeto representa Olá operação toobe concluído.</span><span class="sxs-lookup"><span data-stu-id="18c17-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="18c17-135">Olá seguinte como exemplo de código mostra toocreate um **CloudTable** objeto e um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="18c17-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="18c17-136">operação de Olá tooprepare, um **TableOperation** é criada a entidade de cliente de Olá tooinsert na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="18c17-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="18c17-137">Por fim, a operação de Olá é executada chamando **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="18c17-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="18c17-138">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="18c17-138">Insert a batch of entities</span></span>
<span data-ttu-id="18c17-139">Pode inserir várias entidades numa tabela numa operação de escrita única.</span><span class="sxs-lookup"><span data-stu-id="18c17-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="18c17-140">Olá exemplo de código seguinte cria dois objetos de entidade ("Jorge Santos" e "Bernardo Santos"), adiciona-tooa **TableBatchOperation** de objeto utilizando Olá método Insert e, em seguida, inicia Olá operação chamando  **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="18c17-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

    // Create hello batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a customer entity and add it toohello table.
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";
    customer1.PhoneNumber = "425-555-0104";

    // Create another customer entity and add it toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    customer2.PhoneNumber = "425-555-0102";

    // Add both customer entities toohello batch insert operation.
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);

    // Execute hello batch operation.
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="18c17-141">Obter todas as entidades de Olá numa partição</span><span class="sxs-lookup"><span data-stu-id="18c17-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="18c17-142">tooquery uma tabela para todas as entidades de Olá numa partição, utilize um **TableQuery** objeto.</span><span class="sxs-lookup"><span data-stu-id="18c17-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="18c17-143">Olá exemplo de código seguinte especifica um filtro para entidades em que "Santos" é a chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="18c17-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="18c17-144">Este exemplo imprime os campos de Olá de cada entidade na consola de toohello de resultados de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="18c17-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="18c17-145">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="18c17-145">Get a single entity</span></span>
<span data-ttu-id="18c17-146">Pode escrever uma consulta tooget uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="18c17-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="18c17-147">Olá seguinte código utiliza um **TableOperation** toospecify um cliente "Bernardo Santos" com o nome de objeto.</span><span class="sxs-lookup"><span data-stu-id="18c17-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="18c17-148">Este método devolve apenas uma entidade em vez de uma coleção e Olá devolveu o valor no **Tableresult** é um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="18c17-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="18c17-149">A especificação de chaves de partição e da fila numa consulta é Olá tooretrieve da forma mais rápida uma única entidade de Olá **tabela** serviço.</span><span class="sxs-lookup"><span data-stu-id="18c17-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="18c17-150">Eliminar uma entidade</span><span class="sxs-lookup"><span data-stu-id="18c17-150">Delete an entity</span></span>
<span data-ttu-id="18c17-151">Pode eliminar uma entidade depois de encontrá-lo.</span><span class="sxs-lookup"><span data-stu-id="18c17-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="18c17-152">Olá seguinte código procura uma entidade de cliente "Bernardo Santos" com o nome, e se encontrá-lo, elimina-a.</span><span class="sxs-lookup"><span data-stu-id="18c17-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="18c17-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="18c17-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

