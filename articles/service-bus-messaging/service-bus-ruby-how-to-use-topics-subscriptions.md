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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>Como toouse Service Bus tópicos e subscrições com Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este artigo descreve como toouse Service Bus tópicos e subscrições de aplicações Ruby. Olá os cenários abrangidos incluem **criação de tópicos e subscrições, criar filtros de subscrição, enviar mensagens** tooa tópico, **mensagens a receber de uma subscrição**, e  **eliminar tópicos e subscrições**. Para obter mais informações sobre os tópicos e subscrições, consulte Olá [passos](#next-steps) secção.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>Criar um tópico
Olá **Azure::ServiceBusService** objeto permite-lhe toowork com tópicos. Olá código seguinte cria um **Azure::ServiceBusService** objeto. toocreate um tópico, utilize Olá `create_topic()` método. Olá seguinte exemplo cria um tópico ou imprime os erros de Olá, se existir alguma.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

Também pode passar uma **Azure::ServiceBus::Topic** objeto com as opções adicionais, que lhe permitem toooverride tópico predefinições, tais como o tamanho da mensagem tempo fila toolive ou máximo. Olá seguinte exemplo mostra a definição de fila máximo Olá too5 GB de tamanho e a hora toolive too1 minuto:

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>Criar subscrições
Subscrições de tópico também são criadas com Olá **Azure::ServiceBusService** objeto. As subscrições são denominadas e podem ter um filtro opcional que restringe o conjunto de Olá de mensagens entregues fila virtual da subscrição toohello.

As subscrições sejam persistentes e irão continuar tooexist até que ambos estes ou hello tópico estão associados, são eliminados. Se a sua aplicação contém a lógica toocreate uma subscrição, deve primeiro verificar se a subscrição de Olá já existe utilizando o método de getSubscription Olá.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Criar uma subscrição com o filtro (MatchAll) predefinido de Olá
Olá **MatchAll** filtro é o filtro predefinido Olá que é utilizado se for especificado qualquer filtro quando é criada uma nova subscrição. Quando Olá **MatchAll** filtro é utilizado, tópico de toohello publicados todas as mensagens são colocadas na fila virtual da subscrição Olá. Olá exemplo seguinte cria uma subscrição com o nome "todas as mensagens" e utiliza Olá predefinido **MatchAll** filtro.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>Criar subscrições com filtros
Também pode definir filtros que lhe permitem toospecify quais as mensagens enviadas tooa tópico deve aparecer dentro de uma subscrição específica.

Olá tipo mais flexível do filtro suportado pelas subscrições é Olá **Azure::ServiceBus::SqlFilter**, que implementa um subconjunto de SQL92. Os filtros do SQL operam nas propriedades de Olá Olá de mensagens de que são publicados toohello tópico. Para obter mais detalhes sobre expressões de Olá que podem ser utilizados com um filtro SQL, consulte Olá [SqlFilter](service-bus-messaging-sql-filter.md) sintaxe.

Pode adicionar filtros tooa subscrição utilizando Olá `create_rule()` método de Olá **Azure::ServiceBusService** objeto. Este método permite-lhe tooadd novos filtros tooan subscrição existente.

Uma vez que o filtro predefinido de Olá é aplicado automaticamente tooall novas subscrições, primeiro deve remover o filtro predefinido de Olá ou Olá **MatchAll** substituirão quaisquer outros filtros pode especificar. Pode remover a regra predefinida de Olá utilizando Olá `delete_rule()` método no Olá **Azure::ServiceBusService** objeto.

Olá exemplo seguinte cria uma subscrição com o nome "mensagens de alta" com um **Azure::ServiceBus::SqlFilter** que seleciona apenas as mensagens com um personalizado `message_number` propriedade superior a 3:

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

Da mesma forma, hello exemplo seguinte cria uma subscrição designada `low-messages` com um **Azure::ServiceBus::SqlFilter** que seleciona apenas as mensagens com um `message_number` propriedade inferior ou igual too3:

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

Quando é enviada uma mensagem agora demasiado`test-topic`, é sempre ser entregue tooreceivers subscrito toohello `all-messages` subscrição de tópico e entregue seletivamente tooreceivers subscrito toohello `high-messages` e `low-messages` (subscrições de tópico consoante o conteúdo da mensagem Olá).

## <a name="send-messages-tooa-topic"></a>Enviar tópico tooa de mensagens
um tópico do Service Bus tooa mensagem toosend, a aplicação tem de utilizar Olá `send_topic_message()` método no Olá **Azure::ServiceBusService** objeto. As mensagens enviadas tooService tópicos de Bus são instâncias da Olá **Azure::ServiceBus::BrokeredMessage** objetos. **Azure::ServiceBus::BrokeredMessage** objetos têm um conjunto de propriedades padrão (tais como `label` e `time_to_live`), um dicionário utilizado toohold personalizadas específicas da aplicação propriedades e um corpo de dados de cadeia. Uma aplicação pode definir o corpo de Olá da mensagem de saudação transferindo uma toohello de valor de cadeia `send_topic_message()` necessário método e quaisquer propriedades padrão são preenchidas por valores predefinidos.

Olá exemplo seguinte demonstra como teste toosend cinco mensagens demasiado`test-topic`. Tenha em atenção que Olá `message_number` varia de acordo com o valor da propriedade personalizada de cada mensagem no iteração Olá do ciclo de Olá (Isto determina a subscrição que recebe esta):

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

Tópicos do Service Bus suportam um tamanho da mensagem máximo de 256 KB no Olá [escalão Standard](service-bus-premium-messaging.md) e de 1 MB no Olá [escalão Premium](service-bus-premium-messaging.md). cabeçalho de Olá, que inclui a norma de Olá e propriedades de aplicação personalizada, pode ter um tamanho máximo de 64 KB. Não existe nenhum limite do número de Olá de mensagens contidas num tópico mas não há um limite no tamanho total do Olá das mensagens hello contidas num tópico. O tamanho do tópico é definido no momento de criação, com um limite superior de 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Receber mensagens de uma subscrição
As mensagens são recebidas a partir de uma subscrição com Olá `receive_subscription_message()` método no Olá **Azure::ServiceBusService** objeto. Por predefinição e as mensagens são read(peak) bloqueado sem eliminá-lo da subscrição Olá. Pode ler e eliminar a mensagem de saudação da subscrição Olá por definição Olá `peek_lock` opção demasiado**falso**.

comportamento predefinido de Olá torna Olá ler e eliminar uma operação de duas etapas, que também torna possível toosupport aplicações que não toleram mensagens em falta. Quando o Service Bus recebe um pedido, localiza Olá seguinte toobe de mensagem consumida, bloqueia-tooprevent outros consumidores receção e, em seguida, devolve a mesma aplicação toohello. Após a aplicação Olá concluir o processamento da mensagem de saudação (ou armazena a mesma forma fiável para processamento futuro), conclui Olá segunda etapa do Olá processo de receção ao chamar `delete_subscription_message()` método e fornecer Olá mensagem toobe eliminado como um parâmetro. Olá `delete_subscription_message()` método irá marcar a mensagem de saudação como consumida e removê-lo da subscrição Olá.

Se hello `:peek_lock` parâmetro estiver definido demasiado**falso**, ler e eliminar a mensagem de saudação torna-se modelo mais simples de Olá e funciona melhor para cenários em que uma aplicação pode tolerar o não processamento uma mensagem de evento de Olá de um Falha. toounderstand isto, considere um cenário no quais problemas de consumidor Olá Olá receber o pedido e, em seguida, falhas antes do processamento-lo. Porque o Service Bus terá marcado Olá mensagem como consumida, em seguida, quando a aplicação Olá reinicia e começa a consumir novamente mensagens, terá perdido mensagem de saudação foi consumida falhas toohello anterior.

Olá exemplo seguinte demonstra como podem ser recebidas mensagens e processados utilizando `receive_subscription_message()`. exemplo de Olá recebe e elimina uma mensagem de Olá `low-messages` subscrição utilizando `:peek_lock` definido demasiado**falso**, em seguida, receber outra mensagem de Olá `high-messages` e, em seguida, elimina Olá mensagem através de `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como falhas de aplicação toohandle e mensagens ilegíveis
O Service Bus fornece toohelp funcionalidade que recuperar corretamente de erros na sua aplicação ou problemas no processamento de uma mensagem. Se uma aplicação recetora não é possível tooprocess Olá mensagem por algum motivo, em seguida, pode chamar Olá `unlock_subscription_message()` método no Olá **Azure::ServiceBusService** objeto. Este causas Olá do Service Bus toounlock mensagem numa subscrição Olá e torná-lo disponível toobe novamente recebida, quer por Olá mesmo consumir aplicação ou por outra aplicação de consumo.

Existe também um tempo limite associado à mensagem bloqueada na subscrição Olá, e se a mensagem de saudação tooprocess antes de falha de aplicação Olá Olá tempo limite de bloqueio expira (por exemplo, se a falha da aplicação Olá), o barramento de serviço irá desbloquear a mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.

No Olá eventos Olá aplicação falhas após o processamento da mensagem de saudação mas antes do Olá `delete_subscription_message()` método é denominado, em seguida, mensagem de saudação é reenviada toohello aplicação quando esta reiniciar. Isto é frequentemente designado *, pelo menos, uma vez processamento*; ou seja, cada mensagem será processada, pelo menos, uma vez, mas em certo Olá situações a mesma mensagem poderá ser reenviada. Se o cenário de Olá não conseguir tolerar o processamento duplicado, os programadores da aplicação devem adicionar entrega da mensagem duplicada toohandle lógica adicional tootheir aplicação. Esta lógica é, frequentemente, conseguida utilizando Olá `message_id` propriedade da mensagem de saudação, que permanecerá constante nas tentativas de entrega.

## <a name="delete-topics-and-subscriptions"></a>Eliminar tópicos e subscrições
Os tópicos e subscrições sejam persistentes e tem de ser explicitamente eliminado quer através de Olá [portal do Azure] [ Azure portal] ou através de programação. exemplo de Olá abaixo demonstra como o tópico de Olá toodelete designados `test-topic`.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

Eliminar um tópico elimina também quaisquer subscrições registadas com o tópico Olá. As subscrições também podem ser eliminadas de modo independente. Olá código seguinte demonstra como subscrição de Olá toodelete designados `high-messages` de Olá `test-topic` tópico:

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá dos tópicos de Service Bus, siga estas toolearn ligações mais.

* Consulte [filas, tópicos e subscrições](service-bus-queues-topics-subscriptions.md).
* Referência da API para [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).
* Visite Olá [Azure SDK para Ruby](https://github.com/Azure/azure-sdk-for-ruby) repositório no GitHub.

[Azure portal]: https://portal.azure.com
