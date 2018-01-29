---
title: "Enlaces de Event Hubs do Azure para as funções do Azure"
description: "Compreenda como utilizar os enlaces de Event Hubs do Azure das funções do Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: cfowler
editor: 
tags: 
keywords: "das funções do Azure, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/08/2017
ms.author: wesmc
ms.openlocfilehash: 0d48d0b008d76cfb2d7d7815a69774976e184467
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/02/2018
---
# <a name="azure-event-hubs-bindings-for-azure-functions"></a>Enlaces de Event Hubs do Azure para as funções do Azure

Este artigo explica como trabalhar com [Event Hubs do Azure](../event-hubs/event-hubs-what-is-event-hubs.md) enlaces para as funções do Azure. Funções do Azure suporta acionam e de saída vínculos para os Event Hubs.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="trigger"></a>Acionador

Utilize o acionador de Event Hubs para responder a um evento enviado para um fluxo de eventos de hub de eventos. Tem de ter acesso de leitura para o hub de eventos para configurar o acionador.

Quando uma função de Acionador de Event Hubs é acionada, a mensagem que aciona é transmitida para a função como uma cadeia.

## <a name="trigger---scaling"></a>Acionar - dimensionamento

Cada instância de uma função de Event Hub-Triggered é copiada por apenas 1 instância do EventProcessorHost (EPH). Os Event Hubs garantem que apenas 1 EPH pode obter uma concessão numa determinada partição.

Por exemplo, suponha que começam com a seguinte configuração e pressupostos para um Hub de eventos:

1. 10 partições.
1. 1000 eventos distribuído uniformemente em todas as partições = mensagens de > 100 em cada partição.

Quando a sua função primeiro está ativada, não há apenas 1 instância da função. Vamos chamar esta instância de função Function_0. Function_0 terão 1 EPH que gere para obter uma concessão em todas as partições de 10. Será iniciada ler eventos de partições 0-9. A partir deste ponto, irá ocorrer um dos seguintes:

* **É necessária a instância de função apenas 1** -Function_0 é capaz de processar todos os 1000 antes de lógica de dimensionamento das funções do Azure se inicia. Por conseguinte, todas as mensagens de 1000 são processadas pelo Function_0.

* **Adicionar 1 instância de função mais** -lógica das funções do Azure de dimensionamento determina que Function_0 tem mais de mensagens que pode processá-lo, pelo que é criada uma nova instância, Function_1,. Os Event Hubs Deteta que uma nova instância EPH está a tentar ler as mensagens. Os Event Hubs iniciará o balanceamento de carga as partições entre as instâncias EPH, por exemplo, partições 0-4 estão atribuídas ao Function_0 e partições 5 9 estão atribuídas a Function_1. 

* **Adicionar N mais instâncias de função** -lógica das funções do Azure de dimensionamento determina que Function_0 e Function_1 têm mais mensagens que o podem processar. Será dimensionado novamente para Function_2... N, em que N é maior do que o paritions de Hub de eventos. Os Event Hubs carregará balancear as partições Function_0 … 9 instâncias.

O facto de que N é maior do que o número de partições é dimensionamento lógica exclusivo atual das funções do Azure. Isto é feito para se certificar de que existem sempre instâncias de EPH prontamente disponível para obter rapidamente o bloqueio de partition(s) à medida que ficam disponíveis a partir de outras instâncias. Os utilizadores só são-lhe cobrados os recursos utilizados quando executa a instância de função e desta sobre-aprovisionar não serem cobrados.

Se todas as execuções de função tenha êxito sem erros, os pontos de verificação são adicionados à conta de armazenamento associados. Quando a apontar verificação for bem sucedida, todas as mensagens de 1000 nunca devem ser obtidas novamente.

## <a name="trigger---example"></a>Acionador - exemplo

Veja o exemplo de específicas do idioma:

* [C#](#trigger---c-example)
* [Script do c# (.csx)](#trigger---c-script-example)
* [F#](#trigger---f-example)
* [JavaScript](#trigger---javascript-example)

### <a name="trigger---c-example"></a>Acionador - c# exemplo

O seguinte exemplo mostra um [c# função](functions-dotnet-class-library.md) que regista o corpo da mensagem do acionador de hub de eventos.

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Para obter acesso aos metadados de evento, vincular a um [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) objeto (requer um `using` instrução para `Microsoft.ServiceBus.Messaging`).

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```
Para receber eventos num batch, certifique- `string` ou `EventData` uma matriz:

```cs
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

### <a name="trigger---c-script-example"></a>Acionador - exemplo de script do c#

O exemplo seguinte mostra um acionador de hub de eventos enlace num *function.json* ficheiro e uma [função de script do c#](functions-reference-csharp.md) que utiliza o enlace. A função regista o corpo da mensagem do acionador de hub de eventos.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```
Eis o código de script do c#:

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Para obter acesso aos metadados de evento, vincular a um [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) objeto (requer um utilizando instrução para `Microsoft.ServiceBus.Messaging`).

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

Para receber eventos num batch, certifique- `string` ou `EventData` uma matriz:

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

### <a name="trigger---f-example"></a>Acionador - F # exemplo

O exemplo seguinte mostra um acionador de hub de eventos enlace num *function.json* ficheiro e uma [F # função](functions-reference-fsharp.md) que utiliza o enlace. A função regista o corpo da mensagem do acionador de hub de eventos.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Eis o código F #:

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

### <a name="trigger---javascript-example"></a>Acionador - exemplo de JavaScript

O exemplo seguinte mostra um acionador de hub de eventos enlace num *function.json* ficheiro e uma [JavaScript função](functions-reference-node.md) que utiliza o enlace. A função regista o corpo da mensagem do acionador de hub de eventos.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Eis o código JavaScript:

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

## <a name="trigger---attributes"></a>Acionador - atributos

No [bibliotecas de classes do c#](functions-dotnet-class-library.md), utilize o [EventHubTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs) atributo, que está definido no pacote NuGet [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus).

O construtor do atributo tem o nome do hub de eventos, o nome do grupo de consumidores e o nome de uma definição de aplicação que contenha a cadeia de ligação. Para obter mais informações sobre estas definições, consulte o [acionar a secção de configuração](#trigger---configuration). Eis um `EventHubTriggerAttribute` exemplo do atributo:

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    ...
}
```

Para obter um exemplo completado, consulte [acionador - c# exemplo](#trigger---c-example).

## <a name="trigger---configuration"></a>Acionador - configuração

A tabela seguinte explica as propriedades de configuração de enlace que definir no *function.json* ficheiros e o `EventHubTrigger` atributo.

|propriedade de Function.JSON | Propriedade de atributo |Descrição|
|---------|---------|----------------------|
|**tipo** | n/d | tem de ser definido como `eventHubTrigger`. Esta propriedade é definida automaticamente quando criar o acionador no portal do Azure.|
|**direção** | n/d | tem de ser definido como `in`. Esta propriedade é definida automaticamente quando criar o acionador no portal do Azure. |
|**nome** | n/d | O nome da variável que representa o item de eventos no código da função. | 
|**caminho** |**EventHubName** | O nome do hub de eventos. | 
|**consumerGroup** |**ConsumerGroup** | Uma propriedade opcional que define o [grupo de consumidores](../event-hubs/event-hubs-features.md#event-consumers) utilizado para subscrever o hub de eventos. Se for omitido, o `$Default` é utilizado o grupo de consumidores. | 
|**ligação** |**Ligação** | O nome de uma definição de aplicação que contenha a cadeia de ligação ao espaço de nomes o hub de eventos. Copie esta cadeia de ligação ao clicar no **informações de ligação** botão para o *espaço de nomes*, não o hub de eventos em si. Esta cadeia de ligação tem de ter, pelo menos, permissões de leitura para ativar o acionador.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---hostjson-properties"></a>Acionador - host.json propriedades

O [host.json](functions-host-json.md#eventhub) ficheiro contém definições que controlam o comportamento de Acionador de Event Hubs.

[!INCLUDE [functions-host-json-event-hubs](../../includes/functions-host-json-event-hubs.md)]

## <a name="output"></a>Saída

Utilize a saída de Event Hubs enlace escrever eventos no registo para uma transmissão de eventos. Tem de ter permissão de envio para um hub de eventos para escrever eventos no mesmo.

## <a name="output---example"></a>De saída - exemplo

Veja o exemplo de específicas do idioma:

* [C#](#output---c-example)
* [Script do c# (.csx)](#output---c-script-example)
* [F#](#output---f-example)
* [JavaScript](#output---javascript-example)

### <a name="output---c-example"></a>Saída - c# exemplo

O seguinte exemplo mostra um [c# função](functions-dotnet-class-library.md) que escreve uma mensagem para um hub de eventos, o valor de retorno do método a utilizar como o resultado:

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

### <a name="output---c-script-example"></a>Saída - exemplo de script do c#

O exemplo seguinte mostra um acionador de hub de eventos enlace num *function.json* ficheiro e uma [função de script do c#](functions-reference-csharp.md) que utiliza o enlace. A função escreve uma mensagem para um hub de eventos.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Eis c# código de script que cria uma mensagem:

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

C# código de script Eis que cria várias mensagens:

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

### <a name="output---f-example"></a>Saída - F # exemplo

O exemplo seguinte mostra um acionador de hub de eventos enlace num *function.json* ficheiro e uma [F # função](functions-reference-fsharp.md) que utiliza o enlace. A função escreve uma mensagem para um hub de eventos.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Eis o código F #:

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

### <a name="output---javascript-example"></a>Saída - exemplo de JavaScript

O exemplo seguinte mostra um acionador de hub de eventos enlace num *function.json* ficheiro e uma [JavaScript função](functions-reference-node.md) que utiliza o enlace. A função escreve uma mensagem para um hub de eventos.

Segue-se os dados do enlace *function.json* ficheiro:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

No código JavaScript Eis que envia uma mensagem único:

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

No código JavaScript Eis que envia mensagens vários:

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="output---attributes"></a>Saída - atributos

Para [bibliotecas de classes do c#](functions-dotnet-class-library.md), utilize o [EventHubAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs) atributo, que está definido no pacote NuGet [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus).

O construtor do atributo tem o nome do hub de eventos e o nome de uma definição de aplicação que contenha a cadeia de ligação. Para obter mais informações sobre estas definições, consulte [de saída - configuração](#output---configuration). Eis um `EventHub` exemplo do atributo:

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    ...
}
```

Para obter um exemplo completado, consulte [resultado - c# exemplo](#output---c-example).

## <a name="output---configuration"></a>De saída - configuração

A tabela seguinte explica as propriedades de configuração de enlace que definir no *function.json* ficheiros e o `EventHub` atributo.

|propriedade de Function.JSON | Propriedade de atributo |Descrição|
|---------|---------|----------------------|
|**tipo** | n/d | Tem de ser definida para "eventHub". |
|**direção** | n/d | Tem de ser definida para "out". Este parâmetro é definido automaticamente quando criar o enlace no portal do Azure. |
|**nome** | n/d | O nome da variável utilizado no código de função que representa o evento. | 
|**caminho** |**EventHubName** | O nome do hub de eventos. | 
|**ligação** |**Ligação** | O nome de uma definição de aplicação que contenha a cadeia de ligação ao espaço de nomes o hub de eventos. Copie esta cadeia de ligação ao clicar no **informações de ligação** botão para o *espaço de nomes*, não o hub de eventos em si. Esta cadeia de ligação tem de ter permissões de envio para enviar a mensagem para o fluxo de eventos.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a>Saída - utilização

Em c# e c# script, enviar mensagens com um parâmetro de método como `out string paramName`. No script do c#, `paramName` é o valor especificado no `name` propriedade *function.json*. Para escrever várias mensagens, pode utilizar `ICollector<string>` ou `IAsyncCollector<string>` em vez de `out string`.

Em JavaScript, o evento de saída de acesso utilizando `context.bindings.<name>`. `<name>`o valor especificado no `name` propriedade *function.json*.

## <a name="next-steps"></a>Passos Seguintes

> [!div class="nextstepaction"]
> [Saiba mais sobre as funções do Azure acionadores e enlaces](functions-triggers-bindings.md)
