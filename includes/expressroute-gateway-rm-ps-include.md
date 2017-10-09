<span data-ttu-id="f01a3-101">Olá os passos para utilizar esta tarefa uma VNet com base nos valores de Olá no Olá seguinte lista de referência de configuração.</span><span class="sxs-lookup"><span data-stu-id="f01a3-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="f01a3-102">Nomes e outras definições também são descritos nesta lista.</span><span class="sxs-lookup"><span data-stu-id="f01a3-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="f01a3-103">Iremos não utilize esta lista diretamente em nenhum dos passos de Olá, embora adicionamos variáveis com base nos valores de Olá nesta lista.</span><span class="sxs-lookup"><span data-stu-id="f01a3-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="f01a3-104">Pode copiar Olá lista toouse como uma referência, substituindo os valores de Olá com os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="f01a3-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="f01a3-105">**Lista de referência de configuração**</span><span class="sxs-lookup"><span data-stu-id="f01a3-105">**Configuration reference list**</span></span>

* <span data-ttu-id="f01a3-106">Nome da rede virtual = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="f01a3-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="f01a3-107">Espaço de endereços de rede virtuais = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f01a3-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="f01a3-108">Grupo de recursos = "TestRG"</span><span class="sxs-lookup"><span data-stu-id="f01a3-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="f01a3-109">Subnet1 Name = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="f01a3-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="f01a3-110">Espaço de endereços Subnet1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="f01a3-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="f01a3-111">Nome de sub-rede de gateway: "GatewaySubnet" tem de nome sempre uma sub-rede de gateway *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="f01a3-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="f01a3-112">Espaço de endereços de sub-rede de gateway = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="f01a3-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="f01a3-113">Região = "EUA Leste"</span><span class="sxs-lookup"><span data-stu-id="f01a3-113">Region = "East US"</span></span>
* <span data-ttu-id="f01a3-114">O nome do gateway = "GW"</span><span class="sxs-lookup"><span data-stu-id="f01a3-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="f01a3-115">O nome IP do gateway = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="f01a3-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="f01a3-116">Configuração de IP do gateway Name = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="f01a3-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="f01a3-117">Tipo = "ExpressRoute" deste tipo é necessário para uma configuração do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f01a3-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="f01a3-118">Nome de IP público do gateway = "gwpip"</span><span class="sxs-lookup"><span data-stu-id="f01a3-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="f01a3-119">Adicionar um gateway</span><span class="sxs-lookup"><span data-stu-id="f01a3-119">Add a gateway</span></span>
1. <span data-ttu-id="f01a3-120">Ligar tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="f01a3-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="f01a3-121">Declare as variáveis para este exercício.</span><span class="sxs-lookup"><span data-stu-id="f01a3-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="f01a3-122">Ser tooedit se Olá tooreflect Olá as definições de exemplo que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="f01a3-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="f01a3-123">Armazene o objeto de rede virtual Olá como uma variável.</span><span class="sxs-lookup"><span data-stu-id="f01a3-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="f01a3-124">Adicione um tooyour de sub-rede de gateway rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="f01a3-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="f01a3-125">sub-rede do gateway Olá deve ter o nome "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="f01a3-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="f01a3-126">Deve criar uma sub-rede de gateway é/27 ou superior (/ 26, / 25, etc.).</span><span class="sxs-lookup"><span data-stu-id="f01a3-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="f01a3-127">Definir a configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="f01a3-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="f01a3-128">Armazenar a sub-rede do gateway Olá como uma variável.</span><span class="sxs-lookup"><span data-stu-id="f01a3-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="f01a3-129">Solicitar um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="f01a3-129">Request a public IP address.</span></span> <span data-ttu-id="f01a3-130">o endereço IP de Olá é solicitado antes de criar Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="f01a3-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="f01a3-131">Não é possível especificar o endereço IP Olá que pretende que o toouse; é dinamicamente atribuído.</span><span class="sxs-lookup"><span data-stu-id="f01a3-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="f01a3-132">Utilizará este endereço IP na secção de configuração seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="f01a3-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="f01a3-133">Olá AllocationMethod tem de ser dinâmico.</span><span class="sxs-lookup"><span data-stu-id="f01a3-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="f01a3-134">Crie Olá configuração para o seu gateway.</span><span class="sxs-lookup"><span data-stu-id="f01a3-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="f01a3-135">configuração do gateway de Olá define uma sub-rede de Olá e Olá toouse de endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="f01a3-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="f01a3-136">Neste passo, são especificar a configuração de Olá que será utilizada ao criar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="f01a3-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="f01a3-137">Este passo não criar objeto do gateway Olá efetivamente.</span><span class="sxs-lookup"><span data-stu-id="f01a3-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="f01a3-138">Utilize o exemplo de Olá abaixo toocreate a configuração do gateway.</span><span class="sxs-lookup"><span data-stu-id="f01a3-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="f01a3-139">Crie gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="f01a3-139">Create hello gateway.</span></span> <span data-ttu-id="f01a3-140">Neste passo, Olá **- GatewayType** é especialmente importante.</span><span class="sxs-lookup"><span data-stu-id="f01a3-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="f01a3-141">Tem de utilizar o valor de Olá **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="f01a3-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="f01a3-142">Depois de executar estes cmdlets, gateway Olá pode demorar 45 minutos ou mais toocreate.</span><span class="sxs-lookup"><span data-stu-id="f01a3-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="f01a3-143">Certifique-se de que foi criado o gateway de Olá</span><span class="sxs-lookup"><span data-stu-id="f01a3-143">Verify hello gateway was created</span></span>
<span data-ttu-id="f01a3-144">Utilize Olá os seguintes comandos tooverify Olá gateway tiver sido criada:</span><span class="sxs-lookup"><span data-stu-id="f01a3-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="f01a3-145">Redimensionar um gateway</span><span class="sxs-lookup"><span data-stu-id="f01a3-145">Resize a gateway</span></span>
<span data-ttu-id="f01a3-146">Há uma série de [SKUs de Gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="f01a3-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="f01a3-147">Pode utilizar Olá seguir Olá toochange do comando SKU de Gateway em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="f01a3-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f01a3-148">Este comando não funciona para UltraPerformance gateway.</span><span class="sxs-lookup"><span data-stu-id="f01a3-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="f01a3-149">toochange o gateway de UltraPerformance tooan do gateway, primeiro remova Olá existente ExpressRoute gateway e, em seguida, criar um novo gateway de UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="f01a3-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="f01a3-150">toodowngrade o gateway de um gateway de UltraPerformance, remova primeiro Olá UltraPerformance gateway e, em seguida, crie um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="f01a3-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="f01a3-151">Remover um gateway</span><span class="sxs-lookup"><span data-stu-id="f01a3-151">Remove a gateway</span></span>
<span data-ttu-id="f01a3-152">Utilize os seguintes comandos tooremove um gateway de Olá:</span><span class="sxs-lookup"><span data-stu-id="f01a3-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```