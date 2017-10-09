---
title: "aaaActors diagnóstico e monitorização | Microsoft Docs"
description: "Este artigo descreve os diagnósticos de Olá e funcionalidades no runtime do Service Fabric Reliable Actors Olá, incluindo eventos de Olá e contadores de desempenho emitidos por este de monitorização de desempenho."
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Diagnóstico e monitorização do desempenho dos Reliable Actors
tempo de execução do Olá Reliable Actors emite [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) eventos e [contadores de desempenho](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Estes fornecem informações para o funcionamento do tempo de execução Olá e ajudam a resolver problemas e monitorização do desempenho.

## <a name="eventsource-events"></a>Eventos de EventSource
nome do fornecedor de EventSource Olá para Olá Reliable Actors runtime é "Microsoft-ServiceFabric-Atores". Eventos a partir desta origem de evento são apresentados em Olá [eventos de diagnóstico](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) janela quando a aplicação de ator Olá está a ser [debugged no Visual Studio](service-fabric-debugging-your-application.md).

São exemplos de ferramentas e tecnologias que ajudam na recolha de e/ou a visualização de eventos de EventSource [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [diagnósticos do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md), [registo semântica](https://msdn.microsoft.com/library/dn774980.aspx)e Olá [ Biblioteca do Microsoft TraceEvent](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

### <a name="keywords"></a>Palavras-chave
Todos os eventos que pertencem toohello Reliable Actors EventSource estão associados com uma ou mais palavras-chave. Isto permite a filtragem de eventos que são recolhidos. Olá seguir bits de palavra-chave é definida.

| bits | Descrição |
| --- | --- |
| 0x1 |Conjunto de eventos importantes que resumem operação Olá do tempo de execução do Olá Atores de recursos de infraestrutura. |
| 0x2 |Conjunto de eventos que descrevem chamadas de método de ator. Para obter mais informações, consulte Olá [tópico introdutórias sobre atores](service-fabric-reliable-actors-introduction.md). |
| 0x4 |Conjunto de eventos relacionados tooactor estado. Para obter mais informações, consulte o tópico de Olá no [gestão do Estado de ator](service-fabric-reliable-actors-state-management.md). |
| 0x8 |Conjunto de eventos relacionados com base em tooturn simultaneidade no ator Olá. Para obter mais informações, consulte o tópico de Olá no [simultaneidade](service-fabric-reliable-actors-introduction.md#concurrency). |

## <a name="performance-counters"></a>Contadores de desempenho
tempo de execução do Olá Reliable Actors define Olá seguintes categorias de contador de desempenho.

| Categoria | Descrição |
| --- | --- |
| Ator do Service Fabric |Contadores de atores do Service Fabric tooAzure específicos, por exemplo, tempo decorrido o estado do ator toosave |
| Método de Ator do Service Fabric |Contadores específicos toomethods implementado por atores do Service Fabric, por exemplo, com que frequência um método de atores é invocado |

Cada um dos Olá acima categorias tem um ou mais contadores.

Olá [Monitor de desempenho do Windows](https://technet.microsoft.com/library/cc749249.aspx) aplicação que está disponível por predefinição no sistema de operativo do Windows hello pode ser utilizados dados de contador de desempenho de toocollect e vista. [Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) é outra opção para recolher dados de contador de desempenho e carregá-lo tooAzure tabelas.

### <a name="performance-counter-instance-names"></a>Nomes de instâncias do contador de desempenho
Um cluster com um grande número de serviços de atores ou partições de serviço de atores terão um grande número de instâncias de contador de desempenho de atores. Olá os nomes de instâncias do contador de desempenho podem ajudar a identificar Olá específicos [partição](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) e método de ator (se aplicável) essa instância de contador de desempenho de Olá está associada.

#### <a name="service-fabric-actor-category"></a>Categoria de Atores do Service Fabric
Para a categoria de Olá `Service Fabric Actor`, os nomes de instâncias do contador Olá estão em Olá seguinte formato:

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* é Olá representação de cadeia de Olá ID de partição de Service Fabric Olá instância do contador de desempenho está associado. ID de partição Olá é um GUID e respetiva representação de cadeia que é gerada através de Olá [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método com o especificador de formato "D".

*ActorRuntimeInternalID* é Olá representação de um número inteiro de 64 bits que é gerado pelo tempo de execução do Olá Atores de recursos de infraestrutura para a sua utilização interna. Isto está incluído na instância do contador de desempenho de Olá nome tooensure a exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os utilizadores não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de Olá.

Olá segue-se um exemplo de um nome de instância do contador para um contador que pertence toohello `Service Fabric Actor` categoria:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

No exemplo de Olá acima, `2740af29-78aa-44bc-a20b-7e60fb783264` é Olá representação de cadeia de ID de partição de Service Fabric Olá, e `635650083799324046` é utilizar Olá ID de 64 bits que é gerado para o tempo de execução Olá 's interno.

#### <a name="service-fabric-actor-method-category"></a>Categoria de método de Ator do Service Fabric
Para a categoria de Olá `Service Fabric Actor Method`, os nomes de instâncias do contador Olá estão em Olá seguinte formato:

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*MethodName* é o nome de Olá do método de ator Olá que Olá instância do contador de desempenho está associado. formato de Olá do nome do método Olá é determinado com base em algumas lógica no tempo de execução do Olá Atores de recursos de infraestrutura que equilibra a legibilidade Olá do nome de Olá com restrições de comprimento de máximo de Olá dos nomes de instância de contador de desempenho de Olá no Windows.

*ActorsRuntimeMethodId* é Olá representação de um número inteiro de 32 bits que é gerado pelo tempo de execução do Olá Atores de recursos de infraestrutura para a sua utilização interna. Isto está incluído na instância do contador de desempenho de Olá nome tooensure a exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os utilizadores não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de Olá.

*ServiceFabricPartitionID* é Olá representação de cadeia de Olá ID de partição de Service Fabric Olá instância do contador de desempenho está associado. ID de partição Olá é um GUID e respetiva representação de cadeia que é gerada através de Olá [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método com o especificador de formato "D".

*ActorRuntimeInternalID* é Olá representação de um número inteiro de 64 bits que é gerado pelo tempo de execução do Olá Atores de recursos de infraestrutura para a sua utilização interna. Isto está incluído na instância do contador de desempenho de Olá nome tooensure a exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os utilizadores não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de Olá.

Olá segue-se um exemplo de um nome de instância do contador para um contador que pertence toohello `Service Fabric Actor Method` categoria:

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

No exemplo de Olá acima, `ivoicemailboxactor.leavemessageasync` é o nome do método Olá, `2` é Olá utilizar ID de 32 bits gerado para o tempo de execução Olá 's interno, `89383d32-e57e-4a9b-a6ad-57c6792aa521` é Olá representação de cadeia de ID de partição de Service Fabric Olá, e `635650083804480486` Olá ID de 64 bits gerado para utilização interna do tempo de execução de Olá.

## <a name="list-of-events-and-performance-counters"></a>Lista de eventos e contadores de desempenho
### <a name="actor-method-events-and-performance-counters"></a>Eventos de método de ator e contadores de desempenho
Olá Reliable Actors runtime emite Olá seguintes eventos relacionados com demasiado[métodos de ator](service-fabric-reliable-actors-introduction.md).

| Nome do evento | ID de evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |Verboso |0x2 |Tempo de execução de atores é sobre tooinvoke um método de ator. |
| ActorMethodStop |8 |Verboso |0x2 |Um método de ator terminou a execução. Ou seja, o método de ator do tempo de execução de Olá chamada assíncrona toohello devolveu e tarefa Olá devolvida pelo método de ator Olá tiver sido concluída. |
| ActorMethodThrewException |9 |Aviso |0x3 |Foi emitida uma exceção durante a execução de Olá de um método de ator, durante o método de ator do tempo de execução de Olá chamada assíncrona toohello ou durante a execução de Olá da tarefa de Olá devolvido pelo método de ator Olá. Este evento indica algum tipo de falha no código de ator Olá que necessita de investigação. |

tempo de execução do Olá Reliable Actors publica Olá execução toohello relacionados de contadores de desempenho dos métodos de atores a seguir.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Método de Ator do Service Fabric |Invocações por segundo |Número de vezes que Olá método do serviço de atores é invocado por segundo |
| Método de Ator do Service Fabric |Média em milissegundos por invocação |Método de serviço do tempo que demora tooexecute Olá ator em milissegundos |
| Método de Ator do Service Fabric |Exceções emitidas/seg |Número de vezes que Olá método do serviço de atores gerou uma exceção por segundo |

### <a name="concurrency-events-and-performance-counters"></a>Eventos de simultaneidade e contadores de desempenho
Olá Reliable Actors runtime emite Olá seguintes eventos relacionados com demasiado[simultaneidade](service-fabric-reliable-actors-introduction.md#concurrency).

| Nome do evento | ID de evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |Verboso |0x8 |Este evento é escrito no início de Olá de cada vez novo num ator. Contém Olá diversas pendentes chamadas de atores que estão a aguardar tooacquire Olá do bloqueio por ator que impõe a concorrência com base em ativar. |

tempo de execução do Olá Reliable Actors publica Olá seguir tooconcurrency relacionados de contadores de desempenho.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Ator do Service Fabric |chamadas de atores a aguardar que o bloqueio de ator |Número de pendentes a aguardar tooacquire Olá do bloqueio por ator que impõe a concorrência com base em vez de chamadas de atores |
| Ator do Service Fabric |Média em milissegundos por bloqueio de espera |Tooacquire tempo decorrido (em milissegundos) Olá do bloqueio por ator que impõe a concorrência com base em vez |
| Ator do Service Fabric |Média em milissegundos bloqueio de ator ativado |Tempo (em milissegundos) para que Olá é mantido do bloqueio por ator |

### <a name="actor-state-management-events-and-performance-counters"></a>Eventos de gestão do Estado de ator e contadores de desempenho
Olá Reliable Actors runtime emite Olá seguintes eventos relacionados com demasiado[gestão do Estado de ator](service-fabric-reliable-actors-state-management.md).

| Nome do evento | ID de evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |Verboso |0x4 |Tempo de execução de atores é sobre o estado do ator Olá toosave. |
| ActorSaveStateStop |11 |Verboso |0x4 |Tempo de execução de atores acabou de guardar o estado do ator Olá. |

tempo de execução do Olá Reliable Actors publica Olá seguintes contadores de desempenho relacionados tooactor gestão de estado.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Ator do Service Fabric |Média em milissegundos por operação de guardar Estado |Tempo decorrido toosave o estado de ator em milissegundos |
| Ator do Service Fabric |Média em milissegundos por operação de estado de carregamento |Tempo decorrido o estado do ator tooload em milissegundos |

### <a name="events-related-tooactor-replicas"></a>Eventos relacionados tooactor réplicas
Olá Reliable Actors runtime emite Olá seguintes eventos relacionados com demasiado[réplicas de ator](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

| Nome do evento | ID de evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |Informativo |0x1 |Réplica de ator alterado tooPrimary de função. Isto implica que serão criados atores Olá para esta partição dentro desta réplica. |
| ReplicaChangeRoleFromPrimary |2 |Informativo |0x1 |Réplica de ator Alterar função toonon principal. Isto implica que atores Olá para esta partição já não serão criados no interior desta réplica. Não existem novos pedidos serão entregues tooactors já criado dentro desta réplica. irão ser destruídos atores Olá depois de concluídos todos os pedidos em curso. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>Eventos de ativação e desativação de ator e contadores de desempenho
Olá Reliable Actors runtime emite Olá seguintes eventos relacionados com demasiado[ativação ator e desativação](service-fabric-reliable-actors-lifecycle.md).

| Nome do evento | ID de evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |Informativo |0x1 |Um ator tiver sido ativado. |
| ActorDeactivated |6 |Informativo |0x1 |Um ator foi desativada. |

tempo de execução do Olá Reliable Actors publica Olá seguintes contadores de desempenho relacionados com tooactor ativação e desativação.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Ator do Service Fabric |Média OnActivateAsync em milissegundos |Tempo decorrido tooexecute o método OnActivateAsync em milissegundos |

### <a name="actor-request-processing-performance-counters"></a>Contadores de desempenho do processamento do pedido de ator
Quando um cliente invoca um método através de um objeto de proxy de ator, que resulta numa mensagem de pedido enviada ao longo do serviço de atores do Olá rede toohello. serviço de Olá processa a mensagem de pedido de saudação e envia um cliente de back-toohello de resposta. tempo de execução do Olá Reliable Actors publica Olá após o processamento de pedidos de tooactor relacionados de contadores de desempenho.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Ator do Service Fabric |n. º de pedidos pendentes |Número de pedidos a ser processado no service Olá |
| Ator do Service Fabric |Média em milissegundos por pedido |Tempo decorrido (em milissegundos) por Olá serviço tooprocess um pedido |
| Ator do Service Fabric |Média em milissegundos para a desserialização do pedido |Mensagem de pedido de ator do tempo decorrido (em milissegundos) toodeserialize quando recebido no serviço de Olá |
| Ator do Service Fabric |Média em milissegundos para a serialização da resposta |Mensagem de resposta de tempo decorrido (em milissegundos) tooserialize Olá ator serviço Olá antes do envio de resposta Olá toohello cliente |

## <a name="next-steps"></a>Passos seguintes
* [Como Reliable Actors utilizar plataforma de Service Fabric Olá](service-fabric-reliable-actors-platform.md)
* [Documentação de referência da API de ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Código de exemplo](https://github.com/Azure/servicefabric-samples)
* [Fornecedores de EventSource no PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
