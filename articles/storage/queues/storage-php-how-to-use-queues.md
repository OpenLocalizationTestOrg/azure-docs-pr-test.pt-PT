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
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="e7aac-104">Como toouse armazenamento de filas do PHP</span><span class="sxs-lookup"><span data-stu-id="e7aac-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="e7aac-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="e7aac-105">Overview</span></span>
<span data-ttu-id="e7aac-106">Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7aac-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="e7aac-107">Exemplos de Olá são escritos através de classes de Olá Windows SDK para PHP.</span><span class="sxs-lookup"><span data-stu-id="e7aac-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="e7aac-108">Olá cobertos cenários incluem a inserir, leitura, obter e eliminar mensagens de filas, bem como criar e eliminar filas.</span><span class="sxs-lookup"><span data-stu-id="e7aac-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="e7aac-109">Criar uma aplicação PHP</span><span class="sxs-lookup"><span data-stu-id="e7aac-109">Create a PHP application</span></span>
<span data-ttu-id="e7aac-110">Olá apenas requisito para criar uma aplicação PHP que acede ao armazenamento de filas do Azure é Olá que façam referência de classes de Olá Azure SDK para PHP a partir de dentro do seu código.</span><span class="sxs-lookup"><span data-stu-id="e7aac-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="e7aac-111">Pode utilizar qualquer toocreate de ferramentas de desenvolvimento da aplicação, incluindo o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="e7aac-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="e7aac-112">Neste guia, irá utilizar funcionalidades de armazenamento de filas que podem ser chamadas dentro de uma aplicação PHP localmente, ou no código em execução dentro de uma função da web do Azure, a função de trabalho ou o Web site.</span><span class="sxs-lookup"><span data-stu-id="e7aac-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="e7aac-113">Obter Olá bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="e7aac-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="e7aac-114">Configurar o armazenamento de filas de tooaccess de aplicação</span><span class="sxs-lookup"><span data-stu-id="e7aac-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="e7aac-115">Olá toouse APIs para armazenamento de filas do Azure, tem de:</span><span class="sxs-lookup"><span data-stu-id="e7aac-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="e7aac-116">Ficheiro de Carregador automático de Olá de referência utilizando Olá [require_once] instrução.</span><span class="sxs-lookup"><span data-stu-id="e7aac-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="e7aac-117">Referência a quaisquer classes que poderá utilizar.</span><span class="sxs-lookup"><span data-stu-id="e7aac-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="e7aac-118">Olá exemplo seguinte mostra como tooinclude Olá Carregador automático de ficheiros e referência Olá **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="e7aac-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="e7aac-119">Este exemplo (e outros exemplos neste artigo) pressupõem que tem instalado Olá PHP bibliotecas de cliente para o Azure através do compositor.</span><span class="sxs-lookup"><span data-stu-id="e7aac-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="e7aac-120">Se instalou manualmente bibliotecas Olá, terá de tooreference Olá `WindowsAzure.php` Carregador automático ficheiros.</span><span class="sxs-lookup"><span data-stu-id="e7aac-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="e7aac-121">Nos exemplos de Olá abaixo, Olá `require_once` instrução será sempre apresentada, mas apenas as classes de Olá que são necessárias para tooexecute de exemplo de Olá vai ser referenciadas.</span><span class="sxs-lookup"><span data-stu-id="e7aac-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="e7aac-122">Configurar uma ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e7aac-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="e7aac-123">tooinstantiate um cliente de armazenamento de filas do Azure, tem de ter uma cadeia de ligação válido.</span><span class="sxs-lookup"><span data-stu-id="e7aac-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="e7aac-124">formato de Olá para a cadeia de ligação de serviço de fila de Olá é a seguinte.</span><span class="sxs-lookup"><span data-stu-id="e7aac-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="e7aac-125">Para aceder a um serviço em direto:</span><span class="sxs-lookup"><span data-stu-id="e7aac-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="e7aac-126">Para aceder ao armazenamento de emulador de Olá:</span><span class="sxs-lookup"><span data-stu-id="e7aac-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="e7aac-127">toocreate qualquer cliente de serviço do Azure, terá de toouse Olá **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="e7aac-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="e7aac-128">Pode utilizar qualquer um dos seguintes técnicas de Olá:</span><span class="sxs-lookup"><span data-stu-id="e7aac-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="e7aac-129">Passar ligação Olá cadeia diretamente tooit.</span><span class="sxs-lookup"><span data-stu-id="e7aac-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="e7aac-130">Utilize **CloudConfigurationManager (CCM)** toocheck externo várias origens para a cadeia de ligação de Olá:</span><span class="sxs-lookup"><span data-stu-id="e7aac-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="e7aac-131">Por predefinição, o vem com suporte para uma origem externa — variáveis de ambientais.</span><span class="sxs-lookup"><span data-stu-id="e7aac-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="e7aac-132">Pode adicionar novas origens expandindo Olá **ConnectionStringSource** classe.</span><span class="sxs-lookup"><span data-stu-id="e7aac-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="e7aac-133">Para obter exemplos Olá aqui descritos, cadeia de ligação de Olá será transmitida diretamente.</span><span class="sxs-lookup"><span data-stu-id="e7aac-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="e7aac-134">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="e7aac-134">Create a queue</span></span>
<span data-ttu-id="e7aac-135">A **QueueRestProxy** objeto permite-lhe criar uma fila utilizando Olá **createQueue** método.</span><span class="sxs-lookup"><span data-stu-id="e7aac-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="e7aac-136">Quando criar uma fila, pode definir as opções na fila de Olá, mas fazê-lo, por isso, não é necessário.</span><span class="sxs-lookup"><span data-stu-id="e7aac-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="e7aac-137">(Olá o exemplo abaixo mostra como metadados tooset uma fila.)</span><span class="sxs-lookup"><span data-stu-id="e7aac-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="e7aac-138">Não deverá confiar na sensibilidade às maiúsculas e minúsculas para chaves de metadados.</span><span class="sxs-lookup"><span data-stu-id="e7aac-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="e7aac-139">Todas as chaves são lidos a partir do serviço de Olá em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e7aac-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="e7aac-140">Adicionar uma fila de tooa de mensagens</span><span class="sxs-lookup"><span data-stu-id="e7aac-140">Add a message tooa queue</span></span>
<span data-ttu-id="e7aac-141">utilizar tooadd tooa uma fila, **QueueRestProxy -> createMessage**.</span><span class="sxs-lookup"><span data-stu-id="e7aac-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="e7aac-142">método de Olá aceita o nome da fila Olá, texto da mensagem Olá e opções de mensagens (que são opcionais).</span><span class="sxs-lookup"><span data-stu-id="e7aac-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="e7aac-143">Pré-visualizar a mensagem seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="e7aac-143">Peek at hello next message</span></span>
<span data-ttu-id="e7aac-144">Pode pré-visualizar uma mensagem (ou mensagens) em frente Olá de uma fila sem a remover da fila de Olá chamando **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="e7aac-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="e7aac-145">Por predefinição, Olá **peekMessage** método devolve uma única mensagem, mas pode alterar esse valor utilizando Olá **PeekMessagesOptions -> setNumberOfMessages** método.</span><span class="sxs-lookup"><span data-stu-id="e7aac-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="e7aac-146">Anular a fila a mensagem seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="e7aac-146">De-queue hello next message</span></span>
<span data-ttu-id="e7aac-147">O código remove uma mensagem da fila em dois passos.</span><span class="sxs-lookup"><span data-stu-id="e7aac-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="e7aac-148">Em primeiro lugar, tem de chamar **QueueRestProxy -> listMessages**, o que torna Olá mensagem invisível tooany outro código que está a ler da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="e7aac-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="e7aac-149">Por predefinição, esta mensagem permanecerão invisível durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="e7aac-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="e7aac-150">(Se a mensagem de saudação não é eliminada neste período de tempo, poderá ser visível na fila de Olá novamente.) toofinish remover mensagem de saudação da fila de Olá, tem de chamar **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="e7aac-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="e7aac-151">Este processo de dois passos da remoção de uma mensagem garante que, quando os tooprocess de falha de código pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="e7aac-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="e7aac-152">As chamadas de código **deleteMessage** imediatamente após a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="e7aac-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="e7aac-153">Alterar Olá conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="e7aac-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="e7aac-154">Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá chamando **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="e7aac-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="e7aac-155">Se a mensagem de saudação representa uma tarefa de trabalho, pode utilizar este estado da funcionalidade tooupdate Olá da tarefa de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="e7aac-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="e7aac-156">Olá seguinte código atualiza a mensagem da fila de saudação com novos conteúdos e define tooextend de tempo limite de visibilidade de Olá 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="e7aac-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="e7aac-157">Isto guarda o estado de Olá do trabalho associado à mensagem de saudação e proporciona outra toocontinue minuto a trabalhar na mensagem de saudação cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="e7aac-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="e7aac-158">Pode utilizar esta técnica tootrack com vários passos os fluxos de trabalho na fila de mensagens, sem ter toostart através de Olá início se falhar um passo de processamento devido a falha de toohardware ou software.</span><span class="sxs-lookup"><span data-stu-id="e7aac-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="e7aac-159">Normalmente, também manteria uma contagem de tentativas e se hello mensagem for repetida mais do que  *n*  vezes, deveria eliminá-la.</span><span class="sxs-lookup"><span data-stu-id="e7aac-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="e7aac-160">Esta ação protege contra uma mensagem que aciona um erro da aplicação sempre que é processada.</span><span class="sxs-lookup"><span data-stu-id="e7aac-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="e7aac-161">Opções adicionais para anular a colocação de mensagens</span><span class="sxs-lookup"><span data-stu-id="e7aac-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="e7aac-162">Existem duas formas de personalizar a obtenção de mensagens numa fila.</span><span class="sxs-lookup"><span data-stu-id="e7aac-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="e7aac-163">Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32).</span><span class="sxs-lookup"><span data-stu-id="e7aac-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="e7aac-164">Segundo, pode definir um tempo limite de visibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="e7aac-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="e7aac-165">Olá exemplo de código seguinte utiliza Olá **getMessages** mensagens de tooget 16 método numa chamada.</span><span class="sxs-lookup"><span data-stu-id="e7aac-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="e7aac-166">Em seguida, processa cada mensagem utilizando um **para** ciclo.</span><span class="sxs-lookup"><span data-stu-id="e7aac-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="e7aac-167">Também define minutos toofive de tempo limite de invisibilidade do Olá para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="e7aac-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="e7aac-168">Obter o comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="e7aac-168">Get queue length</span></span>
<span data-ttu-id="e7aac-169">Pode obter uma estimativa do número de Olá de mensagens numa fila.</span><span class="sxs-lookup"><span data-stu-id="e7aac-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="e7aac-170">Olá **QueueRestProxy -> getQueueMetadata** método pede-lhe Olá fila serviço tooreturn metadados sobre fila Olá.</span><span class="sxs-lookup"><span data-stu-id="e7aac-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="e7aac-171">Chamar Olá **getApproximateMessageCount** método no Olá devolveu o objecto fornece uma contagem de é quantidade de mensagens numa fila.</span><span class="sxs-lookup"><span data-stu-id="e7aac-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="e7aac-172">Contagem de Olá apenas é aproximada porque as mensagens podem ser adicionadas ou removidas depois do serviço de fila de Olá responde tooyour pedido.</span><span class="sxs-lookup"><span data-stu-id="e7aac-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="e7aac-173">Eliminar uma fila</span><span class="sxs-lookup"><span data-stu-id="e7aac-173">Delete a queue</span></span>
<span data-ttu-id="e7aac-174">toodelete uma fila e todas as mensagens de Olá, chamar Olá **QueueRestProxy -> deleteQueue** método.</span><span class="sxs-lookup"><span data-stu-id="e7aac-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e7aac-175">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e7aac-175">Next steps</span></span>
<span data-ttu-id="e7aac-176">Agora que aprendeu as noções básicas de Olá do armazenamento de filas do Azure, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas:</span><span class="sxs-lookup"><span data-stu-id="e7aac-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="e7aac-177">Visite Olá [blogue da equipa de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="e7aac-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="e7aac-178">Para obter mais informações, consulte também Olá [Centro para programadores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="e7aac-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

