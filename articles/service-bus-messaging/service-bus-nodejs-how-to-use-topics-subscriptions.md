---
title: "aaaHow toouse Service Bus do Azure tópicos e subscrições com o Node.js | Microsoft Docs"
description: "Saiba como toouse Service Bus tópicos e subscrições no Azure a partir de uma aplicação Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>Como tooUse Service Bus tópicos e subscrições com o Node.js

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este guia descreve como toouse Service Bus tópicos e subscrições de aplicações Node.js. Olá os cenários abrangidos incluem **criação de tópicos e subscrições**, **criar filtros de subscrição**, **envio de mensagens** tooa tópico, **receber mensagens de uma subscrição**, e **eliminar tópicos e subscrições**. Para obter mais informações sobre os tópicos e subscrições, consulte Olá [passos](#next-steps) secção.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>Criar uma aplicação Node.js
Crie uma aplicação Node.js em branco. Para obter instruções sobre como criar uma aplicação Node.js, consulte [criar e implementar uma tooan de aplicação Node.js Web Site do Azure], [serviço em nuvem de Node.js] [ Node.js Cloud Service] utilizando o Windows PowerShell ou do Web Site com o WebMatrix.

## <a name="configure-your-application-toouse-service-bus"></a>Configurar o seu toouse aplicação de Service Bus
toouse Service Bus, transfira Olá pacote do Azure do Node.js. Este pacote inclui um conjunto de bibliotecas que comunicam com os serviços de REST do Service Bus Olá.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utilizar o Gestor de pacote de nó (NPM) tooobtain Olá pacote
1. Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), navegue até pasta toohello onde criou o seu exemplo de aplicação.
2. Tipo **npm instalar azure** na janela de comando Olá, que deve resultar numa Olá seguinte saída:

   ```
       azure@0.7.5 node_modules\azure
   ├── dateformat@1.0.2-1.2.3
   ├── xmlbuilder@0.4.2
   ├── node-uuid@1.2.0
   ├── mime@1.2.9
   ├── underscore@1.4.4
   ├── validator@1.1.1
   ├── tunnel@0.0.2
   ├── wns@0.5.3
   ├── xml2js@0.2.7 (sax@0.5.2)
   └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
   ```
3. Pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta localizar o **azure** pacote, que contém as bibliotecas de Olá terá tooaccess tópicos do Service Bus.

### <a name="import-hello-module"></a>Módulo Olá de importação
Utilizar o bloco de notas ou noutro editor de texto, adicionar Olá seguir toohello superior de Olá **server.js** ficheiro da aplicação Olá:

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>Configurar uma ligação de barramento de serviço
Olá módulo do Azure lê as variáveis de ambiente de Olá `AZURE_SERVICEBUS_NAMESPACE` e `AZURE_SERVICEBUS_ACCESS_KEY` para as informações necessárias tooconnect tooService barramento. Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações da conta Olá ao chamar `createServiceBusService`.

Para obter um exemplo de definição de variáveis de ambiente de Olá um serviço em nuvem do Azure, consulte [Node.js o serviço em nuvem com o armazenamento][Node.js Cloud Service with Storage].

Para obter um exemplo de definição de variáveis de ambiente de Olá para um Web site do Azure, consulte [aplicação Web do Node.js com armazenamento][Node.js Web Application with Storage].

## <a name="create-a-topic"></a>Criar um tópico
Olá **ServiceBusService** objeto permite-lhe toowork com tópicos. O código seguinte cria um **ServiceBusService** objeto. Adicione-a junto ao topo da Olá **server.js** ficheiro, após o módulo do Olá instrução tooimport Olá do azure:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Ao chamar `createTopicIfNotExists` no Olá **ServiceBusService** objeto Olá especificado tópico vai ser devolvido (caso exista) ou um novo tópico com o nome especificado Olá será criado. Olá seguinte código utiliza `createTopicIfNotExists` toocreate ou estabelecer ligação com o nome de tópico de toohello `MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

Olá `createServiceBusService` método também suporta opções adicionais, que lhe permitem toooverride tópico predefinições como hora TTL da mensagem ou o tamanho máximo do tópico. Olá exemplo a seguir define Olá too5GB de tamanho máximo de tópico com um período de tempo toolive de 1 minuto:

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a>Filtros
As operações de filtragem opcionais podem ser aplicados toooperations efetuada utilizando **ServiceBusService**. Operações de filtragem pode incluir registo automaticamente repetir, etc. Os filtros são objetos que implementam um método com assinatura de Olá:

```javascript
function handle (requestOptions, next)
```

Depois de efetuar pré-processamentos nas opções de pedido de Olá, Olá chamadas de método `next`, transmitir uma chamada de retorno com Olá assinatura os seguintes:

```javascript
function (returnObject, finalCallback, next)
```

Esta chamada de retorno e após o processamento Olá `returnObject` (hello a resposta do servidor de toohello Olá pedido), tem de chamada de retorno Olá tooeither invocar em seguida, se existir toocontinue outros filtros de processamento ou da invocação do `finalCallback` , caso contrário, tooend Olá invocação de serviço.

Dois filtros que implementa lógica de repetição são incluídos com Olá Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. seguinte Olá cria um **ServiceBusService** objeto que utiliza Olá **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>Criar subscrições
Subscrições de tópico também são criadas com Olá **ServiceBusService** objeto. As subscrições são denominadas e podem ter um filtro opcional que restringe o conjunto de Olá de mensagens entregues fila virtual da subscrição toohello.

> [!NOTE]
> As subscrições sejam persistentes e irão continuar tooexist até que ambos estes ou hello tópico estão associados, são eliminados. Se a sua aplicação contém a lógica toocreate uma subscrição, este deve primeiro verificar se subscrição Olá já existe utilizando o `getSubscription` método.
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Criar uma subscrição com o filtro (MatchAll) predefinido de Olá
Olá **MatchAll** filtro é o filtro predefinido Olá que é utilizado se for especificado qualquer filtro quando é criada uma nova subscrição. Quando Olá **MatchAll** filtro é utilizado, tópico de toohello publicados todas as mensagens são colocadas na fila virtual da subscrição. Olá exemplo seguinte cria uma subscrição com o nome "AllMessages" e utiliza Olá predefinido **MatchAll** filtro.

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>Criar subscrições com filtros
Também pode criar filtros que permitem-lhe tooscope quais as mensagens enviadas tooa tópico deve aparecer dentro de uma subscrição de tópico específica.

Hello mais flexível tipo de filtro suportado pelas subscrições é a **SqlFilter**, que implementa um subconjunto de SQL92. Os filtros do SQL operam nas propriedades de Olá Olá de mensagens de que são publicados toohello tópico. Para obter mais detalhes sobre expressões de Olá que podem ser utilizados com um filtro SQL, consulte Olá [Sqlexpression] [ SqlFilter.SqlExpression] sintaxe.

Os filtros podem ser adicionados tooa subscrição utilizando Olá `createRule` método de Olá **ServiceBusService** objeto. Este método permite-lhe adicionar novos filtros tooan subscrição existente.

> [!NOTE]
> Porque o filtro predefinido de Olá é aplicado automaticamente tooall novas subscrições, primeiro deve remover o filtro predefinido de Olá ou **MatchAll** substituirão quaisquer outros filtros pode especificar. Pode remover a regra predefinida de Olá utilizando Olá `deleteRule` método o **ServiceBusService** objeto.
>
>

Olá exemplo seguinte cria uma subscrição designada `HighMessages` com um **SqlFilter** que seleciona apenas as mensagens com um personalizado `messagenumber` propriedade superior a 3:

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Da mesma forma, hello exemplo seguinte cria uma subscrição designada `LowMessages` com um **SqlFilter** que seleciona apenas as mensagens com um `messagenumber` propriedade inferior ou igual too3:

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Quando é enviada uma mensagem agora demasiado`MyTopic`, sempre serão entregues para recetores subscritos toohello `AllMessages` subscrição de tópico e entregue seletivamente tooreceivers subscrito toohello `HighMessages` e `LowMessages` subscrições de tópico (consoante o modo de conteúdo da mensagem Olá).

## <a name="how-toosend-messages-tooa-topic"></a>Como toosend mensagens tooa tópico
um tópico do Service Bus tooa mensagem toosend, a aplicação tem de utilizar o `sendTopicMessage` método de Olá **ServiceBusService** objeto.
As mensagens enviadas são tópicos do barramento de tooService **BrokeredMessage** objetos.
**BrokeredMessage** objetos têm um conjunto de propriedades padrão (tais como `Label` e `TimeToLive`), um dicionário utilizado toohold personalizadas específicas da aplicação propriedades e um corpo de dados de cadeia. Uma aplicação pode definir o corpo de Olá da mensagem de saudação através da transmissão de um valor de cadeia ao hello `sendTopicMessage` e necessárias propriedades padrão são preenchidas por valores predefinidos.

Olá exemplo seguinte demonstra como toosend cinco mensagens de teste para `MyTopic`. Tenha em atenção que Olá `messagenumber` varia de acordo com o valor da propriedade de cada mensagem no iteração Olá do ciclo de Olá (Isto irá determinar quais as subscrições receberem):

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

Tópicos do Service Bus suportam um tamanho da mensagem máximo de 256 KB no Olá [escalão Standard](service-bus-premium-messaging.md) e de 1 MB no Olá [escalão Premium](service-bus-premium-messaging.md). cabeçalho de Olá, que inclui a norma de Olá e propriedades de aplicação personalizada, pode ter um tamanho máximo de 64 KB. Não existe nenhum limite do número de Olá de mensagens contidas num tópico mas não há um limite no tamanho total do Olá das mensagens hello contidas num tópico. O tamanho do tópico é definido no momento de criação, com um limite superior de 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Receber mensagens de uma subscrição
As mensagens são recebidas a partir de uma subscrição utilizando o `receiveSubscriptionMessage` método no Olá **ServiceBusService** objeto. Por predefinição, as mensagens são eliminadas da subscrição Olá como estes são lidos; No entanto, pode ler (peek) e bloquear a mensagem de saudação sem eliminá-lo da subscrição Olá por definição Olá o parâmetro opcional `isPeekLock` demasiado**verdadeiro**.

comportamento predefinido de Olá de ler e eliminar a mensagem de saudação como parte da operação de receção é Olá de modelo mais simples e funciona melhor para cenários em que uma aplicação pode tolerar o não processamento de uma mensagem no evento Olá de uma falha. toounderstand isto, considere um cenário no qual o Olá de problemas do consumidor receber o pedido e, em seguida, falhas antes do processamento-lo. Porque o Service Bus terá marcado Olá mensagem como consumida, em seguida, quando a aplicação Olá reinicia e começa a consumir novamente mensagens, terá perdido mensagem de saudação foi consumida falhas toohello anterior.

Se hello `isPeekLock` parâmetro estiver definido demasiado**verdadeiro**, Olá receção torna-se uma operação de duas fases, o que torna possível toosupport aplicações que não toleram mensagens em falta. Quando o Service Bus recebe um pedido, localiza Olá seguinte toobe de mensagem consumida, bloqueia-tooprevent outros consumidores receção e, em seguida, devolve a mesma aplicação toohello.
Após a aplicação Olá concluir o processamento da mensagem de saudação (ou armazena a mesma forma fiável para processamento futuro), conclui Olá segunda etapa do processo de receção ao chamar **deleteMessage** método e fornecer o toobe de mensagem eliminar como parâmetro. Olá **deleteMessage** método irá marcar a mensagem de saudação como consumida e removê-lo da subscrição Olá.

Olá exemplo seguinte demonstra como podem ser recebidas mensagens e processados utilizando `receiveSubscriptionMessage`. Olá exemplo recebe pela primeira vez e elimina uma mensagem de Olá 'LowMessages' subscrição e, em seguida, recebe uma mensagem de Olá 'HighMessages' subscrição utilizar `isPeekLock` definir tootrue. Em seguida, elimina Olá mensagem utilizando `deleteMessage`:

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como falhas de aplicação toohandle e mensagens ilegíveis
O Service Bus fornece toohelp funcionalidade que recuperar corretamente de erros na sua aplicação ou problemas no processamento de uma mensagem. Se uma aplicação recetora não é possível tooprocess Olá mensagem por algum motivo, em seguida, pode chamar Olá `unlockMessage` método no **ServiceBusService** objeto. Esta ação irá fazer com que toounlock de barramento de serviço a mensagem na subscrição Olá e torná-lo disponível toobe novamente recebida, quer por Olá mesmo consumir aplicação ou por outra aplicação de consumo.

Existe também um tempo limite associado à mensagem bloqueada na subscrição, e se a mensagem de saudação tooprocess antes de falha de aplicação Olá Olá tempo limite de bloqueio expira (por exemplo, se a falha da aplicação Olá), o Service Bus desbloqueia a mensagem de saudação automaticamente e torna disponível toobe recebida novamente.

No Olá eventos Olá aplicação falhas após o processamento da mensagem de saudação mas antes do Olá `deleteMessage` método é denominado, em seguida, mensagem de saudação será reenviada toohello aplicação quando esta reiniciar. Isto é frequentemente designado *, pelo menos, uma vez processamento*, ou seja, cada mensagem será processada, pelo menos, uma vez, mas em certo Olá situações a mesma mensagem poderá ser reenviada. Se o cenário de Olá não conseguir tolerar o processamento duplicado, os programadores da aplicação devem adicionar entrega da mensagem duplicada toohandle lógica adicional tootheir aplicação. Isto é, frequentemente, conseguido utilizando o **MessageId** propriedade da mensagem de saudação, que permanecerá constante nas tentativas de entrega.

## <a name="delete-topics-and-subscriptions"></a>Eliminar tópicos e subscrições
Os tópicos e subscrições sejam persistentes e tem de ser explicitamente eliminado quer através de Olá [portal do Azure] [ Azure portal] ou através de programação.
Olá exemplo seguinte demonstra como o tópico de Olá toodelete designados `MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

Eliminar um tópico, apagará igualmente quaisquer subscrições registadas com o tópico Olá. As subscrições também podem ser eliminadas de modo independente. O exemplo seguinte mostra como toodelete uma subscrição com o nome `HighMessages` de Olá `MyTopic` tópico:

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>Passos Seguintes
Agora que aprendeu as noções básicas de Olá dos tópicos de Service Bus, siga estas toolearn ligações mais.

* Consulte [filas, tópicos e subscrições][Queues, topics, and subscriptions].
* Referência da API para [SqlFilter][SqlFilter].
* Visite Olá [Azure SDK para o nó] [ Azure SDK for Node] repositório no GitHub.

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[criar e implementar uma tooan de aplicação Node.js Web Site do Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
