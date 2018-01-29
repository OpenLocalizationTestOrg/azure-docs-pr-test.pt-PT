---
title: 'Ligar a rede no local a uma rede virtual do Azure: Rede de VPNs: Portal | Microsoft Docs'
description: "Passos para criar uma ligação IPsec da sua rede no local a uma rede virtual do Azure através da Internet pública. Estes passos ajudam-no a criar uma ligação de Gateway de Rede de VPNs em vários sites com o portal."
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
ms.date: 11/17/2017
ms.author: cherylmc
ms.openlocfilehash: 4f5e249238020429b6c6e0d39c580c83bc43969e
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/18/2017
---
# <a name="create-a-site-to-site-connection-in-the-azure-portal"></a>Criar uma ligação Site a Site no portal do Azure

Este artigo mostra-lhe como utilizar o portal do Azure para criar uma ligação de gateway de VPN de Site para Site a partir da sua rede no local para a VNet. Os passos deste artigo aplicam-se ao modelo de implementação Resource Manager. Também pode criar esta configuração ao utilizar uma ferramenta de implementação diferente ou modelo de implementação ao selecionar uma opção diferente da lista seguinte:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Uma ligação de gateway de VPN de Site para Site é utilizada para ligar a sua rede no local a uma rede virtual do Azure através de um túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Este tipo de ligação requer um dispositivo VPN localizado no local que tenha um endereço IP público com acesso exterior atribuído ao mesmo. Para obter mais informações sobre o gateways de VPN, veja [About VPN gateway (Acerca do gateway de VPN)](vpn-gateway-about-vpngateways.md).

![Diagrama da ligação de Gateway de Rede de VPNs em vários sites](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Antes de começar

Antes de iniciar a configuração, verifique se cumpre os seguintes critérios:

* Certifique-se de que tem um dispositivo VPN compatível e alguém que o possa configurar. Para obter mais informações sobre os dispositivos VPN compatíveis e a configuração do dispositivo, consulte [About VPN Devices (Acerca dos Dispositivos VPN)](vpn-gateway-about-vpn-devices.md).
* Verifique se tem um endereço IP IPv4 público com acesso exterior para o seu dispositivo VPN. Este endereço IP não pode estar localizado atrás de um NAT.
* Se não estiver familiarizado com os intervalos de endereços IP localizados na configuração de rede no local, tem de se coordenar com alguém que consiga fornecer esses detalhes. Ao criar esta configuração, tem de especificar prefixos de intervalo de endereços IP que o Azure irá encaminhar para a sua localização no local. Nenhuma das sub-redes da rede local pode sobrepor as sub-redes de rede virtual a que pretende ligar. 

### <a name="values"></a>Valores de exemplo

Os exemplos neste artigo utilizam os seguintes valores. Pode utilizar estes valores para criar um ambiente de teste ou consultá-los para compreender melhor os exemplos neste artigo. Para obter mais informações sobre as definições do Gateway de VPN em geral, veja [Sobre as Definições do Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md).

* **Nome da VNet:** TestVNet1
* **Espaço de Endereços:** 10.11.0.0/16 e 10.12.0.0/16 (opcional neste exercício)
* **Subscrição:** a subscrição que pretende utilizar
* **Grupo de Recursos:** TestRG1
* **Localização:** E.U.A. Leste
* **Sub-rede:** FrontEnd: 10.11.0.0/24, BackEnd: 10.12.0.0/24 (opcional neste exercício)
* **Nome da Sub-rede do Gateway:** GatewaySubnet (será preenchido automaticamente no portal)
* **Intervalo de endereços da Sub-rede do Gateway:** 10.11.255.0/27
* **Servidor DNS:** Opcional. O endereço IP do seu servidor DNS.
* **Nome do Gateway de Rede Virtual:** VNet1GW
* **IP Público:** VNet1GWIP
* **Tipo de VPN:** Baseada na rota
* **Tipo de Ligação:** Ste a site (IPsec)
* **Tipo de Gateway:** VPN
* **Nome do Gateway de Rede Local:** Site2
* **Nome da Ligação:** VNet1toSite2
* **Chave partilhada:** neste exemplo, utilizaremos abc123. No entanto, pode utilizar uma chave qualquer, desde que seja compatível com o seu hardware de VPN. O mais importante é que os valores correspondam em ambos os lados da ligação.

## <a name="CreatVNet"></a>1. Criar uma rede virtual

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Especificar um servidor DNS

O DNS não tem de criar uma ligação de Site a Site. No entanto, se pretender ter a resolução de nomes para recursos que são implementados para a sua rede virtual, deve especificar um servidor DNS. Esta definição permite-lhe especificar o servidor DNS que pretende utilizar para a resolução de nomes desta rede virtual. Não cria um servidor DNS. Para obter mais informações sobre a resolução de nomes, veja [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Resolução de Nomes para VMs e instâncias de função).

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Criar a sub-rede de gateway

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Criar o gateway de VPN

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Criar o gateway de rede local

O gateway de rede local refere-se normalmente à sua localização no local. Dê um nome ao site pelo qual o Azure se possa referir ao mesmo e especifique o endereço IP do dispositivo VPN no local para o qual vai criar uma ligação. Também pode especificar os prefixos do endereço IP que vai ser encaminhado através do gateway de VPN para o dispositivo VPN. Os prefixos do endereço que especificar são os que estão localizados na sua rede no local. Se a sua rede no local for alterada ou se precisar de alterar o endereço IP público para o dispositivo VPN, pode atualizar facilmente os valores mais tarde.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Configurar o dispositivo VPN

As ligações de Site a Site para uma rede no local requerem um dispositivo VPN. Neste passo, configure o seu dispositivo VPN. Quando configurar o dispositivo VPN, irá precisar do seguinte:

- Uma chave partilhada. Esta é a mesma chave partilhada que especifica ao criar a ligação VPN de Site a Site. Nos nossos exemplos, iremos utilizar uma chave partilhada básica. Deve gerar uma chave mais complexa para utilizar.
- O endereço IP Público do gateway de rede virtual. Pode ver o endereço IP público através do portal do Azure, do PowerShell ou da CLI. Para encontrar o endereço IP Público do seu gateway de VPN através do portal do Azure, navegue para **Gateways de rede virtual** e, em seguida, clique no nome do gateway.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Criar a ligação VPN

Crie a ligação de Rede de VPNs entre o gateway de rede virtual e o dispositivo VPN no local.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Verificar a ligação VPN

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>Ligar a uma máquina virtual

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>Como repor um gateway de VPN

Repor o gateway de VPN do Azure é útil se perder a conectividade VPN em vários locais num ou mais túneis de rede de VPNs. Nesta situação, os dispositivos VPN no local estão todos a funcionar corretamente, mas não podem estabelecer túneis IPsec com os gateways de VPN do Azure. Para obter os passos, veja [Reset a VPN gateway](vpn-gateway-resetgw-classic.md) (Repor um gateway de VPN).

## <a name="resize"></a>Como alterar um SKU de gateway (redimensionar um gateway)

Para obter os passos para alterar um SKU de gateway, veja [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku) (SKUs de gateway).

## <a name="addconnect"></a>Como adicionar outra ligação a um gateway de VPN

Pode adicionar mais ligações, desde que nenhum desses espaços de endereços se sobreponha entre as ligações.

1. Para adicionar outra ligação, navegue para o gateway de VPN e clique em **Ligações** para abrir a página Ligações.
2. Clique em **+Adicionar** para adicionar a ligação. Ajuste o tipo de ligação para refletir se é VNet a VNet (se estiver a ligar a outro gateway de VPN) ou Site a Site.
3. Se estiver a ligar através de Site a Site e ainda não tiver criado um gateway de rede local para o site ao qual se quer ligar, pode criar um novo.
4. Especifique a chave partilhada que pretende utilizar e clique em **OK** para criar a ligação.

## <a name="next-steps"></a>Passos seguintes

* Para obter informações sobre o BGP, veja a [Descrição Geral do BGP](vpn-gateway-bgp-overview.md) e [Como configurar o BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Para obter informações sobre o túnel forçado, veja [About forced tunneling](vpn-gateway-forced-tunneling-rm.md) (Acerca do túnel forçado).
* Para obter informações sobre ligações Altamente Disponíveis Ativo-Ativo, veja [Premissas cruzadas de disponibilidade elevada e ligação VNet para VNet](vpn-gateway-highlyavailable.md).
* Para obter informações sobre como limitar o tráfego de rede para os recursos numa rede virtual, veja [Segurança da rede](../virtual-network/security-overview.md).
* Para obter informações sobre a forma como o Azure encaminha o tráfego entre os recursos do Azure, do local e da Internet veja [Encaminhamento de tráfego da rede virtual](../virtual-network/virtual-networks-udr-overview.md).
* Para obter informações sobre como criar uma ligação VPN de Site a Site com o modelo Azure Resource Manager, veja [Create a Site-to-Site VPN Connection](https://azure.microsoft.com/resources/templates/101-site-to-site-vpn-create/) (Criar uma Ligação VPN de Site a Site).
* Para obter informações sobre como criar uma ligação VPN de Vnet a Vnet com o modelo Azure Resource Manager, veja [Deploy HBase geo replication](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-geo/) (Implementar georreplicação do HBase).
