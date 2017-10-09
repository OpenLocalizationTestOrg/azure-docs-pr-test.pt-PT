Quando cria um gateway de rede virtual, terá de gateway de Olá toospecify SKU que pretende que o toouse. Selecione os SKUs de Olá que satisfazem os requisitos com base nos tipos de Olá de cargas de trabalho, throughputs, funcionalidades e SLAs.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>Produção *vs.* Cargas de trabalho Dev-Test

Devido a toohello diferenças no SLAs e conjuntos de funcionalidades, recomendamos Olá seguir SKUs para produção *vs* programador teste:

| **Carga de trabalho**                       | **SKU**               |
| ---                                | ---                    |
| **Produção, cargas de trabalho críticas** | VpnGw1, VpnGw2, VpnGw3 |
| **Dev-test ou prova de conceito**   | Básica                  |
|                                    |                        |

Se estiver a utilizar Olá antigo SKUs, recomendações de SKU de produção Olá são padrão e HighPerformance SKUs. Para obter informações sobre Olá SKUs antigos, consulte [SKUs de Gateway (SKUs legados)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).

###  <a name="feature"></a>Conjuntos de funcionalidades do SKU de gateway

SKUs de gateway nova Olá simplificar conjuntos de funcionalidades de Olá oferecidos nos gateways de Olá:

| **SKU**| **Funcionalidades**|
| ---    | ---         |
|**Básica**   | **VPN baseada em rota**: 10 túneis com P2S<br><br>**VPN baseada em políticas**: (IKEv1): 1 túnel; nenhum P2S|
| **VpnGw1, VpnGw2, and VpnGw3** | **VPN baseado na rota**: cópia de segurança too30 túneis (*), P2S, o BGP, ativo-ativo, personalizada da política IPsec/IKE, coexistência ExpressRoute/VPN |
|        |             |

(*) Pode configurar "PolicyBasedTrafficSelectors" tooconnect um baseado na rota VPN gateway (VpnGw1 VpnGw2, VpnGw3) toomultiple dispositivos no local baseado em política de firewall. Consulte demasiado[toomultiple de gateways de estabelecer a ligação VPN no local dispositivos VPN baseado na política com o PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) para obter mais detalhes.

###  <a name="resize"></a>Redimensionar dos SKU de gateway

1. Pode redimensionar entre SKU VpnGw1, VpnGw2 e VpnGw3.
2. Ao trabalhar com SKUs de gateway antigo Olá, pode redimensionar entre básicas, Standard e HighPerformance SKUs.
2. **Não é possível** redimensionar de SKUs de padrão/Basic/HighPerformance toohello SKUs de VpnGw2/VpnGw1/VpnGw3 novo. Tem de, em vez disso, [migrar](#migrate) toohello SKUs de novo.

###  <a name="migrate"></a>Migrar a partir do antigo SKUs toohello SKUs de novo

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
