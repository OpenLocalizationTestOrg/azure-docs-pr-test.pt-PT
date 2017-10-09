---
title: "aaaBest práticas para melhorar o desempenho da utilização do Azure Service Bus | Microsoft Docs"
description: Descreve como toouse desempenho de toooptimize do Service Bus ao comutar mediadas mensagens.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>Melhores práticas para melhorias de desempenho através de mensagens do Service Bus

Este artigo descreve como toouse [mensagens do Service Bus do Azure](https://azure.microsoft.com/services/service-bus/) toooptimize desempenho ao trocar as mensagens mediadas. Olá primeira parte deste tópico descreve os mecanismos de diferentes Olá que são oferecidos toohelp aumento do desempenho. segunda parte do Olá fornece orientações para a forma como toouse Service Bus de forma a que pode oferecer Olá melhor desempenho num determinado cenário.

Ao longo deste tópico, o termo de Olá "cliente" refere-se tooany entidade que acede ao Service Bus. Um cliente pode levar a função de Olá de um remetente ou um recetor. termo Olá ". o remetente" é utilizado para um cliente de fila ou um tópico de barramento de serviço que envia mensagens tooa barramento de serviço fila ou um tópico. termo Olá "recetor" refere-se tooa fila ou a subscrição do cliente do Service Bus que recebe mensagens a partir de uma fila do Service Bus ou uma subscrição.

Estas secções apresentam alguns conceitos que o Service Bus utiliza toohelp desempenho de aumento.

## <a name="protocols"></a>Protocolos
Permite que os clientes toosend ao Service Bus e receber mensagens através de um dos três protocolos:

1. (AMQP) do protocolo de colocação de mensagens de avançadas
2. Mensagens (SBMP) do protocolo do Service Bus
3. HTTP

AMQP e SBMP são mais eficientes porque sejam mantidas Olá ligação tooService Bus, desde a fábrica de mensagens hello existe. Também implementa a criação de batches e prefetching. A menos que explicitamente mencionado, todo o conteúdo deste tópico assume que a utilização Olá AMQP ou SBMP.

## <a name="reusing-factories-and-clients"></a>Reutilizar fábricas e clientes
Cliente do Service Bus objetos, tais como [QueueClient] [ QueueClient] ou [MessageSender][MessageSender], são criados através de um [ MessagingFactory] [ MessagingFactory] objeto, que também fornece gestão interno de ligações. Não deve fechar fábricas de mensagens ou fila, tópico, subscrição clientes e depois de enviar uma mensagem e, em seguida, recrie-las quando enviar mensagem de saudação seguinte. Fechar uma fábrica de mensagens elimina o serviço do Service Bus Olá ligação toohello e uma nova ligação é estabelecida quando recriar fábrica Olá. Estabelecer que uma ligação é uma operação dispendiosa, que pode evitar utilizando novamente Olá mesmo definições de fábrica e cliente objetos para várias operações. Pode utilizar em segurança Olá [QueueClient] [ QueueClient] objeto para envio de mensagens de operações assíncronas em simultâneo e de vários threads. 

## <a name="concurrent-operations"></a>Operações simultâneas
Efetuar uma operação (enviar, receber, eliminar, etc.) demora algum tempo. Neste momento inclui o processamento de Olá da operação de Olá pelo Olá serviço do Service Bus na latência de toohello adição do pedido de Olá e resposta de Olá. tooincrease Olá diversas operações por hora, operações tem de executar em simultâneo. Pode fazê-lo de várias formas diferentes:

* **Operações assíncronas**: cliente Olá agendas operações através de operações assíncronas. pedido seguinte Olá é iniciado antes de Olá anterior é concluído. Olá segue-se um exemplo de uma operação de envio assíncrono:
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  Este é um exemplo de uma recepção assíncrona a operação:
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **Várias fábricas**: Olá, todos os clientes (remetentes na adição tooreceivers) que são criados pela mesma fábrica partilha uma ligação TCP. o débito de mensagem máximo de Olá é limitado pelo número de Olá de operações que pode seguir esta ligação de TCP. débito Olá que pode ser obtido com uma única fábrica varia bastante com vezes reportadas round-trip TCP e tamanho da mensagem. tooobtain taxas de débito superiores, deve utilizar várias fábricas de mensagens.

## <a name="receive-mode"></a>Receber modo
Ao criar um cliente de fila ou a subscrição, pode especificar um modo de receção: *bloqueio observar* ou *receber e eliminar*. predefinição de Olá receber modo é [PeekLock][PeekLock]. Durante o funcionamento neste modo, Olá cliente envia um pedido tooreceive uma mensagem do barramento de serviço. Após ter recebido uma mensagem de saudação cliente Olá, envia uma mensagem de saudação do pedido toocomplete.

Quando definir Olá receber modo demasiado[ReceiveAndDelete][ReceiveAndDelete], os dois passos são combinados num único pedido. Esta reduz Olá global número de operações e pode melhorar o Olá débito global de mensagens. Este ganhos de desempenho é fornecido em risco de Olá de perda de mensagens.

Barramento de serviço não suporta transações para receber e-eliminação de operações. Além disso, é necessária para os cenários em que Olá cliente pretende toodefer semântica de bloqueio peek ou [entregues](service-bus-dead-letter-queues.md) uma mensagem.

## <a name="client-side-batching"></a>A criação de batches de lado do cliente
A criação de batches de lado do cliente permite que uma fila ou um tópico cliente toodelay Olá envio de uma mensagem para um determinado período de tempo. Se o cliente de Olá envia mensagens adicionais durante este período de tempo, transmite mensagens hello do batch único. A criação de batches de lado do cliente também faz com que um toobatch de cliente fila ou a subscrição vários **concluída** pedidos num único pedido. Só está disponível para criação de batches assíncrona **enviar** e **concluída** operações. Operações síncronas são imediatamente enviadas toohello o serviço do Service Bus. Criação de batches não ocorrer para peek ou receber operações nem criação de batches ocorre em clientes.

Por predefinição, um cliente utiliza um intervalo de lote de 20ms. Pode alterar o intervalo de lote Olá por definição Olá [BatchFlushInterval] [ BatchFlushInterval] propriedade antes de criar Olá fábrica de mensagens. Esta definição afeta todos os clientes que são criados por esta fábrica.

criação de batches toodisable, defina Olá [BatchFlushInterval] [ BatchFlushInterval] propriedade demasiado**TimeSpan**. Por exemplo:

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

Criação de batches não afeta o número de Olá de operações de mensagens sujeito a faturação e só está disponível para Olá o protocolo de cliente do Service Bus. Olá protocolo HTTP não suporta a criação de batches.

## <a name="batching-store-access"></a>Acesso à loja de criação de batches
débito de Olá tooincrease de uma fila, tópico ou subscrição, o Service Bus lotes várias mensagens quando escreve arquivo interno tooits. Se estiver ativada numa fila ou um tópico, escrever mensagens no arquivo de Olá será possível criar batch. Se estiver ativada num fila ou subscrição, eliminar as mensagens a partir da loja de Olá será possível criar batch. Se o acesso à loja de batches é ativado para uma entidade, o Service Bus atrasa uma operação de escrita de arquivo sobre essa entidade pela cópia de segurança too20ms. Operações de arquivo adicionais que ocorrem durante este intervalo são adicionadas toohello batch. Em lotes afeta apenas o arquivo de acesso **enviar** e **concluída** operações; receber operações não são afetadas. Acesso à loja de batches é uma propriedade numa entidade. Criação de batches ocorre em todas as entidades que permitem acesso à loja de batches.

Ao criar uma nova fila, tópico ou uma subscrição, o acesso à loja de batches está ativado por predefinição. acesso à loja, conjunto Olá em lotes de toodisable [EnableBatchedOperations] [ EnableBatchedOperations] propriedade demasiado**falso** antes de criar a entidade de Olá. Por exemplo:

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

Acesso à loja de batches não afeta o número de Olá de operações de mensagens sujeito a faturação e é uma propriedade de uma fila, tópico ou uma subscrição. É independente da Olá receber modo e Olá protocolo que é utilizado entre um cliente e Olá serviço do Service Bus.

## <a name="prefetching"></a>Prefetching
Prefetching permite a fila ou a subscrição do cliente tooload adicionais mensagens hello do serviço de Olá quando ele efetuar uma operação de receção. cliente de Olá armazena estas mensagens numa cache local. o tamanho da cache de Olá Olá é determinado pelo Olá [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] ou [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] Propriedades. Cada cliente que permitem prefetching mantém a sua própria cache. Uma cache não é partilhada entre os clientes. Se o cliente de Olá inicia uma operação de receção e respetiva cache está vazia, o serviço de Olá transmite um lote de mensagens. o tamanho do lote de Olá Olá é igual ao tamanho de Olá da cache de Olá ou 256 KB, que for mais pequeno. Se o cliente de Olá inicia uma operação de receção e cache Olá contém uma mensagem, mensagem de saudação é obtida a partir da cache de Olá.

Quando uma mensagem é prefetched, mensagem de saudação de bloqueios serviço do Olá prefetched. Ao fazê-lo, mensagem de saudação prefetched não ser recebida por um recetor diferentes. Se o recetor Olá não é possível concluir a mensagem de saudação antes do bloqueio de Olá, mensagem de saudação torna-se disponíveis tooother recetores. cópia de Olá prefetched da mensagem de saudação permanece na cache de Olá. Olá recetor que consome Olá expirou em cache cópia irá receber uma exceção quando tenta toocomplete essa mensagem. Por predefinição, o bloqueio de mensagem de Olá expira após 60 segundos. Este valor pode ser expandida too5 minutos. consumo de Olá tooprevent de mensagens expiradas, o tamanho da cache Olá deve ser sempre inferior ao número de Olá de mensagens em fila que pode ser utilizada por um cliente dentro do intervalo de tempo limite de bloqueio de Olá.

Quando utilizar a expiração do bloqueio predefinido Olá de 60 segundos, o valor é uma boa para [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] é 20 vezes Olá máximo as taxas de processamento de todos os recetores do factory Olá. Por exemplo, uma fábrica cria 3 recetores e cada recetor pode processar segurança too10 mensagens por segundo. Contagem de obtenção prévia Olá não deve exceder 20 X 3, 10 = 600. Por predefinição, [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] é too0 conjunto, o que significa que não existem mensagens adicionais são recuperadas do serviço de Olá.

Prefetching mensagens aumenta Olá débito global para uma fila ou a subscrição porque esta reduz Olá global número de operações de mensagem ou ida e volta. Obter a mensagem de saudação primeiro, no entanto, irá demorar mais tempo (devido toohello aumentada o tamanho da mensagem). Receber mensagens prefetched irá ser mais rápida porque estas mensagens já foram transferidas pelo cliente de Olá.

Olá time-to-live (TTL) propriedade de uma mensagem está marcada pelo servidor Olá momento Olá servidor Olá envia o cliente de toohello Olá mensagem. cliente de Olá não verificar a propriedade TTL da mensagem de saudação quando é recebida a mensagem de saudação. Em vez disso, a mensagem de saudação pode ser recebida, mesmo se o TTL da mensagem de saudação passou enquanto a mensagem de saudação foi colocado em cache pelo cliente de Olá.

Prefetching não afeta o número de Olá de operações de mensagens sujeito a faturação e só está disponível para Olá o protocolo de cliente do Service Bus. Olá protocolo HTTP não suporta prefetching. Prefetching está disponível para operações síncronas e assíncronas recebem operações.

## <a name="express-queues-and-topics"></a>Express filas e tópicos

Entidades expressas ativar cenários de latência reduzidos e débito alto e são suportadas apenas no escalão de serviço de mensagens Standard Olá. Entidades criadas numa [espaços de nomes Premium](service-bus-premium-messaging.md) não suportam a opção rápida Olá. Com entidades expressas, se é enviada uma mensagem de fila de tooa ou um tópico, mensagem de saudação não será imediatamente armazenada no arquivo de mensagens hello. Em vez disso, este é colocado em cache na memória. Se uma mensagem permanece na fila de Olá por mais do que alguns segundos, automaticamente, é escrito armazenamento toostable, deste modo, a proteger contra a perda de devido a indisponibilidade de tooan. Armazenamento na mensagem de saudação do tempo de Olá escrita de mensagem de saudação para uma cache de memória aumenta o débito e reduz a latência porque não há nenhum toostable de acesso é enviado. As mensagens que são consumidas dentro de alguns segundos não são escritas toohello arquivo de mensagens. Olá seguinte exemplo cria um tópico rápido.

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

Se uma mensagem que contém informações críticas que não devem ser perdidas é enviada entidade rápida tooan, remetente Olá pode forçar o Service Bus tooimmediately manter o armazenamento de toostable Olá mensagem por definição Olá [ForcePersistence] [ ForcePersistence] propriedade demasiado**verdadeiro**.

> [!NOTE]
> Entidades expressas não suporta transações.

## <a name="use-of-partitioned-queues-or-topics"></a>Utilização de filas particionadas ou tópicos
Internamente, o Service Bus utiliza Olá mesmo nó de mensagens e arquivo tooprocess e armazenar todas as mensagens de uma entidade de mensagens (fila ou um tópico). Uma fila particionada ou um tópico, no Olá por outro lado, é distribuído por vários nós e arquivos de mensagens. Particionada filas e tópicos não só produzem um débito mais elevado do que o regulares filas e tópicos, estes também apresentem um disponibilidade superior. toocreate uma entidade particionada, conjunto Olá [EnablePartitioning] [ EnablePartitioning] propriedade demasiado**verdadeiro**, conforme mostrado no seguinte exemplo de Olá. Para obter mais informações sobre entidades particionadas, consulte [entidades de mensagens Particionadas][Partitioned messaging entities].

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>Utilização de várias filas

Se não for possível toouse esperada uma fila particionada ou tópico ou Olá carga não pode ser processada por um único fila particionada ou um tópico, tem de utilizar várias entidades de mensagens. Ao utilizar várias entidades, criar um cliente dedicado para cada entidade, em vez de utilizar Olá mesmo cliente para todas as entidades.

## <a name="development-and-testing-features"></a>Desenvolvimento e teste de funcionalidades

Barramento de serviço possui uma funcionalidade que é utilizada especificamente para o desenvolvimento que **nunca deve ser utilizado em configurações de produção**: [TopicDescription.EnableFilteringMessagesBeforePublishing][].

Quando novas regras ou filtros são adicionados toohello tópico, pode utilizar [TopicDescription.EnableFilteringMessagesBeforePublishing][] tooverify Olá nova expressão de filtro está a funcionar conforme esperado.

## <a name="scenarios"></a>Cenários
Olá secções seguintes descrevem cenários típicos de mensagens e descrevem as definições de Service Bus Olá preferido. Taxas de débito são classificadas como pequenos (menos 1 mensagem por segundo), moderada (1 mensagem por segundo ou superior, mas inferior a 100 mensagens por segundo) e a elevada (100 mensagens/segundo ou superior). Olá número de clientes que está classificado como pequena moderada (5 ou menos), (mais de 5, mas inferior a ou igual too20) e grande (mais do que 20).

### <a name="high-throughput-queue"></a>Fila de débito elevado
Objetivo: Maximize o débito de Olá de uma fila única. número de Olá de remetentes e os recetores é pequeno.

* Utilize uma fila de mensagens particionada para um melhor desempenho e disponibilidade.
* Olá tooincrease geral taxa de envio na fila de Olá, utilize vários remetentes de toocreate de fábricas de mensagens. Para cada remetente, utilize operações assíncronas ou de vários threads.
* Olá tooincrease geral receber taxa da fila de Olá, utilize vários recetores de toocreate de fábricas de mensagens.
* Utilize a vantagem de tootake operações assíncronas do lado do cliente de criação de batches.
* Definir Olá intervalo too50ms tooreduce Olá número as transmissões de protocolo de cliente do Service Bus de criação de batches. Se forem utilizados várias os remetentes, aumente Olá too100ms de intervalo de criação de batches.
* Deixe o acesso de arquivo de batches ativado. Isto aumenta Olá geral taxa a que as mensagens podem ser escritas na fila de Olá.
* Defina as horas de too20 de contagem de obtenção prévia Olá taxas de processamento máximo Olá de todos os recetores de uma fábrica. Isto reduz o número de Olá de transmissões de protocolo de cliente do Service Bus.

### <a name="multiple-high-throughput-queues"></a>Várias filas de débito elevado
Objetivo: Maximize o débito global de várias filas. débito de Olá de uma fila individuais é moderada ou elevada.

o débito máximo tooobtain distribuídos por várias filas, utilize as definições de Olá descritos débito de Olá toomaximize de uma fila única. Além disso, utilize fábricas diferentes toocreate clientes enviar ou recebem as filas diferentes.

### <a name="low-latency-queue"></a>Fila de latência baixa
Objetivo: Minimize a latência de ponto a ponto de uma fila ou tópico. número de Olá de remetentes e os recetores é pequeno. débito de Olá da fila de Olá é pequeno ou moderada.

* Utilize uma fila particionada para disponibilidade melhorada.
* Desative a criação de batches do lado do cliente. cliente de Olá imediatamente envia uma mensagem.
* Desative o acesso à loja de batches. serviço de Olá escreve imediatamente o arquivo de toohello Olá mensagens.
* Se utilizar um único cliente, defina Olá obtenção prévia contagem too20 vezes Olá taxa de processamento do recetor Olá. Se várias mensagens chegam a fila de Olá em Olá mesmo tempo, Olá o protocolo de cliente do Service Bus transmite-os, todos num Olá mesmo tempo. Quando o cliente de Olá recebe a mensagem seguinte Olá, essa mensagem já se encontra na cache local Olá. cache de Olá deve ser pequeno.
* Se utilizar vários clientes, defina too0 de contagem de obtenção prévia Olá. Ao fazê-lo, o cliente segundo Olá pode receber mensagem de saudação segundo enquanto cliente primeiro Olá ainda está a processar mensagem de saudação primeiro.

### <a name="queue-with-a-large-number-of-senders"></a>Fila com um grande número de remetentes de
Objetivo: Maximize o débito de uma fila ou um tópico com um grande número de remetentes. Cada remetente envia mensagens com uma velocidade de moderada. número de Olá de recetores é pequeno.

O Service Bus permite cópias de segurança too1000 ligações simultâneas tooa entidades de mensagens (ou 5000 através de AMQP). Este limite é aplicado ao nível do espaço de nomes de Olá, e tópicos/filas/subscrições são limitadas pelo limite Olá de ligações em simultâneo por espaço de nomes. Para as filas, este número é partilhado entre os remetentes e os recetores. Se a todas as ligações de 1000 são necessárias para os remetentes, deve substituir fila Olá com um tópico e uma única subscrição. Um tópico aceita segurança too1000 ligações simultâneas de remetentes, enquanto que a subscrição de Olá aceita um ligações simultâneas de 1000 adicionais de recetores. Se forem necessários mais de 1000 remetentes em simultâneo, os remetentes de Olá devem enviar mensagens toohello protocolo de Service Bus através de HTTP.

débito toomaximize, Olá a seguir:

* Utilize uma fila de mensagens particionada para um melhor desempenho e disponibilidade.
* Se o remetente de cada um reside num processo diferente, utilize apenas uma único fábrica por processo.
* Utilize a vantagem de tootake operações assíncronas do lado do cliente de criação de batches.
* Utilize predefinição de Olá criação de batches de intervalo de 20ms tooreduce Olá número as transmissões de protocolo de cliente do Service Bus.
* Deixe o acesso de arquivo de batches ativado. Isto aumenta Olá geral taxa a que as mensagens podem ser escritas na fila Olá ou um tópico.
* Defina as horas de too20 de contagem de obtenção prévia Olá taxas de processamento máximo Olá de todos os recetores de uma fábrica. Isto reduz o número de Olá de transmissões de protocolo de cliente do Service Bus.

### <a name="queue-with-a-large-number-of-receivers"></a>Fila com um grande número de recetores
Objetivo: Maximizar Olá receber a taxa de uma fila ou a subscrição com um grande número de recetores. Cada recetor recebe mensagens de uma taxa moderada. número de Olá de remetentes é pequeno.

O Service Bus permite cópias de segurança Entidade de tooan too1000 ligações em simultâneo. Se uma fila precisar de mais de 1000 recetores, deve substituir fila Olá com um tópico e várias subscrições. Cada subscrição pode suportar cópias de segurança too1000 de ligações em simultâneo. Em alternativa, recetores podem aceder a fila de Olá através de Olá protocolo HTTP.

débito toomaximize, Olá a seguir:

* Utilize uma fila de mensagens particionada para um melhor desempenho e disponibilidade.
* Se cada recetor reside num processo diferente, utilize apenas uma único fábrica por processo.
* Recetores podem utilizar operações síncronas ou assíncronas. Olá moderada fornecido receber taxa de um recetor individuais, do lado do cliente de lotes de um pedido de conclusão não afetam o débito do recetor.
* Deixe o acesso de arquivo de batches ativado. Esta reduz Olá carga geral da entidade de Olá. Também reduz Olá geral taxa a que as mensagens podem ser escritas na fila Olá ou um tópico.
* Defina o valor de tooa de contagem de obtenção prévia do Olá pequeno (por exemplo, PrefetchCount = 10). Isto impede que recetores inatividade enquanto outros recetores têm de grandes quantidades de mensagens colocadas em cache.

### <a name="topic-with-a-small-number-of-subscriptions"></a>Tópico com um pequeno número de subscrições
Objetivo: Maximize o débito de Olá de um tópico com um pequeno número de subscrições. Uma mensagem é recebida por várias subscrições, que significa Olá combinado receber taxa através de todas as subscrições é maior do que a velocidade de envio de Olá. número de Olá de remetentes é pequeno. número de Olá de recetores por subscrição é pequeno.

débito toomaximize, Olá a seguir:

* Utilize um tópico particionado para um melhor desempenho e disponibilidade.
* Olá tooincrease geral taxa de envio para o tópico Olá, utilize vários remetentes de toocreate de fábricas de mensagens. Para cada remetente, utilize operações assíncronas ou de vários threads.
* Olá tooincrease geral taxa de receção de uma subscrição, utilize vários recetores de toocreate de fábricas de mensagens. Para cada recetor, utilize operações assíncronas ou de vários threads.
* Utilize a vantagem de tootake operações assíncronas do lado do cliente de criação de batches.
* Utilize predefinição de Olá criação de batches de intervalo de 20ms tooreduce Olá número as transmissões de protocolo de cliente do Service Bus.
* Deixe o acesso de arquivo de batches ativado. Isto aumenta Olá geral taxa a que as mensagens podem ser escritas no tópico Olá.
* Defina as horas de too20 de contagem de obtenção prévia Olá taxas de processamento máximo Olá de todos os recetores de uma fábrica. Isto reduz o número de Olá de transmissões de protocolo de cliente do Service Bus.

### <a name="topic-with-a-large-number-of-subscriptions"></a>Tópico com um grande número de subscrições
Objetivo: Maximize o débito de Olá de um tópico com um grande número de subscrições. Uma mensagem é recebida por várias subscrições, que significa Olá combinado receber taxa através de todas as subscrições é muito maior do que a velocidade de envio de Olá. número de Olá de remetentes é pequeno. número de Olá de recetores por subscrição é pequeno.

Tópicos com um grande número de subscrições expõem normalmente um débito global baixo se todas as mensagens são encaminhadas tooall subscrições. Isto é provocado pelo facto de Olá que cada mensagem é recebida demasiadas vezes e todas as mensagens que estão contidas num tópico e todas as respetivas subscrições são armazenadas no Olá mesmo arquivo. Presume-se que são pequenos número de Olá de remetentes e número de recetores por subscrição. Service Bus suporta até too2, 000 subscrições por tópico.

débito toomaximize, Olá a seguir:

* Utilize um tópico particionado para um melhor desempenho e disponibilidade.
* Utilize a vantagem de tootake operações assíncronas do lado do cliente de criação de batches.
* Utilize predefinição de Olá criação de batches de intervalo de 20ms tooreduce Olá número as transmissões de protocolo de cliente do Service Bus.
* Deixe o acesso de arquivo de batches ativado. Isto aumenta Olá geral taxa a que as mensagens podem ser escritas no tópico Olá.
* Defina as Olá obtenção prévia contagem too20 horas Olá esperado receber taxa em segundos. Isto reduz o número de Olá de transmissões de protocolo de cliente do Service Bus.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre a otimizar o desempenho do Service Bus, consulte [entidades de mensagens Particionadas][Partitioned messaging entities].

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing
