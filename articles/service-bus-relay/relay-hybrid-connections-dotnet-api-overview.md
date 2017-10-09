---
title: "aaaOverview de Olá APIs padrão do .NET de reencaminhamento do Azure | Microsoft Docs"
description: "Descrição geral da API de padrão de .NET de reencaminhamento"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Descrição geral de API padrão do reencaminhamento híbrido ligações .NET do Azure

Este artigo resume algumas das chave Olá Azure reencaminhamento híbrido ligações .NET padrão [APIs cliente](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Construtor de cadeia de ligação de reencaminhamento

Olá [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] classe formatos cadeias de ligação que são as ligações híbridas de tooRelay específico. Pode utilizar este formato de Olá tooverify de uma cadeia de ligação ou toobuild uma cadeia de ligação a partir do zero. Consulte o seguinte código para obter um exemplo de Olá:

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

Também pode passar uma ligação diretamente cadeia toohello `RelayConnectionStringBuilder` método. Esta operação permite-lhe tooverify cadeia de ligação de Olá está num formato válido. Se qualquer um dos parâmetros Olá são inválidos, construtor Olá gera um `ArgumentException`.

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a>Fluxo de ligação híbrida
Olá [HybridConnectionStream] [ HCStream] classe é Olá objeto principal utilizado toosend e receber dados de um ponto final de reencaminhamento do Azure, se estiver a trabalhar com um [HybridConnectionClient] [ HCClient], ou um [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Obter um fluxo de ligação híbrida

#### <a name="listener"></a>Serviço de escuta
Utilizar um [HybridConnectionListener][HCListener], pode obter um `HybridConnectionStream` objeto da seguinte forma:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>Cliente
Utilizar um [HybridConnectionClient][HCClient], pode obter um `HybridConnectionStream` objeto da seguinte forma:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>A receção de dados
Olá [HybridConnectionStream] [ HCStream] classe permite a comunicação bidirecional. Na maioria dos casos, receberá continuamente a partir da sequência de Olá. Se estiver a ler texto do fluxo de Olá, também poderá toouse um [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) objeto, que permite a mais fácil de análise de dados de Olá. Por exemplo, pode ler dados como texto, em vez de como `byte[]`.

Olá seguinte código lê individuais linhas de texto a partir da sequência de Olá até um cancelamento é pedido:

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a>Envio de dados
Assim que tiver uma ligação estabelecida, pode enviar um ponto final da mensagem toohello reencaminhamento. Porque o objeto de ligação de Olá herda [fluxo](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), enviar os dados como um `byte[]`. Olá seguinte exemplo mostra como toodo isto:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

No entanto, se quiser toosend texto diretamente, sem necessitar de cadeia de Olá tooencode sempre que pode encapsular Olá `hybridConnectionStream` objeto com um [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) objeto.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre o reencaminhamento do Azure, visite estas ligações:

* [Referência de Microsoft.Azure.Relay](/dotnet/api/microsoft.azure.relay)
* [O que é o Reencaminhamento do Azure?](relay-what-is-it.md)
* [APIs de reencaminhamento disponíveis](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener