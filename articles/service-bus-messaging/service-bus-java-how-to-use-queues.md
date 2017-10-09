---
title: filas aaaHow toouse Service Bus do Azure com o Java | Microsoft Docs
description: "Saiba como toouse Service Bus são filas no Azure. Exemplos de código escrito em Java."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="3d45c-104">Como toouse Service Bus são filas com Java</span><span class="sxs-lookup"><span data-stu-id="3d45c-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="3d45c-105">Este artigo descreve como toouse filas do Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3d45c-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="3d45c-106">Exemplos de Olá são escritos em Java e utilizar Olá [Azure SDK para Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="3d45c-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="3d45c-107">Olá os cenários abrangidos incluem **criar filas**, **enviar e receber mensagens**, e **eliminar filas**.</span><span class="sxs-lookup"><span data-stu-id="3d45c-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="3d45c-108">Configurar o seu toouse aplicação de Service Bus</span><span class="sxs-lookup"><span data-stu-id="3d45c-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="3d45c-109">Certifique-se de que instalou Olá [Azure SDK para Java] [ Azure SDK for Java] antes de criar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="3d45c-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="3d45c-110">Se estiver a utilizar Eclipse, pode instalar Olá [Toolkit do Azure para o Eclipse] [ Azure Toolkit for Eclipse] que inclua Olá Azure SDK para Java.</span><span class="sxs-lookup"><span data-stu-id="3d45c-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="3d45c-111">Em seguida, pode adicionar Olá **bibliotecas do Microsoft Azure para Java** tooyour projeto:</span><span class="sxs-lookup"><span data-stu-id="3d45c-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="3d45c-112">Adicione Olá seguinte `import` parte superior do toohello de declarações do ficheiro de Java de Olá:</span><span class="sxs-lookup"><span data-stu-id="3d45c-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="3d45c-113">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="3d45c-113">Create a queue</span></span>
<span data-ttu-id="3d45c-114">Operações de gestão para filas do Service Bus podem ser efetuadas através de **ServiceBusContract** classe.</span><span class="sxs-lookup"><span data-stu-id="3d45c-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="3d45c-115">A **ServiceBusContract** objecto é construído com uma configuração apropriada que encapsula o token SAS com permissões toomanage e Olá **ServiceBusContract** classe é ponto único de Olá de comunicação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="3d45c-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="3d45c-116">Olá **ServiceBusService** classe fornece métodos toocreate, enumerar e eliminar filas.</span><span class="sxs-lookup"><span data-stu-id="3d45c-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="3d45c-117">Olá o exemplo abaixo mostra como um **ServiceBusService** objeto pode ser utilizado toocreate com o nome de uma fila `TestQueue`, com um espaço de nomes com o nome `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="3d45c-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="3d45c-118">Existem métodos em `QueueInfo` que permitem que as propriedades de Olá fila toobe otimizados (por exemplo: tooset Olá predefinido time-to-live (TTL) valor toobe aplicada toomessages enviados toohello fila).</span><span class="sxs-lookup"><span data-stu-id="3d45c-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="3d45c-119">Olá exemplo seguinte mostra como toocreate uma fila com o nome `TestQueue` com um tamanho máximo de 5 GB:</span><span class="sxs-lookup"><span data-stu-id="3d45c-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="3d45c-120">Tenha em atenção que pode utilizar Olá `listQueues` método no **ServiceBusContract** objetos toocheck se uma fila com um nome especificado já existe num espaço de nomes do serviço.</span><span class="sxs-lookup"><span data-stu-id="3d45c-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="3d45c-121">Enviar tooa a fila de mensagens</span><span class="sxs-lookup"><span data-stu-id="3d45c-121">Send messages tooa queue</span></span>
<span data-ttu-id="3d45c-122">uma fila do Service Bus tooa toosend, a aplicação obtém um **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="3d45c-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="3d45c-123">Olá a seguir mostra código como toosend uma mensagem para Olá `TestQueue` fila criada anteriormente no Olá `HowToSample` espaço de nomes:</span><span class="sxs-lookup"><span data-stu-id="3d45c-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="3d45c-124">As mensagens enviadas para e recebido do Service Bus as filas são instâncias de Olá [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="3d45c-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="3d45c-125">[BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de propriedades padrão (tais como [etiqueta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), um dicionário que é utilizado toohold personalizado propriedades específicas da aplicação e um corpo de dados arbitrários da aplicação.</span><span class="sxs-lookup"><span data-stu-id="3d45c-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="3d45c-126">Uma aplicação pode definir o corpo de Olá da mensagem de saudação através da transmissão de qualquer objeto serializável para construtor de Olá de Olá [BrokeredMessage][BrokeredMessage], e, em seguida, irá ser utilizado o serializador adequado Olá objeto de Olá tooserialize.</span><span class="sxs-lookup"><span data-stu-id="3d45c-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="3d45c-127">Em alternativa, pode fornecer um **java. E/S. InputStream** objeto.</span><span class="sxs-lookup"><span data-stu-id="3d45c-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="3d45c-128">Olá exemplo seguinte demonstra como teste toosend cinco mensagens toothe `TestQueue` **MessageSender** foi obtido no fragmento de código anterior Olá:</span><span class="sxs-lookup"><span data-stu-id="3d45c-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="3d45c-129">Filas do Service Bus suportam um tamanho da mensagem máximo de 256 KB no Olá [escalão Standard](service-bus-premium-messaging.md) e de 1 MB no Olá [escalão Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="3d45c-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3d45c-130">cabeçalho de Olá, que inclui a norma de Olá e propriedades de aplicação personalizada, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="3d45c-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3d45c-131">Não há nenhum limite do número de Olá de mensagens contidas numa fila mas não existe um limite no tamanho total do Olá das mensagens hello contidas numa fila.</span><span class="sxs-lookup"><span data-stu-id="3d45c-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="3d45c-132">O tamanho da fila é definido no momento de criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="3d45c-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="3d45c-133">Receber mensagens a partir de uma fila</span><span class="sxs-lookup"><span data-stu-id="3d45c-133">Receive messages from a queue</span></span>
<span data-ttu-id="3d45c-134">mensagens Hello do tooreceive forma primária de uma fila é toouse um **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="3d45c-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="3d45c-135">Mensagens recebidas podem funcionar em dois modos diferentes: **ReceiveAndDelete** e **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="3d45c-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="3d45c-136">Quando utilizar Olá **ReceiveAndDelete** modo, receber é uma operação única - ou seja, quando o Service Bus recebe um pedido de leitura de uma mensagem numa fila, marca Olá mensagem como consumida e devolve a mesma aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="3d45c-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="3d45c-137">**ReceiveAndDelete** modo (que é o modo predefinido de Olá) é Olá de modelo mais simples e funciona melhor para cenários em que uma aplicação pode tolerar o não processamento de uma mensagem no evento Olá de uma falha.</span><span class="sxs-lookup"><span data-stu-id="3d45c-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="3d45c-138">toounderstand isto, considere um cenário no quais problemas de consumidor Olá Olá receber o pedido e, em seguida, falhas antes do processamento-lo.</span><span class="sxs-lookup"><span data-stu-id="3d45c-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="3d45c-139">Porque o Service Bus terá marcado Olá mensagem como consumida, em seguida, quando a aplicação Olá reinicia e começa a consumir novamente mensagens, terá perdido mensagem de saudação foi consumida falhas toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="3d45c-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="3d45c-140">No **PeekLock** modo, receção torna-se uma operação de duas fases, o que torna possível toosupport aplicações que não toleram mensagens em falta.</span><span class="sxs-lookup"><span data-stu-id="3d45c-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3d45c-141">Quando o Service Bus recebe um pedido, localiza Olá seguinte toobe de mensagem consumida, bloqueia-tooprevent outros consumidores receção e, em seguida, devolve a mesma aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="3d45c-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="3d45c-142">Após a aplicação Olá concluir o processamento da mensagem de saudação (ou armazena a mesma forma fiável para processamento futuro), conclui Olá segunda etapa do Olá processo de receção ao chamar **eliminar** na mensagem de saudação recebida.</span><span class="sxs-lookup"><span data-stu-id="3d45c-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="3d45c-143">Quando o Service Bus vê Olá **eliminar** chamada, irá marcar a mensagem de saudação como consumida e removê-lo a partir da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d45c-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="3d45c-144">Olá exemplo seguinte demonstra como podem ser recebidas mensagens e processados utilizando **PeekLock** modo (não Olá predefinido).</span><span class="sxs-lookup"><span data-stu-id="3d45c-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="3d45c-145">Olá exemplo abaixo não um ciclo infinito e processa mensagens à medida que chegam no nosso `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="3d45c-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3d45c-146">Como falhas de aplicação toohandle e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="3d45c-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="3d45c-147">O Service Bus fornece toohelp funcionalidade que recuperar corretamente de erros na sua aplicação ou problemas no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="3d45c-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3d45c-148">Se uma aplicação recetora não é possível tooprocess Olá mensagem por algum motivo, em seguida, pode chamar Olá **unlockMessage** método na mensagem de saudação recebida (em vez de Olá **deleteMessage** método).</span><span class="sxs-lookup"><span data-stu-id="3d45c-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="3d45c-149">Este causas Olá toounlock de barramento de serviço de mensagens em fila Olá e torná-lo disponível toobe novamente recebida, quer por Olá mesmo consumir aplicação ou por outra aplicação de consumo.</span><span class="sxs-lookup"><span data-stu-id="3d45c-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3d45c-150">Há também um tempo limite associado à mensagem bloqueada na fila, e se a aplicação Olá falha tooprocess Olá mensagem antes do tempo limite de bloqueio expira (por exemplo, se a falha da aplicação Olá), em seguida, Service Bus desbloqueia automaticamente Olá mensagem e torna disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="3d45c-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="3d45c-151">No Olá eventos Olá aplicação falhas após o processamento da mensagem de saudação mas antes do Olá **deleteMessage** pedido é emitido, em seguida, mensagem de saudação é reenviada toohello aplicação quando esta reiniciar.</span><span class="sxs-lookup"><span data-stu-id="3d45c-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="3d45c-152">Isto é frequentemente designado *, pelo menos, uma vez processamento*; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações a mesma mensagem poderá ser reenviada.</span><span class="sxs-lookup"><span data-stu-id="3d45c-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="3d45c-153">Se o cenário de Olá não conseguir tolerar o processamento duplicado, os programadores da aplicação devem adicionar entrega da mensagem duplicada toohandle lógica adicional tootheir aplicação.</span><span class="sxs-lookup"><span data-stu-id="3d45c-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="3d45c-154">Isto é, frequentemente, conseguido utilizando Olá **getMessageId** método de mensagem de saudação, que permanece constante nas tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="3d45c-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d45c-155">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="3d45c-155">Next Steps</span></span>
<span data-ttu-id="3d45c-156">Agora que aprendeu as noções básicas de Olá de filas do Service Bus, consulte [filas, tópicos e subscrições] [ Queues, topics, and subscriptions] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="3d45c-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="3d45c-157">Para obter mais informações, consulte Olá [Centro de programadores Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="3d45c-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
