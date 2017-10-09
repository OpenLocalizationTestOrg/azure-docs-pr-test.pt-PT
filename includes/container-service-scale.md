# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="25db5-101">Dimensionar nós de agente num cluster do Container Service</span><span class="sxs-lookup"><span data-stu-id="25db5-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="25db5-102">Depois de [implementar um cluster do serviço de contentor Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), poderá ser necessário toochange Olá diversas nós de agente.</span><span class="sxs-lookup"><span data-stu-id="25db5-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="25db5-103">Por exemplo, poderá precisar de mais agentes, de modo a poder executar mais aplicações de contentores ou instâncias.</span><span class="sxs-lookup"><span data-stu-id="25db5-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="25db5-104">Pode alterar o número de Olá de nós de agente de um cluster DC/OS, Docker Swarm ou Kubernetes utilizando Olá portal do Azure ou Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="25db5-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="25db5-105">Dimensionar com Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="25db5-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="25db5-106">No Olá [portal do Azure](https://portal.azure.com), procure **serviços de contentor**e, em seguida, clique em serviço de contentor Olá que pretende que o toomodify.</span><span class="sxs-lookup"><span data-stu-id="25db5-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="25db5-107">No Olá **serviço de contentor** painel, clique em **agentes**.</span><span class="sxs-lookup"><span data-stu-id="25db5-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="25db5-108">No **contagem de VM**, introduza o número de Olá pretendido de nós de agentes.</span><span class="sxs-lookup"><span data-stu-id="25db5-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Um agrupamento no portal de Olá de escala](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="25db5-110">configuração de Olá toosave, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="25db5-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="25db5-111">Dimensionar com Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="25db5-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="25db5-112">Certifique-se de que a [instalado](/cli/azure/install-az-cli2) Olá 2.0 de CLI do Azure mais recente e registado no tooan conta do azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="25db5-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="25db5-113">Consulte a contagem de agentes Olá atual</span><span class="sxs-lookup"><span data-stu-id="25db5-113">See hello current agent count</span></span>
<span data-ttu-id="25db5-114">número de Olá toosee de agentes atualmente num cluster de Olá, execute Olá `az acs show` comando.</span><span class="sxs-lookup"><span data-stu-id="25db5-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="25db5-115">Isto mostra a configuração de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="25db5-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="25db5-116">Por exemplo, Olá a seguir mostra Olá configuração do serviço de contentor Olá com o nome do comando `containerservice-myACSName` no grupo de recursos de Olá `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="25db5-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="25db5-117">comando Olá devolve o número de Olá de agentes no Olá `Count` valor em `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="25db5-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="25db5-118">Utilize Olá az comando da escala de acs</span><span class="sxs-lookup"><span data-stu-id="25db5-118">Use hello az acs scale command</span></span>
<span data-ttu-id="25db5-119">número de Olá toochange de nós de agente, execute Olá `az acs scale` Olá de comando e de alimentação **grupo de recursos**, **nome do serviço de contentor**e Olá pretendido **nova contagem de agente**.</span><span class="sxs-lookup"><span data-stu-id="25db5-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="25db5-120">Ao utilizar um número mais pequeno ou maior, pode reduzir ou aumentar de forma vertical, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="25db5-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="25db5-121">Por exemplo, o número de Olá toochange de agentes Olá anterior too10 de cluster, escreva Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="25db5-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="25db5-122">Olá, Azure CLI 2.0 devolve uma cadeia JSON que representa a nova configuração de Olá do serviço de contentor Olá, incluindo a nova contagem de agente Olá.</span><span class="sxs-lookup"><span data-stu-id="25db5-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="25db5-123">Para obter mais opções de comandos, execute `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="25db5-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="25db5-124">Considerações sobre o dimensionamento</span><span class="sxs-lookup"><span data-stu-id="25db5-124">Scaling considerations</span></span>

* <span data-ttu-id="25db5-125">número de Olá de nós de agente tem de ser entre 1 e 100, inclusive.</span><span class="sxs-lookup"><span data-stu-id="25db5-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="25db5-126">A quota de núcleos pode limitar o número de Olá de nós de agente num cluster.</span><span class="sxs-lookup"><span data-stu-id="25db5-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="25db5-127">Operações de dimensionamento de nó de agente são aplicados tooan conjunto de dimensionamento da máquina virtual do Azure que contém o agrupamento de agentes Olá.</span><span class="sxs-lookup"><span data-stu-id="25db5-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="25db5-128">Num cluster DC/OS, apenas nós de agente no conjunto de privada Olá são ampliados por operações Olá apresentadas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="25db5-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="25db5-129">Consoante o orchestrator de Olá que implementar no seu cluster, pode dimensionar separadamente número Olá de instâncias de um contentor em execução no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="25db5-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="25db5-130">Por exemplo, num cluster DC/OS, utilize Olá [IU do Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange Olá diversas instâncias de uma aplicação de contentor.</span><span class="sxs-lookup"><span data-stu-id="25db5-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="25db5-131">Atualmente, o dimensionamento automático de nós de agentes em clusters de serviços de contentores não é suportado.</span><span class="sxs-lookup"><span data-stu-id="25db5-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25db5-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="25db5-132">Next steps</span></span>
* <span data-ttu-id="25db5-133">Veja [mais exemplos](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) da utilização de comandos da CLI 2.0 do Azure com o Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="25db5-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="25db5-134">Saiba mais sobre os [conjuntos de agentes do DC/SO](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) no Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="25db5-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

