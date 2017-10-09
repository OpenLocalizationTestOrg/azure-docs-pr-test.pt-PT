---
title: filas de aaaService Bus entregues | Microsoft Docs
description: "Descrição geral de filas do Service Bus do Azure entregues"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>Descrição geral de filas do Service Bus entregues

Filas do Service Bus e subscrições proporcionam uma fila secundárias secundária, chamada um *entregues fila* (DLQ). fila de entregues Olá não precisa de toobe explicitamente criado e não pode ser eliminado ou de outra forma independente gerido da entidade principal Olá.

Este artigo aborda entregues filas no Service Bus do Azure. Muitas das debate Olá é ilustrada Olá [exemplo entregues filas](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) no GitHub.
 
## <a name="hello-dead-letter-queue"></a>fila de entregues Olá

objetivo de Olá da fila de entregues Olá é toohold mensagens que não não possível entregar tooany recetor ou mensagens que não foi possível processar. As mensagens podem ser removidas Olá DLQ e inspecionadas. Uma aplicação poderá, com a ajuda de um operador, corrigir problemas e submeta novamente a mensagem de saudação, facto Olá que ocorreu um erro de registo e tomar uma ação corretiva. 

Perspetiva de um protocolo e a API, Olá DLQ é principalmente semelhante tooany outra fila, exceto que só podem ser submetidas mensagens através do gesto de entregues Olá da entidade de principal de Olá. Além disso, a time-to-live não é observados, e não é uma mensagem de um DLQ entregues. fila de entregues Olá suporta totalmente operações transacionais e entrega de bloqueio peek.

Tenha em atenção que não há nenhum limpeza automática de Olá DLQ. Mensagens permanecem no Olá DLQ até obter explicitamente Olá DLQ e chamada [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) na mensagem de entregues Olá.

## <a name="moving-messages-toohello-dlq"></a>Mover mensagens toohello DLQ

Existem várias atividades no Service Bus que causam tooget de mensagens enviadas por push toohello DLQ de dentro de Olá mensagens do motor de si próprio. Uma aplicação explicitamente também pode mover mensagens toohello DLQ. 

Como mensagem de saudação obtém movida mediador Olá, duas propriedades são adicionadas toohello mensagem como mediador Olá chamadas a respetiva versão interno de Olá [mensagens não entregues](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) método na mensagem de saudação: `DeadLetterReason` e `DeadLetterErrorDescription`.

As aplicações podem definir os seus próprios códigos para Olá `DeadLetterReason` propriedade, mas Olá sistema conjuntos Olá os seguintes valores.

| Condição | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| Sempre |HeaderSizeExceeded |quota de tamanho de Olá para esta sequência foi excedido. |
| ! TopicDescription.<br />EnableFilteringMessagesBeforePublishing e SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |exceção. GetType(). Nome |exceção. Mensagem |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |mensagem de saudação expirou e foi inutilizado lettered. |
| SubscriptionDescription.RequiresSession |Id de sessão é nulo. |Entidade de sessão ativado não permite uma mensagem cujo identificador de sessão é nulo. |
| ! entregues fila |MaxTransferHopCountExceeded |Valor nulo |
| Aplicação explícita lettering inutilizado |Especificado por aplicação |Especificado por aplicação |

## <a name="exceeding-maxdeliverycount"></a>Exceder MaxDeliveryCount
As filas e subscrições têm um [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) e [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) propriedade respetivamente; hello o valor predefinido é 10. Sempre que uma mensagem tem sido entregar sob um bloqueio ([ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)), mas foi um explicitamente abandonado ou bloqueio Olá expirou, mensagem de saudação [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) é incrementado. Quando [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) excede [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), mensagem de saudação é movido toohello DLQ, especificando Olá `MaxDeliveryCountExceeded` pelo motivo código.

Não é possível desativar este comportamento, mas pode definir [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) número muito elevado de tooa.

## <a name="exceeding-timetolive"></a>TimeToLive excedesse
Quando Olá [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) ou [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) for definida demasiado**true** (é a predefinição de Olá **falso**), todas as mensagens de expiração são movida toohello DLQ, especificando Olá `TTLExpiredException` pelo motivo código.

Tenha em atenção que apenas são removidas e, por conseguinte, movido toohello DLQ quando existe, pelo menos, um recetor Active Directory extrair em fila principal Olá ou de subscrição; as mensagens de expirada Se o comportamento é por predefinição.

## <a name="errors-while-processing-subscription-rules"></a>Erros ao processar as regras de subscrição
Quando Olá [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) propriedade está ativada para uma subscrição, quaisquer erros que ocorrem enquanto executa a regra de filtro do SQL Server de uma subscrição são capturados num Olá DLQ juntamente com Olá inválida mensagem.

## <a name="application-level-dead-lettering"></a>Ao nível da aplicação mensagens não entregues
Na adição toohello fornecidos pelo sistema mensagens não entregues funcionalidades, as aplicações podem utilizar mensagens hello do DLQ tooexplicitly rejeitar inaceitável. Isto pode incluir as mensagens que não podem ser processadas corretamente devido a ordenação tooany de problema de sistema, as mensagens que contêm payloads com formato incorreto ou mensagens que falham a autenticação quando é utilizada o esquema algumas segurança ao nível da mensagem.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>Mensagens não entregues nos cenários ForwardTo ou SendVia

As mensagens serão enviados toohello fila de entregues transferências em Olá seguintes condições:

- Uma mensagem passa através de mais de 3 filas ou os tópicos [ligadas em cadeia](service-bus-auto-forwarding.md).
- fila de destino Olá ou um tópico, está desativado ou eliminado.
- Olá fila de destino ou um tópico excede o tamanho máximo de entidade de Olá.

tooretrieve estas mensagens lettered de mensagens não pode criar um recetor utilizando Olá [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) método do utilitário.

## <a name="example"></a>Exemplo
Olá seguinte fragmento de código cria um recetor de mensagem. No Olá receber ciclo para a fila principal Olá, código de Olá obtém a mensagem de saudação com [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_), que pede-lhe Olá mediador tooinstantly retorno qualquer mensagem prontamente disponível ou tooreturn com nenhum resultado. Se o código de Olá recebe uma mensagem,-lo imediatamente abandons, que incrementa Olá `DeliveryCount`. Depois do sistema Olá move Olá mensagem toohello DLQ, fila principal Olá está vazia e Olá sai do ciclo, como [ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) devolve **nulo**.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>Passos seguintes
Olá seguintes artigos para obter mais informações sobre as filas do Service Bus, consulte:

* [Introdução às filas do Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [As filas do Azure e o Service Bus filas em comparação comparadas](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

