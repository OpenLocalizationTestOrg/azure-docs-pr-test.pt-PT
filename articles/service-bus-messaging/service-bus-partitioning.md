---
title: "aaaCreate particionada tópicos e filas do Service Bus do Azure | Microsoft Docs"
description: "Descreve como os corretores toopartition filas do Service Bus e tópicos, utilizando vários mensagem."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>Filas e tópicos particionados
Service Bus do Azure emprega várias mensagens de tooprocess de mediadores de mensagens e várias mensagens armazena mensagens toostore. Uma fila convencional ou um tópico é processado por um mediador de mensagens única e armazenado num arquivo de mensagens. Barramento de serviço *partições* ativar as filas e tópicos, ou *entidades de mensagens*, toobe particionado em vários mediadores de mensagens e arquivos de mensagens. Isto significa que Olá débito global de uma entidade particionada já não é limitada pelo desempenho Olá de um mediador de mensagens única ou um arquivo de mensagens. Além disso, uma falha temporária de um arquivo de mensagens não compor uma fila particionada ou um tópico indisponível. Particionada filas e tópicos podem conter avançadas todas as funcionalidades de Service Bus, como o suporte para transações e sessões.

Para obter informações sobre as características de Service Bus, consulte Olá [arquitetura do Service Bus] [ Service Bus architecture] artigo.

Criação de partições é ativada por predefinição durante a criação de entidade em todas as filas e tópicos Standard e Premium mensagens. Pode criar padrão entidades de camada de mensagens sem a criação de partições, mas as filas e tópicos num espaço de nomes Premium sempre de ser particionados; Não é possível desativar esta opção. 

Não é possível toochange Olá criação de partições opção numa fila existente ou tópico em camadas Standard ou Premium, só é possível definir a opção de Olá quando criar entidade Olá.

## <a name="how-it-works"></a>Como funciona

Cada fila particionada ou um tópico é composta por vários fragmentos. Cada fragmento é armazenado num arquivo de mensagens diferentes e processado por um mediador de mensagens diferentes. Quando é enviada uma mensagem de fila particionada tooa ou um tópico, o Service Bus atribui Olá mensagem tooone dos fragmentos Olá. seleção de Olá é feita aleatoriamente ao Service Bus ou utilizando uma chave de partição Olá remetente pode especificar.

Quando um cliente pretende tooreceive uma mensagem numa fila particionada ou de um subscrição tooa particionada tópico, o Service Bus consulta todos os fragmentos para mensagens, em seguida, devolve o primeiro mensagem de saudação que é obtida a partir de qualquer Olá recetor toohello de arquivos de mensagens. Caches de Service Bus Olá outras mensagens e devolve-las quando recebe adicionais recebem pedidos. Um cliente receber não está ciente de criação de partições Olá; Olá comportamento com clientes de uma fila particionada ou um tópico (por exemplo, ler, concluir, diferir, mensagens não entregues, prefetching) é idêntica toohello comportamento de uma entidade regular.

Não há sem custos adicionais quando uma mensagem a enviar ou receber uma mensagem de fila particionada ou tópico.

## <a name="enable-partitioning"></a>Ativar a criação de partições

toouse particionada filas e tópicos com o Service Bus do Azure, utilize Olá Azure SDK versão 2.2 ou posterior, ou especifique `api-version=2013-10` no seu HTTP pedidos.

### <a name="standard"></a>Standard

Na camada de serviço de mensagens Standard de Olá, pode criar filas do Service Bus e tópicos em tamanhos de 1, 2, 3, 4 ou 5 GB (a predefinição de Olá é 1 GB). Com a criação de partições ativada, o Service Bus cria 16 cópias (16 partições) da entidade de Olá de cada GB que especificar. Como tal, se criar uma fila que é de 5 GB de tamanho, com 16 partições Olá tamanho máximo da fila fique (5 \* 16) = 80 GB. Pode ver o tamanho máximo do Olá da sua fila particionada ou tópico observando a entrada no Olá [portal do Azure][Azure portal], no Olá **descrição geral** painel para essa entidade.

### <a name="premium"></a>Premium

Um espaço de nomes de escalão Premium, pode criar filas do Service Bus e tópicos em tamanhos de 1, 2, 3, 4, 5, 10, 20, 40 ou 80 GB (a predefinição de Olá é 1 GB). Com a criação de partições ativada por predefinição, o Service Bus cria duas partições por entidade. Pode ver o tamanho máximo do Olá da sua fila particionada ou tópico observando a entrada no Olá [portal do Azure][Azure portal], no Olá **descrição geral** painel para essa entidade.

Para obter mais informações sobre a criação de partições no escalão de serviço de mensagens hello Premium, consulte [Premium do Service Bus e escalões de mensagens Standard](service-bus-premium-messaging.md). 

### <a name="create-a-partitioned-entity"></a>Criar uma entidade particionada

Existem várias formas toocreate uma fila particionada ou tópico. Quando criar a fila de Olá ou um tópico da sua aplicação, pode ativar a criação de partições para Olá fila ou um tópico por respetivamente Olá de definição [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] ou [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] propriedade demasiado**verdadeiro**. Estas propriedades tem de ser definidas na fila de Olá Olá tempo ou tópico é criado. Conforme indicado anteriormente, é toochange não é possível estas propriedades numa fila existente ou tópico. Por exemplo:

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Em alternativa, pode criar uma fila particionada ou um tópico no Olá [portal do Azure] [ Azure portal] ou no Visual Studio. Quando cria uma fila ou um tópico no portal de Olá, Olá **ativar a criação de partições** opção na fila de Olá ou um tópico **criar** painel está selecionado por predefinição. Só pode desativar esta opção na entidade de escalão Standard; Olá criação de partições de escalão Premium está sempre ativada. No Visual Studio, clique em Olá **ativar partições** caixa de verificação no Olá **nova fila** ou **novo tópico** caixa de diálogo.

## <a name="use-of-partition-keys"></a>Utilização de chaves de partição
Quando uma mensagem é colocados em fila para uma fila particionada ou um tópico, o barramento de serviço verifica a existência de presença de Olá de uma chave de partição. Se localizar alguma, seleciona fragmento Olá com base nessa chave. Se encontrar uma chave de partição, seleciona fragmento Olá com base no algoritmo interno.

### <a name="using-a-partition-key"></a>Utilizar uma chave de partição
Alguns cenários, tais como sessões ou de transações, requerem toobe mensagens armazenado um fragmento específico. Todos estes cenários exigem a utilização de Olá de uma chave de partição. Todas as mensagens que Olá de utilização são atribuídas a mesma chave de partição toohello mesmo fragmento. Se o fragmento de Olá está temporariamente indisponível, o Service Bus devolve um erro.

Dependendo do cenário de Olá, as propriedades da mensagem diferentes são utilizadas como uma chave de partição:

**SessionId**: se uma mensagem tiver Olá [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] propriedade definida, em seguida, o Service Bus utiliza esta propriedade como chave de partição Olá. Desta forma, todas as mensagens que pertencem toohello mesma sessão são processadas pelo Olá mesmo Mediador de mensagens. Isto permite que a mensagem do barramento de serviço tooguarantee de ordenação, bem como a consistência de Olá dos Estados de sessão.

**PartitionKey**: se uma mensagem tiver Olá [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propriedade mas não Olá [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] propriedade definida, em seguida, o Service Bus utiliza Olá [PartitionKey] [ PartitionKey] propriedade como chave de partição Olá. Se a mensagem de saudação tem ambos os Olá [SessionId] [ SessionId] e Olá [PartitionKey] [ PartitionKey] conjunto de propriedades, ambas as propriedades devem ser idênticas. Se hello [PartitionKey] [ PartitionKey] propriedade está definida tooa outro valor que Olá [SessionId] [ SessionId] propriedade, o Service Bus devolve um inválido Exceção de operação. Olá [PartitionKey] [ PartitionKey] propriedade deve ser utilizada se um remetente envia mensagens transacionais de conhecimento não são de sessão. Olá chave de partição garante que todas as mensagens que são enviadas dentro de uma transação são processadas pelo Olá mesmo Mediador de mensagens.

**MessageId**: se Olá fila ou um tópico tem Olá [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] propriedade definida demasiado**verdadeiro** e Olá [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] ou [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propriedades não estão definidas, em seguida, Olá [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] propriedade serve como chave de partição Olá. (Tenha em atenção de que o Microsoft .NET e AMQP bibliotecas ligadas Olá atribuir automaticamente um ID de mensagem se a aplicação de envio de Olá não.) Neste caso, todas as cópias do Olá mesma mensagem são processadas pelo Olá mesmo Mediador de mensagens. Isto permite que o Service Bus toodetect e eliminar mensagens duplicadas. Se hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] propriedade não está definida demasiado**verdadeiro**, Service Bus considere Olá [MessageId] [ MessageId] propriedade como uma chave de partição.

### <a name="not-using-a-partition-key"></a>Não utilizar uma chave de partição
Na ausência de Olá de uma chave de partição, o Service Bus distribui as mensagens de fragmentos de Olá de tooall uma maneira round-robin da fila particionada Olá ou um tópico. Se o fragmento de Olá escolhido não estiver disponível, o Service Bus atribui fragmento do Olá mensagem tooa diferentes. Desta forma, a operação de envio de Olá é bem-sucedida, apesar de indisponibilidade temporária do Olá de um arquivo de mensagens. No entanto, não irá conseguir Olá garantida ordenação que fornece uma chave de partição.

Para um debate mais aprofundado de compromisso de Olá entre disponibilidade (nenhuma chave de partição) e consistência (utilizando uma chave de partição), consulte [neste artigo](../event-hubs/event-hubs-availability-and-consistency.md). Estas informações aplicam-se igualmente toopartitioned entidades de Service Bus e partições de Event Hubs.

toogive serviço barramento suficiente mensagem de saudação do tempo tooenqueue para um fragmento diferentes, hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] valor especificado pelo cliente de Olá que envia a mensagem de saudação tem de ser superior a 15 segundos. É recomendável que defina Olá [OperationTimeout] [ OperationTimeout] toohello predefinido o valor da propriedade de 60 segundos.

Tenha em atenção que uma chave de partição "pins" um fragmento de específica de tooa de mensagem. Se o arquivo de mensagens hello que detém este fragmento do não estiver disponível, o Service Bus devolve um erro. Na ausência de Olá de uma chave de partição, Service Bus pode escolher um fragmento diferentes e operação Olá for bem sucedida. Por conseguinte, é recomendado que não fornecer uma chave de partição, exceto se for necessário.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>Tópicos de avançadas: utilizar transações com entidades particionadas
As mensagens que são enviadas como parte de uma transação tem de especificar uma chave de partição. Isto pode ser uma das seguintes propriedades de Olá: [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], ou [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]. Todas as mensagens que são enviadas como parte da mesma transação tem de especificar de Olá Olá a mesma chave de partição. Se tentar toosend uma mensagem sem uma chave de partição dentro de uma transação, o Service Bus devolve uma exceção de operação inválido. Se tentar toosend Olá, várias mensagens na mesma transação que possuem diferentes chaves de partição, o Service Bus devolve uma exceção de operação inválido. Por exemplo:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

Se qualquer uma das propriedades de Olá que funcionam como uma chave de partição forem definidas, pins de Service Bus Olá fragmento específico de tooa de mensagem. Este comportamento ocorre se ou não é utilizada uma transação. É recomendado que não especificou uma chave de partição se não for necessário.

## <a name="using-sessions-with-partitioned-entities"></a>Utilizar sessões com entidades particionadas
toosend um tópico com suporte para a sessão de tooa de mensagens transacionais ou fila, mensagem de saudação tem de ter Olá [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] propriedade definida. Se hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] é especificada, bem como a propriedade, tem de ser idêntica toohello [SessionId] [ SessionId] propriedade. Caso sejam diferentes, o Service Bus devolve uma exceção de operação inválido.

Ao contrário das filas regulares (não particionadas) ou tópicos, não é possível toouse toosend uma única transação várias sessões de toodifferent de mensagens. Se for tentada, o Service Bus devolve uma exceção de operação inválido. Por exemplo:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>Reencaminhamento de mensagens automática com entidades particionadas
Service Bus suporta mensagem automática de reencaminhamento da, para ou entre entidades particionadas. mensagem automática tooenable reencaminhamento, defina Olá [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] propriedade na fila de origem Olá ou na subscrição. Se a mensagem de saudação Especifica uma chave de partição ([SessionId][SessionId], [PartitionKey][PartitionKey], ou [MessageId] [ MessageId]), essa chave de partição é utilizada para a entidade de destino Olá.

## <a name="considerations-and-guidelines"></a>Considerações e diretrizes
* **Funcionalidades de consistência elevada**: se uma entidade utiliza funcionalidades como sessões, deteção duplicada ou controlo explícito de chave de criação de partições, em seguida, as operações de mensagens de Olá são sempre fragmentos encaminhados toospecific. Se qualquer um dos fragmentos Olá experiência de tráfego elevado ou arquivo subjacente Olá está danificado, essas operações falharem e disponibilidade é reduzida. Em geral, é ainda muito superior a entidades particionadas não; consistência Olá apenas um subconjunto de tráfego está com problemas, como tráfego de Olá tooall oposição ao. Para obter mais informações, consulte este [debate de disponibilidade e consistência](../event-hubs/event-hubs-availability-and-consistency.md).
* **Gestão**: operações, tais como criar, atualizar e eliminar tem de ser efetuadas em todos os fragmentos de Olá da entidade de Olá. Se qualquer fragmento é mau estado de funcionamento pode resultar em falhas para estas operações. Para a operação de Get Olá, informações tais como contagens de mensagem tem de ser agregadas a partir de todos os fragmentos. Se qualquer fragmento é mau estado de funcionamento, o estado de disponibilidade de entidade Olá é reportado como limitado.
* **Cenários de mensagem de volume de baixa**: para tais cenários, especialmente quando utilizar o protocolo de Olá HTTP, poderá ter tooperform vários receber operações na ordem tooobtain todas as mensagens de Olá. Para receber pedidos, front-end de Olá executa receber em todos os fragmentos de Olá e coloca em cache todas as respostas de Olá recebidas. Um pedido de receção subsequentes no Olá mesma ligação seria beneficiar Esta colocação em cache e receber latências será inferior. No entanto, se tiver várias ligações ou utilizar HTTP, que estabelece uma ligação nova para cada pedido. Como tal, não há nenhuma garantia de que este seria apresentado no Olá mesmo nó. Se a todas as mensagens existentes estão bloqueadas e em cache no outro front-end, Olá receber operação devolve **nulo**. Mensagens eventualmente expirarem e pode recebê-las novamente. Recomenda-se a ligação keep-alive de HTTP.
* **Procurar/observar mensagens**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) não devolver sempre Olá número de mensagens especificado no Olá [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) propriedade. Existem duas razões comuns para este. Uma razão é que Olá agregado tamanho da colecção de Olá de mensagens de excede o tamanho máximo do Olá de 256KB. Outra razão é que, se Olá fila ou um tópico tem Olá [EnablePartitioning propriedade](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) definido demasiado**verdadeiro**, uma partição poderá não ter suficiente mensagens toocomplete Olá solicitado o número de mensagens. Em geral, se uma aplicação quiser tooreceive um número específico de mensagens em fila, deve chamar [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) repetidamente até que obtém esse número de mensagens em fila ou não existem nenhum mais toopeek de mensagens. Para obter mais informações, incluindo exemplos de código, consulte [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) ou [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_).

## <a name="latest-added-features"></a>Mais recentes funcionalidades adicionadas
* Adicionar ou remover a regra é agora suportada com entidades particionadas. Diferentes das entidades não particionadas, estas operações não são suportadas em transações. 
* AMQP é agora suportado para enviar e receber mensagens tooand a partir de uma entidade particionada.
* AMQP é agora suportado para Olá seguintes operações: [Batch enviar](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [Batch receber](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [Receive pelo número de sequência](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [observar](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ Renovar bloqueio](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [agendar mensagem](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [Cancelar mensagem agendada](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [Adicionar regra](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [remover a regra](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Bloqueio de renovação de sessão](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [estado da sessão conjunto](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [obter estado da sessão](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), e [enumerar sessões](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync).

## <a name="partitioned-entities-limitations"></a>Limitações de entidades particionadas
Atualmente o Service Bus impõe Olá seguindo limitações do particionada filas e tópicos:

* Particionada filas e tópicos não suportam o envio de mensagens que pertencem toodifferent sessões numa única transação.
* Service Bus permite atualmente too100 particionada filas ou tópicos por espaço de nomes. Cada fila particionada ou um tópico conta para a quota de Olá de 10 000 entidades por espaço de nomes (não é aplicável tooPremium camada).

## <a name="next-steps"></a>Passos seguintes
Consulte a discussão Olá de [AMQP 1.0 suporte para o Service Bus particionada filas e tópicos] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn mais informações sobre a criação de partições de entidades de mensagens. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
