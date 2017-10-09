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
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="40956-103">Ver relatórios de estado de funcionamento do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="40956-103">View Service Fabric health reports</span></span>
<span data-ttu-id="40956-104">Azure Service Fabric apresenta um [modelo de estado de funcionamento](service-fabric-health-introduction.md) com entidades de estado de funcionamento que componentes de sistema e watchdogs pode relatório local as condições que está a monitorizar.</span><span class="sxs-lookup"><span data-stu-id="40956-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="40956-105">Olá [arquivo de estado de funcionamento](service-fabric-health-introduction.md#health-store) agrega todos os toodetermine de dados de estado de funcionamento se entidades estão em bom estadas.</span><span class="sxs-lookup"><span data-stu-id="40956-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="40956-106">cluster de Olá é preenchido automaticamente com os relatórios de estado de funcionamento enviados pelos componentes do sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="40956-107">Leia mais em [tootroubleshoot os relatórios de estado do sistema de utilização](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="40956-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="40956-108">O Service Fabric fornece várias formas tooget Olá agregado estado de funcionamento de entidades de Olá:</span><span class="sxs-lookup"><span data-stu-id="40956-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="40956-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) ou outras ferramentas de visualização</span><span class="sxs-lookup"><span data-stu-id="40956-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="40956-110">Consultas de estado de funcionamento (através do PowerShell, API ou REST)</span><span class="sxs-lookup"><span data-stu-id="40956-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="40956-111">Geral consultas que retorno uma lista de entidades que tenham o estado de funcionamento como uma das propriedades de Olá (através do PowerShell, API ou REST)</span><span class="sxs-lookup"><span data-stu-id="40956-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="40956-112">toodemonstrate estas opções, vamos utilizar um cluster local com cinco nós e Olá [fabric: / WordCount aplicação](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="40956-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="40956-113">Olá **fabric: / WordCount** aplicação contém dois serviços de predefinição, um serviço com monitorização de estado do tipo `WordCountServiceType`e um serviço sem monitorização de estado do tipo `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="40956-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="40956-114">Alterar o Olá `ApplicationManifest.xml` toorequire sete réplicas de destino para serviço com estado Olá e uma partição.</span><span class="sxs-lookup"><span data-stu-id="40956-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="40956-115">Porque existem apenas cinco nós num cluster de Olá, componentes do sistema Olá reportam um aviso na partição de serviço Olá porque é a contagem Olá destino.</span><span class="sxs-lookup"><span data-stu-id="40956-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

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

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="40956-116">Estado de funcionamento no Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="40956-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="40956-117">Service Fabric Explorer proporciona uma vista visual de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="40956-118">Na imagem de Olá abaixo, pode ver que:</span><span class="sxs-lookup"><span data-stu-id="40956-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="40956-119">Olá aplicação **fabric: / WordCount** está vermelho (na erro), porque tem um evento de erro comunicado pelo **MyWatchdog** para a propriedade Olá **disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="40956-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="40956-120">Um dos respetivos serviços, **fabric: / WordCount/WordCountService** for amarelo (em aviso).</span><span class="sxs-lookup"><span data-stu-id="40956-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="40956-121">serviço de Olá está configurado com sete réplicas e cluster Olá com cinco nós, pelo que não é possível colocar duas repicas.</span><span class="sxs-lookup"><span data-stu-id="40956-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="40956-122">Apesar de não ser apresentado aqui, a partição de serviço Olá for amarela devido a um relatório do sistema de `System.FM` indicando que `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="40956-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="40956-123">acionadores de partição amarelo Olá Olá serviço amarelo.</span><span class="sxs-lookup"><span data-stu-id="40956-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="40956-124">cluster de Olá é vermelho devido à aplicação Olá vermelho.</span><span class="sxs-lookup"><span data-stu-id="40956-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="40956-125">avaliação de Olá utiliza políticas predefinidas de manifesto do cluster Olá e o manifesto da aplicação.</span><span class="sxs-lookup"><span data-stu-id="40956-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="40956-126">Estão a políticas strict e não tolerar qualquer falha.</span><span class="sxs-lookup"><span data-stu-id="40956-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="40956-127">Vista de cluster Olá com o Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="40956-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Vista de cluster Olá com o Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="40956-129">Leia mais sobre [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="40956-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="40956-130">Consultas de estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="40956-130">Health queries</span></span>
<span data-ttu-id="40956-131">Service Fabric expõe consultas de estado de funcionamento para cada um dos Olá suportado [tipos de entidade](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="40956-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="40956-132">Pode ser acedidos através de Olá API, através de métodos em [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), cmdlets do PowerShell e REST.</span><span class="sxs-lookup"><span data-stu-id="40956-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="40956-133">Estas consultas devolvem informações de estado de funcionamento completo sobre a entidade de Olá: Olá agregar o estado de funcionamento, eventos de estado de funcionamento da entidade, os Estados de funcionamento de subordinados (quando aplicável), avaliações mau estado de funcionamento (quando Olá entidade não é bom estado de funcionamento) e as estatísticas de estado de funcionamento de elementos subordinados (quando aplicável).</span><span class="sxs-lookup"><span data-stu-id="40956-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="40956-134">Uma entidade de estado de funcionamento é devolvida quando for povoado completamente no arquivo de estado de funcionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="40956-135">entidade Olá tem de ser Active Directory (não eliminado) e tem um relatório de sistema.</span><span class="sxs-lookup"><span data-stu-id="40956-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="40956-136">As entidades principais na cadeia de hierarquia Olá também tem de ter relatórios de sistema.</span><span class="sxs-lookup"><span data-stu-id="40956-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="40956-137">Se qualquer uma das seguintes condições não forem satisfeitas, o estado de funcionamento de Olá consulta devolver um [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) com [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` que mostra o motivo pelo qual a entidade de Olá não é devolvida.</span><span class="sxs-lookup"><span data-stu-id="40956-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="40956-138">consultas de estado de funcionamento de Olá tem de passar no identificador de entidade Olá, que depende do tipo de entidade Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="40956-139">consultas de Olá aceitam parâmetros de política de estado de funcionamento opcionais.</span><span class="sxs-lookup"><span data-stu-id="40956-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="40956-140">Se não existem políticas de estado de funcionamento forem especificadas, Olá [políticas de estado de funcionamento](service-fabric-health-introduction.md#health-policies) do manifesto do cluster ou aplicação Olá são utilizados para avaliação.</span><span class="sxs-lookup"><span data-stu-id="40956-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="40956-141">Se Olá manifestos não contém uma definição para políticas de estado de funcionamento, políticas de estado de funcionamento do Olá predefinidas são utilizadas para avaliação.</span><span class="sxs-lookup"><span data-stu-id="40956-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="40956-142">políticas de estado de funcionamento do Olá predefinidas não tolerar eventuais falhas.</span><span class="sxs-lookup"><span data-stu-id="40956-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="40956-143">consultas de Olá também aceitam filtros para devolver apenas elementos subordinados parciais ou eventos – Olá aqueles que respeitem Olá os filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="40956-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="40956-144">Filtro de outro permite excluir estatísticas de elementos subordinados Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="40956-145">filtros de saída Olá são aplicados no lado do servidor de Olá, para que o tamanho de resposta de mensagem de Olá é reduzido.</span><span class="sxs-lookup"><span data-stu-id="40956-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="40956-146">Recomendamos que utilize filtros de saída Olá toolimit Olá dados devolvidos, em vez de aplicam os filtros do lado do cliente de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="40956-147">Estado de funcionamento de uma entidade contém:</span><span class="sxs-lookup"><span data-stu-id="40956-147">An entity's health contains:</span></span>

* <span data-ttu-id="40956-148">Olá agregado estado de funcionamento da entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="40956-149">Calculado pelo arquivo de estado de funcionamento de Olá com base em relatórios de estado de funcionamento da entidade, os Estados de funcionamento de subordinados (quando aplicável) e políticas de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="40956-150">Leia mais sobre [avaliação de estado de funcionamento da entidade](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="40956-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="40956-151">eventos de estado de funcionamento de Olá na entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="40956-152">coleção de Olá dos Estados de funcionamento de todos os elementos subordinados para entidades de Olá que podem ter elementos subordinados.</span><span class="sxs-lookup"><span data-stu-id="40956-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="40956-153">Estados de funcionamento de Olá contenham identificadores de entidade e Olá estado de funcionamento agregada.</span><span class="sxs-lookup"><span data-stu-id="40956-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="40956-154">Estado de funcionamento completo tooget para um elemento subordinado, chamada o estado de funcionamento do Olá consulta para o tipo de entidade de subordinados Olá e passar no identificador de subordinados Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="40956-155">avaliações de mau estado de funcionamento Olá toohello esse ponto de relatório que acionou Estado Olá da entidade de Olá, se a entidade de Olá não está em bom estada.</span><span class="sxs-lookup"><span data-stu-id="40956-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="40956-156">avaliações de Olá são recursiva, que contém avaliações do Estado de funcionamento de elementos subordinados Olá que acionou o estado de funcionamento atual.</span><span class="sxs-lookup"><span data-stu-id="40956-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="40956-157">Por exemplo, um watchdog do comunicou um erro em relação a uma réplica.</span><span class="sxs-lookup"><span data-stu-id="40956-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="40956-158">Estado de funcionamento da aplicação Olá mostra uma mau avaliação devido serviço mau estado de funcionamento de tooan; serviço de Olá está danificado devido a partição de tooa erro; partição de Olá está danificada devido a réplica de tooa num erro; réplica Olá está danificada devido relatório de estado de funcionamento do toohello watchdog erros.</span><span class="sxs-lookup"><span data-stu-id="40956-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="40956-159">estatísticas de estado de funcionamento de Olá para todos os tipos de elementos subordinados de entidades Olá tem elementos subordinados.</span><span class="sxs-lookup"><span data-stu-id="40956-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="40956-160">Por exemplo, o estado de funcionamento do cluster mostra o número total de Olá de aplicações, serviços, partições, as réplicas e implementar entidades no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="40956-161">Estado de funcionamento de serviço mostra o número total de Olá de partições e réplicas em Olá especificado serviço.</span><span class="sxs-lookup"><span data-stu-id="40956-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="40956-162">Obter o estado de funcionamento do cluster</span><span class="sxs-lookup"><span data-stu-id="40956-162">Get cluster health</span></span>
<span data-ttu-id="40956-163">Devolve Olá estado de funcionamento da entidade de cluster Olá e contém Estados de funcionamento de Olá das aplicações e nós (subordinados do cluster de Olá).</span><span class="sxs-lookup"><span data-stu-id="40956-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="40956-164">Entrada:</span><span class="sxs-lookup"><span data-stu-id="40956-164">Input:</span></span>

* <span data-ttu-id="40956-165">Política de estado de funcionamento do cluster Olá [opcional] utilizadas nós de Olá tooevaluate e eventos de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="40956-166">Mapa de política de estado de funcionamento de aplicação Olá [opcional], com as políticas de estado de funcionamento de Olá utilizado toooverride Olá manifesto as políticas de aplicações.</span><span class="sxs-lookup"><span data-stu-id="40956-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="40956-167">[Opcional] Filtros de eventos, nós e aplicações que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="40956-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="40956-168">Todos os eventos, nós e aplicações são utilizadas tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="40956-169">[Opcional] Filtre tooexclude estatísticas de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="40956-170">[Opcional] Filtrar tooinclude fabric: / as estatísticas de estado de funcionamento do sistema em Olá estatísticas de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="40956-171">Apenas aplicável quando Olá estatísticas de estado de funcionamento não são excluídas.</span><span class="sxs-lookup"><span data-stu-id="40956-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="40956-172">Por predefinição, as estatísticas de estado de funcionamento de Olá incluem apenas as estatísticas de aplicações de utilizador e a aplicação de sistema não Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="40956-173">API</span><span class="sxs-lookup"><span data-stu-id="40956-173">API</span></span>
<span data-ttu-id="40956-174">tooget estado de funcionamento do cluster, crie um `FabricClient` e Olá chamada [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) método no respetivo **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="40956-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="40956-175">Olá chamada seguinte obtém o estado de funcionamento do Olá cluster:</span><span class="sxs-lookup"><span data-stu-id="40956-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="40956-176">Olá código seguinte obtém o estado de funcionamento do Olá cluster utilizando uma política de estado de funcionamento de cluster personalizado e filtros para nós e aplicações.</span><span class="sxs-lookup"><span data-stu-id="40956-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="40956-177">Especifica que as estatísticas de estado de funcionamento de Olá incluem recursos de infraestrutura Olá: / estatísticas de sistema.</span><span class="sxs-lookup"><span data-stu-id="40956-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="40956-178">Cria [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), que contém informações de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

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

### <a name="powershell"></a><span data-ttu-id="40956-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40956-179">PowerShell</span></span>
<span data-ttu-id="40956-180">Estado de funcionamento de Olá cmdlet tooget Olá cluster [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="40956-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="40956-181">Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40956-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="40956-182">Olá estado de cluster Olá é cinco nós, a aplicação de sistema de Olá e fabric: / WordCount configurado, tal como descrito.</span><span class="sxs-lookup"><span data-stu-id="40956-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="40956-183">Olá seguintes cmdlet obtém o estado de funcionamento do cluster através de políticas de estado de funcionamento de predefinição.</span><span class="sxs-lookup"><span data-stu-id="40956-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="40956-184">Olá agregados estado de funcionamento é aviso, porque Olá fabric: / aplicação de WordCount está a ser aviso.</span><span class="sxs-lookup"><span data-stu-id="40956-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="40956-185">Tenha em atenção a como o avaliações de mau estado de funcionamento de Olá fornecem detalhes sobre as condições de Olá que acionou o estado de funcionamento de Olá agregado.</span><span class="sxs-lookup"><span data-stu-id="40956-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

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

<span data-ttu-id="40956-186">Olá seguinte cmdlet do PowerShell obtém estado de funcionamento de Olá do cluster de Olá utilizando uma política de aplicação personalizada.</span><span class="sxs-lookup"><span data-stu-id="40956-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="40956-187">-Filtra as únicas aplicações tooget de resultados e os nós no erro ou aviso.</span><span class="sxs-lookup"><span data-stu-id="40956-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="40956-188">Como resultado, nenhum nó é devolvidos, dado que estão todos em bom Estados.</span><span class="sxs-lookup"><span data-stu-id="40956-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="40956-189">Apenas Olá fabric: / filtro de aplicações de Olá respeita a aplicação WordCount.</span><span class="sxs-lookup"><span data-stu-id="40956-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="40956-190">Porque a política personalizada do Olá Especifica tooconsider avisos como erros dos recursos de infraestrutura de Olá: / WordCount aplicação, aplicação Olá é avaliada como erro veio e cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

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

### <a name="rest"></a><span data-ttu-id="40956-191">REST</span><span class="sxs-lookup"><span data-stu-id="40956-191">REST</span></span>
<span data-ttu-id="40956-192">Pode obter o estado de funcionamento do cluster com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="40956-193">Obter o estado de funcionamento do nó</span><span class="sxs-lookup"><span data-stu-id="40956-193">Get node health</span></span>
<span data-ttu-id="40956-194">Devolve Olá estado de funcionamento da entidade de um nó e contém eventos de estado de funcionamento de Olá comunicados falhas no nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="40956-195">Entrada:</span><span class="sxs-lookup"><span data-stu-id="40956-195">Input:</span></span>

* <span data-ttu-id="40956-196">Nome de nó de Olá [necessária] que identifica o nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="40956-197">Definições de política de estado de funcionamento de cluster de Olá [opcional] utilizadas tooevaluate estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="40956-198">[Opcional] Filtros para os eventos que especificam as entradas de interesse e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="40956-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="40956-199">Todos os eventos são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="40956-200">API</span><span class="sxs-lookup"><span data-stu-id="40956-200">API</span></span>
<span data-ttu-id="40956-201">Estado de funcionamento de nó de tooget através de Olá API, crie um `FabricClient` e Olá chamada [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) método no respetivo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="40956-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="40956-202">Olá código seguinte obtém estado de funcionamento do Olá nó para o nome de nó especificado Olá:</span><span class="sxs-lookup"><span data-stu-id="40956-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="40956-203">Olá código seguinte obtém o estado de funcionamento do Olá nó para Olá especificado o nome do nó e transmite no filtro de eventos e uma política personalizada através de [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="40956-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="40956-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40956-204">PowerShell</span></span>
<span data-ttu-id="40956-205">Estado de funcionamento de Olá cmdlet tooget Olá nó [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="40956-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="40956-206">Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40956-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="40956-207">Olá, os seguintes cmdlet obtém o estado de funcionamento do Olá nó através de políticas de estado de funcionamento de predefinição:</span><span class="sxs-lookup"><span data-stu-id="40956-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

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

<span data-ttu-id="40956-208">Olá seguinte cmdlet obtém o estado de funcionamento de Olá de todos os nós de cluster Olá:</span><span class="sxs-lookup"><span data-stu-id="40956-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

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

### <a name="rest"></a><span data-ttu-id="40956-209">REST</span><span class="sxs-lookup"><span data-stu-id="40956-209">REST</span></span>
<span data-ttu-id="40956-210">Pode obter o estado de funcionamento do nó com uma [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="40956-211">Obter o estado de funcionamento da aplicação</span><span class="sxs-lookup"><span data-stu-id="40956-211">Get application health</span></span>
<span data-ttu-id="40956-212">Devolve Olá estado de funcionamento de uma entidade de aplicação.</span><span class="sxs-lookup"><span data-stu-id="40956-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="40956-213">Contém Estados de funcionamento de Olá da aplicação Olá implementado e subordinados do serviço.</span><span class="sxs-lookup"><span data-stu-id="40956-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="40956-214">Entrada:</span><span class="sxs-lookup"><span data-stu-id="40956-214">Input:</span></span>

* <span data-ttu-id="40956-215">[Necessário] Olá nome da aplicação (URI) que identifica Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="40956-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="40956-216">Política de estado de funcionamento de aplicação Olá [opcional] utilizado toooverride Olá manifesto as políticas de aplicações.</span><span class="sxs-lookup"><span data-stu-id="40956-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="40956-217">[Opcional] Filtros de eventos, serviços e aplicações implementadas que especificam quais entradas são úteis e devem ser devolvidos num resultado de Olá (por exemplo, apenas, erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="40956-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="40956-218">Todos os eventos, serviços e aplicações implementadas são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="40956-219">[Opcional] Filtre as estatísticas de estado de funcionamento do tooexclude Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="40956-220">Se não for especificado, as estatísticas de estado de funcionamento de Olá incluem ok Olá, aviso e contagem de erros para todos os elementos subordinados de aplicação: serviços de partições, réplicas, aplicações implementadas e implementar pacotes de serviços.</span><span class="sxs-lookup"><span data-stu-id="40956-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="40956-221">API</span><span class="sxs-lookup"><span data-stu-id="40956-221">API</span></span>
<span data-ttu-id="40956-222">Estado de funcionamento de aplicação tooget, crie um `FabricClient` e Olá chamada [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) método no respetivo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="40956-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="40956-223">Olá código seguinte obtém estado de funcionamento da aplicação Olá para o nome de aplicação especificada Olá (URI):</span><span class="sxs-lookup"><span data-stu-id="40956-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="40956-224">Olá código seguinte obtém estado de funcionamento da aplicação Olá para o nome de aplicação especificada Olá (URI), com os filtros e as políticas personalizadas especificado através de [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="40956-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

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

### <a name="powershell"></a><span data-ttu-id="40956-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40956-225">PowerShell</span></span>
<span data-ttu-id="40956-226">Estado de funcionamento de Olá cmdlet tooget Olá aplicação [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="40956-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="40956-227">Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40956-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="40956-228">Olá seguinte cmdlet devolve o estado de funcionamento de Olá de Olá **fabric: / WordCount** aplicação:</span><span class="sxs-lookup"><span data-stu-id="40956-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

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

<span data-ttu-id="40956-229">Olá seguir transmite de cmdlet do PowerShell em políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="40956-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="40956-230">Filtra também eventos e subordinados.</span><span class="sxs-lookup"><span data-stu-id="40956-230">It also filters children and events.</span></span>

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

### <a name="rest"></a><span data-ttu-id="40956-231">REST</span><span class="sxs-lookup"><span data-stu-id="40956-231">REST</span></span>
<span data-ttu-id="40956-232">Pode obter o estado de funcionamento de aplicação com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="40956-233">Obter o estado de funcionamento do serviço</span><span class="sxs-lookup"><span data-stu-id="40956-233">Get service health</span></span>
<span data-ttu-id="40956-234">Devolve Olá estado de funcionamento de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="40956-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="40956-235">Contém Olá Estados de funcionamento de partição.</span><span class="sxs-lookup"><span data-stu-id="40956-235">It contains hello partition health states.</span></span> <span data-ttu-id="40956-236">Entrada:</span><span class="sxs-lookup"><span data-stu-id="40956-236">Input:</span></span>

* <span data-ttu-id="40956-237">Olá [necessária] nome do serviço (URI) que identifica o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="40956-238">Política de estado de funcionamento de aplicação Olá [opcional] utilizada a política de manifesto da aplicação Olá toooverride.</span><span class="sxs-lookup"><span data-stu-id="40956-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="40956-239">[Opcional] Filtros de eventos e partições que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="40956-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="40956-240">Todos os eventos e as partições são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="40956-241">[Opcional] Filtre tooexclude estatísticas de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="40956-242">Se não for especificado, Olá Olá de mostrar de estatísticas de estado de funcionamento ok, aviso e erro contagem de todas as partições e réplicas do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="40956-243">API</span><span class="sxs-lookup"><span data-stu-id="40956-243">API</span></span>
<span data-ttu-id="40956-244">Estado de funcionamento de serviço de tooget através de Olá API, crie um `FabricClient` e Olá chamada [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) método no respetivo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="40956-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="40956-245">Olá exemplo seguinte obtém Olá estado de funcionamento um serviço com o nome de serviço especificado (URI):</span><span class="sxs-lookup"><span data-stu-id="40956-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="40956-246">Olá código seguinte obtém Olá serviço estado de funcionamento para o nome de serviço especificado de Olá (URI), especificar os filtros e a política personalizada através de [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="40956-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="40956-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40956-247">PowerShell</span></span>
<span data-ttu-id="40956-248">Estado de funcionamento de Olá cmdlet tooget Olá serviço [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="40956-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="40956-249">Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40956-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="40956-250">Olá seguintes cmdlet obtém o estado de funcionamento de serviço de Olá através de políticas de estado de funcionamento de predefinição:</span><span class="sxs-lookup"><span data-stu-id="40956-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

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

### <a name="rest"></a><span data-ttu-id="40956-251">REST</span><span class="sxs-lookup"><span data-stu-id="40956-251">REST</span></span>
<span data-ttu-id="40956-252">Pode obter o estado de funcionamento do serviço com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="40956-253">Obter o estado de funcionamento de partição</span><span class="sxs-lookup"><span data-stu-id="40956-253">Get partition health</span></span>
<span data-ttu-id="40956-254">Devolve Olá estado de funcionamento de uma entidade de partição.</span><span class="sxs-lookup"><span data-stu-id="40956-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="40956-255">Contém Olá Estados de funcionamento de réplica.</span><span class="sxs-lookup"><span data-stu-id="40956-255">It contains hello replica health states.</span></span> <span data-ttu-id="40956-256">Entrada:</span><span class="sxs-lookup"><span data-stu-id="40956-256">Input:</span></span>

* <span data-ttu-id="40956-257">Partição de Olá [necessária] ID (GUID) que identifica a partição de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="40956-258">Política de estado de funcionamento de aplicação Olá [opcional] utilizada a política de manifesto da aplicação Olá toooverride.</span><span class="sxs-lookup"><span data-stu-id="40956-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="40956-259">[Opcional] Filtros de eventos e as réplicas que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="40956-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="40956-260">Todos os eventos e as réplicas são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="40956-261">[Opcional] Filtre tooexclude estatísticas de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="40956-262">Se não for especificado, as estatísticas de estado de funcionamento de Olá mostram réplicas quantos estão em ok, aviso e erro Estados.</span><span class="sxs-lookup"><span data-stu-id="40956-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="40956-263">API</span><span class="sxs-lookup"><span data-stu-id="40956-263">API</span></span>
<span data-ttu-id="40956-264">Estado de funcionamento do tooget partição através de Olá API, crie um `FabricClient` e Olá chamada [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) método no respetivo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="40956-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="40956-265">os parâmetros opcionais toospecify, criar [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="40956-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="40956-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40956-266">PowerShell</span></span>
<span data-ttu-id="40956-267">Estado de funcionamento de Olá cmdlet tooget Olá partição [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="40956-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="40956-268">Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40956-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="40956-269">Olá seguinte cmdlet obtém estado de funcionamento de Olá para todas as partições da Olá **fabric: / WordCount/WordCountService** serviço e os filtros de saída Estados de funcionamento de réplica:</span><span class="sxs-lookup"><span data-stu-id="40956-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

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

### <a name="rest"></a><span data-ttu-id="40956-270">REST</span><span class="sxs-lookup"><span data-stu-id="40956-270">REST</span></span>
<span data-ttu-id="40956-271">Pode obter o estado de funcionamento de partição com uma [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="40956-272">Obter o estado de funcionamento de réplica</span><span class="sxs-lookup"><span data-stu-id="40956-272">Get replica health</span></span>
<span data-ttu-id="40956-273">Devolve o estado de funcionamento de Olá de uma réplica de monitorização de estado de serviço ou uma instância de serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="40956-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="40956-274">Entrada:</span><span class="sxs-lookup"><span data-stu-id="40956-274">Input:</span></span>

* <span data-ttu-id="40956-275">[Necessário] Olá ID (GUID) e de réplica ID de partição que identifica a réplica de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="40956-276">Parâmetros de política de estado de funcionamento de aplicação Olá [opcional] utilizados toooverride Olá manifesto as políticas de aplicações.</span><span class="sxs-lookup"><span data-stu-id="40956-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="40956-277">[Opcional] Filtros para os eventos que especificam as entradas de interesse e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="40956-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="40956-278">Todos os eventos são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="40956-279">API</span><span class="sxs-lookup"><span data-stu-id="40956-279">API</span></span>
<span data-ttu-id="40956-280">Estado de funcionamento do tooget Olá réplica através de Olá API, crie um `FabricClient` e Olá chamada [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) método no respetivo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="40956-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="40956-281">toospecify avançadas parâmetros, utilize [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="40956-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="40956-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40956-282">PowerShell</span></span>
<span data-ttu-id="40956-283">Estado de funcionamento de Olá cmdlet tooget Olá réplica [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="40956-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="40956-284">Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40956-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="40956-285">Olá seguinte cmdlet obtém estado de funcionamento de Olá da réplica primária do Olá para todas as partições do serviço de Olá:</span><span class="sxs-lookup"><span data-stu-id="40956-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

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

### <a name="rest"></a><span data-ttu-id="40956-286">REST</span><span class="sxs-lookup"><span data-stu-id="40956-286">REST</span></span>
<span data-ttu-id="40956-287">Pode obter o estado de funcionamento de réplica com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="40956-288">Obter o estado de funcionamento da aplicação implementada</span><span class="sxs-lookup"><span data-stu-id="40956-288">Get deployed application health</span></span>
<span data-ttu-id="40956-289">Devolve Olá estado de funcionamento de uma aplicação implementada na entidade de um nó.</span><span class="sxs-lookup"><span data-stu-id="40956-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="40956-290">Contém Estados de funcionamento de pacote de serviço Olá implementado.</span><span class="sxs-lookup"><span data-stu-id="40956-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="40956-291">Entrada:</span><span class="sxs-lookup"><span data-stu-id="40956-291">Input:</span></span>

* <span data-ttu-id="40956-292">Nome da aplicação Olá [necessária] (URI) e o nome de nó (cadeia) que identificam Olá implementar a aplicação.</span><span class="sxs-lookup"><span data-stu-id="40956-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="40956-293">Política de estado de funcionamento de aplicação Olá [opcional] utilizado toooverride Olá manifesto as políticas de aplicações.</span><span class="sxs-lookup"><span data-stu-id="40956-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="40956-294">[Opcional] Filtros para eventos e pacotes de serviço implementado que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="40956-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="40956-295">Todos os eventos e pacotes de serviço implementado são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="40956-296">[Opcional] Filtre tooexclude estatísticas de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="40956-297">Se não for especificado, estatísticas de estado de funcionamento de Olá mostram número de Olá de pacotes de serviços implementados em ok, aviso e erro Estados de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="40956-298">API</span><span class="sxs-lookup"><span data-stu-id="40956-298">API</span></span>
<span data-ttu-id="40956-299">Estado de funcionamento do tooget Olá de uma aplicação implementada num nó através de Olá API, crie um `FabricClient` e Olá chamada [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) método no respetivo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="40956-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="40956-300">utilizar parâmetros opcionais toospecify, [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="40956-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="40956-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40956-301">PowerShell</span></span>
<span data-ttu-id="40956-302">Olá cmdlet tooget Olá implementado aplicação estado de funcionamento é [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="40956-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="40956-303">Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40956-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="40956-304">toofind saída onde está implementada uma aplicação, execute [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e implementados de vista de olhos Olá subordinados de aplicação.</span><span class="sxs-lookup"><span data-stu-id="40956-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="40956-305">Olá seguinte cmdlet obtém estado de funcionamento de Olá de Olá **fabric: / WordCount** aplicação implementada no **node_2**.</span><span class="sxs-lookup"><span data-stu-id="40956-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

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

### <a name="rest"></a><span data-ttu-id="40956-306">REST</span><span class="sxs-lookup"><span data-stu-id="40956-306">REST</span></span>
<span data-ttu-id="40956-307">Pode obter o estado de funcionamento da aplicação implementada com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="40956-308">Obter o estado de funcionamento de pacote de serviço implementado</span><span class="sxs-lookup"><span data-stu-id="40956-308">Get deployed service package health</span></span>
<span data-ttu-id="40956-309">Devolve Olá estado de funcionamento de uma entidade de pacote de serviço implementado.</span><span class="sxs-lookup"><span data-stu-id="40956-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="40956-310">Entrada:</span><span class="sxs-lookup"><span data-stu-id="40956-310">Input:</span></span>

* <span data-ttu-id="40956-311">Nome da aplicação Olá [necessária] (URI), o nome do nó (cadeia) e nome do manifesto do serviço (cadeia) que identificam Olá implementado o pacote de serviço.</span><span class="sxs-lookup"><span data-stu-id="40956-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="40956-312">Política de estado de funcionamento de aplicação Olá [opcional] utilizada a política de manifesto da aplicação Olá toooverride.</span><span class="sxs-lookup"><span data-stu-id="40956-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="40956-313">[Opcional] Filtros para os eventos que especificam as entradas de interesse e devem ser devolvidas num resultado de Olá (por exemplo, apenas, erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="40956-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="40956-314">Todos os eventos são utilizados tooevaluate Olá entidade agregado estado de funcionamento, independentemente do filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="40956-315">API</span><span class="sxs-lookup"><span data-stu-id="40956-315">API</span></span>
<span data-ttu-id="40956-316">Estado de funcionamento do tooget Olá de um pacote de serviço implementado através de Olá API, crie um `FabricClient` e Olá chamada [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) método no respetivo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="40956-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="40956-317">utilizar parâmetros opcionais toospecify, [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="40956-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="40956-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40956-318">PowerShell</span></span>
<span data-ttu-id="40956-319">Olá cmdlet tooget Olá implementado serviço pacote estado de funcionamento é [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="40956-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="40956-320">Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40956-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="40956-321">executar toosee onde uma aplicação é implementada, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e observe a aplicações de Olá implementado.</span><span class="sxs-lookup"><span data-stu-id="40956-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="40956-322">toosee que os pacotes de serviço estão numa aplicação, procure em Olá implementado elementos subordinados do pacote de serviço no Olá [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) saída.</span><span class="sxs-lookup"><span data-stu-id="40956-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="40956-323">Olá seguinte cmdlet obtém estado de funcionamento de Olá de Olá **WordCountServicePkg** pacote do serviço de Olá **fabric: / WordCount** aplicação implementada no **node_2**.</span><span class="sxs-lookup"><span data-stu-id="40956-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="40956-324">Olá entidade tem **System.Hosting** relatórios para ativação com êxito do pacote de serviço e o ponto de entrada e de registo do tipo de serviço com êxito.</span><span class="sxs-lookup"><span data-stu-id="40956-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

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

### <a name="rest"></a><span data-ttu-id="40956-325">REST</span><span class="sxs-lookup"><span data-stu-id="40956-325">REST</span></span>
<span data-ttu-id="40956-326">Pode obter o estado de funcionamento do serviço implementado pacote com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) que inclui as políticas de estado de funcionamento descritas no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="40956-327">Consultas de segmento de estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="40956-327">Health chunk queries</span></span>
<span data-ttu-id="40956-328">as consultas de segmento de estado de funcionamento de Olá podem devolver subordinados de cluster de múltiplos níveis (recursivamente), por filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="40956-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="40956-329">Suporta filtros avançados que permitem muita flexibilidade na escolher subordinados Olá toobe devolvido.</span><span class="sxs-lookup"><span data-stu-id="40956-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="40956-330">filtros de Olá podem especificar subordinados pelo identificador exclusivo Olá ou por outros os identificadores de grupos e/ou os Estados de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="40956-331">Por predefinição, são incluídos, como comandos toohealth oposição ao que incluem sempre o primeiro nível subordinados sem subordinados.</span><span class="sxs-lookup"><span data-stu-id="40956-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="40956-332">Olá [consultas de estado de funcionamento](service-fabric-view-entities-aggregated-health.md#health-queries) devolvidos de apenas primeiro nível de subordinados de Olá especificado entidade por filtros necessárias.</span><span class="sxs-lookup"><span data-stu-id="40956-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="40956-333">tooget Olá elementos subordinados de elementos subordinados de Olá, tem de chamar as APIs de estado de funcionamento adicional para cada entidade de interesse.</span><span class="sxs-lookup"><span data-stu-id="40956-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="40956-334">Da mesma forma, tooget Olá estado de funcionamento entidades específicas, tem de chamar um Estado de funcionamento API para cada entidade pretendida.</span><span class="sxs-lookup"><span data-stu-id="40956-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="40956-335">Olá avançada a filtragem de consulta de segmento permite-lhe toorequest vários itens de interesse numa consulta, minimizando o tamanho da mensagem Olá e número de Olá de mensagens.</span><span class="sxs-lookup"><span data-stu-id="40956-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="40956-336">o valor de Olá da consulta de segmento de Olá é que pode obter o estado de funcionamento para obter mais entidades de cluster (potencialmente todos os clusters entidades começando raiz necessário) numa chamada.</span><span class="sxs-lookup"><span data-stu-id="40956-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="40956-337">Pode express consulta do Estado de funcionamento complexas tais como:</span><span class="sxs-lookup"><span data-stu-id="40956-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="40956-338">Retorno apenas as aplicações num erro de e para essas aplicações incluem todos os serviços de aviso ou erro.</span><span class="sxs-lookup"><span data-stu-id="40956-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="40956-339">Para serviços devolvidos, inclui todas as partições.</span><span class="sxs-lookup"><span data-stu-id="40956-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="40956-340">Devolva apenas Olá estado de funcionamento das quatro aplicações, especificado pelos respetivos nomes.</span><span class="sxs-lookup"><span data-stu-id="40956-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="40956-341">Devolva apenas Olá estado de funcionamento das aplicações de um tipo de aplicação desejada.</span><span class="sxs-lookup"><span data-stu-id="40956-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="40956-342">Devolve entidades de todos os implementado num nó.</span><span class="sxs-lookup"><span data-stu-id="40956-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="40956-343">Devolve todas as aplicações, todas as aplicações implementadas no nó especificado Olá e todos os pacotes de serviços de Olá implementada nesse nó.</span><span class="sxs-lookup"><span data-stu-id="40956-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="40956-344">Devolva todas as réplicas no registo de erros.</span><span class="sxs-lookup"><span data-stu-id="40956-344">Return all replicas in error.</span></span> <span data-ttu-id="40956-345">Devolve todas as aplicações, serviços, partições e réplicas apenas no registo de erros.</span><span class="sxs-lookup"><span data-stu-id="40956-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="40956-346">Devolva todas as aplicações.</span><span class="sxs-lookup"><span data-stu-id="40956-346">Return all applications.</span></span> <span data-ttu-id="40956-347">Para um serviço especificado, inclui todas as partições.</span><span class="sxs-lookup"><span data-stu-id="40956-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="40956-348">Atualmente, a consulta de segmento de estado de funcionamento de Olá está exposta apenas para a entidade de cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="40956-349">Devolve um segmento de estado de funcionamento do cluster, que contém:</span><span class="sxs-lookup"><span data-stu-id="40956-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="40956-350">Estado de funcionamento do Olá cluster agregado.</span><span class="sxs-lookup"><span data-stu-id="40956-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="40956-351">Olá estado de funcionamento Estado segmento a lista de nós que Respeitamos a entrada de filtros.</span><span class="sxs-lookup"><span data-stu-id="40956-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="40956-352">Olá estado de funcionamento Estado segmento lista de aplicações que Respeitamos a entrada de filtros.</span><span class="sxs-lookup"><span data-stu-id="40956-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="40956-353">Cada segmento de estado de funcionamento de aplicação contém uma lista de segmentos com todos os serviços que respeitem filtros de entrada e uma lista de segmentos com todas as aplicações implementadas respeitem filtros Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="40956-354">Mesmo para Olá elementos subordinados de serviços e aplicações implementadas.</span><span class="sxs-lookup"><span data-stu-id="40956-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="40956-355">Desta forma, todas as entidades no cluster de Olá podem potencialmente devolvidas se solicitado, de uma forma hierárquica.</span><span class="sxs-lookup"><span data-stu-id="40956-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="40956-356">Consulta de segmento de estado de funcionamento de cluster</span><span class="sxs-lookup"><span data-stu-id="40956-356">Cluster health chunk query</span></span>
<span data-ttu-id="40956-357">Devolve Olá estado de funcionamento da entidade de cluster Olá e contém segmentos de estado de funcionamento hierárquica Olá de subordinados necessários.</span><span class="sxs-lookup"><span data-stu-id="40956-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="40956-358">Entrada:</span><span class="sxs-lookup"><span data-stu-id="40956-358">Input:</span></span>

* <span data-ttu-id="40956-359">Política de estado de funcionamento do cluster Olá [opcional] utilizadas nós de Olá tooevaluate e eventos de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="40956-360">Mapa de política de estado de funcionamento de aplicação Olá [opcional], com as políticas de estado de funcionamento de Olá utilizado toooverride Olá manifesto as políticas de aplicações.</span><span class="sxs-lookup"><span data-stu-id="40956-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="40956-361">[Opcional] Filtros para nós e aplicações que especificam quais entradas são úteis e devem ser devolvidas num resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="40956-362">filtros de Olá tooan específico entidade/grupo de entidades ou tooall aplicável entidades nesse nível.</span><span class="sxs-lookup"><span data-stu-id="40956-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="40956-363">lista de Olá de filtros de pode conter um gerais de filtro de e/ou filtros para entidades de toofine grão de identificadores específico devolvidos pela consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="40956-364">Se estiver vazio, subordinados Olá não são devolvidos por predefinição.</span><span class="sxs-lookup"><span data-stu-id="40956-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="40956-365">Leia mais informações sobre filtros de Olá em [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) e [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="40956-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="40956-366">Olá aplicação filtros podem recursivamente especificar filtros avançados para elementos subordinados.</span><span class="sxs-lookup"><span data-stu-id="40956-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="40956-367">resultado de segmento de Olá inclui subordinados Olá que respeitem filtros Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="40956-368">Atualmente, consulta de segmento de Olá não devolve avaliações mau estado de funcionamento ou eventos de entidade.</span><span class="sxs-lookup"><span data-stu-id="40956-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="40956-369">Essa informação adicional pode ser obtida utilizando consulta Olá para Estado de funcionamento de cluster existente.</span><span class="sxs-lookup"><span data-stu-id="40956-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="40956-370">API</span><span class="sxs-lookup"><span data-stu-id="40956-370">API</span></span>
<span data-ttu-id="40956-371">o estado de funcionamento do tooget cluster segmento, crie um `FabricClient` e Olá chamada [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) método no respetivo **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="40956-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="40956-372">Pode passar no [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe políticas de estado de funcionamento e filtros avançados.</span><span class="sxs-lookup"><span data-stu-id="40956-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="40956-373">Olá código seguinte obtém segmentos de estado de funcionamento do cluster com filtros avançados.</span><span class="sxs-lookup"><span data-stu-id="40956-373">hello following code gets cluster health chunk with advanced filters.</span></span>

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

### <a name="powershell"></a><span data-ttu-id="40956-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40956-374">PowerShell</span></span>
<span data-ttu-id="40956-375">Estado de funcionamento de Olá cmdlet tooget Olá cluster [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="40956-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="40956-376">Em primeiro lugar, ligue o cluster de toohello utilizando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40956-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="40956-377">Olá código seguinte obtém nós apenas se estiverem no registo de erros, exceto para um nó específico, o que deve sempre ser devolvido.</span><span class="sxs-lookup"><span data-stu-id="40956-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

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

<span data-ttu-id="40956-378">Olá seguintes cmdlet obtém os segmentos de cluster com filtros de aplicação.</span><span class="sxs-lookup"><span data-stu-id="40956-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

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

<span data-ttu-id="40956-379">Olá seguinte cmdlet devolve entidades de todos os implementado num nó.</span><span class="sxs-lookup"><span data-stu-id="40956-379">hello following cmdlet returns all deployed entities on a node.</span></span>

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

### <a name="rest"></a><span data-ttu-id="40956-380">REST</span><span class="sxs-lookup"><span data-stu-id="40956-380">REST</span></span>
<span data-ttu-id="40956-381">Pode obter o segmento de estado de funcionamento de cluster com um [pedido GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) ou um [pedido POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) que inclui políticas de estado de funcionamento e filtros avançados descritos no corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="40956-382">Consultas gerais</span><span class="sxs-lookup"><span data-stu-id="40956-382">General queries</span></span>
<span data-ttu-id="40956-383">Consultas gerais devolvem uma lista de entidades do Service Fabric de um tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="40956-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="40956-384">Estes são expostos através da API de Olá (através de métodos de Olá em **FabricClient.QueryManager**), cmdlets do PowerShell e REST.</span><span class="sxs-lookup"><span data-stu-id="40956-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="40956-385">Estas consultas agregar subconsultas de vários componentes.</span><span class="sxs-lookup"><span data-stu-id="40956-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="40956-386">Uma delas é Olá [arquivo de estado de funcionamento](service-fabric-health-introduction.md#health-store), que preenche Olá agregar o estado de funcionamento para cada resultado da consulta.</span><span class="sxs-lookup"><span data-stu-id="40956-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="40956-387">As consultas gerais devolvem Olá agregada o estado de funcionamento da entidade de Olá e não contêm dados de estado de funcionamento avançado.</span><span class="sxs-lookup"><span data-stu-id="40956-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="40956-388">Se uma entidade não está em bom estada, pode seguir cópias de segurança com o estado de funcionamento consultas tooget todas as respetivas informações de estado de funcionamento, incluindo eventos, Estados de funcionamento de subordinados e avaliações mau estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="40956-389">Se as consultas gerais devolverem um Estado de funcionamento desconhecido para uma entidade, é possível que este arquivo de estado de funcionamento de Olá não tem dados completos sobre a entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="40956-390">Também é possível que um arquivo de estado de funcionamento de toohello subconsulta não foi concluída com êxito (por exemplo, Ocorreu um erro de comunicação ou arquivo de estado de funcionamento de Olá foi limitado).</span><span class="sxs-lookup"><span data-stu-id="40956-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="40956-391">Siga a cópia de segurança com uma consulta do Estado de funcionamento para a entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="40956-392">Se subconsulta Olá encontrou erros transitórios, tais como problemas de rede, pode autenticar esta consulta de seguimento.</span><span class="sxs-lookup"><span data-stu-id="40956-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="40956-393">-Pode também lhe irá fornecer mais detalhes do arquivo de estado de funcionamento de Olá sobre por que motivo não está exposta entidade Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="40956-394">Olá consultas que contêm **HealthState** para entidades são:</span><span class="sxs-lookup"><span data-stu-id="40956-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="40956-395">Lista de nó: devolve nós da lista de Olá num cluster de Olá (bloco paginado).</span><span class="sxs-lookup"><span data-stu-id="40956-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="40956-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="40956-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="40956-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="40956-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="40956-398">Lista de aplicações: lista de Olá devolve de aplicações num cluster de Olá (bloco paginado).</span><span class="sxs-lookup"><span data-stu-id="40956-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="40956-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="40956-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="40956-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="40956-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="40956-401">Lista de serviço: lista de Olá devolve dos serviços de uma aplicação (bloco paginado).</span><span class="sxs-lookup"><span data-stu-id="40956-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="40956-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="40956-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="40956-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="40956-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="40956-404">Lista de partição: lista de Olá devolve de partições num serviço (bloco paginado).</span><span class="sxs-lookup"><span data-stu-id="40956-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="40956-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="40956-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="40956-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="40956-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="40956-407">Lista de réplica: lista de Olá devolve das réplicas numa partição (bloco paginado).</span><span class="sxs-lookup"><span data-stu-id="40956-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="40956-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="40956-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="40956-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="40956-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="40956-410">Implementar a lista de aplicações: lista de Olá devolve das aplicações implementadas num nó.</span><span class="sxs-lookup"><span data-stu-id="40956-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="40956-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="40956-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="40956-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="40956-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="40956-413">Implementar a lista de pacote de serviço: lista de Olá devolve de pacotes do serviço numa aplicação implementada.</span><span class="sxs-lookup"><span data-stu-id="40956-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="40956-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="40956-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="40956-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="40956-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="40956-416">Algumas das consultas de Olá devolvem resultados paginados.</span><span class="sxs-lookup"><span data-stu-id="40956-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="40956-417">Olá retorno das seguintes consultas-se uma lista derivada [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="40956-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="40956-418">Se os resultados de Olá não se enquadram uma mensagem, é devolvida apenas uma página e um ContinuationToken que controla onde parou a enumeração.</span><span class="sxs-lookup"><span data-stu-id="40956-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="40956-419">Continue toocall Olá mesmo consultar e passar no token de continuação Olá de Olá anterior tooget seguintes os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="40956-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="40956-420">Exemplos</span><span class="sxs-lookup"><span data-stu-id="40956-420">Examples</span></span>
<span data-ttu-id="40956-421">Olá código seguinte obtém aplicações mau estado de funcionamento Olá num cluster de Olá:</span><span class="sxs-lookup"><span data-stu-id="40956-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="40956-422">Olá seguinte cmdlet obtém detalhes da aplicação Olá recursos de infraestrutura de Olá: / aplicação WordCount.</span><span class="sxs-lookup"><span data-stu-id="40956-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="40956-423">Tenha em atenção que o estado de funcionamento é em aviso.</span><span class="sxs-lookup"><span data-stu-id="40956-423">Notice that health state is at warning.</span></span>

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

<span data-ttu-id="40956-424">Olá seguinte cmdlet obtém serviços Olá com um Estado de funcionamento de erro:</span><span class="sxs-lookup"><span data-stu-id="40956-424">hello following cmdlet gets hello services with a health state of error:</span></span>

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

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="40956-425">Atualizações de cluster e da aplicação</span><span class="sxs-lookup"><span data-stu-id="40956-425">Cluster and application upgrades</span></span>
<span data-ttu-id="40956-426">Durante uma atualização monitorizada do cluster de Olá e aplicação, o Service Fabric verifica tooensure de estado de funcionamento que tudo permanece bom estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="40956-427">Se uma entidade está danificada, avaliada através de políticas de estado de funcionamento configurado, atualização Olá aplica-se próxima ação Olá da toodetermine de políticas específicas de atualização.</span><span class="sxs-lookup"><span data-stu-id="40956-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="40956-428">atualização Olá poderá estar em pausa tooallow interação do utilizador (tais como corrigir condições de erro ou alteração de políticas) ou, pode automaticamente reverter toohello versão de boa anterior.</span><span class="sxs-lookup"><span data-stu-id="40956-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="40956-429">Durante uma *cluster* atualização, pode obter o estado de atualização de cluster do Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="40956-430">Estado de atualização de Olá inclui avaliações mau estado de funcionamento, que toowhat ponto é mau estado de funcionamento no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="40956-431">Se a atualização Olá for revertida devido a problemas de toohealth, o estado de atualização de Olá memorizou por motivos de mau estado de funcionamento último Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="40956-432">Esta informação pode ajudar os administradores a investigar o que aconteceu após a atualização de Olá revertida ou parado.</span><span class="sxs-lookup"><span data-stu-id="40956-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="40956-433">Da mesma forma, durante um *aplicação* atualização, as avaliações de mau estado de funcionamento estão contidas no estado de atualização da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="40956-434">Olá seguinte mostra o estado de atualização da aplicação Olá para um recurso de infraestrutura modificado: / aplicação WordCount.</span><span class="sxs-lookup"><span data-stu-id="40956-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="40956-435">Um watchdog do comunicou um erro das suas réplicas.</span><span class="sxs-lookup"><span data-stu-id="40956-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="40956-436">atualização de Olá está a implementar porque as verificações de estado de funcionamento de Olá não são respeitadas.</span><span class="sxs-lookup"><span data-stu-id="40956-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

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

<span data-ttu-id="40956-437">Saiba mais sobre Olá [atualização da aplicação de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="40956-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="40956-438">Utilizar tootroubleshoot de avaliações de estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="40956-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="40956-439">Sempre que há um problema com o cluster de Olá ou uma aplicação, observe toopinpoint de estado de funcionamento de cluster ou aplicação Olá o que é incorreto.</span><span class="sxs-lookup"><span data-stu-id="40956-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="40956-440">avaliações de mau estado de funcionamento de Olá fornecem detalhes sobre o estado de mau estado de funcionamento atual Olá accionadas.</span><span class="sxs-lookup"><span data-stu-id="40956-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="40956-441">Se for necessário, pode explorar para baixo subordinados danificados entidades tooidentify Olá causa.</span><span class="sxs-lookup"><span data-stu-id="40956-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="40956-442">Por exemplo, considere uma aplicação mau estado de funcionamento porque não existe um relatório de erros das suas réplicas.</span><span class="sxs-lookup"><span data-stu-id="40956-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="40956-443">Olá seguinte cmdlet do Powershell mostra avaliações Olá de mau estado de funcionamento:</span><span class="sxs-lookup"><span data-stu-id="40956-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

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

<span data-ttu-id="40956-444">Pode observar Olá réplica tooget obter mais informações:</span><span class="sxs-lookup"><span data-stu-id="40956-444">You can look at hello replica tooget more information:</span></span>

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
> <span data-ttu-id="40956-445">Olá avaliações mau estado de funcionamento Mostrar Olá primeiro razão Olá entidade é avaliada toocurrent estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="40956-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="40956-446">Podem existir vários outros eventos que activam este estado, mas não são refletidas em avaliações de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="40956-447">tooget obter mais informações, desagregação em Olá toofigure de entidades de estado de funcionamento enviados todos os relatórios de mau estado de funcionamento de Olá num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="40956-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="40956-448">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="40956-448">Next steps</span></span>
[<span data-ttu-id="40956-449">Utilizar tootroubleshoot de relatórios de estado de funcionamento do sistema</span><span class="sxs-lookup"><span data-stu-id="40956-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="40956-450">Adicionar relatórios de estado de funcionamento personalizados do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="40956-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="40956-451">Como tooreport e verificação de estado de funcionamento do serviço</span><span class="sxs-lookup"><span data-stu-id="40956-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="40956-452">Monitorizar e diagnosticar os serviços localmente</span><span class="sxs-lookup"><span data-stu-id="40956-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="40956-453">Atualização da aplicação de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="40956-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
