---
title: 'Ligar o seu tooan de rede no local rede virtual do Azure: VPN Site a Site: Portal | Microsoft Docs'
description: "Uma ligação de IPsec do seu local de rede tooan rede virtual do Azure através de toocreate de passos Olá Internet pública. Estes passos irão ajudá-lo a criar uma ligação de Gateway de VPN de Site para Site em vários locais através do portal Olá."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Criar uma ligação Site a Site no Olá portal do Azure

Este artigo mostra como toouse Olá toocreate portal do Azure uma ligação de gateway VPN de Site para Site da sua toohello de rede no local VNet. passos de Olá neste artigo aplicam-se o modelo de implementação do Resource Manager toohello. Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Uma ligação de gateway VPN de Site a Site é utilizado tooconnect tooan rede virtual do Azure de rede no local através de um túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Este tipo de ligação requer uma VPN dispositivos localizado no local que tenha um tooit de atribuída de endereço IP público com acesso exterior. Para obter mais informações sobre o gateways de VPN, veja [About VPN gateway (Acerca do gateway de VPN)](vpn-gateway-about-vpngateways.md).

![Diagrama da ligação de Gateway de Rede de VPNs em vários sites](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Antes de começar

Certifique-se de que cumpriu Olá os seguintes critérios antes de iniciar a configuração:

* Certifique-se de um dispositivo VPN compatível e alguém que seja capaz de tooconfigure-lo. Para obter mais informações sobre os dispositivos VPN compatíveis e a configuração do dispositivo, consulte [About VPN Devices (Acerca dos Dispositivos VPN)](vpn-gateway-about-vpn-devices.md).
* Verifique se tem um endereço IP IPv4 público com acesso exterior para o seu dispositivo VPN. Este endereço IP não pode estar localizado atrás de um NAT.
* Se não estiver familiarizado com intervalos de endereços IP Olá localizados na configuração de rede no local, tem de toocoordinate com alguém que consiga fornecer esses detalhes. Ao criar esta configuração, tem de especificar que o Azure irá encaminhar localização no local de tooyour dos prefixos de intervalo de endereços para IP Olá. Nenhuma das sub-redes Olá da sua rede no local pode através de lap com sub-redes da rede virtual Olá que pretende que sejam tooconnect para. 

### <a name="values"></a>Valores de exemplo

Exemplos de Olá neste artigo utilizam Olá os seguintes valores. Pode utilizar estes toocreate de valores num ambiente de teste, ou consulte toothem toobetter compreender exemplos Olá neste artigo.

* **Nome da VNet:** TestVNet1
* **Espaço de Endereços:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (opcional para este exercício)
* **Sub-redes:**
  * Front-End: 10.11.0.0/24
  * Back-End: 10.12.0.0/24 (opcional para este exercício)
* **GatewaySubnet:** 10.11.255.0/27
* **Grupo de Recursos:** TestRG1
* **Localização:** E.U.A. Leste
* **Servidor DNS:** Opcional. endereço IP Hello do servidor DNS.
* **Nome do Gateway de Rede Virtual:** VNet1GW
* **IP Público:** VNet1GWIP
* **Tipo de VPN:** Baseada na rota
* **Tipo de Ligação:** Ste a site (IPsec)
* **Tipo de Gateway:** VPN
* **Nome do Gateway de Rede Local:** Site2
* **Nome da Ligação:** VNet1toSite2

## <a name="CreatVNet"></a>1. Criar uma rede virtual

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Especificar um servidor DNS

DNS não é necessário toocreate um Site para Site ligação. No entanto, se quiser toohave resolução de nomes de recursos que são implementadas tooyour rede virtual, deve especificar um servidor DNS. Esta definição permite-lhe especificar o servidor DNS Olá que pretende que toouse para a resolução de nome para esta rede virtual. Não cria um servidor DNS. Para obter mais informações sobre a resolução de nomes, veja [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Resolução de Nomes para VMs e instâncias de função).

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Criar a sub-rede do gateway Olá

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Criar gateway de VPN Olá

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Criar gateway de rede local Olá

gateway de rede local Olá refere-se normalmente localização do tooyour no local. Dê site Olá um nome pelo qual Azure pode consulte tooit, em seguida, especifique o endereço IP Olá de toowhich de dispositivo VPN do Olá no local, irá criar uma ligação. Também especificar prefixos de endereços IP Olá serão encaminhados através de um dispositivo VPN do Olá VPN gateway toohello. especificar prefixos de endereços de Olá são prefixos Olá localizados na sua rede no local. Se as alterações de rede no local ou precisar de endereço IP público do toochange Olá para o dispositivo VPN Olá, pode atualizar facilmente valores hello mais tarde.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Configurar o dispositivo VPN

Rede do ligações site a Site tooan no local requer um dispositivo VPN. Neste passo, configure o seu dispositivo VPN. Quando configurar o seu dispositivo VPN, terá de seguinte Olá:

- Uma chave partilhada. Isto é Olá mesmo partilhado chave que especificar ao criar a ligação de VPN de Site para Site. Nos nossos exemplos, iremos utilizar uma chave partilhada básica. Recomendamos que geram um toouse chave mais complexa.
- Olá endereço IP público do gateway da rede virtual. Pode ver o endereço IP público Olá utilizando Olá portal do Azure, PowerShell ou a CLI. Olá toofind endereço IP público do seu gateway VPN utilizando Olá portal do Azure, navegue até demasiado**gateways da rede Virtual**, em seguida, clique no nome de Olá do seu gateway.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Criar a ligação de VPN Olá

Crie a ligação de VPN de Olá Site a Site entre o gateway de rede virtual e o dispositivo VPN no local.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Certifique-se a ligação de VPN Olá

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa máquina

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>Como tooreset um gateway de VPN

Repor o gateway de VPN do Azure é útil se perder a conectividade VPN em vários locais num ou mais túneis de rede de VPNs. Nesta situação, os dispositivos VPN no local estão todos os a funcionar corretamente, mas são tooestablish não é possível túneis IPsec com gateways de VPN do Azure Olá. Para obter os passos, veja [Reset a VPN gateway](vpn-gateway-resetgw-classic.md) (Repor um gateway de VPN).

## <a name="resize"></a>Como toochange um gateway de SKU (redimensionar um gateway)

Para obter Olá passos toochange um SKU de gateway, consulte [SKUs de Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="next-steps"></a>Passos seguintes

* Para informações sobre o BGP, consulte Olá [descrição geral do BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Para obter informações sobre o Túnel Forçado, veja [Acerca do Túnel Forçado](vpn-gateway-forced-tunneling-rm.md).
* Para obter informações sobre ligações Altamente Disponíveis Ativo-Ativo, veja [Premissas cruzadas de disponibilidade elevada e ligação VNet para VNet](vpn-gateway-highlyavailable.md).
