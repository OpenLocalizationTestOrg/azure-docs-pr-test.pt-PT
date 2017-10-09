---
title: aaaMonitor um Kubernetes Azure cluster com CoScale | Microsoft Docs
description: "Monitor de um cluster de Kubernetes no serviço de contentor Azure utilizando CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="c70d7-103">Monitor de um cluster de Kubernetes de serviço de contentor do Azure com CoScale</span><span class="sxs-lookup"><span data-stu-id="c70d7-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="c70d7-104">Neste artigo, vamos mostrar-lhe como toodeploy Olá [CoScale](https://www.coscale.com/) toomonitor agente todos os nós e contentores no seu Kubernetes cluster do serviço de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="c70d7-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="c70d7-105">Precisa de uma conta com CoScale para esta configuração.</span><span class="sxs-lookup"><span data-stu-id="c70d7-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="c70d7-106">Sobre CoScale</span><span class="sxs-lookup"><span data-stu-id="c70d7-106">About CoScale</span></span> 

<span data-ttu-id="c70d7-107">CoScale é uma plataforma de monitorização que recolhe métricas e eventos de todos os contentores em várias plataformas de orquestração.</span><span class="sxs-lookup"><span data-stu-id="c70d7-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="c70d7-108">CoScale oferece monitorização completa pilha para ambientes de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c70d7-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="c70d7-109">Fornece visualizações e análise de todas as camadas na pilha de Olá: Olá SO, Kubernetes, Docker e aplicações em execução dentro os contentores.</span><span class="sxs-lookup"><span data-stu-id="c70d7-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="c70d7-110">CoScale oferece várias dashboards de monitorização incorporadas e tem operadores de tooallow de deteção de anomalias incorporadas e problemas de infraestrutura e aplicação de toofind de programadores rápido.</span><span class="sxs-lookup"><span data-stu-id="c70d7-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![CoScale da IU](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="c70d7-112">Como é mostrado neste artigo, pode instalar agentes num toorun de cluster Kubernetes CoScale como uma solução de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c70d7-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="c70d7-113">Se quiser tookeep os dados on-site, CoScale também está disponível para instalação no local.</span><span class="sxs-lookup"><span data-stu-id="c70d7-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c70d7-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c70d7-114">Prerequisites</span></span>

<span data-ttu-id="c70d7-115">Terá primeiro demasiado[criar uma conta de CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="c70d7-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="c70d7-116">Esta instrução parte do princípio de que tem [criado um cluster de Kubernetes utilizando o serviço de contentor do Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="c70d7-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="c70d7-117">Também parte do princípio que tem Olá `az` CLI do Azure e `kubectl` as ferramentas instaladas.</span><span class="sxs-lookup"><span data-stu-id="c70d7-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="c70d7-118">Pode testar se tiver Olá `az` ferramenta instalada através da execução:</span><span class="sxs-lookup"><span data-stu-id="c70d7-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="c70d7-119">Se não tiver Olá `az` ferramenta instalada, existem instruções [aqui](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c70d7-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="c70d7-120">Pode testar se tiver Olá `kubectl` ferramenta instalada através da execução:</span><span class="sxs-lookup"><span data-stu-id="c70d7-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="c70d7-121">Se não tiver `kubectl` instalado, pode executar:</span><span class="sxs-lookup"><span data-stu-id="c70d7-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="c70d7-122">Instalar o agente de CoScale Olá com um DaemonSet</span><span class="sxs-lookup"><span data-stu-id="c70d7-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="c70d7-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) são utilizados pelo Kubernetes toorun uma única instância de um contentor em cada anfitrião no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="c70d7-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="c70d7-124">Se estiver a perfeita para a execução de agentes de monitorização, tais como o agente de CoScale Olá.</span><span class="sxs-lookup"><span data-stu-id="c70d7-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="c70d7-125">Depois de iniciar sessão no tooCoScale, aceda toohello [página agente](https://app.coscale.com/) agentes de CoScale tooinstall no seu cluster utilizando um DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="c70d7-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="c70d7-126">Olá CoScale IU fornece toocreate de passos de configuração orientada um agente e o início da monitorização completa do seu cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c70d7-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![Configuração do agente coScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="c70d7-128">agente de Olá toostart no cluster de Olá, execute o comando de Olá fornecido:</span><span class="sxs-lookup"><span data-stu-id="c70d7-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Iniciar o agente de CoScale Olá](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="c70d7-130">Já está!</span><span class="sxs-lookup"><span data-stu-id="c70d7-130">That's it!</span></span> <span data-ttu-id="c70d7-131">Depois de agentes Olá estão em execução, deve ver os dados na consola de Olá dentro de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="c70d7-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="c70d7-132">Visite Olá [página agente](https://app.coscale.com/) toosee um resumo do cluster, execute os passos de configuração adicionais e ver os dashboards, tais como Olá **descrição geral do cluster Kubernetes**.</span><span class="sxs-lookup"><span data-stu-id="c70d7-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Descrição geral do cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="c70d7-134">agente de CoScale Olá é implementada automaticamente em novos computadores no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="c70d7-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="c70d7-135">Olá as atualizações de agente automaticamente quando é lançada uma nova versão.</span><span class="sxs-lookup"><span data-stu-id="c70d7-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c70d7-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c70d7-136">Next steps</span></span>

<span data-ttu-id="c70d7-137">Consulte Olá [CoScale documentação](http://docs.coscale.com/) e [blogue](https://www.coscale.com/blog) para obter informações sobre CoScale soluções de monitorização.</span><span class="sxs-lookup"><span data-stu-id="c70d7-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

