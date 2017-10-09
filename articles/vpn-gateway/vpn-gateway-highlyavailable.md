---
title: "aaaOverview das configurações de elevada disponibilidade com Gateways de VPN do Azure | Microsoft Docs"
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
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Conectividade em Vários Locais de Elevada Disponibilidade e VNet a VNet
Este artigo disponibiliza uma descrição geral das opções de configurações de elevada disponibilidade para a conectividade em vários locais e VNet a VNet através dos Gateways de VPN do Azure.

## <a name = "activestandby"></a>Sobre a redundância de gateway de VPN do Azure
Todos os Gateways de VPN do Azure consistem em duas instâncias numa configuração ativa-em espera. Para manutenção planeada ou não planeada interrupção que ocorre a instância ativa toohello, instância de reserva dinâmica Olá seria assumir o controlo (ativação pós-falha) automaticamente e retomar Olá S2S VPN ou ligações VNet a VNet. Olá mudar irá causar uma interrupção breve. Manutenção planeada, a conectividade de Olá deve ser restaurada dentro de 10 segundos too15. Para problemas não planeados, recuperação da ligação Olá será maior, sobre 1 too1 minuto e um meio minutos caso pior Olá. Para o gateway de toohello de ligações de cliente P2S VPN, ligações P2S de Olá serão desligadas e utilizadores Olá terá tooreconnect provenientes de máquinas de cliente Olá.

![Ativa- em espera](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Conectividade em Vários Locais de Elevada Disponibilidade
disponibilidade de melhor tooprovide para sua cruzada local ligações, existem algumas das opções disponíveis:

* Vários dispositivos VPN no local
* Gateway de VPN do Azure ativo-ativo
* Uma combinação de ambos

### <a name = "activeactiveonprem"></a>Vários dispositivos VPN no local
Pode utilizar vários dispositivos VPN do seu gateway de VPN do Azure do local rede tooconnect tooyour, conforme mostrado no Olá diagrama a seguir:

![Várias VPNs no Local](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Esta configuração proporciona vários túneis de Active Directory de Olá mesmos VPN do Azure gateway tooyour dispositivos no local no Olá mesma localização. Existem alguns requisitos e limitações:

1. É necessário toocreate várias ligações S2S VPN do seu tooAzure de dispositivos VPN. Quando ligar vários dispositivos VPN de Olá tooAzure de rede do mesmo no local, tem de toocreate gateway de rede local um para cada dispositivo VPN e uma ligação de gateway de VPN do Azure gateway toohello rede local.
2. os gateways de rede local Olá correspondente tooyour dispositivos VPN tem de ter os endereços IP públicos exclusivos Olá "GatewayIpAddress" propriedade.
3. O BGP é necessário para esta configuração. Cada gateway de rede local que representa um dispositivo VPN tem de ter um endereço IP do elemento BGP exclusivo especificado na propriedade de "BgpPeerIpAddress" Olá.
4. campo de propriedade Olá AddressPrefix no cada gateway de rede local não podem sobrepor. Deve especificar Olá "BgpPeerIpAddress" no /32 formato CIDR no campo de AddressPrefix Olá, por exemplo, 10.200.200.254/32.
5. Deve utilizar o BGP tooadvertise Olá mesmos prefixos de Olá mesmo no local de rede prefixos tooyour VPN gateway do Azure e Olá será possível reencaminhar o tráfego através destes túneis em simultâneo.
6. Cada ligação é a contados tendo em conta o número máximo de Olá de túneis para o gateway de VPN do Azure, 10 para básico e padrão SKUs e 30 para HighPerformance SKU. 

Nesta configuração, gateway de VPN do Azure Olá ainda está em modo de reserva dinâmica do Active Directory, Olá, por isso, o mesmo comportamento de ativação pós-falha e interrupção breve ainda acontecerá de tal como descrito [acima](#activestandby). Contudo, esta configuração protege de falhas ou interrupções na sua rede no local e nos seus dispositivos VPN.

### <a name="active-active-azure-vpn-gateway"></a>Gateway de VPN do Azure ativo-ativo
Agora, pode criar um gateway de VPN do Azure uma configuração de ativo-ativo onde diagrama ambas as instâncias de gateway Olá que VMS estabelecerá a que s2s VPN túneis tooyour dispositivo VPN no local, como mostrado Olá seguintes:

![Ativa-ativa](./media/vpn-gateway-highlyavailable/active-active.png)

Nesta configuração, cada instância de gateway do Azure terá um único endereço IP público e cada irão estabelecer uma VPN S2S de IPsec/IKE túnel tooyour no dispositivo VPN local especificado no seu gateway de rede local e a ligação. Tenha em atenção que ambos os túneis VPN são realmente parte Olá mesma ligação. Ainda será necessário tooconfigure sua tooaccept de dispositivo VPN no local ou estabelecer dois S2S VPN túneis toothose dois VPN do Azure gateway endereços IP públicos.

Porque as instâncias de gateway do Azure Olá estão numa configuração de ativo-ativo, o tráfego de Olá do seu tooyour de rede virtual do Azure no local rede será encaminhada através de ambos os túneis em simultâneo, mesmo que o dispositivo VPN no local poderá favor um túnel de ativação pós-falha Olá outro. Tenha em atenção embora Olá mesmo fluxo TCP ou UDP será sempre atravessar Olá mesmo túnel ou caminho, a menos que um evento de manutenção acontece dos instâncias Olá.

Quando uma manutenção planeada ou não planeado eventos acontece tooone uma instância de gateway, túnel IPsec de Olá de tooyour essa instância no local dispositivo VPN será desligado. Olá rotas correspondentes nos seus dispositivos VPN devem ser removidas ou retiradas automaticamente para que o tráfego de Olá vai ser mudado através de toohello outro túnel IPsec Active Directory. No lado do Azure Olá, mudar Olá acontecerá automaticamente da instância do Olá afetado instância toohello Active Directory.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Redundância dupla: gateways de VPN ativos-ativos para redes do Azure e redes no local
opção mais fiável Olá é toocombine Olá ativo-ativo gateways da rede e o Azure, conforme mostrado no diagrama de Olá abaixo.

![Redundância dupla](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

Aqui pode criar e configurar o gateway de VPN do Azure Olá uma configuração de ativo-ativo e criar dois gateways de rede local e duas ligações para os dois no local dispositivos VPN, tal como descrito acima. resultado de Olá é uma conectividade de malha completa dos 4 túneis IPsec entre a rede virtual do Azure e a sua rede no local.

Todos os gateways e túneis estão ativos Olá do lado do Azure, pelo Olá tráfego será propagar-se entre todos os 4 túneis em simultâneo, apesar de cada TCP ou UDP fluxo será novamente siga Olá túnel mesmo ou caminho de hello do lado do Azure. Embora pelo tráfego Olá, poderá ver ligeiramente melhorar o débito através de túneis IPsec de Olá, Olá objetivo primário esta configuração é de elevada disponibilidade. E devido toohello análises natureza Olá propagando-se, é difícil tooprovide medida de Olá no tráfego de aplicações como diferentes condições afetarão o débito agregado Olá.

Esta topologia necessitarão de dois gateways de rede local e o par de Olá toosupport duas ligações de dispositivos VPN no local e o BGP é necessário tooallow Olá duas ligações toohello mesma rede no local. Estes requisitos são Olá mesmo como Olá [acima](#activeactiveonprem). 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Conectividade de VNet a VNet de elevada através de Gateways de VPN do Azure
Olá mesma configuração de ativo-ativo também pode aplicar tooAzure VNet a VNet ligações. Pode criar gateways de VPN de ativo-ativo para ambas as redes virtuais e ligue-Olá tooform em conjunto mesmo completa mesh a conectividade dos 4 túneis entre Olá duas VNets, conforme mostrado no Olá diagrama abaixo:

![VNet a VNet](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

Isto garante que são sempre um par de túneis entre duas redes virtuais Olá para quaisquer eventos de manutenção planeada, fornecendo disponibilidade ainda mais. Apesar de Olá mesma topologia para conectividade entre instalações, necessita de duas ligações, topologia de VNet a VNet Olá mostrada acima irá necessitar de apenas uma ligação para cada gateway. Além disso, o BGP é opcional, a menos que o encaminhamento de trânsito através de Olá ligação VNet a VNet é necessário.

## <a name="next-steps"></a>Passos seguintes
Consulte [configurar Gateways de VPN de ativo-ativo em vários locais e ligações VNet a VNet](vpn-gateway-activeactive-rm-powershell.md) para passos tooconfigure ativo-ativo em vários locais e ligações VNet a VNet.

