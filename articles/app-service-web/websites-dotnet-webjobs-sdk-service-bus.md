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
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>Olá, como toouse barramento de serviço do Azure com o SDK de WebJobs
## <a name="overview"></a>Descrição geral
Este guia fornece c# amostras de código que mostram como tootrigger um processo quando é recebida uma mensagem de Service Bus do Azure. utilização de amostras de código Olá [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versão 1. x.

Guia de Olá parte do princípio de que sabe [como toocreate um projeto do trabalho Web no Visual Studio com ligação cadeias essa conta do storage ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md).

fragmentos de código Olá mostram apenas as funções, não Olá código que cria Olá `JobHost` objeto tal como neste exemplo:

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

A [exemplo de código completado do Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) no repositório do azure-webjobs-sdk-samples Olá no GitHub.com.

## <a id="prerequisites"></a>Pré-requisitos
toowork com o Service Bus tem tooinstall Olá [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet pacote Ademais toohello outros pacotes do SDK de WebJobs. 

Tem a cadeia de ligação do tooset Olá AzureWebJobsServiceBus também nas cadeias de ligação de armazenamento de toohello de adição.  Pode fazê-lo no Olá `connectionStrings` secção do ficheiro App. config Olá, conforme mostrado no seguinte exemplo de Olá:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Para um projeto de exemplo que inclui a definição de cadeia de ligação de barramento de serviço Olá no ficheiro App. config de Olá, consulte [exemplo do Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

cadeias de ligação de Olá também podem ser definidas no ambiente de tempo de execução do Azure de Olá, em seguida, substitui as definições de App. config Olá quando Olá WebJob é executado no Azure; Para obter mais informações, consulte [introdução ao SDK de WebJobs do Olá](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Como é recebida tootrigger uma função de mensagem de fila de barramento de serviço
chamadas de uma função que Olá SDK de WebJobs toowrite quando é recebida uma mensagem de fila, utilize Olá `ServiceBusTrigger` atributo. o construtor de atributos de Olá assume um parâmetro que especifica o nome de Olá de Olá toopoll de fila.

### <a name="how-servicebustrigger-works"></a>Como funciona o ServiceBusTrigger
Olá SDK recebe uma mensagem no `PeekLock` modo e chamadas `Complete` na mensagem de saudação se a função Olá for concluído com êxito ou chamadas `Abandon` se a função de Olá falhar. Se a função de Olá é executada mais de Olá `PeekLock` tempo limite, o bloqueio de Olá automaticamente é renovado.

Barramento de serviço efetua o processamento sua própria fila nocivas que não pode ser controlado ou configurado por Olá SDK de WebJobs. 

### <a name="string-queue-message"></a>Mensagem de fila de cadeia
Olá seguinte exemplo de código lê uma mensagem de fila que contém uma cadeia e escreve Olá cadeia toohello dashboard do SDK de WebJobs.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Nota:** se estiver a criar Olá fila de mensagens de uma aplicação que não utiliza o SDK de WebJobs do Olá, certifique-se de que tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) demasiado "text/plain".

### <a name="poco-queue-message"></a>Mensagem de fila POCO
Olá SDK será automaticamente anular a serialização de uma mensagem de fila contém um JSON para um POCO [(simples objeto antigo de CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) tipo. Olá seguinte exemplo de código lê uma mensagem de fila que contém um `BlobInformation` objeto que tenha um `BlobName` propriedade:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Para exemplos de código que mostra como propriedades de toouse de Olá POCO toowork com blobs e tabelas Olá mesmo funcionar, consulte Olá [versão de filas de armazenamento deste artigo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Se o código que cria a mensagem da fila de saudação não utilizar Olá SDK de WebJobs, utilize toohello semelhante de código seguinte exemplo:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Tipos ServiceBusTrigger funciona com o
Besides `string` e tipos POCO, pode utilizar Olá `ServiceBusTrigger` atributo com uma matriz de bytes ou um `BrokeredMessage` objeto.

## <a id="create"></a>Como toocreate barramento de serviço fila de mensagens
uma função que cria uma nova mensagem de fila de toowrite utilizar Olá `ServiceBus` atributo e passar no construtor de atributos de toohello de nome de fila de Olá. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Criar uma mensagem de fila única de uma função async não
Olá, código de exemplo a seguir utiliza um toocreate de parâmetro de saída uma nova mensagem na fila de Olá com o nome "outputqueue" com Olá mesmo conteúdo como Olá mensagem recebida na fila de Olá com o nome "inputqueue".

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

parâmetro de saída de Olá para a criação de uma mensagem de fila única pode ser qualquer um dos seguintes tipos de Olá:

* `string`
* `byte[]`
* `BrokeredMessage`
* Um tipo POCO serializável por si. Automaticamente serializado como JSON.

Para os parâmetros de tipo POCO, uma mensagem de fila é sempre criada quando termina a função de Olá; Se o parâmetro de Olá for nulo, Olá SDK cria uma mensagem de fila que irá devolver nulo quando a mensagem de saudação é recebida e anular a serialização. Para Olá outros tipos, se Olá parâmetro for nulo nenhuma mensagem de fila é criada.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Criar vários de fila de mensagens ou nas funções de assíncrona
toocreate várias mensagens, utilize Olá `ServiceBus` atributo com `ICollector<T>` ou `IAsyncCollector<T>`, conforme mostrado no seguinte código de exemplo de Olá:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Cada mensagem de fila é criada imediatamente quando hello `Add` método é chamado.

## <a id="topics"></a>Como toowork com tópicos do Service Bus
chamadas de uma função que Olá SDK toowrite quando é recebida uma mensagem de um tópico de barramento de serviço, utilize Olá `ServiceBusTrigger` atributo com o construtor de Olá que demora tópico e nome de subscrição, conforme mostrado no seguinte código de exemplo de Olá:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

toocreate uma mensagem sobre um tópico, utilize Olá `ServiceBus` de atributos com um Olá de nome de tópico igual forma utilizá-lo com um nome de fila.

## <a name="features-added-in-release-11"></a>Funcionalidades adicionadas versão 1.1
Olá funcionalidades a seguir foram adicionado na versão 1.1:

* Permitir a personalização avançada de processamento através de mensagens `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`suporta a personalização de Olá Service Bus `MessagingFactory` e `NamespaceManager`.
* A `MessageProcessor` padrão de estratégia permite-lhe toospecify um processador por fila/tópico.
* Simultaneidade de processamento da mensagem é suportada por predefinição. 
* Personalização fácil de `OnMessageOptions` através de `ServiceBusConfiguration.MessageOptions`.
* Permitir [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe especificado no `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (para cenários em que poderá não ter faça a gestão de direitos). Tenha em atenção que WebJobs do Azure tópicos sem gerir AccessRights e filas do tooautomatically não é possível aprovisionar inexistente.

## <a id="queues"></a>Tópicos relacionados abrangidos por filas de armazenamento Olá como-tooarticle
Para obter informações sobre cenários de SDK de WebJobs tooService não específica Bus, consulte [como toouse Azure fila de armazenamento com Olá SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Tópicos abrangidos esse artigo incluem o seguinte Olá:

* Async funções
* Várias instâncias
* Encerramento correto
* Utilizar o SDK de WebJobs atributos no corpo de Olá de uma função
* Conjunto de cadeias de ligação do SDK de Olá no código
* Definir valores para o SDK de WebJobs os parâmetros do construtor no código
* Acionar manualmente uma função
* Escrever registos

## <a id="nextsteps"></a> Passos seguintes
Este guia forneceu o código de exemplo que mostram como toohandle cenários comuns para trabalhar com o Service Bus do Azure. Para obter mais informações sobre como toouse WebJobs do Azure e Olá SDK de WebJobs, consulte [recursos de recomendada de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).

