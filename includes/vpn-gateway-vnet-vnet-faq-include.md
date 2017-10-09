<span data-ttu-id="2a8fc-101">Olá FAQ de VNet a VNet aplica-se ligações do Gateway tooVPN.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-101">hello VNet-to-VNet FAQ applies tooVPN Gateway connections.</span></span> <span data-ttu-id="2a8fc-102">Se estiver à procura do VNET Peering, veja [Peering de Rede Virtual](../articles/virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2a8fc-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="2a8fc-103">O Azure cobra o tráfego entre VNets?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="2a8fc-104">Tráfego de VNet a VNet no Olá mesma região é gratuita em ambas as direções quando utilizar uma ligação de gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-104">VNet-to-VNet traffic within hello same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="2a8fc-105">Entre a saída de VNet a VNet região tráfego é cobrado com Olá inter-vnet de saída dados velocidades máximas de transferência com base nas regiões de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-105">Cross region VNet-to-VNet egress traffic is charged with hello outbound inter-VNet data transfer rates based on hello source regions.</span></span> <span data-ttu-id="2a8fc-106">Consulte toohello [página de preços do VPN Gateway](https://azure.microsoft.com/pricing/details/vpn-gateway/) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-106">Refer toohello [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="2a8fc-107">Se estiver a ligar as suas VNets utilizando VNet Peering, em vez de Gateway de VPN, consulte Olá [página de preços de rede Virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="2a8fc-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see hello [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a><span data-ttu-id="2a8fc-108">O tráfego VNet a VNet viajam em Olá Internet?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-108">Does VNet-to-VNet traffic travel across hello Internet?</span></span>

<span data-ttu-id="2a8fc-109">Não.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-109">No.</span></span> <span data-ttu-id="2a8fc-110">O tráfego VNet a VNet circula na Olá principal do Microsoft Azure, não Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-110">VNet-to-VNet traffic travels across hello Microsoft Azure backbone, not hello Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="2a8fc-111">O tráfego VNet a VNet é seguro?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="2a8fc-112">Sim, está protegido pela encriptação IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a><span data-ttu-id="2a8fc-113">É necessário um tooconnect de dispositivo VPN VNets em conjunto?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-113">Do I need a VPN device tooconnect VNets together?</span></span>

<span data-ttu-id="2a8fc-114">Não.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-114">No.</span></span> <span data-ttu-id="2a8fc-115">A ligação de várias redes virtuais do Azure em conjunto não precisa de um dispositivo VPN, a menos que precise de conectividade em vários locais.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a><span data-ttu-id="2a8fc-116">A minha VNets precisarem de toobe no Olá mesma região?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-116">Do my VNets need toobe in hello same region?</span></span>

<span data-ttu-id="2a8fc-117">Não.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-117">No.</span></span> <span data-ttu-id="2a8fc-118">redes virtuais Olá podem estar em Olá idêntica ou diferentes regiões (localizações) do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-118">hello virtual networks can be in hello same or different Azure regions (locations).</span></span>

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a><span data-ttu-id="2a8fc-119">Se não estiverem em Olá VNets Olá mesma subscrição, subscrições Olá precisa toobe associado ao inquilino Olá mesmo AD?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-119">If hello VNets are not in hello same subscription, do hello subscriptions need toobe associated with hello same AD tenant?</span></span>

<span data-ttu-id="2a8fc-120">Não.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="2a8fc-121">Pode utilizar a VNet a VNet juntamente com ligações de vários locais?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="2a8fc-122">Sim.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-122">Yes.</span></span> <span data-ttu-id="2a8fc-123">A conectividade de rede virtual pode ser utilizada em simultâneo com VPNs de vários locais.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="2a8fc-124">A quantos sites no local e redes virtuais pode uma rede virtual ligar?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="2a8fc-125">Consulte a tabela [Requisitos do gateway](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="2a8fc-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="2a8fc-126">Pode utilizar a VNet tooconnect VMs ou serviços fora de uma VNet em nuvem?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-126">Can I use VNet-to-VNet tooconnect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="2a8fc-127">Não.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-127">No.</span></span> <span data-ttu-id="2a8fc-128">A VNet a VNet suporta a ligação de redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="2a8fc-129">Não suporta a ligação de máquinas virtuais ou serviços cloud que não estiverem numa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="2a8fc-130">Um serviço cloud ou um ponto de final de balanceamento de carga pode abranger VNets?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="2a8fc-131">Não.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-131">No.</span></span> <span data-ttu-id="2a8fc-132">Um serviço cloud ou um ponto final de balanceamento de carga não pode abranger várias redes virtuais, mesmo se estiverem ligadas em conjunto.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="2a8fc-133">Pode utilizar um tipo de VPN PolicyBased para ligações de VNet a VNet ou de Vários Locais?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="2a8fc-134">Não.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-134">No.</span></span> <span data-ttu-id="2a8fc-135">As ligações VNet a VNet ou de Vários Sites precisam de gateway de VPN do Azure com tipos de VPN RouteBased (anteriormente denominado Encaminhamento Dinâmico).</span><span class="sxs-lookup"><span data-stu-id="2a8fc-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="2a8fc-136">Posso ligar uma VNet com um tipo de VPN RouteBased de tooanother VNet com um tipo de PolicyBased VPN?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-136">Can I connect a VNet with a RouteBased VPN Type tooanother VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="2a8fc-137">Não, ambas as redes virtuais TÊM de utilizar VPNs baseadas na rota (anteriormente chamado Encaminhamento Dinâmico).</span><span class="sxs-lookup"><span data-stu-id="2a8fc-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="2a8fc-138">Os túneis VPN partilham a largura de banda?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="2a8fc-139">Sim.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-139">Yes.</span></span> <span data-ttu-id="2a8fc-140">Todos os túneis VPN da rede virtual Olá partilham a largura de banda disponível Olá no gateway de VPN do Azure Olá e Olá mesmo SLA de disponibilidade de gateway VPN no Azure.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-140">All VPN tunnels of hello virtual network share hello available bandwidth on hello Azure VPN gateway and hello same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="2a8fc-141">Os túneis redundantes são suportados?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="2a8fc-142">Os túneis redundantes entre um par de redes virtuais são suportados quando um gateway de rede virtual está configurado como ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="2a8fc-143">Pode ter espaços de endereços sobrepostos para configurações de VNet a VNet?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="2a8fc-144">Não.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-144">No.</span></span> <span data-ttu-id="2a8fc-145">Não pode ter intervalos de endereços IP sobrepostos.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="2a8fc-146">Pode existir uma sobreposição de espaços de endereços entre as redes virtuais ligadas e os sites locais no local?</span><span class="sxs-lookup"><span data-stu-id="2a8fc-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="2a8fc-147">Não.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-147">No.</span></span> <span data-ttu-id="2a8fc-148">Não pode ter intervalos de endereços IP sobrepostos.</span><span class="sxs-lookup"><span data-stu-id="2a8fc-148">You can't have overlapping IP address ranges.</span></span>



