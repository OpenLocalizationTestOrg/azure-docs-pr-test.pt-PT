---
title: filas aaaHow toouse Service Bus com o PHP | Microsoft Docs
description: "Saiba como toouse Service Bus são filas no Azure. Exemplos de código escrito em PHP."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="b6558-104">Como toouse Service Bus são filas com o PHP</span><span class="sxs-lookup"><span data-stu-id="b6558-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="b6558-105">Este guia mostra como toouse filas do Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b6558-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="b6558-106">Exemplos de Olá são escritos no PHP e utilizam Olá [Azure SDK para PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b6558-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="b6558-107">Olá os cenários abrangidos incluem **criar filas**, **enviar e receber mensagens**, e **eliminar filas**.</span><span class="sxs-lookup"><span data-stu-id="b6558-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="b6558-108">Criar uma aplicação PHP</span><span class="sxs-lookup"><span data-stu-id="b6558-108">Create a PHP application</span></span>
<span data-ttu-id="b6558-109">Olá, só é o requisito para criar uma aplicação PHP que acede ao serviço Blob do Azure de Olá Olá referência de classes no Olá [Azure SDK para PHP](../php-download-sdk.md) de dentro do seu código.</span><span class="sxs-lookup"><span data-stu-id="b6558-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="b6558-110">Pode utilizar qualquer toocreate de ferramentas de desenvolvimento da aplicação ou o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="b6558-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="b6558-111">A instalação do PHP também tem de ter Olá [OpenSSL extensão](http://php.net/openssl) instalado e ativado.</span><span class="sxs-lookup"><span data-stu-id="b6558-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="b6558-112">Neste guia, irá utilizar as funcionalidades de serviço que podem ser chamadas de dentro de uma aplicação PHP localmente, ou no código em execução dentro de uma função da web do Azure, a função de trabalho ou o Web site.</span><span class="sxs-lookup"><span data-stu-id="b6558-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="b6558-113">Obtenha Olá bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="b6558-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="b6558-114">Configurar o seu toouse aplicação de Service Bus</span><span class="sxs-lookup"><span data-stu-id="b6558-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="b6558-115">fila do Service Bus toouse Olá APIs, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="b6558-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="b6558-116">Ficheiro de Carregador automático de Olá de referência utilizando Olá [require_once] [ require_once] instrução.</span><span class="sxs-lookup"><span data-stu-id="b6558-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="b6558-117">Referência a quaisquer classes que poderá utilizar.</span><span class="sxs-lookup"><span data-stu-id="b6558-117">Reference any classes you might use.</span></span>

<span data-ttu-id="b6558-118">Olá exemplo seguinte mostra como tooinclude Olá Carregador automático de ficheiros e referência Olá `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="b6558-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="b6558-119">Este exemplo (e outros exemplos neste artigo) parte do princípio de que instalou Olá PHP bibliotecas de cliente para o Azure através do compositor.</span><span class="sxs-lookup"><span data-stu-id="b6558-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="b6558-120">Se instalou bibliotecas Olá manualmente ou como um pacote PEAR, tem de referenciar Olá **WindowsAzure.php** Carregador automático ficheiros.</span><span class="sxs-lookup"><span data-stu-id="b6558-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="b6558-121">Nos exemplos de Olá abaixo, Olá `require_once` instrução será sempre apresentada, mas apenas Olá classes necessárias para tooexecute de exemplo de Olá são referenciadas.</span><span class="sxs-lookup"><span data-stu-id="b6558-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="b6558-122">Configurar uma ligação de barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="b6558-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="b6558-123">tooinstantiate um cliente do Service Bus, primeiro é necessário ter uma cadeia de ligação válido neste formato:</span><span class="sxs-lookup"><span data-stu-id="b6558-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="b6558-124">Onde `Endpoint` normalmente tem um formato Olá `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="b6558-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="b6558-125">toocreate qualquer cliente de serviço do Azure tem de utilizar Olá `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="b6558-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="b6558-126">Pode:</span><span class="sxs-lookup"><span data-stu-id="b6558-126">You can:</span></span>

* <span data-ttu-id="b6558-127">Passar ligação Olá cadeia diretamente tooit.</span><span class="sxs-lookup"><span data-stu-id="b6558-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="b6558-128">utilizar Olá **CloudConfigurationManager (CCM)** toocheck externo várias origens para a cadeia de ligação de Olá:</span><span class="sxs-lookup"><span data-stu-id="b6558-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="b6558-129">Por predefinição vem com suporte para uma origem externa - variáveis de ambientais</span><span class="sxs-lookup"><span data-stu-id="b6558-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="b6558-130">Pode adicionar novas origens expandindo Olá `ConnectionStringSource` classe</span><span class="sxs-lookup"><span data-stu-id="b6558-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="b6558-131">Para obter exemplos Olá aqui descritos, cadeia de ligação de Olá é transmitida diretamente.</span><span class="sxs-lookup"><span data-stu-id="b6558-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="b6558-132">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="b6558-132">Create a queue</span></span>
<span data-ttu-id="b6558-133">Pode efetuar operações de gestão para filas do Service Bus através de Olá `ServiceBusRestProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="b6558-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="b6558-134">A `ServiceBusRestProxy` objecto é construído através de Olá `ServicesBuilder::createServiceBusService` método de fábrica com uma cadeia de ligação adequado que encapsula Olá permissões token toomanage-lo.</span><span class="sxs-lookup"><span data-stu-id="b6558-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="b6558-135">Olá seguinte exemplo mostra como tooinstantiate um `ServiceBusRestProxy` e chame `ServiceBusRestProxy->createQueue` toocreate uma fila com o nome `myqueue` dentro de um `MySBNamespace` espaço de nomes do serviço:</span><span class="sxs-lookup"><span data-stu-id="b6558-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="b6558-136">Pode utilizar Olá `listQueues` método no `ServiceBusRestProxy` objetos toocheck se uma fila com um nome especificado já existe num espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="b6558-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="b6558-137">Enviar tooa a fila de mensagens</span><span class="sxs-lookup"><span data-stu-id="b6558-137">Send messages tooa queue</span></span>
<span data-ttu-id="b6558-138">uma fila do Service Bus tooa toosend, a aplicação chama Olá `ServiceBusRestProxy->sendQueueMessage` método.</span><span class="sxs-lookup"><span data-stu-id="b6558-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="b6558-139">Olá a seguir mostra código como toosend toohello uma mensagem `myqueue` fila criada anteriormente dentro de `MySBNamespace` espaço de nomes de serviço.</span><span class="sxs-lookup"><span data-stu-id="b6558-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="b6558-140">As mensagens enviadas demasiado (e recebidas do) filas do Service Bus são instâncias da Olá [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="b6558-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="b6558-141">[BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de métodos padrão e as propriedades que são utilizados toohold personalizadas específicas da aplicação propriedades e um corpo de dados arbitrários da aplicação.</span><span class="sxs-lookup"><span data-stu-id="b6558-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="b6558-142">Filas do Service Bus suportam um tamanho da mensagem máximo de 256 KB no Olá [escalão Standard](service-bus-premium-messaging.md) e de 1 MB no Olá [escalão Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="b6558-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="b6558-143">cabeçalho de Olá, que inclui a norma de Olá e propriedades de aplicação personalizada, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="b6558-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="b6558-144">Não há nenhum limite do número de Olá de mensagens contidas numa fila mas não existe um limite no tamanho total do Olá das mensagens hello contidas numa fila.</span><span class="sxs-lookup"><span data-stu-id="b6558-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="b6558-145">Este limite superior em tamanho da fila é de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="b6558-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="b6558-146">Receber mensagens a partir de uma fila</span><span class="sxs-lookup"><span data-stu-id="b6558-146">Receive messages from a queue</span></span>

<span data-ttu-id="b6558-147">Olá melhor forma tooreceive mensagens numa fila é toouse um `ServiceBusRestProxy->receiveQueueMessage` método.</span><span class="sxs-lookup"><span data-stu-id="b6558-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="b6558-148">Podem ser recebidas mensagens em dois modos diferentes: [ *ReceiveAndDelete* ](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) e [ *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="b6558-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="b6558-149">**PeekLock** Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="b6558-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="b6558-150">Quando utilizar [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modo, receber é uma operação única; ou seja, quando o Service Bus recebe um pedido de leitura de uma mensagem numa fila, marca Olá mensagem como consumida e devolve a mesma aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="b6558-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="b6558-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modo é Olá de modelo mais simples e funciona melhor para cenários em que uma aplicação pode tolerar o não processamento de uma mensagem no evento Olá de uma falha.</span><span class="sxs-lookup"><span data-stu-id="b6558-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="b6558-152">toounderstand isto, considere um cenário no quais problemas de consumidor Olá Olá receber o pedido e, em seguida, falhas antes do processamento-lo.</span><span class="sxs-lookup"><span data-stu-id="b6558-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="b6558-153">Porque o Service Bus terá marcado Olá mensagem como consumida, em seguida, quando a aplicação Olá reinicia e começa a consumir novamente mensagens, terá perdido mensagem de saudação foi consumida falhas toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="b6558-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="b6558-154">Na predefinição Olá [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modo, receber uma mensagem torna-se uma operação de duas fases, o que torna possível toosupport aplicações que não toleram mensagens em falta.</span><span class="sxs-lookup"><span data-stu-id="b6558-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="b6558-155">Quando o Service Bus recebe um pedido, localiza toobe Olá seguinte mensagem consumida, bloqueia-tooprevent outros consumidores de receção e, em seguida, devolve a mesma aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="b6558-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="b6558-156">Após a aplicação Olá concluir o processamento da mensagem de saudação (ou armazena a mesma forma fiável para processamento futuro), conclui Olá segunda etapa do Olá receber processo através da transmissão de mensagem de saudação recebida demasiado`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="b6558-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="b6558-157">Quando o Service Bus vê Olá `deleteMessage` chamada, irá marcar a mensagem de saudação como consumida e removê-lo a partir da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="b6558-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="b6558-158">Olá seguinte exemplo mostra como tooreceive e processar uma mensagem utilizando [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modo (Olá predefinido).</span><span class="sxs-lookup"><span data-stu-id="b6558-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="b6558-159">Como falhas de aplicação toohandle e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="b6558-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="b6558-160">O Service Bus fornece toohelp funcionalidade que recuperar corretamente de erros na sua aplicação ou problemas no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="b6558-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="b6558-161">Se uma aplicação recetora não é possível tooprocess Olá mensagem por algum motivo, em seguida, pode chamar Olá `unlockMessage` método na mensagem de saudação recebida (em vez de Olá `deleteMessage` método).</span><span class="sxs-lookup"><span data-stu-id="b6558-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="b6558-162">Isto irá fazer com que a mensagem de saudação do Service Bus toounlock na fila de Olá e torná-lo disponível toobe novamente recebida, quer por Olá mesmo consumir aplicação ou por outra aplicação de consumo.</span><span class="sxs-lookup"><span data-stu-id="b6558-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="b6558-163">Existe também um tempo limite associado à mensagem bloqueada na fila de Olá, e se a mensagem de saudação tooprocess antes de falha de aplicação Olá Olá tempo limite de bloqueio expira (por exemplo, se a falha da aplicação Olá), o barramento de serviço irá desbloquear a mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="b6558-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="b6558-164">No Olá eventos Olá aplicação falhas após o processamento da mensagem de saudação mas antes do Olá `deleteMessage` pedido é emitido, em seguida, mensagem de saudação será reenviada toohello aplicação quando esta reiniciar.</span><span class="sxs-lookup"><span data-stu-id="b6558-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="b6558-165">Isto é frequentemente designado *, pelo menos, uma vez* processamento; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações a mesma mensagem poderá ser reenviada.</span><span class="sxs-lookup"><span data-stu-id="b6558-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="b6558-166">Se o cenário de Olá não conseguir tolerar o processamento duplicado, em seguida, adicionar adicional é recomendada a entrega da mensagem duplicada lógica tooapplications toohandle.</span><span class="sxs-lookup"><span data-stu-id="b6558-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="b6558-167">Isto é, frequentemente, conseguido utilizando Olá `getMessageId` método de mensagem de saudação, que permanece constante nas tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="b6558-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6558-168">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b6558-168">Next steps</span></span>
<span data-ttu-id="b6558-169">Agora que aprendeu as noções básicas de Olá de filas do Service Bus, consulte [filas, tópicos e subscrições] [ Queues, topics, and subscriptions] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b6558-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="b6558-170">Para obter mais informações, visite também Olá [Centro para programadores do PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="b6558-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


