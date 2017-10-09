Olá FAQ de VNet a VNet aplica-se ligações do Gateway tooVPN. Se estiver à procura do VNET Peering, veja [Peering de Rede Virtual](../articles/virtual-network/virtual-network-peering-overview.md)

### <a name="does-azure-charge-for-traffic-between-vnets"></a>O Azure cobra o tráfego entre VNets?

Tráfego de VNet a VNet no Olá mesma região é gratuita em ambas as direções quando utilizar uma ligação de gateway VPN. Entre a saída de VNet a VNet região tráfego é cobrado com Olá inter-vnet de saída dados velocidades máximas de transferência com base nas regiões de origem Olá. Consulte toohello [página de preços do VPN Gateway](https://azure.microsoft.com/pricing/details/vpn-gateway/) para obter mais detalhes. Se estiver a ligar as suas VNets utilizando VNet Peering, em vez de Gateway de VPN, consulte Olá [página de preços de rede Virtual](https://azure.microsoft.com/pricing/details/virtual-network/).

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>O tráfego VNet a VNet viajam em Olá Internet?

Não. O tráfego VNet a VNet circula na Olá principal do Microsoft Azure, não Olá Internet.

### <a name="is-vnet-to-vnet-traffic-secure"></a>O tráfego VNet a VNet é seguro?

Sim, está protegido pela encriptação IPsec/IKE.

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>É necessário um tooconnect de dispositivo VPN VNets em conjunto?

Não. A ligação de várias redes virtuais do Azure em conjunto não precisa de um dispositivo VPN, a menos que precise de conectividade em vários locais.

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>A minha VNets precisarem de toobe no Olá mesma região?

Não. redes virtuais Olá podem estar em Olá idêntica ou diferentes regiões (localizações) do Azure.

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>Se não estiverem em Olá VNets Olá mesma subscrição, subscrições Olá precisa toobe associado ao inquilino Olá mesmo AD?

Não.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>Pode utilizar a VNet a VNet juntamente com ligações de vários locais?

Sim. A conectividade de rede virtual pode ser utilizada em simultâneo com VPNs de vários locais.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>A quantos sites no local e redes virtuais pode uma rede virtual ligar?

Consulte a tabela [Requisitos do gateway](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>Pode utilizar a VNet tooconnect VMs ou serviços fora de uma VNet em nuvem?

Não. A VNet a VNet suporta a ligação de redes virtuais. Não suporta a ligação de máquinas virtuais ou serviços cloud que não estiverem numa rede virtual.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>Um serviço cloud ou um ponto de final de balanceamento de carga pode abranger VNets?

Não. Um serviço cloud ou um ponto final de balanceamento de carga não pode abranger várias redes virtuais, mesmo se estiverem ligadas em conjunto.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>Pode utilizar um tipo de VPN PolicyBased para ligações de VNet a VNet ou de Vários Locais?

Não. As ligações VNet a VNet ou de Vários Sites precisam de gateway de VPN do Azure com tipos de VPN RouteBased (anteriormente denominado Encaminhamento Dinâmico).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>Posso ligar uma VNet com um tipo de VPN RouteBased de tooanother VNet com um tipo de PolicyBased VPN?

Não, ambas as redes virtuais TÊM de utilizar VPNs baseadas na rota (anteriormente chamado Encaminhamento Dinâmico).

### <a name="do-vpn-tunnels-share-bandwidth"></a>Os túneis VPN partilham a largura de banda?

Sim. Todos os túneis VPN da rede virtual Olá partilham a largura de banda disponível Olá no gateway de VPN do Azure Olá e Olá mesmo SLA de disponibilidade de gateway VPN no Azure.

### <a name="are-redundant-tunnels-supported"></a>Os túneis redundantes são suportados?

Os túneis redundantes entre um par de redes virtuais são suportados quando um gateway de rede virtual está configurado como ativo-ativo.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>Pode ter espaços de endereços sobrepostos para configurações de VNet a VNet?

Não. Não pode ter intervalos de endereços IP sobrepostos.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Pode existir uma sobreposição de espaços de endereços entre as redes virtuais ligadas e os sites locais no local?

Não. Não pode ter intervalos de endereços IP sobrepostos.



