Olá legado (antigo) do VPN gateway SKUs são:

* Básica
* Standard
* HighPerformance

Gateway de VPN não utiliza a SKU de gateway de UltraPerformance Olá. Para obter informações sobre Olá UltraPerformance SKU, consulte Olá [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentação.

Ao trabalhar com Olá SKUs legados, considere Olá seguinte:

* Se quiser toouse um tipo de PolicyBased VPN, tem de utilizar Olá SKU básico. As VPNs PolicyBased (anteriormente designadas Encaminhamento Estático) não são suportadas em mais nenhum SKU.
* BGP não é suportado em Olá SKU básico.
* Gateway de VPN do ExpressRoute coexistentes configurações não são suportadas em Olá SKU básico.
* Ligações do S2S VPN Gateway de ativo-ativo podem ser configuradas em Olá HighPerformance SKU apenas.
