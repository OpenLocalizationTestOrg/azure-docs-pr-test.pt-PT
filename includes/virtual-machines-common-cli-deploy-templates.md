
* [<span data-ttu-id="9a87a-101">Criar rapidamente uma máquina virtual no Azure</span><span class="sxs-lookup"><span data-stu-id="9a87a-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="9a87a-102">Implementar uma máquina virtual no Azure a partir de um modelo</span><span class="sxs-lookup"><span data-stu-id="9a87a-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="9a87a-103">Criar uma máquina virtual a partir de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="9a87a-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="9a87a-104">Implementar uma máquina virtual que utiliza uma rede virtual e um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="9a87a-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="9a87a-105">Remover um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9a87a-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="9a87a-106">Mostrar o registo de Olá para uma implementação de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9a87a-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="9a87a-107">Apresentar informações sobre uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9a87a-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="9a87a-108">Ligar a máquina virtual baseado em Linux no tooa</span><span class="sxs-lookup"><span data-stu-id="9a87a-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="9a87a-109">Parar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9a87a-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="9a87a-110">Iniciar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9a87a-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="9a87a-111">Anexar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="9a87a-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="9a87a-112">Preparação</span><span class="sxs-lookup"><span data-stu-id="9a87a-112">Getting ready</span></span>
<span data-ttu-id="9a87a-113">Antes de poder utilizar Olá CLI do Azure com grupos de recursos do Azure, terá de versão do toohave Olá certa CLI do Azure e uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a87a-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="9a87a-114">Se não tiver Olá CLI do Azure, [instalá-lo](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9a87a-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="9a87a-115">Atualizar o seu too0.9.0 de versão da CLI do Azure ou posterior</span><span class="sxs-lookup"><span data-stu-id="9a87a-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="9a87a-116">Tipo `azure --version` toosee se já tiver instalado uma versão 0.9.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9a87a-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="9a87a-117">Se a sua versão não 0.9.0 ou posterior, terá de tooupdate Olá-lo utilizando um dos programas de instalação nativos ou através de **npm** escrevendo `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="9a87a-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="9a87a-118">Também pode executar CLI do Azure como um contentor de Docker utilizando o seguinte Olá [imagem Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="9a87a-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="9a87a-119">A partir de um anfitrião de Docker, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9a87a-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="9a87a-120">Definir a conta e a subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="9a87a-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="9a87a-121">Se ainda não tiver uma subscrição do Azure, mas já tiver uma subscrição do MSDN, pode ativar os seus [benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="9a87a-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="9a87a-122">Também se pode inscreve numa [versão de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a87a-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="9a87a-123">Agora [iniciar sessão na conta do Azure de tooyour interativamente](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) escrevendo `azure login` e seguir Olá pede um tooyour de experiência de início de sessão interativo conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a87a-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="9a87a-124">Se tiver um trabalho ou escola ID e saber o não dispõe de autenticação de dois fatores ativada, poderá **também** utilizar `azure login -u` juntamente com Olá escolar ou profissional do ID toolog no *sem* uma sessão interativa.</span><span class="sxs-lookup"><span data-stu-id="9a87a-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="9a87a-125">Se não tiver um trabalho ou escola ID, pode [criar um id de conta escolar ou profissional da sua conta Microsoft pessoal](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog no Olá mesma forma.</span><span class="sxs-lookup"><span data-stu-id="9a87a-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="9a87a-126">A sua conta pode ter mais de uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="9a87a-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="9a87a-127">Pode escrever `azure account list` para listar as subscrições, o que poderá ser parecido com:</span><span class="sxs-lookup"><span data-stu-id="9a87a-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="9a87a-128">Pode definir a subscrição do Azure atual de Olá, escrevendo Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="9a87a-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="9a87a-129">Utilize Olá nome ou Olá ID de subscrição com recursos de Olá pretende toomanage.</span><span class="sxs-lookup"><span data-stu-id="9a87a-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="9a87a-130">Mudar o modo de grupo de recursos toohello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9a87a-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="9a87a-131">Por predefinição, o Olá CLI do Azure é iniciado no modo de gestão do serviço de Olá (**asm** modo).</span><span class="sxs-lookup"><span data-stu-id="9a87a-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="9a87a-132">Seguir o modo de grupo tooswitch tooresource Olá de tipo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="9a87a-133">Compreender os modelos de recursos e os grupos de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="9a87a-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="9a87a-134">A maioria das aplicações são criadas com base numa combinação de diferentes tipos de recursos (como uma ou mais VMs e contas de armazenamento, uma base de dados SQL, uma rede virtual ou uma rede de entrega de conteúdos).</span><span class="sxs-lookup"><span data-stu-id="9a87a-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="9a87a-135">Olá, API de gestão de serviço do Azure a predefinição e hello portal clássico do Azure representado estes itens, utilizando uma abordagem de serviço ao serviço.</span><span class="sxs-lookup"><span data-stu-id="9a87a-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="9a87a-136">Esta abordagem requer que toodeploy e gerir serviços individuais Olá individualmente (ou encontrar outras ferramentas que fazê-lo) e não como uma única unidade lógica de implementação.</span><span class="sxs-lookup"><span data-stu-id="9a87a-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="9a87a-137">*Modelos Azure Resource Manager*, no entanto, que lhe toodeploy e gerir estes recursos diferentes como uma unidade lógica de implementação de forma declarativa.</span><span class="sxs-lookup"><span data-stu-id="9a87a-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="9a87a-138">Em vez de imperatively informar do Azure que toodeploy um comando após a outra, que descreve a implementação de toda um ficheiro JSON – todos os recursos de Olá e configuração associados e parâmetros de implementação – e dizer Azure toodeploy esses recursos como um grupo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="9a87a-139">Em seguida, pode gerir Olá geral do ciclo de vida dos recursos do grupo de Olá utilizando comandos de gestão de recursos de CLI do Azure para:</span><span class="sxs-lookup"><span data-stu-id="9a87a-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="9a87a-140">Parar, iniciar ou eliminar todos os recursos de Olá dentro do grupo de Olá em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="9a87a-141">Aplica regras de controlo de acesso baseado em funções (RBAC) toolock baixo permissões de segurança nos mesmos.</span><span class="sxs-lookup"><span data-stu-id="9a87a-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="9a87a-142">Auditar operações.</span><span class="sxs-lookup"><span data-stu-id="9a87a-142">Audit operations.</span></span>
* <span data-ttu-id="9a87a-143">Etiquetar recursos com metadados adicionais para um melhor controlo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="9a87a-144">Pode saber mais sobre os grupos de recursos do Azure e o que podem fazer por si no Olá muitos [descrição geral do Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a87a-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="9a87a-145">Se estiver interessado em criar modelos, veja [Authoring Azure Resource Manager templates (Criar modelos do Azure Resource Manager)](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9a87a-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="9a87a-146"><a id="quick-create-a-vm-in-azure"></a>Tarefa: Criar rapidamente uma VM no Azure</span><span class="sxs-lookup"><span data-stu-id="9a87a-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="9a87a-147">Por vezes, sabe que imagem for necessário, e tem agora uma VM a partir dessa imagem e não se preocupar muito infraestrutura Olá – talvez tiver tootest algo numa VM limpa.</span><span class="sxs-lookup"><span data-stu-id="9a87a-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="9a87a-148">Que é quando pretender toouse Olá `azure vm quick-create` de comandos e passar Olá argumentos necessários toocreate uma VM e a respetiva infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="9a87a-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="9a87a-149">O primeiro passo é criar o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9a87a-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="9a87a-150">Depois, vai precisar de uma imagem.</span><span class="sxs-lookup"><span data-stu-id="9a87a-150">Second, you'll need an image.</span></span> <span data-ttu-id="9a87a-151">toofind uma imagem com Olá CLI do Azure, consulte [Navigating e selecionar imagens da máquina virtual do Azure com o PowerShell e Olá CLI do Azure](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a87a-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9a87a-152">Contudo, segue-se uma lista de imagens populares no âmbito deste artigo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="9a87a-153">Vamos utilizar a imagem Stable do CoreOS nesta criação rápida.</span><span class="sxs-lookup"><span data-stu-id="9a87a-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="9a87a-154">Para ComputeImageVersion, pode também simplesmente fornecer 'mais recente' como Olá parâmetro em ambos os idiomas de modelo Olá e em Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a87a-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="9a87a-155">Isto permitirá que tooalways utiliza a versão mais recente e corrigido Olá da imagem de Olá sem ter toomodify os scripts ou modelos.</span><span class="sxs-lookup"><span data-stu-id="9a87a-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="9a87a-156">Isto é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="9a87a-157">Nome do Editor</span><span class="sxs-lookup"><span data-stu-id="9a87a-157">PublisherName</span></span> | <span data-ttu-id="9a87a-158">Oferta</span><span class="sxs-lookup"><span data-stu-id="9a87a-158">Offer</span></span> | <span data-ttu-id="9a87a-159">Sku</span><span class="sxs-lookup"><span data-stu-id="9a87a-159">Sku</span></span> | <span data-ttu-id="9a87a-160">Versão</span><span class="sxs-lookup"><span data-stu-id="9a87a-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9a87a-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="9a87a-161">OpenLogic</span></span> |<span data-ttu-id="9a87a-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="9a87a-162">CentOS</span></span> |<span data-ttu-id="9a87a-163">7</span><span class="sxs-lookup"><span data-stu-id="9a87a-163">7</span></span> |<span data-ttu-id="9a87a-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="9a87a-164">7.0.201503</span></span> |
| <span data-ttu-id="9a87a-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="9a87a-165">OpenLogic</span></span> |<span data-ttu-id="9a87a-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="9a87a-166">CentOS</span></span> |<span data-ttu-id="9a87a-167">7.1</span><span class="sxs-lookup"><span data-stu-id="9a87a-167">7.1</span></span> |<span data-ttu-id="9a87a-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="9a87a-168">7.1.201504</span></span> |
| <span data-ttu-id="9a87a-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9a87a-169">CoreOS</span></span> |<span data-ttu-id="9a87a-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9a87a-170">CoreOS</span></span> |<span data-ttu-id="9a87a-171">Beta</span><span class="sxs-lookup"><span data-stu-id="9a87a-171">Beta</span></span> |<span data-ttu-id="9a87a-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="9a87a-172">647.0.0</span></span> |
| <span data-ttu-id="9a87a-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9a87a-173">CoreOS</span></span> |<span data-ttu-id="9a87a-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9a87a-174">CoreOS</span></span> |<span data-ttu-id="9a87a-175">Estável</span><span class="sxs-lookup"><span data-stu-id="9a87a-175">Stable</span></span> |<span data-ttu-id="9a87a-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="9a87a-176">633.1.0</span></span> |
| <span data-ttu-id="9a87a-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="9a87a-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="9a87a-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="9a87a-178">DynamicsNAV</span></span> |<span data-ttu-id="9a87a-179">2015</span><span class="sxs-lookup"><span data-stu-id="9a87a-179">2015</span></span> |<span data-ttu-id="9a87a-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="9a87a-180">8.0.40459</span></span> |
| <span data-ttu-id="9a87a-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="9a87a-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="9a87a-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="9a87a-183">2013</span><span class="sxs-lookup"><span data-stu-id="9a87a-183">2013</span></span> |<span data-ttu-id="9a87a-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9a87a-184">1.0.0</span></span> |
| <span data-ttu-id="9a87a-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="9a87a-185">msopentech</span></span> |<span data-ttu-id="9a87a-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="9a87a-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="9a87a-187">Standard</span><span class="sxs-lookup"><span data-stu-id="9a87a-187">Standard</span></span> |<span data-ttu-id="9a87a-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9a87a-188">1.0.0</span></span> |
| <span data-ttu-id="9a87a-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="9a87a-189">msopentech</span></span> |<span data-ttu-id="9a87a-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="9a87a-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="9a87a-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="9a87a-191">Enterprise</span></span> |<span data-ttu-id="9a87a-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9a87a-192">1.0.0</span></span> |
| <span data-ttu-id="9a87a-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="9a87a-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="9a87a-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="9a87a-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="9a87a-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="9a87a-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="9a87a-196">12.0.2430</span></span> |
| <span data-ttu-id="9a87a-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="9a87a-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="9a87a-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="9a87a-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="9a87a-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="9a87a-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="9a87a-200">12.0.2430</span></span> |
| <span data-ttu-id="9a87a-201">Canónico</span><span class="sxs-lookup"><span data-stu-id="9a87a-201">Canonical</span></span> |<span data-ttu-id="9a87a-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-202">UbuntuServer</span></span> |<span data-ttu-id="9a87a-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="9a87a-203">12.04.5-LTS</span></span> |<span data-ttu-id="9a87a-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="9a87a-204">12.04.201504230</span></span> |
| <span data-ttu-id="9a87a-205">Canónico</span><span class="sxs-lookup"><span data-stu-id="9a87a-205">Canonical</span></span> |<span data-ttu-id="9a87a-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-206">UbuntuServer</span></span> |<span data-ttu-id="9a87a-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="9a87a-207">14.04.2-LTS</span></span> |<span data-ttu-id="9a87a-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="9a87a-208">14.04.201503090</span></span> |
| <span data-ttu-id="9a87a-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9a87a-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-210">WindowsServer</span></span> |<span data-ttu-id="9a87a-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="9a87a-211">2012-Datacenter</span></span> |<span data-ttu-id="9a87a-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="9a87a-212">3.0.201503</span></span> |
| <span data-ttu-id="9a87a-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9a87a-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-214">WindowsServer</span></span> |<span data-ttu-id="9a87a-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="9a87a-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="9a87a-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="9a87a-216">4.0.201503</span></span> |
| <span data-ttu-id="9a87a-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9a87a-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9a87a-218">WindowsServer</span></span> |<span data-ttu-id="9a87a-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="9a87a-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="9a87a-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="9a87a-220">5.0.201504</span></span> |
| <span data-ttu-id="9a87a-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="9a87a-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="9a87a-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="9a87a-222">WindowsServerEssentials</span></span> |<span data-ttu-id="9a87a-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="9a87a-223">WindowsServerEssentials</span></span> |<span data-ttu-id="9a87a-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="9a87a-224">1.0.141204</span></span> |
| <span data-ttu-id="9a87a-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="9a87a-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="9a87a-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="9a87a-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="9a87a-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="9a87a-227">2012R2</span></span> |<span data-ttu-id="9a87a-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="9a87a-228">4.3.4665</span></span> |

<span data-ttu-id="9a87a-229">Apenas criar a VM introduzindo Olá `azure vm quick-create` comando e a ser preparado para Olá avisos.</span><span class="sxs-lookup"><span data-stu-id="9a87a-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="9a87a-230">Deverá ter um aspeto semelhante a:</span><span class="sxs-lookup"><span data-stu-id="9a87a-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="9a87a-231">E pronto, já tem a sua VM nova.</span><span class="sxs-lookup"><span data-stu-id="9a87a-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="9a87a-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Tarefa: Implementar uma VM no Azure a partir de um modelo</span><span class="sxs-lookup"><span data-stu-id="9a87a-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="9a87a-233">Utilize as instruções de Olá toodeploy estas secções uma nova VM do Azure utilizando um modelo com Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a87a-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="9a87a-234">Este modelo cria uma única máquina virtual de uma nova rede virtual com uma única sub-rede e, ao contrário `azure vm quick-create`, permite toodescribe que pretende precisamente e repita-a sem erros.</span><span class="sxs-lookup"><span data-stu-id="9a87a-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="9a87a-235">Este modelo cria o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a87a-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="9a87a-236">Passo 1: Examine o ficheiro JSON de Olá para os parâmetros do modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="9a87a-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="9a87a-237">Seguem-se o conteúdo de Olá Olá JSON do ficheiro do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a87a-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="9a87a-238">(modelo de Olá também está localizado num [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="9a87a-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="9a87a-239">Os modelos são flexíveis e pelo designer Olá poderá ter escolhido toogive muitos dos parâmetros ou escolhido toooffer apenas alguns ao criar um modelo que é mais fixo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="9a87a-240">Na ordem toocollect Olá as informações que é necessário o modelo de Olá toopass como parâmetros, abra o ficheiro de modelo de Olá (Este tópico tem um modelo inline, abaixo) e examine Olá **parâmetros** valores.</span><span class="sxs-lookup"><span data-stu-id="9a87a-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="9a87a-241">Neste caso, o modelo de Olá abaixo irá perguntar-para:</span><span class="sxs-lookup"><span data-stu-id="9a87a-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="9a87a-242">Um nome de conta de armazenamento exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-242">A unique storage account name.</span></span>
* <span data-ttu-id="9a87a-243">Um nome de utilizador de administrador para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="9a87a-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="9a87a-244">Uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="9a87a-244">A password.</span></span>
* <span data-ttu-id="9a87a-245">Um nome de domínio para Olá fora toouse do mundo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="9a87a-246">Um número de versão Ubuntu Server -- mas aceitará apenas um de uma lista.</span><span class="sxs-lookup"><span data-stu-id="9a87a-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="9a87a-247">Saiba mais sobre os [requisitos de nomes de utilizador e palavras-passe](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="9a87a-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="9a87a-248">Assim que decidir estes valores, está pronto toocreate um grupo para e implementar este modelo para a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a87a-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="9a87a-249">Passo 2: Criar a máquina virtual de Olá utilizando o modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="9a87a-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="9a87a-250">Depois de ter os valores de parâmetro prontos, tem de criar um grupo de recursos para a sua implementação do modelo e, em seguida, implementar a modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a87a-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="9a87a-251">grupo de recursos de Olá toocreate, tipo `azure group create <group name> <location>` com o nome de Olá do grupo de Olá quiser e localização do Centro de dados de Olá na qual pretende que toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9a87a-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="9a87a-252">Isto acontece rapidamente:</span><span class="sxs-lookup"><span data-stu-id="9a87a-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="9a87a-253">Implementação do agora toocreate Olá, chamada `azure group deployment create` e passar:</span><span class="sxs-lookup"><span data-stu-id="9a87a-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="9a87a-254">ficheiro de modelo de Olá (se tiver guardado Olá acima ficheiros locais do tooa de modelo JSON).</span><span class="sxs-lookup"><span data-stu-id="9a87a-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="9a87a-255">Um modelo de URI (se pretender toopoint no ficheiro de Olá no GitHub ou alguns outros endereços web).</span><span class="sxs-lookup"><span data-stu-id="9a87a-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="9a87a-256">grupo de recursos de Olá na qual pretende toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9a87a-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="9a87a-257">Um nome opcional para a implementação.</span><span class="sxs-lookup"><span data-stu-id="9a87a-257">An optional deployment name.</span></span>

<span data-ttu-id="9a87a-258">Será pedido toosupply Olá valores dos parâmetros na secção "parâmetros de" Olá ficheiro JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="9a87a-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="9a87a-259">Quando especificar todos os valores de parâmetro de Olá, irá iniciar a sua implementação.</span><span class="sxs-lookup"><span data-stu-id="9a87a-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="9a87a-260">Segue-se um exemplo:</span><span class="sxs-lookup"><span data-stu-id="9a87a-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="9a87a-261">Receberá Olá seguinte tipo de informações:</span><span class="sxs-lookup"><span data-stu-id="9a87a-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="9a87a-262"><a id="create-a-custom-vm-image"></a>Tarefa: Criar uma imagem de VM personalizada</span><span class="sxs-lookup"><span data-stu-id="9a87a-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="9a87a-263">Que viu a utilização básica de Olá dos modelos acima, pelo que agora podemos utilizar semelhante instruções toocreate uma VM personalizada de um ficheiro. vhd específico no Azure utilizando um modelo através de Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a87a-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="9a87a-264">diferença de Olá aqui é que este modelo cria uma única máquina virtual de um disco de rígido virtual (VHD) especificado.</span><span class="sxs-lookup"><span data-stu-id="9a87a-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="9a87a-265">Passo 1: Examine o ficheiro JSON Olá para o modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="9a87a-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="9a87a-266">Seguem-se o conteúdo de Olá Olá JSON do ficheiro do modelo de Olá que esta secção utiliza como exemplo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="9a87a-267">(modelo de Olá também está localizado num [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="9a87a-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="9a87a-268">Novamente, terá de valores de Olá toofind pretende tooenter para parâmetros de Olá que não têm valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="9a87a-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="9a87a-269">Quando executa Olá `azure group deployment create` comando, Olá CLI do Azure irá solicitar tooenter esses valores.</span><span class="sxs-lookup"><span data-stu-id="9a87a-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="9a87a-270">Passo 2: Obter Olá VHD</span><span class="sxs-lookup"><span data-stu-id="9a87a-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="9a87a-271">Obviamente, precisa de um .vhd para isto.</span><span class="sxs-lookup"><span data-stu-id="9a87a-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="9a87a-272">Pode utilizar um que já tenha no Azure ou carregar outro.</span><span class="sxs-lookup"><span data-stu-id="9a87a-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="9a87a-273">Para uma máquina virtual baseado no Windows, consulte [criar e carregar um VHD do Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a87a-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="9a87a-274">Para uma máquina virtual baseado em Linux, consulte [criar e carregar um disco rígido virtual que contém o sistema de operativo Linux Olá](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a87a-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="9a87a-275">Passo 3: Criar a máquina virtual de Olá utilizando o modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="9a87a-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="9a87a-276">Agora está pronto toocreate uma nova máquina virtual com base no Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="9a87a-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="9a87a-277">Criar um toodeploy de grupo para, utilizando `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="9a87a-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="9a87a-278">Em seguida, criar a implementação de Olá utilizando Olá `--template-uri` toocall de opção no modelo de Olá diretamente (ou pode utilizar Olá `--template-file` opção toouse um ficheiro que guardou localmente).</span><span class="sxs-lookup"><span data-stu-id="9a87a-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="9a87a-279">Tenha em atenção que porque o modelo de Olá tem predefinições especificadas, é-lhe pedida apenas algumas coisas.</span><span class="sxs-lookup"><span data-stu-id="9a87a-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="9a87a-280">Se implementar a modelo Olá em locais diferentes, pode constatar que alguns colisões de nomenclatura ocorrerem com valores predefinidos de Olá (particularmente Olá nome DNS criar).</span><span class="sxs-lookup"><span data-stu-id="9a87a-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="9a87a-281">Saída aspeto semelhante ao seguinte Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a87a-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="9a87a-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Tarefa: Implementar uma aplicação multi-VMs que utiliza uma rede virtual e um balanceador de carga externo</span><span class="sxs-lookup"><span data-stu-id="9a87a-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="9a87a-283">Este modelo permite-lhe toocreate duas máquinas virtuais num Balanceador de carga e configurar uma regra de balanceamento de carga na porta 80.</span><span class="sxs-lookup"><span data-stu-id="9a87a-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="9a87a-284">Também implementa uma conta de armazenamento, uma rede virtual, um endereço IP público, um conjunto de disponibilidade e interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="9a87a-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="9a87a-285">Siga estes passos toodeploy uma aplicação de várias VMS que utiliza uma rede virtual e um balanceador de carga, utilizando um modelo do Resource Manager no repositório de modelo do GitHub Olá através de comandos do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a87a-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="9a87a-286">Passo 1: Examine o ficheiro JSON Olá para o modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="9a87a-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="9a87a-287">Seguem-se o conteúdo de Olá Olá JSON do ficheiro do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a87a-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="9a87a-288">Se pretender que a versão mais recente Olá, tem localizado [no repositório do GitHub Olá para modelos](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9a87a-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="9a87a-289">Este tópico utiliza Olá `--template-uri` comutador toocall no modelo de Olá, mas também pode utilizar Olá `--template-file` comutador toopass uma versão local.</span><span class="sxs-lookup"><span data-stu-id="9a87a-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="9a87a-290">Passo 2: Criar a implementação de Olá utilizando o modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="9a87a-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="9a87a-291">Criar um grupo de recursos para o modelo de Olá utilizando `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="9a87a-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="9a87a-292">Em seguida, crie uma implementação para esse grupo de recursos utilizando `azure group deployment create` e passar o grupo de recursos de Olá, transmitir um nome de implementação e responder a pedidos de Olá para os parâmetros do modelo de Olá que não tinha valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="9a87a-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="9a87a-293">Agora utilize Olá `azure group deployment create` comando e Olá `--template-uri` modelo de Olá toodeploy de opção.</span><span class="sxs-lookup"><span data-stu-id="9a87a-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="9a87a-294">Tenha os valores dos parâmetros à mão quando lhe forem pedidos, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9a87a-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="9a87a-295">Tenha em atenção que este modelo implementa uma imagem do Windows Server. No entanto, pode ser facilmente substituída por qualquer imagem do Linux.</span><span class="sxs-lookup"><span data-stu-id="9a87a-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="9a87a-296">Pretende toocreate um cluster Docker com vários gestores de swarm?</span><span class="sxs-lookup"><span data-stu-id="9a87a-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="9a87a-297">[Pode fazê-lo](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="9a87a-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="9a87a-298"><a id="remove-a-resource-group"></a>Tarefa: Remover um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9a87a-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="9a87a-299">Lembre-se de que pode implementar novamente o grupo de recursos de tooa, mas se terminar com uma, pode eliminá-lo utilizando `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="9a87a-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="9a87a-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Tarefa: Mostrar registo Olá para uma implementação de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9a87a-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="9a87a-301">Esta tarefa é comum quando está a criar ou a utilizar modelos.</span><span class="sxs-lookup"><span data-stu-id="9a87a-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="9a87a-302">implementação de Olá Olá chamada toodisplay os registos para a é um grupo `azure group log show <groupname>`, que apresenta bastantes bits de informações que é útil para compreender por que motivo algo aconteceu – ou não.</span><span class="sxs-lookup"><span data-stu-id="9a87a-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="9a87a-303">(Para obter mais informações sobre a resolução de problemas com implementações, bem como outras informações sobre problemas, veja [Troubleshoot common Azure deployment errors with Azure Resource Manager (Resolver erros comuns de implementações do Azure com o Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).))</span><span class="sxs-lookup"><span data-stu-id="9a87a-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="9a87a-304">falhas específicas do tootarget, por exemplo, poderá utilizar ferramentas como **jq** tooquery coisas um pouco mais precisamente, tais como as falhas individuais tem toocorrect.</span><span class="sxs-lookup"><span data-stu-id="9a87a-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="9a87a-305">Olá exemplo seguinte utiliza **jq** tooparse uma implementação de registo para **lbgroup**, que procuram falhas.</span><span class="sxs-lookup"><span data-stu-id="9a87a-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="9a87a-306">Pode detetar muito rapidamente o que correu mal, corrigir e tentar outra vez.</span><span class="sxs-lookup"><span data-stu-id="9a87a-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="9a87a-307">No Olá seguir caso, modelo Olá tinha sido criar duas VMs Olá mesmo tempo que tiver criado um bloqueio no Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="9a87a-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="9a87a-308">(Após iremos modificação do modelo de Olá, Olá implementação concluída com êxito rapidamente.)</span><span class="sxs-lookup"><span data-stu-id="9a87a-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="9a87a-309"><a id="display-information-about-a-virtual-machine"></a>Tarefa: Apresentar informações sobre uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9a87a-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="9a87a-310">Pode ver informações sobre as VMs específicas no seu grupo de recursos utilizando Olá `azure vm show <groupname> <vmname>` comando.</span><span class="sxs-lookup"><span data-stu-id="9a87a-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="9a87a-311">Se tiver mais do que uma VM no seu grupo, poderá ter primeiro Olá de toolist VMs num grupo utilizando `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="9a87a-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="9a87a-312">E, em seguida, procurar myVM1:</span><span class="sxs-lookup"><span data-stu-id="9a87a-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="9a87a-313">Se pretender tooprogrammatically arquivo e manipular a saída de Olá dos seus comandos de consola, poderá ser útil toouse uma análise de JSON como ferramenta  **[jq](https://github.com/stedolan/jq)**  ou  **[jsawk](https://github.com/micha/jsawk)** , ou bibliotecas de idioma que estão pronto para a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a87a-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="9a87a-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Tarefa: Inicie sessão na máquina de virtual baseado em Linux tooa</span><span class="sxs-lookup"><span data-stu-id="9a87a-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="9a87a-315">Normalmente, os computadores Linux são ligado toothrough SSH.</span><span class="sxs-lookup"><span data-stu-id="9a87a-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="9a87a-316">Para obter mais informações, consulte [como toouse SSH com o Linux no Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a87a-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="9a87a-317"><a id="stop-a-virtual-machine"></a>Tarefa: Parar uma VM</span><span class="sxs-lookup"><span data-stu-id="9a87a-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="9a87a-318">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="9a87a-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="9a87a-319">Utilize este parâmetro tookeep Olá IP virtual (VIP) da vnet Olá, caso seja Olá última VM nessa vnet.</span><span class="sxs-lookup"><span data-stu-id="9a87a-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="9a87a-320">Se utilizar Olá `StayProvisioned` parâmetro, irá ainda ser-lhe cobrado Olá VM.</span><span class="sxs-lookup"><span data-stu-id="9a87a-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="9a87a-321"><a id="start-a-virtual-machine"></a>Tarefa: Iniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="9a87a-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="9a87a-322">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="9a87a-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="9a87a-323"><a id="attach-a-data-disk"></a>Tarefa: Anexar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="9a87a-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="9a87a-324">Também terá de toodecide se tooattach um novo disco ou um que contenha dados.</span><span class="sxs-lookup"><span data-stu-id="9a87a-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="9a87a-325">Para um novo disco, o comando Olá cria o ficheiro. vhd Olá e anexa-lo no Olá mesmo comando.</span><span class="sxs-lookup"><span data-stu-id="9a87a-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="9a87a-326">tooattach um novo disco, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="9a87a-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="9a87a-327">tooattach um disco de dados existente, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="9a87a-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="9a87a-328">Em seguida, terá de disco de Olá toomount, como faria normalmente no Linux.</span><span class="sxs-lookup"><span data-stu-id="9a87a-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a87a-329">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9a87a-329">Next steps</span></span>
<span data-ttu-id="9a87a-330">Para obter mais até que ponto exemplos de utilização da CLI do Azure com Olá **arm** modo, consulte [Using Olá CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9a87a-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="9a87a-331">toolearn mais informações sobre recursos do Azure e os conceitos, consulte [descrição geral do Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a87a-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="9a87a-332">Para obter mais modelos que podem ser utilizados, veja [Modelos de Início Rápido do Azure](https://azure.microsoft.com/documentation/templates/) e [Application frameworks using templates (Arquiteturas de aplicações com modelos)](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a87a-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
