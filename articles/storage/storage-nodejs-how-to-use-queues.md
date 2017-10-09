---
title: aaaHow toouse armazenamento de filas do Node.js | Microsoft Docs
description: "Saiba como toouse Olá filas do Azure service toocreate e filas de eliminação e inserção, obterem e eliminar as mensagens. Amostras de escrita no Node.js."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 977e5994c0be1b5d71c60b7479698ccb694ab860
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a>Como toouse armazenamento de filas do Node.js
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Descrição geral
Este guia mostra como tooperform cenários comuns utilizando Olá serviço fila do Microsoft Azure. Exemplos de Olá são escritos utilizando Olá Node.js API. Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar e eliminar filas**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Criar uma aplicação Node.js
Crie uma aplicação Node.js em branco. Para obter instruções sobre como criar uma aplicação Node.js, consulte [criar uma aplicação web Node.js no App Service do Azure], [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure] utilizando o Windows PowerShell ou [ Criar e implementar uma aplicação de web Node.js tooAzure utilizando a Web Matrix].

## <a name="configure-your-application-tooaccess-storage"></a>Configurar a sua aplicação tooAccess armazenamento
toouse storage do Azure, terá de Olá SDK de armazenamento do Azure para Node.js, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utilizar o Gestor de pacote de nó (NPM) tooobtain Olá pacote
1. Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), navegue até pasta toohello onde criou o seu exemplo de aplicação.
2. Tipo **npm instalar storage do azure** na janela de comandos Olá. O resultado do comando de Olá é semelhante toohello seguinte o exemplo.
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. Pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta encontrará Olá **storage do azure** pacote, que contém as bibliotecas de Olá precisa de aceder ao armazenamento.

### <a name="import-hello-package"></a>Importar o pacote de Olá
Utilizar o bloco de notas ou noutro editor de texto, adicionar Olá toohello principais a seguir a **server.js** ficheiro da aplicação olá onde pretende toouse armazenamento:

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Configurar uma ligação de armazenamento do Azure
módulo Olá do azure será lida a variáveis de ambiente de Olá AZURE\_armazenamento\_conta e o AZURE\_armazenamento\_acesso\_chave ou o AZURE\_armazenamento\_ligação \_Cadeia de informações necessárias tooconnect tooyour conta do storage do Azure. Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações da conta Olá ao chamar **createQueueService**.

Para obter um exemplo de definir variáveis de ambiente de Olá na Olá [Portal do Azure](https://portal.azure.com) para um Web site do Azure, consulte [através da aplicação de web de Node.js Olá o serviço de tabela do Azure].

## <a name="how-to-create-a-queue"></a>Como: Criar uma fila
Olá código seguinte cria um **QueueService** objeto, que permite-lhe toowork com as filas.

```
var queueSvc = azure.createQueueService();
```

Olá utilize **createQueueIfNotExists** método, que devolve a fila especificada Olá se já existe ou cria uma nova fila com o nome especificado Olá se já existir.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Se a fila de Olá é criada, `result.created` é verdadeiro. Se existir a fila de Olá, `result.created` é falso.

### <a name="filters"></a>Filtros
As operações de filtragem opcionais podem ser aplicados toooperations efetuada utilizando **QueueService**. Operações de filtragem pode incluir registo automaticamente repetir, etc. Os filtros são objetos que implementam um método com assinatura de Olá:

```
function handle (requestOptions, next)
```

Depois de efetuar a respetiva pré-processamentos nas opções de pedido de Olá, o método de Olá necessita toocall "seguinte" transmitir uma chamada de retorno com Olá assinatura os seguintes:

```
function (returnObject, finalCallback, next)
```

Esta chamada de retorno e após o processamento Olá returnObject (resposta de hello do servidor de toohello Olá pedido), a chamada de retorno de Olá tem tooeither invocar em seguida, se existir toocontinue outros filtros de processamento ou simplesmente invocar finalCallback tooend; caso contrário, cópia de segurança Olá invocação de serviço.

Dois filtros que implementa lógica de repetição são incluídos com Olá Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. seguinte Olá cria um **QueueService** objeto que utiliza Olá **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Como: Introduzir uma mensagem para uma fila
tooinsert uma mensagem para uma fila, utilize Olá **createMessage** método para criar uma nova mensagem e adicioná-lo toohello fila.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>Como: Pré-visualizar Olá a mensagem seguinte
Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **peekMessages** método. Por predefinição, **peekMessages** observa uma única mensagem.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

Olá `result` contém mensagem de saudação.

> [!NOTE]
> Utilizar **peekMessages** quando existem não existem mensagens na fila de Olá não devolverá um erro, no entanto, não existem mensagens vai ser devolvidas.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>Como: Anular Olá a mensagem seguinte
A processar uma mensagem é um processo de duas fases:

1. Anular a mensagem de saudação.
2. Elimine a mensagem de saudação.

utilizar toodequeue uma mensagem, **getMessages**. Isto faz com que mensagens hello invisível na fila de Olá, pelo que não existem outros clientes podem processá-los. Assim que a aplicação tem de processar uma mensagem, chamar **deleteMessage** toodelete a fila de Olá. Olá seguinte o exemplo obtém uma mensagem, em seguida, elimina-a:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> Por predefinição, uma mensagem apenas está oculto para 30 segundos, após o qual é visível tooother clientes. Pode especificar um valor diferente utilizando `options.visibilityTimeout` com **getMessages**.
> 
> [!NOTE]
> Utilizar **getMessages** quando existem não existem mensagens na fila de Olá não devolverá um erro, no entanto, não existem mensagens vai ser devolvidas.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: Alterar Olá conteúdo de uma mensagem em fila
Pode alterar o conteúdo de Olá de um mensagem no local na Olá fila utilizando **updateMessage**. Olá texto Olá de atualizações de exemplo de uma mensagem a seguir:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Como: Mensagens de opções adicionais para Dequeuing
Existem duas formas que pode personalizar a obtenção de mensagens numa fila:

* `options.numOfMessages`-Obter um lote de mensagens em fila (cópia de segurança too32.)
* `options.visibilityTimeout`-Defina um tempo de limite de invisibilidade superiores ou inferiores.

Olá exemplo seguinte utiliza Olá **getMessages** mensagens tooget 15 de método numa chamada. Em seguida, processa cada mensagem utilizando um ciclo for. Também define minutos toofive de tempo limite de invisibilidade do Olá para todas as mensagens devolvidos por este método.

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a>Como: Obter Olá comprimento da fila
Olá **getQueueMetadata** devolve os metadados sobre fila Olá, incluindo o número aproximado de Olá de mensagens a aguardar na fila de Olá.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>Como: Filas de lista
tooretrieve uma lista de filas, utilize **listQueuesSegmented**. tooretrieve uma lista filtrados por um prefixo específico, utilize **listQueuesSegmentedWithPrefix**.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

Se não podem ser devolvidas todas as filas, `result.continuationToken` pode ser utilizada como Olá primeiro parâmetro de **listQueuesSegmented** ou Olá segundo parâmetro de **listQueuesSegmentedWithPrefix** tooretrieve mais resultados.

## <a name="how-to-delete-a-queue"></a>Como: Eliminar uma fila
toodelete uma fila e todas as mensagens de Olá nela contidas, chame o **deleteQueue** método no objeto de fila de Olá.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

tooclear todas as mensagens de uma fila sem eliminá-lo, utilize **clearMessages**.

## <a name="how-to-work-with-shared-access-signatures"></a>Como: trabalhar com assinaturas de acesso partilhado
Assinaturas de acesso partilhado (SAS) são uma tooqueues de acesso granulares tooprovide de forma segura sem fornecer o nome da conta de armazenamento ou chaves. SAS são frequentemente utilizados tooprovide limitada para aceder a filas tooyour, tais como permitir que uma aplicação móvel toosubmit mensagens.

Uma aplicação como um serviço baseado na nuvem fidedigna gera uma SAS utilizando Olá **generateSharedAccessSignature** de Olá **QueueService**e fornece-tooan fidedigna ou fidedigna por aplicação. Por exemplo, uma aplicação móvel. Olá SAS é gerado utilizando uma política, que descreve o início de Olá e datas final durante o qual Olá SAS é válido, bem como Olá marcador de posição SAS de toohello concedida ao nível de acesso.

Olá seguinte o exemplo gera uma nova política de acesso partilhado, o que permitirá Olá SAS marcador de posição tooadd toohello a fila de mensagens e expira 100 minutos após a hora de Olá que é criado.

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

Tenha em atenção que as informações do anfitrião Olá têm de ser fornecidos também, conforme necessário, quando o marcador de posição do Olá SAS tentativas de fila de Olá tooaccess.

Olá aplicação cliente, em seguida, utiliza Olá SAS com **QueueServiceWithSAS** tooperform operações em relação a fila de Olá. Olá seguinte o exemplo liga toohello fila e cria uma mensagem.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Uma vez que hello SAS foi gerado com adicionar acesso, se foi efetuada uma tentativa tooread, atualizar ou eliminar as mensagens, será devolvido um erro.

### <a name="access-control-lists"></a>Lista de controlo de acesso
Também pode utilizar uma política de acesso de Olá de tooset de lista de controlo de acesso (ACL) para um SAS. Isto é útil se desejar tooallow fila do Olá vários tooaccess de clientes, mas fornecem as políticas de acesso diferentes para cada cliente.

Uma ACL é implementada com uma matriz de políticas de acesso, com um ID associado a cada política. Olá seguinte o exemplo define duas políticas; um para 'user1' e outra para 'Utilizador2':

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Olá seguinte obtém do exemplo Olá ACL atual para **myqueue**, em seguida, adiciona novas políticas de Olá utilizando **setQueueAcl**. Esta abordagem permite:

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Uma vez Olá que ACL foi definida, pode, em seguida, crie um SAS com base no ID de Olá para uma política. Olá seguinte exemplo cria um novo SAS para 'Utilizador2':

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>Passos Seguintes
Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.

* Visite Olá [blogue da equipa de armazenamento do Azure][Azure Storage Team Blog].
* Visite Olá [SDK de armazenamento do Azure para o nó] [ Azure Storage SDK for Node] repositório no GitHub.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[criar uma aplicação web Node.js no App Service do Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[através da aplicação de web de Node.js Olá o serviço de tabela do Azure]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ Criar e implementar uma aplicação de web Node.js tooAzure utilizando a Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
