

![Máquinas virtuais no serviço autónomo em nuvem](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

<span data-ttu-id="b8a0f-102">Se colocar as máquinas virtuais numa rede virtual, pode decidir quantos serviços em nuvem que pretende toouse para conjuntos de disponibilidade e balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-102">If you place your virtual machines in a virtual network, you can decide how many cloud services you want toouse for load balancing and availability sets.</span></span> <span data-ttu-id="b8a0f-103">Além disso, pode organizar Olá máquinas de virtuais em sub-redes Olá mesma forma como o local de rede e ligar Olá tooyour de rede virtual no local rede.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-103">Additionally, you can organize hello virtual machines on subnets in hello same way as your on-premises network and connect hello virtual network tooyour on-premises network.</span></span> <span data-ttu-id="b8a0f-104">Eis um exemplo:</span><span class="sxs-lookup"><span data-stu-id="b8a0f-104">Here's an example:</span></span>

![Máquinas virtuais numa rede virtual](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

<span data-ttu-id="b8a0f-106">Redes virtuais são Olá recomendado forma tooconnect máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-106">Virtual networks are hello recommended way tooconnect virtual machines in Azure.</span></span> <span data-ttu-id="b8a0f-107">Olá melhor prática é tooconfigure cada camada da aplicação no serviço em nuvem separado.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-107">hello best practice is tooconfigure each tier of your application in a separate cloud service.</span></span> <span data-ttu-id="b8a0f-108">No entanto, poderá ser necessário toocombine algumas máquinas virtuais de camadas de aplicações diferentes em Olá mesmo na nuvem tooremain de serviço no máximo, Olá 200 serviços cloud por subscrição.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-108">However, you may need toocombine some virtual machines from different application tiers into hello same cloud service tooremain within hello maximum of 200 cloud services per subscription.</span></span> <span data-ttu-id="b8a0f-109">tooreview esta e outros limites, consulte o artigo [subscrição do Azure e limites de serviço, Quotas e restrições](../articles/azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b8a0f-109">tooreview this and other limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../articles/azure-subscription-service-limits.md).</span></span>

## <a name="connect-vms-in-a-virtual-network"></a><span data-ttu-id="b8a0f-110">Ligar as VMs numa rede virtual</span><span class="sxs-lookup"><span data-stu-id="b8a0f-110">Connect VMs in a virtual network</span></span>
<span data-ttu-id="b8a0f-111">máquinas virtuais de tooconnect numa rede virtual:</span><span class="sxs-lookup"><span data-stu-id="b8a0f-111">tooconnect virtual machines in a virtual network:</span></span>

1. <span data-ttu-id="b8a0f-112">Criar rede virtual Olá no Olá [portal do Azure](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) e especifique 'implementação clássica'.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-112">Create hello virtual network in hello [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) and specify 'classic deployment'.</span></span>
2. <span data-ttu-id="b8a0f-113">Criar conjunto de Olá de serviços em nuvem para a sua implementação tooreflect o design para conjuntos de disponibilidade e o balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-113">Create hello set of cloud services for your deployment tooreflect your design for availability sets and load balancing.</span></span> <span data-ttu-id="b8a0f-114">No portal do Azure Olá, clique em **novo > computação > serviço em nuvem** para cada serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-114">In hello Azure portal, click **New > Compute > Cloud service** for each cloud service.</span></span>

  <span data-ttu-id="b8a0f-115">À medida que preencha os detalhes do serviço de nuvem Olá, escolher Olá mesmo _grupo de recursos_ utilizado com a rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-115">As you fill out hello cloud service details, choose hello same _resource group_ used with hello virtual network.</span></span>

3. <span data-ttu-id="b8a0f-116">toocreate cada novo virtual máquina, clique em **novo > computação**, em seguida, selecione Olá imagem VM adequada de Olá **aplicações em destaque**.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-116">toocreate each new virtual machine, click **New > Compute**, then select hello appropriate VM image from hello **Featured apps**.</span></span>

  <span data-ttu-id="b8a0f-117">No Olá VM **Noções básicas** painel, escolha Olá mesmo _grupo de recursos_ utilizado com a rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-117">In hello VM **Basics** blade, choose hello same _resource group_ used with hello virtual network.</span></span>

  ![Painel de noções básicas de VM ao utilizar uma VNet](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. <span data-ttu-id="b8a0f-119">Como preencher Olá VM **definições**, escolha Olá correto _serviço em nuvem_ ou _rede virtual_ para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-119">As you fill out hello VM **Settings**, choose hello correct _Cloud service_ or _virtual network_ for hello VM.</span></span>

  <span data-ttu-id="b8a0f-120">Azure selecionará Olá outro item com base na sua seleção.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-120">Azure will select hello other item based on your selection.</span></span>

  ![Painel de definições de VM ao utilizar uma VNet](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a><span data-ttu-id="b8a0f-122">Ligar as VMs num serviço autónomo em nuvem</span><span class="sxs-lookup"><span data-stu-id="b8a0f-122">Connect VMs in a standalone cloud service</span></span>
<span data-ttu-id="b8a0f-123">máquinas virtuais de tooconnect num serviço autónomo em nuvem:</span><span class="sxs-lookup"><span data-stu-id="b8a0f-123">tooconnect virtual machines in a standalone cloud service:</span></span>

1. <span data-ttu-id="b8a0f-124">Criar o serviço em nuvem Olá no Olá [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8a0f-124">Create hello cloud service in hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="b8a0f-125">Clique em **novo > computação > serviço em nuvem**.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-125">Click **New > Compute > Cloud service**.</span></span> <span data-ttu-id="b8a0f-126">Em alternativa, pode criar o serviço em nuvem Olá para a sua implementação quando criar a sua primeira máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-126">Or, you can create hello cloud service for your deployment when you create your first virtual machine.</span></span>
2. <span data-ttu-id="b8a0f-127">Ao criar máquinas virtuais Olá, escolha Olá mesmo grupo de recursos utilizado com o serviço em nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-127">When you create hello virtual machines, choose hello same resource group used with hello cloud service.</span></span>

  ![Adicionar um serviço de nuvem existente do virtual machine tooan](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  <span data-ttu-id="b8a0f-129">Como preencher os detalhes VM Olá, escolha o nome de Olá do serviço em nuvem criado no passo primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="b8a0f-129">As you fill out hello VM details, choose hello name of cloud service created in hello first step.</span></span>

  ![Selecionar um serviço em nuvem para uma máquina virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
