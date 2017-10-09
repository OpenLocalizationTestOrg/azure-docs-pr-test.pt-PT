---
title: aaaQuickstart - cluster Kubernetes do Azure para Windows | Microsoft Docs
description: "Saiba rapidamente toocreate um cluster de Kubernetes para contentores do Windows no serviço de contentor do Azure com Olá CLI do Azure."
documentationcenter: 
author: dlepow
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
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="e9784-103">Implementar o cluster do Kubernetes para contentores do Windows</span><span class="sxs-lookup"><span data-stu-id="e9784-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="e9784-104">Olá CLI do Azure é utilizado toocreate e gerir recursos do Azure Olá linha de comandos ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="e9784-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="e9784-105">Detalhes deste Guia utilizando Olá CLI do Azure toodeploy um [Kubernetes](https://kubernetes.io/docs/home/) cluster no [serviço de contentor Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="e9784-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="e9784-106">Depois do cluster de Olá é implementado, ligar tooit com Olá Kubernetes `kubectl` ferramenta da linha de comandos e pretender implementa o primeiro contentor do Windows.</span><span class="sxs-lookup"><span data-stu-id="e9784-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="e9784-107">Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="e9784-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e9784-108">Se escolher tooinstall e utilizar Olá CLI localmente, este guia de introdução requer que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e9784-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e9784-109">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="e9784-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e9784-110">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e9784-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="e9784-111">O suporte para contentores do Windows com Kubernetes no Azure Container Service está em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="e9784-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="e9784-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e9784-112">Create a resource group</span></span>

<span data-ttu-id="e9784-113">Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e9784-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e9784-114">Um grupo de recursos do Azure é um grupo lógico, no qual os recursos do Azure são implementados e geridos.</span><span class="sxs-lookup"><span data-stu-id="e9784-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="e9784-115">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização.</span><span class="sxs-lookup"><span data-stu-id="e9784-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="e9784-116">Criar cluster do Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e9784-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="e9784-117">Criar um cluster de Kubernetes no serviço de contentor do Azure com Olá [az acs criar](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e9784-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="e9784-118">Olá exemplo seguinte cria um cluster com o nome *myK8sCluster* com o um Linux principal de nós e dois nós de agente do Windows.</span><span class="sxs-lookup"><span data-stu-id="e9784-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="e9784-119">Este exemplo cria SSH principal do Linux chaves tooconnect necessários toohello.</span><span class="sxs-lookup"><span data-stu-id="e9784-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="e9784-120">Este exemplo utiliza *azureuser* para um nome de utilizador administrativo e *myPassword12* como palavra-passe de Olá em nós do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e9784-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="e9784-121">Atualize o ambiente de tooyour adequada de toosomething estes valores.</span><span class="sxs-lookup"><span data-stu-id="e9784-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="e9784-122">Após vários minutos, o comando de Olá estiver concluída e mostra-lhe informações sobre a sua implementação.</span><span class="sxs-lookup"><span data-stu-id="e9784-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="e9784-123">Instalar o kubectl</span><span class="sxs-lookup"><span data-stu-id="e9784-123">Install kubectl</span></span>

<span data-ttu-id="e9784-124">tooconnect toohello Kubernetes cluster do computador cliente, utilize [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), cliente da linha de comandos do Olá Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e9784-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="e9784-125">Se estiver a utilizar o Azure CloudShell, `kubectl` já está instalado.</span><span class="sxs-lookup"><span data-stu-id="e9784-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="e9784-126">Se quiser tooinstall-la localmente, pode utilizar Olá [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="e9784-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="e9784-127">Olá a CLI do Azure exemplo instala os seguintes `kubectl` tooyour sistema.</span><span class="sxs-lookup"><span data-stu-id="e9784-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="e9784-128">No Windows, execute este comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="e9784-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="e9784-129">Ligar-se com kubectl</span><span class="sxs-lookup"><span data-stu-id="e9784-129">Connect with kubectl</span></span>

<span data-ttu-id="e9784-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, execute Olá [az acs kubernetes get-credenciais](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="e9784-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="e9784-131">Olá exemplo seguinte transfere para o seu cluster Kubernetes a configuração do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="e9784-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="e9784-132">tooverify Olá ligação tooyour cluster partir do seu computador, tente executar:</span><span class="sxs-lookup"><span data-stu-id="e9784-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="e9784-133">`kubectl`Apresenta uma lista de nós de Olá mestre e o agente.</span><span class="sxs-lookup"><span data-stu-id="e9784-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="e9784-134">Implementar um contentor do IIS do Windows</span><span class="sxs-lookup"><span data-stu-id="e9784-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="e9784-135">Pode executar um contentor do Docker dentro de um *pod* do Kubernetes, que contém um ou mais contentores.</span><span class="sxs-lookup"><span data-stu-id="e9784-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="e9784-136">Neste exemplo básico utiliza um toospecify de ficheiro JSON um contentor de servidor de informação Internet (IIS) da Microsoft e, em seguida, cria pod Olá utilizando Olá `kubctl apply` comando.</span><span class="sxs-lookup"><span data-stu-id="e9784-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="e9784-137">Criar um ficheiro local com o nome `iis.json` e Olá cópia seguindo texto.</span><span class="sxs-lookup"><span data-stu-id="e9784-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="e9784-138">Este ficheiro indica Kubernetes toorun IIS no servidor do Windows Server 2016 nano for apresentado, utilizando uma imagem de contentor público de [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="e9784-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="e9784-139">contentor de Olá utiliza a porta 80, mas inicialmente só é acessível na rede de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="e9784-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="e9784-140">toostart pod de Olá, tipo:</span><span class="sxs-lookup"><span data-stu-id="e9784-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="e9784-141">implementação de Olá tootrack, tipo:</span><span class="sxs-lookup"><span data-stu-id="e9784-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="e9784-142">Enquanto está a implementar pod Olá, o estado de Olá é `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="e9784-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="e9784-143">Pode demorar alguns minutos para Olá do Olá contentor tooenter `Running` estado.</span><span class="sxs-lookup"><span data-stu-id="e9784-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="e9784-144">Olá vista página de boas-vindas do IIS</span><span class="sxs-lookup"><span data-stu-id="e9784-144">View hello IIS welcome page</span></span>

<span data-ttu-id="e9784-145">tooexpose Olá pod toohello mundo com um endereço IP público, Olá tipo os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="e9784-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="e9784-146">Com este comando, Kubernetes cria um serviço e um [regra de Balanceador de carga do Azure](container-service-kubernetes-load-balancing.md) com um endereço IP público para o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="e9784-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="e9784-147">Execute Olá seguir o estado do comando toosee Olá do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="e9784-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="e9784-148">Endereço IP Olá aparece inicialmente como `pending`.</span><span class="sxs-lookup"><span data-stu-id="e9784-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="e9784-149">Após alguns minutos, Olá endereço IP externo de Olá `iis` pod está definido:</span><span class="sxs-lookup"><span data-stu-id="e9784-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="e9784-150">Pode utilizar um browser da sua choice toosee Olá predefinido IIS bem-vindo página no endereço IP externo de Olá:</span><span class="sxs-lookup"><span data-stu-id="e9784-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![Imagem de navegação tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="e9784-152">Eliminar o cluster</span><span class="sxs-lookup"><span data-stu-id="e9784-152">Delete cluster</span></span>
<span data-ttu-id="e9784-153">Quando o cluster de Olá já não é necessário, pode utilizar Olá [eliminação do grupo de az](/cli/azure/group#delete) comando o grupo de recursos do tooremove Olá, serviço de contentor e relacionados todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="e9784-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="e9784-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e9784-154">Next steps</span></span>

<span data-ttu-id="e9784-155">Neste guia de início rápido, implementou um cluster do Kubernetes, ligado a `kubectl`, e implementou um pod com um contentor IIS.</span><span class="sxs-lookup"><span data-stu-id="e9784-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="e9784-156">toolearn mais informações sobre o serviço de contentor do Azure, continuar toohello Kubernetes tutorial.</span><span class="sxs-lookup"><span data-stu-id="e9784-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e9784-157">Gerir um cluster do ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e9784-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
