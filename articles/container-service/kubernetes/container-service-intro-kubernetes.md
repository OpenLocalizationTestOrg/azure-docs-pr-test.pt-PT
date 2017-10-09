---
title: "aaaIntroduction tooAzure serviço de contentor para Kubernetes | Microsoft Docs"
description: "Serviço de contentor do Azure para Kubernetes torna simple toodeploy e gerir as aplicações baseadas no contentor no Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, Containers, Microsserviços, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="52d52-104">Introdução tooAzure serviço de contentor para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="52d52-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="52d52-105">Serviço de contentor do Azure para Kubernetes torna simple toocreate, configurar e gerir um cluster de máquinas virtuais que estão pré-configuradas toorun de aplicações.</span><span class="sxs-lookup"><span data-stu-id="52d52-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="52d52-106">Isto permite-lhe toouse suas competências existentes, ou desenhar após um corpo de grande e crescente de conhecimentos de Comunidade, toodeploy e gerir as aplicações baseadas no contentor no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="52d52-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="52d52-107">Ao utilizar o serviço de contentor do Azure, pode tirar partido das Olá funcionalidades de nível empresarial do Azure, mantendo ainda portabilidade de aplicações através de Kubernetes e Olá formato de imagem de Docker.</span><span class="sxs-lookup"><span data-stu-id="52d52-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="52d52-108">Utilizar o Azure Container Service para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="52d52-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="52d52-109">O nosso objetivo com o serviço de contentor do Azure é tooprovide num ambiente de alojamento do contentor utilizando ferramentas open source e tecnologias que estão atualmente populares entre os nossos clientes.</span><span class="sxs-lookup"><span data-stu-id="52d52-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="52d52-110">fim de toothis, expomos pontos finais da API de Kubernetes padrão Olá.</span><span class="sxs-lookup"><span data-stu-id="52d52-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="52d52-111">Utilizando estes pontos finais padrão, pode tirar partido do software que seja capaz de comunicar tooa Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="52d52-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="52d52-112">Por exemplo, pode escolher [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) ou [draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="52d52-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="52d52-113">Criar um cluster do Kubernetes com o Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="52d52-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="52d52-114">toobegin utilizando o serviço de contentor do Azure, implementar um cluster do serviço de contentor do Azure com Olá [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) ou através do portal Olá (Olá pesquisa Marketplace para **serviço de contentor Azure**).</span><span class="sxs-lookup"><span data-stu-id="52d52-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="52d52-115">Se um utilizador avançado que necessitam de mais controlo sobre os modelos do Azure Resource Manager Olá, pode utilizar open source para Olá [motor de acs](https://github.com/Azure/acs-engine) projeto toobuild os seus próprios Kubernetes personalizados do cluster e implementá-la através de Olá `az` CLI.</span><span class="sxs-lookup"><span data-stu-id="52d52-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="52d52-116">Utilizar Kubernetes</span><span class="sxs-lookup"><span data-stu-id="52d52-116">Using Kubernetes</span></span>
<span data-ttu-id="52d52-117">O Kubernetes automatiza a implementação, o dimensionamento e a gestão de aplicações no contentor.</span><span class="sxs-lookup"><span data-stu-id="52d52-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="52d52-118">Tem um conjunto avançado de funcionalidades, incluindo:</span><span class="sxs-lookup"><span data-stu-id="52d52-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="52d52-119">Empacotamento automático</span><span class="sxs-lookup"><span data-stu-id="52d52-119">Automatic binpacking</span></span>
* <span data-ttu-id="52d52-120">Autorrecuperação</span><span class="sxs-lookup"><span data-stu-id="52d52-120">Self-healing</span></span>
* <span data-ttu-id="52d52-121">Dimensionamento horizontal</span><span class="sxs-lookup"><span data-stu-id="52d52-121">Horizontal scaling</span></span>
* <span data-ttu-id="52d52-122">Deteção do serviço e balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="52d52-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="52d52-123">Implementações e reversões automáticas</span><span class="sxs-lookup"><span data-stu-id="52d52-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="52d52-124">Gestão de segredos e de configurações</span><span class="sxs-lookup"><span data-stu-id="52d52-124">Secret and configuration management</span></span>
* <span data-ttu-id="52d52-125">Orquestração de armazenamento</span><span class="sxs-lookup"><span data-stu-id="52d52-125">Storage orchestration</span></span>
* <span data-ttu-id="52d52-126">Execução de lotes</span><span class="sxs-lookup"><span data-stu-id="52d52-126">Batch execution</span></span>

<span data-ttu-id="52d52-127">Diagrama da arquitetura de Kubernetes implementado através do Azure Container Service:</span><span class="sxs-lookup"><span data-stu-id="52d52-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Serviço de contentor do Azure configurada toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="52d52-129">Vídeos</span><span class="sxs-lookup"><span data-stu-id="52d52-129">Videos</span></span>

<span data-ttu-id="52d52-130">Suporte de Kubernetes no Azure Container Service (Azure Friday, janeiro de 2017):</span><span class="sxs-lookup"><span data-stu-id="52d52-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="52d52-131">Ferramentas para Programar e Implementar Aplicações no Kubernetes (Azure OpenDev, junho de 2017):</span><span class="sxs-lookup"><span data-stu-id="52d52-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="52d52-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="52d52-132">Next steps</span></span>

<span data-ttu-id="52d52-133">Explorar Olá [início rápido de Kubernetes](container-service-kubernetes-walkthrough.md) toobegin explorar o serviço de contentor do Azure hoje.</span><span class="sxs-lookup"><span data-stu-id="52d52-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
