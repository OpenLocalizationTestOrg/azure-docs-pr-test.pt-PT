---
title: "Azure Cosmos DB enlaces de funções"
description: "Compreenda como utilizar o Azure Cosmos DB acionadores e enlaces das funções do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "das funções do Azure, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.service: functions; cosmos-db
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/21/2017
ms.author: glenga
ms.openlocfilehash: ab55281b6adcc8867f207e6887c88a26c1a8616b
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/19/2018
---
# <a name="azure-cosmos-db-bindings-for-azure-functions"></a>Enlaces de Cosmos BD do Azure para as funções do Azure

Este artigo explica como trabalhar com [Azure Cosmos DB](..\cosmos-db\serverless-computing-database.md) enlaces de funções do Azure. Funções do Azure suporta acionam, de entrada e saída enlaces para Azure Cosmos DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="trigger"></a>Acionador

O acionador de base de dados do Azure Cosmos utiliza o [Azure Cosmos DB alteração Feed](../cosmos-db/change-feed.md) para escutar alterações de em partições. O feed de alteração publica inserções e atualizações, eliminações não. 

## <a name="trigger---example"></a>Acionador - exemplo

Veja o exemplo de específicas do idioma:

* [C#](#trigger---c-example)
* [Script do c# (.csx)](#trigger---c-script-example)
* [JavaScript](#trigger---javascript-example)

### <a name="trigger---c-example"></a>Acionador - c# exemplo

O seguinte exemplo mostra um [c# função](functions-dotnet-class-library.md) que aciona a partir de uma base de dados específica e a coleção.

```cs
    using System.Collections.Generic;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;

    [FunctionName("DocumentUpdates")]
    public static void Run(
        [CosmosDBTrigger("database", "collection", ConnectionStringSetting = "myCosmosDB")]
    IReadOnlyList<Document> documents,
        TraceWriter log)
    {
            log.Info("Documents modified " + documents.Count);
            log.Info("First document Id " + documents[0].Id);
    }
```

### <a name="trigger---c-script-example"></a>Acionador - exemplo de script do c#

O exemplo seguinte mostra um acionador de base de dados do Cosmos enlace num *function.json* ficheiro e uma [função de script do c#](functions-reference-csharp.md) que utiliza o enlace. A função escreve mensagens de registo quando são modificados registos da base de dados do Cosmos.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "type": "cosmosDBTrigger",
    "name": "documents",
    "direction": "in",
    "leaseCollectionName": "leases",
    "connectionStringSetting": "<connection-app-setting>",
    "databaseName": "Tasks",
    "collectionName": "Items",
    "createLeaseCollectionIfNotExists": true
}
```

Eis o código de script do c#:
 
```cs 
    #r "Microsoft.Azure.Documents.Client"
    
    using System;
    using Microsoft.Azure.Documents;
    using System.Collections.Generic;
    

    public static void Run(IReadOnlyList<Document> documents, TraceWriter log)
    {
      log.Verbose("Documents modified " + documents.Count);
      log.Verbose("First document Id " + documents[0].Id);
    }
```

### <a name="trigger---javascript-example"></a>Acionador - exemplo de JavaScript

O exemplo seguinte mostra um acionador de base de dados do Cosmos enlace num *function.json* ficheiro e uma [JavaScript função](functions-reference-node.md) que utiliza o enlace. A função escreve mensagens de registo quando são modificados registos da base de dados do Cosmos.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "type": "cosmosDBTrigger",
    "name": "documents",
    "direction": "in",
    "leaseCollectionName": "leases",
    "connectionStringSetting": "<connection-app-setting>",
    "databaseName": "Tasks",
    "collectionName": "Items",
    "createLeaseCollectionIfNotExists": true
}
```

Eis o código JavaScript:

```javascript
    module.exports = function (context, documents) {
      context.log('First document Id modified : ', documents[0].id);

      context.done();
    }
```

## <a name="trigger---attributes"></a>Acionador - atributos

No [bibliotecas de classes do c#](functions-dotnet-class-library.md), utilize o [CosmosDBTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/Trigger/CosmosDBTriggerAttribute.cs) atributo, que está definido no pacote NuGet [Microsoft.Azure.WebJobs.Extensions.DocumentDB](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB).

O construtor do atributo tem o nome de base de dados e o nome da coleção. Para obter informações sobre essas definições e outras propriedades que pode configurar, consulte [acionador - configuração](#trigger---configuration). Eis um `CosmosDBTrigger` exemplo de atributo na assinatura do método:

```csharp
    [FunctionName("DocumentUpdates")]
    public static void Run(
        [CosmosDBTrigger("database", "collection", ConnectionStringSetting = "myCosmosDB")]
    IReadOnlyList<Document> documents,
        TraceWriter log)
    {
        ...
    }
```

Para obter um exemplo completado, consulte [acionador - c# exemplo](#trigger---c-example).

## <a name="trigger---configuration"></a>Acionador - configuração

A tabela seguinte explica as propriedades de configuração de enlace que definir no *function.json* ficheiros e o `CosmosDBTrigger` atributo.

|propriedade de Function.JSON | Propriedade de atributo |Descrição|
|---------|---------|----------------------|
|**type** || tem de ser definido como `cosmosDBTrigger`. |
|**direction** || tem de ser definido como `in`. Este parâmetro é definido automaticamente quando criar o acionador no portal do Azure. |
|**name** || O nome da variável utilizado no código de função que representa a lista de documentos com as alterações. | 
|**connectionStringSetting**|**ConnectionStringSetting** | O nome de uma definição de aplicação que contém a cadeia de ligação utilizada para ligar à conta de base de dados do Azure Cosmos a ser monitorizada. |
|**databaseName**|**DatabaseName**  | O nome da base de dados do Azure Cosmos DB com a coleção que está a ser monitorizada. |
|**collectionName** |**CollectionName** | O nome da coleção que está a ser monitorizado. |
|**leaseConnectionStringSetting** | **LeaseConnectionStringSetting** | (Opcional) O nome de uma definição de aplicação que contenha a cadeia de ligação ao serviço que contém a coleção de concessão. Quando não definido, o `connectionStringSetting` valor é utilizado. Este parâmetro é automaticamente definido quando o enlace é criado no portal. A cadeia de ligação para a coleção de concessões tem de ter permissões de escrita.|
|**leaseDatabaseName** |**LeaseDatabaseName** | (Opcional) O nome da base de dados que contém a coleção utilizada para armazenar concessões. Quando não definido, o valor da `databaseName` definição é utilizada. Este parâmetro é automaticamente definido quando o enlace é criado no portal. |
|**leaseCollectionName** | **LeaseCollectionName** | (Opcional) O nome da coleção utilizado para armazenar concessões. Quando não definido, o valor `leases` é utilizado. |
|**createLeaseCollectionIfNotExists** | **CreateLeaseCollectionIfNotExists** | (Opcional) Quando definido como `true`, a coleção de concessões é criada automaticamente quando já não existir. O valor predefinido é `false`. |
|**leasesCollectionThroughput**| **LeasesCollectionThroughput**| (Opcional) Define a quantidade de unidades de pedido para atribuir quando é criada a coleção de concessões. Esta definição é apenas utilizado quando `createLeaseCollectionIfNotExists` está definido como `true`. Este parâmetro é automaticamente definido quando o enlace é criado utilizando o portal.
| |**LeaseOptions** | Configurar opções de concessão definindo as propriedades numa instância do [ChangeFeedHostOptions](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.changefeedprocessor.changefeedhostoptions) classe.

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---usage"></a>Acionador - utilização

O acionador requer uma segunda coleção, que utiliza para armazenar _concessões_ através de partições. A coleção que está a ser monitorizado e a coleção que contém os concessões tem de estar disponíveis para acionar a funcionar.

 >[!IMPORTANT]
 > Se várias funções estão configuradas para utilizar um acionador de base de dados do Cosmos para a mesma coleção, cada uma das funções deve utilizar uma coleção de concessão dedicado. Caso contrário, será acionada apenas uma das funções. 

O acionador não indica se um documento foi atualizado ou inserir, fornece apenas o documento de si próprio. Se precisar de lidar com as atualizações e inserções de forma diferente, pode fazê-lo implementando timestamp campos para inserção ou atualização.

## <a name="input"></a>Input

O enlace de entrada de base de dados do Azure Cosmos obtém um ou mais documentos de base de dados do Azure Cosmos e transmite-os para o parâmetro de entrada da função. Os parâmetros de consulta ou ID do documento podem ser determinados com base no acionador que invoca a função. 

>[!NOTE]
> Não utilize a base de dados do Azure Cosmos entrada ou saída enlaces se estiver a utilizar a API do MongoDB numa conta de base de dados do Cosmos. É possível danos nos dados.

## <a name="input---example-1"></a>Entrada - exemplo 1

Veja o exemplo de específicas do idioma que lê um único documento:

* [C#](#input---c-example)
* [Script do c# (.csx)](#input---c-script-example)
* [F#](#input---f-example)
* [JavaScript](#input---javascript-example)

### <a name="input---c-example"></a>Entrada - c# exemplo

O seguinte exemplo mostra um [c# função](functions-dotnet-class-library.md) que obtém um único documento a partir de uma base de dados específica e a coleção. 

Primeiro, `Id` e `Maker` valores para um `CarReview` instância são transferidos para uma fila. A BD do Cosmos enlace utiliza `Id` e `Maker` da mensagem de fila para obter o documento da base de dados.

```cs
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;

    namespace CosmosDB
    {
        public static class SingleEntry
        {
            [FunctionName("SingleEntry")]
            public static void Run(
                [QueueTrigger("car-reviews", Connection = "StorageConnectionString")] CarReview carReview,
                [DocumentDB("cars", "car-reviews", PartitionKey = "{maker}", Id= "{id}", ConnectionStringSetting = "CarReviewsConnectionString")] CarReview document,
                TraceWriter log)
            {
                log.Info( $"Selected Review - {document?.Review}"); 
            }
        }
    }
```

Eis o `CarReview` POCO:

 ```cs
    public class CarReview
    {
        public string Id { get; set; }
        public string Maker { get; set; }
        public string Description { get; set; }
        public string Model { get; set; }
        public string Image { get; set; }
        public string Review { get; set; }
    }
 ```

### <a name="input---c-script-example"></a>Entrada - exemplo de script do c#

O exemplo seguinte mostra um enlace de entrada do Cosmos DB num *function.json* ficheiro e uma [função de script do c#](functions-reference-csharp.md) que utiliza o enlace. A função lê um único documento e atualiza o valor de texto do documento.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "name": "inputDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger}",
    "partitionKey": "{partition key value}",
    "connection": "MyAccount_COSMOSDB",     
    "direction": "in"
}
```
O [configuração](#input---configuration) secção explica estas propriedades.

Eis o código de script do c#:

```cs
    using System;

    // Change input document contents using Azure Cosmos DB input binding 
    public static void Run(string myQueueItem, dynamic inputDocument)
    {   
      inputDocument.text = "This has changed.";
    }
```

<a name="infsharp"></a>

### <a name="input---f-example"></a>Entrada - F # exemplo

O exemplo seguinte mostra um enlace de entrada do Cosmos DB num *function.json* ficheiro e uma [F # função](functions-reference-fsharp.md) que utiliza o enlace. A função lê um único documento e atualiza o valor de texto do documento.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "name": "inputDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger}",
    "connection": "MyAccount_COSMOSDB",     
    "direction": "in"
}
```

O [configuração](#input---configuration) secção explica estas propriedades.

Eis o código F #:

```fsharp
    (* Change input document contents using Azure Cosmos DB input binding *)
    open FSharp.Interop.Dynamic
    let Run(myQueueItem: string, inputDocument: obj) =
    inputDocument?text <- "This has changed."
```

Este exemplo requer um `project.json` ficheiro que especifica o `FSharp.Interop.Dynamic` e `Dynamitey` NuGet dependências:

```json
{
    "frameworks": {
        "net46": {
            "dependencies": {
                "Dynamitey": "1.0.2",
                "FSharp.Interop.Dynamic": "3.0.0"
            }
        }
    }
}
```

Para adicionar um `project.json` de ficheiros, consulte [gestão de pacotes F #](functions-reference-fsharp.md#package).

### <a name="input---javascript-example"></a>Entrada - exemplo de JavaScript

O exemplo seguinte mostra um enlace de entrada do Cosmos DB num *function.json* ficheiro e uma [JavaScript função](functions-reference-node.md) que utiliza o enlace. A função lê um único documento e atualiza o valor de texto do documento.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "name": "inputDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger_payload_property}",
    "partitionKey": "{queueTrigger_payload_property}",
    "connection": "MyAccount_COSMOSDB",     
    "direction": "in"
}
```
O [configuração](#input---configuration) secção explica estas propriedades.

Eis o código JavaScript:

```javascript
    // Change input document contents using Azure Cosmos DB input binding, using context.bindings.inputDocumentOut
    module.exports = function (context) {   
    context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
    context.bindings.inputDocumentOut.text = "This was updated!";
    context.done();
    };
```

## <a name="input---example-2"></a>Entrada - exemplo 2

Veja o exemplo de específicas do idioma que lê vários documentos:

* [C#](#input---c-example-2)
* [Script do c# (.csx)](#input---c-script-example-2)
* [JavaScript](#input---javascript-example-2)

### <a name="input---c-example-2"></a>Entrada - c# exemplo 2

O seguinte exemplo mostra um [c# função](functions-dotnet-class-library.md) que executa uma consulta SQL. Para utilizar o `SqlQuery` parâmetro, tem de instalar a versão mais recente do beta do `Microsoft.Azure.WebJobs.Extensions.DocumentDB` pacote NuGet.

```csharp
    using System.Net;
    using System.Net.Http;
    using System.Collections.Generic;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Extensions.Http;

    [FunctionName("CosmosDBSample")]
    public static HttpResponseMessage Run(
        [HttpTrigger(AuthorizationLevel.Anonymous, "get")] HttpRequestMessage req,
        [DocumentDB("test", "test", ConnectionStringSetting = "CosmosDB", SqlQuery = "SELECT top 2 * FROM c order by c._ts desc")] IEnumerable<object> documents)
    {
        return req.CreateResponse(HttpStatusCode.OK, documents);
    }
```

### <a name="input---c-script-example-2"></a>Entrada - c# exemplo de script 2

O exemplo seguinte mostra um enlace de entrada da base de dados do Azure Cosmos num *function.json* ficheiro e uma [função de script do c#](functions-reference-csharp.md) que utiliza o enlace. A função obtém vários documentos especificados por uma consulta de SQL Server, com um acionador de fila para personalizar os parâmetros de consulta.

O acionador de filas fornece um parâmetro `departmentId`. Uma mensagem de fila de `{ "departmentId" : "Finance" }` iria devolver todos os registos para o departamento financeiro. 

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
    "connection": "CosmosDBConnection"
}
```

O [configuração](#input---configuration) secção explica estas propriedades.

Eis o código de script do c#:

```csharp
    public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
    {   
        foreach (var doc in documents)
        {
            // operate on each document
        }    
    }

    public class QueuePayload
    {
        public string departmentId { get; set; }
    }
```

### <a name="input---javascript-example-2"></a>Entrada - JavaScript exemplo 2

O exemplo seguinte mostra um enlace de entrada da base de dados do Azure Cosmos num *function.json* ficheiro e uma [JavaScript função](functions-reference-node.md) que utiliza o enlace. A função obtém vários documentos especificados por uma consulta de SQL Server, com um acionador de fila para personalizar os parâmetros de consulta.

O acionador de filas fornece um parâmetro `departmentId`. Uma mensagem de fila de `{ "departmentId" : "Finance" }` iria devolver todos os registos para o departamento financeiro. 

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
    "connection": "CosmosDBConnection"
}
```

O [configuração](#input---configuration) secção explica estas propriedades.

Eis o código JavaScript:

```javascript
    module.exports = function (context, input) {    
        var documents = context.bindings.documents;
        for (var i = 0; i < documents.length; i++) {
            var document = documents[i];
            // operate on each document
        }       
        context.done();
    };
```

## <a name="input---attributes"></a>Entrada - atributos

No [bibliotecas de classes do c#](functions-dotnet-class-library.md), utilize o [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) atributo, que está definido no pacote NuGet [Microsoft.Azure.WebJobs.Extensions.DocumentDB](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB).

O construtor do atributo tem o nome de base de dados e o nome da coleção. Para obter informações sobre essas definições e outras propriedades que pode configurar, consulte [a secção de configuração seguintes](#input---configuration). 

## <a name="input---configuration"></a>Entrada - configuração

A tabela seguinte explica as propriedades de configuração de enlace que definir no *function.json* ficheiros e o `DocumentDB` atributo.

|propriedade de Function.JSON | Propriedade de atributo |Descrição|
|---------|---------|----------------------|
|**type**     || tem de ser definido como `documentdb`.        |
|**direction**     || tem de ser definido como `in`.         |
|**name**     || Nome do parâmetro de enlace que representa o documento na função.  |
|**databaseName** |**DatabaseName** |A base de dados que contém o documento.        |
|**collectionName** |**CollectionName** | O nome da coleção que contém o documento. |
|**id**    | **Id** | O ID do documento para obter. Esta propriedade suporta parâmetros de enlaces. Para obter mais informações, consulte [vincular a propriedades personalizadas de entrada numa expressão de enlace](functions-triggers-bindings.md#bind-to-custom-input-properties). Não definir ambos os **id** e **sqlQuery** propriedades. Se não definir uma, é obtida a coleção completa. |
|**sqlQuery**  |**SqlQuery**  | Uma consulta de base de dados SQL do Azure Cosmos utilizada para obter vários documentos. A propriedade suporta os enlaces de tempo de execução, tal como neste exemplo: `SELECT * FROM c where c.departmentId = {departmentId}`. Não definir ambos os **id** e **sqlQuery** propriedades. Se não definir uma, é obtida a coleção completa.|
|**connection**     |**ConnectionStringSetting**|O nome da definição de aplicação que contém a cadeia de ligação de base de dados do Azure Cosmos.        |
|**partitionKey**|**PartitionKey**|Especifica o valor de chave de partição para a pesquisa. Pode incluir parâmetros de enlace.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="input---usage"></a>Entrada - utilização

Em c# e F # funções, quando a função sai com sucesso, quaisquer alterações efetuadas para o documento de entrada através dos parâmetros de entrada com nome são mantidas automaticamente. 

Nas funções de JavaScript, as atualizações não são efetuadas automaticamente após a saída da função. Em alternativa, utilize `context.bindings.<documentName>In` e `context.bindings.<documentName>Out` para disponibilizar atualizações. Consulte o [JavaScript exemplo](#input---javascript-example).

## <a name="output"></a>Saída

A saída de base de dados do Azure Cosmos enlace permite escrever um novo documento para uma base de dados do Azure Cosmos DB. 

>[!NOTE]
> Não utilize a base de dados do Azure Cosmos entrada ou saída enlaces se estiver a utilizar a API do MongoDB numa conta de base de dados do Cosmos. É possível danos nos dados.

## <a name="output---example"></a>De saída - exemplo

Veja o exemplo de específicas do idioma:

* [C#](#output---c-example)
* [Script do c# (.csx)](#output---c-script-example)
* [F#](#output---f-example)
* [JavaScript](#output---javascript-example)

### <a name="output---c-example"></a>Saída - c# exemplo

O seguinte exemplo mostra um [c# função](functions-dotnet-class-library.md) que adiciona um documento a uma base de dados, com dados fornecidos na mensagem a partir do armazenamento de filas.

```cs
    using System;
    using Microsoft.Azure.WebJobs;

    [FunctionName("QueueToDocDB")]        
    public static void Run(
        [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
        [DocumentDB("ToDoList", "Items", Id = "id", ConnectionStringSetting = "myCosmosDB")] out dynamic document)
    {
        document = new { Text = myQueueItem, id = Guid.NewGuid() };
    }
```

### <a name="output---c-script-example"></a>Saída - exemplo de script do c#

O exemplo seguinte mostra uma saída de base de dados do Azure Cosmos enlace num *function.json* ficheiro e uma [função de script do c#](functions-reference-csharp.md) que utiliza o enlace. A função utiliza um enlace de fila de entrada para uma fila que recebe JSON no seguinte formato:

```json
{
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

A função cria documentos de base de dados do Azure Cosmos no seguinte formato para cada registo:

```json
{
    "id": "John Henry-123456",
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "name": "employeeDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": true,
    "connection": "MyAccount_COSMOSDB",     
    "direction": "out"
}
```

O [configuração](#output---configuration) secção explica estas propriedades.

Eis o código de script do c#:

```cs
    #r "Newtonsoft.Json"

    using Microsoft.Azure.WebJobs.Host;
    using Newtonsoft.Json.Linq;

    public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
    {
      log.Info($"C# Queue trigger function processed: {myQueueItem}");

      dynamic employee = JObject.Parse(myQueueItem);

      employeeDocument = new {
        id = employee.name + "-" + employee.employeeId,
        name = employee.name,
        employeeId = employee.employeeId,
        address = employee.address
      };
    }
```

Para criar vários documentos, é possível vincular ao `ICollector<T>` ou `IAsyncCollector<T>` onde `T` é um dos tipos suportados.

### <a name="output---f-example"></a>Saída - F # exemplo

O exemplo seguinte mostra uma saída de base de dados do Azure Cosmos enlace num *function.json* ficheiro e uma [F # função](functions-reference-fsharp.md) que utiliza o enlace. A função utiliza um enlace de fila de entrada para uma fila que recebe JSON no seguinte formato:

```json
{
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

A função cria documentos de base de dados do Azure Cosmos no seguinte formato para cada registo:

```json
{
    "id": "John Henry-123456",
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "name": "employeeDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": true,
    "connection": "MyAccount_COSMOSDB",     
    "direction": "out"
}
```
O [configuração](#output---configuration) secção explica estas propriedades.

Eis o código F #:

```fsharp
    open FSharp.Interop.Dynamic
    open Newtonsoft.Json

    type Employee = {
      id: string
      name: string
      employeeId: string
      address: string
    }

    let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
      log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
      let employee = JObject.Parse(myQueueItem)
      employeeDocument <-
        { id = sprintf "%s-%s" employee?name employee?employeeId
          name = employee?name
          employeeId = employee?employeeId
          address = employee?address }
```

Este exemplo requer um `project.json` ficheiro que especifica o `FSharp.Interop.Dynamic` e `Dynamitey` NuGet dependências:

```json
{
    "frameworks": {
        "net46": {
          "dependencies": {
            "Dynamitey": "1.0.2",
            "FSharp.Interop.Dynamic": "3.0.0"
           }
        }
    }
}
```

Para adicionar um `project.json` de ficheiros, consulte [gestão de pacotes F #](functions-reference-fsharp.md#package).

### <a name="output---javascript-example"></a>Saída - exemplo de JavaScript

O exemplo seguinte mostra uma saída de base de dados do Azure Cosmos enlace num *function.json* ficheiro e uma [JavaScript função](functions-reference-node.md) que utiliza o enlace. A função utiliza um enlace de fila de entrada para uma fila que recebe JSON no seguinte formato:

```json
{
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

A função cria documentos de base de dados do Azure Cosmos no seguinte formato para cada registo:

```json
{
    "id": "John Henry-123456",
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "name": "employeeDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": true,
    "connection": "MyAccount_COSMOSDB",     
    "direction": "out"
}
```

O [configuração](#output---configuration) secção explica estas propriedades.

Eis o código JavaScript:

```javascript
    module.exports = function (context) {

      context.bindings.employeeDocument = JSON.stringify({ 
        id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
        name: context.bindings.myQueueItem.name,
        employeeId: context.bindings.myQueueItem.employeeId,
        address: context.bindings.myQueueItem.address
      });

      context.done();
    };
```

## <a name="output---attributes"></a>Saída - atributos

No [bibliotecas de classes do c#](functions-dotnet-class-library.md), utilize o [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) atributo, que está definido no pacote NuGet [Microsoft.Azure.WebJobs.Extensions.DocumentDB](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB).

O construtor do atributo tem o nome de base de dados e o nome da coleção. Para obter informações sobre essas definições e outras propriedades que pode configurar, consulte [de saída - configuração](#output---configuration). Eis um `DocumentDB` exemplo de atributo na assinatura do método:

```csharp
    [FunctionName("QueueToDocDB")]        
    public static void Run(
        [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
        [DocumentDB("ToDoList", "Items", Id = "id", ConnectionStringSetting = "myCosmosDB")] out dynamic document)
    {
        ...
    }
```

Para obter um exemplo completado, consulte [resultado - c# exemplo](#output---c-example).

## <a name="output---configuration"></a>De saída - configuração

A tabela seguinte explica as propriedades de configuração de enlace que definir no *function.json* ficheiros e o `DocumentDB` atributo.

|propriedade de Function.JSON | Propriedade de atributo |Descrição|
|---------|---------|----------------------|
|**type**     || tem de ser definido como `documentdb`.        |
|**direction**     || tem de ser definido como `out`.         |
|**name**     || Nome do parâmetro de enlace que representa o documento na função.  |
|**databaseName** | **DatabaseName**|A base de dados que contém a coleção onde o documento é criado.     |
|**collectionName** |**CollectionName**  | O nome da coleção em que o documento é criado. |
|**createIfNotExists**  |**CreateIfNotExists**    | Um valor booleano para indicar se a coleção é criada quando não existe. A predefinição é *falso* porque são criadas novas coleções com débito reservado, que tem custos implicações. Para obter mais informações, veja a [página de preços](https://azure.microsoft.com/pricing/details/documentdb/).  |
|**partitionKey**|**PartitionKey** |Quando `CreateIfNotExists` for VERDADEIRO, define o caminho de chave de partição para a coleção criada.|
|**collectionThroughput**|**CollectionThroughput**| Quando `CreateIfNotExists` for VERDADEIRO, define o [débito](../cosmos-db/set-throughput.md) da coleção criada.|
|**connection**    |**ConnectionStringSetting** |O nome da definição de aplicação que contém a cadeia de ligação de base de dados do Azure Cosmos.        |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a>Saída - utilização

Por predefinição, quando escreve para o parâmetro de saída na sua função, um documento é criado na base de dados. Este documento tem um GUID automaticamente gerado como o ID do documento. Pode especificar o ID do documento do documento de saída, especificando o `id` propriedade no objeto JSON transmitido para o parâmetro de saída. 

> [!Note]  
> Quando especificar o ID de um documento existente, obtém substituído pelo novo documento de saída. 

## <a name="next-steps"></a>Passos Seguintes

> [!div class="nextstepaction"]
> [Ir para um guia de introdução que utiliza um acionador de base de dados do Cosmos](functions-create-cosmos-db-triggered-function.md)

> [!div class="nextstepaction"]
> [Saiba mais sobre a base de dados sem servidor informática com Cosmos DB](..\cosmos-db\serverless-computing-database.md)

> [!div class="nextstepaction"]
> [Saiba mais sobre as funções do Azure acionadores e enlaces](functions-triggers-bindings.md)
