---
title: contentores de saldo aaaLoad no cluster DC/OS do Azure | Microsoft Docs
description: "O balanceamento de carga entre vários contentores num cluster DC/OS do serviço de contentor do Azure."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contentores, Microserviços, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="313b7-104">Contentores de balanceamento de carga de um cluster do serviço de contentor do Azure DC/OS</span><span class="sxs-lookup"><span data-stu-id="313b7-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="313b7-105">Neste artigo, vamos explorar como toocreate um balanceador de carga interno no DC/SO gerido o serviço de contentor Azure utilizando o Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="313b7-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="313b7-106">Esta configuração permite tooscale as suas aplicações horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="313b7-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="313b7-107">Também permite-lhe tootake partido dos clusters de agente públicas e privadas Olá colocando os balanceadores de carga no cluster pública Olá e os contentores de aplicação no cluster privada Olá.</span><span class="sxs-lookup"><span data-stu-id="313b7-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="313b7-108">Neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="313b7-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="313b7-109">Configurar um balanceador de carga Marathon</span><span class="sxs-lookup"><span data-stu-id="313b7-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="313b7-110">Implementar uma aplicação utilizando Olá Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="313b7-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="313b7-111">Configurar e Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="313b7-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="313b7-112">Precisa de um DC/OS ACS Olá toocomplete de cluster, os passos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="313b7-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="313b7-113">Se for necessário, [este script de exemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar uma por si.</span><span class="sxs-lookup"><span data-stu-id="313b7-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="313b7-114">Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="313b7-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="313b7-115">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="313b7-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="313b7-116">Se precisar de tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="313b7-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="313b7-117">Descrição geral do balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="313b7-117">Load balancing overview</span></span>

<span data-ttu-id="313b7-118">Existem duas camadas de balanceamento de carga num cluster DC/OS do serviço de contentor do Azure:</span><span class="sxs-lookup"><span data-stu-id="313b7-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="313b7-119">**Balanceador de carga do Azure** fornece pontos de entrada públicos (Olá aqueles que os utilizadores finais acesso).</span><span class="sxs-lookup"><span data-stu-id="313b7-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="313b7-120">Um Azure LB é fornecido automaticamente pelo serviço de contentor do Azure e está, por predefinição, configurado tooexpose porta 80, 443 e 8080.</span><span class="sxs-lookup"><span data-stu-id="313b7-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="313b7-121">**Olá Balanceador de carga Marathon (marathon-lb)** instâncias de toocontainer de pedidos que estes pedidos de serviço de entrada de rotas.</span><span class="sxs-lookup"><span data-stu-id="313b7-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="313b7-122">À medida que dimensionamos os contentores de Olá que fornecem o nosso serviço web, Olá marathon-lb feita dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="313b7-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="313b7-123">Este Balanceador de carga não é fornecido por predefinição no seu serviço de contentor, mas é fácil tooinstall.</span><span class="sxs-lookup"><span data-stu-id="313b7-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="313b7-124">Configurar o Balanceador de carga Marathon</span><span class="sxs-lookup"><span data-stu-id="313b7-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="313b7-125">Balanceador de carga Marathon reconfigura dinamicamente com base nos contentores Olá que tenha implementado.</span><span class="sxs-lookup"><span data-stu-id="313b7-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="313b7-126">Também é resiliente toohello perda de um contentor ou um agente - se isto ocorrer, o Apache Mesos reinicia o contentor de Olá noutro local e marathon-lb feita.</span><span class="sxs-lookup"><span data-stu-id="313b7-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="313b7-127">Execute Olá seguindo o Balanceador de carga marathon do comando tooinstall Olá do cluster do agente Olá público.</span><span class="sxs-lookup"><span data-stu-id="313b7-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="313b7-128">Implementar aplicações com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="313b7-128">Deploy load balanced application</span></span>

<span data-ttu-id="313b7-129">Agora que temos o pacote do marathon-lb Olá, podemos implementar um contentor de aplicação que pretendemos saldo tooload.</span><span class="sxs-lookup"><span data-stu-id="313b7-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="313b7-130">Em primeiro lugar, obter Olá FQDN dos agentes de Olá publicamente exposto.</span><span class="sxs-lookup"><span data-stu-id="313b7-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="313b7-131">Em seguida, crie um ficheiro denominado *Olá web.json* e de cópia no Olá seguir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="313b7-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="313b7-132">Olá `HAPROXY_0_VHOST` toobe atualizado com Olá FQDN dos agentes DC/SO de Olá tem de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="313b7-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="313b7-133">Utilize Olá CLI de DC/SO toorun Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="313b7-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="313b7-134">Por predefinição o Marathon implementa cluster privada do Olá Olá applicaton toohello.</span><span class="sxs-lookup"><span data-stu-id="313b7-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="313b7-135">Isto significa que Olá acima implementação só é acessível através do seu Balanceador de carga, que é normalmente o comportamento de Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="313b7-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="313b7-136">Quando tiver sido implementada a aplicação Olá, procure toohello FQDN Olá agente cluster tooview com balanceamento de carga aplicação.</span><span class="sxs-lookup"><span data-stu-id="313b7-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![Imagem da aplicação com balanceamento de carga](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="313b7-138">Configurar o Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="313b7-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="313b7-139">Por predefinição, o Balanceador de Carga do Azure expõe as portas 80, 8080 e 443.</span><span class="sxs-lookup"><span data-stu-id="313b7-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="313b7-140">Se estiver a utilizar uma destas três portas (como no Olá acima exemplo), então, não há nada que terá toodo.</span><span class="sxs-lookup"><span data-stu-id="313b7-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="313b7-141">Deve ser capaz de toohit FQDN do Balanceador de carga do agente e, sempre que atualizar, irá aceder a um dos seus três servidores web de uma maneira round-robin.</span><span class="sxs-lookup"><span data-stu-id="313b7-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="313b7-142">Se utilizar uma porta diferente, terá de regra de tooadd round robin e uma sonda no balanceador de carga Olá para a porta de Olá que utilizou.</span><span class="sxs-lookup"><span data-stu-id="313b7-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="313b7-143">Pode fazê-lo de Olá [CLI do Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), com os comandos de Olá `azure network lb rule create` e `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="313b7-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="313b7-144">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="313b7-144">Next steps</span></span>

<span data-ttu-id="313b7-145">Neste tutorial, aprendeu sobre balanceamento de carga no ACS com o Marathon Olá e carga do Azure balanceadores incluindo Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="313b7-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="313b7-146">Configurar um balanceador de carga Marathon</span><span class="sxs-lookup"><span data-stu-id="313b7-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="313b7-147">Implementar uma aplicação utilizando Olá Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="313b7-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="313b7-148">Configurar e Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="313b7-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="313b7-149">Produzir toohello seguinte toolearn tutorial sobre a integração de armazenamento do Azure com o DC/OS, no Azure.</span><span class="sxs-lookup"><span data-stu-id="313b7-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="313b7-150">Azure de montar a partilha de ficheiros no cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="313b7-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)