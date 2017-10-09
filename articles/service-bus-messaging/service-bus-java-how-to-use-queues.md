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
# <a name="how-toouse-service-bus-queues-with-java"></a>Como toouse Service Bus são filas com Java
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este artigo descreve como toouse filas do Service Bus. Exemplos de Olá são escritos em Java e utilizar Olá [Azure SDK para Java][Azure SDK for Java]. Olá os cenários abrangidos incluem **criar filas**, **enviar e receber mensagens**, e **eliminar filas**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar o seu toouse aplicação de Service Bus
Certifique-se de que instalou Olá [Azure SDK para Java] [ Azure SDK for Java] antes de criar este exemplo. Se estiver a utilizar Eclipse, pode instalar Olá [Toolkit do Azure para o Eclipse] [ Azure Toolkit for Eclipse] que inclua Olá Azure SDK para Java. Em seguida, pode adicionar Olá **bibliotecas do Microsoft Azure para Java** tooyour projeto:

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Adicione Olá seguinte `import` parte superior do toohello de declarações do ficheiro de Java de Olá:

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>Criar uma fila
Operações de gestão para filas do Service Bus podem ser efetuadas através de **ServiceBusContract** classe. A **ServiceBusContract** objecto é construído com uma configuração apropriada que encapsula o token SAS com permissões toomanage e Olá **ServiceBusContract** classe é ponto único de Olá de comunicação com o Azure.

Olá **ServiceBusService** classe fornece métodos toocreate, enumerar e eliminar filas. Olá o exemplo abaixo mostra como um **ServiceBusService** objeto pode ser utilizado toocreate com o nome de uma fila `TestQueue`, com um espaço de nomes com o nome `HowToSample`:

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

Existem métodos em `QueueInfo` que permitem que as propriedades de Olá fila toobe otimizados (por exemplo: tooset Olá predefinido time-to-live (TTL) valor toobe aplicada toomessages enviados toohello fila). Olá exemplo seguinte mostra como toocreate uma fila com o nome `TestQueue` com um tamanho máximo de 5 GB:

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Tenha em atenção que pode utilizar Olá `listQueues` método no **ServiceBusContract** objetos toocheck se uma fila com um nome especificado já existe num espaço de nomes do serviço.

## <a name="send-messages-tooa-queue"></a>Enviar tooa a fila de mensagens
uma fila do Service Bus tooa toosend, a aplicação obtém um **ServiceBusContract** objeto. Olá a seguir mostra código como toosend uma mensagem para Olá `TestQueue` fila criada anteriormente no Olá `HowToSample` espaço de nomes:

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

As mensagens enviadas para e recebido do Service Bus as filas são instâncias de Olá [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de propriedades padrão (tais como [etiqueta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), um dicionário que é utilizado toohold personalizado propriedades específicas da aplicação e um corpo de dados arbitrários da aplicação. Uma aplicação pode definir o corpo de Olá da mensagem de saudação através da transmissão de qualquer objeto serializável para construtor de Olá de Olá [BrokeredMessage][BrokeredMessage], e, em seguida, irá ser utilizado o serializador adequado Olá objeto de Olá tooserialize. Em alternativa, pode fornecer um **java. E/S. InputStream** objeto.

Olá exemplo seguinte demonstra como teste toosend cinco mensagens toothe `TestQueue` **MessageSender** foi obtido no fragmento de código anterior Olá:

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

Filas do Service Bus suportam um tamanho da mensagem máximo de 256 KB no Olá [escalão Standard](service-bus-premium-messaging.md) e de 1 MB no Olá [escalão Premium](service-bus-premium-messaging.md). cabeçalho de Olá, que inclui a norma de Olá e propriedades de aplicação personalizada, pode ter um tamanho máximo de 64 KB. Não há nenhum limite do número de Olá de mensagens contidas numa fila mas não existe um limite no tamanho total do Olá das mensagens hello contidas numa fila. O tamanho da fila é definido no momento de criação, com um limite superior de 5 GB.

## <a name="receive-messages-from-a-queue"></a>Receber mensagens a partir de uma fila
mensagens Hello do tooreceive forma primária de uma fila é toouse um **ServiceBusContract** objeto. Mensagens recebidas podem funcionar em dois modos diferentes: **ReceiveAndDelete** e **PeekLock**.

Quando utilizar Olá **ReceiveAndDelete** modo, receber é uma operação única - ou seja, quando o Service Bus recebe um pedido de leitura de uma mensagem numa fila, marca Olá mensagem como consumida e devolve a mesma aplicação toohello. **ReceiveAndDelete** modo (que é o modo predefinido de Olá) é Olá de modelo mais simples e funciona melhor para cenários em que uma aplicação pode tolerar o não processamento de uma mensagem no evento Olá de uma falha. toounderstand isto, considere um cenário no quais problemas de consumidor Olá Olá receber o pedido e, em seguida, falhas antes do processamento-lo.
Porque o Service Bus terá marcado Olá mensagem como consumida, em seguida, quando a aplicação Olá reinicia e começa a consumir novamente mensagens, terá perdido mensagem de saudação foi consumida falhas toohello anterior.

No **PeekLock** modo, receção torna-se uma operação de duas fases, o que torna possível toosupport aplicações que não toleram mensagens em falta. Quando o Service Bus recebe um pedido, localiza Olá seguinte toobe de mensagem consumida, bloqueia-tooprevent outros consumidores receção e, em seguida, devolve a mesma aplicação toohello. Após a aplicação Olá concluir o processamento da mensagem de saudação (ou armazena a mesma forma fiável para processamento futuro), conclui Olá segunda etapa do Olá processo de receção ao chamar **eliminar** na mensagem de saudação recebida. Quando o Service Bus vê Olá **eliminar** chamada, irá marcar a mensagem de saudação como consumida e removê-lo a partir da fila de Olá.

Olá exemplo seguinte demonstra como podem ser recebidas mensagens e processados utilizando **PeekLock** modo (não Olá predefinido). Olá exemplo abaixo não um ciclo infinito e processa mensagens à medida que chegam no nosso `TestQueue`:

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como falhas de aplicação toohandle e mensagens ilegíveis
O Service Bus fornece toohelp funcionalidade que recuperar corretamente de erros na sua aplicação ou problemas no processamento de uma mensagem. Se uma aplicação recetora não é possível tooprocess Olá mensagem por algum motivo, em seguida, pode chamar Olá **unlockMessage** método na mensagem de saudação recebida (em vez de Olá **deleteMessage** método). Este causas Olá toounlock de barramento de serviço de mensagens em fila Olá e torná-lo disponível toobe novamente recebida, quer por Olá mesmo consumir aplicação ou por outra aplicação de consumo.

Há também um tempo limite associado à mensagem bloqueada na fila, e se a aplicação Olá falha tooprocess Olá mensagem antes do tempo limite de bloqueio expira (por exemplo, se a falha da aplicação Olá), em seguida, Service Bus desbloqueia automaticamente Olá mensagem e torna disponível toobe recebida novamente.

No Olá eventos Olá aplicação falhas após o processamento da mensagem de saudação mas antes do Olá **deleteMessage** pedido é emitido, em seguida, mensagem de saudação é reenviada toohello aplicação quando esta reiniciar. Isto é frequentemente designado *, pelo menos, uma vez processamento*; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações a mesma mensagem poderá ser reenviada. Se o cenário de Olá não conseguir tolerar o processamento duplicado, os programadores da aplicação devem adicionar entrega da mensagem duplicada toohandle lógica adicional tootheir aplicação. Isto é, frequentemente, conseguido utilizando Olá **getMessageId** método de mensagem de saudação, que permanece constante nas tentativas de entrega.

## <a name="next-steps"></a>Passos Seguintes
Agora que aprendeu as noções básicas de Olá de filas do Service Bus, consulte [filas, tópicos e subscrições] [ Queues, topics, and subscriptions] para obter mais informações.

Para obter mais informações, consulte Olá [Centro de programadores Java](https://azure.microsoft.com/develop/java/).

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
