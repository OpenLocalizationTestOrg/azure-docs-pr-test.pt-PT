---
title: "tópicos do Service Bus aaaHow toouse (Ruby) | Microsoft Docs"
description: "Saiba como toouse Service Bus tópicos e subscrições no Azure. Exemplos de código são escritos para aplicações Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="ed276-104">Como toouse Service Bus tópicos e subscrições com Ruby</span><span class="sxs-lookup"><span data-stu-id="ed276-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="ed276-105">Este artigo descreve como toouse Service Bus tópicos e subscrições de aplicações Ruby.</span><span class="sxs-lookup"><span data-stu-id="ed276-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="ed276-106">Olá os cenários abrangidos incluem **criação de tópicos e subscrições, criar filtros de subscrição, enviar mensagens** tooa tópico, **mensagens a receber de uma subscrição**, e  **eliminar tópicos e subscrições**.</span><span class="sxs-lookup"><span data-stu-id="ed276-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="ed276-107">Para obter mais informações sobre os tópicos e subscrições, consulte Olá [passos](#next-steps) secção.</span><span class="sxs-lookup"><span data-stu-id="ed276-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="ed276-108">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="ed276-108">Create a topic</span></span>
<span data-ttu-id="ed276-109">Olá **Azure::ServiceBusService** objeto permite-lhe toowork com tópicos.</span><span class="sxs-lookup"><span data-stu-id="ed276-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="ed276-110">Olá código seguinte cria um **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ed276-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ed276-111">toocreate um tópico, utilize Olá `create_topic()` método.</span><span class="sxs-lookup"><span data-stu-id="ed276-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="ed276-112">Olá seguinte exemplo cria um tópico ou imprime os erros de Olá, se existir alguma.</span><span class="sxs-lookup"><span data-stu-id="ed276-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="ed276-113">Também pode passar uma **Azure::ServiceBus::Topic** objeto com as opções adicionais, que lhe permitem toooverride tópico predefinições, tais como o tamanho da mensagem tempo fila toolive ou máximo.</span><span class="sxs-lookup"><span data-stu-id="ed276-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="ed276-114">Olá seguinte exemplo mostra a definição de fila máximo Olá too5 GB de tamanho e a hora toolive too1 minuto:</span><span class="sxs-lookup"><span data-stu-id="ed276-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="ed276-115">Criar subscrições</span><span class="sxs-lookup"><span data-stu-id="ed276-115">Create subscriptions</span></span>
<span data-ttu-id="ed276-116">Subscrições de tópico também são criadas com Olá **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ed276-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ed276-117">As subscrições são denominadas e podem ter um filtro opcional que restringe o conjunto de Olá de mensagens entregues fila virtual da subscrição toohello.</span><span class="sxs-lookup"><span data-stu-id="ed276-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="ed276-118">As subscrições sejam persistentes e irão continuar tooexist até que ambos estes ou hello tópico estão associados, são eliminados.</span><span class="sxs-lookup"><span data-stu-id="ed276-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="ed276-119">Se a sua aplicação contém a lógica toocreate uma subscrição, deve primeiro verificar se a subscrição de Olá já existe utilizando o método de getSubscription Olá.</span><span class="sxs-lookup"><span data-stu-id="ed276-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="ed276-120">Criar uma subscrição com o filtro (MatchAll) predefinido de Olá</span><span class="sxs-lookup"><span data-stu-id="ed276-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="ed276-121">Olá **MatchAll** filtro é o filtro predefinido Olá que é utilizado se for especificado qualquer filtro quando é criada uma nova subscrição.</span><span class="sxs-lookup"><span data-stu-id="ed276-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="ed276-122">Quando Olá **MatchAll** filtro é utilizado, tópico de toohello publicados todas as mensagens são colocadas na fila virtual da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="ed276-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="ed276-123">Olá exemplo seguinte cria uma subscrição com o nome "todas as mensagens" e utiliza Olá predefinido **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="ed276-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="ed276-124">Criar subscrições com filtros</span><span class="sxs-lookup"><span data-stu-id="ed276-124">Create subscriptions with filters</span></span>
<span data-ttu-id="ed276-125">Também pode definir filtros que lhe permitem toospecify quais as mensagens enviadas tooa tópico deve aparecer dentro de uma subscrição específica.</span><span class="sxs-lookup"><span data-stu-id="ed276-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="ed276-126">Olá tipo mais flexível do filtro suportado pelas subscrições é Olá **Azure::ServiceBus::SqlFilter**, que implementa um subconjunto de SQL92.</span><span class="sxs-lookup"><span data-stu-id="ed276-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="ed276-127">Os filtros do SQL operam nas propriedades de Olá Olá de mensagens de que são publicados toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="ed276-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="ed276-128">Para obter mais detalhes sobre expressões de Olá que podem ser utilizados com um filtro SQL, consulte Olá [SqlFilter](service-bus-messaging-sql-filter.md) sintaxe.</span><span class="sxs-lookup"><span data-stu-id="ed276-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="ed276-129">Pode adicionar filtros tooa subscrição utilizando Olá `create_rule()` método de Olá **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ed276-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ed276-130">Este método permite-lhe tooadd novos filtros tooan subscrição existente.</span><span class="sxs-lookup"><span data-stu-id="ed276-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="ed276-131">Uma vez que o filtro predefinido de Olá é aplicado automaticamente tooall novas subscrições, primeiro deve remover o filtro predefinido de Olá ou Olá **MatchAll** substituirão quaisquer outros filtros pode especificar.</span><span class="sxs-lookup"><span data-stu-id="ed276-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="ed276-132">Pode remover a regra predefinida de Olá utilizando Olá `delete_rule()` método no Olá **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ed276-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="ed276-133">Olá exemplo seguinte cria uma subscrição com o nome "mensagens de alta" com um **Azure::ServiceBus::SqlFilter** que seleciona apenas as mensagens com um personalizado `message_number` propriedade superior a 3:</span><span class="sxs-lookup"><span data-stu-id="ed276-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="ed276-134">Da mesma forma, hello exemplo seguinte cria uma subscrição designada `low-messages` com um **Azure::ServiceBus::SqlFilter** que seleciona apenas as mensagens com um `message_number` propriedade inferior ou igual too3:</span><span class="sxs-lookup"><span data-stu-id="ed276-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="ed276-135">Quando é enviada uma mensagem agora demasiado`test-topic`, é sempre ser entregue tooreceivers subscrito toohello `all-messages` subscrição de tópico e entregue seletivamente tooreceivers subscrito toohello `high-messages` e `low-messages` (subscrições de tópico consoante o conteúdo da mensagem Olá).</span><span class="sxs-lookup"><span data-stu-id="ed276-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="ed276-136">Enviar tópico tooa de mensagens</span><span class="sxs-lookup"><span data-stu-id="ed276-136">Send messages tooa topic</span></span>
<span data-ttu-id="ed276-137">um tópico do Service Bus tooa mensagem toosend, a aplicação tem de utilizar Olá `send_topic_message()` método no Olá **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ed276-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ed276-138">As mensagens enviadas tooService tópicos de Bus são instâncias da Olá **Azure::ServiceBus::BrokeredMessage** objetos.</span><span class="sxs-lookup"><span data-stu-id="ed276-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="ed276-139">**Azure::ServiceBus::BrokeredMessage** objetos têm um conjunto de propriedades padrão (tais como `label` e `time_to_live`), um dicionário utilizado toohold personalizadas específicas da aplicação propriedades e um corpo de dados de cadeia.</span><span class="sxs-lookup"><span data-stu-id="ed276-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="ed276-140">Uma aplicação pode definir o corpo de Olá da mensagem de saudação transferindo uma toohello de valor de cadeia `send_topic_message()` necessário método e quaisquer propriedades padrão são preenchidas por valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="ed276-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="ed276-141">Olá exemplo seguinte demonstra como teste toosend cinco mensagens demasiado`test-topic`.</span><span class="sxs-lookup"><span data-stu-id="ed276-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="ed276-142">Tenha em atenção que Olá `message_number` varia de acordo com o valor da propriedade personalizada de cada mensagem no iteração Olá do ciclo de Olá (Isto determina a subscrição que recebe esta):</span><span class="sxs-lookup"><span data-stu-id="ed276-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="ed276-143">Tópicos do Service Bus suportam um tamanho da mensagem máximo de 256 KB no Olá [escalão Standard](service-bus-premium-messaging.md) e de 1 MB no Olá [escalão Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="ed276-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ed276-144">cabeçalho de Olá, que inclui a norma de Olá e propriedades de aplicação personalizada, pode ter um tamanho máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="ed276-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ed276-145">Não existe nenhum limite do número de Olá de mensagens contidas num tópico mas não há um limite no tamanho total do Olá das mensagens hello contidas num tópico.</span><span class="sxs-lookup"><span data-stu-id="ed276-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="ed276-146">O tamanho do tópico é definido no momento de criação, com um limite superior de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="ed276-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="ed276-147">Receber mensagens de uma subscrição</span><span class="sxs-lookup"><span data-stu-id="ed276-147">Receive messages from a subscription</span></span>
<span data-ttu-id="ed276-148">As mensagens são recebidas a partir de uma subscrição com Olá `receive_subscription_message()` método no Olá **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ed276-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ed276-149">Por predefinição e as mensagens são read(peak) bloqueado sem eliminá-lo da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="ed276-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="ed276-150">Pode ler e eliminar a mensagem de saudação da subscrição Olá por definição Olá `peek_lock` opção demasiado**falso**.</span><span class="sxs-lookup"><span data-stu-id="ed276-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="ed276-151">comportamento predefinido de Olá torna Olá ler e eliminar uma operação de duas etapas, que também torna possível toosupport aplicações que não toleram mensagens em falta.</span><span class="sxs-lookup"><span data-stu-id="ed276-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ed276-152">Quando o Service Bus recebe um pedido, localiza Olá seguinte toobe de mensagem consumida, bloqueia-tooprevent outros consumidores receção e, em seguida, devolve a mesma aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="ed276-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="ed276-153">Após a aplicação Olá concluir o processamento da mensagem de saudação (ou armazena a mesma forma fiável para processamento futuro), conclui Olá segunda etapa do Olá processo de receção ao chamar `delete_subscription_message()` método e fornecer Olá mensagem toobe eliminado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ed276-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="ed276-154">Olá `delete_subscription_message()` método irá marcar a mensagem de saudação como consumida e removê-lo da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="ed276-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="ed276-155">Se hello `:peek_lock` parâmetro estiver definido demasiado**falso**, ler e eliminar a mensagem de saudação torna-se modelo mais simples de Olá e funciona melhor para cenários em que uma aplicação pode tolerar o não processamento uma mensagem de evento de Olá de um Falha.</span><span class="sxs-lookup"><span data-stu-id="ed276-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="ed276-156">toounderstand isto, considere um cenário no quais problemas de consumidor Olá Olá receber o pedido e, em seguida, falhas antes do processamento-lo.</span><span class="sxs-lookup"><span data-stu-id="ed276-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="ed276-157">Porque o Service Bus terá marcado Olá mensagem como consumida, em seguida, quando a aplicação Olá reinicia e começa a consumir novamente mensagens, terá perdido mensagem de saudação foi consumida falhas toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="ed276-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="ed276-158">Olá exemplo seguinte demonstra como podem ser recebidas mensagens e processados utilizando `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="ed276-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="ed276-159">exemplo de Olá recebe e elimina uma mensagem de Olá `low-messages` subscrição utilizando `:peek_lock` definido demasiado**falso**, em seguida, receber outra mensagem de Olá `high-messages` e, em seguida, elimina Olá mensagem através de `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="ed276-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ed276-160">Como falhas de aplicação toohandle e mensagens ilegíveis</span><span class="sxs-lookup"><span data-stu-id="ed276-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="ed276-161">O Service Bus fornece toohelp funcionalidade que recuperar corretamente de erros na sua aplicação ou problemas no processamento de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="ed276-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ed276-162">Se uma aplicação recetora não é possível tooprocess Olá mensagem por algum motivo, em seguida, pode chamar Olá `unlock_subscription_message()` método no Olá **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ed276-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ed276-163">Este causas Olá do Service Bus toounlock mensagem numa subscrição Olá e torná-lo disponível toobe novamente recebida, quer por Olá mesmo consumir aplicação ou por outra aplicação de consumo.</span><span class="sxs-lookup"><span data-stu-id="ed276-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ed276-164">Existe também um tempo limite associado à mensagem bloqueada na subscrição Olá, e se a mensagem de saudação tooprocess antes de falha de aplicação Olá Olá tempo limite de bloqueio expira (por exemplo, se a falha da aplicação Olá), o barramento de serviço irá desbloquear a mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.</span><span class="sxs-lookup"><span data-stu-id="ed276-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="ed276-165">No Olá eventos Olá aplicação falhas após o processamento da mensagem de saudação mas antes do Olá `delete_subscription_message()` método é denominado, em seguida, mensagem de saudação é reenviada toohello aplicação quando esta reiniciar.</span><span class="sxs-lookup"><span data-stu-id="ed276-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="ed276-166">Isto é frequentemente designado *, pelo menos, uma vez processamento*; ou seja, cada mensagem será processada, pelo menos, uma vez, mas em certo Olá situações a mesma mensagem poderá ser reenviada.</span><span class="sxs-lookup"><span data-stu-id="ed276-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="ed276-167">Se o cenário de Olá não conseguir tolerar o processamento duplicado, os programadores da aplicação devem adicionar entrega da mensagem duplicada toohandle lógica adicional tootheir aplicação.</span><span class="sxs-lookup"><span data-stu-id="ed276-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="ed276-168">Esta lógica é, frequentemente, conseguida utilizando Olá `message_id` propriedade da mensagem de saudação, que permanecerá constante nas tentativas de entrega.</span><span class="sxs-lookup"><span data-stu-id="ed276-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="ed276-169">Eliminar tópicos e subscrições</span><span class="sxs-lookup"><span data-stu-id="ed276-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="ed276-170">Os tópicos e subscrições sejam persistentes e tem de ser explicitamente eliminado quer através de Olá [portal do Azure] [ Azure portal] ou através de programação.</span><span class="sxs-lookup"><span data-stu-id="ed276-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="ed276-171">exemplo de Olá abaixo demonstra como o tópico de Olá toodelete designados `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="ed276-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="ed276-172">Eliminar um tópico elimina também quaisquer subscrições registadas com o tópico Olá.</span><span class="sxs-lookup"><span data-stu-id="ed276-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="ed276-173">As subscrições também podem ser eliminadas de modo independente.</span><span class="sxs-lookup"><span data-stu-id="ed276-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="ed276-174">Olá código seguinte demonstra como subscrição de Olá toodelete designados `high-messages` de Olá `test-topic` tópico:</span><span class="sxs-lookup"><span data-stu-id="ed276-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="ed276-175">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ed276-175">Next steps</span></span>
<span data-ttu-id="ed276-176">Agora que aprendeu as noções básicas de Olá dos tópicos de Service Bus, siga estas toolearn ligações mais.</span><span class="sxs-lookup"><span data-stu-id="ed276-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="ed276-177">Consulte [filas, tópicos e subscrições](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="ed276-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="ed276-178">Referência da API para [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="ed276-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="ed276-179">Visite Olá [Azure SDK para Ruby](https://github.com/Azure/azure-sdk-for-ruby) repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ed276-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
