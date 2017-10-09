---
title: aaaArchitecture do Service Fabric do Azure | Microsoft Docs
description: "Service Fabric é que uma plataforma de sistemas distribuídos utilizada toobuild dimensionável, fiável e aplicações facilmente geridos para a nuvem de Olá. Este artigo mostra a arquitetura de Olá do Service Fabric."
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>Arquitetura do Service Fabric
Service Fabric baseia-se com subsistemas em camadas. Estes subsistemas de permitem que aplicações toowrite são:

* Elevada disponibilidade
* Escalável
* Gerível
* Testable

Olá seguinte diagrama mostra subsistemas de principais de Olá do Service Fabric.

![Diagrama da arquitetura do Service Fabric](media/service-fabric-architecture/service-fabric-architecture.png)

Num sistema distribuído, Olá capacidade toosecurely comunicar entre os nós no cluster é fundamental. Olá base da pilha de Olá está subsistema de transporte de Olá, que fornece uma comunicação segura entre nós. Acima transporte Olá subsistema se situa o subsistema de Federação Olá, os clusters Olá nós diferentes para uma única entidade (com o nome clusters), para que possam detetar falhas, efetuar eleição leader e fornecem encaminhamento consistente Service Fabric. o subsistema de fiabilidade Olá, em camadas sobre subsistema de Federação Olá, é responsável por fiabilidade Olá dos serviços do Service Fabric através de mecanismos, tais como a replicação, a gestão de recursos e a ativação pós-falha. o subsistema de Federação Olá também subjacente Olá ativação e que aloja o subsistema, que gere o ciclo de vida de Olá de uma aplicação num único nó. o subsistema de gestão de Olá gere Olá ciclo de vida das aplicações e serviços. o subsistema de teste de Olá ajuda os programadores de aplicações testar os seus serviços através de falhas simuladas antes e após a implementação de ambientes de tooproduction de aplicações e serviços. Service Fabric fornece a capacidade de Olá tooresolve localizações de serviço através do respetivo subsistema de comunicação. Olá, modelos de programação de aplicações toodevelopers expostas são em camadas sobre estes subsistemas juntamente com as ferramentas de tooenable de modelo de aplicação Olá.

## <a name="transport-subsystem"></a>Subsistema de transporte
o subsistema de transporte de Olá implementa um canal de comunicação de datagrama de ponto a ponto. Este canal é utilizado para comunicação nos clusters de recursos de infraestrutura de serviço e a comunicação entre clientes e o cluster do Olá service fabric. Suporta unidirecional e padrões de comunicação de pedido-resposta, que fornece a base de Olá para implementar a difusão e multicast nas Olá camada de Federação. o subsistema de transporte de Olá protege comunicação utilizando X509 certificados ou de segurança do Windows. Este subsistema é utilizado internamente pelo serviço de recursos de infraestrutura e não está acessível diretamente toodevelopers para a programação de aplicações.

## <a name="federation-subsystem"></a>Subsistema de Federação
Ordem tooreason sobre um conjunto de nós num sistema distribuído, terá de toohave uma vista do sistema de Olá consistente. o subsistema de Federação Olá utiliza primitivos de comunicação de Olá fornecidos pelo subsistema de transporte de Olá e stitches Olá vários nós para um único cluster unificado pode pelo motivo sobre. Fornece Olá distribuída sistemas primitivos necessitam Olá por outros subsistemas - a deteção de falha, eleição leader e encaminhamento consistente. o subsistema de Federação Olá é desenvolvido com tabelas hash distribuída com um espaço de token de 128 bits. o subsistema de Olá cria uma topologia em anel nós Olá, com cada nó em anel Olá que está a ser atribuído um subconjunto de espaço de token de Olá de propriedade. Para a deteção de falha, a camada de Olá utiliza um mecanismo de locação com base em heart beating e arbitragem. o subsistema de Federação Olá também garante que através da associação intricate e protocolos de partida se existe apenas um único proprietário de um token em qualquer altura. Isto proporciona eleição leader e consistentes garantias de encaminhamento.

## <a name="reliability-subsystem"></a>Subsistema de fiabilidade
Olá subsistema de fiabilidade fornece Olá mecanismo toomake Olá estado de um serviço do Service Fabric altamente disponível através da utilização de Olá de Olá *replicador*, *Failover Manager*, e  *Balanceador de recursos*.

* Olá replicador assegura que as alterações de estado na réplica de serviço principal Olá será automaticamente réplicas toosecondary replicados, manter a consistência entre réplicas primária e secundária Olá num conjunto de réplicas do serviço. replicador Olá é responsável pela gestão de quórum entre réplicas Olá no conjunto de réplicas Olá. Interage com lista Olá tooget de unidade de ativação pós-falha de Olá de tooreplicate de operações e o agente de reconfiguração Olá fornece-o com a configuração de Olá do conjunto de réplicas Olá. Se a configuração indica as operações de Olá réplicas necessário toobe replicado. O Service Fabric fornece um replicador predefinido denominado replicador de recursos de infraestrutura, o que pode ser utilizado por Olá modelo API toomake Olá estado do serviço de elevada disponibilidade e fiável de programação.
* Olá Failover Manager assegura que quando são adicionados nós tooor removida do cluster de Olá, carga Olá é automaticamente redistribuída entre os nós disponíveis Olá. Se falhar um nó de cluster Olá, cluster Olá será automaticamente reconfigurar a disponibilidade do Olá serviço réplicas toomaintain.
* Olá Resource Manager coloca réplicas serviço através de domínio de falha no cluster de Olá e assegura que todas as unidades de ativação pós-falha estão operacionais. Olá Gestor de recursos também equilibra a recursos do serviço em Olá subjacente agrupamento partilhado de distribuição de carga uniform ideal de tooachieve de nós de cluster.

## <a name="management-subsystem"></a>Subsistema de gestão
o subsistema de gestão de Olá fornece ponto-a-ponto serviço e gestão de ciclo de vida de aplicações. Cmdlets do PowerShell e APIs administrativas permitem-lhe tooprovision, implementar, patches, a atualização e anular o aprovisionamento aplicações sem perda de disponibilidade. o subsistema de gestão de Olá efetua este através de Olá os seguintes serviços.

* **Gestor de clusters**: Este é o serviço primário Olá que interage com Olá Gestor de ativação pós-falha a partir de aplicações de Olá tooplace fiabilidade em nós de Olá com base nas restrições de posicionamento do serviço de Olá. Olá Gestor de recursos no subsistema de ativação pós-falha assegura que as restrições de Olá nunca sejam interrompidas. Gestor de clusters de Olá gere Olá ciclo de vida das aplicações de Olá de aprovisionar toode-aprovisionar. É integrado com tooensure de Gestor de estado de funcionamento de Olá que de disponibilidade de aplicações não é perdida numa perspetiva de estado de funcionamento semântica durante as atualizações.
* **Gestor de estado de funcionamento**: este serviço permite a monitorização de estado de funcionamento de aplicações, serviços e entidades do cluster. Entidades de cluster (por exemplo, nós, partições de serviço e as réplicas) podem comunicar informações de estado de funcionamento, o que são agregadas, em seguida, no arquivo de estado de funcionamento centralizada Olá. Estas informações de estado de funcionamento fornecem um instantâneo do Estado de funcionamento geral ponto no tempo dos serviços de Olá e nós distribuídas por vários nós num cluster de Olá, permitindo-lhe tootake quaisquer ações corretivas necessárias. Consulta de estado de funcionamento que APIs permitem-lhe eventos de estado de funcionamento de Olá tooquery comunicadas toohello subsistema de estado de funcionamento. consulta de estado de funcionamento de Olá APIs devolver do arquivo de dados de estado de funcionamento não processados Olá armazenados no estado de funcionamento de Olá ou Olá agregados, interpretado dados de estado de funcionamento para uma entidade de cluster específicos.
* **Arquivo de imagens**: este serviço fornece armazenamento e a distribuição da Olá os binários da aplicação. Este serviço fornece um arquivo de ficheiros distribuído simples em que aplicações Olá são carregado tooand transferido a partir do.

## <a name="hosting-subsystem"></a>Subsistema de alojamento
Gestor de clusters de Olá informa Olá subsistema (em execução em cada nó) que repara de alojamento tem toomanage para um determinado nó. Olá subsistema de alojamento, em seguida, gere Olá ciclo de vida da aplicação Olá nesse nó. Interage com Olá fiabilidade e o estado de funcionamento componentes tooensure que réplicas Olá são colocadas corretamente e que estão em bom estadas.

## <a name="communication-subsystem"></a>Subsistema de comunicação
Este subsistema fornece mensagens fiáveis dentro da deteção de cluster e o serviço de Olá através do serviço de nomes de Olá. Olá Naming service resolve localização tooa de nomes de serviço no cluster de Olá e permite que os utilizadores toomanage serviço nomes e propriedades. Utilizar o serviço de nomes de Olá, os clientes podem em segurança comunicar com qualquer nó do Olá cluster tooresolve um nome de serviço e obter metadados do serviço. Utilizar um cliente de nomenclatura simple API, os utilizadores do Service Fabric podem desenvolver serviços e clientes com capacidade de resolver Olá localização de rede atual, não obstante dynamism do nó ou Olá novamente o dimensionamento de clusters de Olá.

## <a name="testability-subsystem"></a>Subsistema de teste
Teste é um conjunto de ferramentas que tenham sido concebidas especificamente para fins de teste de serviços incorporados no Service Fabric. Olá ferramentas permitir que um programador facilmente induce falhas significativas e executar tooexercise de cenários de teste e validar Olá vários Estados e transições que um serviço irá ocorrer ao longo da respetiva duração, todos os de forma controlada e segura. Teste também fornece um mecanismo toorun mais testes que podem iterar através de vários possíveis falhas sem perda de disponibilidade. Isto fornece um ambiente de teste em produção.

