---
title: "Referência para programadores de Java para as funções do Azure | Microsoft Docs"
description: "Compreenda como desenvolver funções com o Java."
services: functions
documentationcenter: na
author: rloutlaw
manager: justhe
keywords: "Azure funções, funções, processamento, webhooks, computação dinâmica, arquitetura sem servidor, java de eventos"
ms.service: functions
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/07/2017
ms.author: routlaw
ms.openlocfilehash: 09a48d61cb27b4db0778295565d167a0688cc99f
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/08/2018
---
# <a name="azure-functions-java-developer-guide"></a>Guia para programadores do Java de funções do Azure
> [!div class="op_single_selector"]
[!INCLUDE [functions-selector-languages](../../includes/functions-selector-languages.md)]

## <a name="programming-model"></a>Modelo de programação 

A função do Azure deve ser um método de classe sem monitorização de estado que processa a entrada e produz saída. Embora tem permissão para escrever os métodos de instância, a função tem depende da quaisquer campos de instância da classe. Todos os métodos de função tem de ter um `public` modificador de acesso.

## <a name="triggers-and-annotations"></a>Acionadores e anotações

Normalmente, uma função do Azure é invocada devido a um acionador externo. A função tem de processar essa acionador e respetivas entradas associadas e produzir uma ou mais saídas.

Anotações do Java estão incluídas no `azure-functions-java-core` pacote vincular a entrada e saídas ao seu métodos. Suportado acionadores de entrada e saída anotações de enlace estão incluídas na tabela seguinte:

Vínculo | Anotação
---|---
CosmosDB | N/A
HTTP | <ul><li>`HttpTrigger`</li><li>`HttpOutput`</li></ul>
Mobile Apps | N/A
Hubs de Notificação | N/A
Blob de armazenamento | <ul><li>`BlobTrigger`</li><li>`BlobInput`</li><li>`BlobOutput`</li></ul>
Fila de Armazenamento | <ul><li>`QueueTrigger`</li><li>`QueueOutput`</li></ul>
Tabela de armazenamento | <ul><li>`TableInput`</li><li>`TableOutput`</li></ul>
Temporizador | <ul><li>`TimerTrigger`</li></ul>
Twilio | N/A

Acionador entradas e saídas também podem ser definidas no [function.json](/azure/azure-functions/functions-reference#function-code) para a sua aplicação.

> [!IMPORTANT] 
> Tem de configurar uma conta de armazenamento do Azure no seu [local.settings.json](/azure/azure-functions/functions-run-local#local-settings-file) executar localmente acionadores de Blob de armazenamento do Azure, a fila ou a tabela.

Exemplo utilizando anotações:

```java
import com.microsoft.azure.serverless.functions.annotation.HttpTrigger;
import com.microsoft.azure.serverless.functions.ExecutionContext;

public class Function {
    public String echo(@HttpTrigger(name = "req", methods = {"post"},  authLevel = AuthorizationLevel.ANONYMOUS) 
        String req, ExecutionContext context) {
        return String.format(req);
    }
}
```

A mesma função escrita sem anotações:

```java
package com.example;

public class MyClass {
    public static String echo(String in) {
        return in;
    }
}
```

com o correspondente `function.json`:

```json
{
  "scriptFile": "azure-functions-example.jar",
  "entryPoint": "com.example.MyClass.echo",
  "bindings": [
    {
      "type": "httpTrigger",
      "name": "req",
      "direction": "in",
      "authLevel": "anonymous",
      "methods": [ "post" ]
    },
    {
      "type": "http",
      "name": "$return",
      "direction": "out"
    }
  ]
}

```

## <a name="data-types"></a>Tipos de Dados

É utilizar todos os tipos de dados em Java para os dados de entrada e de saída, incluindo os tipos nativos do; tipos de Java e tipos de Azure especializados definidos nos personalizados `azure-functions-java-core` pacote. As funções do Azure runtime tenta converter a entrada recebida no tipo de pedido pelo seu código.

### <a name="strings"></a>Cadeias

Serão possível converter valores transmitidos para métodos de função cadeias se o tipo de parâmetro de entrada correspondente para a função é do tipo `String`. 

### <a name="plain-old-java-objects-pojos"></a>Objetos de Java (POJOs) antigos simples

As cadeias a formatados com JSON irão ser convertidas em tipos de Java se espera que a entrada do método função desse tipo de Java. Esta conversão permite-lhe transmita entradas JSON para as suas funções e os tipos de Java no seu código sem ter de implementar a conversão no seu próprio código.

Tipos POJO utilizados como entradas para as funções tem o mesmo `public` modificador de acesso como os métodos de função estão a ser utilizados numa. Não tem de declarar os campos de classe POJO `public`. Por exemplo, uma cadeia JSON `{ "x": 3 }` é capaz de ser convertida para o seguinte tipo POJO:

```Java
public class MyData {
    private int x;
}
```

### <a name="binary-data"></a>Dados binários

Dados binários são representados como uma `byte[]` no seu código de funções do Azure. Vincular binárias entradas ou saídas para as suas funções definindo a `dataType` campo no seu function.json para `binary`:

```json
 {
  "scriptFile": "azure-functions-example.jar",
  "entryPoint": "com.example.MyClass.echo",
  "bindings": [
    {
      "type": "blob",
      "name": "content",
      "direction": "in",
      "dataType": "binary",
      "path": "container/myfile.bin",
      "connection": "ExampleStorageAccount"
    },
  ]
}
```

Em seguida, utilizá-lo no seu código de função:

```java
// Class definition and imports are omitted here
public static String echoLength(byte[] content) {
}
```

Utilize `OutputBinding<byte[]>` tipo para tornar um enlace de saída binário.


## <a name="function-method-overloading"></a>A sobrecarga do método de função

São permitidos para métodos de função com o mesmo nome mas com tipos diferentes de sobrecarga. Por exemplo, pode ter ambos `String echo(String s)` e `String echo(MyType s)` uma classe e as funções do Azure runtime decide qual para invocar ao examinar o tipo de entrada real (para o tipo MIME de entrada, HTTP `text/plain` leva a `String` enquanto `application/json` representa `MyType`).

## <a name="inputs"></a>Entradas

Entrada são divididos em duas categorias de funções do Azure: uma é a entrada de acionamento e o outro é a entrada adicional. Embora forem diferentes no `function.json`, a utilização é idêntica no código de Java. Por exemplo, vamos seguinte fragmento de código:

```java
package com.example;

import com.microsoft.azure.serverless.functions.annotation.BindingName;
import java.util.Optional;

public class MyClass {
    public static String echo(Optional<String> in, @BindingName("item") MyObject obj) {
        return "Hello, " + in.orElse("Azure") + " and " + obj.getKey() + ".";
    }

    private static class MyObject {
        public String getKey() { return this.RowKey; }
        private String RowKey;
    }
}
```

O `@BindingName` anotação aceita um `String` propriedade que representa o nome do acionador/enlace definido no `function.json`:

```json
{
  "scriptFile": "azure-functions-example.jar",
  "entryPoint": "com.example.MyClass.echo",
  "bindings": [
    {
      "type": "httpTrigger",
      "name": "req",
      "direction": "in",
      "authLevel": "anonymous",
      "methods": [ "put" ],
      "route": "items/{id}"
    },
    {
      "type": "table",
      "name": "item",
      "direction": "in",
      "tableName": "items",
      "partitionKey": "Example",
      "rowKey": "{id}",
      "connection": "ExampleStorageAccount"
    },
    {
      "type": "http",
      "name": "$return",
      "direction": "out"
    }
  ]
}
```

Para que quando esta função é invocada, o payload de pedido HTTP passa opcional `String` para o argumento `in` e um Table Storage do Azure `MyObject` transmitida para o argumento de tipo `obj`. Utilize o `Optional<T>` tipo para processar entradas para as suas funções que podem ser nulos.

## <a name="outputs"></a>Saídas

Podem ser expressadas saídas no valor de retorno ou os parâmetros de saída. Se existir apenas uma saída, recomendamos que utilize o valor de retorno. Para várias saídas, tem de utilizar os parâmetros de saída.

Valor de retorno é a forma mais simples de saída, apenas a devolver o valor de qualquer tipo e tempo de execução das funções do Azure tentará empacotar referências-lo novamente para o tipo real (por exemplo, uma resposta HTTP). No `functions.json`, utilizar `$return` como o nome do enlace de saída.

Para produzir vários valores de saída, utilize `OutputBinding<T>` tipo definido no `azure-functions-java-core` pacote. Se precisar de efetuar uma resposta HTTP e enviar uma mensagem para uma fila, bem como, pode escrever algo semelhante ao seguinte:

```java
package com.example;

import com.microsoft.azure.serverless.functions.OutputBinding;
import com.microsoft.azure.serverless.functions.annotation.BindingName;

public class MyClass {
    public static String echo(String body, 
    @QueueOutput(queueName = "messages", connection = "AzureWebJobsStorage", name = "queue") OutputBinding<String> queue) {
        String result = "Hello, " + body + ".";
        queue.setValue(result);
        return result;
    }
}
```

qual deve definir o enlace de saída no `function.json`:

```json
{
  "scriptFile": "azure-functions-example.jar",
  "entryPoint": "com.example.MyClass.echo",
  "bindings": [
    {
      "type": "httpTrigger",
      "name": "req",
      "direction": "in",
      "authLevel": "anonymous",
      "methods": [ "post" ]
    },
    {
      "type": "queue",
      "name": "queue",
      "direction": "out",
      "queueName": "messages",
      "connection": "AzureWebJobsStorage"
    },
    {
      "type": "http",
      "name": "$return",
      "direction": "out"
    }
  ]
}
```
## <a name="specialized-types"></a>Tipos de especializado

Por vezes, uma função tem de ter detalhadas controlo sobre entradas e saídas. Especializada tipos o `azure-functions-java-core` pacote são fornecidos para manipular informações de pedido e personalizar o estado de retorno de um acionador HTTP:

| Tipo especializado      |       Alvo        | Utilização normal                  |
| --------------------- | :-----------------: | ------------------------------ |
| `HttpRequestMessage<T>`  |    Acionador de HTTP     | Obter o método, cabeçalhos ou consultas |
| `HttpResponseMessage<T>` | Enlace de saída de HTTP | Devolver o estado diferente de 200   |

> [!NOTE] 
> Também pode utilizar `@BindingName` anotação para obter os cabeçalhos de HTTP e consultas. Por exemplo, `@BindingName("name") String query` itera os cabeçalhos de pedido HTTP e consultas e transmitir esse valor para o método. Por exemplo, `query` será `"test"` se o URL do pedido for `http://example.org/api/echo?name=test`.

### <a name="metadata"></a>Metadados

Metadados provém de diferentes origens, como cabeçalhos HTTP, consultas HTTP, e [acionar metadados](/azure/azure-functions/functions-triggers-bindings#trigger-metadata-properties). Utilize o `@BindingName` anotação juntamente com o nome de metadados para obter o valor.

Por exemplo, o `queryValue` o código seguinte fragmento serão `"test"` se o URL pedido é `http://{example.host}/api/metadata?name=test`.

```Java
package com.example;

import java.util.Optional;
import com.microsoft.azure.serverless.functions.annotation.*;

public class MyClass {
    @FunctionName("metadata")
    public static String metadata(
        @HttpTrigger(name = "req", methods = { "get", "post" }, authLevel = AuthorizationLevel.ANONYMOUS) Optional<String> body,
        @BindingName("name") String queryValue
    ) {
        return body.orElse(queryValue);
    }
}
```

## <a name="functions-execution-context"></a>Contexto de execução de funções

Interagir com o ambiente de execução das funções do Azure através de `ExecutionContext` objecto definido no `azure-functions-java-core` pacote. Utilize o `ExecutionContext` objeto utilizar informações de invocação e informações de tempo de execução de funções no seu código.

### <a name="logging"></a>Registo

Acesso para o registo de tempo de execução de funções está disponível através de `ExecutionContext` objeto. Este registo está associado para o monitor do Azure e permite-lhe sinalizador avisos e erros encontrados durante a execução de função.

O código de exemplo seguintes regista uma mensagem de aviso quando o corpo do pedido recebido está vazio.

```java
import com.microsoft.azure.serverless.functions.annotation.HttpTrigger;
import com.microsoft.azure.serverless.functions.ExecutionContext;

public class Function {
    public String echo(@HttpTrigger(name = "req", methods = {"post"}, authLevel = AuthorizationLevel.ANONYMOUS) String req, ExecutionContext context) {
        if (req.isEmpty()) {
            context.getLogger().warning("Empty request body received by function " + context.getFunctionName() + " with invocation " + context.getInvocationId());
        }
        return String.format(req);
    }
}
```

## <a name="next-steps"></a>Passos Seguintes
Para obter mais informações, consulte os seguintes recursos:

* [Best Practices for Azure Functions (Melhores Práticas para as Funções do Azure)](functions-best-practices.md)
* [Referência para programadores das Funções do Azure](functions-reference.md)
* [Acionadores de funções do Azure e os enlaces](functions-triggers-bindings.md)
