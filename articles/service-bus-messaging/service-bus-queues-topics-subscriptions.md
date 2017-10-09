---
title: "aaaOverview de mensagens de filas, tópicos e subscrições do Azure Service Bus | Microsoft Docs"
description: "Descrição geral de entidades de mensagens do Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Filas, tópicos e subscrições do Service Bus

Microsoft Azure Service Bus suporta um conjunto de tecnologias de middleware baseado na nuvem, orientado para a mensagem, incluindo a colocação de mensagens fiável e durável publicação de mensagens. Estas capacidades de mensagens "mediadas" podem considerar como desassociados mensagens funcionalidades que o suporte de publicação-subscrição, temporal desacoplamento e cenários de utilização de recursos de infraestrutura mensagens do Service Bus Olá de balanceamento de carga. A comunicação desacoplada tem muitas vantagens; por exemplo, os clientes e os servidores podem ligar-se conforme necessário e efetuar as operações de forma assíncrona.

entidades de mensagens Hello que formam core Olá de Olá mensagens capacidades no Service Bus são filas, tópicos e subscrições e regras/ações.

## <a name="queues"></a>Filas

As filas oferecem *First In, Out primeiro* tooone de entrega de mensagem (FIFO) ou mais consumidores concorrentes. Ou seja, as mensagens são normalmente esperado toobe recebidas e processadas pelos recetores segundo Olá Olá ordem pela qual foram adicionadas toohello fila, e cada mensagem é recebida e processada por apenas um consumidor de mensagens. Uma vantagem de utilizar as filas é tooachieve "desacoplamento temporal" dos componentes da aplicação. Olá por outras palavras, os produtores (remetentes) e os consumidores (recetores) não têm toobe envio e receção de mensagens em Olá mesmo tempo, porque as mensagens são armazenadas de maneira duradoura na fila de Olá. Além disso, o produtor de Olá não possui toowait para uma resposta do consumidor Olá na ordem toocontinue tooprocess e enviar mensagens.

Uma vantagem relacionada é "carga nivelamento," que permite toosend produtores e consumidores e recebe mensagens a taxas diferentes. Em muitas aplicações, a carga de sistema Olá varia ao longo do tempo; No entanto, o tempo de processamento de Olá necessário para cada unidade de trabalho é geralmente constante. A intermediação de mensagem de produtores e consumidores através de uma fila significa que Olá consumir aplicação só tem toobe toobe aprovisionado toohandle capaz de carga média em vez de pico de carga. profundidade Olá da fila de Olá aumenta e contrai como carga hello a receber varia. Tal poupa diretamente dinheiro com a quantidade de toohello regard de carga da infraestrutura necessária tooservice Olá aplicação. Como Olá carga aumenta, mais processos de trabalho podem ser adicionado tooread da fila de Olá. Cada mensagem é processada apenas por um Olá de processos de trabalho. Além disso, este balanceamento de carga baseado na solicitação permite a utilização ideal de computadores de trabalho de Olá, mesmo se os computadores de trabalho de Olá diferem com regard tooprocessing corrente, o vez que transmitirão as mensagens na sua própria taxa máxima. Este padrão é frequentemente denominado padrão padrão de "competir consumidor" Olá.

Se utilizar filas toointermediate entre mensagem produtores e consumidores fornece um coupling soltas inerente entre os componentes de Olá. Porque os produtores e consumidores não têm conhecimento entre si, um consumidor possa ser atualizado sem ter qualquer efeito em produtor Olá.

Criar uma fila é um processo de vários passo. Efetuar operações de gestão do Service Bus entidades (filas e tópicos) através de Olá de mensagens [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe, que é criada, fornecendo o endereço base do Olá do Olá Service Bus espaço de nomes e Olá as credenciais do utilizador. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) fornece métodos toocreate, enumerar e eliminar entidades de mensagens. Depois de criar um [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) objeto de objeto de nome SAS Olá e chave e um gestão de espaço de nomes de serviço, pode utilizar Olá [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) fila do método toocreate Olá. Por exemplo:

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

Em seguida, pode criar um objeto de fila e uma fábrica de mensagens com Olá URI do Service Bus como um argumento. Por exemplo:

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

Em seguida, pode enviar toohello a fila de mensagens. Por exemplo, se tiver uma lista de mensagens mediadas chamado `MessageList`, código de Olá aparece semelhante toohello seguinte:

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

Em seguida, receber mensagens da fila de Olá da seguinte forma:

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

No Olá [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modo, Olá receber operação única; ou seja, quando o Service Bus recebe o pedido de Olá, marca Olá mensagem como consumida e devolve a mesma aplicação toohello. **ReceiveAndDelete** modo é Olá de modelo mais simples e funciona melhor para cenários em que Olá aplicação pode tolerar o não processamento de uma mensagem no evento Olá de uma falha. toounderstand isto, considere um cenário no quais problemas de consumidor Olá Olá receber o pedido e, em seguida, falhas antes do processamento-lo. Porque o Service Bus marca a mensagem de saudação como consumida, quando a aplicação Olá reinicia e começa a consumir novamente mensagens, terá perdido mensagem de saudação foi consumida falhas toohello anterior.

No [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) modo, Olá receber operação torna-se duas etapas, que torna possível toosupport aplicações que não toleram mensagens em falta. Quando o Service Bus recebe o pedido de Olá, localiza toobe Olá seguinte mensagem consumida, bloqueia-tooprevent outros consumidores de receção e, em seguida, devolve a mesma aplicação toohello. Após a aplicação Olá concluir o processamento da mensagem de saudação (ou armazena a mesma forma fiável para processamento futuro), conclui Olá segunda etapa do Olá processo de receção ao chamar [concluída](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) na mensagem de saudação recebida. Quando o Service Bus vê Olá **concluída** chamada, marca a mensagem de saudação como consumida.

Se a aplicação Olá for não é possível tooprocess Olá mensagem por algum motivo, pode chamar Olá [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) método na mensagem de saudação recebida (em vez de [concluída](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Isto permite que a mensagem de saudação do Service Bus toounlock e torná-lo disponível toobe novamente recebida, por Olá consumidor mesmo ou outro consumidor concorrente. Lugar, existe é associado a um tempo limite de bloqueio de Olá e se a aplicação Olá falha tooprocess Olá mensagem antes de Olá tempo limite de bloqueio expira (por exemplo, se a falha da aplicação Olá), o Service Bus desbloqueia a mensagem de saudação e torna toobe disponível novamente recebida (essencialmente efetuar um [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operação por predefinição).

Tenha em atenção que no Olá eventos Olá aplicação falhas após o processamento da mensagem de saudação, mas antes de Olá **concluída** pedido é emitido, mensagem de saudação é reenviada toohello aplicação quando esta reiniciar. Isto é frequentemente designado *, pelo menos, uma vez* processamento; ou seja, cada mensagem é processada pelo menos uma vez. No entanto, em determinadas Olá situações mesma mensagem poderá ser reenviada. Se o cenário de Olá não pode tolerar o processamento duplicado, em seguida, é necessário lógica adicional no Olá aplicação toodetect os duplicados que podem ser conseguidos com base no Olá **MessageId** propriedade da mensagem de saudação, que permanece constante nas tentativas de entrega. Isto é conhecido como *exatamente uma vez* processamento.

## <a name="topics-and-subscriptions"></a>Tópicos e subscrições
Em contraste tooqueues, em que cada mensagem é processada por um único consumidor, *tópicos* e *subscrições* proporcionar uma forma de um-para-muitos de comunicação, um *publicação* padrão. Útil para dimensionamento toovery grandes quantidades de destinatários, cada mensagem publicada é efetuada registada no tópico Olá de subscrição de tooeach disponíveis. As mensagens são enviadas tooa tópico e entregue tooone ou mais subscrições associadas, consoante as regras de filtro que podem ser definidas numa base por subscrição. subscrições de Olá podem utilizar mensagens hello toorestrict de filtros adicionais que querem tooreceive. As mensagens são enviadas tooa tópico Olá mesma forma são enviadas tooa fila, mas as mensagens não são recebeu tópico Olá diretamente. Em vez disso, são recebidos de subscrições. Uma subscrição de tópico é semelhante uma fila virtual que recebe cópias das mensagens hello que são enviadas toohello tópico. As mensagens são recebidas a partir de uma subscrição de forma idêntica forma toohello que são recebidos a partir de uma fila.

A título de comparação, hello funcionalidade de envio de mensagem de uma fila mapeia diretamente tooa tópico e a funcionalidade de receção de mensagens mapeia tooa subscrição. Entre outras coisas, isto significa que as subscrições suportam Olá padrões mesmos descritas anteriormente nesta secção com regard tooqueues: consumidor concorrente, desacoplamento temporal, nivelamento de carga e balanceamento de carga.

A criação de um tópico é semelhante toocreating uma fila, conforme mostrado no exemplo de Olá na secção anterior Olá. Criar serviço Olá URI e, em seguida, utilizar Olá [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) cliente de espaço de nomes do classe toocreate Olá. Em seguida, pode criar um tópico com Olá [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) método. Por exemplo:

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

Em seguida, adicione as subscrições como pretendido:

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

Em seguida, pode criar um cliente de tópico. Por exemplo:

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

Utilizar o remetente da mensagem Olá, pode enviar e receber mensagens tooand de tópico Olá, conforme mostrado na secção anterior Olá. Por exemplo:

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

Tooqueues semelhantes, as mensagens são recebidos a partir de uma subscrição a utilizar um [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) objeto em vez de um [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) objeto. Criar o cliente de subscrição de Olá, transmitir o nome de Olá tópico Olá, nome de Olá da subscrição de Olá, e (opcionalmente) Olá receber o modo como parâmetros. Por exemplo, com Olá **inventário** subscrição:

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>Regras e ações
Em vários cenários, as mensagens com características específicas tem de ser processadas de formas diferentes. tooenable, pode configurar subscrições toofind mensagens tem pretendido propriedades e, em seguida, efetuar determinadas propriedades de toothose modificações. Enquanto as subscrições do Service Bus ver todas as mensagens enviadas toohello tópico, só poderá copiar um subconjunto de a fila de mensagens toohello virtual da subscrição. Isto é conseguido utilizando filtros de subscrição. Essas alterações são denominadas *filtrar ações*. Quando é criada uma subscrição, pode fornecer uma expressão de filtro que opera em Olá as propriedades da mensagem de saudação, ambos Olá propriedades do sistema (por exemplo, **etiqueta**) e as propriedades de aplicação personalizada (por exemplo, **StoreName**.) Olá expressão de filtro do SQL Server é opcional neste caso; sem uma expressão de filtro do SQL Server, será efetuada qualquer ação do filtro definida em subscrições em todas as mensagens de Olá dessa subscrição.

Utilizando o exemplo anterior Olá, mensagens de toofilter apenas feitos **Store1**, poderá criar subscrição de Dashboard Olá da seguinte forma:

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

Com este filtro de subscrição no local, apenas as mensagens hello `StoreName` propriedade definida demasiado`Store1` são copiados toohello fila virtual para Olá `Dashboard` subscrição.

Para obter mais informações sobre os valores de filtro possíveis, consulte a documentação de Olá para Olá [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) e [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classes. Além disso, consulte Olá [mensagens mediadas: filtros avançados](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) e [filtros de tópico](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) amostras.

## <a name="next-steps"></a>Passos seguintes
Consulte o artigo seguinte Olá avançadas tópicos para obter mais informações e exemplos de como utilizar mensagens do Service Bus.

* [Descrição geral das mensagens do Service Bus](service-bus-messaging-overview.md)
* [Tutorial de .NET de mensagens mediadas do Service Bus](service-bus-brokered-tutorial-dotnet.md)
* [Tutorial de REST de mensagens mediadas do Service Bus](service-bus-brokered-tutorial-rest.md)
* [Exemplo de filtros de tópico](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [Mensagens mediadas: Exemplo de filtros de avançadas](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

