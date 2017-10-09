---
title: "Configurar a imposição do túnel para ligações do Azure Site a Site: Resource Manager | Microsoft Docs"
description: "Como tooyour do tráfego de Internet vinculados back do tooredirect ou 'force' todos os localização no local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>Configurar a imposição do túnel utilizando o modelo de implementação Azure Resource Manager Olá

Imposição do túnel permite redirecionar ou "forçar" todos os vinculado à Internet tráfego back tooyour localização no local através de um túnel VPN Site a Site para inspeção e auditoria. Este é um requisito de segurança críticas para TI empresariais de maioria das políticas. Sem a imposição do túnel, o tráfego vinculado à Internet do seu VMs no Azure sempre atravessa da infraestrutura de rede do Azure diretamente saída toohello Internet, sem Olá opção tooallow, tráfego de Olá tooinspect ou de auditoria. Acesso à Internet não autorizado pode provocar potencialmente tooinformation divulgação ou outros tipos de falhas de segurança.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

Este artigo explica como configurar forçado túnel para redes virtuais criadas com o modelo de implementação do Resource Manager Olá. Imposição do túnel pode ser configurado utilizando o PowerShell, não através do portal Olá. Se quiser tooconfigure imposição do túnel para o modelo de implementação clássica Olá, selecione artigo clássico Olá na lista pendente a seguir:

> [!div class="op_single_selector"]
> * [PowerShell – Clássica](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell – Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>Prestes imposição do túnel

Olá seguinte diagrama ilustra funciona como imposição de túnel. 

![Túnel Forçado](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

No exemplo de Olá acima, Olá front-end sub-rede não está a ser forçada em túnel. Olá cargas de trabalho na sub-rede do front-end de Olá podem continuar tooaccept e responder a pedidos de toocustomer de Olá Internet diretamente. Olá sub-redes de camada média dimensão que e back-end são forçadas em túnel. Quaisquer ligações de saída do toohello duas sub-redes Internet será tooan forçada ou redirecionado novamente o site de no local através de um dos Olá que túneis S2S VPN.

Isto permite-lhe toorestrict e inspecionar o acesso à Internet das suas máquinas virtuais ou serviços em nuvem na Azure, ao continuar tooenable a arquitetura do serviço de várias camadas necessárias. Se não houver nenhuma cargas de trabalho para a Internet nas suas redes virtuais, também pode aplicar forçada túnel toohello todo redes virtuais.

## <a name="requirements-and-considerations"></a>Requisitos e considerações

Imposição do túnel no Azure está configurado através de rotas definidas pelo utilizador de rede virtual. Redirecionar o tráfego tooan no local site é expresso como um gateway de VPN do Azure de toohello de rota predefinida. Para obter mais informações sobre o encaminhamento definido pelo utilizador e redes virtuais, consulte [rotas definidas pelo utilizador e reencaminhamento IP](../virtual-network/virtual-networks-udr-overview.md).

* Cada sub-rede da rede virtual tem uma tabela de encaminhamento incorporada, do sistema. tabela de encaminhamento de sistema de Olá tem Olá seguintes três grupos de rotas:
  
  * **Rotas de VNet locais:** diretamente toohello destino VMs no Olá mesma rede virtual.
  * **No local rotas:** toohello VPN gateway do Azure.
  * **Rota predefinida:** toohello diretamente à Internet. Pacotes destinados a toohello endereços IP privados não abrangidos por rotas Olá dois anteriores são ignorados.
* Este procedimento utiliza rotas definidas pelo utilizador (UDR) toocreate um tooadd de tabela de encaminhamento uma rota predefinida e, em seguida, associar Olá encaminhamento tabela tooyour VNet subnet(s) tooenable forçado túnel em dessas sub-redes.
* Imposição do túnel tem de ser associado a uma VNet com um gateway de VPN baseado na rota. É necessário tooset "site predefinido" entre a rede virtual do Olá em vários locais sites locais toohello ligado. Além disso, Olá no local do dispositivo VPN tem de ser configurado utilizando 0.0.0.0/0 como seletores de tráfego. 
* ExpressRoute imposição do túnel não está configurada através desta mecanismo, mas em vez disso, é ativado por uma rota predefinida através de Olá BGP de ExpressRoute de publicidade sessões de peering. Para obter mais informações, consulte Olá [documentação do ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="configuration-overview"></a>Descrição geral de configuração

Olá, seguindo o procedimento ajuda a criar um grupo de recursos e uma VNet. Em seguida, irá criar um gateway de VPN e configurar a imposição do túnel. Neste procedimento, Olá a rede virtual 'MultiTier VNet' tem três sub-redes: 'Front-end', 'Midtier' e 'Back-end', com quatro em vários locais ligações: 'DefaultSiteHQ' e três ramos.

passos do procedimento de Olá definidas Olá 'DefaultSiteHQ' como ligação de site Olá predefinido para a imposição do túnel e configurar Olá 'Midtier' e 'Back-end' sub-redes toouse imposição do túnel.

## <a name="before-you-begin"></a>Antes de começar

Instale a versão mais recente do Olá do Olá cmdlets do PowerShell do Azure Resource Manager. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre a instalação de cmdlets do PowerShell Olá.

### <a name="toolog-in"></a>toolog no

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>Configurar túnel forçado

1. Crie um grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. Criar uma rede virtual e especificar sub-redes.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Crie Olá gateways de rede local.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Crie Regra de rota e tabela de rota de Olá.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Associe toohello de tabela de rota Olá Midtier e sub-redes de back-end.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Crie Olá Gateway com um site predefinido. Este passo demora alguns toocomplete de tempo, por vezes, 45 minutos ou mais, porque são criar e configurar o gateway de Olá.<br> Olá **- GatewayDefaultSite** é Olá parâmetros do cmdlet que lhe permite Olá forçado encaminhamento toowork de configuração, por isso, demorar cuidado tooconfigure esta definição corretamente. Este parâmetro é disponíveis no PowerShell 1.0 ou posterior.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Estabelece ligações de VPN Olá Site para Site.

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```