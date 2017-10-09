---
title: "aaaHow toouse Service Bus do Azure com Olá SDK de WebJobs"
description: "Saiba como toouse filas de Service Bus do Azure e tópicos com o SDK de WebJobs Olá."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a><span data-ttu-id="2b2d1-103">Olá, como toouse barramento de serviço do Azure com o SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="2b2d1-103">How toouse Azure Service Bus with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="2b2d1-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="2b2d1-104">Overview</span></span>
<span data-ttu-id="2b2d1-105">Este guia fornece c# amostras de código que mostram como tootrigger um processo quando é recebida uma mensagem de Service Bus do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-105">This guide provides C# code samples that show how tootrigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="2b2d1-106">utilização de amostras de código Olá [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versão 1. x.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-106">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="2b2d1-107">Guia de Olá parte do princípio de que sabe [como toocreate um projeto do trabalho Web no Visual Studio com ligação cadeias essa conta do storage ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2b2d1-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="2b2d1-108">fragmentos de código Olá mostram apenas as funções, não Olá código que cria Olá `JobHost` objeto tal como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="2b2d1-108">hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

<span data-ttu-id="2b2d1-109">A [exemplo de código completado do Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) no repositório do azure-webjobs-sdk-samples Olá no GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in hello azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="2b2d1-110"><a id="prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2b2d1-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="2b2d1-111">toowork com o Service Bus tem tooinstall Olá [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet pacote Ademais toohello outros pacotes do SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-111">toowork with Service Bus you have tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition toohello other WebJobs SDK packages.</span></span> 

<span data-ttu-id="2b2d1-112">Tem a cadeia de ligação do tooset Olá AzureWebJobsServiceBus também nas cadeias de ligação de armazenamento de toohello de adição.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-112">You also have tooset hello AzureWebJobsServiceBus connection string in addition toohello storage connection strings.</span></span>  <span data-ttu-id="2b2d1-113">Pode fazê-lo no Olá `connectionStrings` secção do ficheiro App. config Olá, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="2b2d1-113">You can do this in hello `connectionStrings` section of hello App.config file, as shown in hello following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="2b2d1-114">Para um projeto de exemplo que inclui a definição de cadeia de ligação de barramento de serviço Olá no ficheiro App. config de Olá, consulte [exemplo do Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="2b2d1-114">For a sample project that includes hello Service Bus connection string setting in hello App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="2b2d1-115">cadeias de ligação de Olá também podem ser definidas no ambiente de tempo de execução do Azure de Olá, em seguida, substitui as definições de App. config Olá quando Olá WebJob é executado no Azure; Para obter mais informações, consulte [introdução ao SDK de WebJobs do Olá](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2b2d1-115">hello connection strings can also be set in hello Azure runtime environment, which then overrides hello App.config settings when hello WebJob runs in Azure; for more information, see [Get Started with hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="2b2d1-116"><a id="trigger"></a>Como é recebida tootrigger uma função de mensagem de fila de barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="2b2d1-116"><a id="trigger"></a> How tootrigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="2b2d1-117">chamadas de uma função que Olá SDK de WebJobs toowrite quando é recebida uma mensagem de fila, utilize Olá `ServiceBusTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-117">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="2b2d1-118">o construtor de atributos de Olá assume um parâmetro que especifica o nome de Olá de Olá toopoll de fila.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-118">hello attribute constructor takes a parameter that specifies hello name of hello queue toopoll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="2b2d1-119">Como funciona o ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="2b2d1-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="2b2d1-120">Olá SDK recebe uma mensagem no `PeekLock` modo e chamadas `Complete` na mensagem de saudação se a função Olá for concluído com êxito ou chamadas `Abandon` se a função de Olá falhar.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-120">hello SDK receives a message in `PeekLock` mode and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> <span data-ttu-id="2b2d1-121">Se a função de Olá é executada mais de Olá `PeekLock` tempo limite, o bloqueio de Olá automaticamente é renovado.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-121">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<span data-ttu-id="2b2d1-122">Barramento de serviço efetua o processamento sua própria fila nocivas que não pode ser controlado ou configurado por Olá SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-122">Service Bus does its own poison queue handling which cannot be controlled or configured by hello WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="2b2d1-123">Mensagem de fila de cadeia</span><span class="sxs-lookup"><span data-stu-id="2b2d1-123">String queue message</span></span>
<span data-ttu-id="2b2d1-124">Olá seguinte exemplo de código lê uma mensagem de fila que contém uma cadeia e escreve Olá cadeia toohello dashboard do SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-124">hello following code sample reads a queue message that contains a string and writes hello string toohello WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="2b2d1-125">**Nota:** se estiver a criar Olá fila de mensagens de uma aplicação que não utiliza o SDK de WebJobs do Olá, certifique-se de que tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) demasiado "text/plain".</span><span class="sxs-lookup"><span data-stu-id="2b2d1-125">**Note:** If you are creating hello queue messages in an application that doesn't use hello WebJobs SDK, make sure tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) too"text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="2b2d1-126">Mensagem de fila POCO</span><span class="sxs-lookup"><span data-stu-id="2b2d1-126">POCO queue message</span></span>
<span data-ttu-id="2b2d1-127">Olá SDK será automaticamente anular a serialização de uma mensagem de fila contém um JSON para um POCO [(simples objeto antigo de CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) tipo.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-127">hello SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="2b2d1-128">Olá seguinte exemplo de código lê uma mensagem de fila que contém um `BlobInformation` objeto que tenha um `BlobName` propriedade:</span><span class="sxs-lookup"><span data-stu-id="2b2d1-128">hello following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="2b2d1-129">Para exemplos de código que mostra como propriedades de toouse de Olá POCO toowork com blobs e tabelas Olá mesmo funcionar, consulte Olá [versão de filas de armazenamento deste artigo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="2b2d1-129">For code samples showing how toouse properties of hello POCO toowork with blobs and tables in hello same function, see hello [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="2b2d1-130">Se o código que cria a mensagem da fila de saudação não utilizar Olá SDK de WebJobs, utilize toohello semelhante de código seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="2b2d1-130">If your code that creates hello queue message doesn't use hello WebJobs SDK, use code similar toohello following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="2b2d1-131">Tipos ServiceBusTrigger funciona com o</span><span class="sxs-lookup"><span data-stu-id="2b2d1-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="2b2d1-132">Besides `string` e tipos POCO, pode utilizar Olá `ServiceBusTrigger` atributo com uma matriz de bytes ou um `BrokeredMessage` objeto.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-132">Besides `string` and POCO  types, you can use hello `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="2b2d1-133"><a id="create"></a>Como toocreate barramento de serviço fila de mensagens</span><span class="sxs-lookup"><span data-stu-id="2b2d1-133"><a id="create"></a> How toocreate Service Bus queue messages</span></span>
<span data-ttu-id="2b2d1-134">uma função que cria uma nova mensagem de fila de toowrite utilizar Olá `ServiceBus` atributo e passar no construtor de atributos de toohello de nome de fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-134">toowrite a function that creates a new queue message use hello `ServiceBus` attribute and pass in hello queue name toohello attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="2b2d1-135">Criar uma mensagem de fila única de uma função async não</span><span class="sxs-lookup"><span data-stu-id="2b2d1-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="2b2d1-136">Olá, código de exemplo a seguir utiliza um toocreate de parâmetro de saída uma nova mensagem na fila de Olá com o nome "outputqueue" com Olá mesmo conteúdo como Olá mensagem recebida na fila de Olá com o nome "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="2b2d1-136">hello following code sample uses an output parameter toocreate a new message in hello queue named "outputqueue" with hello same content as hello message received in hello queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="2b2d1-137">parâmetro de saída de Olá para a criação de uma mensagem de fila única pode ser qualquer um dos seguintes tipos de Olá:</span><span class="sxs-lookup"><span data-stu-id="2b2d1-137">hello output parameter for creating a single queue message can be any of hello following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="2b2d1-138">Um tipo POCO serializável por si.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="2b2d1-139">Automaticamente serializado como JSON.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="2b2d1-140">Para os parâmetros de tipo POCO, uma mensagem de fila é sempre criada quando termina a função de Olá; Se o parâmetro de Olá for nulo, Olá SDK cria uma mensagem de fila que irá devolver nulo quando a mensagem de saudação é recebida e anular a serialização.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-140">For POCO type parameters, a queue message is always created when hello function ends; if hello parameter is null, hello SDK creates a queue message that will return null when hello message is received and deserialized.</span></span> <span data-ttu-id="2b2d1-141">Para Olá outros tipos, se Olá parâmetro for nulo nenhuma mensagem de fila é criada.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-141">For hello other types, if hello parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="2b2d1-142">Criar vários de fila de mensagens ou nas funções de assíncrona</span><span class="sxs-lookup"><span data-stu-id="2b2d1-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="2b2d1-143">toocreate várias mensagens, utilize Olá `ServiceBus` atributo com `ICollector<T>` ou `IAsyncCollector<T>`, conforme mostrado no seguinte código de exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="2b2d1-143">toocreate multiple messages, use  hello `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="2b2d1-144">Cada mensagem de fila é criada imediatamente quando hello `Add` método é chamado.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-144">Each queue message is created immediately when hello `Add` method is called.</span></span>

## <span data-ttu-id="2b2d1-145"><a id="topics"></a>Como toowork com tópicos do Service Bus</span><span class="sxs-lookup"><span data-stu-id="2b2d1-145"><a id="topics"></a>How toowork with Service Bus topics</span></span>
<span data-ttu-id="2b2d1-146">chamadas de uma função que Olá SDK toowrite quando é recebida uma mensagem de um tópico de barramento de serviço, utilize Olá `ServiceBusTrigger` atributo com o construtor de Olá que demora tópico e nome de subscrição, conforme mostrado no seguinte código de exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="2b2d1-146">toowrite a function that hello SDK calls when a message is received on a Service Bus topic, use hello `ServiceBusTrigger` attribute with hello constructor that takes topic name and subscription name, as shown in hello following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="2b2d1-147">toocreate uma mensagem sobre um tópico, utilize Olá `ServiceBus` de atributos com um Olá de nome de tópico igual forma utilizá-lo com um nome de fila.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-147">toocreate a message on a topic, use hello `ServiceBus` attribute with a topic name hello same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="2b2d1-148">Funcionalidades adicionadas versão 1.1</span><span class="sxs-lookup"><span data-stu-id="2b2d1-148">Features added in release 1.1</span></span>
<span data-ttu-id="2b2d1-149">Olá funcionalidades a seguir foram adicionado na versão 1.1:</span><span class="sxs-lookup"><span data-stu-id="2b2d1-149">hello following features were added in release 1.1:</span></span>

* <span data-ttu-id="2b2d1-150">Permitir a personalização avançada de processamento através de mensagens `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="2b2d1-151">`MessagingProvider`suporta a personalização de Olá Service Bus `MessagingFactory` e `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-151">`MessagingProvider` supports customization of hello Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="2b2d1-152">A `MessageProcessor` padrão de estratégia permite-lhe toospecify um processador por fila/tópico.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-152">A `MessageProcessor` strategy pattern allows you toospecify a processor per queue/topic.</span></span>
* <span data-ttu-id="2b2d1-153">Simultaneidade de processamento da mensagem é suportada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="2b2d1-154">Personalização fácil de `OnMessageOptions` através de `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="2b2d1-155">Permitir [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe especificado no `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (para cenários em que poderá não ter faça a gestão de direitos).</span><span class="sxs-lookup"><span data-stu-id="2b2d1-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="2b2d1-156">Tenha em atenção que WebJobs do Azure tópicos sem gerir AccessRights e filas do tooautomatically não é possível aprovisionar inexistente.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-156">Note that Azure WebJobs is unable tooautomatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="2b2d1-157"><a id="queues"></a>Tópicos relacionados abrangidos por filas de armazenamento Olá como-tooarticle</span><span class="sxs-lookup"><span data-stu-id="2b2d1-157"><a id="queues"></a>Related topics covered by hello storage queues how-tooarticle</span></span>
<span data-ttu-id="2b2d1-158">Para obter informações sobre cenários de SDK de WebJobs tooService não específica Bus, consulte [como toouse Azure fila de armazenamento com Olá SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="2b2d1-158">For information about WebJobs SDK scenarios not specific tooService Bus, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="2b2d1-159">Tópicos abrangidos esse artigo incluem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="2b2d1-159">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="2b2d1-160">Async funções</span><span class="sxs-lookup"><span data-stu-id="2b2d1-160">Async functions</span></span>
* <span data-ttu-id="2b2d1-161">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="2b2d1-161">Multiple instances</span></span>
* <span data-ttu-id="2b2d1-162">Encerramento correto</span><span class="sxs-lookup"><span data-stu-id="2b2d1-162">Graceful shutdown</span></span>
* <span data-ttu-id="2b2d1-163">Utilizar o SDK de WebJobs atributos no corpo de Olá de uma função</span><span class="sxs-lookup"><span data-stu-id="2b2d1-163">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="2b2d1-164">Conjunto de cadeias de ligação do SDK de Olá no código</span><span class="sxs-lookup"><span data-stu-id="2b2d1-164">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="2b2d1-165">Definir valores para o SDK de WebJobs os parâmetros do construtor no código</span><span class="sxs-lookup"><span data-stu-id="2b2d1-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="2b2d1-166">Acionar manualmente uma função</span><span class="sxs-lookup"><span data-stu-id="2b2d1-166">Trigger a function manually</span></span>
* <span data-ttu-id="2b2d1-167">Escrever registos</span><span class="sxs-lookup"><span data-stu-id="2b2d1-167">Write logs</span></span>

## <span data-ttu-id="2b2d1-168"><a id="nextsteps"></a> Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2b2d1-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="2b2d1-169">Este guia forneceu o código de exemplo que mostram como toohandle cenários comuns para trabalhar com o Service Bus do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b2d1-169">This guide has provided code samples that show how toohandle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="2b2d1-170">Para obter mais informações sobre como toouse WebJobs do Azure e Olá SDK de WebJobs, consulte [recursos de recomendada de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="2b2d1-170">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

