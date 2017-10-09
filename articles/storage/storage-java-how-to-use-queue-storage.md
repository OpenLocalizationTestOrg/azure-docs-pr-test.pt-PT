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
# <a name="how-toouse-queue-storage-from-java"></a>Como toouse armazenamento de filas do Java
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Descrição geral
Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Azure. Exemplos de Olá são escritos em Java e utilizar Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java]. Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar** e **eliminar** filas. Para obter mais informações sobre as filas, consulte Olá [passos](#Next-Steps) secção.

Nota: Um SDK está disponível para programadores que estiver a utilizar o armazenamento do Azure em dispositivos Android. Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Criar uma aplicação Java
Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação Java localmente ou numa código em execução numa função da web ou função de trabalho no Azure.

toodo por isso, terá de tooinstall Olá Kit de desenvolvimento Java (JDK) e criar uma conta de armazenamento do Azure na sua subscrição do Azure. Assim que tiver feito, terá de tooverify que o seu sistema de desenvolvimento cumpre os requisitos mínimos de Olá e dependências que são apresentadas nas Olá [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub. Se o seu sistema cumpre os requisitos, pode seguir Olá as instruções para transferir e instalar Olá bibliotecas de armazenamento do Azure para Java no seu sistema desse repositório. Depois de concluir essas tarefas, será capaz de toocreate uma aplicação de Java que utiliza os exemplos de Olá neste artigo.

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurar o armazenamento de filas de tooaccess de aplicação
Adicione Olá importação instruções toohello superior do ficheiro de Java olá onde pretende que as filas do tooaccess APIs de armazenamento do Azure do toouse os seguintes:

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configurar uma cadeia de ligação de armazenamento do Azure
Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados. Quando em execução numa aplicação de cliente, tem de fornecer uma cadeia de ligação de armazenamento Olá no Olá seguir o formato, utilizando o nome de Olá da sua conta de armazenamento e Olá chave de acesso primária para a conta de armazenamento de Olá listada no Olá [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores. Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Na execução aplicação dentro de uma função no Microsoft Azure, esta cadeia pode ser armazenada no ficheiro de configuração de serviço Olá, *serviceconfiguration. Cscfg*e pode ser acedido com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método. Eis um exemplo de obter a cadeia de ligação de Olá de um **definição** elemento com o nome *StorageConnectionString* no ficheiro de configuração do serviço de Olá:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.

## <a name="how-to-create-a-queue"></a>Como: criar uma fila
A **CloudQueueClient** objeto permite-lhe obter objetos de referência para as filas. Olá código seguinte cria um **CloudQueueClient** objeto. (Nota: existem formas adicionais toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** no Olá [referência do SDK do Azure armazenamento cliente].)

Olá utilize **CloudQueueClient** tooget uma fila de toohello referência pretende toouse de objeto. Pode criar fila Olá se não existir.

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

## <a name="how-to-add-a-message-tooa-queue"></a>Como: adicionar uma fila de tooa de mensagens
tooinsert uma mensagem numa fila existente, primeiro crie um novo **CloudQueueMessage**. Em seguida, chame Olá **addMessage** método. A **CloudQueueMessage** podem ser criados a partir de uma cadeia (no formato UTF-8) ou uma matriz de bytes. Eis o código que cria uma fila (se não existir) e a mensagem de saudação inserções "Olá, mundo".

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

## <a name="how-to-peek-at-hello-next-message"></a>Como: pré-visualizar a mensagem seguinte Olá
Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá chamando **peekMessage**.

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: alterar Olá conteúdo de uma mensagem em fila
Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá. Se a mensagem de saudação representa uma tarefa de trabalho, pode utilizar este estado da funcionalidade tooupdate Olá da tarefa de trabalho de Olá. Olá seguinte código atualiza a mensagem da fila de saudação com novos conteúdos e conjuntos Olá tooextend de tempo limite de visibilidade 60 segundos. Isto guarda Olá estado do trabalho associado à mensagem de saudação e atribui o cliente de Olá toocontinue minuto outra mensagem de saudação a trabalhar. Pode utilizar esta técnica tootrack com vários passos os fluxos de trabalho na fila de mensagens, sem ter toostart através de Olá início se falhar um passo de processamento devido a falha de toohardware ou software. Normalmente, também manteria uma contagem de tentativas e se hello mensagem for repetida mais do que  *n*  vezes, deveria eliminá-la. Esta ação protege contra uma mensagem que aciona um erro da aplicação sempre que é processada.

seguinte Olá code pesquisas de exemplo através da fila de Olá de mensagens, localiza a primeira mensagem de saudação que corresponde a "Olá, mundo" para o conteúdo de Olá, em seguida, modifica o conteúdo de mensagem de saudação e sai.

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

Em alternativa, hello seguinte exemplo de código atualiza apenas primeiro visível mensagem de saudação na fila de Olá.

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

## <a name="how-to-get-hello-queue-length"></a>Como: obter o comprimento da fila Olá
Pode obter uma estimativa do número de Olá de mensagens numa fila. Olá **downloadAttributes** método pede-lhe Olá fila de serviço para os vários valores atuais, incluindo uma contagem de é quantidade de mensagens numa fila. Contagem de Olá apenas é aproximada porque as mensagens podem ser adicionadas ou removidas após Olá serviço fila responde tooyour pedido. Olá **getApproximateMessageCount** método devolve Olá último valor obtido pelo chamada Olá demasiado**downloadAttributes**, sem chamar o serviço de fila de Olá.

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

## <a name="how-to-dequeue-hello-next-message"></a>Como: anular a mensagem de saudação seguinte
O código dequeues uma mensagem da fila em dois passos. Quando chamar **retrieveMessage**, obterá a mensagem seguinte Olá numa fila. Uma mensagem devolvida por **retrieveMessage** torna-se invisível tooany outro código de leitura de mensagens desta fila. Por predefinição, esta mensagem permanece invisível durante 30 segundos. toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **deleteMessage**. Este processo de dois passos da remoção de uma mensagem garante que se o código de falha tooprocess que pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá a mesma mensagem e tente novamente. As chamadas de código **deleteMessage** imediatamente após a mensagem de saudação foi processada.

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

## <a name="additional-options-for-dequeuing-messages"></a>Opções adicionais para mensagens dequeuing
Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila. Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32). Segundo, pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem.

Olá exemplo de código seguinte utiliza Olá **retrieveMessages** mensagens de tooget 20 método numa chamada. Em seguida, processa cada mensagem utilizando um **para** ciclo. Também define toofive minutos (300 segundos) de invisibilidade tempo limite Olá para cada mensagem. Tenha em atenção que Olá cinco minutos inicia para todas as mensagens no Olá mesmo tempo, pelo que, quando cinco passaram minutos desde a chamada de Olá demasiado**retrieveMessages**, as mensagens que não tenham sido eliminadas ficarão visíveis novamente.

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

## <a name="how-to-list-hello-queues"></a>Como: lista filas Olá
tooobtain uma lista de Olá atual as filas, chamada Olá **CloudQueueClient.listQueues()** método, o que irá devolver uma coleção de **CloudQueue** objetos.

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

## <a name="how-to-delete-a-queue"></a>Como: eliminar uma fila
toodelete uma fila e todas as mensagens de Olá nela contidas, chamada Olá **deleteIfExists** método no Olá **CloudQueue** objeto.

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

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.

* [Armazenamento do Azure SDK para Java][Azure Storage SDK for Java]
* [Referência do SDK de cliente de armazenamento do Azure][referência do SDK do Azure armazenamento cliente]
* [REST API dos serviços do Storage do Azure][Azure Storage Services REST API]
* [Blogue da equipa do Storage do Azure][Azure Storage Team Blog]

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência do SDK do Azure armazenamento cliente]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
