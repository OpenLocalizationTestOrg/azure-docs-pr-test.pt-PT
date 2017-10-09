# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="fd088-101">Se um cluster tooa ligação remota Kubernetes, DC/OS ou Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="fd088-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="fd088-102">Depois de criar um cluster do serviço de contentor do Azure, é necessário tooconnect toohello cluster toodeploy e gerir as cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fd088-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="fd088-103">Este artigo descreve como tooconnect toohello mestre VM de Olá cluster a partir de um computador remoto.</span><span class="sxs-lookup"><span data-stu-id="fd088-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="fd088-104">clusters de Olá Kubernetes, DC/OS e Docker Swarm fornecem pontos finais de HTTP localmente.</span><span class="sxs-lookup"><span data-stu-id="fd088-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="fd088-105">Para Kubernetes, este ponto final de forma segura está exposta no Olá internet e pode aceder ao mesmo executando Olá `kubectl` ferramenta da linha de comandos a partir de qualquer computador ligado à internet.</span><span class="sxs-lookup"><span data-stu-id="fd088-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="fd088-106">Para DC/OS e Docker Swarm, recomendamos que crie um túnel secure shell (SSH) do seu sistema de gestão de cluster do computador local toohello.</span><span class="sxs-lookup"><span data-stu-id="fd088-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="fd088-107">Uma vez estabelecido túnel Olá, pode executar os comandos que utilizam pontos finais HTTP Olá e interface web da vista Olá do orchestrator (se disponível) do sistema local.</span><span class="sxs-lookup"><span data-stu-id="fd088-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fd088-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fd088-108">Prerequisites</span></span>

* <span data-ttu-id="fd088-109">Um cluster do Kubernetes, DC/OS, Docker ou Swarm [implementado no Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="fd088-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="fd088-110">SSH RSA ficheiro de chave privada, correspondente toohello toohello adicionado de chave pública cluster durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="fd088-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="fd088-111">Estes comandos pressupõem que está a essa chave SSH privada Olá ser `$HOME/.ssh/id_rsa` no seu computador.</span><span class="sxs-lookup"><span data-stu-id="fd088-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="fd088-112">Veja estas instruções para [macOS e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md), para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="fd088-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="fd088-113">Se Olá ligação SSH não está a funcionar, poderá ser necessário demasiado [repor as chaves SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="fd088-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="fd088-114">Ligue tooa Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="fd088-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="fd088-115">Siga estes passos tooinstall e configurar `kubectl` no seu computador.</span><span class="sxs-lookup"><span data-stu-id="fd088-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="fd088-116">No Linux ou macOS, poderá ser necessário comandos Olá toorun esta secção utilizando `sudo`.</span><span class="sxs-lookup"><span data-stu-id="fd088-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="fd088-117">Instalar o kubectl</span><span class="sxs-lookup"><span data-stu-id="fd088-117">Install kubectl</span></span>
<span data-ttu-id="fd088-118">Uma forma tooinstall esta ferramenta é toouse Olá `az acs kubernetes install-cli` comandos de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="fd088-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="fd088-119">toorun este comando, certifique-se de que a [instalado](/cli/azure/install-az-cli2) Olá 2.0 de CLI do Azure mais recente e registado no tooan conta do Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="fd088-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="fd088-120">Em alternativa, pode transferir os mais recentes Olá `kubectl` cliente diretamente a partir de Olá [Kubernetes versões página](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="fd088-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="fd088-121">Para obter mais informações, consulte [Installing and Setting up kubectl (Instalar e Configurar o kubectl)](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="fd088-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="fd088-122">Transferir as credenciais do cluster</span><span class="sxs-lookup"><span data-stu-id="fd088-122">Download cluster credentials</span></span>
<span data-ttu-id="fd088-123">Assim que tiver `kubectl` instalado, terá de máquina de tooyour do toocopy Olá cluster credenciais.</span><span class="sxs-lookup"><span data-stu-id="fd088-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="fd088-124">As credenciais do toodo unidirecional get Olá é com Olá `az acs kubernetes get-credentials` comando.</span><span class="sxs-lookup"><span data-stu-id="fd088-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="fd088-125">Transmita o nome de Olá Olá do grupo de recursos e o nome de Olá do recurso de serviço de contentor Olá:</span><span class="sxs-lookup"><span data-stu-id="fd088-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="fd088-126">Este comando transfere as credenciais de cluster Olá demasiado`$HOME/.kube/config`, onde `kubectl` espera que toobe localizado.</span><span class="sxs-lookup"><span data-stu-id="fd088-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="fd088-127">Em alternativa, pode utilizar `scp` toosecurely copiar o ficheiro da Olá de `$HOME/.kube/config` no Olá mestre VM tooyour computador local.</span><span class="sxs-lookup"><span data-stu-id="fd088-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="fd088-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fd088-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="fd088-129">Se estiver no Windows, pode utilizar Bash no Ubuntu no Windows, o cliente de cópia de ficheiros segura PuTTy Olá ou uma ferramenta semelhante.</span><span class="sxs-lookup"><span data-stu-id="fd088-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="fd088-130">Utilizar o kubectl</span><span class="sxs-lookup"><span data-stu-id="fd088-130">Use kubectl</span></span>

<span data-ttu-id="fd088-131">Assim que tiver `kubectl` configurado, testar a ligação de Olá enumerando nós Olá do cluster:</span><span class="sxs-lookup"><span data-stu-id="fd088-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="fd088-132">Pode experimentar outros comandos do `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="fd088-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="fd088-133">Por exemplo, pode ver Olá Kubernetes Dashboard.</span><span class="sxs-lookup"><span data-stu-id="fd088-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="fd088-134">Primeiro, execute um proxy de servidor de Kubernetes API toohello:</span><span class="sxs-lookup"><span data-stu-id="fd088-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="fd088-135">Olá Kubernetes IU está agora disponível em: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="fd088-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="fd088-136">Para obter mais informações, consulte Olá [início rápido Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="fd088-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="fd088-137">Ligue o cluster de DC/OS ou Swarm tooa</span><span class="sxs-lookup"><span data-stu-id="fd088-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="fd088-138">Olá toouse DC/OS e Docker Swarm clusters implementados pelo serviço de contentor do Azure, siga estas instruções toocreate um túnel SSH do sistema local do Linux, macOS ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="fd088-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="fd088-139">Estas instruções centram-se no encapsulamento do tráfego TCP através de SSH.</span><span class="sxs-lookup"><span data-stu-id="fd088-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="fd088-140">Também pode iniciar uma sessão interativa de SSH com um dos sistemas de gestão de cluster interno Olá, mas não é recomendável.</span><span class="sxs-lookup"><span data-stu-id="fd088-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="fd088-141">Trabalhar diretamente num sistema interno acarreta riscos de fazer alterações à configuração inadvertidamente.</span><span class="sxs-lookup"><span data-stu-id="fd088-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="fd088-142">Criar um túnel SSH no Linux ou macOS</span><span class="sxs-lookup"><span data-stu-id="fd088-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="fd088-143">Olá primeira coisa que que fazer quando criar um túnel SSH no Linux ou macOS é toolocate Olá pública nome DNS Olá com balanceamento de carga modelos de estrutura mestres.</span><span class="sxs-lookup"><span data-stu-id="fd088-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="fd088-144">Siga estes passos.</span><span class="sxs-lookup"><span data-stu-id="fd088-144">Follow these steps:</span></span>


1. <span data-ttu-id="fd088-145">No Olá [portal do Azure](https://portal.azure.com), procure o grupo de recursos de toohello que contém o cluster do serviço de contentor.</span><span class="sxs-lookup"><span data-stu-id="fd088-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="fd088-146">Expanda o grupo de recursos de Olá, para que cada recurso é apresentado.</span><span class="sxs-lookup"><span data-stu-id="fd088-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="fd088-147">Clique em Olá **serviço de contentor** recursos e clique em **descrição geral**.</span><span class="sxs-lookup"><span data-stu-id="fd088-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="fd088-148">Olá **mestre FQDN** de Olá cluster aparecerá em **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="fd088-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="fd088-149">Guarde este nome para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="fd088-149">Save this name for later use.</span></span> 

    ![Nome DNS público](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="fd088-151">Em alternativa, execute Olá `az acs show` comando no seu serviço de contentor.</span><span class="sxs-lookup"><span data-stu-id="fd088-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="fd088-152">Procure Olá **mestre de perfil: fqdn** propriedade no resultado do comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd088-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="fd088-153">Agora, abra uma shell e execute Olá `ssh` comando, especificando Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="fd088-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="fd088-154">**LOCAL_PORT** é a porta TCP Olá no lado do serviço de Olá da Olá túnel tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="fd088-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="fd088-155">Para o Swarm, defina este too2375.</span><span class="sxs-lookup"><span data-stu-id="fd088-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="fd088-156">Para DC/OS, defina este too80.</span><span class="sxs-lookup"><span data-stu-id="fd088-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="fd088-157">**REMOTE_PORT** Olá é a porta do ponto final de Olá que pretende que o tooexpose.</span><span class="sxs-lookup"><span data-stu-id="fd088-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="fd088-158">Para Swarm, utilize a porta 2375.</span><span class="sxs-lookup"><span data-stu-id="fd088-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="fd088-159">Para o DC/OS, utilize a porta 80.</span><span class="sxs-lookup"><span data-stu-id="fd088-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="fd088-160">**Nome de utilizador** é o nome de utilizador de Olá fornecido quando implementou o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd088-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="fd088-161">**DNSPREFIX** é Olá prefixo DNS que forneceu quando implementou o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd088-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="fd088-162">**REGIÃO** região Olá em que o grupo de recursos está localizado.</span><span class="sxs-lookup"><span data-stu-id="fd088-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="fd088-163">**PATH_TO_PRIVATE_KEY** [opcional] é Olá caminho toohello chave privada que corresponde ao toohello chave pública que forneceu quando criou o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd088-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="fd088-164">Utilize esta opção com Olá `-i` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="fd088-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="fd088-165">Olá porta de ligação SSH é 2200 e não Olá porta padrão 22.</span><span class="sxs-lookup"><span data-stu-id="fd088-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="fd088-166">Num cluster com mais do que uma VM principal, este é Olá ligação porta toohello primeiro mestre de VM.</span><span class="sxs-lookup"><span data-stu-id="fd088-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="fd088-167">comando de Olá devolve sem saída.</span><span class="sxs-lookup"><span data-stu-id="fd088-167">hello command returns without output.</span></span>

<span data-ttu-id="fd088-168">Veja exemplos de Olá para DC/OS e Swarm no Olá seguintes secções:</span><span class="sxs-lookup"><span data-stu-id="fd088-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="fd088-169">Túnel do DC/OS</span><span class="sxs-lookup"><span data-stu-id="fd088-169">DC/OS tunnel</span></span>
<span data-ttu-id="fd088-170">tooopen um túnel para pontos finais de DC/OS, execute um comando semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd088-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="fd088-171">Certifique-se de que não tem outro processo local que vincule a porta 80.</span><span class="sxs-lookup"><span data-stu-id="fd088-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="fd088-172">Se necessário, pode especificar uma porta local diferente da 80, como a 8080.</span><span class="sxs-lookup"><span data-stu-id="fd088-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="fd088-173">Contudo, se utilizar esta porta, alguns links da IU da Web poderão não funcionar.</span><span class="sxs-lookup"><span data-stu-id="fd088-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="fd088-174">Agora pode aceder aos pontos finais de DC/SO Olá do sistema local através de Olá os seguintes URLs (assumindo que local porta 80):</span><span class="sxs-lookup"><span data-stu-id="fd088-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="fd088-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="fd088-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="fd088-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="fd088-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="fd088-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="fd088-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="fd088-178">Da mesma forma, pode atingir resto Olá das APIs para cada aplicação através deste túnel.</span><span class="sxs-lookup"><span data-stu-id="fd088-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="fd088-179">Túnel do Swarm</span><span class="sxs-lookup"><span data-stu-id="fd088-179">Swarm tunnel</span></span>
<span data-ttu-id="fd088-180">tooopen um túnel toohello ponto final Swarm, execute um comando semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd088-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="fd088-181">Certifique-se de que não tem outro processo local que vincule a porta 2375.</span><span class="sxs-lookup"><span data-stu-id="fd088-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="fd088-182">Por exemplo, se estiver a executar o daemon de Docker Olá localmente, é definido pela porta de toouse predefinida 2375.</span><span class="sxs-lookup"><span data-stu-id="fd088-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="fd088-183">Se necessário, pode especificar uma porta local diferente da 2375.</span><span class="sxs-lookup"><span data-stu-id="fd088-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="fd088-184">Agora pode aceder na cluster Docker Swarm Olá utilizando a interface de linha de comandos (CLI do Docker) do Olá Docker no sistema local.</span><span class="sxs-lookup"><span data-stu-id="fd088-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="fd088-185">Para instruções de instalação, veja [Instalar Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="fd088-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="fd088-186">Defina o toohello de variável de ambiente de DOCKER_HOST porta local configurado para túnel Olá.</span><span class="sxs-lookup"><span data-stu-id="fd088-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="fd088-187">Execute os comandos de Docker esse toohello túnel do cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="fd088-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="fd088-188">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fd088-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="fd088-189">Criar um túnel SSH no Windows</span><span class="sxs-lookup"><span data-stu-id="fd088-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="fd088-190">Existem várias opções para criar túneis SSH no Windows.</span><span class="sxs-lookup"><span data-stu-id="fd088-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="fd088-191">Se estiver a executar Bash no Ubuntu no Windows ou uma ferramenta semelhante, pode seguir as instruções de túnel de SSH de Olá mostradas anteriormente neste artigo para macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="fd088-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="fd088-192">Como alternativa no Windows, esta secção descreve como túnel de Olá toouse PuTTY toocreate.</span><span class="sxs-lookup"><span data-stu-id="fd088-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="fd088-193">[Transfira o PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="fd088-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="fd088-194">Execute a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="fd088-194">Run hello application.</span></span>

3. <span data-ttu-id="fd088-195">Introduza um nome de anfitrião que é composta por nome de utilizador de administrador de cluster Olá e o nome DNS público Olá Olá primeiro do mestre de no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd088-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="fd088-196">Olá **nome de anfitrião** semelhante demasiado`azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="fd088-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="fd088-197">Introduza 2200 para Olá **porta**.</span><span class="sxs-lookup"><span data-stu-id="fd088-197">Enter 2200 for hello **Port**.</span></span>

    ![Configuração do puTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="fd088-199">Selecione **SSH > Auth**. Adicione um caminho tooyour ficheiro de chave privada (*.ppk formato) para autenticação.</span><span class="sxs-lookup"><span data-stu-id="fd088-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="fd088-200">Pode utilizar uma ferramenta como [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate este ficheiro de Olá cluster de Olá toocreate utilizadas chaves de SSH.</span><span class="sxs-lookup"><span data-stu-id="fd088-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![Configuração do puTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="fd088-202">Selecione **SSH > túneis** e configure Olá seguintes portas reencaminhadas:</span><span class="sxs-lookup"><span data-stu-id="fd088-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="fd088-203">**Porta de Origem:** utilize a porta 80 para DC/OS ou a 2375 para Swarm.</span><span class="sxs-lookup"><span data-stu-id="fd088-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="fd088-204">**Destino:** utilize localhost:80 para DC/OS ou localhost:2375 para Swarm.</span><span class="sxs-lookup"><span data-stu-id="fd088-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="fd088-205">Olá seguinte o exemplo está configurado para DC/OS, mas será semelhante para Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="fd088-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fd088-206">A porta 80 não deve ser utilizada quando cria este túnel.</span><span class="sxs-lookup"><span data-stu-id="fd088-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Configuração do puTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="fd088-208">Quando tiver terminado, clique em **sessão > guardar** configuração da ligação toosave Olá.</span><span class="sxs-lookup"><span data-stu-id="fd088-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="fd088-209">tooconnect toohello sessão do PuTTY, clique em **abra**.</span><span class="sxs-lookup"><span data-stu-id="fd088-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="fd088-210">Quando se liga, pode ver a configuração da porta no registo de eventos do PuTTY Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="fd088-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![Registo de eventos do puTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="fd088-212">Depois de ter configurado o túnel de Olá para DC/OS, pode aceder Olá relacionadas com pontos finais em:</span><span class="sxs-lookup"><span data-stu-id="fd088-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="fd088-213">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="fd088-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="fd088-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="fd088-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="fd088-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="fd088-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="fd088-216">Depois de ter configurado o túnel de Olá para Docker Swarm, abra o tooconfigure de definições do Windows uma variável de ambiente de sistema com o nome `DOCKER_HOST` com um valor de `:2375`.</span><span class="sxs-lookup"><span data-stu-id="fd088-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="fd088-217">Em seguida, podem aceder cluster Swarm de Olá através de Olá CLI do Docker.</span><span class="sxs-lookup"><span data-stu-id="fd088-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd088-218">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fd088-218">Next steps</span></span>
<span data-ttu-id="fd088-219">Implementar e gerir contentores no seu cluster:</span><span class="sxs-lookup"><span data-stu-id="fd088-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="fd088-220">Trabalhar com o Azure Container Service e o Kubernetes</span><span class="sxs-lookup"><span data-stu-id="fd088-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="fd088-221">Trabalhar com o Azure Container Service e o DC/OS</span><span class="sxs-lookup"><span data-stu-id="fd088-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="fd088-222">Trabalhar com Olá serviço de contentor do Azure e Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="fd088-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

