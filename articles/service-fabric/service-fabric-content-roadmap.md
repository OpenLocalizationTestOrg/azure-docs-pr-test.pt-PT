---
title: "mais informações sobre o Azure Service Fabric aaaLearn | Microsoft Docs"
description: "Saiba mais sobre conceitos principais de Olá e áreas principais do Azure Service Fabric. Fornece uma descrição geral expandida do Service Fabric e como toocreate micro-serviços."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>Por isso, pretende toolearn sobre recursos de infraestrutura de serviço?
Azure Service Fabric é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implementar e gerir micro-serviços escaláveis e fiáveis.  Service Fabric tem uma área de superfície grande, no entanto, e há muito toolearn.  Este artigo fornece um resumo dos recursos de infraestrutura de serviço e descreve os conceitos de principais de Olá, modelos, o ciclo de vida de aplicação, testar, clusters e monitorização de estado de funcionamento de programação. Olá leitura [descrição geral](service-fabric-overview.md) e [quais são micro-serviços?](service-fabric-overview-microservices.md) para uma introdução e como o Service Fabric pode ser utilizado toocreate micro-serviços. Este artigo não contém uma lista completa de conteúdo, mas a ligação toooverview e obter artigos iniciados para cada área de Service Fabric. 

## <a name="core-concepts"></a>Conceitos-chave
[Terminologia de Service Fabric](service-fabric-technical-overview.md), [modelo de aplicação](service-fabric-application-model.md), e [suportados modelos de programação](service-fabric-choose-framework.md) fornecer mais conceitos e as descrições, mas aqui são Noções básicas de Olá.

<table><tr><th>Conceitos-chave</th><th>Tempo de design</th><th>Tempo de execução</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>Tempo de design: tipo de aplicação, o tipo de serviço, pacote de aplicação e manifesto, pacote de serviço e o manifesto
Um aplicação é do tipo Olá. o nome/versão atribuído tooa coleção de tipos de serviço. Isto está definido um *ApplicationManifest.xml* ficheiro, que está incorporado num diretório do pacote de aplicação. Olá pacote de aplicação é, em seguida, copiado o arquivo de imagens do cluster do Service Fabric toohello. Em seguida, pode criar uma aplicação com o nome deste tipo de aplicação, que, em seguida, é executado dentro de cluster Olá. 

Um tipo de serviço é atribuída de Olá. o nome/versão do serviço de tooa código pacotes, pacotes de dados e pacotes de configuração. Isto é definido num ficheiro ServiceManifest.xml, que está incorporado num diretório de pacote de serviço. Olá diretório do pacote de serviço é, em seguida, referenciado por um pacote de aplicação *ApplicationManifest.xml* ficheiro. Dentro do cluster de Olá, depois de criar uma aplicação com nome, pode criar um serviço com nome de um dos Olá tipos de serviço do tipo de aplicação. Um tipo de serviço é descrito pelo respetivo *ServiceManifest.xml* ficheiro. o tipo de serviço Olá é composto por definições de configuração do código executável serviço, que são carregadas no tempo de execução, e os dados estáticos, que são consumidos pelo serviço de Olá.

![Tipos de aplicação de Service Fabric e os tipos de serviço][cluster-imagestore-apptypes]

Olá pacote de aplicações é um diretório de disco que contém o tipo de aplicação a Olá *ApplicationManifest.xml* ficheiro, que faz referência a pacotes de serviços de Olá para cada tipo de serviço que constitui o tipo de aplicação Olá. Por exemplo, um pacote de aplicação de um tipo de aplicação de e-mail pode conter o pacote de serviço de fila de tooa referências, um pacote de serviço de front-end e um pacote de serviço de base de dados. ficheiros de Olá no diretório de pacote de aplicação Olá estão arquivo de imagens do cluster do Service Fabric toohello copiado. 

Um pacote de serviço é um diretório de disco que contém o tipo de serviço a Olá *ServiceManifest.xml* ficheiro, que referencia o código de Olá, dados estáticos e pacotes de configuração para o tipo de serviço Olá. ficheiros de Olá no diretório de pacote de serviço Olá são referenciados por tipo de aplicação a Olá *ApplicationManifest.xml* ficheiro. Por exemplo, um pacote de serviço foi Consulte toohello código, dados estáticos e pacotes de configuração que compõem um serviço de base de dados.

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>Tempo de execução: clusters e nós, com o nome de aplicações, com o nome de serviços, partições e réplicas
Um [cluster do Service Fabric](service-fabric-deploy-anywhere.md) é um conjunto ligado à rede de máquinas virtuais ou físicas, no qual os microsserviços são implementados e geridos. Clusters podem Dimensionar toothousands de máquinas.

Um computador ou a VM que faz parte de um cluster é designado por um nó. Cada nó é atribuído um nome de nó (uma cadeia). Os nós têm características como propriedades de colocação. Cada computador ou a VM tem um serviço de início automático do Windows, `FabricHost.exe`, que inicia a executar após o arranque e, em seguida, inicia duas executáveis: `Fabric.exe` e `FabricGateway.exe`. Estes dois executáveis constituem nó Olá. Para programação ou para cenários de teste, pode alojar vários nós num único computador ou VM ao executar várias instâncias do `Fabric.exe` e `FabricGateway.exe`.

Uma aplicação com o nome é uma coleção de serviços com nome que efetua um determinado tipo de função ou funções. Um serviço executa uma função de completa e autónoma (que pode iniciar e executar independentemente outros serviços) e é composto de código, configuração e dados. Depois de um pacote de aplicação é copiado toohello arquivo de imagens, cria uma instância da aplicação Olá num cluster de Olá especificando um tipo de aplicação do pacote de aplicação Olá (utilizando o respetivo nome/versão). Cada instância de tipo de aplicação é atribuída um nome URI que se assemelha *fabric: / MyNamedApp*. Num cluster, pode criar várias aplicações com o nome de um tipo de aplicação único. Também pode criar aplicações com o nome dos tipos de aplicação diferente. Cada aplicação nomeada é gerido e com a versão independentemente.

Depois de criar uma aplicação com nome, pode criar uma instância de um dos respetivos tipos de serviço (um serviço com nome) no cluster de Olá especificando um tipo de serviço Olá (utilizando o respetivo nome/versão). Cada instância de tipo de serviço é atribuída um nome URI em URI da sua aplicação com o nome de âmbito. Por exemplo, se criar um serviço dentro de uma aplicação com o nome "MyNamedApp" com o nome "MyDatabase", Olá URI aspeto: *fabric: / MyNamedApp/MyDatabase*. Dentro de uma aplicação com nome, pode criar um ou mais serviços com nome. Cada serviço com o nome pode ter o seu próprio esquema de partição e réplica/instância contagens. 

Existem dois tipos de serviços: sem monitorização de estado e com monitorização de estado. Serviços sem monitorização de estado podem armazenar o estado persistente num serviço de armazenamento externo, como o Storage do Azure, SQL Database do Azure ou do Azure Cosmos DB. Utilize um serviço sem estado ao serviço Olá não tem nenhum armazenamento persistente de todo. Um serviço com estado utiliza o Service Fabric toomanage estado do serviço através das suas coleções fiável ou Reliable Actors modelos de programação. 

Ao criar um serviço com nome, especifique um esquema de partição. Serviços com grandes quantidades de estado dividir dados Olá por partições. Cada partição é responsável por uma parte Olá completa do Estado do serviço de Olá, que é distribuído por todos nós do cluster Olá. Dentro de uma partição, os serviços com nome sem monitorização de estado ter instâncias enquanto serviços nomeados com monitorização de estado têm as réplicas. Normalmente, sem monitorização de estado com nome serviços apenas alguma vez de ter uma partição, uma vez que não têm nenhum Estado interno. Com monitorização de estado com o nome dos serviços de manter o respetivo estado dentro de réplicas e de cada partição tem a suas próprias réplica definido. Operações de leitura e escrita são efetuadas a uma réplica (denominada Olá principal). Alterações toostate de escrita operações são replicados toomultiple outras réplicas (denominadas bases de dados secundárias Active Directory). 

Olá seguinte diagrama mostra Olá relação entre as aplicações e instâncias de serviço, partições e réplicas.

![As partições e réplicas dentro de um serviço][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>Criação de partições, dimensionamento e disponibilidade
[Criação de partições](service-fabric-concepts-partitioning.md) não é exclusivo tooService recursos de infraestrutura. Uma forma bem conhecida de criação de partições é a criação de partições de dados de mensagens em fila ou a fragmentação. Serviços com monitorização de estado com grandes quantidades de estado dividir dados Olá por partições. Cada partição é responsável por uma parte do Estado de conclusão de Olá do serviço de Olá. 

Olá as réplicas de cada partição são distribuídas por nós do cluster Olá, que lhe permite estado do serviço com nome demasiado[escala](service-fabric-concepts-scalability.md). À medida que os dados de Olá necessitam aumentam, aumentam as partições e o Service Fabric efetua novamente o balanceamento partições entre nós toomake uma utilização eficiente dos recursos de hardware. Se adicionar o novo cluster de toohello de nós, o Service Fabric rebalancear as réplicas de partição Olá em Olá maior número de nós. Em geral melhora o desempenho da aplicação e contenção de toomemory acesso diminui. Se não estão a ser utilizados nós de Olá no cluster de Olá forma eficiente, pode diminuir o número de Olá de nós no cluster de Olá. Service Fabric novamente efetua novamente o balanceamento réplicas de partição Olá através de Olá diminuído número de nós toomake melhor utilização hardware Olá em cada nó.

Dentro de uma partição, os serviços com nome sem monitorização de estado ter instâncias enquanto serviços nomeados com monitorização de estado têm as réplicas. Normalmente, sem monitorização de estado com nome serviços apenas alguma vez de ter uma partição, uma vez que não têm nenhum Estado interno. instâncias de partição Olá fornecem para [disponibilidade](service-fabric-availability-services.md). Se uma instância falhar, outras instâncias continuar toooperate normalmente e, em seguida, o Service Fabric cria uma nova instância. Com monitorização de estado com o nome dos serviços de manter o respetivo estado dentro de réplicas e de cada partição tem a suas próprias réplica definido. Operações de leitura e escrita são efetuadas a uma réplica (denominada Olá principal). Alterações toostate de escrita operações são replicados toomultiple outras réplicas (denominadas bases de dados secundárias Active Directory). Se uma réplica falhar, o Service Fabric cria uma nova réplica de réplicas existentes Olá.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Micro-serviços sem monitorização de estado e com monitorização de estado para o Service Fabric
Recursos de infraestrutura de serviço permite-lhe toobuild aplicações que são compostos micro-serviços ou contentores. Sem monitorização de estado micro-serviços (como gateways de protocolo e web proxies) não manter um Estado mutável fora de um pedido e a resposta do serviço de Olá. As funções de trabalho de serviços em nuvem do Azure são um exemplo de um serviço sem estado. Com monitorização de estado micro-serviços (por exemplo, contas de utilizador, as bases de dados, dispositivos, carts compras e filas) mantêm um Estado mutável, autoritativo, para além do pedido de Olá e respetiva resposta. Aplicações de dimensionamento de Internet de hoje consistem de uma combinação de micro-serviços sem monitorização de estado e com monitorização de estado. 

Uma chave differentation com o Service Fabric é o foco forte na criação de serviços com monitorização de estado, com Olá [incorporada modelos de programação ](service-fabric-choose-framework.md) ou de serviços com monitorização de estado. Olá [cenários de aplicação](service-fabric-application-scenarios.md) descrevem os cenários de olá onde são utilizados serviços com monitorização de estado.

Por que razão tem micro-serviços com monitorização de estado, juntamente com aqueles sem monitorização de estado? Olá dois principais razões são:

* Pode criar o débito de elevado, baixa latência, os serviços de processamento de tolerância a falhas de transação online (OLTP) por manter o código e Olá, feche dados no mesmo computador. Alguns exemplos são storefronts interativas, pesquisa, sistemas de Internet das coisas (IoT), sistemas de negociação, sistemas de deteção de processamento e fraude do cartão de crédito e gestão de registo pessoal.
* Pode simplificar a estrutura de aplicação. Com monitorização de estado micro-serviços remover a necessidade de Olá para filas adicionais e caches, que são tradicionalmente tooaddress Olá disponibilidade e a latência requisitos necessários de uma aplicação puramente sem estado. Serviços com monitorização de estado são naturalmente elevada disponibilidade e baixa latência, que reduz o número de Olá de mover partes toomanage na sua aplicação como um todo.

## <a name="supported-programming-models"></a>Modelos de programação suportados
Recursos de infraestrutura de serviço oferece várias formas toowrite e gerir os seus serviços. Os serviços podem utilizar Olá APIs de recursos de infraestrutura de serviço tootake tirem o máximo partido das funcionalidades e estruturas de aplicações da plataforma Olá. Os serviços também podem ser qualquer programa do executável compilado escritos em qualquer idioma e alojadas num cluster do Service Fabric. Para obter mais informações, consulte [suportados modelos de programação](service-fabric-choose-framework.md).

### <a name="containers"></a>Contentores
Por predefinição, o Service Fabric implementa e ativa serviços como processos. Serviço de recursos de infraestrutura também pode implementar serviços no [contentores](service-fabric-containers-overview.md). Importante ainda, pode combinar os serviços de processos e serviços nos contentores no Olá mesma aplicação. Serviço de recursos de infraestrutura suporta a implementação do Linux contentores contentores do Windows no Windows Server 2016. Pode implementar as aplicações existentes, serviços sem monitorização de estado ou serviços com monitorização de Estado nos contentores. 

### <a name="reliable-services"></a>Reliable Services
[Reliable Services](service-fabric-reliable-services-introduction.md) é uma estrutura simples de escrita de serviços que integram com a plataforma de Service Fabric Olá e beneficiam do conjunto completo de Olá das funcionalidades de plataforma. Reliable Services podem ser sem monitorização de estado (semelhante toomost serviço plataformas, tais como servidores web ou funções de trabalho na Cloud Services do Azure), onde o estado é persistente numa solução externa, como a base de dados do Azure ou o Table Storage do Azure. Reliable Services também podem ser com monitorização de estado, onde o estado é persistente diretamente no serviço de Olá próprio através de coleções fiável. Estado é efetuado [elevada](service-fabric-availability-services.md) através da replicação e distribuídos através de [criação de partições](service-fabric-concepts-partitioning.md), todos os geridos automaticamente pelo Service Fabric.

### <a name="reliable-actors"></a>Reliable Actors
Desenvolvida Reliable Services, Olá [Ator fiável](service-fabric-reliable-actors-introduction.md) framework é uma arquitetura de aplicações que implementa o padrão de Ator Virtual Olá, com base num padrão de conceção de ator Olá. arquitetura de Ator fiável Olá utiliza independentes unidades de estado e de computação com single-threaded execução chamada atores. Olá Ator fiável framework fornece incorporado na comunicação de atores e persistência do estado predefinido e configurações de escalamento horizontal.

### <a name="aspnet-core"></a>Núcleo de ASP.NET
Integra de Service Fabric [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) como um modelo de programação de primeira classe para a criação de web e aplicações de API

### <a name="guest-executables"></a>Executáveis de convidado
A [executável convidado](service-fabric-deploy-existing-app.md) é um existente, arbitrário executável (escrito em qualquer idioma) alojado num cluster do Service Fabric juntamente com outros serviços. Executáveis convidado não integrar diretamente com APIs de recursos de infraestrutura de serviço. No entanto, ainda beneficiam das funcionalidades Olá ofertas de plataforma, tais como estado de funcionamento personalizado e carregar relatórios e capacidade de deteção do serviço ao chamar as APIs REST. Também têm o suporte de ciclo de vida de aplicação completa. 

## <a name="application-lifecycle"></a>Ciclo de vida da aplicação
Com outras plataformas, uma aplicação no Service Fabric normalmente realiza Olá seguintes fases: estrutura, desenvolvimento, teste, implementação, a atualização, manutenção e remoção. O Service Fabric fornece suporte de primeira classe para Olá ciclo de vida de aplicação completa das aplicações em nuvem, de desenvolvimento através da implementação, gestão diária e desativação de tooeventual de manutenção. modelo de serviço Olá permite várias funções diferentes tooparticipate independentemente no ciclo de vida da aplicação Olá. [Ciclo de vida de aplicação de Service Fabric](service-fabric-application-lifecycle.md) fornece uma descrição geral de Olá APIs e como são utilizados pelas funções diferentes de Olá ao longo de fases Olá do ciclo de vida de aplicação de Service Fabric de Olá. 

ciclo de vida de aplicação completa de Olá pode ser gerido utilizando [cmdlets do PowerShell](/powershell/module/ServiceFabric/), [c# APIs](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [APIs de Java](/java/api/system.fabric._application_management_client), e [REST APIs](/rest/api/servicefabric/). Também pode configurar a integração contínua/contínua implementação pipelines com ferramentas como [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) ou [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md).

Olá vídeo Microsoft Virtual Academy seguinte descreve como toomanage o ciclo de vida de aplicação:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>Testar aplicações e serviços
toocreate verdadeiramente serviços de escala da nuvem, é tooverify crítico que as suas aplicações e serviços podem conseguir falhas do mundo real. Olá falhas Analysis Service foi concebido para serviços que são criados no Service Fabric de teste. Com Olá [falhas Analysis Service](service-fabric-testability-overview.md), pode induce falhas significativas e executar cenários de teste concluída contra as suas aplicações. Estes cenários de falhas e exercer e validar Olá vários Estados e transições que um serviço irá ocorrer ao longo da respetiva duração, todos os de forma consistente, controlada e segura.

[Ações](service-fabric-testability-actions.md) um serviço para testes com falhas individuais de destino. Um programador de serviço pode utilizá-las como blocos modulares toowrite complicou cenários. Exemplos de simulada falhas são:

* Reinicie um nó toosimulate qualquer número de situações em que uma VM ou o computador for reiniciado.
* Mova uma réplica do seu serviço com estado toosimulate balanceamento de carga, ativação pós-falha ou atualização da aplicação.
* Invocar perda de quórum no toocreate serviço com estado uma situação em que as operações de escrita não é possível continuar porque não existe não são suficientes réplicas "cópia de segurança" ou "secundário" tooaccept novos dados.
* Invocar perda de dados no toocreate serviço com estado uma situação em que todos os Estados de memória é completamente eliminados.

[Cenários](service-fabric-testability-scenarios.md) são operações complexas de compostas por uma ou mais ações. Olá falhas Analysis Service fornece dois cenários completos incorporados:

* [Cenário de Chaos](service-fabric-controlled-chaos.md)-simula contínuas, intercaladas falhas (correto e ungraceful) ao longo do cluster de Olá ao longo de períodos de tempo prolongados.
* [Cenário de ativação pós-falha](service-fabric-testability-scenarios.md#failover-test)-uma versão do cenário de teste de chaos Olá destina-se uma partição de serviço específicos, mantendo a outros serviços afetados.

## <a name="clusters"></a>Clusters
Um [cluster do Service Fabric](service-fabric-deploy-anywhere.md) é um conjunto ligado à rede de máquinas virtuais ou físicas, no qual os microsserviços são implementados e geridos. Clusters podem Dimensionar toothousands de máquinas. Um computador ou a VM que faz parte de um cluster é designado por um nó de cluster. Cada nó é atribuído um nome de nó (uma cadeia). Os nós têm características como propriedades de colocação. Cada computador ou a VM tem um serviço de início automático, `FabricHost.exe`, que inicia a executar após o arranque e, em seguida, inicia duas executáveis: Fabric.exe e FabricGateway.exe. Estes dois executáveis constituem nó Olá. Para cenários de teste, pode alojar vários nós num único computador ou VM ao executar várias instâncias do `Fabric.exe` e `FabricGateway.exe`.

Clusters de Service Fabric podem ser criados na máquinas virtuais ou físicas que executem Windows Server ou Linux. São capaz toodeploy e executar aplicações de Service Fabric em qualquer ambiente em que tem um conjunto de computadores Windows Server ou Linux que estão interligados: no local, no Microsoft Azure ou em qualquer fornecedor de nuvem.

Olá vídeo Microsoft Virtual Academy seguinte descreve os clusters de Service Fabric:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Clusters no Azure
Service Fabric os clusters em execução no Azure disponibiliza a integração com outras funcionalidades do Azure e os serviços, tornando operações e a gestão de cluster Olá mais fácil e mais fiável. Um cluster é um recurso do Azure Resource Manager, para modelar os clusters como quaisquer outros recursos no Azure. Gestor de recursos também fornece o facilitar a gestão de todos os recursos utilizados pelo cluster de Olá como uma única unidade. Clusters no Azure estão integradas no diagnóstico do Azure e análise de registos. Os tipos de nó de cluster são [conjuntos de dimensionamento de máquina virtual](/azure/virtual-machine-scale-sets/index), pelo que a funcionalidade de dimensionamento automático é incorporada.

Pode criar um cluster no Azure através de Olá [portal do Azure](service-fabric-cluster-creation-via-portal.md), de um [modelo](service-fabric-cluster-creation-via-arm.md), ou a partir de [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

pré-visualização de Olá do Service Fabric no Linux permite-lhe toobuild, implementar e gerir aplicações de elevada disponibilidade e altamente dimensionáveis no Linux, tal como faria no Windows. estruturas de Service Fabric Olá (Reliable Services e Reliable Actors) estão disponíveis em Java em Linux, adição tooC n. º (.NET Core). Também pode criar [os serviços de convidados executável](service-fabric-deploy-existing-app.md) com qualquer linguagem ou arquitetura. Além disso, a pré-visualização de Olá também suporta da orquestração contentores de Docker. Os contentores de docker podem executar executáveis de convidado ou serviços do Service Fabric nativos, que utilizam as estruturas de Service Fabric Olá. Para obter mais informações, leia o artigo [Service Fabric no Linux](service-fabric-linux-overview.md).

Uma vez que o Service Fabric no Linux é uma pré-visualização, existem algumas funcionalidades que são suportadas no Windows, mas não no Linux. toolearn mais, leia [diferenças entre o Service Fabric no Linux e Windows](service-fabric-linux-windows-differences.md).

### <a name="standalone-clusters"></a>Clusters autónomos
O Service Fabric fornece um pacote de instalação para toocreate autónomo Service Fabric clusters no local ou em qualquer fornecedor de nuvem. Autónomo clusters conceder Olá liberdade toohost um cluster, onde quiser. Se os seus dados são toocompliance do requerente ou restrições de regulamentação ou, se quiser tookeep local dados, pode alojar o seu próprio cluster e aplicações. Aplicações de Service Fabric podem ser executadas em vários ambientes de alojamento sem alterações, pelo que os dados de conhecimento da criação de aplicações acarreta de um tooanother de ambiente de alojamento. 

[Criar o primeiro cluster de autónoma do Service Fabric](service-fabric-get-started-standalone-cluster.md)

Clusters do Linux autónomos ainda não são suportadas.

### <a name="cluster-security"></a>Segurança do cluster
Clusters tem de ser utilizadores protegidos tooprevent não autorizado a ligação de tooyour cluster, sobretudo quando tem cargas de trabalho de produção em execução no mesmo. Embora seja possível toocreate um cluster não segura, se o fizer, permite que os utilizadores anónimos tooconnect tooit se pontos finais de gestão são expostos toohello internet pública. Não é possível toolater ativar segurança num cluster protegida: segurança do cluster está ativada no momento de criação do cluster.

cenários de segurança do cluster Olá são:
* Segurança de nó de nó
* Segurança de nó de cliente
* Controlo de acesso baseado em funções (RBAC)

Para obter mais informações, leia o artigo [proteger um cluster](service-fabric-cluster-security.md).

### <a name="scaling"></a>Dimensionamento
Se adicionar o novo cluster de toohello de nós, Service Fabric efetua novamente o balanceamento réplicas de partição Olá e instâncias em Olá maior número de nós. Em geral melhora o desempenho da aplicação e contenção de toomemory acesso diminui. Se não estão a ser utilizados nós de Olá no cluster de Olá forma eficiente, pode diminuir o número de Olá de nós no cluster de Olá. Service Fabric novamente efetua novamente o balanceamento réplicas de partição Olá e instâncias em Olá diminuído número de nós toomake melhor utilização de hardware de Olá em cada nó. Pode dimensionar clusters no Azure ou [manualmente](service-fabric-cluster-scale-up-down.md) ou [programaticamente](service-fabric-cluster-programmatic-scaling.md). Podem ser escalados para clusters autónomos [manualmente](service-fabric-cluster-windows-server-add-remove-nodes.md).

### <a name="cluster-upgrades"></a>Atualizações de cluster
Periodicamente, são lançadas novas versões do tempo de execução do Olá Service Fabric. Efetua as atualizações de tempo de execução ou recursos de infraestrutura, no seu cluster, para que executem sempre um [versão suportada](service-fabric-support.md). Além disso toofabric atualiza, também pode atualizar a configuração de cluster, tais como certificados ou as portas de aplicação.

Um cluster do Service Fabric é um recurso que possui, mas está parcialmente gerida pela Microsoft. Microsoft é responsável pela aplicação de patches Olá subjacente SO e efetuar as atualizações de recursos de infraestrutura no seu cluster. Pode definir o seu cluster tooreceive automática dos recursos de infraestrutura atualizações, quando a Microsoft disponibiliza uma nova versão, ou escolha tooselect uma versão suportada de recursos de infraestrutura que pretende. As atualizações de recursos de infraestrutura e a configuração podem ser definidas através de Olá portal do Azure ou através do Resource Manager. Para obter mais informações, leia o artigo [atualizar um cluster do Service Fabric](service-fabric-cluster-upgrade.md). 

Um cluster autónomo é um recurso que é completamente próprio. É responsável pela aplicação de patches Olá subjacente SO e iniciar as atualizações de recursos de infraestrutura. Se o cluster pode ligar-se demasiado[https://www.microsoft.com/download](https://www.microsoft.com/download), pode definir transferência tooautomatically cluster e aprovisionar Olá recursos de infraestrutura de serviço novo pacote de tempo de execução. Em seguida, deverá iniciar atualização Olá. Se o cluster não conseguir aceder [https://www.microsoft.com/download](https://www.microsoft.com/download), pode transferir manualmente o novo pacote de tempo de execução Olá partir de uma máquina ligado à internet e, em seguida, iniciar a atualização de Olá. Para obter mais informações, leia o artigo [atualizar um cluster de Service Fabric autónomo](service-fabric-cluster-upgrade-windows-server.md).

## <a name="health-monitoring"></a>Monitorização do estado de funcionamento
Service Fabric apresenta um [modelo de estado de funcionamento](service-fabric-health-introduction.md) concebido cluster mau estado de funcionamento tooflag e condições de aplicação no entidades específicas (como nós de cluster e réplicas do serviço). modelo de estado de funcionamento de Olá utiliza Informadores de estado de funcionamento (componentes de sistema e watchdogs). o objetivo de Olá é rápido e fácil de diagnóstico e de reparação. Os escritores de serviço tem de antemão toothink sobre estado de funcionamento e como demasiado[relatórios de estado de funcionamento de design](service-fabric-report-health.md#design-health-reporting). Deve ser comunicada qualquer condição que pode afetar o estado de funcionamento, especialmente se pode ajudar a problemas de sinalizador fechar toohello raiz. informações de estado de funcionamento de Olá podem poupar tempo e esforço na depuração e investigação assim que o serviço de Olá está ativo e em execução à escala na produção.

monitor de Informadores de Service Fabric Olá identificados condições de interesse. Estes relatórios sobre as condições com base na respetiva vista local. Olá [arquivo de estado de funcionamento](service-fabric-health-introduction.md#health-store) agrega dados de estado de funcionamento enviados por todos os Informadores toodetermine se entidades estão em bom estado de funcionamento global. modelo de Olá é toouse avançado, flexíveis e fáceis de toobe pretendido. qualidade de Olá dos relatórios de estado de funcionamento de Olá determina precisão Olá da vista de estado de funcionamento de Olá do cluster de Olá. Falsos positivos que mostram erradamente problemas mau estado de funcionamento podem afetar negativamente as atualizações ou outros serviços que utilizam dados de estado de funcionamento. Exemplos desses serviços são serviços de reparação e mecanismos de alertas. Por conseguinte, algumas profundamente é tooprovide necessários relatórios que capturam as condições de interesse no Olá melhor forma possível.

Relatórios podem ser feito de:
* Olá monitorizados instâncias ou de réplicas de serviço do Service Fabric.
* Watchdogs internos implementados como um serviço do Service Fabric (por exemplo, um serviço sem monitorização de estado serviço Fabric que monitoriza condições e relatórios de problemas). watchdogs Olá podem ser implementados em todos os nós ou podem ser serviço toohello com monitorizados.
* Watchdogs internos que serem executadas em nós de Service Fabric Olá, mas não estão implementados como serviços do Service Fabric.
* Externa watchdogs esse recurso Olá de sonda de cluster do Service Fabric Olá externa (por exemplo, serviço de monitorização, como Gomez).

Box Olá, os componentes do Service Fabric reportam o estado de funcionamento em todas as entidades no cluster de Olá. [Relatórios de estado de funcionamento do sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md) proporcionam visibilidade do cluster e aplicação funcionalidade e sinalizador problemas através do Estado de funcionamento. Para aplicações e serviços, relatórios de estado de funcionamento do sistema Certifique-se de que as entidades são implementadas e se comportam corretamente da perspetiva de Olá Olá Service Fabric Runtime. relatórios de Olá não fornecem qualquer monitorização de estado de funcionamento de lógica de negócio Olá do serviço de Olá ou detetar processos bloqueados. lógica de tooadd informações tooyour específico do serviço de integridade, [implementar o relatório de estado de funcionamento personalizado](service-fabric-report-health.md) nos serviços.

O Service Fabric fornece várias formas demasiado[ver relatórios de estado de funcionamento](service-fabric-view-entities-aggregated-health.md) agregados no arquivo de estado de funcionamento de Olá:
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) ou outras ferramentas de visualização.
* Consultas de estado de funcionamento (através de [PowerShell](/powershell/module/ServiceFabric/), Olá [c# FabricClient APIs](/api/system.fabric.fabricclient.healthclient) e [Java FabricClient APIs](/java/api/system.fabric._health_client), ou [REST APIs](/rest/api/servicefabric)).
* Gerais consultas que devolvam uma lista de entidades que têm o estado de funcionamento como uma das propriedades de Olá (através do PowerShell, API de Olá ou REST).

Olá que seguintes Microsoft Virtual Academy vídeo descreve o modelo de estado de funcionamento do Service Fabric Olá e como são utilizadas:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>Passos seguintes
* Saiba como toocreate um [cluster no Azure](service-fabric-cluster-creation-via-portal.md) ou um [cluster autónomo no Windows](service-fabric-cluster-creation-for-windows-server.md).
* Tente criar um serviço utilizando Olá [Reliable Services](service-fabric-reliable-services-quick-start.md) ou [Reliable Actors](service-fabric-reliable-actors-get-started.md) modelos de programação.
* Saiba como demasiado[migrar a partir de serviços em nuvem](service-fabric-cloud-services-migration-differences.md).
* Saiba demasiado[monitorizar e diagnosticar os serviços](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). 
* Saiba demasiado[testar as suas aplicações e serviços](service-fabric-testability-overview.md).
* Saiba demasiado[gerir e orquestram os recursos do cluster](service-fabric-cluster-resource-manager-introduction.md).
* Examine Olá [exemplos de Service Fabric](http://aka.ms/servicefabricsamples).
* Saiba mais sobre [as opções de suporte do Service Fabric](service-fabric-support.md).
* Olá leitura [blogue de equipa](https://blogs.msdn.microsoft.com/azureservicefabric/) para artigos e anúncios.


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
