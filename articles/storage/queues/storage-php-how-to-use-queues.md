---
title: aaaHow toouse armazenamento de filas do PHP | Microsoft Docs
description: "Saiba como toocreate de serviço do armazenamento de filas do Azure do toouse Olá e filas de eliminação e inserção, obterem e eliminar as mensagens. Exemplos são escritos no PHP."
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 8daabcc9b3b4de121a309f21bb3325242cff06f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a>Como toouse armazenamento de filas do PHP
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Descrição geral
Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Azure. Exemplos de Olá são escritos através de classes de Olá Windows SDK para PHP. Olá cobertos cenários incluem a inserir, leitura, obter e eliminar mensagens de filas, bem como criar e eliminar filas.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Criar uma aplicação PHP
Olá apenas requisito para criar uma aplicação PHP que acede ao armazenamento de filas do Azure é Olá que façam referência de classes de Olá Azure SDK para PHP a partir de dentro do seu código. Pode utilizar qualquer toocreate de ferramentas de desenvolvimento da aplicação, incluindo o bloco de notas.

Neste guia, irá utilizar funcionalidades de armazenamento de filas que podem ser chamadas dentro de uma aplicação PHP localmente, ou no código em execução dentro de uma função da web do Azure, a função de trabalho ou o Web site.

## <a name="get-hello-azure-client-libraries"></a>Obter Olá bibliotecas de cliente do Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurar o armazenamento de filas de tooaccess de aplicação
Olá toouse APIs para armazenamento de filas do Azure, tem de:

1. Ficheiro de Carregador automático de Olá de referência utilizando Olá [require_once] instrução.
2. Referência a quaisquer classes que poderá utilizar.

Olá exemplo seguinte mostra como tooinclude Olá Carregador automático de ficheiros e referência Olá **ServicesBuilder** classe.

> [!NOTE]
> Este exemplo (e outros exemplos neste artigo) pressupõem que tem instalado Olá PHP bibliotecas de cliente para o Azure através do compositor. Se instalou manualmente bibliotecas Olá, terá de tooreference Olá `WindowsAzure.php` Carregador automático ficheiros.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

Nos exemplos de Olá abaixo, Olá `require_once` instrução será sempre apresentada, mas apenas as classes de Olá que são necessárias para tooexecute de exemplo de Olá vai ser referenciadas.

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma ligação de armazenamento do Azure
tooinstantiate um cliente de armazenamento de filas do Azure, tem de ter uma cadeia de ligação válido. formato de Olá para a cadeia de ligação de serviço de fila de Olá é a seguinte.

Para aceder a um serviço em direto:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Para aceder ao armazenamento de emulador de Olá:

```php
UseDevelopmentStorage=true
```

toocreate qualquer cliente de serviço do Azure, terá de toouse Olá **ServicesBuilder** classe. Pode utilizar qualquer um dos seguintes técnicas de Olá:

* Passar ligação Olá cadeia diretamente tooit.
* Utilize **CloudConfigurationManager (CCM)** toocheck externo várias origens para a cadeia de ligação de Olá:
  * Por predefinição, o vem com suporte para uma origem externa — variáveis de ambientais.
  * Pode adicionar novas origens expandindo Olá **ConnectionStringSource** classe.

Para obter exemplos Olá aqui descritos, cadeia de ligação de Olá será transmitida diretamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Criar uma fila
A **QueueRestProxy** objeto permite-lhe criar uma fila utilizando Olá **createQueue** método. Quando criar uma fila, pode definir as opções na fila de Olá, mas fazê-lo, por isso, não é necessário. (Olá o exemplo abaixo mostra como metadados tooset uma fila.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> Não deverá confiar na sensibilidade às maiúsculas e minúsculas para chaves de metadados. Todas as chaves são lidos a partir do serviço de Olá em minúsculas.
> 
> 

## <a name="add-a-message-tooa-queue"></a>Adicionar uma fila de tooa de mensagens
utilizar tooadd tooa uma fila, **QueueRestProxy -> createMessage**. método de Olá aceita o nome da fila Olá, texto da mensagem Olá e opções de mensagens (que são opcionais).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-hello-next-message"></a>Pré-visualizar a mensagem seguinte Olá
Pode pré-visualizar uma mensagem (ou mensagens) em frente Olá de uma fila sem a remover da fila de Olá chamando **QueueRestProxy -> peekMessages**. Por predefinição, Olá **peekMessage** método devolve uma única mensagem, mas pode alterar esse valor utilizando Olá **PeekMessagesOptions -> setNumberOfMessages** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-hello-next-message"></a>Anular a fila a mensagem seguinte Olá
O código remove uma mensagem da fila em dois passos. Em primeiro lugar, tem de chamar **QueueRestProxy -> listMessages**, o que torna Olá mensagem invisível tooany outro código que está a ler da fila de Olá. Por predefinição, esta mensagem permanecerão invisível durante 30 segundos. (Se a mensagem de saudação não é eliminada neste período de tempo, poderá ser visível na fila de Olá novamente.) toofinish remover mensagem de saudação da fila de Olá, tem de chamar **QueueRestProxy -> deleteMessage**. Este processo de dois passos da remoção de uma mensagem garante que, quando os tooprocess de falha de código pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá mesma mensagem e tente novamente. As chamadas de código **deleteMessage** imediatamente após a mensagem de saudação foi processada.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-hello-contents-of-a-queued-message"></a>Alterar Olá conteúdo de uma mensagem em fila
Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá chamando **QueueRestProxy -> updateMessage**. Se a mensagem de saudação representa uma tarefa de trabalho, pode utilizar este estado da funcionalidade tooupdate Olá da tarefa de trabalho de Olá. Olá seguinte código atualiza a mensagem da fila de saudação com novos conteúdos e define tooextend de tempo limite de visibilidade de Olá 60 segundos. Isto guarda o estado de Olá do trabalho associado à mensagem de saudação e proporciona outra toocontinue minuto a trabalhar na mensagem de saudação cliente Olá. Pode utilizar esta técnica tootrack com vários passos os fluxos de trabalho na fila de mensagens, sem ter toostart através de Olá início se falhar um passo de processamento devido a falha de toohardware ou software. Normalmente, também manteria uma contagem de tentativas e se hello mensagem for repetida mais do que  *n*  vezes, deveria eliminá-la. Esta ação protege contra uma mensagem que aciona um erro da aplicação sempre que é processada.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a>Opções adicionais para anular a colocação de mensagens
Existem duas formas de personalizar a obtenção de mensagens numa fila. Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32). Segundo, pode definir um tempo limite de visibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem. Olá exemplo de código seguinte utiliza Olá **getMessages** mensagens de tooget 16 método numa chamada. Em seguida, processa cada mensagem utilizando um **para** ciclo. Também define minutos toofive de tempo limite de invisibilidade do Olá para cada mensagem.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a>Obter o comprimento da fila
Pode obter uma estimativa do número de Olá de mensagens numa fila. Olá **QueueRestProxy -> getQueueMetadata** método pede-lhe Olá fila serviço tooreturn metadados sobre fila Olá. Chamar Olá **getApproximateMessageCount** método no Olá devolveu o objecto fornece uma contagem de é quantidade de mensagens numa fila. Contagem de Olá apenas é aproximada porque as mensagens podem ser adicionadas ou removidas depois do serviço de fila de Olá responde tooyour pedido.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a>Eliminar uma fila
toodelete uma fila e todas as mensagens de Olá, chamar Olá **QueueRestProxy -> deleteQueue** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá do armazenamento de filas do Azure, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas:

* Visite Olá [blogue da equipa de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/).

Para obter mais informações, consulte também Olá [Centro para programadores do PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

