---
title: "cluster aaaMonitor um serviço de contentor do Azure com Sysdig | Microsoft Docs"
description: Monitorizar um cluster do Azure Container Service com o Sysdig.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contentores, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="299eb-104">Monitorizar um cluster do Azure Container Service com o Sysdig</span><span class="sxs-lookup"><span data-stu-id="299eb-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="299eb-105">Neste artigo, iremos implementar Sysdig agentes tooall Olá agente nós do cluster do serviço de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="299eb-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="299eb-106">Para esta configuração, é necessária uma conta do Sysdig.</span><span class="sxs-lookup"><span data-stu-id="299eb-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="299eb-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="299eb-107">Prerequisites</span></span>
<span data-ttu-id="299eb-108">[Implemente](container-service-deployment.md) e [ligue](../container-service-connect.md) um cluster configurado pelo Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="299eb-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="299eb-109">Explorar Olá [IU do Marathon](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="299eb-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="299eb-110">Aceda demasiado[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset uma conta de nuvem Sysdig.</span><span class="sxs-lookup"><span data-stu-id="299eb-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="299eb-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="299eb-111">Sysdig</span></span>
<span data-ttu-id="299eb-112">Sysdig é um serviço de monitorização que permite-lhe toomonitor os contentores no seu cluster.</span><span class="sxs-lookup"><span data-stu-id="299eb-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="299eb-113">Sysdig é conhecido toohelp na resolução de problemas, mas também tem as métricas de monitorização básicas para a CPU, redes, memória e e/s.</span><span class="sxs-lookup"><span data-stu-id="299eb-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="299eb-114">Sysdig torna mais fácil toosee os contentores estão a funcionar Olá hardest ou essencialmente utilizando hello mais memória e CPU.</span><span class="sxs-lookup"><span data-stu-id="299eb-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="299eb-115">Esta vista está a ser Olá secção "Descrição geral", o que está atualmente na versão beta.</span><span class="sxs-lookup"><span data-stu-id="299eb-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![IU do Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="299eb-117">Configurar uma implementação do Sysdig com o Marathon</span><span class="sxs-lookup"><span data-stu-id="299eb-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="299eb-118">Estes passos irão mostrar como tooconfigure e implementar Sysdig aplicações tooyour cluster com o Marathon.</span><span class="sxs-lookup"><span data-stu-id="299eb-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="299eb-119">Aceder à IU do DC/OS, através de [http://localhost:80 /](http://localhost:80/) uma vez na IU do DC/SO de Olá navegue toohello "Universo", que se encontre na Olá inferior esquerda e, em seguida, procure "Sysdig."</span><span class="sxs-lookup"><span data-stu-id="299eb-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![Sysdig no DC/OS Universe](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="299eb-121">Agora o configuração de Olá toocomplete terá um Sysdig nuvem conta ou uma conta de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="299eb-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="299eb-122">Uma vez que tem sessão iniciada num Web site do toohello Sysdig na nuvem, clique em seu nome de utilizador e, na página Olá, deverá ver a "chave de acesso".</span><span class="sxs-lookup"><span data-stu-id="299eb-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Chave de API do Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="299eb-124">Em seguida, introduza a chave de acesso na configuração de Sysdig Olá dentro Olá do DC/OS.</span><span class="sxs-lookup"><span data-stu-id="299eb-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![Configuração de Sysdig no Olá do DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="299eb-126">Agora defina Olá instâncias too10000000 para que sempre que é adicionado um novo nó de toohello cluster Sysdig irão implementar automaticamente um agente toothat novo nó.</span><span class="sxs-lookup"><span data-stu-id="299eb-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="299eb-127">Este é um toomake solução provisória se que sysdig implementará tooall novos agentes num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="299eb-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Configuração de Sysdig no Olá DC/SO universo-instâncias](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="299eb-129">Assim que instalou o pacote de Olá navegue toohello back Sysdig IU e irá ser tooexplore capaz de métricas de utilização diferentes Olá para contentores de Olá dentro do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="299eb-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="299eb-130">Também pode instalar dasboards específicos do Mesos e do Marathon através do [assistente de dashboard novo](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="299eb-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
