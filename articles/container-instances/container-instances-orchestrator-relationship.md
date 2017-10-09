---
title: "Instâncias de contentor aaaAzure e orquestração de contentor"
description: "Compreender a forma como as instâncias de contentor do Azure interagir com orchestrators de contentor"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="f3412-103">Instâncias de contentor do Azure e orchestrators de contentor</span><span class="sxs-lookup"><span data-stu-id="f3412-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="f3412-104">Devido ao respetivo tamanho pequeno e a orientação de aplicação, os contentores são adequados para ambientes de entrega seja ágil e arquiteturas de microsserviço.</span><span class="sxs-lookup"><span data-stu-id="f3412-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="f3412-105">tarefa de Olá de automatizar e gerir um grande número de contentores e como eles interagem é conhecida como *orchestration*.</span><span class="sxs-lookup"><span data-stu-id="f3412-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="f3412-106">Orchestrators contentor populares incluem Kubernetes, DC/OS e Docker Swarm, todos os que estão disponíveis no Olá [serviço de contentor Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="f3412-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="f3412-107">Instâncias de contentor do Azure fornece algumas das Olá básico de funcionalidades de plataformas de orquestração de agendamento, mas não abrange os serviços de valor mais alto de Olá que essas plataformas fornecem e na realidade podem ser complementares com os mesmos.</span><span class="sxs-lookup"><span data-stu-id="f3412-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="f3412-108">Este artigo descreve âmbito Olá que processa as instâncias de contentor do Azure e como completa orchestrators contentor podem interagir com ele.</span><span class="sxs-lookup"><span data-stu-id="f3412-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="f3412-109">Orquestração tradicional</span><span class="sxs-lookup"><span data-stu-id="f3412-109">Traditional orchestration</span></span>

<span data-ttu-id="f3412-110">definição do padrão de Olá da orquestração inclui Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="f3412-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="f3412-111">**Agendamento**: dada uma imagem de contentor e um pedido de recurso, localizar uma máquina adequada no contentor de Olá que toorun.</span><span class="sxs-lookup"><span data-stu-id="f3412-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="f3412-112">**Afinidade/Anti-affinity**: especificar que um conjunto de contentores deverão ser executadas próximas entre si (para um desempenho) ou suficientemente até que ponto apart (para disponibilidade).</span><span class="sxs-lookup"><span data-stu-id="f3412-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="f3412-113">**Monitorização de estado de funcionamento**: ver para as falhas de contentor e automaticamente reprogramá-los.</span><span class="sxs-lookup"><span data-stu-id="f3412-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="f3412-114">**Ativação pós-falha**: monitorizar o que está a ser executado em cada máquina e Reprogramar contentores de nós de toohealthy máquinas com falhas.</span><span class="sxs-lookup"><span data-stu-id="f3412-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="f3412-115">**Dimensionamento**: Adicionar ou remover o pedido de toomatch de instâncias de contentor, manualmente ou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f3412-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="f3412-116">**Rede**: forneça uma rede de sobreposição para coordenar contentores toocommunicate em várias máquinas de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="f3412-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="f3412-117">**Deteção do serviço**: Ativar contentores toolocate entre si automaticamente, mesmo que tal como mover entre computadores anfitriões e alterar os endereços IP.</span><span class="sxs-lookup"><span data-stu-id="f3412-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="f3412-118">**Coordenado as atualizações de aplicações**: Gerir contentor atualizações tooavoid aplicação tempo e ativar a reversão se algo não bate certo.</span><span class="sxs-lookup"><span data-stu-id="f3412-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="f3412-119">Orquestração com instâncias de contentor do Azure: uma abordagem em camadas</span><span class="sxs-lookup"><span data-stu-id="f3412-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="f3412-120">Instâncias de contentor do Azure permite tooorchestration uma abordagem em camadas, fornecendo todas Olá agendamento e as capacidades de gestão necessário toorun um único contentor, permitindo orchestrator tarefas de contentor de várias plataformas toomanage seguir.</span><span class="sxs-lookup"><span data-stu-id="f3412-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="f3412-121">Porque todos os Olá subjacente infraestrutura para instâncias de contentor é gerido pelo Azure, uma plataforma do orchestrator não precisa de tooconcern próprio com localizar uma máquina de anfitrião adequado no qual toorun um único contentor.</span><span class="sxs-lookup"><span data-stu-id="f3412-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="f3412-122">elasticidade Olá da nuvem Olá garante que uma está sempre disponível.</span><span class="sxs-lookup"><span data-stu-id="f3412-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="f3412-123">Em vez disso, o orchestrator Olá pode se focarem em tarefas de Olá que simplificam o desenvolvimento de Olá de arquiteturas de contentor multi, incluindo o dimensionamento e atualizações coordenadas.</span><span class="sxs-lookup"><span data-stu-id="f3412-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="f3412-124">Potenciais cenários</span><span class="sxs-lookup"><span data-stu-id="f3412-124">Potential scenarios</span></span>

<span data-ttu-id="f3412-125">Enquanto a integração do orchestrator com instâncias de contentor do Azure é ainda nascent, iremos prevê que podem surgir alguns ambientes diferentes:</span><span class="sxs-lookup"><span data-stu-id="f3412-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="f3412-126">Orquestração de instâncias de contentor de forma exclusiva</span><span class="sxs-lookup"><span data-stu-id="f3412-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="f3412-127">Pois começar rapidamente e faturado por Olá segundo, um ambiente com base no exclusivamente instâncias de contentor do Azure oferece iniciado Olá tooget de forma mais rápida e toodeal com cargas de trabalho altamente variáveis.</span><span class="sxs-lookup"><span data-stu-id="f3412-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="f3412-128">Combinação de instâncias de contentor e contentores nas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f3412-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="f3412-129">Para demoradas, cargas de trabalho estáveis, da orquestração contentores num cluster de máquinas virtuais dedicadas normalmente, será mais barata que executar Olá contentores mesmos com instâncias de contentor.</span><span class="sxs-lookup"><span data-stu-id="f3412-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="f3412-130">No entanto, as instâncias de contentor oferecem uma excelente solução para rápida expansão e contracting toodeal da capacidade global com picos inesperados ou curta duração em utilização.</span><span class="sxs-lookup"><span data-stu-id="f3412-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="f3412-131">Em vez de aumentar horizontalmente o número de Olá de máquinas virtuais no seu cluster, em seguida, implementar contentores adicionais dessas máquinas, Olá orchestrator pode simplesmente agendar contentores adicionais Olá utilizando as instâncias de contentor e eliminá-los quando forem não são necessários.</span><span class="sxs-lookup"><span data-stu-id="f3412-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="f3412-132">Implementação de exemplo: conector de instâncias de contentor do Azure para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="f3412-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="f3412-133">toodemonstrate como plataformas de orquestração do contentor podem integrar com instâncias de contentor do Azure, podemos ter sido iniciado edifício um [conector de exemplo para Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="f3412-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="f3412-134">Olá conector para Kubernetes mimics Olá [kubelet] [ kubelet-doc] ao registar como um nó com capacidade ilimitada e emissão criação Olá de [pods] [ pod-doc] como grupos de contentor em instâncias de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3412-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="f3412-135">Pode ser criados conectores para outras orchestrators que da mesma forma integrada com energia Olá de toocombine de primitivos do plataforma do orchestrator Olá API com velocidade de Olá e na simplicidade da gestão de contentores em instâncias de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3412-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="f3412-136">Olá conector ACI para Kubernetes é *experimental* e não deve ser utilizado em produção.</span><span class="sxs-lookup"><span data-stu-id="f3412-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3412-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f3412-137">Next steps</span></span>

<span data-ttu-id="f3412-138">Criar o contentor do primeiro com instâncias de contentor do Azure utilizando o Olá [guia de introdução](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="f3412-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/