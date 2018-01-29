---
title: "Descrição geral das configurações de elevada disponibilidade com Gateways de VPN do Azure | Microsoft Docs"
description: "Este artigo disponibiliza uma descrição geral das opções de configurações de elevada disponibilidade através de Gateways de VPN do Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 3708a2f7c445a161f02416cf8427b1707e1db8f0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Conectividade em Vários Locais de Elevada Disponibilidade e VNet a VNet
Este artigo disponibiliza uma descrição geral das opções de configurações de elevada disponibilidade para a conectividade em vários locais e VNet a VNet através dos Gateways de VPN do Azure.

## <a name = "activestandby"></a>Sobre a redundância de gateway de VPN do Azure
Todos os Gateways de VPN do Azure consistem em duas instâncias numa configuração ativa-em espera. Caso ocorra uma manutenção planeada ou uma interrupção não planeada na instância ativa, a instância em espera assume o controlo (ativação pós-falha) automaticamente e retoma as ligações VPN S2S ou VNet a VNet. A mudança causará uma breve interrupção. Nas manutenções planeadas, a conectividade deve ser restabelecida ao fim de 10 a 15 segundos. Relativamente a problemas não planeados, a recuperação da ligação demorará mais tempo, cerca de um minuto a um minuto e meio, na pior das hipóteses. Para as ligações de cliente VPN S2S ao gateway, as ligações P2S serão desligadas e os utilizadores terão de restabelecê-las a partir dos computadores cliente.

![Ativa- em espera](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Conectividade em Vários Locais de Elevada Disponibilidade
Para proporcionar melhor disponibilidade para as ligações em vários locais, há algumas opções disponíveis:

* Vários dispositivos VPN no local
* Gateway de VPN do Azure ativo-ativo
* Uma combinação de ambos

### <a name = "activeactiveonprem"></a>Vários dispositivos VPN no local
Pode utilizar vários dispositivos VPN da sua rede no local para ligar ao Gateway de VPN do Azure, conforme mostrado no diagrama seguinte:

![Várias VPNs no Local](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Esta configuração fornece vários túneis ativos do mesmo gateway de VPN do Azure para os dispositivos no local na mesma localização. Existem alguns requisitos e limitações:

1. Tem de criar várias ligações VPN S2S dos dispositivos VPN para o Azure. Quando liga múltiplos dispositivos VPN da mesma rede no local ao Azure, tem de criar um gateway de rede local para cada um desses dispositivos e uma ligação do gateway de VPN do Azure ao gateway de rede local.
2. Os gateways de rede local correspondentes aos dispositivos VPN têm de ter endereços IP públicos exclusivos na propriedade "GatewayIpAddress".
3. O BGP é necessário para esta configuração. Cada gateway de rede local que representa um dispositivo VPN tem de ter um endereço IP de elemento de rede BGP especificado na propriedade “BgpPeerIpAddress”.
4. O campo da propriedade AddressPrefix de cada gateway de rede local não se pode sobrepor. Deve especificar "BgpPeerIpAddress" no formato /32 CIDR no campo AddressPrefix, por exemplo, 10.200.200.254/32.
5. Deve utilizar o BGP para anunciar os mesmos prefixos dos mesmos prefixos da rede no local ao gateway de VPN do Azure e o tráfego será encaminhado através destes túneis simultaneamente.
6. Cada ligação é contabilizada face ao número máximo de túneis do seu gateway de VPN do Azure, 10 para os SKUs Básico e Standard e 30 para o SKU HighPerformance. 

Nesta configuração, o gateway de VPN do Azure continua no modo ativo-em espera, pelo que o mesmo comportamento de ativação pós-falha e a breve interrupção ainda vão ocorrer, conforme descrito [anteriormente](#activestandby). Contudo, esta configuração protege de falhas ou interrupções na sua rede no local e nos seus dispositivos VPN.

### <a name="active-active-azure-vpn-gateway"></a>Gateway de VPN do Azure ativo-ativo
Agora, pode criar um gateway de VPN do Azure numa configuração ativa-ativa, em que ambas as instâncias das VMs do gateway estabelecem túneis VPN S2S para o dispositivo VPN no local, conforme mostrado no diagrama seguinte:

![Ativa-ativa](./media/vpn-gateway-highlyavailable/active-active.png)

Nesta configuração, cada instância do gateway do Azure terá um endereço IP público exclusivo e estabelecerá um túnel VPN S2S IPsec/IKE para o dispositivo VPN no local especificado no gateway e na ligação de rede no local. Tenha em conta que ambos os túneis VPN fazem, efetivamente, parte da mesma ligação. Continua a ter de configurar o dispositivo VPN no local para aceitar ou estabelecer dois túneis VPN S2S para aqueles dois endereços IP públicos do gateway de VPN do Azure.

Uma vez que as instâncias do gateway do Azure estão numa configuração ativa-ativa, o tráfego da rede virtual do Azure para a rede no local continua a ser encaminhado através de ambos os túneis em simultâneo, mesmo que o dispositivo VPN no local possa preferir um em detrimento do outro. Tenha em atenção que o mesmo fluxo de TCP ou UDP atravessará sempre o mesmo túnel ou caminho, a não ser que ocorra um evento de manutenção numa das instâncias.

Quando se verifica um evento de manutenção planeada ou não planeada numa instância do gateway, o túnel IPsec dessa instância para o dispositivo VPN no local será desligado. As rotas correspondentes nos seus dispositivos VPN devem ser removidas ou retiradas automaticamente, para que o tráfego mude para o outro túnel IPsec ativo. Do lado do Azure, a mudança dá-se automaticamente da instância afetada para a ativa.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Redundância dupla: gateways de VPN ativos-ativos para redes do Azure e redes no local
A opção mais fiável é combinar os gateways ativos-ativos na sua rede e no Azure, conforme mostrado no diagrama abaixo.

![Redundância dupla](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

Aqui, pode criar e configurar o gateway de VPN do Azure numa configuração ativa-ativa e criar dois gateways de rede no local e duas ligações para os seus dois dispositivos VPN no local, conforme descrito acima. O resultado é uma conectividade de malha completa de quatro túneis IPsec entre a rede virtual do Azure e a sua rede no local.

Todos os gateways e túneis estão ativos no lado do Azure, pelo que o tráfego se vai propagar pelos quatro túneis em simultâneo, embora cada fluxo de TCP ou UDP volte a seguir, novamente, o mesmo túnel ou caminho do lado do Azure. Não obstante propagar o tráfego, poderá ver um débito ligeiramente superior nos túneis IPsec. O principal objetivo desta configuração é a elevada disponibilidade. E devido à natureza estatística da propagação, é difícil disponibilizar as medidas em como as diferentes condições de tráfego da aplicação vão afetar o débito agregado.

Esta topologia vai exigir dois gateways de rede local e duas ligações para suportar o par de dispositivos VPN no local e o BGP é necessário para permitir ambas as ligações à mesma rede no local. Estes requisitos são os mesmos que os indicados [acima](#activeactiveonprem). 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Conectividade de VNet a VNet de elevada através de Gateways de VPN do Azure
Também pode aplicar a mesma configuração ativa-ativa a ligações VNet a VNet do Azure. Pode criar gateways de VPN ativos-ativos para ambas as redes virtuais e ligá-los para formar a conectividade de malha completa de quatro túneis entre as duas VNets, conforme mostrado no diagrama abaixo:

![VNet a VNet](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

Desta forma, é garantido que há sempre um par de túneis entre as duas redes virtuais para eventuais eventos de manutenção planeada, proporcionando uma disponibilidade ainda melhor. Apesar de a mesma topologia para conectividade em vários locais precisar de duas ligações, a topologia de VNet a VNet mostrada anteriormente requer apenas uma ligação para cada gateway. Além disso, o BGP é opcional, a não ser que o encaminhamento do trânsito através da ligação VNet a VNet seja um requisito.

## <a name="next-steps"></a>Passos seguintes
Veja [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections (Configurar Gateways de VPN Ativos-Ativos para Ligações em Vários Locais e VNet a VNet)](vpn-gateway-activeactive-rm-powershell.md) para obter os passos para configurar ligações ativas-ativas em vários locais e VNet a VNet.

