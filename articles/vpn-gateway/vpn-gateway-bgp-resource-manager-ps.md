---
title: 'Configurar o BGP nos Gateways de VPN do Azure: o Gestor de recursos: PowerShell | Microsoft Docs'
description: Este artigo explica como configurar o BGP com Gateways de VPN do Azure com o Azure Resource Manager e o PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: b00a3fe7ba4b12c2e9c486188c292cd6fafb60a3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a>Como configurar o BGP nos Gateways de VPN do Azure com o PowerShell
Este artigo explica os passos para ativar o BGP numa ligação de VPN de Site a Site (S2S) em vários locais e uma ligação VNet a VNet com o modelo de implementação do Resource Manager e o PowerShell.

## <a name="about-bgp"></a>Sobre o BGP
O BGP é o protocolo de encaminhamento padrão utilizado normalmente na Internet para trocar informações de encaminhamento e acessibilidade entre duas ou mais redes. BGP permite que os Gateways de VPN do Azure e os dispositivos VPN no local, chamados elementos BGP ou vizinhos, troquem "rotas" que informarão ambos os gateways da disponibilidade e acessibilidade para esses prefixos percorrerem os gateways ou routers envolvidos. O BGP também pode permitir o encaminhamento de tráfego entre várias redes ao propagar rotas para todos os outros elementos de rede BGP, que um gateway BGP aprende de um elemento de rede BGP.

Consulte [descrição geral do BGP com Gateways de VPN do Azure](vpn-gateway-bgp-overview.md) para obter mais debate sobre vantagens do BGP e compreender os requisitos técnicos e as considerações de utilizar o BGP.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Introdução ao BGP nos gateways de VPN do Azure

Este artigo explica os passos para efetuar as seguintes tarefas:

* [Parte 1 - ativar o BGP no gateway de VPN do Azure](#enablebgp)
* [Parte 2 - estabelecer uma ligação em vários locais com o BGP](#crossprembgp)
* [Parte 3 - estabelecer uma ligação VNet a VNet com o BGP](#v2vbgp)

Cada parte das instruções constitui um bloco modular básico para ativar o BGP na sua conectividade de rede. Se concluir todos os três partes, criar a topologia conforme mostrado no diagrama seguinte:

![Topologia BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

Pode combinar partes em conjunto para criar uma rede de trânsito mais complexas, multi-HOP, que responde às suas necessidades.

## <a name ="enablebgp"></a>Parte 1 - configurar o BGP no Gateway de VPN do Azure
Os passos de configuração configurar os parâmetros BGP do gateway de VPN do Azure, conforme mostrado no diagrama seguinte:

![Gateway do BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Antes de começar
* Verifique se tem uma subscrição do Azure. Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Instale os cmdlets do PowerShell do Azure Resource Manager. Para obter mais informações sobre como instalar os cmdlets do PowerShell, veja [How to install and configure Azure PowerShell (Como instalar e configurar o Azure PowerShell)](/powershell/azure/overview) . 

### <a name="step-1---create-and-configure-vnet1"></a>Passo 1 – criar e configurar VNet1
#### <a name="1-declare-your-variables"></a>1. Declarar as variáveis
Para este exercício, vamos começar por declarar as nossas variáveis. O exemplo seguinte declara as variáveis com os valores para este exercício. Verifique se substitui os valores pelos seus quando configurar para produção. Pode utilizar estas variáveis se estiver a executar os passos para se familiarizar com este tipo de configuração. Modifique as variáveis e, em seguida, copie e cole a consola do PowerShell.

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a>2. Ligar à sua subscrição e crie um novo grupo de recursos
Para utilizar os cmdlets Resource Manager, certifique-se de que muda para o modo do PowerShell. Para obter mais informações, veja [Utilizar o Windows PowerShell com o Resource Manager](../powershell-azure-resource-manager.md).

Abra a consola do PowerShell e ligue-se à sua conta. Utilize o seguinte exemplo para o ajudar na ligação:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Criar a TestVNet1
O exemplo seguinte cria uma rede virtual denominada TestVNet1 e três sub-redes, um GatewaySubnet chamado, um front-end e um back-end. Quando estiver a substituir os valores, é importante que dê sempre à sub-rede do gateway o nome específico GatewaySubnet. Se der outro nome, a criação da gateway falha.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>Passo 2 - criar o VPN Gateway da TestVNet1 com parâmetros BGP
#### <a name="1-create-the-ip-and-subnet-configurations"></a>1. Criar as configurações de IP e a sub-rede
Peça para que seja atribuído um endereço IP público ao gateway que vai criar para a VNet. Também irá definir a sub-rede necessário e as configurações de IP.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a>2. Criar o gateway VPN com o número AS
Crie o gateway de rede virtual para TestVNet1. BGP requer um gateway de VPN baseado na rota bem como o parâmetro de adição, - Asn, para definir o ASN (número AS) da TestVNet1. Se não definir o parâmetro ASN, ASN de 65515 está atribuído. A criação de um gateway pode demorar algum tempo (30 minutos ou mais).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a>3. Obter o endereço IP do elemento de BGP de Azure
Assim que for criado o gateway, terá de obter o endereço IP do elemento BGP no Gateway de VPN do Azure. Este endereço é necessária para configurar o Gateway de VPN do Azure como um elemento de rede BGP para os seus dispositivos VPN no local.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

O último comando mostra as configurações correspondentes do BGP no Gateway de VPN do Azure; Por exemplo:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Assim que for criado o gateway, pode utilizar este gateway para estabelecer a ligação em vários locais ou a ligação VNet a VNet com o BGP. As secções seguintes percorrer os passos para concluir o exercício.

## <a name ="crossprembbgp"></a>Parte 2 - estabelecer uma ligação em vários locais com o BGP

Para estabelecer uma ligação entre locais, terá de criar um Gateway de rede Local para representar o dispositivo VPN no local e uma ligação para ligar o gateway VPN com o gateway de rede local. Enquanto existem artigos que explica como estes passos, este artigo contém as propriedades adicionais necessárias para especificar os parâmetros de configuração de BGP.

![BGP para vários locais](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Antes de continuar, certifique-se de que concluiu [parte 1](#enablebgp) neste exercício.

### <a name="step-1---create-and-configure-the-local-network-gateway"></a>Passo 1 – criar e configurar o gateway de rede local

#### <a name="1-declare-your-variables"></a>1. Declarar as variáveis

Neste exercício continua a criar a configuração de mostrado no diagrama. Confirme que substitui os valores pelos que pretende utilizar para a configuração.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Algumas coisas a salientar sobre os parâmetros de gateway de rede local:

* O gateway de rede local pode estar no mesma ou outra localização e grupo de recursos como o gateway VPN. Este exemplo mostra-los em grupos de recursos diferentes em diferentes localizações.
* O prefixo mínimo que tem de indicar para o gateway de rede local é o endereço do anfitrião do seu endereço de IP do elemento BGP no seu dispositivo VPN. Neste caso, é um /32 prefixo do nome de "10.52.255.254/32".
* Como um lembrete, tem de utilizar ASNs diferentes de BGP entre as redes no local e a VNet do Azure. Se estes são os mesmos, terá de alterar o ASN de VNet, se o dispositivo VPN no local que já utiliza o ASN para peering com outros vizinhos BGP.

Antes de continuar, verifique se ainda está ligado à Subscrição 1.

#### <a name="2-create-the-local-network-gateway-for-site5"></a>2. Criar o gateway de rede local para Site5

Lembre-se de que pretende criar o grupo de recursos, caso não é criado, antes de criar o gateway de rede local. Tenha em atenção os dois parâmetros adicionais para o gateway de rede local: Asn e BgpPeerAddress.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a>Passo 2 - ligar o gateway de VNet e o gateway de rede local

#### <a name="1-get-the-two-gateways"></a>1. Obter os dois gateways

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a>2. Criar a ligação da TestVNet1 para Site5

Neste passo, criará a ligação da TestVNet1 para Site5. Tem de especificar "-EnableBGP $True" para ativar o BGP para esta ligação. Tal como abordado anteriormente, é possível ter ligações BGP e não BGP para o mesmo Gateway de VPN do Azure. A menos que o BGP está ativado na propriedade de ligação, Azure não permitirão o BGP para esta ligação, apesar de parâmetros BGP já estão configurados em ambas as gateways.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

O exemplo seguinte lista os parâmetros que introduzir na secção de configuração de BGP no dispositivo VPN no local para este exercício:

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

A ligação for estabelecida após alguns minutos e, a sessão de peering de BGP inicia uma vez IPsec ligação for estabelecida.

## <a name ="v2vbgp"></a>Parte 3 - estabelecer uma ligação VNet a VNet com o BGP

Esta secção adiciona uma ligação VNet a VNet com o BGP, conforme mostrado no diagrama seguinte:

![BGP para VNet a VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

As seguintes instruções continuam dos passos anteriores. Tem de concluir [parte I](#enablebgp) para criar e configurar a TestVNet1 e o Gateway de VPN com o BGP. 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a>Passo 1 – criar TestVNet2 e o gateway VPN

É importante certificar-se de que o espaço de endereços IP da rede virtual novo, TestVNet2, não se sobreponha a nenhum dos intervalos sua VNet.

Neste exemplo, as redes virtuais pertencem à mesma subscrição. Pode configurar ligações VNet a VNet entre subscrições diferentes. Para obter mais informações, consulte [configurar uma ligação VNet a VNet](vpn-gateway-vnet-vnet-rm-ps.md). Certifique-se de que adiciona o "-EnableBgp $True" quando criar as ligações para ativar o BGP.

#### <a name="1-declare-your-variables"></a>1. Declarar as variáveis

Confirme que substitui os valores pelos que pretende utilizar para a configuração.

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a>2. Criar TestVNet2 no novo grupo de recursos

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Criar o gateway VPN para TestVNet2 com parâmetros BGP

Solicitar um endereço IP público para ser atribuído ao gateway será criado para a VNet e defina a sub-rede necessário e as configurações de IP.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Crie o gateway VPN com o número AS. Tem de substituir a predefinição ASN em gateways de VPN do Azure. Os ASNs para as VNets ligados têm de ser diferentes para ativar o BGP e o encaminhamento de trânsito.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a>Passo 2 – ligar os gateways TestVNet1 e TestVNet2

Neste exemplo, ambos os gateways estão na mesma subscrição. Pode concluir este passo na mesma sessão do PowerShell.

#### <a name="1-get-both-gateways"></a>1. Obter ambas as gateways

Confirme que inicia sessão e se liga à Subscrição 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Criar ambas as ligações

Neste passo, vai criar a ligação da TestVNet1 para TestVNet2 e a ligação de TestVNet2 para a TestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> É necessário ativar o BGP para ambas as ligações.
> 
> 

Depois de concluir estes passos, é estabelecida a ligação após alguns minutos. A sessão de peering de BGP está ativo depois da ligação VNet a VNet está concluída.

Se concluiu todos os três partes neste exercício, tem de estabelecer a topologia de rede seguinte:

![BGP para VNet a VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Passos seguintes

Assim que a ligação estiver concluída, pode adicionar máquinas virtuais às redes virtuais. Veja [Criar uma Máquina Virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter os passos.