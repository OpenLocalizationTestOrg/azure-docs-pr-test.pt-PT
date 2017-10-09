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
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introdução ao table storage do Azure e o Visual Studio ligado serviços (projetos de serviços de nuvem)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Descrição geral
Este artigo descreve como tooget iniciado utilizando o table storage do Azure no Visual Studio depois de ter criado ou referenciada uma conta de armazenamento do Azure num projeto de serviços em nuvem utilizando Olá Visual Studio **adicionar serviços ligados** caixa de diálogo . Olá **adicionar serviços ligados** operação instala tooaccess de pacotes de NuGet adequado do Olá storage do Azure no seu projeto e adiciona a cadeia de ligação de Olá para hello armazenamento conta tooyour ficheiros de configuração do projeto.

Olá serviço de armazenamento de tabelas do Azure permite-lhe toostore grandes quantidades de dados estruturados. o serviço de Olá é um arquivo de dados NoSQL que aceita chamadas autenticadas de dentro e fora Olá em nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.

tooget iniciado, terá primeiro toocreate uma tabela na sua conta de armazenamento. Vamos mostrar-lhe como toocreate um Azure uma tabela no código, e também como tabela básico tooperform e operações de entidade, tais como adicionar, modificar, ler e ao ler a tabela entidades. Exemplos de Olá são escritos no C\# código e utilizar Olá [biblioteca de clientes de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

**Nota:** algumas das Olá APIs que efetuar chamadas o tooAzure storage são assíncronas. Consulte [programação assíncrona com Async-Await](http://msdn.microsoft.com/library/hh191443.aspx) para obter mais informações. código de Olá abaixo parte do princípio de métodos de programação assíncrona estão a ser utilizados.

* Consulte [introdução ao Table storage do Azure através do .NET](storage-dotnet-how-to-use-tables.md) para obter mais informações sobre manipular programaticamente tabelas.
* Consulte [documentação do Storage](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o Storage do Azure.
* Consulte [documentação dos serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços em nuvem do Azure.
* Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre a programação de aplicações do ASP.NET.

## <a name="access-tables-in-code"></a>Tabelas de acesso no código
tabelas tooaccess projetos do serviço em nuvem, terá de Olá tooinclude os seguintes itens tooany c# os ficheiros de origem que acedem ao table storage do Azure.

1. Certifique-se de declarações de espaço de nomes de Olá, Olá parte superior do ficheiro de Olá c# incluem estes **utilizando** instruções.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Utilize Olá seguintes código tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação de configuração de serviço do Azure Olá.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > Utilize todas Olá acima código à frente do código Olá Olá exemplos a seguir.
   > 
   > 
3. Obter um **CloudTableClient** objetos de tabela de Olá tooreference na sua conta de armazenamento de objeto.
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Obter um **CloudTable** objeto tooreference uma tabela específica e entidades de referência.
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Criar uma tabela no código
Olá toocreate tabela do Azure, basta adicionar uma chamada demasiado**CreateIfNotExistsAsync** toohello depois um **CloudTable** conforme descrito na secção de "Acesso as tabelas no código" Olá de objeto.

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de tooa entidade
tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de Olá de entidade. Olá código seguinte define uma classe de entidade chamada **CustomerEntity** que utiliza Olá nome do próprio do cliente como chave de linha de Olá e apelido Olá como chave de partição Olá.

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

Operações da tabela que envolvem entidades são efetuadas utilizando Olá **CloudTable** objeto que criou anteriormente no "Tabelas de acesso no código." Olá **TableOperation** objeto representa Olá operação toobe concluído. Olá seguinte como exemplo de código mostra toocreate um **CloudTable** objeto e um **CustomerEntity** objeto. operação de Olá tooprepare, um **TableOperation** é criada a entidade de cliente de Olá tooinsert na tabela de Olá. Por fim, a operação de Olá é executada chamando **CloudTable.ExecuteAsync**.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a>Inserir um lote de entidades
Pode inserir várias entidades numa tabela numa operação de escrita única. Olá exemplo de código seguinte cria dois objetos de entidade ("Jorge Santos" e "Bernardo Santos"), adiciona-tooa **TableBatchOperation** de objeto utilizando Olá método Insert e, em seguida, inicia Olá operação chamando  **CloudTable.ExecuteBatchAsync**.

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

## <a name="get-all-of-hello-entities-in-a-partition"></a>Obter todas as entidades de Olá numa partição
tooquery uma tabela para todas as entidades de Olá numa partição, utilize um **TableQuery** objeto. Olá exemplo de código seguinte especifica um filtro para entidades em que "Santos" é a chave de partição Olá. Este exemplo imprime os campos de Olá de cada entidade na consola de toohello de resultados de consulta Olá.

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


## <a name="get-a-single-entity"></a>Obter uma única entidade
Pode escrever uma consulta tooget uma entidade única e específica. Olá seguinte código utiliza um **TableOperation** toospecify um cliente "Bernardo Santos" com o nome de objeto. Este método devolve apenas uma entidade em vez de uma coleção e Olá devolveu o valor no **Tableresult** é um **CustomerEntity** objeto. A especificação de chaves de partição e da fila numa consulta é Olá tooretrieve da forma mais rápida uma única entidade de Olá **tabela** serviço.

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>Eliminar uma entidade
Pode eliminar uma entidade depois de encontrá-lo. Olá seguinte código procura uma entidade de cliente "Bernardo Santos" com o nome, e se encontrá-lo, elimina-a.

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

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

