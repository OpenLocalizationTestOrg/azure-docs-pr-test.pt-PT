---
title: cluster de Azure Kubernetes aaaManage com IU da web | Microsoft Docs
description: "Utilizar Olá Kubernetes IU da web do serviço de contentor do Azure"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="527af-103">Utilizar Olá Kubernetes IU da web do serviço de contentor do Azure</span><span class="sxs-lookup"><span data-stu-id="527af-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="527af-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="527af-104">Prerequisites</span></span>
<span data-ttu-id="527af-105">Esta instrução parte do princípio de que tem [criado um cluster de Kubernetes utilizando o serviço de contentor do Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="527af-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="527af-106">Também parte do princípio que tem Olá Azure CLI 2.0 e `kubectl` as ferramentas instaladas.</span><span class="sxs-lookup"><span data-stu-id="527af-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="527af-107">Pode testar se tiver Olá `az` ferramenta instalada através da execução:</span><span class="sxs-lookup"><span data-stu-id="527af-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="527af-108">Se não tiver Olá `az` ferramenta instalada, existem instruções [aqui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="527af-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="527af-109">Pode testar se tiver Olá `kubectl` ferramenta instalada através da execução:</span><span class="sxs-lookup"><span data-stu-id="527af-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="527af-110">Se não tiver `kubectl` instalado, pode executar:</span><span class="sxs-lookup"><span data-stu-id="527af-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="527af-111">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="527af-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="527af-112">Ligar a IU da web do toohello</span><span class="sxs-lookup"><span data-stu-id="527af-112">Connect toohello web UI</span></span>
<span data-ttu-id="527af-113">Pode iniciar a IU da web do Olá Kubernetes executando:</span><span class="sxs-lookup"><span data-stu-id="527af-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="527af-114">Isto deve abrir um browser configurado tootalk tooa segura proxy web ligar o seu computador local toohello Kubernetes IU da web do.</span><span class="sxs-lookup"><span data-stu-id="527af-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="527af-115">Criar e expor um serviço</span><span class="sxs-lookup"><span data-stu-id="527af-115">Create and expose a service</span></span>
1. <span data-ttu-id="527af-116">Na IU da web de Kubernetes a Olá, clique em **criar** botão na janela do Olá superior direito.</span><span class="sxs-lookup"><span data-stu-id="527af-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Kubernetes criar a IU](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="527af-118">Abre de caixa de diálogo onde podem iniciar a criação da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="527af-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="527af-119">Atribua o nome de Olá `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="527af-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="527af-120">Olá utilize [ `nginx` contentor do Docker](https://hub.docker.com/_/nginx/) e implementar três réplicas deste serviço web.</span><span class="sxs-lookup"><span data-stu-id="527af-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Caixa de diálogo de criar Kubernetes Pod](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="527af-122">Em **serviço**, selecione **externo** e introduza a porta 80.</span><span class="sxs-lookup"><span data-stu-id="527af-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="527af-123">Esta definição carga balanceia três réplicas toohello de tráfego.</span><span class="sxs-lookup"><span data-stu-id="527af-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Caixa de diálogo Criar do serviço de Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="527af-125">Clique em **implementar** toodeploy desses contentores e serviços.</span><span class="sxs-lookup"><span data-stu-id="527af-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Implementar Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="527af-127">Ver os contentores</span><span class="sxs-lookup"><span data-stu-id="527af-127">View your containers</span></span>
<span data-ttu-id="527af-128">Depois de clicar em **implementar**, Olá IU mostra uma vista do seu serviço, como implementa:</span><span class="sxs-lookup"><span data-stu-id="527af-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Estado de Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="527af-130">Pode ver o estado de Olá de cada objeto Kubernetes no círculo Olá no lado esquerdo do Olá da IU, em **Pods**.</span><span class="sxs-lookup"><span data-stu-id="527af-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="527af-131">Se for um círculo parcialmente completo, em seguida, objeto Olá ainda está em implementação.</span><span class="sxs-lookup"><span data-stu-id="527af-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="527af-132">Quando um objeto é totalmente implementado, apresenta uma marca de verificação verde:</span><span class="sxs-lookup"><span data-stu-id="527af-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes implementado](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="527af-134">Assim que tudo está a ser executado, clique das suas pods toosee detalhes Olá com o serviço web.</span><span class="sxs-lookup"><span data-stu-id="527af-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Kubernetes Pods](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="527af-136">No Olá **Pods** vista, pode ver informações sobre contentores de Olá no pod Olá, bem como os recursos de CPU e memória do Olá utilizados por esses contentores:</span><span class="sxs-lookup"><span data-stu-id="527af-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Kubernetes recursos](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="527af-138">Se não vir recursos Olá, que poderá necessitar toowait alguns minutos para Olá toopropagate de dados de monitorização.</span><span class="sxs-lookup"><span data-stu-id="527af-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="527af-139">toosee Olá registos para o contentor, clique em **ver registos**.</span><span class="sxs-lookup"><span data-stu-id="527af-139">toosee hello logs for your container, click **View logs**.</span></span>

![Registos de Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="527af-141">Visualizar o seu serviço</span><span class="sxs-lookup"><span data-stu-id="527af-141">Viewing your service</span></span>
<span data-ttu-id="527af-142">Na adição toorunning os contentores Olá Kubernetes IU criou um externo `Service` que Aprovisiona a contentores de tráfego toohello com uma carga balanceador toobring no seu cluster.</span><span class="sxs-lookup"><span data-stu-id="527af-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="527af-143">No painel de navegação esquerdo Olá, clique em **serviços** tooview todos os serviços (deve haver apenas um).</span><span class="sxs-lookup"><span data-stu-id="527af-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Serviços de Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="527af-145">Nessa vista, deverá ver um ponto final externo (endereço IP) que foi alocado tooyour serviço.</span><span class="sxs-lookup"><span data-stu-id="527af-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="527af-146">Se clicar nesse endereço IP, deverá ver o contentor Nginx em execução por detrás do Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="527af-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![Vista de nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="527af-148">Redimensionar o seu serviço</span><span class="sxs-lookup"><span data-stu-id="527af-148">Resizing your service</span></span>
<span data-ttu-id="527af-149">Na adição tooviewing os seus objetos no Olá IU, pode editar e atualizar Olá Kubernetes API objetos.</span><span class="sxs-lookup"><span data-stu-id="527af-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="527af-150">Em primeiro lugar, clique em **implementações** no Olá deixado navegação painel toosee Olá implementação do serviço.</span><span class="sxs-lookup"><span data-stu-id="527af-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="527af-151">Assim que estiver nessa vista, clique no conjunto de réplicas Olá e, em seguida, clique em **editar** na barra de navegação superior Olá:</span><span class="sxs-lookup"><span data-stu-id="527af-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Editar Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="527af-153">Editar Olá `spec.replicas` campo toobe `2`e clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="527af-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="527af-154">Isto faz com que número de Olá de réplicas toodrop tootwo, eliminando um dos seus pods.</span><span class="sxs-lookup"><span data-stu-id="527af-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

