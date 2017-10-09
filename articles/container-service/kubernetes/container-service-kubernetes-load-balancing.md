---
title: aaaLoad equilibrar Kubernetes contentores no Azure | Microsoft Docs
description: "Ligue externamente e o balanceamento de carga entre vários contentores num cluster Kubernetes no serviço de contentor do Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contentores, microserviços, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="6ad07-104">Contentores de balanceamento de carga num cluster Kubernetes no serviço de contentor do Azure</span><span class="sxs-lookup"><span data-stu-id="6ad07-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="6ad07-105">Este artigo apresenta balanceamento de carga no cluster Kubernetes no serviço de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ad07-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="6ad07-106">Balanceamento de carga fornece um endereço IP externamente acessível para o serviço de Olá e distribui o tráfego de rede entre pods Olá em execução em VMs do agente.</span><span class="sxs-lookup"><span data-stu-id="6ad07-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="6ad07-107">Pode configurar um toouse de serviço Kubernetes [Balanceador de carga do Azure](../../load-balancer/load-balancer-overview.md) toomanage externo tráfego de rede (TCP).</span><span class="sxs-lookup"><span data-stu-id="6ad07-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="6ad07-108">Sem configuração adicional, a carga de balanceamento e o encaminhamento de tráfego HTTP ou HTTPS ou cenários mais avançados é possível.</span><span class="sxs-lookup"><span data-stu-id="6ad07-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ad07-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6ad07-109">Prerequisites</span></span>
* <span data-ttu-id="6ad07-110">[Implementar um cluster de Kubernetes](container-service-kubernetes-walkthrough.md) no serviço de contentor do Azure</span><span class="sxs-lookup"><span data-stu-id="6ad07-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="6ad07-111">[Ligar o seu cliente](../container-service-connect.md) tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="6ad07-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="6ad07-112">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="6ad07-112">Azure load balancer</span></span>

<span data-ttu-id="6ad07-113">Por predefinição, um cluster de Kubernetes implementado no serviço de contentor do Azure inclui um balanceador de carga do Azure para a Internet para o agente de Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="6ad07-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="6ad07-114">(Um recurso de Balanceador de carga individual está configurado para mestre Olá VMs.) Balanceador de carga do Azure é um balanceador de carga de camada 4.</span><span class="sxs-lookup"><span data-stu-id="6ad07-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="6ad07-115">Atualmente, o Balanceador de carga Olá suporta apenas a tráfego TCP no Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6ad07-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="6ad07-116">Ao criar um serviço Kubernetes, podem configurar automaticamente o serviço de toohello de acesso de tooallow Balanceador de carga do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="6ad07-117">Balanceador de carga de Olá tooconfigure, conjunto Olá serviço `type` demasiado`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="6ad07-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="6ad07-118">Balanceador de carga Olá cria uma regra toomap um endereço IP público e número de porta de receber tráfego toohello privados IP endereços de serviço e números de porta de pods de Olá no agente VMs (e vice-versa para o tráfego de resposta).</span><span class="sxs-lookup"><span data-stu-id="6ad07-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="6ad07-119">Seguem-se dois exemplos que mostra como tooset Olá Kubernetes serviço `type` demasiado`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="6ad07-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="6ad07-120">(Depois tentar exemplos de Olá, eliminar as implementações de Olá se já não precisar delas.)</span><span class="sxs-lookup"><span data-stu-id="6ad07-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="6ad07-121">Exemplo: Olá de utilização `kubectl expose` comando</span><span class="sxs-lookup"><span data-stu-id="6ad07-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="6ad07-122">Olá [Kubernetes instruções](container-service-kubernetes-walkthrough.md) inclui um exemplo de como tooexpose um serviço com Olá `kubectl expose` comando e a respetiva `--type=LoadBalancer` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="6ad07-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="6ad07-123">Eis os passos de Olá:</span><span class="sxs-lookup"><span data-stu-id="6ad07-123">Here are hello steps :</span></span>

1. <span data-ttu-id="6ad07-124">Inicie uma nova implementação do contentor.</span><span class="sxs-lookup"><span data-stu-id="6ad07-124">Start a new container deployment.</span></span> <span data-ttu-id="6ad07-125">Por exemplo, Olá seguir inicia comando chamada de uma nova implementação `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="6ad07-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="6ad07-126">implementação de Olá consiste em três contentores com base na imagem de Docker Olá para o servidor de web Olá Nginx.</span><span class="sxs-lookup"><span data-stu-id="6ad07-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="6ad07-127">Certifique-se de que os contentores de Olá estão em execução.</span><span class="sxs-lookup"><span data-stu-id="6ad07-127">Verify that hello containers are running.</span></span> <span data-ttu-id="6ad07-128">Por exemplo, se consultar para contentores de Olá com `kubectl get pods`, consulte o seguinte de toohello semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="6ad07-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Obter contentores Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="6ad07-130">tooconfigure Olá carga balanceador tooaccept tráfego externo toohello implementação, execute `kubectl expose` com `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="6ad07-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="6ad07-131">Olá seguinte comando expõe servidor de Nginx Olá na porta 80:</span><span class="sxs-lookup"><span data-stu-id="6ad07-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="6ad07-132">Tipo `kubectl get svc` estado de Olá toosee dos serviços de Olá num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="6ad07-133">Enquanto o Balanceador de carga Olá configura a regra de Olá, Olá `EXTERNAL-IP` de Olá serviço aparece como `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="6ad07-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="6ad07-134">Após alguns minutos, é configurado o endereço IP externo de Olá:</span><span class="sxs-lookup"><span data-stu-id="6ad07-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurar o Balanceador de carga do Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="6ad07-136">Certifique-se de que pode aceder ao serviço de Olá no endereço IP externo de Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="6ad07-137">Por exemplo, abra um endereço IP do web browser toohello mostrado.</span><span class="sxs-lookup"><span data-stu-id="6ad07-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="6ad07-138">browser de Olá mostra Olá Nginx web servidor a executar dos contentores Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="6ad07-139">Em alternativa, execute Olá `curl` ou `wget` comando.</span><span class="sxs-lookup"><span data-stu-id="6ad07-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="6ad07-140">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6ad07-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="6ad07-141">Deverá ver uma saída semelhante a:</span><span class="sxs-lookup"><span data-stu-id="6ad07-141">You should see output similar to:</span></span>

    ![Acesso Nginx com curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="6ad07-143">configuração de Olá toosee Olá do Azure de Balanceador de carga, aceda toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6ad07-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="6ad07-144">Navegue para o grupo de recursos de Olá para o cluster do serviço de contentor e selecione o Balanceador de carga Olá para o agente de Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="6ad07-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="6ad07-145">O nome deve ser Olá, mesmo que o serviço de contentor Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="6ad07-146">(Não escolha Balanceador de carga Olá para nós principais Olá, Olá um cujo nome inclui **master-lb**.)</span><span class="sxs-lookup"><span data-stu-id="6ad07-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![Balanceador de carga no grupo de recursos](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="6ad07-148">detalhes de Olá toosee da configuração de Balanceador de carga Olá, clique em **as regras de balanceamento de carga** e o nome de Olá Olá de regra de que foi configurada.</span><span class="sxs-lookup"><span data-stu-id="6ad07-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![Regras de Balanceador de carga](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="6ad07-150">Exemplo: Especificar `type: LoadBalancer` no ficheiro de configuração do serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="6ad07-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="6ad07-151">Se implementar uma aplicação de contentor Kubernetes de JSON ou YAML [ficheiro de configuração do serviço](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), especifique um balanceador de carga externo, adicionando Olá especificação de serviço linha toohello os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6ad07-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="6ad07-152">Olá passos seguintes utilizam Olá Kubernetes [Guestbook exemplo](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="6ad07-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="6ad07-153">Neste exemplo é uma aplicação web de várias camadas com base nas imagens de Redis e PHP Docker.</span><span class="sxs-lookup"><span data-stu-id="6ad07-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="6ad07-154">Pode especificar no ficheiro de configuração do serviço de Olá que Olá front-end PHP o servidor utiliza o Balanceador de carga do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="6ad07-155">Transferir o ficheiro de Olá `guestbook-all-in-one.yaml` de [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="6ad07-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="6ad07-156">Procurar Olá `spec` para Olá `frontend` serviço.</span><span class="sxs-lookup"><span data-stu-id="6ad07-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="6ad07-157">Anule os comentários linha Olá `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="6ad07-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![Balanceador de carga na configuração do serviço](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="6ad07-159">Guarde o ficheiro de Olá e implementar a aplicação Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6ad07-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="6ad07-160">Tipo `kubectl get svc` estado de Olá toosee dos serviços de Olá num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="6ad07-161">Enquanto o Balanceador de carga Olá configura a regra de Olá, Olá `EXTERNAL-IP` de Olá `frontend` serviço aparece como `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="6ad07-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="6ad07-162">Após alguns minutos, é configurado o endereço IP externo de Olá:</span><span class="sxs-lookup"><span data-stu-id="6ad07-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurar o Balanceador de carga do Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="6ad07-164">Certifique-se de que pode aceder ao serviço de Olá no endereço IP externo de Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="6ad07-165">Por exemplo, pode abrir um web browser toohello endereço IP externo do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![Acesso guestbook externamente](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="6ad07-167">Pode adicionar guestbook entradas.</span><span class="sxs-lookup"><span data-stu-id="6ad07-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="6ad07-168">configuração de Olá toosee Olá do Azure de Balanceador de carga, navegue para o recurso de Balanceador de carga Olá para cluster Olá Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6ad07-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6ad07-169">Consulte os passos Olá no exemplo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="6ad07-170">Considerações</span><span class="sxs-lookup"><span data-stu-id="6ad07-170">Considerations</span></span>

* <span data-ttu-id="6ad07-171">A criação de regra de Balanceador de carga Olá acontece de forma assíncrona e informações sobre o Balanceador de Olá aprovisionado são publicadas no serviço de Olá `status.loadBalancer` campo.</span><span class="sxs-lookup"><span data-stu-id="6ad07-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="6ad07-172">Cada serviço é atribuído automaticamente o seu próprio endereço IP virtual no balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="6ad07-173">Se quiser Balanceador de carga de Olá tooreach por um nome DNS, trabalhar com o seu toocreate de fornecedor de serviço de domínio um nome DNS para endereço IP da regra de Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="6ad07-174">Tráfego HTTP ou HTTPS</span><span class="sxs-lookup"><span data-stu-id="6ad07-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="6ad07-175">Saldo de tooload HTTP ou HTTPS tráfego toocontainer aplicações web e gerir certificados de segurança de camada de transporte (TLS), pode utilizar Olá Kubernetes [entrada](https://kubernetes.io/docs/user-guide/ingress/) recursos.</span><span class="sxs-lookup"><span data-stu-id="6ad07-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="6ad07-176">Uma entrada é uma coleção de regras que permitem ligações de entrada serviços de cluster de Olá tooreach.</span><span class="sxs-lookup"><span data-stu-id="6ad07-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="6ad07-177">Para um toowork de recurso de entrada, cluster de Kubernetes Olá tem de ter um [controlador entrada](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) em execução.</span><span class="sxs-lookup"><span data-stu-id="6ad07-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="6ad07-178">Serviço de contentor do Azure não implementa um controlador de entrada Kubernetes automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6ad07-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="6ad07-179">Estão disponíveis várias implementações de controlador.</span><span class="sxs-lookup"><span data-stu-id="6ad07-179">Several controller implementations are available.</span></span> <span data-ttu-id="6ad07-180">Atualmente, Olá [controlador Nginx entrada](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) recomenda tooconfigure regras de entrada e de balanceamento de carga de tráfego HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6ad07-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="6ad07-181">Para obter mais informações, consulte Olá [documentação do controlador de entrada Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="6ad07-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ad07-182">Quando utilizar Olá controlador Nginx entrada no serviço de contentor do Azure, tem de expor como um serviço com a implementação do controlador de Olá `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="6ad07-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="6ad07-183">Esta ação configura o controlador de toohello de tráfego de tooroute Balanceador de carga do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="6ad07-184">Para obter mais informações, consulte a secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="6ad07-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6ad07-185">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6ad07-185">Next steps</span></span>

* <span data-ttu-id="6ad07-186">Consulte Olá [Kubernetes LoadBalancer documentação](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="6ad07-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="6ad07-187">Saiba mais sobre [controladores Kubernetes entrada e de entrada](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="6ad07-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="6ad07-188">Consulte [Kubernetes exemplos](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="6ad07-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

