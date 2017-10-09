1. <span data-ttu-id="bf45a-101">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bf45a-101">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="bf45a-102">A partir do canto superior esquerdo de Olá, clique em **novo > computação > Centro de dados do Windows Server 2016**.</span><span class="sxs-lookup"><span data-stu-id="bf45a-102">Starting in hello upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Navegue toohello imagens de VM do Azure no portal de Olá](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="bf45a-104">No Centro de dados do Windows Server 2016 Olá, selecione o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="bf45a-104">On hello Windows Server 2016 Datacenter, select hello Classic deployment model.</span></span> <span data-ttu-id="bf45a-105">Clique em Criar.</span><span class="sxs-lookup"><span data-stu-id="bf45a-105">Click Create.</span></span>

    ![Captura de ecrã que mostra as imagens de VM do Azure Olá disponíveis no portal de Olá](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="bf45a-107">1. Painel Básico</span><span class="sxs-lookup"><span data-stu-id="bf45a-107">1. Basics blade</span></span>

<span data-ttu-id="bf45a-108">Painel de noções básicas de Olá pedidos administrativas informações de Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bf45a-108">hello Basics blade requests administrative information for hello virtual machine.</span></span>

1. <span data-ttu-id="bf45a-109">Introduza um **nome** para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="bf45a-109">Enter a **Name** for hello virtual machine.</span></span> <span data-ttu-id="bf45a-110">Exemplo de Olá, _HeroVM_ é Olá nome da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="bf45a-110">In hello example, _HeroVM_ is hello name of hello virtual machine.</span></span> <span data-ttu-id="bf45a-111">nome de Olá tem de ser 1-15 carateres e não pode conter carateres especiais.</span><span class="sxs-lookup"><span data-stu-id="bf45a-111">hello name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="bf45a-112">Introduza um **nome de utilizador** e uma forte **palavra-passe** que são utilizado toocreate uma conta local no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="bf45a-112">Enter a **User name** and a strong **Password** that are used toocreate a local account on hello VM.</span></span> <span data-ttu-id="bf45a-113">Olá conta local é utilizada toosign no tooand gerir Olá VM.</span><span class="sxs-lookup"><span data-stu-id="bf45a-113">hello local account is used toosign in tooand manage hello VM.</span></span> <span data-ttu-id="bf45a-114">Exemplo de Olá, _azureuser_ é Olá nome de utilizador.</span><span class="sxs-lookup"><span data-stu-id="bf45a-114">In hello example, _azureuser_ is hello user name.</span></span>

 <span data-ttu-id="bf45a-115">Olá palavra-passe tem de ter entre 8-123 carateres e cumprir três fora de requisitos de complexidade de seguintes quatro de Olá: uma minúscula, uma maiúscula, um número e um caráter especial.</span><span class="sxs-lookup"><span data-stu-id="bf45a-115">hello password must be 8-123 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="bf45a-116">Saiba mais sobre os [requisitos de nomes de utilizador e palavras-passe](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="bf45a-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="bf45a-117">Olá **subscrição** é opcional.</span><span class="sxs-lookup"><span data-stu-id="bf45a-117">hello **Subscription** is optional.</span></span> <span data-ttu-id="bf45a-118">Uma definição comum é "Pay As You Go".</span><span class="sxs-lookup"><span data-stu-id="bf45a-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="bf45a-119">Selecione um existente **grupo de recursos** ou nome de Olá de tipo para um novo.</span><span class="sxs-lookup"><span data-stu-id="bf45a-119">Select an existing **Resource group** or type hello name for a new one.</span></span> <span data-ttu-id="bf45a-120">Exemplo de Olá, _HeroVMRG_ é o nome de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf45a-120">In hello example, _HeroVMRG_ is hello name of hello resource group.</span></span>

5. <span data-ttu-id="bf45a-121">Selecione um datacenter Azure **localização** onde pretende Olá toorun VM.</span><span class="sxs-lookup"><span data-stu-id="bf45a-121">Select an Azure datacenter **Location** where you want hello VM toorun.</span></span> <span data-ttu-id="bf45a-122">Exemplo de Olá, **EUA Leste** Olá localização.</span><span class="sxs-lookup"><span data-stu-id="bf45a-122">In hello example, **East US** is hello location.</span></span>

6. <span data-ttu-id="bf45a-123">Quando tiver terminado, clique em **seguinte** toocontinue toohello seguinte painel.</span><span class="sxs-lookup"><span data-stu-id="bf45a-123">When you are done, click **Next** toocontinue toohello next blade.</span></span>

    ![Captura de ecrã que mostra as Olá no painel de noções básicas de Olá para configurar uma VM do Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="bf45a-125">2. Painel Tamanho</span><span class="sxs-lookup"><span data-stu-id="bf45a-125">2. Size blade</span></span>

<span data-ttu-id="bf45a-126">Painel de tamanho de Olá identifica os detalhes de configuração de Olá de Olá VM e apresenta uma lista de várias opções que incluem o SO, número de processadores, tipo de disco de armazenamento e custos de utilização mensais estimado.</span><span class="sxs-lookup"><span data-stu-id="bf45a-126">hello Size blade identifies hello configuration details of hello VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="bf45a-127">Escolher um tamanho VM e, em seguida, clique em **selecione** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="bf45a-127">Choose a VM size, and then click **Select** toocontinue.</span></span> <span data-ttu-id="bf45a-128">Neste exemplo, _DS1_\__V2 padrão_ é o tamanho da VM Olá.</span><span class="sxs-lookup"><span data-stu-id="bf45a-128">In this example, _DS1_\__V2 Standard_ is hello VM size.</span></span>

  ![Captura de ecrã do painel de tamanho de Olá que mostra Olá tamanhos de VM do Azure que pode selecionar](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="bf45a-130">3. Painel Definições</span><span class="sxs-lookup"><span data-stu-id="bf45a-130">3. Settings blade</span></span>

<span data-ttu-id="bf45a-131">Painel de definições de Olá pedidos opções de armazenamento e rede.</span><span class="sxs-lookup"><span data-stu-id="bf45a-131">hello Settings blade requests storage and network options.</span></span> <span data-ttu-id="bf45a-132">Pode aceitar as predefinições de Olá.</span><span class="sxs-lookup"><span data-stu-id="bf45a-132">You can accept hello default settings.</span></span> <span data-ttu-id="bf45a-133">O Azure cria entradas adequadas sempre que necessário.</span><span class="sxs-lookup"><span data-stu-id="bf45a-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="bf45a-134">Se tiver selecionado um tamanho da máquina virtual que o suporte, pode experimentar o Armazenamento Premium do Azure ao selecionar Premium (SSD) em Tipo de Disco.</span><span class="sxs-lookup"><span data-stu-id="bf45a-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="bf45a-135">Quando terminar de efetuar alterações, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf45a-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="bf45a-136">4. Painel Resumo</span><span class="sxs-lookup"><span data-stu-id="bf45a-136">4. Summary blade</span></span>

<span data-ttu-id="bf45a-137">Painel de resumo de Olá lista as definições de Olá especificadas no painel anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="bf45a-137">hello Summary blade lists hello settings specified in hello previous blades.</span></span> <span data-ttu-id="bf45a-138">Clique em **OK** quando estiver a imagem de Olá toomake pronto.</span><span class="sxs-lookup"><span data-stu-id="bf45a-138">Click **OK** when you're ready toomake hello image.</span></span>

 ![Relatório de resumo painel fornecer as definições especificadas da máquina virtual de Olá](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="bf45a-140">Depois de criar a máquina virtual de Olá, portal Olá apresenta uma lista de Olá nova máquina virtual em **todos os recursos**e apresenta um mosaico de máquina virtual de Olá no dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="bf45a-140">After hello virtual machine is created, hello portal lists hello new virtual machine under **All resources**, and displays a tile of hello virtual machine on hello dashboard.</span></span> <span data-ttu-id="bf45a-141">Olá nuvem serviço e o armazenamento conta correspondente também são criadas e listados.</span><span class="sxs-lookup"><span data-stu-id="bf45a-141">hello corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="bf45a-142">Máquina virtual de Olá e o serviço em nuvem são iniciados automaticamente e o estado está listado como **executar**.</span><span class="sxs-lookup"><span data-stu-id="bf45a-142">Both hello virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Configurar o agente da VM e Olá pontos finais da máquina virtual de Olá](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
