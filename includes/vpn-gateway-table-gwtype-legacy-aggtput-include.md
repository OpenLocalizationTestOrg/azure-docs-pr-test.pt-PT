Olá tabela seguinte mostra os tipos de gateway de Olá e débito agregado estimado de Olá por SKU de gateway. Esta tabela aplica-se toohello Resource Manager e modelos de implementação clássica. 

Há diferença de preços entre os SKUs de gateway. Para obter mais informações, veja [Preços do Gateway de VPN](https://azure.microsoft.com/pricing/details/vpn-gateway).

Tenha em atenção que gateway de UltraPerformance Olá que SKU não é representada nesta tabela. Para obter informações sobre Olá UltraPerformance SKU, consulte Olá [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentação.

|  | **Débito do Gateway de VPN (1)** | **Máximo de túneis IPsec do Gateway de VPN (2)** | **Débito do Gateway do ExpressRoute** | **Coexistência do ExpressRoute e do Gateway de VPN** |
| --- | --- | --- | --- | --- |
| **SKU Básico (3)(5)(6)** |100 Mbps |10 |500 Mbps (6) |Não |
| **SKU Padrão (4)(5)** |100 Mbps |10 |1000 Mbps |Sim |
| **SKU de Elevado Desempenho (4)** |200 Mbps |30 |2000 Mbps |Sim |


(1) débito da VPN Olá é uma estimativa aproximada baseada em medidas de Olá entre VNets na Olá mesma região do Azure. Não é um débito garantido para ligações em vários locais em Olá Internet. É medida de débito máximo de possíveis Olá.

(2) número de Olá de túneis Consulte tooRouteBased VPNs. Uma VPN PolicyBased só pode suportar um túnel VPN de Rede de VPNs.

(3) BGP não é suportada para Olá SKU básico.

(4) As VPNs PolicyBased não são suportadas para este SKU. São suportadas para Olá SKU básico apenas.

(5) As ligações do Gateway de VPN S2S no modo ativo/ativo não são suportadas por este SKU. Olá HighPerformance SKU só é suportada ativo-ativo.

(6) SKU básico foi preterido para utilização com o ExpressRoute.
