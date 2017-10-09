---
title: clusters aaaCreate Azure Service Fabric no Windows Server e do Linux | Microsoft Docs
description: "Clusters de Service Fabric executadas no Windows Server e do Linux, o que significa será capazes de aplicações de Service Fabric toodeploy e o anfitrião de qualquer lugar, pode executar o Windows Server ou Linux."
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Criar clusters de Service Fabric no Windows Server ou Linux
Um cluster do Service Fabric do Azure é um conjunto de ligados à rede de máquinas virtuais ou físicos para o qual os micro-serviços são implementados e geridos. Um computador ou a VM que faz parte de um cluster é designado por um nó de cluster. Clusters podem Dimensionar toothousands de nós. Se adicionar o novo cluster de toohello de nós, Service Fabric efetua novamente o balanceamento réplicas de partição de serviço Olá e instâncias em Olá maior número de nós. Em geral melhora o desempenho da aplicação e contenção de toomemory acesso diminui. Se não estão a ser utilizados nós de Olá no cluster de Olá forma eficiente, pode diminuir o número de Olá de nós no cluster de Olá. Service Fabric novamente efetua novamente o balanceamento réplicas de partição Olá e instâncias em Olá diminuído número de nós toomake melhor utilização de hardware de Olá em cada nó.

Service Fabric permite a criação de Olá de clusters de Service Fabric em quaisquer VMs ou computadores que executam o Windows Server ou Linux. Isto significa que é capaz toodeploy e executar aplicações de Service Fabric em qualquer ambiente em que tem um conjunto de computadores Windows Server ou Linux que estão interligados, sê-lo no local, Microsoft Azure ou com qualquer fornecedor de nuvem.

## <a name="create-service-fabric-clusters-on-azure"></a>Criar clusters do Service Fabric no Azure
É feita a criação de um cluster no Azure ou através de um modelo de recursos ou Olá portal do Azure. Leitura [criar um cluster do Service Fabric utilizando um modelo do Resource Manager](service-fabric-cluster-creation-via-arm.md) ou [criar um cluster do Service Fabric do portal do Azure de Olá](service-fabric-cluster-creation-via-portal.md) para obter mais informações.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Sistemas operativos suportados para clusters no Azure
São toocreate capaz de clusters em VMs em execução nesses sistemas operativos:

* Windows Server 2012 R2
* Windows Server 2016 
* 16.04 de Ubuntu Linux (em pré-visualização pública) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Criar autónoma do Service Fabric clusters no local ou com qualquer fornecedor de nuvem
O Service Fabric fornece um pacote de instalação para toocreate autónomo Service Fabric clusters no local ou em qualquer fornecedor de nuvem

Para obter mais informações sobre como configurar a infraestrutura de serviço autónomo clusters no Windows Server, leia [criação do cluster de Service Fabric para o Windows Server](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Quaisquer implementações de nuvem vs. as implementações no local
processo de Olá para criar um cluster do Service Fabric no local é semelhante toohello processo de criação de um cluster em nenhuma nuvem da sua preferência com um conjunto de VMs. Olá passos iniciais tooprovision Olá VMs são regida pelo fornecedor de nuvem Olá ou de ambiente no local que está a utilizar. Depois de ter um conjunto de VMs com conectividade de rede ativada entre eles, em seguida, Olá passos tooset dos pacotes de Service Fabric Olá, editar definições de cluster Olá e executar a criação do cluster Olá e scripts de gestão são idênticas. Isto garante que os dados de conhecimento e a experiência de operar e gerir clusters de Service Fabric é transferable quando escolhe tootarget novos ambientes de alojamento.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Vantagens da criação de clusters de Service Fabric autónomo
* São toochoose livre qualquer nuvem toohost do fornecedor do cluster.
* Aplicações de Service Fabric, escritas uma vez, podem ser executadas em vários ambientes de alojamento com alterações mínimas toono.
* Dados de conhecimento da criação de aplicações do Service Fabric acarreta de um tooanother de ambiente de alojamento.
* Operacional experiência de execução e gestão do Service Fabric clusters ativada através de um ambiente tooanother.
* Cliente abrangente alcance é unbounded por restrições de ambiente de alojamento.
* Existe uma camada adicional de proteção contra falhas ampla e fiabilidade porque pode mover serviços Olá sobre o ambiente de implementação tooanother se um centro de dados ou o fornecedor de nuvem tem um blackout.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Sistemas operativos suportados para clusters autónomos
São toocreate capaz de clusters em VMs ou computadores que executam estes sistemas operativos:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (brevemente)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Vantagens dos clusters de Service Fabric no Azure através de autónomos, que clusters de Service Fabric criado no local
Service Fabric os clusters em execução no Azure fornece vantagens relativamente ao opção no local de Olá, pelo que o se não tiver necessidades específicas para onde executar clusters, em seguida, sugerimos que executar no Azure. No Azure, podemos fornecer integração com outros serviços, tornando operações e a gestão de cluster Olá mais fácil e mais fiável e funcionalidades do Azure.

* **Portal do Azure:** portal do Azure torna mais fácil toocreate e gerir clusters.
* **O Azure Resource Manager:** utilização do Gestor de recursos do Azure permite que o facilitar a gestão de todos os recursos utilizados pelo cluster de Olá como uma unidade e simplifica a faturação e o controlo de custo.
* **Cluster do Service Fabric como um recurso do Azure** cluster A Service Fabric é um recurso ARM, pelo que pode ser modelo como fazer outros recursos do ARM no Azure.
* **Integração com a infraestrutura do Azure** Service Fabric coordena com Olá subjacente a infraestrutura do Azure para o SO, rede e outras atualizações tooimprove disponibilidade e fiabilidade das suas aplicações.  
* **Diagnósticos:** no Azure, fornecemos integração com o diagnóstico do Azure e análise de registos.
* **Dimensionamento automático:** para os clusters no Azure, podemos fornecer a funcionalidade incorporada dimensionamento automático devido tooVirtual máquina-conjuntos de dimensionamento. No local e noutros ambientes de nuvem, é necessário toobuild sua própria funcionalidade ou escala manualmente utilizando Olá APIs que expõe os recursos de infraestrutura de serviço para o dimensionamento de clusters de dimensionamento automático.

## <a name="next-steps"></a>Passos seguintes

* Criar um cluster no VMs ou computadores que executam o Windows Server: [criação do cluster de Service Fabric para o Windows Server](service-fabric-cluster-creation-for-windows-server.md)
* Criar um cluster no VMs ou computadores que executam o Linux: [Service Fabric no Linux](service-fabric-linux-overview.md)
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)

