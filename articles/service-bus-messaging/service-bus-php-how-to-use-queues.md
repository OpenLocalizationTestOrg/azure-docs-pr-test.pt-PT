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
# <a name="how-toouse-service-bus-queues-with-php"></a>Como toouse Service Bus são filas com o PHP
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este guia mostra como toouse filas do Service Bus. Exemplos de Olá são escritos no PHP e utilizam Olá [Azure SDK para PHP](../php-download-sdk.md). Olá os cenários abrangidos incluem **criar filas**, **enviar e receber mensagens**, e **eliminar filas**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>Criar uma aplicação PHP
Olá, só é o requisito para criar uma aplicação PHP que acede ao serviço Blob do Azure de Olá Olá referência de classes no Olá [Azure SDK para PHP](../php-download-sdk.md) de dentro do seu código. Pode utilizar qualquer toocreate de ferramentas de desenvolvimento da aplicação ou o bloco de notas.

> [!NOTE]
> A instalação do PHP também tem de ter Olá [OpenSSL extensão](http://php.net/openssl) instalado e ativado.
> 
> 

Neste guia, irá utilizar as funcionalidades de serviço que podem ser chamadas de dentro de uma aplicação PHP localmente, ou no código em execução dentro de uma função da web do Azure, a função de trabalho ou o Web site.

## <a name="get-hello-azure-client-libraries"></a>Obtenha Olá bibliotecas de cliente do Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar o seu toouse aplicação de Service Bus
fila do Service Bus toouse Olá APIs, Olá seguintes:

1. Ficheiro de Carregador automático de Olá de referência utilizando Olá [require_once] [ require_once] instrução.
2. Referência a quaisquer classes que poderá utilizar.

Olá exemplo seguinte mostra como tooinclude Olá Carregador automático de ficheiros e referência Olá `ServicesBuilder` classe.

> [!NOTE]
> Este exemplo (e outros exemplos neste artigo) parte do princípio de que instalou Olá PHP bibliotecas de cliente para o Azure através do compositor. Se instalou bibliotecas Olá manualmente ou como um pacote PEAR, tem de referenciar Olá **WindowsAzure.php** Carregador automático ficheiros.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Nos exemplos de Olá abaixo, Olá `require_once` instrução será sempre apresentada, mas apenas Olá classes necessárias para tooexecute de exemplo de Olá são referenciadas.

## <a name="set-up-a-service-bus-connection"></a>Configurar uma ligação de barramento de serviço
tooinstantiate um cliente do Service Bus, primeiro é necessário ter uma cadeia de ligação válido neste formato:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Onde `Endpoint` normalmente tem um formato Olá `[yourNamespace].servicebus.windows.net`.

toocreate qualquer cliente de serviço do Azure tem de utilizar Olá `ServicesBuilder` classe. Pode:

* Passar ligação Olá cadeia diretamente tooit.
* utilizar Olá **CloudConfigurationManager (CCM)** toocheck externo várias origens para a cadeia de ligação de Olá:
  * Por predefinição vem com suporte para uma origem externa - variáveis de ambientais
  * Pode adicionar novas origens expandindo Olá `ConnectionStringSource` classe

Para obter exemplos Olá aqui descritos, cadeia de ligação de Olá é transmitida diretamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>Criar uma fila
Pode efetuar operações de gestão para filas do Service Bus através de Olá `ServiceBusRestProxy` classe. A `ServiceBusRestProxy` objecto é construído através de Olá `ServicesBuilder::createServiceBusService` método de fábrica com uma cadeia de ligação adequado que encapsula Olá permissões token toomanage-lo.

Olá seguinte exemplo mostra como tooinstantiate um `ServiceBusRestProxy` e chame `ServiceBusRestProxy->createQueue` toocreate uma fila com o nome `myqueue` dentro de um `MySBNamespace` espaço de nomes do serviço:

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
> Pode utilizar Olá `listQueues` método no `ServiceBusRestProxy` objetos toocheck se uma fila com um nome especificado já existe num espaço de nomes.
> 
> 

## <a name="send-messages-tooa-queue"></a>Enviar tooa a fila de mensagens
uma fila do Service Bus tooa toosend, a aplicação chama Olá `ServiceBusRestProxy->sendQueueMessage` método. Olá a seguir mostra código como toosend toohello uma mensagem `myqueue` fila criada anteriormente dentro de `MySBNamespace` espaço de nomes de serviço.

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

As mensagens enviadas demasiado (e recebidas do) filas do Service Bus são instâncias da Olá [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de métodos padrão e as propriedades que são utilizados toohold personalizadas específicas da aplicação propriedades e um corpo de dados arbitrários da aplicação.

Filas do Service Bus suportam um tamanho da mensagem máximo de 256 KB no Olá [escalão Standard](service-bus-premium-messaging.md) e de 1 MB no Olá [escalão Premium](service-bus-premium-messaging.md). cabeçalho de Olá, que inclui a norma de Olá e propriedades de aplicação personalizada, pode ter um tamanho máximo de 64 KB. Não há nenhum limite do número de Olá de mensagens contidas numa fila mas não existe um limite no tamanho total do Olá das mensagens hello contidas numa fila. Este limite superior em tamanho da fila é de 5 GB.

## <a name="receive-messages-from-a-queue"></a>Receber mensagens a partir de uma fila

Olá melhor forma tooreceive mensagens numa fila é toouse um `ServiceBusRestProxy->receiveQueueMessage` método. Podem ser recebidas mensagens em dois modos diferentes: [ *ReceiveAndDelete* ](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) e [ *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock). **PeekLock** Olá predefinido.

Quando utilizar [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modo, receber é uma operação única; ou seja, quando o Service Bus recebe um pedido de leitura de uma mensagem numa fila, marca Olá mensagem como consumida e devolve a mesma aplicação toohello. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modo é Olá de modelo mais simples e funciona melhor para cenários em que uma aplicação pode tolerar o não processamento de uma mensagem no evento Olá de uma falha. toounderstand isto, considere um cenário no quais problemas de consumidor Olá Olá receber o pedido e, em seguida, falhas antes do processamento-lo. Porque o Service Bus terá marcado Olá mensagem como consumida, em seguida, quando a aplicação Olá reinicia e começa a consumir novamente mensagens, terá perdido mensagem de saudação foi consumida falhas toohello anterior.

Na predefinição Olá [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modo, receber uma mensagem torna-se uma operação de duas fases, o que torna possível toosupport aplicações que não toleram mensagens em falta. Quando o Service Bus recebe um pedido, localiza toobe Olá seguinte mensagem consumida, bloqueia-tooprevent outros consumidores de receção e, em seguida, devolve a mesma aplicação toohello. Após a aplicação Olá concluir o processamento da mensagem de saudação (ou armazena a mesma forma fiável para processamento futuro), conclui Olá segunda etapa do Olá receber processo através da transmissão de mensagem de saudação recebida demasiado`ServiceBusRestProxy->deleteMessage`. Quando o Service Bus vê Olá `deleteMessage` chamada, irá marcar a mensagem de saudação como consumida e removê-lo a partir da fila de Olá.

Olá seguinte exemplo mostra como tooreceive e processar uma mensagem utilizando [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modo (Olá predefinido).

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como falhas de aplicação toohandle e mensagens ilegíveis

O Service Bus fornece toohelp funcionalidade que recuperar corretamente de erros na sua aplicação ou problemas no processamento de uma mensagem. Se uma aplicação recetora não é possível tooprocess Olá mensagem por algum motivo, em seguida, pode chamar Olá `unlockMessage` método na mensagem de saudação recebida (em vez de Olá `deleteMessage` método). Isto irá fazer com que a mensagem de saudação do Service Bus toounlock na fila de Olá e torná-lo disponível toobe novamente recebida, quer por Olá mesmo consumir aplicação ou por outra aplicação de consumo.

Existe também um tempo limite associado à mensagem bloqueada na fila de Olá, e se a mensagem de saudação tooprocess antes de falha de aplicação Olá Olá tempo limite de bloqueio expira (por exemplo, se a falha da aplicação Olá), o barramento de serviço irá desbloquear a mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.

No Olá eventos Olá aplicação falhas após o processamento da mensagem de saudação mas antes do Olá `deleteMessage` pedido é emitido, em seguida, mensagem de saudação será reenviada toohello aplicação quando esta reiniciar. Isto é frequentemente designado *, pelo menos, uma vez* processamento; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações a mesma mensagem poderá ser reenviada. Se o cenário de Olá não conseguir tolerar o processamento duplicado, em seguida, adicionar adicional é recomendada a entrega da mensagem duplicada lógica tooapplications toohandle. Isto é, frequentemente, conseguido utilizando Olá `getMessageId` método de mensagem de saudação, que permanece constante nas tentativas de entrega.

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá de filas do Service Bus, consulte [filas, tópicos e subscrições] [ Queues, topics, and subscriptions] para obter mais informações.

Para obter mais informações, visite também Olá [Centro para programadores do PHP](https://azure.microsoft.com/develop/php/).

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


