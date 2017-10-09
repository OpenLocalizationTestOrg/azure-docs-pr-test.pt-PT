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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="c59a9-103">Descrição geral de API padrão do reencaminhamento híbrido ligações .NET do Azure</span><span class="sxs-lookup"><span data-stu-id="c59a9-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="c59a9-104">Este artigo resume algumas das chave Olá Azure reencaminhamento híbrido ligações .NET padrão [APIs cliente](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="c59a9-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="c59a9-105">Construtor de cadeia de ligação de reencaminhamento</span><span class="sxs-lookup"><span data-stu-id="c59a9-105">Relay Connection String Builder</span></span>

<span data-ttu-id="c59a9-106">Olá [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] classe formatos cadeias de ligação que são as ligações híbridas de tooRelay específico.</span><span class="sxs-lookup"><span data-stu-id="c59a9-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="c59a9-107">Pode utilizar este formato de Olá tooverify de uma cadeia de ligação ou toobuild uma cadeia de ligação a partir do zero.</span><span class="sxs-lookup"><span data-stu-id="c59a9-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="c59a9-108">Consulte o seguinte código para obter um exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="c59a9-108">See hello following code for an example:</span></span>

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

<span data-ttu-id="c59a9-109">Também pode passar uma ligação diretamente cadeia toohello `RelayConnectionStringBuilder` método.</span><span class="sxs-lookup"><span data-stu-id="c59a9-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="c59a9-110">Esta operação permite-lhe tooverify cadeia de ligação de Olá está num formato válido.</span><span class="sxs-lookup"><span data-stu-id="c59a9-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="c59a9-111">Se qualquer um dos parâmetros Olá são inválidos, construtor Olá gera um `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="c59a9-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

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

## <a name="hybrid-connection-stream"></a><span data-ttu-id="c59a9-112">Fluxo de ligação híbrida</span><span class="sxs-lookup"><span data-stu-id="c59a9-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="c59a9-113">Olá [HybridConnectionStream] [ HCStream] classe é Olá objeto principal utilizado toosend e receber dados de um ponto final de reencaminhamento do Azure, se estiver a trabalhar com um [HybridConnectionClient] [ HCClient], ou um [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="c59a9-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="c59a9-114">Obter um fluxo de ligação híbrida</span><span class="sxs-lookup"><span data-stu-id="c59a9-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="c59a9-115">Serviço de escuta</span><span class="sxs-lookup"><span data-stu-id="c59a9-115">Listener</span></span>
<span data-ttu-id="c59a9-116">Utilizar um [HybridConnectionListener][HCListener], pode obter um `HybridConnectionStream` objeto da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="c59a9-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="c59a9-117">Cliente</span><span class="sxs-lookup"><span data-stu-id="c59a9-117">Client</span></span>
<span data-ttu-id="c59a9-118">Utilizar um [HybridConnectionClient][HCClient], pode obter um `HybridConnectionStream` objeto da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="c59a9-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="c59a9-119">A receção de dados</span><span class="sxs-lookup"><span data-stu-id="c59a9-119">Receiving data</span></span>
<span data-ttu-id="c59a9-120">Olá [HybridConnectionStream] [ HCStream] classe permite a comunicação bidirecional.</span><span class="sxs-lookup"><span data-stu-id="c59a9-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="c59a9-121">Na maioria dos casos, receberá continuamente a partir da sequência de Olá.</span><span class="sxs-lookup"><span data-stu-id="c59a9-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="c59a9-122">Se estiver a ler texto do fluxo de Olá, também poderá toouse um [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) objeto, que permite a mais fácil de análise de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="c59a9-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="c59a9-123">Por exemplo, pode ler dados como texto, em vez de como `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="c59a9-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="c59a9-124">Olá seguinte código lê individuais linhas de texto a partir da sequência de Olá até um cancelamento é pedido:</span><span class="sxs-lookup"><span data-stu-id="c59a9-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

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

### <a name="sending-data"></a><span data-ttu-id="c59a9-125">Envio de dados</span><span class="sxs-lookup"><span data-stu-id="c59a9-125">Sending data</span></span>
<span data-ttu-id="c59a9-126">Assim que tiver uma ligação estabelecida, pode enviar um ponto final da mensagem toohello reencaminhamento.</span><span class="sxs-lookup"><span data-stu-id="c59a9-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="c59a9-127">Porque o objeto de ligação de Olá herda [fluxo](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), enviar os dados como um `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="c59a9-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="c59a9-128">Olá seguinte exemplo mostra como toodo isto:</span><span class="sxs-lookup"><span data-stu-id="c59a9-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="c59a9-129">No entanto, se quiser toosend texto diretamente, sem necessitar de cadeia de Olá tooencode sempre que pode encapsular Olá `hybridConnectionStream` objeto com um [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) objeto.</span><span class="sxs-lookup"><span data-stu-id="c59a9-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="c59a9-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c59a9-130">Next steps</span></span>
<span data-ttu-id="c59a9-131">toolearn mais informações sobre o reencaminhamento do Azure, visite estas ligações:</span><span class="sxs-lookup"><span data-stu-id="c59a9-131">toolearn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="c59a9-132">Referência de Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="c59a9-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="c59a9-133">O que é o Reencaminhamento do Azure?</span><span class="sxs-lookup"><span data-stu-id="c59a9-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="c59a9-134">APIs de reencaminhamento disponíveis</span><span class="sxs-lookup"><span data-stu-id="c59a9-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener