---
title: aaaHow toouse armazenamento de filas do Java | Microsoft Docs
description: "Saiba como toouse Olá filas do Azure service toocreate e filas de eliminação e inserção, obterem e eliminar as mensagens. Amostras de escrita em Java."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2d5211ec5b6454f7dbc126aad4ba9950df13661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="8aa8e-104">Como toouse armazenamento de filas do Java</span><span class="sxs-lookup"><span data-stu-id="8aa8e-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="8aa8e-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="8aa8e-105">Overview</span></span>
<span data-ttu-id="8aa8e-106">Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="8aa8e-107">Exemplos de Olá são escritos em Java e utilizar Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="8aa8e-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="8aa8e-108">Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar** e **eliminar** filas.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="8aa8e-109">Para obter mais informações sobre as filas, consulte Olá [passos](#Next-Steps) secção.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="8aa8e-110">Nota: Um SDK está disponível para programadores que estiver a utilizar o armazenamento do Azure em dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="8aa8e-111">Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="8aa8e-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="8aa8e-112">Criar uma aplicação Java</span><span class="sxs-lookup"><span data-stu-id="8aa8e-112">Create a Java application</span></span>
<span data-ttu-id="8aa8e-113">Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação Java localmente ou numa código em execução numa função da web ou função de trabalho no Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="8aa8e-114">toodo por isso, terá de tooinstall Olá Kit de desenvolvimento Java (JDK) e criar uma conta de armazenamento do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="8aa8e-115">Assim que tiver feito, terá de tooverify que o seu sistema de desenvolvimento cumpre os requisitos mínimos de Olá e dependências que são apresentadas nas Olá [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="8aa8e-116">Se o seu sistema cumpre os requisitos, pode seguir Olá as instruções para transferir e instalar Olá bibliotecas de armazenamento do Azure para Java no seu sistema desse repositório.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="8aa8e-117">Depois de concluir essas tarefas, será capaz de toocreate uma aplicação de Java que utiliza os exemplos de Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="8aa8e-118">Configurar o armazenamento de filas de tooaccess de aplicação</span><span class="sxs-lookup"><span data-stu-id="8aa8e-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="8aa8e-119">Adicione Olá importação instruções toohello superior do ficheiro de Java olá onde pretende que as filas do tooaccess APIs de armazenamento do Azure do toouse os seguintes:</span><span class="sxs-lookup"><span data-stu-id="8aa8e-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="8aa8e-120">Configurar uma cadeia de ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8aa8e-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="8aa8e-121">Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="8aa8e-122">Quando em execução numa aplicação de cliente, tem de fornecer uma cadeia de ligação de armazenamento Olá no Olá seguir o formato, utilizando o nome de Olá da sua conta de armazenamento e Olá chave de acesso primária para a conta de armazenamento de Olá listada no Olá [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="8aa8e-123">Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:</span><span class="sxs-lookup"><span data-stu-id="8aa8e-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="8aa8e-124">Na execução aplicação dentro de uma função no Microsoft Azure, esta cadeia pode ser armazenada no ficheiro de configuração de serviço Olá, *serviceconfiguration. Cscfg*e pode ser acedido com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="8aa8e-125">Eis um exemplo de obter a cadeia de ligação de Olá de um **definição** elemento com o nome *StorageConnectionString* no ficheiro de configuração do serviço de Olá:</span><span class="sxs-lookup"><span data-stu-id="8aa8e-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="8aa8e-126">Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="8aa8e-127">Como: criar uma fila</span><span class="sxs-lookup"><span data-stu-id="8aa8e-127">How to: Create a queue</span></span>
<span data-ttu-id="8aa8e-128">A **CloudQueueClient** objeto permite-lhe obter objetos de referência para as filas.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="8aa8e-129">Olá código seguinte cria um **CloudQueueClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="8aa8e-130">(Nota: existem formas adicionais toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** no Olá [referência do SDK do Azure armazenamento cliente].)</span><span class="sxs-lookup"><span data-stu-id="8aa8e-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="8aa8e-131">Olá utilize **CloudQueueClient** tooget uma fila de toohello referência pretende toouse de objeto.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="8aa8e-132">Pode criar fila Olá se não existir.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-132">You can create hello queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="8aa8e-133">Como: adicionar uma fila de tooa de mensagens</span><span class="sxs-lookup"><span data-stu-id="8aa8e-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="8aa8e-134">tooinsert uma mensagem numa fila existente, primeiro crie um novo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="8aa8e-135">Em seguida, chame Olá **addMessage** método.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="8aa8e-136">A **CloudQueueMessage** podem ser criados a partir de uma cadeia (no formato UTF-8) ou uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="8aa8e-137">Eis o código que cria uma fila (se não existir) e a mensagem de saudação inserções "Olá, mundo".</span><span class="sxs-lookup"><span data-stu-id="8aa8e-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="8aa8e-138">Como: pré-visualizar a mensagem seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="8aa8e-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="8aa8e-139">Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá chamando **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="8aa8e-140">Como: alterar Olá conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="8aa8e-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="8aa8e-141">Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="8aa8e-142">Se a mensagem de saudação representa uma tarefa de trabalho, pode utilizar este estado da funcionalidade tooupdate Olá da tarefa de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="8aa8e-143">Olá seguinte código atualiza a mensagem da fila de saudação com novos conteúdos e conjuntos Olá tooextend de tempo limite de visibilidade 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="8aa8e-144">Isto guarda Olá estado do trabalho associado à mensagem de saudação e atribui o cliente de Olá toocontinue minuto outra mensagem de saudação a trabalhar.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="8aa8e-145">Pode utilizar esta técnica tootrack com vários passos os fluxos de trabalho na fila de mensagens, sem ter toostart através de Olá início se falhar um passo de processamento devido a falha de toohardware ou software.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="8aa8e-146">Normalmente, também manteria uma contagem de tentativas e se hello mensagem for repetida mais do que  *n*  vezes, deveria eliminá-la.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="8aa8e-147">Esta ação protege contra uma mensagem que aciona um erro da aplicação sempre que é processada.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="8aa8e-148">seguinte Olá code pesquisas de exemplo através da fila de Olá de mensagens, localiza a primeira mensagem de saudação que corresponde a "Olá, mundo" para o conteúdo de Olá, em seguida, modifica o conteúdo de mensagem de saudação e sai.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="8aa8e-149">Em alternativa, hello seguinte exemplo de código atualiza apenas primeiro visível mensagem de saudação na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="8aa8e-150">Como: obter o comprimento da fila Olá</span><span class="sxs-lookup"><span data-stu-id="8aa8e-150">How to: Get hello queue length</span></span>
<span data-ttu-id="8aa8e-151">Pode obter uma estimativa do número de Olá de mensagens numa fila.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="8aa8e-152">Olá **downloadAttributes** método pede-lhe Olá fila de serviço para os vários valores atuais, incluindo uma contagem de é quantidade de mensagens numa fila.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="8aa8e-153">Contagem de Olá apenas é aproximada porque as mensagens podem ser adicionadas ou removidas após Olá serviço fila responde tooyour pedido.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="8aa8e-154">Olá **getApproximateMessageCount** método devolve Olá último valor obtido pelo chamada Olá demasiado**downloadAttributes**, sem chamar o serviço de fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="8aa8e-155">Como: anular a mensagem de saudação seguinte</span><span class="sxs-lookup"><span data-stu-id="8aa8e-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="8aa8e-156">O código dequeues uma mensagem da fila em dois passos.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="8aa8e-157">Quando chamar **retrieveMessage**, obterá a mensagem seguinte Olá numa fila.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="8aa8e-158">Uma mensagem devolvida por **retrieveMessage** torna-se invisível tooany outro código de leitura de mensagens desta fila.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="8aa8e-159">Por predefinição, esta mensagem permanece invisível durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="8aa8e-160">toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="8aa8e-161">Este processo de dois passos da remoção de uma mensagem garante que se o código de falha tooprocess que pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="8aa8e-162">As chamadas de código **deleteMessage** imediatamente após a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="8aa8e-163">Opções adicionais para mensagens dequeuing</span><span class="sxs-lookup"><span data-stu-id="8aa8e-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="8aa8e-164">Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="8aa8e-165">Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32).</span><span class="sxs-lookup"><span data-stu-id="8aa8e-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="8aa8e-166">Segundo, pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="8aa8e-167">Olá exemplo de código seguinte utiliza Olá **retrieveMessages** mensagens de tooget 20 método numa chamada.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="8aa8e-168">Em seguida, processa cada mensagem utilizando um **para** ciclo.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="8aa8e-169">Também define toofive minutos (300 segundos) de invisibilidade tempo limite Olá para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="8aa8e-170">Tenha em atenção que Olá cinco minutos inicia para todas as mensagens no Olá mesmo tempo, pelo que, quando cinco passaram minutos desde a chamada de Olá demasiado**retrieveMessages**, as mensagens que não tenham sido eliminadas ficarão visíveis novamente.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="8aa8e-171">Como: lista filas Olá</span><span class="sxs-lookup"><span data-stu-id="8aa8e-171">How to: List hello queues</span></span>
<span data-ttu-id="8aa8e-172">tooobtain uma lista de Olá atual as filas, chamada Olá **CloudQueueClient.listQueues()** método, o que irá devolver uma coleção de **CloudQueue** objetos.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="8aa8e-173">Como: eliminar uma fila</span><span class="sxs-lookup"><span data-stu-id="8aa8e-173">How to: Delete a queue</span></span>
<span data-ttu-id="8aa8e-174">toodelete uma fila e todas as mensagens de Olá nela contidas, chamada Olá **deleteIfExists** método no Olá **CloudQueue** objeto.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="8aa8e-175">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8aa8e-175">Next steps</span></span>
<span data-ttu-id="8aa8e-176">Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="8aa8e-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="8aa8e-177">[Armazenamento do Azure SDK para Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="8aa8e-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="8aa8e-178">[Referência do SDK de cliente de armazenamento do Azure][referência do SDK do Azure armazenamento cliente]</span><span class="sxs-lookup"><span data-stu-id="8aa8e-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="8aa8e-179">[REST API dos serviços do Storage do Azure][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="8aa8e-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="8aa8e-180">[Blogue da equipa do Storage do Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="8aa8e-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência do SDK do Azure armazenamento cliente]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
