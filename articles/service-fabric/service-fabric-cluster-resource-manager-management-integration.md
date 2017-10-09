---
title: "aaaService Gestor de recursos de Cluster de recursos de infraestrutura - integração de gestão | Microsoft Docs"
description: "Uma descrição geral de pontos de integração de Olá entre Olá Gestor de recursos do Cluster e gestão de recursos de infraestrutura de serviço."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9a24c9de121fbe2e8e5e8e4d117e64686918936a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a>Integração de Gestor de recursos de cluster com a gestão de cluster do Service Fabric
Olá Gestor de recursos de Cluster do serviço de recursos de infraestrutura não unidade atualizações no Service Fabric, mas está envolvida. Olá forma primeiro que Olá ajuda-o Gestor de recursos de Cluster com a gestão é pelo controlo Olá pretendido estado do cluster Olá e serviços Olá dentro do mesmo. Olá Gestor de recursos do Cluster de envia relatórios de estado de funcionamento quando este não é possível colocar o cluster Olá numa configuração pretendida Olá. Por exemplo, se não existir insuficientes Olá capacidade Gestor de recursos do Cluster envia os avisos de estado de funcionamento e erros que possam indicar problemas de Olá. Outra informação de integração tem toodo com como funcionam as atualizações. Olá Gestor de recursos do Cluster altera o comportamento ligeiramente durante as atualizações.  

## <a name="health-integration"></a>Integração de estado de funcionamento
Olá Gestor de recursos do Cluster constantemente controla as regras de Olá que definiu para colocar os serviços. É também controla Olá restantes capacidade para cada métrica em nós de Olá e no cluster de Olá e no cluster de Olá como um todo. Se não é possível satisfazer essas regras ou se existir capacidade insuficiente, erros e avisos sobre o estado de funcionamento são emitidos. Por exemplo, se um nó é efetuada através de capacidade e Olá Gestor de recursos do Cluster tentará situação de Olá toofix movendo serviços. Se este não é possível corrigir a situação de Olá emite um aviso de estado de funcionamento que indica que o nó é através de capacidade de e para as métricas.

Outro exemplo de Olá Resource Manager avisos de estado de funcionamento é violações de restrições de posicionamento. Por exemplo, se definiu uma restrição de posicionamento (tais como `“NodeColor == Blue”`) e Olá Resource Manager Deteta uma violação dessa restrição, emite um aviso de estado de funcionamento. Isto é verdadeiro para restrições personalizadas e restrições predefinidas de Olá (como restrições de domínio de falhas e de domínio de atualização de Olá).

Eis um exemplo de um relatório de estado de funcionamento deste tipo. Neste caso, o relatório de estado de funcionamento de Olá é uma das partições do serviço de sistema Olá. mensagem de estado de funcionamento de saudação indica Olá réplicas dessa partição estão temporariamente packed em poucos domínios de atualização.

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating hello Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

Eis o que esta mensagem de estado de funcionamento está a informar-nos é:

1. Todas as réplicas de Olá próprios estão em bom Estadas: cada tem AggregatedHealthState: Ok
2. Olá restrição de distribuição de domínio de atualização está atualmente a ser violado. Isto significa que um determinado domínio de atualização tem mais réplicas desta partição que devia.
3. Nó que contém a violação de Olá que provocou do Olá réplica. Neste caso é nó Olá com o nome de Olá "Node.8"
4. Indica se uma atualização está a acontecer para esta partição ("atualmente atualizar – false")
5. Olá, política de distribuição para este serviço: "--de política de distribuição mais". Isto é regido pelos Olá `RequireDomainDistribution` [política de colocação](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). "Packing" indica que neste caso DomainDistribution foi _não_ necessário, para que possamos saber que a política de colocação não foi especificada para este serviço. 
6. Quando o relatório de Olá foi efetuada - 8/10/2015 as 19:13:02: 00

Informações como esta alertas powers que fire no toolet produção sabe algo tornou errado e também é utilizada toodetect e pare atualizações incorretas. Neste caso, seria aconselhável toosee se vamos descobrir o motivo pelo qual Olá Gestor de recursos tinha réplicas de Olá toopack para Olá domínio de atualização. Normalmente, packing é transitório porque nós Olá Olá outros domínios de atualização foram, por exemplo.

Digamos Olá Gestor de recursos de Cluster está a tentar tooplace alguns serviços, mas não existe qualquer soluções que funcionam. Quando não não possível colocar os serviços, destina-se, normalmente, um dos Olá seguintes motivos:

1. Alguns condição transitória fez com que tooplace impossível esta instância de serviço ou a réplica corretamente
2. requisitos de posicionamento do serviço de Olá são unsatisfiable.

Nestes casos, relatórios de estado de funcionamento de Olá Gestor de recursos do Cluster de ajudam a determinar por que motivo não é possível colocar o serviço de Olá. Chamamos a esta sequência de eliminação de restrição de Olá do processo. Durante a mesma, sistema Olá explica as restrições de Olá configurado que afetam o serviço de Olá e registos possam eliminar. Desta forma, quando os serviços não são capaz toobe colocada, pode ver quais os nós que foram eliminados e por que motivo.

## <a name="constraint-types"></a>Tipos de restrição
Vamos falar sobre cada uma das restrições de diferentes Olá nestes relatórios de estado de funcionamento. Verá as restrições de toothese relacionados de mensagens de estado de funcionamento quando não não possível colocar as réplicas.

* **ReplicaExclusionStatic** e **ReplicaExclusionDynamic**: destas restrições indica que uma solução foi rejeitada porque a mesma partição de Olá dois objetos de serviço do seria ter toobe colocada Olá mesmo nó. Isto não é permitido porque, em seguida, falha de nó excessivamente teria um impacto dessa partição. ReplicaExclusionStatic e ReplicaExclusionDynamic são quase Olá mesmas diferenças de regra e Olá realmente não importa. Se vir uma sequência de eliminação de restrição que contém o Olá ReplicaExclusionStatic ou ReplicaExclusionDynamic uma restrição, Olá Gestor de recursos do Cluster pensa que não nós suficientes. Isto requer que os restantes soluções toouse estes inválido possam ser posicionadas livremente que não é permitidos. Olá outras limitações na sequência de Olá normalmente nos irão dizer por que motivo nós estão a ser eliminado o aperto assegurados primeiro Olá.
* **PlacementConstraint**: Se vir esta mensagem, significa que foi eliminado o aperto alguns nós porque estes não correspondiam restrições de posicionamento do serviço de Olá. Iremos rastreio saída restrições de posicionamento de Olá atualmente configurada como parte desta mensagem. Isto é normal se tiver uma restrição de posicionamento definida. No entanto, se a restrição de posicionamento está a causar incorretamente demasiadas toobe de nós eliminado o aperto esta é a forma como iria Repare.
* **NodeCapacity**: esta restrição significa que Olá Gestor de recursos do Cluster não foi possível colocar réplicas Olá num Olá indicado nós porque que seria colocá-los através de capacidade.
* **Afinidade**: esta restrição indica que iremos não foi possível colocar a réplica Olá em nós de Olá afetado porque causaria uma violação de restrição de afinidade de Olá. Mais informações sobre a afinidade estão a ser [neste artigo](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
* **FaultDomain** e **UpgradeDomain**: esta restrição elimina nós se colocar réplica Olá Olá indicado nós causaria packing num determinado falhas ou domínio de atualização. São vários os exemplos debater esta restrição são apresentados no tópico Olá [restrições de domínio de falhas e a atualização e o comportamento resultante](service-fabric-cluster-resource-manager-cluster-description.md)
* **PreferredLocation**: normalmente não os deveriam ver esta restrição remover nós da solução de Olá, uma vez que é executada como otimização por predefinição. Olá preferencial a restrição de localização encontra-se também durante as atualizações. É utilizado toomove serviços back toowhere que estavam quando iniciar a atualização de Olá durante a atualização.

## <a name="blocklisting-nodes"></a>Blocklisting nós
Outro relatórios de Gestor de recursos do Cluster de Olá a mensagem de estado de funcionamento é quando nós são blocklisted. Pode considerar blocklisting como uma restrição temporária que é aplicada automaticamente para si. Nós obtém blocklisted registam falhas repetidas quando iniciar instâncias desse tipo de serviço. Nós são blocklisted numa base por--tipo de serviço. Um nó pode ser blocklisted para o tipo de um serviço, mas não outro. 

Verá blocklisting Iniciar muitas vezes durante o desenvolvimento: alguns erros faz com que a sua toocrash de anfitrião do serviço no arranque. Service Fabric tenta anfitrião do serviço toocreate Olá algumas vezes e falha Olá mantém a ocorrer. Após alguns tentativas, o nó de Olá obtém blocklisted e Olá Gestor de recursos do Cluster tentará toocreate serviço de Olá noutro local. Se essa falha mantém a acontecer em vários nós, é possível que todos os nós de válido Olá no final de cluster Olá cópias de segurança de bloqueado. Blocklisting pode também remover nós tantas insuficiente pode iniciar com êxito escala do Olá serviço toomeet Olá assim o desejar. Normalmente, irá ver erros adicionais ou avisos de Olá Gestor de recursos de Cluster com a indicação de que o serviço de Olá está abaixo réplica pretendido Olá ou a contagem de instâncias, bem como as mensagens de estado de funcionamento que indica que falha Olá é que origina toohello blocklisting assegurados primeiro Olá.

Blocklisting não é uma condição permanente. Após alguns minutos, o nó de Olá é removido do Olá blocklist e Service Fabric pode ativar os serviços de Olá nesse nó novamente. Se os serviços continuem toofail, o nó de Olá é novamente blocklisted para esse tipo de serviço. 

### <a name="constraint-priorities"></a>Prioridades da restrição

> [!WARNING]
> Alterar as prioridades de restrição não se recomenda e pode ter efeitos adversos significativos no seu cluster. Olá abaixo informações é fornecida para a referência de prioridades de restrição de predefinição Olá e o comportamento. 
>

Com todas as destas restrições, poderá ter sido pensar "Hei responsável pelo – julgo que restrições de domínio de falhas são coisa mais importante de Olá no meu sistema. Na ordem tooensure hello restrição de domínio de falhas não é violada, estou dispostos tooviolate outras restrições. "

Restrições podem ser configuradas com níveis de prioridade diferente. Nomeadamente:

   - "rígido" (0)
   - "soft" (1)
   - "otimização" (2)
   - "off" (-1). 
   
Na maioria das restrições de Olá está configurada como restrições de disco rígidas, por predefinição.

Alterar a prioridade de Olá restrições é invulgar. Existiram vezes onde prioridades de restrição necessários toochange, normalmente toowork em torno alguns erros ou comportamento que está a afetar ambiente Olá. Geralmente flexibilidade Olá da infraestrutura de prioridade de restrição de Olá trabalhou muito bem, mas este não é necessário frequentemente. A maioria do tempo de Olá tudo encontra-se nas respetivas prioridades da predefinição. 

níveis de prioridade de Olá não significam que uma restrição determinada _será_ ser violado, nem que será sempre ser satisfeita. Prioridades da restrição definem uma ordem na qual as restrições são aplicadas. Prioridades definem fala Olá quando é impossível toosatisfy todas as restrições. Normalmente, todas as restrições de Olá podem ser satisfeitas a menos que exista um senão passa no ambiente de Olá. Alguns exemplos de cenários que irão causar tooconstraint violações são as restrições em conflito, ou grande número de falhas em simultâneo.

Em situações avançadas, pode alterar as prioridades de restrição de Olá. Por exemplo, imagine que pretendia tooensure que afinidade sempre deverá ser violada quando emite a capacidade de nó toosolve necessário. tooachieve, foi possível definir a prioridade de Olá Olá afinidade restrição demasiado "forma recuperável" (1) e deixar Olá capacidade restrição definida demasiado "disco rígida" (0).

valores de prioridade Olá predefinidos para as restrições de diferentes Olá estão especificados na Olá a seguinte configuração:

ClusterManifest.xml

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

através de Clusterconfig para implementações autónomas ou Template do Azure alojada clusters:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a>Restrições de domínio do domínio e a atualização falha
Olá Gestor de recursos do Cluster pretende serviços tookeep distribuir entre domínios de falhas e a atualização. Modelos tal como uma restrição dentro Olá Cluster o Gestor de recursos do motor. Para obter mais informações sobre como são utilizadas e o respetivo comportamento específico, consulte o artigo de Olá no [configuração de cluster](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior).

Olá Gestor de recursos do Cluster pode ser necessário toopack alguns réplicas para um domínio de atualização na ordem toodeal com as atualizações, falhas ou outras violações de restrição. Packing em domínios de falhas ou atualização normalmente ocorre apenas quando existem várias falhas ou outro volume de alterações no sistema de Olá impedir a colocação corretas. Se desejar tooprevent packing, mesmo durante estas situações, pode utilizar Olá `RequireDomainDistribution` [política de colocação](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). Tenha em atenção que isto pode afetar a disponibilidade do serviço e a fiabilidade como efeito, por isso considere.

Se o ambiente de Olá está configurado corretamente, os todas as restrições, completamente são respeitadas, mesmo durante as atualizações. Olá chave é essa Olá Gestor de recursos de Cluster está a observar para as restrições. Quando Deteta uma violação-lo imediatamente relatórios-lo e tenta problema de Olá toocorrect.

## <a name="hello-preferred-location-constraint"></a>restrição de localização de Olá preferido
Olá PreferredLocation restrição é ligeiramente diferente, porque tem dois utiliza diferentes. É uma utilização desta restrição durante as atualizações de aplicações. Olá Gestor de recursos do Cluster gere automaticamente esta restrição durante as atualizações. É utilizado tooensure que, ao atualiza estiverem concluídas de que as réplicas devolvem tootheir localizações iniciais. Olá outra utilização de Olá PreferredLocation restrição destina Olá [ `PreferredPrimaryDomain` política de colocação](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md). Estes são otimizações, não sendo, por conseguinte, Olá PreferredLocation restrição restrição apenas Olá definida demasiado "Otimização" por predefinição.

## <a name="upgrades"></a>Atualizações
Também ajuda Olá Gestor de recursos do Cluster durante a aplicação e atualizações de cluster, durante os quais tem duas tarefas:

* Certifique-se de que existem regras de Olá do cluster de Olá não fiquem comprometidas
* Tente aceda de atualização de Olá toohelp facilmente

### <a name="keep-enforcing-hello-rules"></a>Manter a impor regras Olá
Olá coisa principal toobe em consideração é que ainda são impostas quais regras Olá – Olá strict as restrições, como restrições de posicionamento e as capacidades - durante as atualizações. Restrições de posicionamento Certifique-se de que as cargas de trabalho executam apenas em que estão autorizados a, mesmo durante as atualizações. Quando os serviços são altamente restrita, as atualizações podem demorar mais tempo. Quando o serviço de Olá ou nó de Olá está em execução no é colocada para uma atualização poderão existir algumas opções para onde pode aceder.

### <a name="smart-replacements"></a>Substituições inteligentes
Quando uma atualização é iniciado, Olá Resource Manager tira um instantâneo de disposição atual do Olá de cluster Olá. Como cada domínio de atualização estiver concluída, tenta serviços de Olá tooreturn que se encontravam em que disposição original de tootheir de domínio de atualização. Desta forma existem no máximo duas transições para um serviço durante a atualização de Olá. Existe uma movimentação fora do nó de Olá afetado e um regresse. Devolver toohow de cluster ou o serviço de Olá foi antes de atualização de Olá também garante a atualização de Olá não tem impacto esquema Olá do cluster de Olá. 

### <a name="reduced-churn"></a>Volume de alterações reduzida
Outra coisa a fazer durante atualizações é essa Olá Gestor de recursos do Cluster se desligar balanceamento. Impedir balanceamento impede reactions desnecessários toohello atualização em si, como mover serviços para nós que foram esvaziados para atualização Olá. Se a atualização de Olá em questão for uma atualização do Cluster, cluster completo Olá não é balanceado durante a atualização de Olá. Verificações de restrição permanecerá ativas, movimento apenas com base no Olá balanceamento proativa das métricas está desativado.

### <a name="buffered-capacity--upgrade"></a>Capacidade de memória intermédia & atualização
Geralmente, quer toocomplete atualização Olá, mesmo que esteja cluster Olá toofull restrita ou fechar. Gerir a capacidade de Olá do cluster de Olá é ainda mais importante durante as atualizações que o habitual. Consoante Olá número de domínios de atualização, entre 5 e 20 por cento da capacidade de têm de ser migrado como hello atualização se faz através de cluster Olá. Se o trabalho tem toogo algures. Isto é olá onde noção do [colocado na memória intermédia as capacidades](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity) é útil. Capacidade de memória intermédia é respeitada durante o funcionamento normal. Olá Gestor de recursos do Cluster pode preencher nós segurança tootheir capacidade total (a consumir memória intermédia de Olá) durante as atualizações, se necessário.

## <a name="next-steps"></a>Passos seguintes
* Partir do início de Olá e [obter uma introdução toohello Gestor de recursos de Cluster do Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
