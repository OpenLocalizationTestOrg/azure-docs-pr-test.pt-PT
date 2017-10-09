---
title: "aaaService barramento de serviço de mensagens assíncrono | Microsoft Docs"
description: "Descrição do serviço de mensagens assíncrono do Service Bus do Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>Padrões de mensagens assíncronas e elevada disponibilidade

Serviço de mensagens assíncrono pode ser implementado numa variedade de formas diferentes. Com as filas, tópicos e subscrições, o Service Bus do Azure suporta asynchronism através de uma loja e o mecanismo de reencaminhar. Na operação (síncrona) normal, pode enviar mensagens tooqueues e tópicos e recebe mensagens de filas e subscrições. As aplicações que escreve dependem estas entidades sempre que está a ser disponíveis. Quando muda de estado de funcionamento de entidade de Olá, devido a tooa diversas circunstâncias, precisa de uma forma tooprovide uma entidade de capacidade reduzida que pode satisfazer a maioria das necessidades.

As aplicações utilizam normalmente tooenable padrões mensagens um número de cenários de comunicação assíncrona. Pode criar aplicações no qual os clientes podem enviar mensagens tooservices, mesmo quando o serviço de Olá não está em execução. Para aplicações que experiência bursts das comunicações, uma fila pode ajudar a nível Olá carregar, fornecendo uma comunicações de toobuffer local. Por fim, pode obter uma carga simple, mas eficaz mensagens de toodistribute balanceador em várias máquinas.

Disponibilidade de toomaintain de ordem de qualquer uma destas entidades, considere um número de diferentes formas em que estas entidades podem aparecer indisponíveis para um sistema de mensagens durável. Um modo geral, vemos entidade Olá ficar indisponível tooapplications, que iremos escrever em Olá seguir formas diferentes:

* Não é possível toosend mensagens.
* Não é possível tooreceive mensagens.
* Não é possível toomanage entidades (criar, obter, atualizar ou eliminar entidades).
* Serviço de Olá toocontact não é possível.

Para cada uma destas falhas, modos diferentes falha existem que permitem um trabalho de tooperform toocontinue aplicação certo nível de capacidade reduzida. Por exemplo, um sistema que pode enviar mensagens, mas não recebê-las pode continuar a receber as ordens de clientes, mas não é possível processar as ordens. Este tópico aborda problemas potenciais que podem ocorrer, e como são atenuados desses problemas. Barramento de serviço foi introduzido um número de atenuações que tem a participar no, e este tópico descreve também Olá regras que rege Olá utilizam essas mitigações de optar ativamente por participar no.

## <a name="reliability-in-service-bus"></a>Fiabilidade no Service Bus
Existem várias formas toohandle problemas de mensagem e a entidade e existem diretrizes que rege a utilização adequada Olá esses mitigações. diretrizes de Olá toounderstand, tem de compreender primeiro o que pode efetuar no Service Bus. Devido a estrutura de toohello de sistemas do Azure, todos estes problemas tendem toobe curta duração. Um nível elevado, causas diferentes Olá indisponibilidade aparecem da seguinte forma:

* Limitação de um sistema externo em que depende do Service Bus. Limitação ocorre de interações com os recursos de armazenamento e computação.
* Problema de um sistema de que depende de Service Bus. Por exemplo, uma determinada parte de armazenamento pode encontrar problemas.
* Falha do Service Bus no subsistema único. Nesta situação, um nó de computação pode obter num estado inconsistente e tem de reiniciar o próprio, fazendo com que todas as entidades serve saldo tooload tooother nós. Isto por sua vez, pode causar um curto período de tempo de processamento de mensagens lenta.
* Falha do Service Bus dentro de um datacenter do Azure. Esta é uma "Falha catastrófica" durante os quais sistema Olá está inacessível para o número de minutos ou algumas horas.

> [!NOTE]
> termo do Olá **armazenamento** pode significar Storage do Azure e SQL Azure.
> 
> 

Barramento de serviço contém um número de mitigações para estes problemas. Olá secções a seguir aborda e os respetivas mitigações de cada problema.

### <a name="throttling"></a>Limitação
Com o Service Bus, a limitação permite a gestão de taxa de mensagem cooperative. Cada nó de barramento de serviço individual aloja várias entidades. Cada uma dessas entidades estabelece exigências no sistema de Olá em termos de CPU, memória, armazenamento e outros aspetos. Quando qualquer uma destas facetas Deteta utilização que exceder os limiares definidos, Service Bus pode negar um pedido específico. autor da chamada Olá recebe um [ServerBusyException] [ ServerBusyException] e repete após 10 segundos.

Como uma mitigação código Olá tem de ler erro Olá e pare quaisquer tentativas de mensagem de saudação para, pelo menos, 10 segundos. Uma vez que o erro de Olá pode acontecer em partes da aplicação de cliente Olá, espera-se que cada peça executa independentemente a lógica de repetição de Olá. código de Olá pode reduzir a probabilidade de Olá de limitação, permitindo a criação de partições num fila ou tópico.

### <a name="issue-for-an-azure-dependency"></a>Problema de uma dependência do Azure
Outros componentes no Azure, ocasionalmente, podem ter problemas de serviço. Por exemplo, quando está a ser atualizado um sistema que utiliza o Service Bus, esse sistema temporariamente pode experimentar capacidades reduzidas. toowork à volta destes tipos de problemas, o Service Bus regularmente investiga e implementa mitigações. Só aparecem efeitos secundários destas mitigações. Por exemplo, toohandle transitório problemas com o armazenamento, o Service Bus implementa um sistema que permite toowork de operações de envio de mensagem de forma consistente. Devido a natureza toohello mitigação de Olá, uma mensagem enviada pode demorar até too15 minutos tooappear na fila de Olá afetado ou na subscrição e estar pronto para uma operação de receção. Um modo geral, a maior parte das entidades não irá ocorrer este problema. No entanto, tendo em conta o número de Olá de entidades no Service Bus no Azure, este mitigação, por vezes, é necessário para um pequeno subconjunto de clientes do Service Bus.

### <a name="service-bus-failure-on-a-single-subsystem"></a>Falha de barramento de serviço de subsistema de um único
Com qualquer aplicação, circunstâncias podem fazer com que um componente interno do Service Bus toobecome inconsistente. Quando o Service Bus Deteta isto, recolhe dados de aplicação de Olá tooaid diagnosticar o que aconteceu. Depois de Olá os dados são recolhidos, a aplicação Olá é reiniciado no tooreturn tentativa-tooa consistente. Este processo ocorre razoavelmente depressa e resultados numa entidade apresentação toobe disponível para a cópia de segurança tooa alguns minutos, embora típico para baixo vezes são muito mais curtos.

Nestes casos, aplicações de cliente Olá gera um [System.TimeoutException] [ System.TimeoutException] ou [MessagingException] [ MessagingException] exceção. Barramento de serviço contém uma mitigação para este problema no formulário de Olá de lógica de repetição de clientes automatizada. Depois de se esgota período Olá e não for entregue a mensagem de saudação, pode explorar utilizar outras funcionalidades, tais como [emparelhado espaços de nomes][paired namespaces]. Espaços de nomes emparelhados têm outras limitações que são debatidas esse artigo.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Falha do Service Bus dentro de um datacenter do Azure
Olá motivo mais provável uma falha num datacenter do Azure é uma implementação de atualização falhada do Service Bus ou um sistema dependente. Dado que a plataforma de Olá amadureceu, tem o seu probabilidade Olá deste tipo de falha. Também pode ocorrer uma falha de centro de dados por motivos que incluem Olá seguinte:

* Falha de elétrica (fonte de alimentação e energia gerar desaparecer).
* Conectividade (quebra de internet entre os clientes e o Azure).

Em ambos os casos, um desastre natural ou man-made causou o problema de Olá. toowork contornar esta situação e certifique-se de que podem ainda enviar mensagens, pode utilizar [emparelhado espaços de nomes] [ paired namespaces] tooenable mensagens toobe enviado tooa segunda localização enquanto localização primária Olá é efetuada em bom estado novamente. Para obter mais informações, consulte [melhores práticas para insulating aplicações contra falhas de Service Bus e perante desastres][Best practices for insulating applications against Service Bus outages and disasters].

## <a name="paired-namespaces"></a>Espaços de nomes emparelhados
Olá [emparelhado espaços de nomes] [ paired namespaces] funcionalidade suporta cenários em que uma entidade de barramento de serviço ou a implementação no Centro de dados fica indisponível. Enquanto este evento ocorre com pouca frequência, sistemas distribuídos ainda devem estar preparados toohandle pior cenários de caso. Normalmente, este evento ocorre porque algumas elemento de que depende de barramento de serviço estão a ocorrer um problema de curta duração. disponibilidade da aplicação toomaintain durante uma falha, os utilizadores do Service Bus podem utilizar o dois separados espaços de nomes, de preferência nos centros de dados separada, toohost as entidades de mensagens. resto Olá esta secção utiliza Olá seguinte terminologia:

* Espaço de nomes primário: Olá espaço de nomes com o qual a aplicação interage, para enviar e receber operações.
* Espaço de nomes secundário: Olá espaço de nomes que age como um espaço de nomes de principal de toohello cópia de segurança. Lógica da aplicação não interage com este espaço de nomes.
* Intervalo de ativação pós-falha: quantidade de Olá de falhas normais de tooaccept tempo antes de aplicação Olá muda de Olá espaço de nomes primário toohello secundário espaço de nomes.

Suporte de espaços de nomes de emparelhar *enviar disponibilidade*. Envie mensagens hello do toosend capacidade de preserva de disponibilidade. disponibilidade de envio de toouse, a aplicação tem de cumprir Olá os requisitos:

1. Apenas são recebidas mensagens do espaço de nomes de principal Olá.
2. Tooa de mensagens enviadas fornecido a fila ou um tópico pode chegarem fora de ordem.
3. Poderão chegam fora de ordem mensagens dentro de uma sessão. Esta é uma quebra da funcionalidade normal das sessões. Isto significa que a aplicação utiliza mensagens de grupo de toologically sessões.
4. Estado da sessão só é mantido no espaço de nomes de principal Olá.
5. fila primário Olá pode ficar online e iniciar a aceitação das mensagens antes de fila secundária Olá fornece todas as mensagens na fila primário Olá.

Olá secções a seguir aborda Olá APIs, como são implementadas Olá APIs e código de exemplo mostra que utiliza a funcionalidade de Olá. Tenha em atenção que existem implicações de faturação associadas a esta funcionalidade.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>Olá MessagingFactory.PairNamespaceAsync API
funcionalidade de espaços de nomes emparelhado Olá inclui Olá [PairNamespaceAsync] [ PairNamespaceAsync] método no Olá [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] classe:

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Quando Olá tarefa estiver concluída, o emparelhamento do espaço de nomes Olá, também é completa e pronto tooact após para qualquer [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], ou [TopicClient] [ TopicClient] criados com Olá [MessagingFactory] [ MessagingFactory] instância. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] é classe base do Olá para Olá diferentes tipos de emparelhamento que estão disponíveis com um [MessagingFactory] [ MessagingFactory] objeto. Atualmente, Olá só classe derivada é um nome [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], que implementa os requisitos de disponibilidade de envio de Olá. [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] tem um conjunto de construtores que criar entre si. Consultar o construtor de Olá com Olá maioria dos parâmetros, pode compreender Olá comportamento dos Olá outros construtores.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

Estes parâmetros tem Olá significados os seguintes:

* *secondaryNamespaceManager*: um inicializado [NamespaceManager] [ NamespaceManager] instância para o espaço de nomes secundário Olá esse Olá [PairNamespaceAsync] [ PairNamespaceAsync] método pode utilizar tooset segurança secundário Olá de espaço de nomes. Gestor de espaço de nomes de Olá-se tooobtain utilizados Olá lista de filas no espaço de nomes de Olá e toomake se de que as filas de registo de segurança de Olá necessário existem. Se não existirem as filas, são criados. [NamespaceManager] [ NamespaceManager] requer Olá capacidade toocreate um token com Olá **gerir** de afirmação.
* *messagingFactory*: Olá [MessagingFactory] [ MessagingFactory] instância para secundário Olá de espaço de nomes. Olá [MessagingFactory] [ MessagingFactory] objeto é utilizado toosend e, se hello [EnableSyphon] [ EnableSyphon] for definida demasiado**verdadeiro** , receber mensagens de filas de registo de segurança de Olá.
* *backlogQueueCount*: número de Olá de registo de segurança de filas toocreate. Este valor tem de ser no mínimo 1. Ao enviar o registo de segurança de mensagens toohello, uma destas filas é escolhida aleatoriamente. Se definir Olá valor too1, em seguida, apenas uma fila pode alguma vez ser utilizada. Quando isto acontece e fila de um registo de segurança de Olá gera erros, o cliente Olá não é possível tootry uma fila de registo de segurança diferentes e pode falhar toosend da mensagem. Recomendamos que a definição deste valor toosome maior valor e predefinido Olá valor too10. Pode alterar este tooa superior ou um valor inferior, dependendo da quantidade de dados que a aplicação envia por dia. Cada fila de registo de segurança pode manter cópias de segurança too5 GB de mensagens em fila.
* *failoverInterval*: Olá período de tempo durante os quais irá aceitar falhas no espaço de nomes de principal Olá antes de mudar qualquer entidade única através de espaço de nomes secundário toohello. As ativações pós-falha ocorrerem numa entidade pela entidade base. As entidades de um único espaço de nomes com frequência em direto em nós diferentes no Service Bus. Uma falha de uma entidade não implica uma falha no outro. Pode definir este valor demasiado[System.TimeSpan.Zero] [ System.TimeSpan.Zero] toofailover toohello secundário imediatamente após a falha da primeira, não transitório. Falhas de acionam de temporizador de ativação pós-falha de Olá são qualquer [MessagingException] [ MessagingException] no qual Olá [IsTransient] [ IsTransient] propriedade é false, ou um [System.TimeoutException][System.TimeoutException]. Outras exceções, tal como [UnauthorizedAccessException] [ UnauthorizedAccessException] não fazer com que a ativação pós-falha, porque indicam que o cliente Olá está configurado incorretamente. A [ServerBusyException] [ ServerBusyException] não causa ativação pós-falha porque padrão correto Olá toowait 10 segundos, em seguida, enviar mensagem de saudação novamente.
* *enableSyphon*: indica que este emparelhamento específica deve também syphon mensagens do Olá espaço de nomes secundário back toohello primário espaço de nomes. Em geral, as aplicações que enviam mensagens devem definir este valor demasiado**falso**; as aplicações que receber mensagens devem definir este valor demasiado**verdadeiro**. motivo Olá para isto é que frequentemente, existem menos recetores de mensagem que os remetentes de mensagens. Dependendo do número de Olá de recetores, pode escolher toohave uma única aplicação instância identificador Olá syphon deveres relativos. Utilizar vários recetores tem implicações de faturação para cada fila de registo de segurança.

toouse Olá código, crie um site primário [MessagingFactory] [ MessagingFactory] instância de uma secundária [MessagingFactory] [ MessagingFactory] instância de uma secundária [NamespaceManager] [ NamespaceManager] instância e um [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] instância. chamada de Olá pode ser tão simple como seguinte Olá:

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Olá quando a tarefa devolvida pelo Olá [PairNamespaceAsync] [ PairNamespaceAsync] método estiver concluída, tudo está configurado e pronto toouse. Antes da devolução da tarefa de Olá, poderá não concluiu todos os Olá em segundo plano trabalho necessário para Olá emparelhamento toowork direito. Como resultado, não deve começar a enviar mensagens, até que a tarefa de Olá devolve. Se tiver ocorreram quaisquer falhas, tais como credenciais incorretas, ou em filas de registo de segurança do falha toocreate Olá, essas exceções serão emitidas uma vez concluída a tarefa de Olá. Depois de o devolve a tarefa de Olá, certifique-se de que filas Olá foram localizadas ou criadas, examinando Olá [BacklogQueueCount] [ BacklogQueueCount] propriedade no seu [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] instância. Para Olá precedente código, essa operação aparece da seguinte forma:

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá de mensagens assíncronas no Service Bus, leia mais detalhes sobre [emparelhado espaços de nomes][paired namespaces].

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
