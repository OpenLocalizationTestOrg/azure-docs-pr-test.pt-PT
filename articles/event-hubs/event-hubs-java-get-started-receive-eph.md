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
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="6349e-103">Receber eventos de linguagem Java de Event Hubs do Azure</span><span class="sxs-lookup"><span data-stu-id="6349e-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="6349e-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="6349e-104">Introduction</span></span>
<span data-ttu-id="6349e-105">Os Event Hubs são um sistema de ingestão altamente dimensionável, que pode ingerir milhões de eventos por segundo, permitindo tooprocess uma aplicação e analisar Olá quantidades enormes de dados produzidos pelos seus dispositivos e aplicações ligados.</span><span class="sxs-lookup"><span data-stu-id="6349e-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="6349e-106">Depois de recolhidos nos Event Hubs, pode transformar e armazenar dados em qualquer fornecedor de análise em tempo real ou cluster de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6349e-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="6349e-107">Para obter mais informações, consulte Olá [descrição geral dos Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="6349e-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="6349e-108">Este tutorial mostra como tooreceive eventos para um hub de eventos utilizando uma aplicação de consola escrita em Java.</span><span class="sxs-lookup"><span data-stu-id="6349e-108">This tutorial shows how tooreceive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6349e-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6349e-109">Prerequisites</span></span>

<span data-ttu-id="6349e-110">Ordem toocomplete neste tutorial, terá de Olá os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="6349e-110">In order toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="6349e-111">Ambiente de desenvolvimento Java.</span><span class="sxs-lookup"><span data-stu-id="6349e-111">A Java development environment.</span></span> <span data-ttu-id="6349e-112">Para este tutorial, partimos do pressuposto [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="6349e-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="6349e-113">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="6349e-113">An active Azure account.</span></span> <br/><span data-ttu-id="6349e-114">Se não tiver uma conta, pode criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6349e-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="6349e-115">Para obter mais detalhes, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Avaliação Gratuita do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="6349e-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="6349e-116">Receber mensagens com o EventProcessorHost em Java</span><span class="sxs-lookup"><span data-stu-id="6349e-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="6349e-117">**EventProcessorHost** é uma classe do Java que simplifica a receção de eventos provenientes dos Event Hubs ao gerir pontos de verificação persistentes e receções em paralelo desses Event hubs.</span><span class="sxs-lookup"><span data-stu-id="6349e-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="6349e-118">Se utilizar o EventProcessorHost, pode dividir eventos por vários recetores, mesmo quando alojados em nós diferentes.</span><span class="sxs-lookup"><span data-stu-id="6349e-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="6349e-119">Este exemplo mostra como toouse EventProcessorHost para um recetor único.</span><span class="sxs-lookup"><span data-stu-id="6349e-119">This example shows how toouse EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="6349e-120">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="6349e-120">Create a storage account</span></span>
<span data-ttu-id="6349e-121">toouse EventProcessorHost, tem de ter um [conta de armazenamento do Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="6349e-121">toouse EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="6349e-122">Inicie sessão no toohello [portal do Azure][Azure portal]e clique em **+ novo** no lado esquerdo do Olá do ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="6349e-122">Log on toohello [Azure portal][Azure portal], and click **+ New** on hello left-hand side of hello screen.</span></span>
2. <span data-ttu-id="6349e-123">Clique em **Armazenamento** e, em seguida, clique em **Conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="6349e-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="6349e-124">No Olá **criar conta de armazenamento** painel, escreva um nome para a conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="6349e-124">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="6349e-125">Conclua o restante Olá campos Olá, selecione a região pretendida e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="6349e-125">Complete hello rest of hello fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="6349e-126">Clique na conta de armazenamento Olá recém-criado e clique **gerir chaves de acesso**:</span><span class="sxs-lookup"><span data-stu-id="6349e-126">Click hello newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="6349e-127">Copie Olá primário aceder à chave tooa temporário localização, toouse mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="6349e-127">Copy hello primary access key tooa temporary location, toouse later in this tutorial.</span></span>

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a><span data-ttu-id="6349e-128">Criar um projeto Java com Olá Eventprocessorhost</span><span class="sxs-lookup"><span data-stu-id="6349e-128">Create a Java project using hello EventProcessor Host</span></span>
<span data-ttu-id="6349e-129">Olá biblioteca de cliente de Java para os Event Hubs está disponível para utilização em projetos Maven a partir de Olá [repositório Central Maven][Maven Package]e pode ser referenciada através de Olá seguinte declaração de dependência dentro do Ficheiro de projeto maven:</span><span class="sxs-lookup"><span data-stu-id="6349e-129">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository][Maven Package], and can be referenced using hello following dependency declaration inside your Maven project file:</span></span>    

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

<span data-ttu-id="6349e-130">Para diferentes tipos de ambientes de compilação, explicitamente pode obter ficheiros JAR Olá lançada mais recente de Olá [repositório Central Maven] [ Maven Package] ou a partir de [Olá ponto de distribuição de versão no GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="6349e-130">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository][Maven Package] or from [hello release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="6349e-131">Para seguir o exemplo de Olá, primeiro crie um novo projeto Maven para uma consola/aplicação shell no seu ambiente de desenvolvimento Java favorito.</span><span class="sxs-lookup"><span data-stu-id="6349e-131">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="6349e-132">classe de Olá denomina `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="6349e-132">hello class is called `ErrorNotificationHandler`.</span></span>     
   
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
2. <span data-ttu-id="6349e-133">Seguinte de Olá de utilização código toocreate uma nova classe denominada `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="6349e-133">Use hello following code toocreate a new class called `EventProcessor`.</span></span>
   
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
3. <span data-ttu-id="6349e-134">Criar uma classe mais chamada `EventProcessorSample`com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="6349e-134">Create one more class called `EventProcessorSample`, using hello following code.</span></span>
   
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
4. <span data-ttu-id="6349e-135">Substitua Olá os seguintes campos com valores de Olá que utilizou quando criou a conta de armazenamento e de hub de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="6349e-135">Replace hello following fields with hello values used when you created hello event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="6349e-136">Este tutorial utiliza uma única instância do EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="6349e-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="6349e-137">débito tooincrease, recomenda-se que execute várias instâncias do EventProcessorHost, preferencialmente, em computadores separados.</span><span class="sxs-lookup"><span data-stu-id="6349e-137">tooincrease throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="6349e-138">Isto fornece redundância bem.</span><span class="sxs-lookup"><span data-stu-id="6349e-138">This provides redundancy as well.</span></span> <span data-ttu-id="6349e-139">Nesses casos, Olá que várias instâncias coordenam-se automaticamente entre si no Olá de saldo ordem tooload recebeu eventos.</span><span class="sxs-lookup"><span data-stu-id="6349e-139">In those cases, hello various instances automatically coordinate with each other in order tooload balance hello received events.</span></span> <span data-ttu-id="6349e-140">Se pretender que o processo de tooeach vários recetores *todos os* Olá eventos, tem de utilizar Olá **ConsumerGroup** conceito.</span><span class="sxs-lookup"><span data-stu-id="6349e-140">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="6349e-141">Se receber eventos de vários computadores, poderá ser útil toospecify os nomes de instâncias do EventProcessorHost com base nas máquinas hello (ou funções) em que estão implementadas.</span><span class="sxs-lookup"><span data-stu-id="6349e-141">When receiving events from different machines, it might be useful toospecify names for EventProcessorHost instances based on hello machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6349e-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6349e-142">Next steps</span></span>
<span data-ttu-id="6349e-143">Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:</span><span class="sxs-lookup"><span data-stu-id="6349e-143">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="6349e-144">Descrição geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="6349e-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6349e-145">Criar um Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="6349e-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="6349e-146">FAQ dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="6349e-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
