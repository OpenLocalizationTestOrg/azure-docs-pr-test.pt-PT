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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="11652-103">Como tooUse Service Bus tópicos e subscrições com o Node.js</span><span class="sxs-lookup"><span data-stu-id="11652-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="11652-104">Este guia descreve como toouse Service Bus tópicos e subscrições de aplicações Node.js.</span><span class="sxs-lookup"><span data-stu-id="11652-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="11652-105">Olá os cenários abrangidos incluem **criação de tópicos e subscrições**, **criar filtros de subscrição**, **envio de mensagens** tooa tópico, **receber mensagens de uma subscrição**, e **eliminar tópicos e subscrições**.</span><span class="sxs-lookup"><span data-stu-id="11652-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="11652-106">Para obter mais informações sobre os tópicos e subscrições, consulte Olá [passos](#next-steps) secção.</span><span class="sxs-lookup"><span data-stu-id="11652-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="11652-107">Criar uma aplicação Node.js</span><span class="sxs-lookup"><span data-stu-id="11652-107">Create a Node.js application</span></span>
<span data-ttu-id="11652-108">Crie uma aplicação Node.js em branco.</span><span class="sxs-lookup"><span data-stu-id="11652-108">Create a blank Node.js application.</span></span> <span data-ttu-id="11652-109">Para obter instruções sobre como criar uma aplicação Node.js, consulte [criar e implementar uma tooan de aplicação Node.js Web Site do Azure], [serviço em nuvem de Node.js] [ Node.js Cloud Service] utilizando o Windows PowerShell ou do Web Site com o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="11652-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="11652-110">Configurar o seu toouse aplicação de Service Bus</span><span class="sxs-lookup"><span data-stu-id="11652-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="11652-111">toouse Service Bus, transfira Olá pacote do Azure do Node.js.</span><span class="sxs-lookup"><span data-stu-id="11652-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="11652-112">Este pacote inclui um conjunto de bibliotecas que comunicam com os serviços de REST do Service Bus Olá.</span><span class="sxs-lookup"><span data-stu-id="11652-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="11652-113">Utilizar o Gestor de pacote de nó (NPM) tooobtain Olá pacote</span><span class="sxs-lookup"><span data-stu-id="11652-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="11652-114">Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), navegue até pasta toohello onde criou o seu exemplo de aplicação.</span><span class="sxs-lookup"><span data-stu-id="11652-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="11652-115">Tipo **npm instalar azure** na janela de comando Olá, que deve resultar numa Olá seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="11652-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="11652-116">Pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="11652-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="11652-117">Dentro dessa pasta localizar o **azure** pacote, que contém as bibliotecas de Olá terá tooaccess tópicos do Service Bus.</span><span class="sxs-lookup"><span data-stu-id="11652-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="11652-118">Módulo Olá de importação</span><span class="sxs-lookup"><span data-stu-id="11652-118">Import hello module</span></span>
<span data-ttu-id="11652-119">Utilizar o bloco de notas ou noutro editor de texto, adicionar Olá seguir toohello superior de Olá **server.js** ficheiro da aplicação Olá:</span><span class="sxs-lookup"><span data-stu-id="11652-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="11652-120">Configurar uma ligação de barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="11652-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="11652-121">Olá módulo do Azure lê as variáveis de ambiente de Olá `AZURE_SERVICEBUS_NAMESPACE` e `AZURE_SERVICEBUS_ACCESS_KEY` para as informações necessárias tooconnect tooService barramento.</span><span class="sxs-lookup"><span data-stu-id="11652-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="11652-122">Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações da conta Olá ao chamar `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="11652-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="11652-123">Para obter um exemplo de definição de variáveis de ambiente de Olá um serviço em nuvem do Azure, consulte [Node.js o serviço em nuvem com o armazenamento][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="11652-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="11652-124">Para obter um exemplo de definição de variáveis de ambiente de Olá para um Web site do Azure, consulte [aplicação Web do Node.js com armazenamento][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="11652-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="11652-125">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="11652-125">Create a topic</span></span>
<span data-ttu-id="11652-126">Olá **ServiceBusService** objeto permite-lhe toowork com tópicos.</span><span class="sxs-lookup"><span data-stu-id="11652-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="11652-127">O código seguinte cria um **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="11652-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="11652-128">Adicione-a junto ao topo da Olá **server.js** ficheiro, após o módulo do Olá instrução tooimport Olá do azure:</span><span class="sxs-lookup"><span data-stu-id="11652-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="11652-129">Ao chamar `createTopicIfNotExists` no Olá **ServiceBusService** objeto Olá especificado tópico vai ser devolvido (caso exista) ou um novo tópico com o nome especificado Olá será criado.</span><span class="sxs-lookup"><span data-stu-id="11652-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="11652-130">Olá seguinte código utiliza `createTopicIfNotExists` toocreate ou estabelecer ligação com o nome de tópico de toohello `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="11652-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="11652-131">Olá `createServiceBusService` método também suporta opções adicionais, que lhe permitem toooverride tópico predefinições como hora TTL da mensagem ou o tamanho máximo do tópico.</span><span class="sxs-lookup"><span data-stu-id="11652-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="11652-132">Olá exemplo a seguir define Olá too5GB de tamanho máximo de tópico com um período de tempo toolive de 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="11652-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="11652-133">Filtros</span><span class="sxs-lookup"><span data-stu-id="11652-133">Filters</span></span>
<span data-ttu-id="11652-134">As operações de filtragem opcionais podem ser aplicados toooperations efetuada utilizando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="11652-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="11652-135">Operações de filtragem pode incluir registo automaticamente repetir, etc. Os filtros são objetos que implementam um método com assinatura de Olá:</span><span class="sxs-lookup"><span data-stu-id="11652-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="11652-136">Depois de efetuar pré-processamentos nas opções de pedido de Olá, Olá chamadas de método `next`, transmitir uma chamada de retorno com Olá assinatura os seguintes:</span><span class="sxs-lookup"><span data-stu-id="11652-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="11652-137">Esta chamada de retorno e após o processamento Olá `returnObject` (hello a resposta do servidor de toohello Olá pedido), tem de chamada de retorno Olá tooeither invocar em seguida, se existir toocontinue outros filtros de processamento ou da invocação do `finalCallback` , caso contrário, tooend Olá invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="11652-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="11652-138">Dois filtros que implementa lógica de repetição são incluídos com Olá Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="11652-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="11652-139">seguinte Olá cria um **ServiceBusService** objeto que utiliza Olá **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="11652-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="11652-140">Criar subscrições</span><span class="sxs-lookup"><span data-stu-id="11652-140">Create subscriptions</span></span>
<span data-ttu-id="11652-141">Subscrições de tópico também são criadas com Olá **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="11652-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="11652-142">As subscrições são denominadas e podem ter um filtro opcional que restringe o conjunto de Olá de mensagens entregues fila virtual da subscrição toohello.</span><span class="sxs-lookup"><span data-stu-id="11652-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="11652-143">As subscrições sejam persistentes e irão continuar tooexist até que ambos estes ou hello tópico estão associados, são eliminados.</span><span class="sxs-lookup"><span data-stu-id="11652-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="11652-144">Se a sua aplicação contém a lógica toocreate uma subscrição, este deve primeiro verificar se subscrição Olá já existe utilizando o `getSubscription` método.</span><span class="sxs-lookup"><span data-stu-id="11652-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="11652-145">Criar uma subscrição com o filtro (MatchAll) predefinido de Olá</span><span class="sxs-lookup"><span data-stu-id="11652-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="11652-146">Olá **MatchAll** filtro é o filtro predefinido Olá que é utilizado se for especificado qualquer filtro quando é criada uma nova subscrição.</span><span class="sxs-lookup"><span data-stu-id="11652-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="11652-147">Quando Olá **MatchAll** filtro é utilizado, tópico de toohello publicados todas as mensagens são colocadas na fila virtual da subscrição.</span><span class="sxs-lookup"><span data-stu-id="11652-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="11652-148">Olá exemplo seguinte cria uma subscrição com o nome "AllMessages" e utiliza Olá predefinido **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="11652-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="11652-149">Criar subscrições com filtros</span><span class="sxs-lookup"><span data-stu-id="11652-149">Create subscriptions with filters</span></span>
<span data-ttu-id="11652-150">Também pode criar filtros que permitem-lhe tooscope quais as mensagens enviadas tooa tópico deve aparecer dentro de uma subscrição de tópico específica.</span><span class="sxs-lookup"><span data-stu-id="11652-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="11652-151">Hello mais flexível tipo de filtro suportado pelas subscrições é a **SqlFilter**, que implementa um subconjunto de SQL92.</span><span class="sxs-lookup"><span data-stu-id="11652-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="11652-152">Os filtros do SQL operam nas propriedades de Olá Olá de mensagens de que são publicados toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="11652-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="11652-153">Para obter mais detalhes sobre expressões de Olá que podem ser utilizados com um filtro SQL, consulte Olá [Sqlexpression] [ SqlFilter.SqlExpression] sintaxe.</span><span class="sxs-lookup"><span data-stu-id="11652-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="11652-154">Os filtros podem ser adicionados tooa subscrição utilizando Olá `createRule` método de Olá **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="11652-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="11652-155">Este método permite-lhe adicionar novos filtros tooan subscrição existente.</span><span class="sxs-lookup"><span data-stu-id="11652-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="11652-156">Porque o filtro predefinido de Olá é aplicado automaticamente tooall novas subscrições, primeiro deve remover o filtro predefinido de Olá ou **MatchAll** substituirão quaisquer outros filtros pode especificar.</span><span class="sxs-lookup"><span data-stu-id="11652-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="11652-157">Pode remover a regra predefinida de Olá utilizando Olá `deleteRule` método o **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="11652-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="11652-158">Olá exemplo seguinte cria uma subscrição designada `HighMessages` com um **SqlFilter** que seleciona apenas as mensagens com um personalizado `messagenumber` propriedade superior a 3:</span><span class="sxs-lookup"><span data-stu-id="11652-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="11652-159">Da mesma forma, hello exemplo seguinte cria uma subscrição designada `LowMessages` com um **SqlFilter** que seleciona apenas as mensagens com um `messagenumber` propriedade inferior ou igual too3:</span><span class="sxs-lookup"><span data-stu-id="11652-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="11652-160">Quando é enviada uma mensagem agora demasiado`MyTopic`, sempre serão entregues para recetores subscritos toohello `AllMessages` subscrição de tópico e entregue seletivamente tooreceivers subscrito toohello `HighMessages` e `LowMessages` subscrições de tópico (consoante o modo de conteúdo da mensagem Olá).</span><span class="sxs-lookup"><span data-stu-id="11652-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="11652-161">Como toosend mensagens tooa tópico</span><span class="sxs-lookup"><span data-stu-id="11652-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="11652-162">um tópico do Service Bus tooa mensagem toosend, a aplicação tem de utilizar o `sendTopicMessage` método de Olá **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="11652-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="11652-163">As mensagens enviadas são tópicos do barramento de tooService **BrokeredMessage** objetos.</span><span class="sxs-lookup"><span data-stu-id="11652-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="11652-164">**BrokeredMessage** objetos têm um conjunto de propriedades padrão (tais como `Label` e `TimeToLive`), um dicionário utilizado toohold personalizadas específicas da aplicação propriedades e um corpo de dados de cadeia.</span><span class="sxs-lookup"><span data-stu-id="11652-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="11652-165">Uma aplicação pode definir o corpo de Olá da mensagem de saudação através da transmissão de um valor de cadeia ao hello `sendTopicMessage` e necessárias propriedades padrão são preenchidas por valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="11652-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="11652-166">Olá exemplo seguinte demonstra como toosend cinco mensagens de teste para `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="11652-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="11652-167">Tenha em atenção que Olá `messagenumber` varia de acordo com o valor da propriedade de cada mensagem no iteração Olá do ciclo de Olá (Isto irá determinar quais as subscrições receberem):</span><span class="sxs-lookup"><span data-stu-id="11652-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="11652-168">Tópicos do Service Bus suportam um tamanho da mensagem máximo de 256 KB no Olá [escalão Standard](service-bus-premium-messaging.md) e de 1 MB no Olá [escalão Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="11652-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="11652-169">cabeçalho de Olá, que inclui a norma de Olá e propriedades de aplicação personalizada, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="11652-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="11652-170">Não existe nenhum limite do número de Olá de mensagens contidas num tópico mas não há um limite no tamanho total do Olá das mensagens hello contidas num tópico.</span><span class="sxs-lookup"><span data-stu-id="11652-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="11652-171">O tamanho do tópico é definido no momento de criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="11652-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="11652-172">Receber mensagens de uma subscrição</span><span class="sxs-lookup"><span data-stu-id="11652-172">Receive messages from a subscription</span></span>
<span data-ttu-id="11652-173">As mensagens são recebidas a partir de uma subscrição utilizando o `receiveSubscriptionMessage` método no Olá **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="11652-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="11652-174">Por predefinição, as mensagens são eliminadas da subscrição Olá como estes são lidos; No entanto, pode ler (peek) e bloquear a mensagem de saudação sem eliminá-lo da subscrição Olá por definição Olá o parâmetro opcional `isPeekLock` demasiado**verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="11652-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="11652-175">comportamento predefinido de Olá de ler e eliminar a mensagem de saudação como parte da operação de receção é Olá de modelo mais simples e funciona melhor para cenários em que uma aplicação pode tolerar o não processamento de uma mensagem no evento Olá de uma falha.</span><span class="sxs-lookup"><span data-stu-id="11652-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="11652-176">toounderstand isto, considere um cenário no qual o Olá de problemas do consumidor receber o pedido e, em seguida, falhas antes do processamento-lo.</span><span class="sxs-lookup"><span data-stu-id="11652-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="11652-177">Porque o Service Bus terá marcado Olá mensagem como consumida, em seguida, quando a aplicação Olá reinicia e começa a consumir novamente mensagens, terá perdido mensagem de saudação foi consumida falhas toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="11652-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="11652-178">Se hello `isPeekLock` parâmetro estiver definido demasiado**verdadeiro**, Olá receção torna-se uma operação de duas fases, o que torna possível toosupport aplicações que não toleram mensagens em falta.</span><span class="sxs-lookup"><span data-stu-id="11652-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="11652-179">Quando o Service Bus recebe um pedido, localiza Olá seguinte toobe de mensagem consumida, bloqueia-tooprevent outros consumidores receção e, em seguida, devolve a mesma aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="11652-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="11652-180">Após a aplicação Olá concluir o processamento da mensagem de saudação (ou armazena a mesma forma fiável para processamento futuro), conclui Olá segunda etapa do processo de receção ao chamar **deleteMessage** método e fornecer o toobe de mensagem eliminar como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="11652-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="11652-181">Olá **deleteMessage** método irá marcar a mensagem de saudação como consumida e removê-lo da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="11652-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="11652-182">Olá exemplo seguinte demonstra como podem ser recebidas mensagens e processados utilizando `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="11652-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="11652-183">Olá exemplo recebe pela primeira vez e elimina uma mensagem de Olá 'LowMessages' subscrição e, em seguida, recebe uma mensagem de Olá 'HighMessages' subscrição utilizar `isPeekLock` definir tootrue.</span><span class="sxs-lookup"><span data-stu-id="11652-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="11652-184">Em seguida, elimina Olá mensagem utilizando `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="11652-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="11652-185">Como falhas de aplicação toohandle e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="11652-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="11652-186">O Service Bus fornece toohelp funcionalidade que recuperar corretamente de erros na sua aplicação ou problemas no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="11652-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="11652-187">Se uma aplicação recetora não é possível tooprocess Olá mensagem por algum motivo, em seguida, pode chamar Olá `unlockMessage` método no **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="11652-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="11652-188">Esta ação irá fazer com que toounlock de barramento de serviço a mensagem na subscrição Olá e torná-lo disponível toobe novamente recebida, quer por Olá mesmo consumir aplicação ou por outra aplicação de consumo.</span><span class="sxs-lookup"><span data-stu-id="11652-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="11652-189">Existe também um tempo limite associado à mensagem bloqueada na subscrição, e se a mensagem de saudação tooprocess antes de falha de aplicação Olá Olá tempo limite de bloqueio expira (por exemplo, se a falha da aplicação Olá), o Service Bus desbloqueia a mensagem de saudação automaticamente e torna disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="11652-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="11652-190">No Olá eventos Olá aplicação falhas após o processamento da mensagem de saudação mas antes do Olá `deleteMessage` método é denominado, em seguida, mensagem de saudação será reenviada toohello aplicação quando esta reiniciar.</span><span class="sxs-lookup"><span data-stu-id="11652-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="11652-191">Isto é frequentemente designado *, pelo menos, uma vez processamento*, ou seja, cada mensagem será processada, pelo menos, uma vez, mas em certo Olá situações a mesma mensagem poderá ser reenviada.</span><span class="sxs-lookup"><span data-stu-id="11652-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="11652-192">Se o cenário de Olá não conseguir tolerar o processamento duplicado, os programadores da aplicação devem adicionar entrega da mensagem duplicada toohandle lógica adicional tootheir aplicação.</span><span class="sxs-lookup"><span data-stu-id="11652-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="11652-193">Isto é, frequentemente, conseguido utilizando o **MessageId** propriedade da mensagem de saudação, que permanecerá constante nas tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="11652-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="11652-194">Eliminar tópicos e subscrições</span><span class="sxs-lookup"><span data-stu-id="11652-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="11652-195">Os tópicos e subscrições sejam persistentes e tem de ser explicitamente eliminado quer através de Olá [portal do Azure] [ Azure portal] ou através de programação.</span><span class="sxs-lookup"><span data-stu-id="11652-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="11652-196">Olá exemplo seguinte demonstra como o tópico de Olá toodelete designados `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="11652-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="11652-197">Eliminar um tópico, apagará igualmente quaisquer subscrições registadas com o tópico Olá.</span><span class="sxs-lookup"><span data-stu-id="11652-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="11652-198">As subscrições também podem ser eliminadas de modo independente.</span><span class="sxs-lookup"><span data-stu-id="11652-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="11652-199">O exemplo seguinte mostra como toodelete uma subscrição com o nome `HighMessages` de Olá `MyTopic` tópico:</span><span class="sxs-lookup"><span data-stu-id="11652-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="11652-200">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="11652-200">Next Steps</span></span>
<span data-ttu-id="11652-201">Agora que aprendeu as noções básicas de Olá dos tópicos de Service Bus, siga estas toolearn ligações mais.</span><span class="sxs-lookup"><span data-stu-id="11652-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="11652-202">Consulte [filas, tópicos e subscrições][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="11652-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="11652-203">Referência da API para [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="11652-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="11652-204">Visite Olá [Azure SDK para o nó] [ Azure SDK for Node] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="11652-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[criar e implementar uma tooan de aplicação Node.js Web Site do Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
