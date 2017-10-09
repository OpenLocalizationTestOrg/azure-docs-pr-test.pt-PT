### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>O BGP é suportado em todos os SKUs do VPN Gateway do Azure?
Não, o BGP é suportado nos gateways de VPN **Standard** e **HighPerformance** do Azure. O SKU **Básico** NÃO é suportado.

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>Posso utilizar o BGP com gateways de VPN do Azure baseados em políticas?
Não, o BGP é apenas suportado em gateways de VPN baseados na rota.

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>Posso utilizar ASNs (Números de Sistema Autónomo) privados?
Sim, pode utilizar os seus próprios ASNs públicos ou privados para as suas redes no local e para redes virtuais do Azure.

### <a name="are-there-asns-reserved-by-azure"></a>Existem ASNs reservados pelo Azure?
Sim, hello seguintes ASNs são reservados pelo Azure para peerings internos e externos:

* ASNs públicos: 8075, 8076, 12076
* ASNs privados: 65515 65517, 65518, 65519, 65520

Não é possível especificar estes ASNs para o dispositivos VPN no local ao ligar os gateways de VPN tooAzure.

### <a name="are-there-any-other-asns-that-i-cant-use"></a>Existem outros ASNs que não posso utilizar?
Sim, Olá seguintes ASNs é [reservado pela IANA](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml) e não é possível configurar o Gateway de VPN do Azure:

23456, 64496-64511, 65535-65551 e 429496729

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>Posso utilizar Olá mesmo ASN para ambos no local redes VPN e as VNets do Azure?
Não, tem de atribuir ASNs diferentes entre as suas redes no local e as VNets do Azure se estiver a ligá-las entre si com o BGP. Os Gateways de VPN do Azure têm uma predefinição ASN de 65515 atribuída,quer o BGP esteja ou não ativado para a conectividade em vários locais. Pode substituir esta predefinição atribuindo um ASN diferente ao criar o gateway de VPN Olá ou alterar Olá ASN depois do gateway Olá é criado. Terá de tooassign sua toohello de ASNs no local correspondente Gateways de rede Local do Azure.

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>Que endereço prefixos será gateways de VPN do Azure anunciam toome?
Gateway VPN do Azure irá anunciar Olá seguintes rotas tooyour dispositivos BGP no local:

* Os seus prefixos de endereços VNet
* Prefixos de endereço para cada gateway de VPN do Azure ligado toohello Gateways de rede Local
* Rotas aprendidas de outro BGP peering sessões toohello ligado VPN gateway do Azure, **exceto predefinido rota ou as rotas que se sobreponham a um prefixo VNet**.

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>Pode anunciar gateways de VPN do predefinida (0.0.0.0/0) de rota tooAzure?
Sim.

Tenha em atenção de que este irá forçar a todo o tráfego de saída VNet para o site no local e irá impedir que as VMs de VNet Olá aceitar comunicações públicas de Olá Internet diretamente, esse RDP ou SSH do Olá Internet toohello VMs.

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>Pode anunciar prefixos exatos Olá como prefixos minha rede Virtual?

Não, Olá de publicidade mesmos prefixos como qualquer um dos seus prefixos de endereço de rede Virtual será bloqueado ou filtrado por Olá plataforma Azure. No entanto, pode anunciar um prefixo que é um conjunto mais amplo do que tem no interior da Rede Virtual. 

Por exemplo, se a rede virtual utilizada Olá endereço espaço 10.0.0.0/16, foi anunciar 10.0.0.0/8. Contudo, não pode anunciar 10.0.0.0/16 ou 10.0.0.0/24.

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>Posso utilizar o BGP com as minhas ligações VNet a VNet?
Sim, pode utilizar o BGP para ligações em vários locais e ligações VNet a VNet.

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>Posso combinar ligações BGP com ligações não BGP para os meus gateways de VPN do Azure?
Sim, pode combinar ambos os BGP e ligações não BGP para Olá mesmo gateway de VPN do Azure.

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>O gateway de VPN do Azure suporta encaminhamento de trânsito BGP?
Sim, o encaminhamento de trânsito BGP é suportado, com exceção de Olá gateways de VPN do Azure **não** anunciar predefinido encaminha tooother elementos BGP. trânsito tooenable encaminhamento através de vários gateways de VPN do Azure, tem de ativar BGP em todas as ligações vnet para VNet intermédias.

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>Posso ter mais do que um túnel entre o gateway de VPN do Azure e a minha rede no local?
Sim, pode estabelecer mais do que um túnel VPN S2S entre um gateway de VPN do Azure e a sua rede no local. Tenha em atenção que todos estes túneis serão contados face do número total de Olá de túneis dos seus gateways de VPN do Azure e tem de ativar BGP em ambos os túneis.

Por exemplo, se tiver dois túneis redundantes entre o gateway de VPN do Azure e uma das suas redes no local, irá consumir 2 túneis quota total do Olá para o gateway de VPN do Azure (10 para Standard) e 30 para HighPerformance.

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>Posso ter vários túneis entre duas VNets do Azure com BGP?
Sim, mas pelo menos um dos gateways de rede virtual Olá tem de ser na configuração de ativo-ativo.

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>Posso utilizar o BGP para VPN S2S numa configuração de coexistência ExpressRoute/VPN S2S?
Sim. 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>Que endereço utiliza o gateway de VPN do Azure para o IP do Elemento de Rede BGP?
Olá VPN gateway do Azure irá alocar um único endereço IP de Olá intervalo GatewaySubnet definido para a rede virtual Olá. Por predefinição, é Olá penúltimo endereço do intervalo de Olá. Por exemplo, se o GatewaySubnet for 10.12.255.0/27/27, entre 10.12.255.0 too10.12.255.31, Olá endereço IP do elemento BGP no gateway de VPN do Azure Olá será 10.12.255.30. Pode encontrar estas informações quando listar Olá informações do gateway de VPN do Azure.

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>Quais são os requisitos de Olá para endereços de IP do elemento BGP Olá no meu dispositivo VPN?
O endereço de elemento de rede BGP no local **não deve** ser Olá mesmo como endereço IP público Olá do seu dispositivo VPN. Utilize um endereço IP diferente no dispositivo VPN Olá para o IP do elemento BGP. Pode ser um endereço atribuído toohello interface de loopback no dispositivo Olá. Especifique este endereço Olá correspondente Gateway de rede Local que representa Olá localização.

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>O que devo especificar como prefixos de endereços para Olá Gateway de rede Local ao utilizar o BGP?
Gateway de rede Local do Azure Especifica os prefixos de endereço inicial do Olá para rede no local de Olá. Com o BGP, tem de alocar o prefixo de anfitrião Olá (/ 32 prefixo) do seu endereço de IP do elemento BGP como o espaço de endereços de Olá para essa rede no local. Se o IP do elemento BGP for 10.52.255.254, deve especificar "10.52.255.254/32" como o localNetworkAddressSpace Olá de Olá Gateway de rede Local que representa esta rede no local. Este é tooensure Olá VPN do Azure gateway estabelece a sessão de BGP de Olá através do túnel S2S VPN de Olá.

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>O que deve adicionar dispositivo VPN do toomy no local para a sessão de peering de BGP de Olá?
Deve adicionar uma rota de anfitrião de Olá endereço IP do elemento de rede de BGP de Azure no seu dispositivo VPN túnel IPsec S2S VPN de toohello a apontar. Por exemplo, se Olá IP do elemento VPN do Azure for "10.12.255.30", deve adicionar uma rota de anfitrião para "10.12.255.30" com uma interface nexthop da interface de túnel IPsec de Olá correspondente no seu dispositivo VPN.

