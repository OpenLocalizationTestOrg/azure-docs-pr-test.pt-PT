---
title: "aaaOverview Olá ciclo de vida dos Reliable Services do Azure Service Fabric | Microsoft Docs"
description: "Saiba mais sobre eventos de ciclo de vida de diferentes Olá nos serviços de fiáveis de Service Fabric"
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Descrição geral do ciclo de vida de serviços fiável
> [!div class="op_single_selector"]
> * [C# no Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java em Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Quando pensar sobre Olá ciclos de vida dos Reliable Services, Olá Noções básicas do ciclo de vida de Olá são Olá mais importante. Em geral:

- Durante o arranque
  - Os serviços são construídos
  - Têm um tooconstruct oportunidade e devolver zero ou mais serviços de escuta
  - Os serviços de escuta devolvidos estão abertos, permitir a comunicação com o serviço de Olá
  - runasync com do serviço de Olá se chama o método, permitindo Olá serviço toodo execução longa ou em segundo plano de trabalho
- Durante o encerramento
  - Olá cancelamento token transmitido tooRunAsync foi cancelada e os serviços de escuta de Olá estão fechados
  - Assim que estiver concluído, é de objeto de serviço Olá próprio destructed

Existem detalhes em torno Olá exato de ordenação destes eventos. Em particular, ordem de Olá de eventos podem ser alteradas ligeiramente dependendo se o serviço fiável de Olá é Stateless ou de monitorização de estado. Além disso, para os serviços com monitorização de estado, temos toodeal com cenário de comutação primário Olá. Durante esta sequência e função Olá de principal é tooanother transferidos réplica (ou volta) sem serviço Olá encerrar. Por fim, temos toothink sobre as condições de erro ou falha.

## <a name="stateless-service-startup"></a>Arranque do serviço sem monitorização de estado
Olá ciclo de vida de um serviço sem monitorização de estado é bastante simples. Segue-se a ordem de Olá de eventos:

1. Olá serviço é construído
2. Em seguida, em paralelas duas coisas ocorrer:
    - `StatelessService.CreateServiceInstanceListeners()`é invocada e quaisquer serviços de escuta devolvidos estão abertos. `ICommunicationListener.OpenAsync()`é chamado para cada serviço de escuta
    - Olá do serviço `StatelessService.RunAsync()` método é denominado
3. Se estiver presente, hello do serviço `StatelessService.OnOpenAsync()` método é chamado. Esta é uma substituição invulgar, mas está disponível.

É importante toonote que não há nenhum ordenação entre Olá chamadas toocreate e os serviços de escuta de Olá aberta e runasync com. Serviços de escuta de Olá poderão abrir antes runasync com é iniciado. Da mesma forma, runasync com poderá acabar invocado antes de serviços de escuta de comunicação de Olá abertos ou mesmo foi construídos. Se for necessária qualquer sincronização, será deixada como um implementador de toohello exercício. Soluções comuns:

  - Por vezes, os serviços de escuta não podem funcionar até que outras informações é criado ou trabalho efectuadas. Para os serviços sem monitorização de estado de trabalho pode normalmente ser feito noutras localizações, tais como: 
    - no construtor do serviço de Olá
    - durante a Olá `CreateServiceInstanceListeners()` chamar
    - como parte de construção de Olá do serviço de escuta de Olá próprio
  - Por vezes, hello código runasync com pretende toostart até que os serviços de escuta de Olá estão abertos. Neste caso coordenação adicional é necessária. Uma solução comum é algumas sinalizador dentro de serviços de escuta de Olá que indicam quando estes estiverem concluídas. Este sinalizador, em seguida, é verificado em runasync com antes de continuar o trabalho tooactual.

## <a name="stateless-service-shutdown"></a>Encerramento do serviço sem monitorização de estado
Quando encerrar um serviço sem monitorização de estado, hello mesmo padrão é seguido, apenas na inversa:

1. Em paralelo
    - Quaisquer serviços de escuta abertos são fechados. `ICommunicationListener.CloseAsync()`é chamado para cada serviço de escuta.
    - token de cancelamento Olá passou demasiado`RunAsync()` foi cancelada. Do token de verificação Olá cancelamento `IsCancellationRequested` propriedade devolve true e se a chamada do token de Olá `ThrowIfCancellationRequested` método gera um `OperationCanceledException`.
2. Uma vez `CloseAsync()` conclusão em cada serviço de escuta e `RunAsync()` também estiver concluída, do serviço de Olá `StatelessService.OnCloseAsync()` se chama o método, se estiver presente. É toooverride invulgar `StatelessService.OnCloseAsync()`.
3. Depois de `StatelessService.OnCloseAsync()` estiver concluída, o objeto de serviço Olá é destructed

## <a name="stateful-service-startup"></a>Arranque de serviço com estado
Os serviços com monitorização de estado têm um serviços toostateless padrão semelhante, com algumas alterações. Quando a partir de um serviço com monitorização de estado, ordem de Olá de eventos é o seguinte:

1. Olá serviço é construído
2. `StatefulServiceBase.OnOpenAsync()`é chamado. Isto é uncommonly substituí-lo no serviço de Olá.
3. Olá seguintes ações ocorrem em paralelo
    - `StatefulServiceBase.CreateServiceReplicaListeners()`é invocado 
      - Se o serviço de Olá for um site primário todos os serviços de escuta devolvidos estão abertos. `ICommunicationListener.OpenAsync()`é chamado para cada serviço de escuta.
      - Se o serviço de Olá uma secundária, só esses serviços de escuta marcada como `ListenOnSecondary = true` estão abertas. É menos comum ter os serviços de escuta que são abertos em bases de dados secundárias.
    - Olá se Olá serviço atualmente é um serviço Olá primário, `StatefulServiceBase.RunAsync()` método é denominado
4. Depois de todos os hello do serviço de escuta de réplica `OpenAsync()` chamadas concluir e `RunAsync()` denomina-se, `StatefulServiceBase.OnChangeRoleAsync()` é chamado. Isto é uncommonly substituí-lo no serviço de Olá.

Da mesma forma toostateless serviços, não existe nenhum coordenação entre ordem Olá no qual Olá são criados e abrir os serviços de escuta e quando runasync com é chamado. Se precisar de coordenação, soluções Olá são muito Olá mesmo. Há um cenário adicional: dizer que as chamadas de Olá a chegar ao serviços de escuta de comunicação de Olá necessitam de informações mantidas dentro de alguns [coleções fiável](service-fabric-reliable-services-reliable-collections.md). Porque os serviços de escuta de comunicação de Olá foi aberta antes de coleções fiável Olá são legíveis ou gravável e antes de runasync com conseguiu iniciar, algumas adicional coordenação é necessária. solução mais simples e mais comuns de Olá destina-se tooreturn de serviços de escuta de comunicação de Olá algum código de erro hello do cliente utiliza tooknow tooretry Olá pedido.

## <a name="stateful-service-shutdown"></a>Encerramento de serviço com estado
Da mesma forma tooStateless serviços, eventos de ciclo de vida de Olá durante o encerramento são Olá mesmo como durante o arranque, mas invertido. Quando um serviço com monitorização de estado está a ser encerrado, hello eventos seguintes ocorrem:

1. Em paralelo
    - Quaisquer serviços de escuta abertos são fechados. `ICommunicationListener.CloseAsync()`é chamado para cada serviço de escuta.
    - token de cancelamento Olá passou demasiado`RunAsync()` foi cancelada. Do token de verificação Olá cancelamento `IsCancellationRequested` propriedade devolve true e se a chamada do token de Olá `ThrowIfCancellationRequested` método gera um `OperationCanceledException`.
2. Uma vez `CloseAsync()` conclusão em cada serviço de escuta e `RunAsync()` também estiver concluída, do serviço de Olá `StatefulServiceBase.OnChangeRoleAsync()` é chamado. (Isto é uncommonly substituído no serviço de Olá.)
    - A aguardar runasync com toocomplete é apenas necessário se esta réplica de serviço foi um site primário.
3. Uma vez Olá `StatefulServiceBase.OnChangeRoleAsync()` método estiver concluída, hello `StatefulServiceBase.OnCloseAsync()` método é chamado. Esta é uma substituição invulgar, mas está disponível.
3. Depois de `StatefulServiceBase.OnCloseAsync()` estiver concluída, o objeto de serviço Olá é destructed.

## <a name="stateful-service-primary-swaps"></a>Trocas de principal de serviço com estado
Enquanto um serviço com estado estiver em execução, só hello réplicas primárias que serviços com monitorização de estado de tem os respetivos serviços de escuta de comunicação abertos e o respetivo método runasync com chamado. Secundário são construídos mas Consulte não chamadas adicionais. Enquanto um serviço com estado estiver em execução no entanto, a qual a réplica está atualmente Olá principal pode alterar. O que significa em termos de eventos de ciclo de vida de Olá que pode ver uma réplica? Olá comportamento Olá réplica com monitorização de estado vê depende é réplica Olá que está a ser despromovida ou promovida durante a troca de Olá.

### <a name="for-hello-primary-being-demoted"></a>Para Olá primário que está a ser despromovido
Service Fabric tem toostop esta réplica processamento de mensagens e sair de qualquer trabalho em segundo plano que esteja a executar. Como resultado, este passo procura semelhante toowhen Olá serviço está a ser encerrado. Uma diferença é que Olá serviço não se encontra destructed ou fechado, uma vez que continua a ser como uma secundária. é denominado Olá APIs os seguintes:

1. Em paralelo
    - Quaisquer serviços de escuta abertos são fechados. `ICommunicationListener.CloseAsync()`é chamado para cada serviço de escuta.
    - token de cancelamento Olá passou demasiado`RunAsync()` foi cancelada. Do token de verificação Olá cancelamento `IsCancellationRequested` propriedade devolve true e se a chamada do token de Olá `ThrowIfCancellationRequested` método gera um `OperationCanceledException`.
2. Uma vez `CloseAsync()` conclusão em cada serviço de escuta e `RunAsync()` também estiver concluída, do serviço de Olá `StatefulServiceBase.OnChangeRoleAsync()` é chamado. Isto é uncommonly substituí-lo no serviço de Olá.

### <a name="for-hello-secondary-being-promoted"></a>A ser promovido para Olá secundário
Da mesma forma, o Service Fabric tem toostart esta réplica escutar mensagens na transmissão de Olá e iniciar quaisquer tarefas em segundo plano que cares sobre. Como resultado, parece este processo é criado o serviço de Olá toowhen semelhante, exceto essa réplica Olá próprio já existe. é denominado Olá APIs os seguintes:

1. Em paralelo
    - `StatefulServiceBase.CreateServiceReplicaListeners()`é invocada e quaisquer serviços de escuta devolvidos estão abertos. `ICommunicationListener.OpenAsync()`é chamado para cada serviço de escuta.
    - Olá do serviço `StatefulServiceBase.RunAsync()` método é denominado
2. Depois de todos os hello do serviço de escuta de réplica `OpenAsync()` chamadas concluir e `RunAsync()` ter sido chamado `StatefulServiceBase.OnChangeRoleAsync()` é chamado. Isto é uncommonly substituí-lo no serviço de Olá.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>Problemas comuns durante o encerramento do serviço com monitorização de estado e despromoção primária
Alterações do Service Fabric Olá principal de um serviço com monitorização de estado para diversos motivos. Hello mais comuns são [cluster reequilíbrio](service-fabric-cluster-resource-manager-balancing.md) e [atualização da aplicação](service-fabric-application-upgrade.md). Durante estas operações (bem como durante o encerramento do serviço normal, como o que poderá ver se o serviço de Olá foi eliminado), é importante que Olá de relativamente do serviço de Olá `CancellationToken`. Serviços que não processar corretamente o cancelamento irão ocorrer vários problemas. Em particular, estas operações serão lentas, uma vez que o Service Fabric aguarda Olá serviços toostop corretamente. Esta situação pode, em última análise levar toofailed atualizações que o limite de tempo e reverter. Token de cancelamento do falha toohonor Olá pode também fazer com que os clusters imbalanced porque nós obter frequente mas não podem ser reequilibrados serviços Olá, uma vez que demora demasiado tempo toomove-los noutro local. 

Uma vez que os serviços de Olá com monitorização de estado, também é provável que estão a utilizar Olá [coleções fiável](service-fabric-reliable-services-reliable-collections.md). No Service Fabric, quando um site primário é despromovido, um dos primeiros aspetos de Olá que ocorre é que o estado do acesso de escrita toohello subjacente foi revogado. Esta situação origina tooa segundo conjunto de problemas que podem afetar o ciclo de vida do Olá serviço. coleções de Olá exceções retorno baseadas em temporização Olá e se está a ser movida réplica Olá ou encerramento. Estas exceções devem ser processadas corretamente. Exceções acionadas por Service Fabric enquadram permanente [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) e transitório [(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet) categorias. Permanentes exceções devem ser registadas e emitidas, enquanto exceções transitório Olá podem ser repetidas com base em algumas lógica de repetição.

Processamento de exceções de Olá que vêm da utilização de Olá `ReliableCollections` em conjunto com eventos de ciclo de vida do serviço é uma parte importante de teste e a validar um serviço fiável. Olá recomendação é sempre o serviço de carga toorun ao efetuar atualizações e [chaos testar](service-fabric-controlled-chaos.md) antes de implementar alguma vez tooproduction. Os passos básicos ajudam a garantir que o seu serviço é corretamente implementado e processa eventos de ciclo de vida corretamente.


## <a name="notes-on-service-lifecycle"></a>Notas sobre o ciclo de vida do serviço
  - Ambos os Olá `RunAsync()` método e Olá `CreateServiceReplicaListeners/CreateServiceInstanceListeners` chamadas são opcionais. Um serviço pode ter um dos mesmos, ambos ou nenhum. Por exemplo, se o serviço de Olá todos os respetivo trabalho em resposta toouser chamadas, não é necessário para o mesmo tooimplement `RunAsync()`. Apenas Olá comunicação os serviços de escuta e o respetivo código associado são necessárias. Da mesma forma, criar devolver os serviços de escuta de comunicação é opcional, como serviço Olá pode ter apenas em segundo plano toodo de trabalho e, por isso, só deverá tooimplement`RunAsync()`
  - É válido para um serviço toocomplete `RunAsync()` com êxito e retorno do mesmo. A conclusão não é uma condição de falha. A concluir `RunAsync()` indica que o trabalho em segundo plano de Olá do serviço de Olá foi concluída. Para os serviços fiáveis com monitorização de estado, `RunAsync()` denomina-se novamente se a réplica Olá foram despromovida de tooSecondary primário e, em seguida, promovido tooPrimary anterior.
  - Se um serviço sai do `RunAsync()` por argumentoutofrangeexception algumas exceção inesperada, isto constitui uma falha. objeto de serviço Olá é encerrado e reportado um erro de estado de funcionamento.
  - Enquanto não estiver não existe nenhum limite de tempo na devolução destes métodos, perder imediatamente Olá capacidade toowrite tooReliable coleções e, por conseguinte, não é possível concluir qualquer trabalho real. Recomenda-se que poderá devolve mais rapidamente possível após a receção de pedido de cancelamento Olá. Se o serviço não responder toothese API chamadas dentro de um período de tempo de que Service Fabric pode forçar a razoável termine o serviço. Normalmente, isto só ocorre durante as atualizações de aplicações ou quando um serviço está a ser eliminado. Este tempo limite é de 15 minutos por predefinição.
  - Falhas na Olá `OnCloseAsync()` resultado de caminho no `OnAbort()` chamados que é uma oportunidade de melhor esforço de última oportunidade para Olá tooclean de serviço cópia de segurança e quaisquer recursos que possam tem reclamado de versão.

## <a name="next-steps"></a>Passos seguintes
- [Introdução tooReliable serviços](service-fabric-reliable-services-introduction.md)
- [Início rápido de serviços fiável](service-fabric-reliable-services-quick-start.md)
- [Reliable Services avançadas de utilização](service-fabric-reliable-services-advanced-usage.md)
