---
title: "aaaScale um recurso de infraestrutura do serviço de cluster ou reduzir | Microsoft Docs"
description: "Dimensione um cluster do Service Fabric ou reduzir a pedido de toomatch definindo as regras de dimensionamento automático para cada conjunto de dimensionamento da Máquina Virtual/tipo nó. Adicionar ou remover cluster do Service Fabric nós tooa"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>Um cluster do Service Fabric no ou utilizando regras de dimensionamento automático de escala
Conjuntos de dimensionamento de máquina virtual são um recurso de computação do Azure que pode utilizar toodeploy e gerir uma coleção de máquinas virtuais como um conjunto. Cada tipo de nó que está definido num cluster de Service Fabric está configurado como um conjunto de dimensionamento de Máquina Virtual separado. Cada tipo de nó, em seguida, pode ser ampliado na ou saída de forma independente, têm conjuntos diferentes de portas abertas e pode ter as métricas de capacidade diferentes. Saiba mais sobre-lo na Olá [nodetypes de Service Fabric](service-fabric-cluster-nodetypes.md) documento. Uma vez que os tipos de nó de Service Fabric Olá no seu cluster são constituídos por conjuntos de dimensionamento de Máquina Virtual no back-end de Olá, terá de tooset configurar regras de dimensionamento automático para cada conjunto de dimensionamento da Máquina Virtual/tipo nó.

> [!NOTE]
> A subscrição tem de ter suficiente tooadd núcleos Olá novas VMs que compõem este cluster. Não há nenhuma validação de modelo atualmente, para obter uma falha de tempo de implementação, se qualquer um dos limites de quota Olá são acessos.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Escolha o tipo do nó de Olá/Virtual dimensionamento da máquina definir tooscale
Atualmente, não toospecify capaz de regras de dimensionamento automático de Olá para conjuntos de dimensionamento de Máquina Virtual através do portal Olá, por isso, permitem-nos utilizar tipos de nó do Azure PowerShell (com+ 1.0) toolist Olá e, em seguida, adicionar toothem de regras de dimensionamento automático.

lista de Olá tooget da Máquina Virtual do conjunto de dimensionamento que compõem o cluster, execute Olá os seguintes cmdlets:

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Definir regras de dimensionamento automático para o conjunto de dimensionamento da Máquina Virtual/tipo Olá nó
Se o cluster tem vários tipos de nó, em seguida, repita que esta ação para cada nó tipos/Virtual dimensionamento da máquina define que pretende que tooscale (entrada ou saída). Demorar, no número de Olá de conta de nós, que tem de ter antes de configurar o dimensionamento automático. número mínimo de Olá de nós que tem de ter para o tipo de nó principal Olá é conduzido por nível de fiabilidade Olá que escolheu. Leia mais sobre [níveis de fiabilidade](service-fabric-cluster-capacity.md).

> [!NOTE]
> Dimensionamento baixo tooless de tipo de nó principal Olá que o número mínimo de Olá fazer cluster Olá instável, ou colocá-lo para baixo. Isto pode resultar em perda de dados para as suas aplicações e serviços do sistema de Olá.
> 
> 

Atualmente funcionalidade de dimensionamento automático de Olá não é condicionada por cargas Olá que as aplicações podem ser reporting tooService recursos de infraestrutura. Por isso, no Olá tempo depara-se de dimensionamento automático é puramente conduzido pelos contadores de desempenho de Olá que são emitidos por cada uma das instâncias de conjunto de dimensionamento de Máquina Virtual de Olá.  

Siga estas instruções [tooset segurança dimensionamento automático para cada conjunto de dimensionamento da Máquina Virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).

> [!NOTE]
> Uma escala baixo cenário, a menos que o tipo de nó tem um nível de durabilidade de ouro ou Silver terá toocall Olá [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/azure/mt125993.aspx) com o nome de nó adequado Olá.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Adicionar manualmente VMs tooa nó tipo/Virtual conjunto de dimensionamento da máquina
Siga Olá/instruções de exemplo no Olá [Galeria de modelo de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange Olá diversas VMs em cada Nodetype. 

> [!NOTE]
> A adição de VMs leva tempo, pelo que não espera Olá adições toobe instantânea. Para planear a capacidade de tooadd bem em tempo, tooallow durante mais de 10 minutos antes de Olá capacidade de VM está disponível para réplicas de Olá / tooget instâncias colocada de serviço.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Remova manualmente as VMs do conjunto de dimensionamento da Máquina Virtual/tipo Olá nó principal
> [!NOTE]
> executam serviços do sistema de recursos de infraestrutura de serviço de Olá no tipo de nó principal Olá no seu cluster. Por isso nunca deve encerrar ou reduzir verticalmente o número de Olá de instâncias em que tipos de nó menor do que o escalão de fiabilidade Olá warrants. Consulte demasiado[Olá detalhes sobre camadas de fiabilidade aqui](service-fabric-cluster-capacity.md). 
> 
> 

Terá de tooexecute seguinte Olá passos uma instância VM a uma hora. Este procedimento permite que os serviços de sistema de Olá (e os serviços com monitorização de estado) toobe encerrado sem problemas na instância de VM de Olá estiver a remover e réplicas novo criadas nos outros nós.

1. Executar [desativar ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) com o nó de Olá de toodisable 'RemoveNode' intenção vai tooremove (instância mais elevada para os Olá esse tipo de nó).
2. Executar [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake se esse nó Olá realmente transitou toodisabled. Caso contrário, aguarde até que o nó de Olá está desativada. Não é possível hurry este passo.
3. Siga Olá/instruções de exemplo no Olá [Galeria de modelo de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange Olá diversas VMs por um em que Nodetype. instância de Olá removida é maior instância de VM Olá. 
4. Repita os passos 1 a 3 conforme necessário, mas nunca reduzir verticalmente o número de Olá de instâncias em tipos de nó principal Olá menor que o escalão de fiabilidade Olá warrants. Consulte demasiado[Olá detalhes sobre camadas de fiabilidade aqui](service-fabric-cluster-capacity.md). 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Remova manualmente as VMs de Olá não primário nó tipo/Virtual conjunto de dimensionamento da máquina
> [!NOTE]
> Para um serviço com estado, precisa de um determinado número de nós toobe sempre para cima do Estado de disponibilidade e preserve toomaintain do seu serviço. Em Olá muito mínimo, precisa de número de Olá de toohello igual destino réplica conjunto o número de nós de Olá partição/serviços. 
> 
> 

Terá de Olá executar Olá uma instância VM passos a seguir a uma hora. Este procedimento permite que os serviços de sistema de Olá (e os serviços com monitorização de estado) toobe encerrar corretamente em Olá instância VM que está a remover e réplicas nova criada onde pessoa.

1. Executar [desativar ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) com o nó de Olá de toodisable 'RemoveNode' intenção vai tooremove (instância mais elevada para os Olá esse tipo de nó).
2. Executar [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake se esse nó Olá realmente transitou toodisabled. Se não for Aguarde até o nó de Olá está desativada. Não é possível hurry este passo.
3. Siga Olá/instruções de exemplo no Olá [Galeria de modelo de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange Olá diversas VMs por um em que Nodetype. Agora, esta ação irá remover instância de VM Olá mais elevada. 
4. Repita os passos 1 a 3 conforme necessário, mas nunca reduzir verticalmente o número de Olá de instâncias em tipos de nó principal Olá menor que o escalão de fiabilidade Olá warrants. Consulte demasiado[Olá detalhes sobre camadas de fiabilidade aqui](service-fabric-cluster-capacity.md).

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Comportamentos que pode observar no Service Fabric Explorer
Ao aumentar verticalmente Olá um cluster Service Fabric Explorer irá refletir o número de Olá de nós (as instâncias do conjunto de dimensionamento de Máquina Virtual), que fazem parte do cluster de Olá.  No entanto, quando dimensiona um cluster inativo, verá instância de nó/VM Olá removido apresentada em mau estado de funcionamento, a menos que tem de chamar [remover ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) com o nome de nó adequado Olá.   

Eis explicação Olá para este comportamento.

Olá nós listados no Service Fabric Explorer são um reflexão dos serviços de sistema de Service Fabric que Olá (FM especificamente) conhece o número de Olá de nós Olá cluster tinha/tem. Quando dimensionar Olá conjunto para baixo de dimensionamento de Máquina Virtual, Olá VM foi eliminada, mas o serviço do system FM pensa ainda nesse nó Olá (que foi mapeada toohello VM que foi eliminada) voltar. Por isso, Service Fabric Explorer continua toodisplay esse nó (embora o estado de funcionamento de Olá pode ser erro ou desconhecido).

No toomake de ordem se de que um nó é removido quando uma VM for removida, tem duas opções:

1) Escolha o nível de durabilidade de ouro ou Silver (disponível em breve) Olá para tipos de nó do cluster, que lhe oferece Olá integração de infraestrutura. Que, em seguida, removerá automaticamente nós de Olá do nosso estado do sistema de serviços (FM) quando reduzir verticalmente.
Consulte demasiado[Olá detalhes nos níveis de durabilidade aqui](service-fabric-cluster-capacity.md)

2) Assim que a instância de VM Olá tem sido ampliada para baixo, terá de toocall Olá [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/mt125993.aspx).

> [!NOTE]
> Clusters de recursos de infraestrutura serviços necessitam de um determinado número de nós toobe cópias de segurança em todos os Olá tempo na ordem toomaintain disponibilidade e preserve Estado - tooas referenciado "manter o quórum". Por isso, é normalmente insegura tooshut baixo todas as máquinas de Olá num cluster de Olá, exceto se tiver efetuado primeiro um [cópia de segurança completa do seu estado](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Passos seguintes
Olá leitura seguir tooalso Saiba mais sobre o planeamento da capacidade de cluster, atualização de um cluster e a criação de partições de serviços:

* [Planear a capacidade de cluster](service-fabric-cluster-capacity.md)
* [Atualizações de cluster](service-fabric-cluster-upgrade.md)
* [Serviços de monitorização de estado de partição para dimensionamento máximo](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
