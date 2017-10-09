---
title: aaaOverview do BGP com Gateways de VPN do Azure | Microsoft Docs
description: "Este artigo fornece uma descrição geral do BGP com Gateways de VPN do Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a>Descrição geral do BGP com Gateways de VPN do Azure
Este artigo fornece uma descrição geral do suporte BGP (Border Gateway Protocol) nos Gateways de VPN do Azure.

BGP é Olá protocolo de encaminhamento padrão utilizado normalmente na Olá tooexchange encaminhamento e acessibilidade informação de Internet entre duas ou mais redes. Quando utilizado no contexto de Olá de redes virtuais do Azure, BGP permite que os Gateways de VPN do Azure Olá e os dispositivos VPN no local, denominados elementos BGP ou vizinhos, tooexchange "rotas" que informarão ambos os gateways no Olá disponibilidade e acessibilidade os prefixos toogo através de gateways de Olá ou routers envolvidos. BGP também pode ativar o encaminhamento de tráfego entre várias redes ao propagar rotas um gateway BGP aprende de um tooall de elemento de rede BGP outros elementos de rede BGP. 

## <a name="why-use-bgp"></a>Porquê utilizar o BGP?
O BGP é uma funcionalidade opcional que pode utilizar com os gateways de VPN do Azure Baseados na Rota. Também deve certificar-se de que os dispositivos VPN no local suportam o BGP, antes de ativar a funcionalidade de Olá. Pode continuar toouse gateways de VPN do Azure e os dispositivos VPN no local sem o BGP. É Olá equivalente a utilizar rotas estáticas (sem BGP) *vs* utilizar encaminhamento dinâmico com BGP entre as suas redes e do Azure.

O BGP possui várias vantagens e novas capacidades:

### <a name="support-automatic-and-flexible-prefix-updates"></a>Suporte de atualizações de prefixos automáticas e flexíveis
Com o BGP, só precisa de toodeclare um prefixo mínimo tooa específico elemento de rede BGP túnel IPsec S2S VPN Olá. Pode ser tão pequena como um prefixo de anfitrião (/ 32) de Olá endereço IP do elemento de rede BGP do seu dispositivo VPN no local. Pode controlar que prefixos no local rede pretende tooadvertise tooAzure tooallow tooaccess a rede Virtual do Azure.

Também pode anunciar prefixos maiores, que podem incluir alguns dos seus prefixos de endereço VNet, tais como um grande privado espaço de endereços IP (por exemplo, 10.0.0.0/8). Tenha em atenção que os prefixos de Olá não podem ser idênticos a nenhum dos seus prefixos VNet. As rotas idênticas tooyour prefixos de VNet serão rejeitados.

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a>Suporte de vários túneis entre uma VNet e um site no local, com ativação pós-falha automática baseada no BGP
Pode estabelecer várias ligações entre a VNet do Azure e os dispositivos VPN no local na Olá mesma localização. Esta capacidade proporciona vários túneis (caminhos) entre duas redes de Olá uma configuração de ativo-ativo. Se um dos túneis Olá estiver desligado, rotas Olá de correspondentes serão retiradas através do BGP e tráfego de Olá automaticamente desvia toohello restantes túneis.

Olá diagrama a seguir mostra um exemplo simples desta configuração de elevada disponibilidade:

![Vários caminhos ativos](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a>Suporte do encaminhamento do tráfego entre as suas redes no local e várias VNets do Azure
BGP permite que vários gateways toolearn e propaguem os prefixos a partir de redes diferentes, se estiverem direta ou indiretamente ligados. Esta opção pode ativar o encaminhamento de tráfego com os gateways de VPN do Azure entre os sites no local ou entre várias Redes Virtuais do Azure.

Olá diagrama seguinte mostra um exemplo de uma topologia multi-HOP com vários caminhos em que o tráfego pode transitar entre Olá duas redes no local através de gateways de VPN do Azure dentro Olá Networks Microsoft:

![Tráfego multi-hop](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a>FAQ SOBRE O BGP
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a>Passos seguintes
Consulte [introdução ao BGP nos gateways de VPN do Azure](vpn-gateway-bgp-resource-manager-ps.md) para passos tooconfigure BGP para as ligações de VNet a VNet e em vários locais.

