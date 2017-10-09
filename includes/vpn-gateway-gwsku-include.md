<span data-ttu-id="ecab7-101">Quando cria um gateway de rede virtual, terá de gateway de Olá toospecify SKU que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="ecab7-101">When you create a virtual network gateway, you need toospecify hello gateway SKU that you want toouse.</span></span> <span data-ttu-id="ecab7-102">Selecione os SKUs de Olá que satisfazem os requisitos com base nos tipos de Olá de cargas de trabalho, throughputs, funcionalidades e SLAs.</span><span class="sxs-lookup"><span data-stu-id="ecab7-102">Select hello SKUs that satisfy your requirements based on hello types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="ecab7-103"><a name="workloads"></a>Produção *vs.* Cargas de trabalho Dev-Test</span><span class="sxs-lookup"><span data-stu-id="ecab7-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="ecab7-104">Devido a toohello diferenças no SLAs e conjuntos de funcionalidades, recomendamos Olá seguir SKUs para produção *vs* programador teste:</span><span class="sxs-lookup"><span data-stu-id="ecab7-104">Due toohello differences in SLAs and feature sets, we recommend hello following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="ecab7-105">**Carga de trabalho**</span><span class="sxs-lookup"><span data-stu-id="ecab7-105">**Workload**</span></span>                       | <span data-ttu-id="ecab7-106">**SKU**</span><span class="sxs-lookup"><span data-stu-id="ecab7-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="ecab7-107">**Produção, cargas de trabalho críticas**</span><span class="sxs-lookup"><span data-stu-id="ecab7-107">**Production, critical workloads**</span></span> | <span data-ttu-id="ecab7-108">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="ecab7-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="ecab7-109">**Dev-test ou prova de conceito**</span><span class="sxs-lookup"><span data-stu-id="ecab7-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="ecab7-110">Básica</span><span class="sxs-lookup"><span data-stu-id="ecab7-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="ecab7-111">Se estiver a utilizar Olá antigo SKUs, recomendações de SKU de produção Olá são padrão e HighPerformance SKUs.</span><span class="sxs-lookup"><span data-stu-id="ecab7-111">If you are using hello old SKUs, hello production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="ecab7-112">Para obter informações sobre Olá SKUs antigos, consulte [SKUs de Gateway (SKUs legados)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="ecab7-112">For information on hello old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="ecab7-113"><a name="feature"></a>Conjuntos de funcionalidades do SKU de gateway</span><span class="sxs-lookup"><span data-stu-id="ecab7-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="ecab7-114">SKUs de gateway nova Olá simplificar conjuntos de funcionalidades de Olá oferecidos nos gateways de Olá:</span><span class="sxs-lookup"><span data-stu-id="ecab7-114">hello new gateway SKUs streamline hello feature sets offered on hello gateways:</span></span>

| <span data-ttu-id="ecab7-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="ecab7-115">**SKU**</span></span>| <span data-ttu-id="ecab7-116">**Funcionalidades**</span><span class="sxs-lookup"><span data-stu-id="ecab7-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="ecab7-117">**Básica**</span><span class="sxs-lookup"><span data-stu-id="ecab7-117">**Basic**</span></span>   | <span data-ttu-id="ecab7-118">**VPN baseada em rota**: 10 túneis com P2S</span><span class="sxs-lookup"><span data-stu-id="ecab7-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="ecab7-119">**VPN baseada em políticas**: (IKEv1): 1 túnel; nenhum P2S</span><span class="sxs-lookup"><span data-stu-id="ecab7-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="ecab7-120">**VpnGw1, VpnGw2, and VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="ecab7-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="ecab7-121">**VPN baseado na rota**: cópia de segurança too30 túneis (*), P2S, o BGP, ativo-ativo, personalizada da política IPsec/IKE, coexistência ExpressRoute/VPN</span><span class="sxs-lookup"><span data-stu-id="ecab7-121">**Route-based VPN**: up too30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="ecab7-122">(*) Pode configurar "PolicyBasedTrafficSelectors" tooconnect um baseado na rota VPN gateway (VpnGw1 VpnGw2, VpnGw3) toomultiple dispositivos no local baseado em política de firewall.</span><span class="sxs-lookup"><span data-stu-id="ecab7-122">(*) You can configure "PolicyBasedTrafficSelectors" tooconnect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) toomultiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="ecab7-123">Consulte demasiado[toomultiple de gateways de estabelecer a ligação VPN no local dispositivos VPN baseado na política com o PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ecab7-123">Refer too[Connect VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="ecab7-124"><a name="resize"></a>Redimensionar dos SKU de gateway</span><span class="sxs-lookup"><span data-stu-id="ecab7-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="ecab7-125">Pode redimensionar entre SKU VpnGw1, VpnGw2 e VpnGw3.</span><span class="sxs-lookup"><span data-stu-id="ecab7-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="ecab7-126">Ao trabalhar com SKUs de gateway antigo Olá, pode redimensionar entre básicas, Standard e HighPerformance SKUs.</span><span class="sxs-lookup"><span data-stu-id="ecab7-126">When working with hello old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="ecab7-127">**Não é possível** redimensionar de SKUs de padrão/Basic/HighPerformance toohello SKUs de VpnGw2/VpnGw1/VpnGw3 novo.</span><span class="sxs-lookup"><span data-stu-id="ecab7-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs toohello new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="ecab7-128">Tem de, em vez disso, [migrar](#migrate) toohello SKUs de novo.</span><span class="sxs-lookup"><span data-stu-id="ecab7-128">You must, instead, [migrate](#migrate) toohello new SKUs.</span></span>

###  <span data-ttu-id="ecab7-129"><a name="migrate"></a>Migrar a partir do antigo SKUs toohello SKUs de novo</span><span class="sxs-lookup"><span data-stu-id="ecab7-129"><a name="migrate"></a>Migrating from old SKUs toohello new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
