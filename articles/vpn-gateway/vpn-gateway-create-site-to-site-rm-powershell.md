---
title: 'Ligar o seu tooan de rede no local rede virtual do Azure: VPN Site a Site: PowerShell | Microsoft Docs'
description: "Uma ligação de IPsec do seu local de rede tooan rede virtual do Azure através de toocreate de passos Olá Internet pública. Estes passos ajudam-no a criar uma ligação de Gateway de Rede de VPNs em vários sites com o PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>Criar uma VNet com uma ligação de Rede de VPNs com o PowerShell

Este artigo mostra como toouse PowerShell ligação de gateway VPN toocreate um Site para Site do seu local de rede toohello VNet. passos de Olá neste artigo aplicam-se o modelo de implementação do Resource Manager toohello. Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Portal clássico (clássico)](vpn-gateway-site-to-site-create.md)
> 
>


Uma ligação de gateway VPN de Site a Site é utilizado tooconnect tooan rede virtual do Azure de rede no local através de um túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Este tipo de ligação requer uma VPN dispositivos localizado no local que tenha um tooit de atribuída de endereço IP público com acesso exterior. Para obter mais informações sobre o gateways de VPN, veja [About VPN gateway (Acerca do gateway de VPN)](vpn-gateway-about-vpngateways.md).

![Diagrama da ligação de Gateway de Rede de VPNs em vários sites](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>Antes de começar

Certifique-se de que cumpriu Olá os seguintes critérios antes de iniciar a configuração:

* Certifique-se de um dispositivo VPN compatível e alguém que seja capaz de tooconfigure-lo. Para obter mais informações sobre os dispositivos VPN compatíveis e a configuração do dispositivo, consulte [About VPN Devices (Acerca dos Dispositivos VPN)](vpn-gateway-about-vpn-devices.md).
* Verifique se tem um endereço IP IPv4 público com acesso exterior para o seu dispositivo VPN. Este endereço IP não pode estar localizado atrás de um NAT.
* Se não estiver familiarizado com intervalos de endereços IP Olá localizados na configuração de rede no local, tem de toocoordinate com alguém que consiga fornecer esses detalhes. Ao criar esta configuração, tem de especificar que o Azure irá encaminhar localização no local de tooyour dos prefixos de intervalo de endereços para IP Olá. Nenhuma das sub-redes Olá da sua rede no local pode através de lap com sub-redes da rede virtual Olá que pretende que sejam tooconnect para.
* Instale a versão mais recente do Olá do Olá cmdlets do PowerShell do Azure Resource Manager. Cmdlets do PowerShell são frequentemente atualizados e, normalmente, terá de tooupdate a PowerShell cmdlets tooget Olá mais recente funcionalidade. Se não atualizar os seus cmdlets do PowerShell, os valores de Olá especificados poderão falhar. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como transferir e instalar os cmdlets do PowerShell.

### <a name="example"></a>Valores de exemplo

Exemplos de Olá neste artigo utilizam Olá os seguintes valores. Pode utilizar estes toocreate de valores num ambiente de teste, ou consulte toothem toobetter compreender exemplos Olá neste artigo.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Ligar tooyour subscrição

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. Criar uma rede virtual e uma sub-rede de gateway

Se ainda não tiver uma rede virtual, crie uma. Ao criar uma rede virtual, certifique-se de que os espaços de endereços Olá que especificou não se sobrepõem a qualquer um dos espaços de endereços de Olá que tem na sua rede no local.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate uma rede virtual e uma sub-rede de gateway

Este exemplo cria uma rede virtual e uma sub-rede de gateway. Se já tiver uma rede virtual que necessitam de tooadd uma sub-rede de gateway para ver [tooadd uma gateway sub-rede tooa rede virtual que já criou](#gatewaysubnet).

Criar um grupo de recursos:

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

Criar a sua rede virtual.

1. Definir variáveis de Olá.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Crie Olá VNet.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>tooadd uma rede virtual do gateway sub-rede tooa que já criou

1. Definir variáveis de Olá.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Crie a sub-rede do gateway Olá.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Definir a configuração de Olá.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Criar gateway de rede local Olá

gateway de rede local Olá refere-se normalmente localização do tooyour no local. Dê site Olá um nome pelo qual Azure pode consulte tooit, em seguida, especifique o endereço IP Olá de toowhich de dispositivo VPN do Olá no local, irá criar uma ligação. Também especificar prefixos de endereços IP Olá serão encaminhados através de um dispositivo VPN do Olá VPN gateway toohello. especificar prefixos de endereços de Olá são prefixos Olá localizados na sua rede no local. Se alterar a sua rede no local, pode facilmente atualizar prefixos Olá.

Utilize Olá os seguintes valores:

* Olá *GatewayIPAddress* é Olá endereço IP do seu dispositivo VPN no local. O dispositivo VPN não pode estar localizado atrás de um NAT.
* Olá *AddressPrefix* está no local espaço de endereços.

tooadd um gateway de rede local com um prefixo de endereço único:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

tooadd um gateway de rede local com vários prefixos de endereço:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

toomodify os prefixos de endereço IP para o gateway de rede local:<br>
Às vezes, os prefixos de gateway da sua rede local mudam. passos de Olá tomar toomodify seu endereço IP prefixos dependem se tiver criado uma ligação de gateway VPN. Consulte Olá [prefixos de endereços IP modificar para um gateway de rede local](#modify) secção deste artigo.

## <a name="PublicIP"></a>4. Solicitar um endereço IP Público

Um gateway de VPN deve ter um endereço IP público. Primeiro pedido de recurso de endereço IP de Olá e, em seguida, consulte tooit ao criar o gateway de rede virtual. Olá está atribuído endereço IP dinamicamente recursos toohello quando Olá gateway de VPN criado. O Gateway de VPN, atualmente, apenas suporta a alocação de endereços IP públicos *dinâmicos*. Não é possível pedir uma atribuição de endereço IP Público Estático. No entanto, isto não significa que o endereço IP Olá alterado depois de lhe ser atribuído tooyour gateway de VPN. tempo apenas Olá alterações do endereço de IP público de Olá quando é Olá gateway é eliminado e recriado. Não é alterado ao redimensionar, repor ou ao realizar qualquer outra manutenção/atualização interna do gateway de VPN.

Solicitar um endereço de IP público que será atribuído tooyour de rede virtual gateway de VPN.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Criar a configuração de endereçamento de IP do gateway Olá

configuração do gateway de Olá define uma sub-rede de Olá e Olá toouse de endereço IP público. Utilize a configuração do gateway de Olá toocreate de exemplo a seguir:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Criar gateway de VPN Olá

Crie gateway de VPN de rede virtual Olá. Criar um gateway VPN pode demorar até too45 minutos ou mais toocomplete.

Utilize Olá os seguintes valores:

* Olá *- GatewayType* para uma Site a Site é configuração *Vpn*. tipo de gateway Olá é sempre configuração toohello específico que estiver a implementar. Por exemplo, outras configurações de gateway poderão exigir o ExpressRoute -GatewayType.
* Olá *- VpnType* pode ser *RouteBased* (referido tooas um Gateway dinâmico em alguma documentação), ou *PolicyBased* (referido tooas Gateway estático em alguma documentação ). Para obter mais informações sobre os tipos de gateways de VPN, veja [Acerca dos Gateways de VPN](vpn-gateway-about-vpngateways.md).
* Selecione Olá SKU de Gateway que pretende que o toouse. Existem limitações de configuração para determinados SKUs. Para obter mais informações, veja [SKUs de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku). Se obtiver um erro ao criar o gateway de VPN Olá sobre Olá - GatewaySku, certifique-se de que instalou a versão mais recente do Olá Olá de cmdlets do PowerShell.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. Configurar o dispositivo VPN

Rede do ligações site a Site tooan no local requer um dispositivo VPN. Neste passo, configure o seu dispositivo VPN. Quando configurar o seu dispositivo VPN, terá de seguinte Olá:

- Uma chave partilhada. Isto é Olá mesmo partilhado chave que especificar ao criar a ligação de VPN de Site para Site. Nos nossos exemplos, iremos utilizar uma chave partilhada básica. Recomendamos que geram um toouse chave mais complexa.
- Olá endereço IP público do gateway da rede virtual. Pode ver o endereço IP público Olá utilizando Olá portal do Azure, PowerShell ou a CLI. Olá toofind endereço IP público do seu gateway de rede virtual com o PowerShell, o seguinte exemplo de Olá de utilização:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Criar a ligação de VPN Olá

Em seguida, crie a ligação de VPN de Site para Site Olá entre o gateway de rede virtual e o seu dispositivo VPN. Ser se valores de Olá tooreplace com os seus próprios. chave partilhada Olá tem de corresponder ao valor de Olá utilizado para a configuração do dispositivo VPN. Tenha em atenção que Olá '-ConnectionType' para o Site a Site é *IPsec*.

1. Definir variáveis de Olá.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Crie ligação Olá.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

Após um curto período ao hello será estabelecida ligação.

## <a name="toverify"></a>9. Certifique-se a ligação de VPN Olá

Existem algumas formas diferentes tooverify a ligação VPN.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa máquina

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>Modificar os prefixos de endereços IP de um gateway de rede local

Se alterar prefixos de endereços IP Olá que pretende que sejam encaminhados localização do tooyour no local, pode modificar o gateway de rede local Olá. São fornecidos dois conjuntos de instruções. instruções de Olá que escolher dependem se já tiver criado a ligação de gateway.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>Modificar o endereço IP do gateway Olá para um gateway de rede local

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Passos seguintes

*  Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais. Para obter mais informações, veja [Máquinas Virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Para informações sobre o BGP, consulte Olá [descrição geral do BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
