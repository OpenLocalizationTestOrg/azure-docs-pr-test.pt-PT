---
title: aaaReceive eventos provenientes dos Hubs de eventos do Azure utilizando Java | Microsoft Docs
description: "Começar a receber de Event Hubs utilizando Java"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a>Receber eventos de linguagem Java de Event Hubs do Azure


## <a name="introduction"></a>Introdução
Os Event Hubs são um sistema de ingestão altamente dimensionável, que pode ingerir milhões de eventos por segundo, permitindo tooprocess uma aplicação e analisar Olá quantidades enormes de dados produzidos pelos seus dispositivos e aplicações ligados. Depois de recolhidos nos Event Hubs, pode transformar e armazenar dados em qualquer fornecedor de análise em tempo real ou cluster de armazenamento.

Para obter mais informações, consulte Olá [descrição geral dos Event Hubs][Event Hubs overview].

Este tutorial mostra como tooreceive eventos para um hub de eventos utilizando uma aplicação de consola escrita em Java.

## <a name="prerequisites"></a>Pré-requisitos

Ordem toocomplete neste tutorial, terá de Olá os seguintes pré-requisitos:

* Ambiente de desenvolvimento Java. Para este tutorial, partimos do pressuposto [Eclipse](https://www.eclipse.org/).
* Uma conta ativa do Azure. <br/>Se não tiver uma conta, pode criar uma conta gratuita em apenas alguns minutos. Para obter mais detalhes, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Avaliação Gratuita do Azure</a>.

## <a name="receive-messages-with-eventprocessorhost-in-java"></a>Receber mensagens com o EventProcessorHost em Java

**EventProcessorHost** é uma classe do Java que simplifica a receção de eventos provenientes dos Event Hubs ao gerir pontos de verificação persistentes e receções em paralelo desses Event hubs. Se utilizar o EventProcessorHost, pode dividir eventos por vários recetores, mesmo quando alojados em nós diferentes. Este exemplo mostra como toouse EventProcessorHost para um recetor único.

### <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
toouse EventProcessorHost, tem de ter um [conta de armazenamento do Azure][Azure Storage account]:

1. Inicie sessão no toohello [portal do Azure][Azure portal]e clique em **+ novo** no lado esquerdo do Olá do ecrã de Olá.
2. Clique em **Armazenamento** e, em seguida, clique em **Conta de armazenamento**. No Olá **criar conta de armazenamento** painel, escreva um nome para a conta de armazenamento Olá. Conclua o restante Olá campos Olá, selecione a região pretendida e, em seguida, clique em **criar**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. Clique na conta de armazenamento Olá recém-criado e clique **gerir chaves de acesso**:
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    Copie Olá primário aceder à chave tooa temporário localização, toouse mais tarde no tutorial.

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a>Criar um projeto Java com Olá Eventprocessorhost
Olá biblioteca de cliente de Java para os Event Hubs está disponível para utilização em projetos Maven a partir de Olá [repositório Central Maven][Maven Package]e pode ser referenciada através de Olá seguinte declaração de dependência dentro do Ficheiro de projeto maven:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

Para diferentes tipos de ambientes de compilação, explicitamente pode obter ficheiros JAR Olá lançada mais recente de Olá [repositório Central Maven] [ Maven Package] ou a partir de [Olá ponto de distribuição de versão no GitHub](https://github.com/Azure/azure-event-hubs/releases).  

1. Para seguir o exemplo de Olá, primeiro crie um novo projeto Maven para uma consola/aplicação shell no seu ambiente de desenvolvimento Java favorito. classe de Olá denomina `ErrorNotificationHandler`.     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. Seguinte de Olá de utilização código toocreate uma nova classe denominada `EventProcessor`.
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. Criar uma classe mais chamada `EventProcessorSample`com Olá seguinte código.
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter toostop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. Substitua Olá os seguintes campos com valores de Olá que utilizou quando criou a conta de armazenamento e de hub de eventos de Olá.
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> Este tutorial utiliza uma única instância do EventProcessorHost. débito tooincrease, recomenda-se que execute várias instâncias do EventProcessorHost, preferencialmente, em computadores separados.  Isto fornece redundância bem. Nesses casos, Olá que várias instâncias coordenam-se automaticamente entre si no Olá de saldo ordem tooload recebeu eventos. Se pretender que o processo de tooeach vários recetores *todos os* Olá eventos, tem de utilizar Olá **ConsumerGroup** conceito. Se receber eventos de vários computadores, poderá ser útil toospecify os nomes de instâncias do EventProcessorHost com base nas máquinas hello (ou funções) em que estão implementadas.
> 
> 

## <a name="next-steps"></a>Passos seguintes
Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:

* [Descrição geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um Hub de Eventos](event-hubs-create.md)
* [FAQ dos Hubs de Eventos](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
