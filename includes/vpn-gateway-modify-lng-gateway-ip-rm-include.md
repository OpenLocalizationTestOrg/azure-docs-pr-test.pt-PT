### <span data-ttu-id="0f4c7-101"><a name="gwipnoconnection"></a>gateway de rede local toomodify Olá 'GatewayIpAddress' - nenhuma ligação de gateway</span><span class="sxs-lookup"><span data-stu-id="0f4c7-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="0f4c7-102">Se o dispositivo VPN de Olá que pretende que o tooconnect toohas alterar o respetivo endereço IP público, tem de toomodify Olá rede local gateway tooreflect que alteram.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="0f4c7-103">Utilize o exemplo de Olá toomodify um gateway de rede local que não tem uma ligação de gateway.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="0f4c7-104">Quando modificar este valor, também pode modificar os prefixos de endereços de Olá em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="0f4c7-105">Na ordem toooverwrite Olá as definições atuais de ser se toouse Olá nome existente do gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="0f4c7-106">Se utilizar um nome diferente, criar um novo gateway de rede local, em vez de substituir Olá já existente.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="0f4c7-107"><a name="gwipwithconnection"></a>gateway de rede local toomodify Olá 'GatewayIpAddress' - ligação de gateway existente</span><span class="sxs-lookup"><span data-stu-id="0f4c7-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="0f4c7-108">Se o dispositivo VPN de Olá que pretende que o tooconnect toohas alterar o respetivo endereço IP público, tem de toomodify Olá rede local gateway tooreflect que alteram.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="0f4c7-109">Se gateway já existe uma ligação, terá primeiro de ligação de Olá tooremove.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="0f4c7-110">Depois de remover a ligação de Olá, pode modificar o endereço IP do gateway Olá e recriá-lo de uma nova ligação.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="0f4c7-111">Também pode modificar os prefixos de endereços de Olá em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="0f4c7-112">Este procedimento resulta num período de indisponibilidade da ligação VPN.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="0f4c7-113">Quando modificar o endereço IP do gateway Olá, não precisa de gateway de VPN de Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="0f4c7-114">Só precisa de ligação de Olá tooremove.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="0f4c7-115">Remova ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-115">Remove hello connection.</span></span> <span data-ttu-id="0f4c7-116">Pode encontrar o nome Olá da sua ligação utilizando o cmdlet Olá 'Get-AzureRmVirtualNetworkGatewayConnection'.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="0f4c7-117">Modifique o valor de 'GatewayIpAddress' Olá.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="0f4c7-118">Também pode modificar os prefixos de endereços de Olá em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="0f4c7-119">Ser se toouse Olá existente nome da sua rede local gateway toooverwrite Olá definições atuais.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="0f4c7-120">Caso contrário, crie um novo gateway de rede local, em vez de substituir Olá já existente.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="0f4c7-121">Crie ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-121">Create hello connection.</span></span> <span data-ttu-id="0f4c7-122">Neste exemplo, configuramos uma ligação do tipo IPsec.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="0f4c7-123">Ao recriar a ligação, utilize o tipo de ligação de Olá especificado para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="0f4c7-124">Para tipos de ligação adicionais, consulte Olá [cmdlet do PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="0f4c7-125">nome do tooobtain Olá VirtualNetworkGateway, pode executar Olá 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="0f4c7-126">Definir variáveis de Olá.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="0f4c7-127">Crie ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="0f4c7-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```