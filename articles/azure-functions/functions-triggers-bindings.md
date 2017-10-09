---
title: "aaaWork com acionadores e enlaces de funções do Azure | Microsoft Docs"
description: "Saiba como toouse aciona e os enlaces de funções do Azure tooconnect os eventos de tooonline de execução de código e os serviços baseados na nuvem."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "funções do azure, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Conceitos de enlaces e acionadores de funções do Azure
As funções do Azure permite-lhe toowrite código na resposta tooevents no Azure e outros serviços, através de *acionadores* e *enlaces*. Este artigo é uma descrição geral conceptual dos acionadores e enlaces para todos os suportados linguagens de programação. As funcionalidades que são comuns tooall enlaces são descritas aqui.

## <a name="overview"></a>Descrição geral

Acionadores e enlaces são uma forma declarativa toodefine como uma função é invocada e os dados que funciona com. A *acionador* define a forma como uma função é invocada. Uma função tem de ter exatamente um acionador. Acionadores associou dados, o que é normalmente payload Olá que acionou a função de Olá. 

Entrada e saída *enlaces* fornecem uma forma declarativa tooconnect toodata de dentro do seu código. Tootriggers semelhante, especificar as cadeias de ligação e outras propriedades na configuração da função. Enlaces são opcionais e uma função pode ter vários de entrada e saída enlaces. 

Utilizar acionadores e enlaces, pode escrever código que é mais genérico e faz a que codifique os detalhes de Olá dos serviços de Olá com a qual interage. Dados provenientes de valores de entrada de serviços simplesmente tornar-se para o seu código de função. serviço de tooanother toooutput data (como criar uma nova linha no Table Storage do Azure), utilize valor de retorno de Olá do método Olá. Ou, se precisar de toooutput vários valores, utilize um objeto de programa auxiliar. Acionadores e enlaces têm um **nome** propriedade, o que é um identificador que utilize o enlace de Olá tooaccess código.

Pode configurar acionadores e enlaces na Olá **integrar** separador no portal do Olá das funções do Azure. Em bastidores Olá, Olá IU modifica um ficheiro chamado *function.json* ficheiro no diretório de função Olá. Pode editar este ficheiro alterando toohello **editor avançada**.

Olá tabela seguinte mostra os acionadores de Olá e enlaces que são suportadas as funções do Azure. 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>Exemplo: acionador de filas e tabela de saída do enlace

Suponha que pretender toowrite um tooAzure linha nova Table Storage sempre que uma nova mensagem é apresentada no armazenamento de filas do Azure. Este cenário pode ser implementado através de uma fila do Azure acionador e uma tabela de saída do enlace. 

Necessita de um acionador de fila Olá seguindo as informações no Olá **integrar** separador:

* nome de Olá da definição de aplicação Olá que contém a cadeia da ligação de conta de armazenamento de Olá para a fila de Olá
* nome da fila Olá
* Olá identificador no seu código tooread Olá do conteúdo da mensagem da fila de Olá, tais como `order`.

toowrite tooAzure Table Storage, utilize um enlace de saída com Olá os detalhes:

* nome de Olá da definição de aplicação Olá que contém a cadeia da ligação de conta de armazenamento de Olá para a tabela de Olá
* nome da tabela Olá
* Identificador de Olá no seu toocreate de código de saída itens ou valor de retorno de Olá da função de Olá.

Enlaces de utilizam as definições de aplicação para Olá de tooenforce de cadeias de ligação melhores práticas que *function.json* não contém segredos do serviço.

Em seguida, utilize identificadores de Olá fornecido toointegrate com armazenamento do Azure no seu código.

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

Eis Olá *function.json* que corresponde toohello precedente código. Tenha em atenção que Olá a mesma configuração pode ser utilizada, independentemente do idioma Olá de implementação da função de Olá.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
tooview e editar Olá conteúdo *function.json* no portal do Azure Olá, clique em Olá **editor avançada** opção no Olá **integrar** separador da sua função.

Para obter mais exemplos de código e detalhes sobre a integração com o Storage do Azure, consulte [acionadores de funções do Azure e vínculos para armazenamento do Azure](functions-bindings-storage.md).

### <a name="binding-direction"></a>Direção de enlace

Todos os acionadores e enlaces de tem um `direction` propriedade:

- Para acionadores, a direção de Olá é sempre`in`
- Utilizam enlaces de entrada e de saída `in` e`out`
- Alguns enlaces suportam uma direção especial `inout`. Se utilizar `inout`, apenas Olá **editor avançada** está disponível no Olá **integrar** separador.

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>Utilizar Olá função tipo de retorno tooreturn de saída única

Olá anterior exemplo mostra como toouse Olá função valor de retorno tooprovide saída tooa enlace, o que é conseguido utilizando o parâmetro de nome especial Olá `$return`. (Esta é apenas suportada em idiomas de que tem um valor de retorno, como c#, JavaScript e F #.) Se uma função tem múltiplos enlaces de resultados, utilize `$return` para apenas um dos enlaces de saída Olá. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

Exemplos de Olá abaixo mostra como devolvem tipos são utilizados com enlaces de saída em c#, JavaScript e F #.

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>Propriedade de tipo de dados de enlace

No .NET, utilize o tipo de dados do Olá tipos toodefine Olá para dados de entrada. Por exemplo, utilize `string` toobind toohello texto de um acionador de fila e um tooread de matriz de bytes como binário.

Para os idiomas que são escritos dinamicamente, como JavaScript, utilize Olá `dataType` propriedade na definição de enlace Olá. Por exemplo, tooread Olá conteúdo de um pedido HTTP no formato binário, utilize o tipo de Olá `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Outras opções para `dataType` são `stream` e `string`.

## <a name="resolving-app-settings"></a>Resolver as definições de aplicação
Como melhor prática, os segredos e cadeias de ligação devem ser geridas utilizando as definições de aplicação, em vez de ficheiros de configuração. Isto limita o acesso toothese segredos e torna toostore seguro *function.json* num repositório de controlo de origem público.

As definições de aplicações também são úteis sempre que pretender configuração toochange com base no ambiente de Olá. Por exemplo, num ambiente de teste, poderá ser útil toomonitor um contentor de armazenamento de fila ou blob diferente.

São resolvidas as definições de aplicação sempre que um valor está entre símbolos de percentagem inicia, tais como `%MyAppSetting%`. Tenha em atenção que Olá `connection` propriedade de acionadores e enlaces é num caso especial e resolve automaticamente os valores das definições de aplicação. 

Olá exemplo seguinte é um acionador de fila que utiliza uma definição de aplicação `%input-queue-name%` toodefine Olá fila tootrigger no.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>Propriedades de metadados do acionador

Payload de dados do toohello de adição fornecido por um acionador (por exemplo, a mensagem da fila de saudação que acionou uma função), acionadores muitos fornecem valores de metadados adicionais. Estes valores podem ser utilizados como parâmetros de entrada em c# e F # ou as propriedades de Olá `context.bindings` objeto em JavaScript. 

Por exemplo, um acionador de fila suporta Olá seguintes propriedades:

* QueueTrigger - acionar o conteúdo da mensagem se uma cadeia válida
* DequeueCount
* expirationTime
* Id
* InsertionTime
* NextVisibleTime
* PopReceipt

Detalhes das propriedades de metadados para cada acionador são descritos no tópico de referência Olá correspondente. Documentação também está disponível no Olá **integrar** separador do portal de Olá, no Olá **documentação** secção abaixo área de configuração de enlace Olá.  

Por exemplo, uma vez que os acionadores de blob têm alguns atrasos, pode utilizar um toorun de Acionador de fila a função (consulte [acionador de armazenamento de BLOBs](functions-bindings-storage-blob.md#storage-blob-trigger). mensagem de fila de saudação iria conter Olá blob filename tootrigger no. Utilizar Olá `queueTrigger` propriedade de metadados, pode especificar este comportamento todos na sua configuração, em vez de código.

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

Propriedades de metadados de um acionador também podem ser utilizadas num *expressão de enlace* para outro enlace, como Olá descrito na secção a seguir.

## <a name="binding-expressions-and-patterns"></a>Expressões de enlace e padrões

Uma das funcionalidades mais poderosas do Olá de acionadores e enlaces é *expressões de enlace*. No seu enlace, pode definir as expressões de padrão que, em seguida, podem ser utilizadas noutros enlaces ou o seu código. Também podem ser utilizado o acionador metadados no enlace expressões, como a mostrar no exemplo de Olá no Olá anterior a secção.

Por exemplo, suponha que pretende tooresize imagens no contentor de armazenamento de blob específico, toohello semelhante **imagem Resizer** modelo no Olá **nova função** página. Aceda demasiado**nova função** -> idioma **c#** -> cenário **amostras** -> **ImageResizer CSharp**. 

Eis Olá *function.json* definição:

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

Tenha em atenção que Olá `filename` parâmetro é utilizado de definição do acionador de blob Olá, bem como blob Olá vínculo de saída. Este parâmetro também pode ser utilizado no código da função.

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>GUIDs aleatórios
As funções do Azure fornece uma sintaxe de conveniência para gerar GUIDs dos enlaces, através de Olá `{rand-guid}` expressão de enlace. Olá exemplo seguinte utiliza este toogenerate um nome exclusivo de blob: 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>Hora atual

Pode utilizar a expressão de enlace Olá `DateTime`, que resolve demasiado`DateTime.UtcNow`.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>Vincular as propriedades de entrada de toocustom numa expressão de enlace

Expressões de enlace também podem referenciar propriedades que são definidas no payload de Acionador de Olá próprio. Por exemplo, poderá ser útil o ficheiro de armazenamento do BLOBs do toodynamically enlace tooa de um nome de ficheiro fornecido num webhook.

Por exemplo, Olá seguir *function.json* utiliza uma propriedade denominada `BlobName` do payload de Acionador de Olá:

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish este em c# e F #, tem de definir um POCO que define os campos de Olá cuja serialização irão ser anulados no payload de Acionador de Olá.

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

Em JavaScript, a desserialização de JSON é automaticamente executada e pode utilizar propriedades de Olá diretamente.

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>Configuração de enlace de dados em tempo de execução

Em c# e outras linguagens .NET, pode utilizar um padrão de enlace imperativo, como toohello oposição ao enlaces declarativa no *function.json*. Enlace imperativo é útil se precisam de parâmetros de enlace toobe calculada ao tempo de tempo de execução, em vez de design. toolearn mais, consulte [enlace no tempo de execução através dos enlaces imperativo](functions-reference-csharp.md#imperative-bindings) numa referência de programador Olá c#.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre um enlace específico, consulte Olá seguintes artigos:

- [HTTP e webhooks](functions-bindings-http-webhook.md)
- [Temporizador](functions-bindings-timer.md)
- [Armazenamento de filas](functions-bindings-storage-queue.md)
- [Armazenamento de blobs](functions-bindings-storage-blob.md)
- [Armazenamento de tabelas](functions-bindings-storage-table.md)
- [Hub de Eventos](functions-bindings-event-hubs.md)
- [Service Bus](functions-bindings-service-bus.md)
- [BD do Cosmos](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Hubs de Notificação](functions-bindings-notification-hubs.md)
- [Aplicações Móveis](functions-bindings-mobile-apps.md)
- [Ficheiro externo](functions-bindings-external-file.md)
