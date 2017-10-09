---
title: Estado de funcionamento de agregados de aaaHow tooview Azure Service Fabric entidades | Microsoft Docs
description: "Descreve como ver tooquery e avaliar agregados estado de funcionamento as entidades do Azure Service Fabric, através de consultas de estado de funcionamento e consultas gerais."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a>Ver relatórios de estado de funcionamento do Service Fabric
Azure Service Fabric apresenta um [modelo de estado de funcionamento](service-fabric-health-introduction.md) com entidades de estado de funcionamento que componentes de sistema e watchdogs pode relatório local as condições que está a monitorizar. Olá [arquivo de estado de funcionamento](service-fabric-health-introduction.md#health-store) agrega todos os toodetermine de dados de estado de funcionamento se entidades estão em bom estadas.

cluster de Olá é preenchido automaticamente com os relatórios de estado de funcionamento enviados pelos componentes do sistema de Olá. Leia mais em [tootroubleshoot os relatórios de estado do sistema de utilização](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).

O Service Fabric fornece várias formas tooget Olá agregado estado de funcionamento de entidades de Olá:

* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) ou outras ferramentas de visualização
* Consultas de estado de funcionamento (através do PowerShell, API ou REST)
* Geral consultas que retorno uma lista de entidades que tenham o estado de funcionamento como uma das propriedades de Olá (através do PowerShell, API ou REST)

toodemonstrate estas opções, vamos utilizar um cluster local com cinco nós e Olá [fabric: / WordCount aplicação](http://aka.ms/servicefabric-wordcountapp). Olá **fabric: / WordCount** aplicação contém dois serviços de predefinição, um serviço com monitorização de estado do tipo `WordCountServiceType`e um serviço sem monitorização de estado do tipo `WordCountWebServiceType`. Alterar o Olá `ApplicationManifest.xml` toorequire sete réplicas de destino para serviço com estado Olá e uma partição. Porque existem apenas cinco nós num cluster de Olá, componentes do sistema Olá reportam um aviso na partição de serviço Olá porque é a contagem Olá destino.

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a>Estado de funcionamento no Service Fabric Explorer
Service Fabric Explorer proporciona uma vista visual de cluster Olá. Na imagem de Olá abaixo, pode ver que:

* Olá aplicação **fabric: / WordCount** está vermelho (na erro), porque tem um evento de erro comunicado pelo **MyWatchdog** para a propriedade Olá **disponibilidade**.
* Um dos respetivos serviços, **fabric: / WordCount/WordCountService** for amarelo (em aviso). serviço de Olá está configurado com sete réplicas e cluster Olá com cinco nós, pelo que não é possível colocar duas repicas. Apesar de não ser apresentado aqui, a partição de serviço Olá for amarela devido a um relatório do sistema de `System.FM` indicando que `Partition is below target replica or instance count`. acionadores de partição amarelo Olá Olá serviço amarelo.
* cluster de Olá é vermelho devido à aplicação Olá vermelho.

avaliação de Olá utiliza políticas predefinidas de manifesto do cluster Olá e o manifesto da aplicação. Estão a políticas strict e não tolerar qualquer falha.

Vista de cluster Olá com o Service Fabric Explorer:

![Vista de cluster Olá com o Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> Leia mais sobre [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

## <a name="health-queries"></a>Consultas de estado de funcionamento
Service Fabric expõe consultas de estado de funcionamento para cada um dos Olá suportado [tipos de entidade](service-fabric-health-introduction.md#health-entities-and-hierarchy). Pode ser acedidos através de Olá API, através de métodos em [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), cmdlets do PowerShell e REST. Estas consultas devolvem informações de estado de funcionamento completo sobre a entidade de Olá: Olá agregar o estado de funcionamento, eventos de estado de funcionamento da entidade, os Estados de funcionamento de subordinados (quando aplicável), avaliações mau estado de funcionamento (quando Olá entidade não é bom estado de funcionamento) e as estatísticas de estado de funcionamento de elementos subordinados (quando aplicável).

> [!NOTE]
> Uma entidade de estado de funcionamento é devolvida quando for povoado completamente no arquivo de estado de funcionamento de Olá. entidade Olá tem de ser Active Directory (não eliminado) e tem um relatório de sistema. As entidades principais na cadeia de hierarquia Olá também tem de ter relatórios de sistema. Se qualquer uma das seguintes condições não forem satisfeitas, o estado de funcionamento de Olá consulta devolver um [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) com [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` que mostra o motivo pelo qual a entidade de Olá não é devolvida.
>
>

consultas de estado de funcionamento de Olá tem de passar no identificador de entidade Olá, que depende do tipo de entidade Olá. consultas de Olá aceitam parâmetros de política de estado de funcionamento opcionais. Se não existem políticas de estado de funcionamento forem especificadas, Olá [políticas de estado de funcionamento](service-fabric-health-introduction.md#health-policies) do manifesto do cluster ou aplicação Olá são utilizados para avaliação. Se Olá manifestos não contém uma definição para políticas de estado de funcionamento, políticas de estado de funcionamento do Olá predefinidas são utilizadas para avaliação. políticas de estado de funcionamento do Olá predefinidas não tolerar eventuais falhas. consultas de Olá também aceitam filtros para devolver apenas elementos subordinados parciais ou eventos – Olá aqueles que respeitem Olá os filtros especificados. Filtro de outro permite excluir estatísticas de elementos subordinados Olá.

> [!NOTE]
> filtros de saída Olá são aplicados no lado do servidor de Olá, para que o tamanho de resposta de mensagem de Olá é reduzido. Recomendamos que utilize filtros de saída Olá toolimit Olá dados devolvidos, em vez de aplicam os filtros do lado do cliente de Olá.
>
>

Estado de funcionamento de uma entidade contém:

* Olá agregado estado de funcionamento da entidade de Olá. Calculado pelo arquivo de estado de funcionamento de Olá com base em relatórios de estado de funcionamento da entidade, os Estados de funcionamento de subordinados (quando aplicável) e políticas de estado de funcionamento. Leia mais sobre [avaliação de estado de funcionamento da entidade](service-fabric-health-introduction.md#health-evaluation).  
* eventos de estado de funcionamento de Olá na entidade de Olá.
* coleção de Olá dos Estados de funcionamento de todos os elementos subordinados para entidades de Olá que podem ter elementos subordinados. Estados de funcionamento de Olá contenham identificadores de entidade e Olá estado de funcionamento agregada. Estado de funcionamento completo tooget para um elemento subordinado, chamada o estado de funcionamento do Olá consulta para o tipo de entidade de subordinados Olá e passar no identificador de subordinados Olá.
* avaliações de mau estado de funcionamento Olá toohello esse ponto de relatório que acionou Estado Olá da entidade de Olá, se a entidade de Olá não está em bom estada. avaliações de Olá são recursiva, que contém avaliações do Estado de funcionamento de elementos subordinados Olá que acionou o estado de funcionamento atual. Por exemplo, um watchdog do comunicou um erro em relação a uma réplica. Estado de funcionamento da aplicação Olá mostra uma mau avaliação devido serviço mau estado de funcionamento de tooan; serviço de Olá está danificado devido a partição de tooa erro; partição de Olá está danificada devido a réplica de tooa num erro; réplica Olá está danificada devido relatório de estado de funcionamento do toohello watchdog erros.
* estatísticas de estado de funcionamento de Olá para todos os tipos de elementos subordinados de entidades Olá tem elementos subordinados. Por exemplo, o estado de funcionamento do cluster mostra o número total de Olá de aplicações, serviços, partições, as réplicas e implementar entidades no cluster de Olá. Estado de funcionamento de serviço mostra o número total de Olá de partições e réplicas em Olá especificado serviço.

## <a name="get-cluster-health"></a>Obter o estado de funcionamento do cluster
Devolve Olá estado de funcionamento da entidade de cluster Olá e contém Estados de funcionamento de Olá das aplicações e nós (subordinados do cluster de Olá). Entrada:

* Política de estado de funcionamento do cluster Olá [opcional] utilizadas nós de Olá tooevaluate e eventos de cluster Olá.
* Mapa de política de estado de funcionamento de aplicação Olá [opcional], com as políticas de estado de funcionamento de Olá utilizado toooverride Olá manifesto as políticas de aplicações.
* [Opcional] Filtros de eventos, nós e aplicações que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros). Todos os eventos, nós e aplicações são utilizadas tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.
* [Opcional] Filtre tooexclude estatísticas de estado de funcionamento.
* [Opcional] Filtrar tooinclude fabric: / as estatísticas de estado de funcionamento do sistema em Olá estatísticas de estado de funcionamento. Apenas aplicável quando Olá estatísticas de estado de funcionamento não são excluídas. Por predefinição, as estatísticas de estado de funcionamento de Olá incluem apenas as estatísticas de aplicações de utilizador e a aplicação de sistema não Olá.

### <a name="api"></a>API
tooget estado de funcionamento do cluster, crie um `FabricClient` e Olá chamada [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) método no respetivo **HealthManager**.

Olá chamada seguinte obtém o estado de funcionamento do Olá cluster:

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

Olá código seguinte obtém o estado de funcionamento do Olá cluster utilizando uma política de estado de funcionamento de cluster personalizado e filtros para nós e aplicações. Especifica que as estatísticas de estado de funcionamento de Olá incluem recursos de infraestrutura Olá: / estatísticas de sistema. Cria [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), que contém informações de entrada Olá.

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Estado de funcionamento de Olá cmdlet tooget Olá cluster [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth). Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá estado de cluster Olá é cinco nós, a aplicação de sistema de Olá e fabric: / WordCount configurado, tal como descrito.

Olá seguintes cmdlet obtém o estado de funcionamento do cluster através de políticas de estado de funcionamento de predefinição. Olá agregados estado de funcionamento é aviso, porque Olá fabric: / aplicação de WordCount está a ser aviso. Tenha em atenção a como o avaliações de mau estado de funcionamento de Olá fornecem detalhes sobre as condições de Olá que acionou o estado de funcionamento de Olá agregado.

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

Olá seguinte cmdlet do PowerShell obtém estado de funcionamento de Olá do cluster de Olá utilizando uma política de aplicação personalizada. -Filtra as únicas aplicações tooget de resultados e os nós no erro ou aviso. Como resultado, nenhum nó é devolvidos, dado que estão todos em bom Estados. Apenas Olá fabric: / filtro de aplicações de Olá respeita a aplicação WordCount. Porque a política personalizada do Olá Especifica tooconsider avisos como erros dos recursos de infraestrutura de Olá: / WordCount aplicação, aplicação Olá é avaliada como erro veio e cluster Olá.

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a>REST
Pode obter o estado de funcionamento do cluster com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.

## <a name="get-node-health"></a>Obter o estado de funcionamento do nó
Devolve Olá estado de funcionamento da entidade de um nó e contém eventos de estado de funcionamento de Olá comunicados falhas no nó de Olá. Entrada:

* Nome de nó de Olá [necessária] que identifica o nó de Olá.
* Definições de política de estado de funcionamento de cluster de Olá [opcional] utilizadas tooevaluate estado de funcionamento.
* [Opcional] Filtros para os eventos que especificam as entradas de interesse e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros). Todos os eventos são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.

### <a name="api"></a>API
Estado de funcionamento de nó de tooget através de Olá API, crie um `FabricClient` e Olá chamada [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) método no respetivo HealthManager.

Olá código seguinte obtém estado de funcionamento do Olá nó para o nome de nó especificado Olá:

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

Olá código seguinte obtém o estado de funcionamento do Olá nó para Olá especificado o nome do nó e transmite no filtro de eventos e uma política personalizada através de [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Estado de funcionamento de Olá cmdlet tooget Olá nó [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth). Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.
Olá, os seguintes cmdlet obtém o estado de funcionamento do Olá nó através de políticas de estado de funcionamento de predefinição:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Olá seguinte cmdlet obtém o estado de funcionamento de Olá de todos os nós de cluster Olá:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a>REST
Pode obter o estado de funcionamento do nó com uma [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.

## <a name="get-application-health"></a>Obter o estado de funcionamento da aplicação
Devolve Olá estado de funcionamento de uma entidade de aplicação. Contém Estados de funcionamento de Olá da aplicação Olá implementado e subordinados do serviço. Entrada:

* [Necessário] Olá nome da aplicação (URI) que identifica Olá aplicação.
* Política de estado de funcionamento de aplicação Olá [opcional] utilizado toooverride Olá manifesto as políticas de aplicações.
* [Opcional] Filtros de eventos, serviços e aplicações implementadas que especificam quais entradas são úteis e devem ser devolvidos num resultado de Olá (por exemplo, apenas, erros ou avisos e erros). Todos os eventos, serviços e aplicações implementadas são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.
* [Opcional] Filtre as estatísticas de estado de funcionamento do tooexclude Olá. Se não for especificado, as estatísticas de estado de funcionamento de Olá incluem ok Olá, aviso e contagem de erros para todos os elementos subordinados de aplicação: serviços de partições, réplicas, aplicações implementadas e implementar pacotes de serviços.

### <a name="api"></a>API
Estado de funcionamento de aplicação tooget, crie um `FabricClient` e Olá chamada [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) método no respetivo HealthManager.

Olá código seguinte obtém estado de funcionamento da aplicação Olá para o nome de aplicação especificada Olá (URI):

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

Olá código seguinte obtém estado de funcionamento da aplicação Olá para o nome de aplicação especificada Olá (URI), com os filtros e as políticas personalizadas especificado através de [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Estado de funcionamento de Olá cmdlet tooget Olá aplicação [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps). Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá seguinte cmdlet devolve o estado de funcionamento de Olá de Olá **fabric: / WordCount** aplicação:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

Olá seguir transmite de cmdlet do PowerShell em políticas personalizadas. Filtra também eventos e subordinados.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a>REST
Pode obter o estado de funcionamento de aplicação com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.

## <a name="get-service-health"></a>Obter o estado de funcionamento do serviço
Devolve Olá estado de funcionamento de uma entidade de serviço. Contém Olá Estados de funcionamento de partição. Entrada:

* Olá [necessária] nome do serviço (URI) que identifica o serviço de Olá.
* Política de estado de funcionamento de aplicação Olá [opcional] utilizada a política de manifesto da aplicação Olá toooverride.
* [Opcional] Filtros de eventos e partições que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros). Todos os eventos e as partições são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.
* [Opcional] Filtre tooexclude estatísticas de estado de funcionamento. Se não for especificado, Olá Olá de mostrar de estatísticas de estado de funcionamento ok, aviso e erro contagem de todas as partições e réplicas do serviço de Olá.

### <a name="api"></a>API
Estado de funcionamento de serviço de tooget através de Olá API, crie um `FabricClient` e Olá chamada [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) método no respetivo HealthManager.

Olá exemplo seguinte obtém Olá estado de funcionamento um serviço com o nome de serviço especificado (URI):

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

Olá código seguinte obtém Olá serviço estado de funcionamento para o nome de serviço especificado de Olá (URI), especificar os filtros e a política personalizada através de [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Estado de funcionamento de Olá cmdlet tooget Olá serviço [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth). Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá seguintes cmdlet obtém o estado de funcionamento de serviço de Olá através de políticas de estado de funcionamento de predefinição:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a>REST
Pode obter o estado de funcionamento do serviço com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.

## <a name="get-partition-health"></a>Obter o estado de funcionamento de partição
Devolve Olá estado de funcionamento de uma entidade de partição. Contém Olá Estados de funcionamento de réplica. Entrada:

* Partição de Olá [necessária] ID (GUID) que identifica a partição de Olá.
* Política de estado de funcionamento de aplicação Olá [opcional] utilizada a política de manifesto da aplicação Olá toooverride.
* [Opcional] Filtros de eventos e as réplicas que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros). Todos os eventos e as réplicas são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.
* [Opcional] Filtre tooexclude estatísticas de estado de funcionamento. Se não for especificado, as estatísticas de estado de funcionamento de Olá mostram réplicas quantos estão em ok, aviso e erro Estados.

### <a name="api"></a>API
Estado de funcionamento do tooget partição através de Olá API, crie um `FabricClient` e Olá chamada [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) método no respetivo HealthManager. os parâmetros opcionais toospecify, criar [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
Estado de funcionamento de Olá cmdlet tooget Olá partição [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth). Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá seguinte cmdlet obtém estado de funcionamento de Olá para todas as partições da Olá **fabric: / WordCount/WordCountService** serviço e os filtros de saída Estados de funcionamento de réplica:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Pode obter o estado de funcionamento de partição com uma [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.

## <a name="get-replica-health"></a>Obter o estado de funcionamento de réplica
Devolve o estado de funcionamento de Olá de uma réplica de monitorização de estado de serviço ou uma instância de serviço sem estado. Entrada:

* [Necessário] Olá ID (GUID) e de réplica ID de partição que identifica a réplica de Olá.
* Parâmetros de política de estado de funcionamento de aplicação Olá [opcional] utilizados toooverride Olá manifesto as políticas de aplicações.
* [Opcional] Filtros para os eventos que especificam as entradas de interesse e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros). Todos os eventos são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.

### <a name="api"></a>API
Estado de funcionamento do tooget Olá réplica através de Olá API, crie um `FabricClient` e Olá chamada [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) método no respetivo HealthManager. toospecify avançadas parâmetros, utilize [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
Estado de funcionamento de Olá cmdlet tooget Olá réplica [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth). Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá seguinte cmdlet obtém estado de funcionamento de Olá da réplica primária do Olá para todas as partições do serviço de Olá:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Pode obter o estado de funcionamento de réplica com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.

## <a name="get-deployed-application-health"></a>Obter o estado de funcionamento da aplicação implementada
Devolve Olá estado de funcionamento de uma aplicação implementada na entidade de um nó. Contém Estados de funcionamento de pacote de serviço Olá implementado. Entrada:

* Nome da aplicação Olá [necessária] (URI) e o nome de nó (cadeia) que identificam Olá implementar a aplicação.
* Política de estado de funcionamento de aplicação Olá [opcional] utilizado toooverride Olá manifesto as políticas de aplicações.
* [Opcional] Filtros para eventos e pacotes de serviço implementado que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros). Todos os eventos e pacotes de serviço implementado são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.
* [Opcional] Filtre tooexclude estatísticas de estado de funcionamento. Se não for especificado, estatísticas de estado de funcionamento de Olá mostram número de Olá de pacotes de serviços implementados em ok, aviso e erro Estados de funcionamento.

### <a name="api"></a>API
Estado de funcionamento do tooget Olá de uma aplicação implementada num nó através de Olá API, crie um `FabricClient` e Olá chamada [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) método no respetivo HealthManager. utilizar parâmetros opcionais toospecify, [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
Olá cmdlet tooget Olá implementado aplicação estado de funcionamento é [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps). Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. toofind saída onde está implementada uma aplicação, execute [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e implementados de vista de olhos Olá subordinados de aplicação.

Olá seguinte cmdlet obtém estado de funcionamento de Olá de Olá **fabric: / WordCount** aplicação implementada no **node_2**.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Pode obter o estado de funcionamento da aplicação implementada com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.

## <a name="get-deployed-service-package-health"></a>Obter o estado de funcionamento de pacote de serviço implementado
Devolve Olá estado de funcionamento de uma entidade de pacote de serviço implementado. Entrada:

* Nome da aplicação Olá [necessária] (URI), o nome do nó (cadeia) e nome do manifesto do serviço (cadeia) que identificam Olá implementado o pacote de serviço.
* Política de estado de funcionamento de aplicação Olá [opcional] utilizada a política de manifesto da aplicação Olá toooverride.
* [Opcional] Filtros para os eventos que especificam as entradas de interesse e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros). Todos os eventos são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.

### <a name="api"></a>API
Estado de funcionamento do tooget Olá de um pacote de serviço implementado através de Olá API, crie um `FabricClient` e Olá chamada [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) método no respetivo HealthManager. utilizar parâmetros opcionais toospecify, [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
Olá cmdlet tooget Olá implementado serviço pacote estado de funcionamento é [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth). Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. executar toosee onde uma aplicação é implementada, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e observe a aplicações de Olá implementado. toosee que os pacotes de serviço estão numa aplicação, procure em Olá implementado elementos subordinados do pacote de serviço no Olá [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) saída.

Olá seguinte cmdlet obtém estado de funcionamento de Olá de Olá **WordCountServicePkg** pacote do serviço de Olá **fabric: / WordCount** aplicação implementada no **node_2**. Olá entidade tem **System.Hosting** relatórios para ativação com êxito do pacote de serviço e o ponto de entrada e de registo do tipo de serviço com êxito.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Pode obter o estado de funcionamento do serviço implementado pacote com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.

## <a name="health-chunk-queries"></a>Consultas de segmento de estado de funcionamento
as consultas de segmento de estado de funcionamento de Olá podem devolver subordinados de cluster de múltiplos níveis (recursivamente), por filtros de entrada. Suporta filtros avançados que permitem muita flexibilidade na escolher subordinados Olá toobe devolvido. filtros de Olá podem especificar subordinados pelo identificador exclusivo Olá ou por outros os identificadores de grupos e/ou os Estados de funcionamento. Por predefinição, são incluídos, como comandos toohealth oposição ao que incluem sempre o primeiro nível subordinados sem subordinados.

Olá [consultas de estado de funcionamento](service-fabric-view-entities-aggregated-health.md#health-queries) devolvidos de apenas primeiro nível de subordinados de Olá especificado entidade por filtros necessárias. tooget Olá elementos subordinados de elementos subordinados de Olá, tem de chamar as APIs de estado de funcionamento adicional para cada entidade de interesse. Da mesma forma, tooget Olá estado de funcionamento entidades específicas, tem de chamar um Estado de funcionamento API para cada entidade pretendida. Olá avançada a filtragem de consulta de segmento permite-lhe toorequest vários itens de interesse numa consulta, minimizando o tamanho da mensagem Olá e número de Olá de mensagens.

o valor de Olá da consulta de segmento de Olá é que pode obter o estado de funcionamento para obter mais entidades de cluster (potencialmente todos os clusters entidades começando raiz necessário) numa chamada. Pode express consulta do Estado de funcionamento complexas tais como:

* Retorno apenas as aplicações num erro de e para essas aplicações incluem todos os serviços de aviso ou erro. Para serviços devolvidos, inclui todas as partições.
* Devolva apenas Olá estado de funcionamento das quatro aplicações, especificado pelos respetivos nomes.
* Devolva apenas Olá estado de funcionamento das aplicações de um tipo de aplicação desejada.
* Devolve entidades de todos os implementado num nó. Devolve todas as aplicações, todas as aplicações implementadas no nó especificado Olá e todos os pacotes de serviços de Olá implementada nesse nó.
* Devolva todas as réplicas no registo de erros. Devolve todas as aplicações, serviços, partições e réplicas apenas no registo de erros.
* Devolva todas as aplicações. Para um serviço especificado, inclui todas as partições.

Atualmente, a consulta de segmento de estado de funcionamento de Olá está exposta apenas para a entidade de cluster de Olá. Devolve um segmento de estado de funcionamento do cluster, que contém:

* Estado de funcionamento do Olá cluster agregado.
* Olá estado de funcionamento Estado segmento a lista de nós que Respeitamos a entrada de filtros.
* Olá estado de funcionamento Estado segmento lista de aplicações que Respeitamos a entrada de filtros. Cada segmento de estado de funcionamento de aplicação contém uma lista de segmentos com todos os serviços que respeitem filtros de entrada e uma lista de segmentos com todas as aplicações implementadas respeitem filtros Olá. Mesmo para Olá elementos subordinados de serviços e aplicações implementadas. Desta forma, todas as entidades no cluster de Olá podem potencialmente devolvidas se solicitado, de uma forma hierárquica.

### <a name="cluster-health-chunk-query"></a>Consulta de segmento de estado de funcionamento de cluster
Devolve Olá estado de funcionamento da entidade de cluster Olá e contém segmentos de estado de funcionamento hierárquica Olá de subordinados necessários. Entrada:

* Política de estado de funcionamento do cluster Olá [opcional] utilizadas nós de Olá tooevaluate e eventos de cluster Olá.
* Mapa de política de estado de funcionamento de aplicação Olá [opcional], com as políticas de estado de funcionamento de Olá utilizado toooverride Olá manifesto as políticas de aplicações.
* [Opcional] Filtros para nós e aplicações que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá. filtros de Olá tooan específico entidade/grupo de entidades ou tooall aplicável entidades nesse nível. lista de Olá de filtros de pode conter um gerais de filtro de e/ou filtros para entidades de toofine grão de identificadores específico devolvidos pela consulta Olá. Se estiver vazio, subordinados Olá não são devolvidos por predefinição.
  Leia mais informações sobre filtros de Olá em [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) e [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter). Olá aplicação filtros podem recursivamente especificar filtros avançados para elementos subordinados.

resultado de segmento de Olá inclui subordinados Olá que respeitem filtros Olá.

Atualmente, consulta de segmento de Olá não devolve avaliações mau estado de funcionamento ou eventos de entidade. Essa informação adicional pode ser obtida utilizando consulta Olá para Estado de funcionamento de cluster existente.

### <a name="api"></a>API
o estado de funcionamento do tooget cluster segmento, crie um `FabricClient` e Olá chamada [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) método no respetivo **HealthManager**. Pode passar no [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe políticas de estado de funcionamento e filtros avançados.

Olá código seguinte obtém segmentos de estado de funcionamento do cluster com filtros avançados.

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Estado de funcionamento de Olá cmdlet tooget Olá cluster [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk). Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá código seguinte obtém nós apenas se estiverem no registo de erros, exceto para um nó específico, o que deve sempre ser devolvido.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

Olá seguintes cmdlet obtém os segmentos de cluster com filtros de aplicação.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

Olá seguinte cmdlet devolve entidades de todos os implementado num nó.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a>REST
Pode obter o segmento de estado de funcionamento de cluster com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) que inclui políticas de estado de funcionamento e filtros avançados descritos no corpo de Olá.

## <a name="general-queries"></a>Consultas gerais
Consultas gerais devolvem uma lista de entidades do Service Fabric de um tipo especificado. Estes são expostos através da API de Olá (através de métodos de Olá em **FabricClient.QueryManager**), cmdlets do PowerShell e REST. Estas consultas agregar subconsultas de vários componentes. Uma delas é Olá [arquivo de estado de funcionamento](service-fabric-health-introduction.md#health-store), que preenche Olá agregar o estado de funcionamento para cada resultado da consulta.  

> [!NOTE]
> As consultas gerais devolvem Olá agregada o estado de funcionamento da entidade de Olá e não contêm dados de estado de funcionamento avançado. Se uma entidade não está em bom estada, pode seguir cópias de segurança com o estado de funcionamento consultas tooget todas as respetivas informações de estado de funcionamento, incluindo eventos, Estados de funcionamento de subordinados e avaliações mau estado de funcionamento.
>
>

Se as consultas gerais devolverem um Estado de funcionamento desconhecido para uma entidade, é possível que este arquivo de estado de funcionamento de Olá não tem dados completos sobre a entidade de Olá. Também é possível que um arquivo de estado de funcionamento de toohello subconsulta não foi concluída com êxito (por exemplo, Ocorreu um erro de comunicação ou arquivo de estado de funcionamento de Olá foi limitado). Siga a cópia de segurança com uma consulta do Estado de funcionamento para a entidade de Olá. Se subconsulta Olá encontrou erros transitórios, tais como problemas de rede, pode autenticar esta consulta de seguimento. -Pode também lhe irá fornecer mais detalhes do arquivo de estado de funcionamento de Olá sobre por que motivo não está exposta entidade Olá.

Olá consultas que contêm **HealthState** para entidades são:

* Lista de nó: devolve nós da lista de Olá num cluster de Olá (bloco paginado).
  * API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * PowerShell: Get-ServiceFabricNode
* Lista de aplicações: lista de Olá devolve de aplicações num cluster de Olá (bloco paginado).
  * API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * PowerShell: Get-ServiceFabricApplication
* Lista de serviço: lista de Olá devolve dos serviços de uma aplicação (bloco paginado).
  * API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * PowerShell: Get-ServiceFabricService
* Lista de partição: lista de Olá devolve de partições num serviço (bloco paginado).
  * API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * PowerShell: Get-ServiceFabricPartition
* Lista de réplica: lista de Olá devolve das réplicas numa partição (bloco paginado).
  * API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * PowerShell: Get-ServiceFabricReplica
* Implementar a lista de aplicações: lista de Olá devolve das aplicações implementadas num nó.
  * API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication
* Implementar a lista de pacote de serviço: lista de Olá devolve de pacotes do serviço numa aplicação implementada.
  * API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication

> [!NOTE]
> Algumas das consultas de Olá devolvem resultados paginados. Olá retorno das seguintes consultas-se uma lista derivada [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1). Se os resultados de Olá não se enquadram uma mensagem, é devolvida apenas uma página e um ContinuationToken que controla onde parou a enumeração. Continue toocall Olá mesmo consultar e passar no token de continuação Olá de Olá anterior tooget seguintes os resultados da consulta.
>
>

### <a name="examples"></a>Exemplos
Olá código seguinte obtém aplicações mau estado de funcionamento Olá num cluster de Olá:

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

Olá seguinte cmdlet obtém detalhes da aplicação Olá recursos de infraestrutura de Olá: / aplicação WordCount. Tenha em atenção que o estado de funcionamento é em aviso.

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

Olá seguinte cmdlet obtém serviços Olá com um Estado de funcionamento de erro:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a>Atualizações de cluster e da aplicação
Durante uma atualização monitorizada do cluster de Olá e aplicação, o Service Fabric verifica tooensure de estado de funcionamento que tudo permanece bom estado de funcionamento. Se uma entidade está danificada, avaliada através de políticas de estado de funcionamento configurado, atualização Olá aplica-se próxima ação Olá da toodetermine de políticas específicas de atualização. atualização Olá poderá estar em pausa tooallow interação do utilizador (tais como corrigir condições de erro ou alteração de políticas) ou, pode automaticamente reverter toohello versão de boa anterior.

Durante uma *cluster* atualização, pode obter o estado de atualização de cluster do Olá. Estado de atualização de Olá inclui avaliações mau estado de funcionamento, que toowhat ponto é mau estado de funcionamento no cluster de Olá. Se a atualização Olá for revertida devido a problemas de toohealth, o estado de atualização de Olá memorizou por motivos de mau estado de funcionamento último Olá. Esta informação pode ajudar os administradores a investigar o que aconteceu após a atualização de Olá revertida ou parado.

Da mesma forma, durante um *aplicação* atualização, as avaliações de mau estado de funcionamento estão contidas no estado de atualização da aplicação Olá.

Olá seguinte mostra o estado de atualização da aplicação Olá para um recurso de infraestrutura modificado: / aplicação WordCount. Um watchdog do comunicou um erro das suas réplicas. atualização de Olá está a implementar porque as verificações de estado de funcionamento de Olá não são respeitadas.

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

Saiba mais sobre Olá [atualização da aplicação de Service Fabric](service-fabric-application-upgrade.md).

## <a name="use-health-evaluations-tootroubleshoot"></a>Utilizar tootroubleshoot de avaliações de estado de funcionamento
Sempre que há um problema com o cluster de Olá ou uma aplicação, observe toopinpoint de estado de funcionamento de cluster ou aplicação Olá o que é incorreto. avaliações de mau estado de funcionamento de Olá fornecem detalhes sobre o estado de mau estado de funcionamento atual Olá accionadas. Se for necessário, pode explorar para baixo subordinados danificados entidades tooidentify Olá causa.

Por exemplo, considere uma aplicação mau estado de funcionamento porque não existe um relatório de erros das suas réplicas. Olá seguinte cmdlet do Powershell mostra avaliações Olá de mau estado de funcionamento:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

Pode observar Olá réplica tooget obter mais informações:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> Olá avaliações mau estado de funcionamento Mostrar Olá primeiro razão Olá entidade é avaliada toocurrent estado de funcionamento. Podem existir vários outros eventos que activam este estado, mas não são refletidas em avaliações de Olá. tooget obter mais informações, desagregação em Olá toofigure de entidades de estado de funcionamento enviados todos os relatórios de mau estado de funcionamento de Olá num cluster de Olá.
>
>

## <a name="next-steps"></a>Passos seguintes
[Utilizar tootroubleshoot de relatórios de estado de funcionamento do sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Adicionar relatórios de estado de funcionamento personalizados do Service Fabric](service-fabric-report-health.md)

[Como tooreport e verificação de estado de funcionamento do serviço](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Monitorizar e diagnosticar os serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Atualização da aplicação de Service Fabric](service-fabric-application-upgrade.md)
