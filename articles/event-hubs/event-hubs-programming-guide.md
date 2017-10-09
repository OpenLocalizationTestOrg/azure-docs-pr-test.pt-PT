---
title: Guia de aaaProgramming para Event Hubs do Azure | Microsoft Docs
description: "Escreva código para utilizar Olá SDK .NET do Azure de Event Hubs do Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>Guia de programação dos Event Hubs

Este artigo aborda alguns cenários comuns escrever código com o Event Hubs do Azure e Olá SDK .NET do Azure. Parte do princípio de que possui compreensão preliminar dos Event Hubs. Para uma descrição geral conceptual dos Event Hubs, consulte Olá [descrição geral dos Event Hubs](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Publicadores de eventos

Enviar o hub de eventos de tooan eventos utilizando o HTTP POST ou através de uma ligação AMQP 1.0. Olá, escolha de qual toouse e quando depende do cenário específico Olá que está a ser resolvido. As ligações AMQP 1.0 são medidas como ligações mediadas no Service Bus e são mais adequadas nos cenários com requisitos de latência inferiores e volumes de mensagens altos frequentes, que fornecem um canal de mensagens persistente.

Criar e gerir os Event Hubs utilizando Olá [NamespaceManager][] classe. Quando utilizar Olá .NET APIs geridas, Olá primário construções para publicar dados tooEvent Hubs são Olá [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) e [EventData][] classes. [EventHubClient][] fornece o canal de comunicação AMQP Olá durante o qual os eventos são enviados toohello hub de eventos. Olá [EventData][] classe representa um evento e é utilizado toopublish mensagens tooan event hub. Esta classe inclui Olá corpo, alguns metadados e as informações de cabeçalho sobre eventos de Olá. Outras propriedades são adicionadas toohello [EventData][] objeto como estes passam por um hub de eventos.

## <a name="get-started"></a>Introdução

classes de .NET de Olá que suportam Event Hubs são fornecidas no Olá assemblagem Microsoft.ServiceBus.dll. Olá mais fácil Olá tooreference de forma API do Service Bus e tooconfigure a aplicação com todas as Olá dependências do Service Bus é Olá toodownload [pacote NuGet do Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus). Em alternativa, pode utilizar Olá [consola do Gestor de pacotes](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) no Visual Studio. toodo por isso, emitir Olá seguinte comando na Olá [consola do Gestor de pacotes](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) janela:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Criar um hub de eventos
Pode utilizar Olá [NamespaceManager][] classe toocreate Event Hubs. Por exemplo:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

Na maioria dos casos, é recomendado que utilize Olá [CreateEventHubIfNotExists][] tooavoid métodos geração de exceções se Olá serviço for reiniciado. Por exemplo:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

Todas as operações de criação de Event Hubs, incluindo [CreateEventHubIfNotExists][], requerem **gerir** permissões Olá espaço de nomes em questão. Se pretender que as permissões de Olá toolimit das suas aplicações de consumidor ou do publicador, pode evitar estas criar chamadas de operação no código de produção ao utilizar as credenciais com permissões limitadas.

Olá [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) classe contém detalhes sobre um hub de eventos, incluindo as regras de autorização de Olá, intervalo de retenção de mensagem de Olá, IDs de partição, estado e caminho. Pode utilizar estes metadados de Olá tooupdate classe para um hub de eventos.

## <a name="create-an-event-hubs-client"></a>Criar um cliente dos Event Hubs
Olá classe principal para interagir com os Event Hubs é [eventhubclient][EventHubClient]. Esta classe fornece capacidades tanto para o emissor como para o recetor. Pode instanciar esta classe utilizando Olá [criar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) método, conforme mostrado no seguinte exemplo de Olá.

```csharp
var client = EventHubClient.Create(description.Path);
```

Este método utiliza as informações de ligação do Service Bus Olá no ficheiro App. config de Olá, no Olá `appSettings` secção. Para obter um exemplo de Olá `appSettings` XML utilizado informações de ligação do toostore Olá Service Bus, consulte a documentação de Olá para Olá [eventhubclient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) método.

Outra opção é toocreate cliente Olá uma cadeia de ligação. Esta opção funciona bem quando utilizar funções de trabalho do Azure, porque pode armazenar cadeia Olá nas propriedades de configuração de Olá para trabalho Olá. Por exemplo:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

cadeia de ligação de Olá vai estar no mesmo formato como é apresentado no ficheiro App. config Olá métodos anteriores Olá de Olá:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Por fim, também é possível toocreate um [EventHubClient][] objeto a partir de um [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instância, conforme mostrado no seguinte exemplo de Olá.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

É importante toonote adicional que [EventHubClient][] objetos criados a partir de uma instância de fábrica de mensagens irão reutilizar Olá mesma ligação TCP subjacente. Por conseguinte, estes objetos têm um limite de débito no lado do cliente. Olá [criar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) método reutiliza uma fábrica de mensagens única. Se precisar de débito muito elevado de um remetente único, pode criar várias fábricas de mensagens e um objeto [EventHubClient][] a partir de cada fábrica de mensagens.

## <a name="send-events-tooan-event-hub"></a>Enviar o hub de eventos de tooan de eventos
Enviar o hub de eventos de tooan eventos criando uma [EventData][] instância e enviar através de Olá [enviar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) método. Este método aceita um único [EventData][] parâmetro da instância e envia-modo síncrono hub de eventos de tooan.

## <a name="event-serialization"></a>Serialização de eventos
Olá [EventData][] classe tem [quatro construtores sobrecarregados](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) que assumem uma variedade de parâmetros, tais como um objeto e o serializador, uma matriz de bytes ou uma transmissão em fluxo. Também é possível tooinstantiate Olá [EventData][] classe e definir o fluxo do corpo Olá posteriormente. Quando utilizar o JSON com [EventData][], pode utilizar **Encoding.UTF8.GetBytes()** matriz de bytes de Olá tooretrieve para uma cadeia codificada em JSON.

## <a name="partition-key"></a>Chave de partição
Olá [EventData][] classe tem um [PartitionKey][] propriedade permite Olá remetente toospecify um valor que é protegido por hash tooproduce uma atribuição de partição. Utilizar uma chave de partição garante que todos os Olá eventos com Olá a mesma chave são enviados toohello mesma partição do hub de eventos de Olá. As chaves de partição comuns incluem os IDs de sessão do utilizador e os IDs do remetente exclusivos. Olá [PartitionKey][] propriedade é opcional e pode ser fornecida quando utilizar Olá [Microsoft](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) ou [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) métodos. Se não fornecer um valor para [PartitionKey][], enviados eventos são distribuídas toopartitions através de um modelo round robin.

### <a name="availability-considerations"></a>Considerações de disponibilidade

Utilizar uma chave de partição é opcional e, pondere cuidadosamente se pretende ou não toouse um. Em muitos casos, a utilização de uma chave de partição é uma boa opção se a ordenação de eventos é importante. Quando utiliza uma chave de partição, estas partições necessitam de disponibilidade num único nó e podem ocorrer falhas ao longo do tempo; Por exemplo, quando computação reinício de nós e patch. Como tal, se definir um ID de partição e que partição fica indisponível por algum motivo, um tentativa de tooaccess Olá os dados dessa partição irão falhar. Se elevada disponibilidade é mais importante, não especifique uma chave de partição; Nesse caso eventos serão enviados toopartitions utilizando o modelo round robin de Olá descrito anteriormente. Neste cenário, estiver a efetuar uma opção explícita entre disponibilidade (ID de partição) e consistência (ID de partição tooa de eventos de afixação).

Outra consideração está a processar atrasos no processamento de eventos. Em alguns casos, poderá ser melhor toodrop dados e repita que tootry e manter-se com o processamento, que pode provocar, potencialmente, atrasos de mais processamento a jusante. Por exemplo, com um ticker as cotações é melhor toowait para dados atualizados concluídos, mas num chat em direto ou cenário VOIP seria em vez disso tiver Olá dados rapidamente, mesmo que não está concluída.

Fornecido estas considerações de disponibilidade, nestes cenários, poderá escolher uma das seguintes estratégias de processamento de erros de Olá:

- Parar (paragem ler a partir de Event Hubs até que sejam corrigidas coisas)
- Remover (mensagens não são importantes, largue-os)
- Repita (Olá de novamente mensagens como ver cabem)
- [Entregues](../service-bus-messaging/service-bus-dead-letter-queues.md) (utilize uma fila ou outro toodead de hub de eventos letra só Olá mensagens não conseguiu processar)

Para obter mais informações e ver um debate sobre Olá trade-offs entre a disponibilidade e consistência, consulte [disponibilidade e a consistência no Event Hubs](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Operações de envio de eventos em lote
Enviar eventos em lotes pode aumentar substancialmente o débito. Olá [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) método um **IEnumerable** parâmetro do tipo [EventData][] e envia Olá lote inteiro como um hub de eventos de toohello operação atómica.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Tenha em atenção que um único lote não deve exceder o limite de 256 KB Olá de um evento. Além disso, cada mensagem no lote de Olá utiliza Olá mesma identidade do publicador. É responsabilidade Olá de Olá remetente tooensure que Olá batch não exceder o tamanho máximo do evento de Olá. Se exceder esse tamanho, é gerado um erro **Enviar** do cliente.

## <a name="send-asynchronously-and-send-at-scale"></a>Enviar no modo assíncrono e enviar à escala
Também pode enviar hub de eventos de tooan de eventos no modo assíncrono. Enviar no modo assíncrono pode aumentar a taxa de Olá em que um cliente é capaz de toosend eventos. Ambos os Olá [enviar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) e [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) métodos estão disponíveis em versões assíncronas que devolvem um [tarefas](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) objeto. Enquanto esta técnica pode aumentar o débito, este pode também fazer com que Olá eventos do cliente toocontinue toosend mesmo quando este está a ser limitado por Olá serviço dos Event Hubs e pode resultar em falhas de com Olá cliente ou mensagens perdidas se não for implementada corretamente. Além disso, pode utilizar Olá [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) propriedade Olá cliente toocontrol cliente as opções de repetição.

## <a name="create-a-partition-sender"></a>Criar um remetente de partição
Embora seja mais comuns toosend eventos tooan hub de eventos sem uma chave de partição, em alguns casos poderá toosend eventos diretamente tooa fornecido partição. Por exemplo:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) devolve um [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) que pode utilizar partição do hub de eventos específico toopublish eventos tooa de objeto.

## <a name="event-consumers"></a>Consumidores de eventos
Os Event Hubs possuem dois modelos principais para o consumo de eventos: recetores diretos e abstrações de nível superior, tais como [EventProcessorHost][]. Os recetores diretos são responsáveis pela sua própria coordenação de acesso toopartitions dentro de um grupo de consumidores.

### <a name="direct-consumer"></a>Consumidor direto
Olá tooread de forma mais direta de uma partição dentro de um grupo de consumidores é toouse Olá [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) classe. toocreate uma instância desta classe, tem de utilizar uma instância de Olá [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) classe. No seguinte exemplo de Olá, ID de partição Olá tem de ser especificado ao criar o recetor Olá para o grupo de consumidores Olá.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

Olá [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) método tem várias sobrecargas que facilitam o controlo sobre o leitor de Olá a ser criada. Estes métodos incluem a especificação de um desvio como uma cadeia ou timestamp e Olá toospecify capacidade se tooinclude este desvio especificado na Olá devolvido transmitir ou iniciar depois. Depois de criar o recetor Olá, pode começar a receber eventos no Olá devolvida objeto. Olá [Receive](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) o método tem quatro sobrecargas que Olá controlo receber parâmetros de operação, por exemplo, tamanho de lote e aguarde algum tempo. Pode utilizar versões assíncronas Olá estes métodos tooincrease Olá débito um consumidor. Por exemplo:

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

Com relativamente tooa de partição específica, mensagens hello são recebidas na ordem Olá em que foram enviadas toohello hub de eventos. o desvio de Olá é uma cadeia token utilizado tooidentify uma mensagem numa partição.

Tenha em atenção que uma única partição dentro de um grupo de consumidores não pode ter mais de 5 leitores simultâneos ligados em qualquer altura. Como os leitores se ligam ou desligam, as respetivas sessões poderão permanecer ativas durante vários minutos antes do serviço de Olá reconhece que estes se desligaram. Durante este período, a partição tooa restabelecer a ligação poderá falhar. Para obter um exemplo completo de escrever um recetor direto para os Event Hubs, consulte Olá [Recetores diretos de Hubs de eventos](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) exemplo.

### <a name="event-processor-host"></a>Anfitrião do processador de eventos
Olá [EventProcessorHost][] classe processa dados dos Event Hubs. Deve utilizar esta implementação quando criar os leitores dos eventos na plataforma de .NET Olá. O [EventProcessorHost][] fornece um ambiente de tempo de execução seguro para thread com vários processos para as implementações do processador de eventos que também fornece pontos de verificação e gestão da concessão da partição.

Olá toouse [EventProcessorHost][] classe, pode implementar [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor). Esta interface contém três métodos:

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

processamento de eventos de toostart instanciar [EventProcessorHost][], fornecendo os parâmetros adequados Olá para o seu hub de eventos. Em seguida, chame [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister sua [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) implementação com Olá tempo de execução. Neste momento, o anfitrião de Olá tentará tooacquire uma concessão em cada partição num hub de eventos de Olá utilizando um algoritmo "abrangente". Estas concessões duram um determinado período de tempo e, em seguida, têm de ser renovadas. Como novos nós, instâncias de trabalho neste caso, fique online, colocam reservas de concessões e ao longo do tempo carga Olá desvia entre nós como cada uma tenta tooacquire mais concessões.

![Anfitrião do Processador de Eventos](./media/event-hubs-programming-guide/IC759863.png)

Ao longo do tempo, é estabelecido um equilíbrio. Esta capacidade dinâmica permite que o dimensionamento automático baseado em CPU tooconsumers de toobe aplicada para ambos aumentar verticalmente e horizontalmente. Porque os Event Hubs não têm um conceito direto de contagens de mensagens, a utilização média da CPU é, frequentemente, Olá melhor mecanismo toomeasure back-end ou o consumidor escala. Se os publicadores começarem toopublish que mais eventos que os consumidores podem processar, Olá aumento de CPU nos consumidores pode ser utilizado toocause um dimensionamento automático na contagem de instâncias de trabalho.

Olá [EventProcessorHost][] classe também implementa um mecanismo de pontos de verificação de baseado no armazenamento do Azure. Este Olá de arquivos de mecanismo desvio numa base por partição, para que cada consumidor possa determinar que Olá último ponto de verificação do consumidor anterior Olá foi. Tal como a transição das partições entre nós por concessões, este é o mecanismo de sincronização de Olá que facilita a deslocação da carga.

## <a name="publisher-revocation"></a>Revogação do publicador
Além disso toohello avançadas funcionalidades de tempo de execução do [EventProcessorHost][], os Event Hubs permitem a revogação do publicador na ordem tooblock específico os publicadores de enviar o hub de eventos do evento tooan. Estas funcionalidades são particularmente úteis se um token do publicador tiver ficado comprometido ou se uma atualização de software está a causá-los toobehave inadequada. Nestas situações, identidade do publicador Olá, o que faz parte do respetivo token SAS, pode ser impedida de publicar eventos.

Para obter mais informações sobre a revogação do publicador e como toosend tooEvent Hubs como publicador, consulte o artigo Olá [Event Hubs grande escala publicação segura](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) exemplo.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre cenários dos Event Hubs, visite estas ligações:

* [Descrição geral da API dos Hubs de Eventos](event-hubs-api-overview.md)
* [Novidades dos Event Hubs](event-hubs-what-is-event-hubs.md)
* [Disponibilidade e consistência em Hubs de Eventos](event-hubs-availability-and-consistency.md)
* [Event processor host API reference (Referência da API do anfitrião do processador de eventos)](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
