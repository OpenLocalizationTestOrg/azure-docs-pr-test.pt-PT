---
title: "aaaOverview do modelo de programação de serviço do Service Fabric fiável Olá | Microsoft Docs"
description: "Saiba mais sobre o modelo de programação do Service Fabric serviço fiável e começar a escrever os seus próprios serviços."
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>Descrição geral do Reliable Services
Azure Service Fabric simplifica escrever e gerir serviços fiável sem monitorização de estado e com monitorização de estado. Este tópico abrange:

* Olá Reliable Services modelo de programação de para serviços sem monitorização de estado e com monitorização de estado.
* Opções de Olá tiver toomake ao escrever um serviço fiável.
* Alguns cenários e exemplos de quando toouse fiável serviços e como são escritos.

Reliable Services é uma das Olá modelos disponíveis no Service Fabric de programação. Olá, outro é Olá Ator fiável modelo de programação, que fornece um modelo de programação de Ator virtual por cima do modelo de Reliable Services Olá. Para obter mais informações sobre o modelo de programação do Olá Reliable Actors, consulte [tooService de introdução dos recursos de infraestrutura Reliable Actors](service-fabric-reliable-actors-introduction.md).

O Service Fabric gere duração Olá de serviços, a partir de aprovisionamento e implementação através da atualização e eliminação, através de [gestão de aplicações de Service Fabric](service-fabric-deploy-remove-applications.md).

## <a name="what-are-reliable-services"></a>Quais são Reliable Services?
Reliable Services dá-lhe um simples, poderoso, o nível superior de programação toohelp modelo express, o que é importante tooyour aplicação. Olá Reliable Services modelo de programação, obter:

* Restante toohello acesso Olá APIs de programação do Service Fabric. Ao contrário dos serviços do Service Fabric modelada como [convidado executáveis](service-fabric-deploy-existing-app.md), Reliable Services obter toouse restante Olá Olá APIs de recursos de infraestrutura de serviço diretamente. Isto permite que os serviços:
  * Sistema de Olá de consulta
  * Estado de funcionamento do relatório sobre entidades no cluster de Olá
  * receber notificações sobre as alterações de configuração e code
  * localizar e comunicar com outros serviços
  * (opcionalmente) utilizar Olá [coleções fiável](service-fabric-reliable-services-reliable-collections.md)
  * .. e. concedendo-lhes aceder toomany outras funcionalidades, tudo a partir de um modelo de programação de primeira classe em várias linguagens de programação.
* Um modelo simple para executar o seu próprio código que se pareça com modelos que é utilizados para de programação. O código tem um ponto de entrada bem definidos e o ciclo de vida facilmente gerido.
* Um modelo de comunicação incorporável. Utilize o transporte de Olá à sua escolha, tal como HTTP com [Web API](service-fabric-reliable-services-communication-webapi.md), WebSockets, protocolos TCP personalizados, ou qualquer outra função. Reliable Services fornecem algumas excelente out of box opções pode utilizar, ou pode fornecer os seus próprios.
* Para os serviços com monitorização de estado, Olá Reliable Services modelo de programação permite-lhe tooconsistently e fiável armazenar o estado do direito dentro do seu serviço utilizando [coleções fiável](service-fabric-reliable-services-reliable-collections.md). Coleções fiáveis são um conjunto simple de classes de coleção e de elevada disponibilidade fiável que irão estar familiarizado tooanyone que tenha utilizado c# coleções. Tradicionalmente, os serviços necessários sistemas externos para a gestão de estado fiável. Com coleções fiável, pode armazenar a computação tooyour seguinte estado com Olá mesma elevada disponibilidade e fiabilidade tiver tooexpect provenientes de arquivos de externos altamente disponíveis. Este modelo melhora também a latência porque são alocar conjuntamente Olá computação e de estado tem de toofunction.

Veja este vídeo Microsoft Virtual Academy para uma descrição geral dos serviços fiáveis:<center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>O que faz com que Reliable Services diferentes?
Reliable Services no Service Fabric são diferentes dos serviços que pode ter escritas antes. O Service Fabric fornece escalabilidade, consistência, disponibilidade e fiabilidade.

* **Fiabilidade** - a sua service mantém-se a cópia de segurança mesmo em ambientes pouco fiáveis, onde as máquinas falharam ou prima problemas de rede, ou em casos onde Olá serviços se encontrar erros e falhas ou falhar. Para os serviços com monitorização de estado, o estado é preservado mesmo na presença de Olá de rede ou outras falhas.
* **Disponibilidade** -o serviço é acessível e reativa. Service Fabric mantém o número pretendido de cópias a executar.
* **Escalabilidade** - os serviços são dissociados da hardware específico e podem aumentar ou diminuir o conforme necessário, através da adição de Olá ou remoção de hardware ou outros recursos. Os serviços são tooensure facilmente particionada (especialmente no caso de monitorização de estado de Olá) que pode dimensionar o serviço de Olá e o identificador de falhas parciais. Os serviços podem ser criados e eliminado dinamicamente através de código, permitir mais de instâncias toobe acelerada conforme necessário, diga na resposta toocustomer pedidos. Por fim, o Service Fabric encoraja lightweight toobe de serviços. Service Fabric permite milhares de toobe serviços aprovisionados dentro de um processo único, em vez de exigir ou dedicação de instâncias de SO todos ou processos tooa instância de um serviço.
* **Consistência** -todas as informações armazenadas neste serviço podem ser garantidas toobe consistente. Isto acontece mesmo através de várias coleções fiáveis dentro de um serviço. É possível efetuar alterações em coleções dentro de um serviço de uma forma de uma forma atomic.

## <a name="service-lifecycle"></a>Ciclo de vida do serviço
Se o serviço está com monitorização de estado ou sem monitorização de estado, Reliable Services fornecem um ciclo de vida simple que lhe permite rapidamente fixação no seu código e começar a utilizar.  Existem apenas um ou dois métodos que terá de tooimplement tooget seu serviço operacional.

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** -este método é onde o serviço de Olá define Olá comunicação stack(s) que quer que toouse. Olá, tais como a pilha de comunicações, [Web API](service-fabric-reliable-services-communication-webapi.md), é o que define Olá ponto final de escuta ou pontos finais para Olá serviço (como os clientes conseguirem contactar o serviço de Olá). Também define como mensagens hello que aparecem interagem com os restantes Olá código do serviço Olá.
* **Runasync com** -este método é onde o seu serviço é executada a respetiva lógica de negócio e onde-seria iniciar quaisquer tarefas em segundo plano que devem ser executado para duração Olá do serviço de Olá. o token de cancelamento de Olá fornecido é um sinal de quando esse trabalho deverá ser interrompida. Por exemplo, se o serviço de Olá tem mensagens toopull fora de uma fila fiável e processá-los, este é onde ocorre que funcionam.

Se estiver a aprender sobre reliable services para Olá pela primeira vez, leia sobre! Se pretender para instruções detalhadas Olá ciclo de vida dos serviços fiáveis, pode aceda demasiado[neste artigo](service-fabric-reliable-services-lifecycle.md).

## <a name="example-services"></a>Serviços de exemplo
Saber este modelo de programação, vamos ver rapidamente dois toosee diferentes serviços a forma como estas peças encaixam.

### <a name="stateless-reliable-services"></a>Sem monitorização de estado Reliable Services
Um serviço sem monitorização de estado é um onde há sem estado mantido no âmbito do serviço de Olá entre chamadas. Qualquer Estado que se encontra presente é inteiramente disposable e não necessita de sincronização, replicação, persistência ou elevada disponibilidade.

Por exemplo, considere uma calculadora que tenha sem memória e recebe todos os tooperform de termos e operações em simultâneo.

Neste caso, Olá `RunAsync()` (c#) ou `runAsync()` (Java) de Olá serviço pode estar vazio, porque não existe nenhum em segundo plano que o serviço de Olá de processamento de tarefas tem toodo. Quando é criado o serviço de Calculadora Olá, devolve uma `ICommunicationListener` (c#) ou `CommunicationListener` (Java) (por exemplo [Web API](service-fabric-reliable-services-communication-webapi.md)) que se abre um ponto final de escuta no algumas portas. Este ponto final de escuta hooks dos métodos de cálculo diferente toohello (exemplo: "Adicionar (n1, n2)") que define de API pública da Calculadora Olá.

Quando é efetuada uma chamada a partir de um cliente, método adequado Olá é invocado e serviço de calculadora de Olá efetua operações Olá Olá dados fornecidos e devolve o resultado de Olá. -Não armazena qualquer Estado.

Não armazenar qualquer Estado interno torna esta Calculadora de exemplo simples. Mas a maioria dos serviços não são verdadeiramente sem estado. Em vez disso, estes externalize toosome respetivo estado outro arquivo. (Por exemplo, todas as aplicações web que depende de manter o estado da sessão de um arquivo de cópia de segurança ou a cache não é sem monitorização de estado.)

Um exemplo comum dos serviços sem monitorização de estado como são utilizadas no Service Fabric é como um front-end que expõe Olá API destinado ao público para uma aplicação web. em seguida, o serviço de front-end Olá sua toostateful serviços toocomplete um pedido de utilizador. Neste caso, as chamadas a partir de clientes são direcionado tooa conhecido porta, por exemplo 80, onde o serviço sem estado Olá está a escutar. Este serviço sem monitorização de estado recebe Olá chamada e determina se a chamada de Olá é de uma entidade fidedigna e o serviço é destinado a.  Em seguida, o serviço de sem monitorização de estado de Olá reencaminha partição correto do Olá chamada toohello de serviço com estado Olá e aguarda uma resposta. Quando o serviço sem estado Olá recebe uma resposta, responde cliente original toohello. Um exemplo de tal serviço é nos nossos exemplos [c#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService). Esta é apenas um exemplo deste padrão de nos exemplos de Olá, existem outras pessoas, bem como outros exemplos.

### <a name="stateful-reliable-services"></a>Reliable Services com monitorização de estado
Um serviço com estado é aquele que tem de ter uma parte do estado mantido consistente e presente para que Olá toofunction de serviço. Considere um serviço que constantemente calcula um média móvel dos últimos um valor com base nas actualizações recebe. toodo, tem de ter Olá conjunto atual de pedidos de entrada tem de tooprocess e Olá média atual. Qualquer serviço que obtém, processa e armazena informações num arquivo externo (por exemplo, um Azure blob ou tabela arquivo hoje) tem o estado monitorizado. Apenas mantém o estado no armazenamento de Estados externos de Olá.

Maioria dos serviços hoje armazenar o respetivo estado externamente, uma vez que o arquivo externo Olá é o que fornece a fiabilidade, disponibilidade, escalabilidade e consistência para esse Estado. No Service Fabric, serviços não é necessária toostore respetivo estado externamente. Service Fabric encarrega-se parte destes requisitos para o código do serviço Olá e o estado do serviço de Olá.

> [!NOTE]
> Suporte para monitorização de estado Reliable Services não está disponível no Linux ainda (para c# ou Java).
>

Imaginemos que queremos toowrite um serviço que processa as imagens. toodo isto, Olá serviço demora uma série de imagem e Olá de tooperform conversões nessa imagem. Este serviço devolve um serviço de escuta de comunicação (vamos Suponhamos é um end de WebAPI) que expõe uma API, como `ConvertImage(Image i, IList<Conversion> conversions)`. Quando recebe um pedido, o serviço Olá armazena-a num `IReliableQueue`e devolve o cliente de toohello algumas id para acompanhar o pedido de Olá.

Neste serviço `RunAsync()` pode ser mais complexas. serviço Olá tem um ciclo dentro respetivo `RunAsync()` que obtém a pedidos de `IReliableQueue` e efetua conversões Olá pedidas. resultados de Olá obterem armazenados num `IReliableDictionary` para que quando o cliente de Olá volta a, podem obter as suas imagens convertidas. tooensure ou até mesmo se algo falhar imagem Olá não é perdido, este serviço fiável seria solicitar fora fila Olá, efetuar conversões Olá e armazenar o resultado de Olá tudo numa só transação. Neste caso, a mensagem de saudação é removida da fila de Olá e Olá estão armazenados no dicionário de resultado Olá apenas quando conversões Olá estiverem concluídas. Em alternativa, o serviço de Olá foi solicitar a imagem de Olá fora fila Olá e imediatamente armazene-o num arquivo remoto. Esta reduz Olá quantidade de serviço de estado do Olá tem toomanage, mas aumenta a complexidade, uma vez que o serviço de Olá tem tookeep Olá metadados necessários toomanage Olá remoto arquivo. Com uma abordagem, se algo falha no pedido de média Olá Olá permanece na Olá fila à espera toobe processado.

Uma coisa toonote sobre este serviço é que o se SOA como um serviço normal do .NET! Olá única diferença é que Olá estruturas de dados a ser utilizado (`IReliableQueue` e `IReliableDictionary`) são fornecidas pelo serviço de recursos de infraestrutura e são de elevada disponibilidade fiável, e consistente.

## <a name="when-toouse-reliable-services-apis"></a>Quando toouse fiável APIs de serviços
Se qualquer um dos seguintes Olá caracterizam suas necessidades de serviço de aplicações, em seguida, deve considerar a fiável APIs de serviços:

* Pretende código do serviço (e opcionalmente de estado) toobe de elevada disponibilidade e fiável
* Terá de garantias transacionais em várias unidades de estado (por exemplo, as ordens e itens de linha de ordem).
* Estado da aplicação pode ser naturalmente modelado como dicionários fiável e pelas filas.
* O código de aplicações ou estado tem toobe elevada com latência baixa leituras e escritas.
* A aplicação necessita de simultaneidade de Olá toocontrol ou granularidade de operações transacionadas num ou mais coleções fiável.
* Pretende que as comunicações de Olá toomanage ou Olá controlo a criação de partições de esquema para o seu serviço.
* O código tem um ambiente de tempo de execução free-threaded.
* A aplicação tem de toodynamically criar ou destruir dicionários fiável ou filas ou serviços todo no tempo de execução.
* É necessário tooprogrammatically fornecido de recursos de infraestrutura do serviço de cópia de segurança e restauro funcionalidades de controlo para o estado do serviço.
* A aplicação necessita de toomaintain histórico de alterações para o respetivas unidades de estado.
* Pretende toodevelop ou consumir fornecedores de estado personalizado, desenvolvido de terceiros de terceiros.

## <a name="next-steps"></a>Passos seguintes
* [Início rápido de serviços fiável](service-fabric-reliable-services-quick-start.md)
* [Reliable Services avançadas de utilização](service-fabric-reliable-services-advanced-usage.md)
* [modelo de programação do Olá Reliable Actors](service-fabric-reliable-actors-introduction.md)
