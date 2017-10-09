## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="5cd47-101">Como toocreate uma VNet clássica a utilizar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5cd47-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="5cd47-102">Pode utilizar Olá CLI do Azure toomanage os recursos do Azure a partir da linha de comandos Olá partir de qualquer computador com Windows, Linux ou OSX.</span><span class="sxs-lookup"><span data-stu-id="5cd47-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="5cd47-103">toocreate uma VNet utilizando Olá CLI do Azure, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="5cd47-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="5cd47-104">Se nunca tiver utilizado a CLI do Azure, consulte o artigo [instalar e configurar a CLI do Azure de Olá](../articles/cli-install-nodejs.md) e siga as instruções de Olá toohello ponto onde poderá selecionar a sua conta do Azure e a subscrição de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="5cd47-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="5cd47-105">Executar Olá **criar rede azure vnet** comando toocreate uma VNet e uma sub-rede, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5cd47-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="5cd47-106">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="5cd47-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="5cd47-107">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="5cd47-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="5cd47-108">**-- vnet**.</span><span class="sxs-lookup"><span data-stu-id="5cd47-108">**--vnet**.</span></span> <span data-ttu-id="5cd47-109">Nome do Olá VNet toobe criado.</span><span class="sxs-lookup"><span data-stu-id="5cd47-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="5cd47-110">Para o nosso cenário *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="5cd47-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="5cd47-111">**-e (ou - espaço de endereços)**.</span><span class="sxs-lookup"><span data-stu-id="5cd47-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="5cd47-112">Espaço de endereços da VNet.</span><span class="sxs-lookup"><span data-stu-id="5cd47-112">VNet address space.</span></span> <span data-ttu-id="5cd47-113">Para o nosso cenário *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="5cd47-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="5cd47-114">**-i (ou - cidr)**.</span><span class="sxs-lookup"><span data-stu-id="5cd47-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="5cd47-115">Máscara de rede no formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="5cd47-115">Network mask in CIDR format.</span></span> <span data-ttu-id="5cd47-116">Para o nosso cenário *16*.</span><span class="sxs-lookup"><span data-stu-id="5cd47-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="5cd47-117">**-n (ou - nome de sub-rede**).</span><span class="sxs-lookup"><span data-stu-id="5cd47-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="5cd47-118">Nome da sub-rede primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="5cd47-118">Name of hello first subnet.</span></span> <span data-ttu-id="5cd47-119">Para o nosso cenário *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="5cd47-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="5cd47-120">**-p (ou - ip de início de sub-rede)**.</span><span class="sxs-lookup"><span data-stu-id="5cd47-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="5cd47-121">Endereço IP inicial para a sub-rede ou espaço de endereços de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5cd47-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="5cd47-122">Para o nosso cenário *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="5cd47-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="5cd47-123">**-r (ou - sub-rede cidr)**.</span><span class="sxs-lookup"><span data-stu-id="5cd47-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="5cd47-124">Máscara de rede no formato CIDR para a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5cd47-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="5cd47-125">Para o nosso cenário *24*.</span><span class="sxs-lookup"><span data-stu-id="5cd47-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="5cd47-126">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="5cd47-126">**-l (or --location)**.</span></span> <span data-ttu-id="5cd47-127">Região do Azure onde será criada Olá VNet.</span><span class="sxs-lookup"><span data-stu-id="5cd47-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="5cd47-128">Para o nosso cenário *EUA Central*.</span><span class="sxs-lookup"><span data-stu-id="5cd47-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="5cd47-129">Executar Olá **sub-rede da vnet de rede do azure crie** comando toocreate uma sub-rede, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5cd47-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="5cd47-130">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="5cd47-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="5cd47-131">O resultado para o comando de Olá acima Olá esperado é:</span><span class="sxs-lookup"><span data-stu-id="5cd47-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="5cd47-132">**-t (ou -- vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="5cd47-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="5cd47-133">Nome da VNet onde será criada a sub-rede de Olá de Olá.</span><span class="sxs-lookup"><span data-stu-id="5cd47-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="5cd47-134">Para o nosso cenário *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="5cd47-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="5cd47-135">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="5cd47-135">**-n (or --name)**.</span></span> <span data-ttu-id="5cd47-136">Nome da nova sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="5cd47-136">Name of hello new subnet.</span></span> <span data-ttu-id="5cd47-137">Para o nosso cenário *back-end*.</span><span class="sxs-lookup"><span data-stu-id="5cd47-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="5cd47-138">**-a (or --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="5cd47-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="5cd47-139">Bloco CIDR da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5cd47-139">Subnet CIDR block.</span></span> <span data-ttu-id="5cd47-140">Quatro nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="5cd47-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="5cd47-141">Executar Olá **mostrar de vnet de rede do azure** comando Propriedades de Olá tooview de Olá nova vnet, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5cd47-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="5cd47-142">O resultado para o comando de Olá acima Olá esperado é:</span><span class="sxs-lookup"><span data-stu-id="5cd47-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

