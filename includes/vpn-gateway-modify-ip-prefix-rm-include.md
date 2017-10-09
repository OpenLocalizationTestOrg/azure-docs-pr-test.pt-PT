### <span data-ttu-id="b1768-101"><a name="noconnection"></a>prefixos de endereços IP de gateway de rede local toomodify - nenhuma ligação de gateway</span><span class="sxs-lookup"><span data-stu-id="b1768-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="b1768-102">tooadd prefixos de endereços adicionais:</span><span class="sxs-lookup"><span data-stu-id="b1768-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="b1768-103">prefixos de endereço tooremove:</span><span class="sxs-lookup"><span data-stu-id="b1768-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="b1768-104">Deixe os prefixos de Olá que já não necessita.</span><span class="sxs-lookup"><span data-stu-id="b1768-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="b1768-105">Neste exemplo, vamos já não precisamos do prefixo 20.0.0.0/24 (do exemplo anterior Olá), pelo que iremos atualizar o gateway de rede local Olá, excluir esse prefixo.</span><span class="sxs-lookup"><span data-stu-id="b1768-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="b1768-106"><a name="withconnection"></a>toomodify rede local gateway prefixos de endereços IP - existente a ligação de gateway</span><span class="sxs-lookup"><span data-stu-id="b1768-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="b1768-107">Se tiver uma ligação de gateway e pretender tooadd ou remover prefixos de endereço IP do Olá contidos no gateway de rede local, terá de Olá toodo os seguintes passos, por ordem.</span><span class="sxs-lookup"><span data-stu-id="b1768-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="b1768-108">Este procedimento resulta num período de indisponibilidade da ligação VPN.</span><span class="sxs-lookup"><span data-stu-id="b1768-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="b1768-109">Ao modificar os prefixos de endereços IP, não precisa de gateway de VPN de Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="b1768-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="b1768-110">Só precisa de ligação de Olá tooremove.</span><span class="sxs-lookup"><span data-stu-id="b1768-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="b1768-111">Remova ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="b1768-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="b1768-112">Modificar os prefixos de endereço de Olá para gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="b1768-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="b1768-113">Definir variável Olá para Olá LocalNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="b1768-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="b1768-114">Modificar os prefixos de Olá.</span><span class="sxs-lookup"><span data-stu-id="b1768-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="b1768-115">Crie ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="b1768-115">Create hello connection.</span></span> <span data-ttu-id="b1768-116">Neste exemplo, configuramos uma ligação do tipo IPsec.</span><span class="sxs-lookup"><span data-stu-id="b1768-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="b1768-117">Ao recriar a ligação, utilize o tipo de ligação de Olá especificado para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="b1768-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="b1768-118">Para tipos de ligação adicionais, consulte Olá [cmdlet do PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="b1768-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="b1768-119">Definir variável Olá para Olá VirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="b1768-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="b1768-120">Crie ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="b1768-120">Create hello connection.</span></span> <span data-ttu-id="b1768-121">Este exemplo utiliza a variável de Olá $local que configurou no passo 2.</span><span class="sxs-lookup"><span data-stu-id="b1768-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```