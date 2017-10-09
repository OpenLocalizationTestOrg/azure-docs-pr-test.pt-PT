---
title: "cluster de Azure Kubernetes aaaMonitor - operações de gestão | Microsoft Docs"
description: "Monitorização de Kubernetes cluster no serviço de contentor Azure utilizando o Microsoft Operations Management Suite"
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="d34e1-103">Monitor de um cluster do serviço de contentor do Azure com o Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="d34e1-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d34e1-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d34e1-104">Prerequisites</span></span>
<span data-ttu-id="d34e1-105">Esta instrução parte do princípio de que tem [criado um cluster de Kubernetes utilizando o serviço de contentor do Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d34e1-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="d34e1-106">Também parte do princípio que tem Olá `az` cli do Azure e `kubectl` as ferramentas instaladas.</span><span class="sxs-lookup"><span data-stu-id="d34e1-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="d34e1-107">Pode testar se tiver Olá `az` ferramenta instalada através da execução:</span><span class="sxs-lookup"><span data-stu-id="d34e1-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="d34e1-108">Se não tiver Olá `az` ferramenta instalada, existem instruções [aqui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="d34e1-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="d34e1-109">Em alternativa, pode utilizar [Shell de nuvem do Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), que tem Olá `az` cli do Azure e `kubectl` ferramentas já instaladas por si.</span><span class="sxs-lookup"><span data-stu-id="d34e1-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="d34e1-110">Pode testar se tiver Olá `kubectl` ferramenta instalada através da execução:</span><span class="sxs-lookup"><span data-stu-id="d34e1-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="d34e1-111">Se não tiver `kubectl` instalado, pode executar:</span><span class="sxs-lookup"><span data-stu-id="d34e1-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="d34e1-112">tootest se tiver chaves kubernetes instaladas na sua ferramenta kubectl pode executar:</span><span class="sxs-lookup"><span data-stu-id="d34e1-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="d34e1-113">Se hello acima erros de comando terminar, terá das chaves de cluster do tooinstall kubernetes para a ferramenta de kubectl.</span><span class="sxs-lookup"><span data-stu-id="d34e1-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="d34e1-114">Pode fazê-lo com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d34e1-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="d34e1-115">Contentores de monitorização no Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="d34e1-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="d34e1-116">Gestão de operações do Microsoft (OMS) é baseado na nuvem IT solução de gestão que o ajuda a gerir e proteger no local e a infraestrutura de nuvem. da Microsoft</span><span class="sxs-lookup"><span data-stu-id="d34e1-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="d34e1-117">Contentor é uma solução na análise de registos do OMS, que ajuda-o a ver Olá contentor o inventário, o desempenho e registos numa única localização.</span><span class="sxs-lookup"><span data-stu-id="d34e1-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="d34e1-118">Pode de auditoria, resolver problemas de contentores através da visualização de registos de Olá numa localização centralizada e localizar inúteis consumir contentor em excesso num anfitrião.</span><span class="sxs-lookup"><span data-stu-id="d34e1-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="d34e1-119">Para obter mais informações sobre a solução de contentor, consulte toothe [análise de registos do contentor solução](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="d34e1-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="d34e1-120">Instalar OMS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d34e1-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="d34e1-121">Obter o ID da área de trabalho e a chave</span><span class="sxs-lookup"><span data-stu-id="d34e1-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="d34e1-122">Para Olá serviço toohello tootalk de agente do OMS tem toobe configurado com um id de área de trabalho e uma chave de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d34e1-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="d34e1-123">tooget Olá id e a chave tem de toocreate um OMS conta em <https://mms.microsoft.com>. Siga os passos de Olá toocreate uma conta.</span><span class="sxs-lookup"><span data-stu-id="d34e1-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="d34e1-124">Quando tiver terminado a criar conta de Olá, terá de tooobtain o id e a chave clicando **definições**, em seguida, **origens ligadas**e, em seguida, **servidores Linux**, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d34e1-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="d34e1-125">Instalar o agente do OMS Olá utilizando um DaemonSet</span><span class="sxs-lookup"><span data-stu-id="d34e1-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="d34e1-126">DaemonSets são utilizadas pelo Kubernetes toorun uma única instância de um contentor em cada anfitrião no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="d34e1-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="d34e1-127">Se estiver a perfeita para a execução de agentes de monitorização.</span><span class="sxs-lookup"><span data-stu-id="d34e1-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="d34e1-128">Eis Olá [ficheiro DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="d34e1-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="d34e1-129">Guarde este ficheiro de tooa denominado `oms-daemonset.yaml` e substitua os valores de marcador de posição-Olá para `WSID` e `KEY` com o id da área de trabalho e a chave no ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="d34e1-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="d34e1-130">Depois de adicionar o seu ID de área de trabalho e a chave toohello DaemonSet configuração, pode instalar o agente do OMS Olá no seu cluster com Olá `kubectl` ferramenta de linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="d34e1-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="d34e1-131">Instalar o agente do OMS Olá utilizando um segredo Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d34e1-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="d34e1-132">tooprotect o ID da área de trabalho OMS e a chave, pode utilizar o segredo Kubernetes como parte do ficheiro de DaemonSet YAML.</span><span class="sxs-lookup"><span data-stu-id="d34e1-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="d34e1-133">Copie o script Olá, o ficheiro de modelo secreta e Olá ficheiro DaemonSet YAML (de [repositório](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) e certifique-se de que estão na Olá mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="d34e1-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="d34e1-134">segredo gerar script - gen.sh segredo</span><span class="sxs-lookup"><span data-stu-id="d34e1-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="d34e1-135">modelo secreto - template.yaml segredo</span><span class="sxs-lookup"><span data-stu-id="d34e1-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="d34e1-136">Ficheiro DaemonSet YAML - omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="d34e1-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="d34e1-137">Execute script de Olá.</span><span class="sxs-lookup"><span data-stu-id="d34e1-137">Run hello script.</span></span> <span data-ttu-id="d34e1-138">script de Olá pedirá para Olá ID da área de trabalho OMS e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="d34e1-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="d34e1-139">Insira o que e script Olá irá criar um ficheiro de yaml secreta, pelo que pode executá-lo.</span><span class="sxs-lookup"><span data-stu-id="d34e1-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="d34e1-140">Crie pod de segredos Olá, executando Olá seguinte:``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="d34e1-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="d34e1-141">toocheck, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="d34e1-141">toocheck, run hello following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="d34e1-142">Criar a sua omsagent daemon-set executando``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="d34e1-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="d34e1-143">Conclusão</span><span class="sxs-lookup"><span data-stu-id="d34e1-143">Conclusion</span></span>
<span data-ttu-id="d34e1-144">Já está!</span><span class="sxs-lookup"><span data-stu-id="d34e1-144">That's it!</span></span> <span data-ttu-id="d34e1-145">Após alguns minutos, deve ser dados toosee capaz de fluir tooyour dashboard do OMS.</span><span class="sxs-lookup"><span data-stu-id="d34e1-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
