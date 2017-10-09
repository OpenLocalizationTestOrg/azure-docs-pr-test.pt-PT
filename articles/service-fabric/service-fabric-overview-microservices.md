---
title: aaaIntroduction toomicroservices no Azure | Microsoft Docs
description: "Uma descrição geral do motivo pelo qual a criação de aplicações em nuvem com uma abordagem de micro-serviços é importante para o desenvolvimento de aplicações modernas e como Azure Service Fabric fornece uma plataforma tooachieve de isto."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>Por que motivo um micro-serviços abordar toobuilding aplicações?
Como os programadores de software, não há nada de novo na forma como acreditamos sobre factoring uma aplicação em partes de componente. É paradigma central de Olá de orientação de objeto, abstrações de software e componentization. Atualmente, este factorization tende tootake Olá formato classes e interfaces entre camadas de tecnologia e bibliotecas partilhadas. Normalmente, é necessária uma abordagem em camadas com um arquivo de back-end, lógica de negócio de camada média e uma interface de front-end de utilizador (IU). O que *tem* alteraram ao longo do Olá últimos anos alguns é que podemos, como os programadores, está a criar aplicações que são de nuvem Olá distribuídas e condicionadas pela empresa Olá.

necessidades de negócio a alteração Olá são:

* Um serviço que é criado e funciona em clientes de tooreach escala em regiões geográficas novo (por exemplo).
* Entrega mais rápida de funcionalidades e capacidades toobe toorespond capaz de toocustomer exigências de uma forma seja ágil.
* Custos de tooreduce de utilização melhorada de recursos.

Estas necessidades de negócio são afetar *como* iremos criar aplicações.

Para obter mais informações sobre a abordagem de Olá toomicroservices do Azure, leia o artigo [micro-serviços: uma rotações de aplicação que utiliza a tecnologia de nuvem Olá](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).

## <a name="monolithic-vs-microservice-design-approach"></a>Monolithic vs abordagem de conceção de microsserviço
Todas as aplicações evoluem ao longo do tempo. Aplicações com êxito evoluem pelo facto de ser toopeople útil. Aplicações sem não evoluem e, eventualmente, foram preteridas. pergunta Olá torna-se: quanto sabe sobre os requisitos de hoje em dia, e que estes serão no Olá futura? Por exemplo, digamos que está a criar uma aplicação de relatórios para um departamento. Tem a certeza de que a aplicação Olá permanece no âmbito de Olá da sua empresa e de que os relatórios de Olá curta duração. À sua escolha abordagem é diferente do, diga, criação de um serviço que fornece as vídeo tootens conteúdo de milhões de clientes. 

Por vezes, obter algo saída porta Olá como prova de conceito é Olá despertar o fator, enquanto sabe que aplicações Olá podem reestruturada mais tarde. Não há pouca ponto excessiva de engenharia algo que nunca é utilizado. De Olá habitual engenharia compromisso. No Olá por outro lado, quando as empresas abordadas edifício hello nuvem, expectativa Olá é crescimento e utilização. problema de Olá é que o crescimento e escala estão imprevisíveis. Gostaríamos tooprototype capaz de toobe rapidamente sabendo também que estamos no toodeal caminho com êxito futuro. Esta é a abordagem de arranque lean Olá: criar, medidas, saiba e iterar.

Durante a era de cliente-servidor Olá, iremos tended toofocus na criação de aplicações em camadas através de tecnologias específicas em cada camada. termo do Olá *monolithic* aplicação tem emerged para estas abordagens. interfaces de Olá tended toobe entre camadas Olá e foi utilizado um design mais fortemente conjugado entre componentes em cada camada. Os programadores concebidos e factored classes que foram compiladas em bibliotecas e ligadas em conjunto para alguns executáveis e DLLs. 

Existem vantagens toosuch uma abordagem de monolithic design. É frequentemente toodesign mais simples e tem chamadas mais rápidas entre os componentes, porque estas chamadas são, muitas vezes, através de comunicação entre processos (IPC). Além disso, todos os testes de um único produto, tende toobe mais pessoas recursos eficiente. downside Olá é que existe uma sólida coupling entre camadas em camadas, e não pode dimensionar componentes individuais. Se precisar de correções tooperform ou atualizações, terá de toowait para outros toofinish os testes. É mais difícil toobe seja ágil.

Micro-serviços endereços estes downsides e mais alinhada com Olá anterior a necessidades comerciais, mas também têm benefícios e liabilities. Olá das vantagens micro-serviços é que cada um deles encapsula normalmente funcionalidades empresariais mais simples, o que pode aumentar ou reduzir verticalmente, teste, implementar e gere de forma independente. Uma vantagem importante de uma abordagem de microsserviço é que as equipas são condicionadas mais por cenários de negócios que através da tecnologia Olá abordagem em camadas encoraja. Na prática, mais pequenas equipas desenvolver um microsserviço com base no cenário de cliente em utilizam as tecnologias que escolherem. 

Por outras palavras, a organização de Olá não necessita de aplicações de microsserviço toostandardize técnico toomaintain. Equipas individuais que os seus próprios serviços podem fazer que é adequado para os mesmos com base nos conhecimentos de equipa ou o que é o problema de Olá toosolve mais adequado. Na prática, um conjunto de tecnologias recomendadas, tais como um determinado NoSQL arquivo ou estrutura da aplicação de web, é preferível.

downside Olá de micro-serviços inclui gerir Olá maior número de entidades separadas e lidar com implementações mais complexas e de controlo de versões. Tráfego de rede entre Olá micro-serviços aumenta, bem como as latências de rede correspondente Olá. Muitos serviços chatty, granulares são uma receitas para um nightmare de desempenho. Sem ferramentas toohelp ver estas dependências, é difícil demasiado "ver" todo o sistema Olá. 

Normas tornar a abordagem de microsserviço Olá funcionam aceita como toocommunicate e a tolerância a falhas das ações de Olá só tem de um serviço, em vez de rigid contratos. É importante toodefine estes contratos adiantado Olá conceber, porque os serviços de atualização independente entre si. Outra descrição coined para estruturar com uma abordagem de micro-serviços é "detalhada serviço arquitetura orientada (SOA)."

***No respetivo mais simples, hello micro-serviços design abordagem é sobre Federação dos serviços, com alterações independentes tooeach e normas acordado, para a comunicação desacoplada.***

Como são produzidas mais aplicações na nuvem, as pessoas detetar que este decomposição de Olá geral aplicação para os serviços de independentes, concentra-se cenário é uma abordagem de melhor a longo prazo.

## <a name="comparison-between-application-development-approaches"></a>Comparação entre abordagens de desenvolvimento de aplicações
![Desenvolvimento de aplicações de plataforma do Service Fabric][Image1]

1) Uma aplicação monolithic contém funcionalidades específicas do domínio e normalmente é dividida por camadas funcionais, por exemplo, dados, negócio e web.

2) Pode dimensionar a uma aplicação monolithic através da clonagem-lo em vários servidores/máquinas virtuais/contentores.

3) Uma aplicação de microsserviço separa funcionalidade nos serviços de menores separados.

4) Olá micro-serviços abordagem escalas terminar através da implementação de cada serviço independentemente, criar instâncias destes serviços em máquinas virtuais/servidores/contentores.

Conceber com um microsserviço abordagem não é um panacea para todos os projetos, mas mais detalhadamente alinhar com os objetivos de negócio Olá descritos anteriormente. Começar com uma abordagem monolithic poderá ser aceitável se souber que tenha de código do Olá oportunidade toorework hello mais tarde para uma estrutura de micro-serviços. Mais frequentemente, pode começa com uma aplicação monolithic e lentamente divida-a em fases, começando com áreas de funcional Olá que necessitam de toobe mais dimensionável, ou seja ágil.

toosummarize, Olá microsserviço abordagem é toocompose a aplicação de vários serviços pequenos. Serviços de Olá são executados nos contentores que são implementados através de um cluster de máquinas. Equipas menores desenvolver um serviço que se centra num cenário e independentemente de teste, versão, implementar e dimensionar cada serviço, para que a aplicação completo Olá pode evoluem.

## <a name="what-is-a-microservice"></a>O que é um microsserviço?
Existem definições diferentes das micro-serviços. Se procurar Olá Internet, encontrará muitos recursos úteis que fornecem as suas próprias viewpoints e definições. No entanto, a maioria Olá seguir características de micro-serviços é amplamente acordada:

* Encapsulam um cenário de negócio ou cliente. O que é o problema de Olá que são a resolver?
* Desenvolvido por uma pequena equipa de engenharia.
* Escritas em qualquer linguagem de programação e utilizar qualquer estrutura.
* São compostos de código e (opcionalmente). o estado, que são independentemente com versão do, implementadas e ampliada.
* Interagir com outros micro-serviços através de interfaces bem definidas e protocolos.
* Os nomes exclusivos (URL) utilizou tooresolve a respetiva localização.
* Permanecer consistente e disponíveis na presença de Olá de falhas.

Pode resumem estas características em:

***Aplicações de Microsserviço são compostas por pequenos, independentemente com versão e dimensionáveis concentra-se ao cliente os serviços que comunicam entre si através de protocolos padrão com interfaces bem definidas.***

Iremos abordadas duas primeiras pontos Olá Olá anterior a secção e agora vamos expanda no e esclarecer Olá outras pessoas.

### <a name="written-in-any-programming-language-and-use-any-framework"></a>Escritas em qualquer linguagem de programação e utilizar qualquer estrutura
Como programadores, deverá ser toochoose livre uma linguagem ou arquitetura que queremos, dependendo do nosso competências ou necessidades Olá do serviço de Olá. Em alguns serviços, poderá valor benefícios de desempenho de Olá do C++ acima de todos os pessoa. Outros serviços, poderá ser mais importante facilidade de Olá de gerido desenvolvimento em c# ou Java. Em alguns casos, poderá ser necessário toouse uma biblioteca de parceira específica, a tecnologia de armazenamento de dados, ou meios de exposição Olá tooclients de serviço.

Depois de escolher uma tecnologia, vêm toohello operacional ou o ciclo de vida gestão e o dimensionamento do serviço de Olá.

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>Permite que toobe de código e o estado independentemente com versão do, implementadas e escalado
No entanto, optar toowrite micro-serviços, Olá código do e, opcionalmente, o estado de Olá deve independentemente implementar, atualizar e dimensionar. Isto é, na verdade, uma das Olá mais difícil toosolve de problemas, porque se trata de baixo tooyour escolha das tecnologias. Para o dimensionamento, compreender a forma como toopartition (ou de partições horizontais) ambos Olá código e o estado é um desafio. Quando Olá código e o estado de utilizam tecnologias separadas, que é comum hoje em dia, scripts de implementação de Olá para sua microsserviço tem toobe toocope consegue com dimensionamento-los ambas. Este é também sobre agilidade e a flexibilidade, pelo que pode atualizar algumas das Olá micro-serviços sem ter tooupgrade todos eles em simultâneo.

Devolver toohello monolithic versus microsserviço abordagem para um momento, hello diagrama seguinte mostra as diferenças de Olá no estado de toostoring Olá abordagem.

#### <a name="state-storage-between-application-styles"></a>Armazenamento de estado entre os estilos de aplicação
![Armazenamento de Estados de plataforma do Service Fabric][Image2]

***abordagem de monolithic Olá Olá esquerda tem uma base de dados e de camadas de tecnologias específicas.***

***abordagem de micro-serviços Olá no Olá direita tem um gráfico de micro-serviços interligados onde o estado é normalmente âmbito toohello microsserviço e várias tecnologias são utilizadas.***

Uma abordagem monolithic, normalmente aplicação Olá utiliza uma base de dados. a vantagem de Olá é que é uma localização única, o que torna mais fácil toodeploy. Cada componente pode ter uma única tabela toostore estado. As equipas necessário toostrictly separado do Estado, que é um desafio. Inevitavelmente existem temptations tooadd uma nova coluna tooan cliente tabela existente, não uma associação entre as tabelas e criar dependências na camada de armazenamento Olá. Depois de esta situação acontece, não é possível aumentar componentes individuais. 

Abordagem de micro-serviços Olá, cada serviço gere e armazena o estado da sua própria. Cada serviço é responsável por código e o estado em conjunto toomeet Olá resposta às exigências de serviço Olá de dimensionamento. Um downside é que, quando existe um toocreate necessidade vistas ou consultas, de dados da sua aplicação, terá de tooquery em lojas de estado diferentes. Normalmente, isto é resolvido por ter um microsserviço separado que cria uma vista através de uma coleção de micro-serviços. Se precisar de tooperform várias consultas impromptu nos dados de Olá, cada microsserviço deve considerar a escrever o respetivo tooa data warehousing serviço de dados para análise offline.

Controlo de versões é toohello específico, implementado versão de um microsserviço, por isso, esse várias versões diferentes implementar e executar lado. Controlo de versões endereços cenários Olá em que uma versão mais recente de um microsserviço falha durante a atualização e tem de tooroll tooan de back-versão anterior. Olá outro cenário para controlo de versões está a efetuar A/B-estilo de teste, onde os utilizadores diferentes experiência versões diferentes do serviço de Olá. Por exemplo, é comum tooupgrade um microsserviço para um conjunto específico de novas funcionalidades de clientes tootest antes de a disponibilizar mais amplamente. Depois de gestão de ciclo de vida dos micro-serviços, agora dá-nos toocommunication entre eles.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>Interage com outros micro-serviços através de interfaces bem definidas e protocolos
Este tópico necessita de pouca atenção aqui, porque um vasto conjunto literature sobre a arquitetura orientada para serviços que foi publicada através de Olá nos últimos 10 anos descreve os padrões de comunicação. Geralmente, a comunicação de serviço utiliza uma abordagem REST com protocolos HTTP e TCP e XML ou JSON como formato de serialização Olá. A partir de uma perspetiva de interface, é sobre a adoção da abordagem de design Olá web. Mas nada o deixa de utilizar protocolos binários ou os seus próprios formatos de dados. Estar preparadas para pessoas toohave uma vez mais difícil utilizando o seu micro-serviços se estes estiverem disponíveis abertamente.

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>Um nome exclusivo (URL) utilizou tooresolve localização
Lembre-se como vamos manter a indicar que a abordagem de microsserviço Olá é como Olá web? Como web Olá, sua microsserviço tem toobe endereçável independentemente do local onde se encontra em execução. Se estiver a pensar sobre máquinas e qual está a executar um determinado microsserviço, coisas correrem incorretas rapidamente. 

No Olá resolve igual forma se o DNS se uma determinada máquina específica de tooa de URL, o microsserviço tem toohave um nome exclusivo para que seja detetável a sua localização atual. Micro-serviços tem nomes endereçáveis-as independentes da infraestrutura de Olá que estes estão em execução. Isto significa que há uma interação entre a forma como o seu serviço é implementado e como é detetado, porque tem toobe de registo do serviço. Igualmente, quando uma máquina falha, o serviço de registo de Olá tem indicam onde Olá serviço está agora a ser executado. 

Isto permite beneficiar de nos tópico seguinte toohello: resiliência e consistência.

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>Permanece consistente e disponíveis na presença de Olá de falhas
Lidar com falhas inesperadas é uma das Olá hardest toosolve de problemas, especialmente num sistema distribuído. Grande parte do código de Olá que vamos escrever como programadores está a processar as exceções e este é também onde hello mais tempo é gasto no teste. problema de Olá é mais envolvido que escrever código toohandle falhas. O que acontece quando ocorre uma falha de máquina olá onde Olá microsserviço está em execução? Não só terá toodetect esta falha de microsserviço (um problema no seu próprio disco rígido), mas também terá de algo toorestart sua microsserviço. 

Um microsserviço tem toofailures resiliente toobe e, muitas vezes, reiniciar noutra máquina por motivos de disponibilidade. Esta informação ser proveniente também baixo toohello Estado que foi guardado em nome de microsserviço Olá, onde Olá microsserviço pode recuperar deste Estado do e se Olá microsserviço é capaz de toorestart com êxito. Por outras palavras, tem de resiliência toobe na computação Olá (Olá processo reinicia), bem como a resiliência no estado de Olá ou dados (sem perda e Olá dados permanecem consistentes).

problemas de Olá de resiliência são compounded durante a outros cenários, como quando falhas ocorrem durante uma atualização da aplicação. Olá microsserviço, trabalhar com o sistema de implementação de Olá, não necessita de toorecover. Tem também de toothen decidir se pode continuar a versão mais recente do toomove toohello direta ou em vez disso, reverter toomaintain versão anterior do tooa num estado consistente. Perguntas, tais como se suficiente máquinas estão disponível tookeep daqui para a frente e como toorecover versões anteriores de microsserviço Olá necessário toobe considerado. Isto requer Olá microsserviço tooemit estado de funcionamento informações toobe capaz de toomake estas decisões.

### <a name="reports-health-and-diagnostics"></a>Estado de funcionamento de relatórios e diagnóstico
Pode parecer óbvios e são muitas vezes ignorada, mas um microsserviço deve comunicar o estado de funcionamento e diagnósticos. Caso contrário, não há poucas informações de uma perspetiva de operações. Correlacionar eventos de diagnóstico através de um conjunto de serviços independentes e lidar com skews do relógio de computador toomake sentido de ordem de evento Olá é difícil. No Olá formatos da mesma forma que interagem com um microsserviço através de protocolos acordado e os dados, emerges existe necessidade de uniformização na como toolog estado de funcionamento e eventos de diagnóstico que basicamente acabar num evento de arquivo para consultar e visualização. Uma abordagem de micro-serviços é chave que concorda com equipas diferentes no formato de um único registo. Tem de toobe eventos de diagnóstico de tooviewing uma abordagem consistente na aplicação Olá como um todo.

Estado de funcionamento é diferente do diagnóstico. Estado de funcionamento é sobre microsserviço Olá reporting as ações adequadas da tootake do estado atual. Um bom exemplo está a trabalhar com disponibilidade de toomaintain de mecanismos de atualização e implementação. Apesar de um serviço pode estar danificado devido a falhas de processo tooa ou reinicialização do computador, o serviço de Olá poderão ainda estar operacional. Olá última coisa que precisa é toomake este worse efetuando uma atualização. abordagem de melhor Olá é toodo uma investigação pela primeira vez ou aguarde algum tempo para Olá microsserviço toorecover. Eventos de estado de funcionamento de um microsserviço ajudam-na tomar decisões informadas e, em vigor, ajudar a criar serviços autorrecuperação.

## <a name="service-fabric-as-a-microservices-platform"></a>Serviço de recursos de infraestrutura como uma plataforma de micro-serviços
Azure Service Fabric emerged de uma transição pela Microsoft, de entrega de produtos de caixa, que foram normalmente monolithic no estilo, toodelivering serviços. experiência de Olá de compilação e a funcionar grande serviços, tais como SQL Database do Azure e a base de dados do Azure Cosmos em forma de Service Fabric. plataforma de Olá evoluiu e deu lugar ao longo do tempo como serviços mais adotado uma larga maioria-lo. Importante ainda, o Service Fabric tinha toorun não apenas no Azure, mas também das implementações autónomas do Windows Server.

***objetivo de Olá de Service Fabric é toosolve problemas de disco rígido Olá de criar e executar um serviço e utilizam os recursos de infraestrutura de forma eficiente, para que as equipas podem resolver problemas de empresas utilizando uma abordagem de micro-serviços.***

O Service Fabric fornece três toohelp áreas abrangente criar aplicações que utilizam uma abordagem de micro-serviços:

* Uma plataforma que fornece toodeploy de serviços do sistema, atualizar, detetar e reinicie os serviços de falha, detetar serviços, encaminhar mensagens, gerir o estado e monitorizar estado de funcionamento. Estes serviços do sistema em vigor ativar muitas das características de Olá de micro-serviços descritos anteriormente.
* Aplicações de toodeploy capacidade ambos em execução nos contentores ou como processa. Recursos de infraestrutura de serviço é um contentor e orchestrator de processo.
* APIs de programação produtivas, toohelp compilar aplicações como micro-serviços: [ASP.NET Core, Reliable Actors e Reliable Services](service-fabric-choose-framework.md). Pode escolher qualquer código toobuild sua microsserviço. Mas estas APIs torne tarefa Olá mais simples e integram com a plataforma de Olá um nível mais aprofundado. Desta forma, por exemplo, pode obter informações de estado de funcionamento e diagnósticos ou, pode tirar partido de elevada disponibilidade incorporada.

***Service Fabric é agnóstico relativamente sobre como criar o seu serviço, e pode utilizar qualquer tecnologia. No entanto, este fornecer APIs de programação incorporadas que torna mais fácil toobuild micro-serviços.***

### <a name="migrating-existing-applications-tooservice-fabric"></a>Migrar existente aplicações tooService recursos de infraestrutura
Uma abordagem de chave de tooService recursos de infraestrutura é código existente tooreuse, que, em seguida, pode ser modernized com micro-serviços novo. Existem cinco fases tooapplication modernization e pode iniciar e parar em qualquer uma das fases Olá. Estes são;

1) Colocar uma aplicação monolithic tradicional
2) Comparação de precisão e deslocar - Utilize contentores ou código do convidado executáveis toohost existente no Service Fabric.
3) Modernization - novo micro-serviços adicionados juntamente com o código de existente. 
4) Inovar - quebrar Olá monolithic micro-serviços puramente com base na necessidade.
5) Transformado micro-serviços - transformação Olá de existente monolithic aplicações ou criar novas aplicações greenfield.

![Migração tooMicroservices][Image3]

É importante tooemphasis novamente, que pode **iniciar e parar em qualquer um destas fases**, não são formos forçados toomoved toohello próxima fase. Vamos agora ver exemplos para cada um destas fases.

**Comparação de precisão e deslocar** - grande número de empresas é lifting e mudarem aplicações monolithic existentes em contentores toofor dois motivos pelos quais;

- Redução de custo devido a tooconsolidation e remoção de aplicações existentes de hardware ou com a densidade superior. 
- Contrato de implementação consistente entre desenvolvimento e operações.

Custos reductions são compreensíveis e na Microsoft grandes quantidades de aplicações existentes estão a ser de simplesmente toomillions dos utilizados no compromisso. Implementação consistente é mais difícil tooevaluate, mas como igualmente importante. Diz que os programadores podem ainda ser toochoose livre Olá tecnologia que conjuntos-las, no entanto, as operações de Olá apenas aceitar uma única forma toodeploy e gerir estas aplicações. -Alivia operações Olá de ter toodeal com a complexidade de Olá muitas tecnologias diferentes ou forçar os programadores tooonly escolha determinadas aqueles. Essencialmente, cada aplicação é de imagens de implementação autónomo.

Muitas organizações parar aqui. Que já têm vantagens Olá de contentores e o Service Fabric fornece Olá experiência de gestão completo de implementação, atualizações, controlo de versões, reverte, etc de monitorização de estado de funcionamento.

**Modernization** -é Olá adição de novos serviços em conjunto com o código de existente. Se pretender toowrite novo código, é melhor toodecide tootake breves passos para baixo do caminho do Olá micro-serviços. Isto foi possível adicionar um novo ponto final de REST API ou novo lógica de negócio. Desta forma, iniciar num journey Olá de micro-serviços novo edifício e práticas de desenvolvimento e implementação dos mesmos.

**Inovar** -Lembre-se esses original alteração necessidades comerciais início Olá deste artigo, que estão a impulsionar abordagem de micro-serviços Olá? A Olá esta fase é decisão, estes são acontecer toomy atual aplicação e se assim for, necessário toostart dividir monolith Olá ou innovating. Um exemplo aqui é quando uma base de dados se tornar um estrangulamento do processamento, uma vez que está a ser utilizado como uma fila de fluxo de trabalho. Como o número de Olá de pedidos de fluxo de trabalho aumentar Olá funcionam toobe necessidades distribuída de escala. Por isso, para essa informação específica da aplicação Olá que não é dimensionamento ou precisa tooupdate mais frequentemente, dividir este limite num microsserviço e inovar. 

**Transformado micro-serviços** -esta é a onde a aplicação totalmente composto (ou decomposed para) micro-serviços. Aqui tooreach efetuou journey do Olá micro-serviços. Pode começar aqui, mas toodo isto sem um toohelp de plataforma micro-serviços é um investimento significativo. 

### <a name="are-microservices-right-for-my-application"></a>São micro-serviços à direita para a minha aplicação?
Talvez. Iremos teve foi que como mais equipas na Microsoft começou toobuild para a nuvem de Olá por razões de negócio, muitos dos mesmos realizados vantagens Olá de seguindo uma abordagem de microsserviço semelhante. Bing, por exemplo, tenha sido desenvolver micro-serviços na pesquisa de anos. Para outras equipas, a abordagem de micro-serviços Olá foi novo. As equipas encontrado que ocorreram problemas de disco rígido toosolve fora do respetivas áreas de núcleos da força. Esta é a razão pela qual o Service Fabric adquiridos traction como tecnologia de Olá de eleição para criação de serviços.

objetivo do Olá de Service Fabric é complexidades de Olá tooreduce de criação de aplicações com uma abordagem de microsserviço, para que não tenham toogo através de como redesigns muitas dispendiosos. Comece por algo pequeno, dimensionar quando for necessário, despromover serviços, adicionar novos e evoluir com o cliente utilização é a abordagem de Olá. Também Sabemos que existem muitos outros problemas ainda toobe resolvidos toomake micro-serviços mais acessível para a maior parte dos programadores. Contentores e modelo de programação de ator Olá são exemplos de passos pequenos do que direção e estamos a certeza de que mais inovações irão surgir toomake isto mais fácil.
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Passos seguintes
* [Descrição geral de terminologia do Service Fabric](service-fabric-technical-overview.md)
* [Micro-serviços: Uma aplicação rotações utiliza a tecnologia de nuvem Olá](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png
