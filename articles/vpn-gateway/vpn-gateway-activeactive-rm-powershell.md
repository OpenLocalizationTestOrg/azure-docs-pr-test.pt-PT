---
title: "Configurar as ligações de S2S VPN de ativo-ativo para Gateways de VPN: o Gestor de recursos do Azure: PowerShell | Microsoft Docs"
description: "Este artigo explica como configurar ligações de ativo-ativo com Gateways de VPN do Azure com o Azure Resource Manager e o PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Configurar ligações de S2S VPN de ativo-ativo com Gateways de VPN do Azure

Este artigo explica Olá passos toocreate ativo-ativo em vários locais e ligações VNet a VNet com o modelo de implementação do Resource Manager Olá e PowerShell.

## <a name="about-highly-available-cross-premises-connections"></a>Acerca das ligações em vários locais elevada
tooachieve elevada disponibilidade para conectividade de VNet a VNet e em vários locais, deve implementar vários gateways VPN e estabelecer várias ligações paralelas entre as suas redes e do Azure. Consulte [altamente disponível em vários locais e VNet a VNet conectividade](vpn-gateway-highlyavailable.md) para uma descrição geral da topologia e as opções de conectividade.

Este artigo fornece instruções de Olá tooset segurança de um ativo-ativo em vários locais ligação VPN e ligação de ativo-ativo entre duas redes virtuais:

* [Parte 1 – criar e configurar o gateway de VPN do Azure no modo ativo-ativo](#aagateway)
* [Parte 2 - estabelecer ligações de ativo-ativo em vários locais](#aacrossprem)
* [Parte 3 - estabelecer ligações VNet a VNet de ativo-ativo](#aav2v)
* [Parte 4 - atualizar gateway existente entre ativo-ativo e modo de espera ativo](#aaupdate)

Pode combinar estas toobuild em conjunto uma topologia de rede mais complexa, altamente disponíveis que satisfaça as suas necessidades.

> [!IMPORTANT]
> Tenha em atenção de que modo de ativo-ativo Olá utiliza Olá apenas SKUs os seguintes: 
  * VpnGw1, VpnGw2, VpnGw3
  * HighPerformance (para SKUs legados antigos)
> 
> 

## <a name ="aagateway"></a>Parte 1 – criar e configurar os gateways de VPN de ativo-ativo
Olá, os passos seguintes irá configurar o gateway de VPN do Azure nos modos de ativo-ativo. Olá principais diferenças entre os gateways de ativo-ativo e modo de espera ativo Olá:

* Terá de toocreate configurações de IP do Gateway dois com dois endereços IP públicos
* Precisa de definir o sinalizador de EnableActiveActiveFeature Olá
* SKU de gateway Olá tem de ser VpnGw1, VpnGw2, VpnGw3 ou HighPerformance (legado SKU).

Olá outras propriedades são Olá igual a gateways do Olá não ativo-ativo. 

### <a name="before-you-begin"></a>Antes de começar
* Verifique se tem uma subscrição do Azure. Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Irá precisar de tooinstall Olá Azure Resource Manager PowerShell cmdlets. Consulte [descrição geral do Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre a instalação de cmdlets do PowerShell Olá.

### <a name="step-1---create-and-configure-vnet1"></a>Passo 1 – criar e configurar VNet1
#### <a name="1-declare-your-variables"></a>1. Declarar as variáveis
Para este exercício, vamos começar por declarar as nossas variáveis. exemplo de Olá abaixo declara as variáveis de Olá utilizando valores de Olá para este exercício. Quando configurar para produção de ser valores de Olá tooreplace se com os seus próprios. Pode utilizar estas variáveis se estiver a executar através de Olá passos toobecome familiarizado com este tipo de configuração. Modificar variáveis de Olá e, em seguida, copie e cole a consola do PowerShell.

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Ligar tooyour subscrição e crie um novo grupo de recursos
Certifique-se de que muda tooPowerShell-Olá modo toouse cmdlets do Resource Manager. Para obter mais informações, veja [Utilizar o Windows PowerShell com o Resource Manager](../powershell-azure-resource-manager.md).

Abra a consola do PowerShell e ligue tooyour conta. Utilize Olá toohelp de exemplo, ligar os seguintes:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Criar a TestVNet1
exemplo de Olá abaixo cria uma rede virtual denominada TestVNet1 e três sub-redes, um GatewaySubnet chamado, um front-end e um back-end. Quando estiver a substituir os valores, é importante que dê sempre à sub-rede do gateway o nome específico GatewaySubnet. Se der outro nome, a criação da gateway falhará.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>Passo 2 - Criar gateway de VPN Olá da TestVNet1 com modo ativo-ativo
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Criar os endereços IP públicos Olá e configurações de IP do gateway
Pedido de dois pública IP endereços toobe toohello alocado gateway que será criado para a sua VNet. Também irá definir sub-rede Olá e configurações de IP necessárias.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. Criar gateway de VPN de Olá com a configuração de ativo-ativo
Crie gateway de rede virtual Olá da TestVNet1. Tenha em atenção que existem duas entradas GatewayIpConfig e Olá EnableActiveActiveFeature sinalizador está definido. Criar um gateway pode demorar algum tempo (45 minutos ou mais toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Obter Olá gateway os endereços IP públicos e endereço de IP do elemento BGP Olá
Assim que for criado o gateway de Olá, terá de endereço de IP do elemento BGP Olá tooobtain no Olá Gateway de VPN do Azure. Este endereço é necessário tooconfigure Olá Gateway de VPN do Azure como um elemento de rede BGP para os seus dispositivos VPN no local.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

Utilize os seguintes cmdlets tooshow Olá dois endereços IP públicos alocados para o gateway de VPN e os respetivos endereços de IP do elemento BGP correspondentes para cada instância de gateway de Olá:

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

ordem de Olá dos endereços IP públicos do Olá para instâncias de gateway Olá e Olá endereços de Peering de BGP correspondentes são Olá mesmo. Neste exemplo, o gateway de Olá VM com o IP público de 40.112.190.5 utilizará 10.12.255.4 como o respetivo endereço de Peering de BGP e gateway Olá com 138.91.156.129 utilizará 10.12.255.5. Esta informação é necessária quando configura um local em dispositivos VPN a ligar o gateway de ativo-ativo toohello. gateway de Olá é mostrado no diagrama de Olá abaixo com todos os endereços:

![gateway de ativo-ativo](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

Assim que for criado o gateway de Olá, pode utilizar esta ligação de VNet a VNet ou gateway tooestablish ativo-ativo em vários locais. Olá secções a seguir irá guiá-Olá passos toocomplete Olá exercício.

## <a name ="aacrossprem"></a>Parte 2 - estabelecer uma ligação de ativo-ativo em vários locais
tooestablish uma ligação entre locais, terá de toocreate toorepresent um Gateway de rede Local o dispositivo VPN no local e um ligação tooconnect Olá VPN gateway do Azure com o gateway de rede local Olá. Neste exemplo, o gateway de VPN do Azure Olá está no modo de ativo-ativo. Como resultado, mesmo apesar de não existir apenas um no local o dispositivo VPN (gateway de rede local) e de recursos de uma ligação, ambas as instâncias de gateway de VPN do Azure irão estabelecer túneis S2S VPN com o dispositivo do Olá no local.

Antes de continuar, certifique-se de que concluiu [parte 1](#aagateway) neste exercício.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Passo 1 – criar e configurar o gateway de rede local Olá
#### <a name="1-declare-your-variables"></a>1. Declarar as variáveis
Neste exercício irá continuar a configuração de Olá toobuild mostrada no diagrama de Olá. Ser tooreplace se valores Olá com Olá aqueles que pretende que toouse para a sua configuração.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

Alguns aspetos toonote sobre os parâmetros de gateway de rede local Olá:

* gateway de rede local Olá pode ter Olá mesmo ou outra localização e recursos de grupo como Olá gateway de VPN. Este exemplo mostra-los em grupos de recursos diferente, mas Olá mesma localização do Azure.
* Se houver apenas um dispositivo VPN no local, conforme mostrado acima, a ligação de ativo-ativo Olá pode trabalhar com ou sem protocolo BGP. Este exemplo utiliza o BGP para ligação do Olá em vários locais.
* Se o BGP está ativado, o prefixo de Olá precisa toodeclare para gateway de rede local Olá é endereço do anfitrião Olá do seu endereço de IP do elemento BGP no seu dispositivo VPN. Neste caso, é um /32 prefixo do nome de "10.52.255.253/32".
* Como um lembrete, tem de utilizar ASNs diferentes de BGP entre as redes no local e a VNet do Azure. Se são hello iguais, é necessário toochange o ASN de VNet se o dispositivo VPN no local utiliza já Olá ASN toopeer com outros vizinhos BGP.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Criar gateway de rede local Olá para Site5
Antes de continuar, certifique-se de que estão ligado ainda tooSubscription 1. Crie grupo de recursos de Olá se ainda não é criado.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Passo 2 - ligar o gateway de VNet Olá e gateway de rede local
#### <a name="1-get-hello-two-gateways"></a>1. Obter Olá dois gateways

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Criar a ligação de tooSite5 Olá TestVNet1
Neste passo, vai criar Olá ligação da TestVNet1 tooSite5_1 com "EnableBGP" definido demasiado$ True.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. Parâmetros VPN e BGP para o dispositivo VPN no local
exemplo de Olá abaixo apresenta uma lista de parâmetros de Olá que vai introduzir no Olá secção de configuração de BGP no dispositivo VPN no local para este exercício:

    - Site5 ASN: 65050
    - IP do BGP Site5: 10.52.255.253
    - Prefixos tooannounce: (por exemplo) 10.51.0.0/16 e 10.52.0.0/16
    - ASN de VNet do Azure: 65010
    - IP de BGP do Azure VNet 1: 10.12.255.4 para too40.112.190.5 de túnel
    - IP de BGP do Azure VNet 2: 10.12.255.5 para too138.91.156.129 de túnel
    - Rotas estáticas: destino 10.12.255.4/32, nexthop Olá VPN túnel interface too40.112.190.5 destino 10.12.255.5/32, too138.91.156.129 de interface de túnel do nexthop Olá VPN
    - eBGP Multihop: Certifique-se de opção de "multihop" Olá para eBGP está ativado no seu dispositivo, se for necessário

deve ser estabelecida a ligação de Olá após alguns minutos e a sessão de peering de BGP de Olá serão iniciado depois de é estabelecido Olá ligação IPsec. Neste exemplo, até ao momento configurou o dispositivo VPN no local apenas uma, resultando no diagrama de Olá mostrado abaixo:

![ativo-ativo-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>Passo 3 – ligar os dois locais VPN dispositivos toohello ativo-ativo do VPN gateway
Se tiver dois dispositivos VPN no Olá mesmo local rede, pode conseguir redundância dupla por ligação Olá VPN do Azure toohello segundo VPN dispositivo de gateway.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Criar gateway de rede local segundo Olá para Site5
Tenha em atenção que o endereço IP do gateway Olá, prefixo de endereço e endereço de peering de BGP de gateway de rede local segundo Olá não podem sobrepor com gateway rede local anterior Olá para Olá mesmo rede no local.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Ligar o gateway de VNet Olá e gateway de rede local segundo Olá
Criar ligação Olá da TestVNet1 tooSite5_2 com "EnableBGP" definido demasiado$ True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. Parâmetros VPN e BGP para o segundo dispositivo VPN no local
Da mesma forma, abaixo apresenta uma lista de parâmetros de Olá irá introduzir no dispositivo VPN segundo Olá:

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Assim que são estabelecida a ligação de Olá (túneis), terá duplos dispositivos VPN redundantes e túneis ligar a rede no local e o Azure:

![Dual-redundância-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>Parte 3 - estabelecer uma ligação de VNet a VNet ativo-ativo
Esta secção cria uma ligação de VNet a VNet ativo-ativo com o BGP. 

instruções de Olá abaixo continuam dos passos anteriores Olá listados acima. Tem de concluir [parte 1](#aagateway) toocreate e configurar a TestVNet1 e Olá Gateway de VPN com o BGP. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Passo 1 – criar gateway VPN TestVNet2 e Olá
É importante toomake certificar-se de que espaço de endereços IP Olá de Olá nova rede virtual, TestVNet2, não se sobreponha a nenhum dos intervalos sua VNet.

Neste exemplo, redes virtuais Olá pertencem toohello mesma subscrição. Pode configurar ligações VNet a VNet entre subscrições diferentes; Consulte demasiado[configurar uma ligação VNet a VNet](vpn-gateway-vnet-vnet-rm-ps.md) toolearn mais detalhes. Certifique-se de adicionar Olá "-EnableBgp $True" quando criar Olá tooenable ligações BGP.

#### <a name="1-declare-your-variables"></a>1. Declarar as variáveis
Ser tooreplace se valores Olá com Olá aqueles que pretende que toouse para a sua configuração.

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. Criar TestVNet2 no novo grupo de recursos Olá

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. Criar gateway de VPN do Olá ativo-ativo para TestVNet2
Pedido de dois pública IP endereços toobe toohello alocado gateway que será criado para a sua VNet. Também irá definir sub-rede Olá e configurações de IP necessárias.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

Crie gateway de VPN Olá com Olá como número e Olá sinalizador "EnableActiveActiveFeature". Tenha em atenção que tem de substituir a predefinição de Olá ASN em gateways de VPN do Azure. Olá ASNs para Olá ligados a VNets tem de ser diferentes tooenable BGP e o encaminhamento de trânsito.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>Passo 2 – ligar os gateways de TestVNet1 e TestVNet2 Olá
Neste exemplo, ambas as gateways estão na Olá mesma subscrição. Pode concluir este passo na Olá mesma sessão do PowerShell.

#### <a name="1-get-both-gateways"></a>1. Obter ambas as gateways
Certifique-se de que iniciar sessão e ligar tooSubscription 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Criar ambas as ligações
Neste passo, irá criar a ligação Olá da TestVNet1 tooTestVNet2 e ligação Olá de TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Ser tooenable se BGP para ambas as ligações.
> 
> 

Depois de concluir estes passos, será possível estabelecer ligação Olá dentro de alguns minutos e sessões de peering de BGP de Olá serão cópias de segurança depois de concluída a ligação de Olá VNet a VNet com redundância dupla:

![ativo-ativo-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>Parte 4 - atualizar gateway existente entre ativo-ativo e modo de espera ativo
última seção do Olá descrevem como configurar um gateway de VPN do Azure existente do modo de tooactive-Active Directory de modo de espera ativo, ou vice versa.

> [!NOTE]
> Esta secção inclui os passos de Olá tooresize um SKU legado (antigo SKU) de um gateway VPN já criou de tooHighPerformance padrão. Estes passos não atualizar um tooone SKU legado antigo de Olá SKUs de novo.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>Configurar um gateway do gateway de modo de espera ativo tooactive-Active Directory
#### <a name="1-gateway-parameters"></a>1. Parâmetros de gateway
Olá seguinte o exemplo converte um gateway de modo de espera ativo de um gateway de ativo-ativo. É necessário toocreate outro endereço IP público, em seguida, adicionar uma segunda configuração de IP do Gateway. Abaixo mostra hello utilizados parâmetros:

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Criar endereço IP público do Olá, em seguida, adicionar configuração de IP do gateway segundo Olá

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. Ativar o gateway de Olá de modo e de atualização de ativo-ativo
Tem de definir o objeto do gateway Olá na atualização do PowerShell tootrigger Olá real. Olá SKU do gateway de rede virtual Olá tem também de ser alterada tooHighPerformance (redimensionado), uma vez que foi criada anteriormente como padrão.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

Esta atualização pode demorar too45 de 30 minutos.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>Configurar um gateway de tooactive-modo de espera ativo-ativo gateway
#### <a name="1-gateway-parameters"></a>1. Parâmetros de gateway
Utilize Olá mesmo parâmetros acima, como obter o nome de Olá Olá da configuração de IP que pretende tooremove.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Remova a configuração de IP do gateway Olá e desativar o modo de ativo-ativo Olá
Da mesma forma, é necessário definir o objeto do gateway Olá na atualização do PowerShell tootrigger Olá real.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

Esta atualização pode demorar até too30 demasiado 45 minutos.

## <a name="next-steps"></a>Passos seguintes
Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais. Veja [Criar uma Máquina Virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter os passos.
