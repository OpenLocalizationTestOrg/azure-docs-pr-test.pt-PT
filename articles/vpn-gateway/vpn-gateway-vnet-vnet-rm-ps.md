---
title: 'Ligar um tooanother de rede virtual do Azure VNet: PowerShell | Microsoft Docs'
description: "Este artigo explica como ligar redes virtuais entre si através do Azure Resource Manager e do PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>Configurar uma ligação de gateway de VPN de VNet a VNet com o PowerShell

Este artigo mostra como toocreate uma ligação de gateway VPN entre redes virtuais. Olá redes virtuais podem estar em Olá regiões idêntica ou diferentes e de Olá mesmo ou subscrições diferentes. Quando ao ligar VNets de diferentes subscrições, subscrições Olá não é necessário toobe associado Olá mesmo inquilino do Active Directory. 

passos de Olá neste artigo aplicam-se modelo de implementação do Resource Manager toohello e utilizam o PowerShell. Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI do Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Ligue diferentes modelos de implementação - portal do Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Ligue diferentes modelos de implementação - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Ligar a rede virtual tooanother rede virtual (VNet a VNet) é semelhante tooconnecting uma localização de site do VNet tooan no local. Ambos os tipos de conetividade utilizam um tooprovide de gateway VPN um túnel seguro através de IPsec/IKE. Se as suas VNets estiverem na Olá mesma região, poderá ser útil tooconsider ligá-las a utilização de VNet Peering. O VNet peering não utiliza um gateway de VPN. Para obter mais informações, veja [VNet peering](../virtual-network/virtual-network-peering-overview.md).

A comunicação VNet a VNet pode ser combinada com configurações multilocal. Isto permite-lhe estabelecer topologias de rede que combinam uma conectividade entre instalações com conectividade de rede intervirtual, como mostrado na Olá diagrama a seguir:

![Acerca das ligações](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>Por que motivo ligar redes virtuais?

Poderá pretender redes virtuais tooconnect para Olá seguintes motivos:

* **Geopresença e georredundância entre várias regiões**

  * Pode configurar a sua própria georreplicação ou sincronização com uma conetividade segura sem passar por pontos finais com acesso à Internet.
  * Com o Gestor de Tráfego e o Balanceador de Carga do Azure, pode configurar uma carga de trabalho de elevada disponibilidade com georredundância em várias regiões do Azure. Um exemplo importante consiste tooset cópias de segurança SQL Always On com grupos de disponibilidade propagando-se em várias regiões do Azure.
* **Aplicações multicamadas regionais com isolamento ou limites administrativos**

  * Olá da mesma região, pode configurar aplicações de várias camadas com várias redes virtuais ligadas em conjunto devido tooisolation ou a requisitos administrativos.

Para obter mais informações sobre ligações VNet a VNet, consulte Olá [FAQ de VNet a VNet](#faq) no fim de Olá deste artigo.

## <a name="which-set-of-steps-should-i-use"></a>Que conjunto de passos devo utilizar?

Neste artigo, verá dois conjuntos de passos diferentes. Um conjunto de passos para [Olá de VNets que residem na mesma subscrição](#samesub)e outra para [VNets que residem em subscrições diferentes](#difsub). Olá principal diferença entre conjuntos de Olá é se pode criar e configurar todos os gateway de rede e recursos virtuais no Olá mesma sessão do PowerShell.

Olá passos neste artigo utilizam as variáveis que são declaradas no início de Olá de cada secção. Se já estiver a trabalhar com as VNets existentes, modifique Olá variáveis tooreflect Olá as definições no seu próprio ambiente. Se pretender a resolução de nomes para as suas redes virtuais, veja [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Resolução de nomes).

## <a name="samesub"></a>Como tooconnect VNets que estão em Olá mesma subscrição

![Diagrama v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>Antes de começar

Antes de começar, terá de versão mais recente de Olá tooinstall Olá do Azure Resource Manager de cmdlets do PowerShell, pelo menos 4.0 ou posteriores. Para obter mais informações sobre a instalação de cmdlets do PowerShell Olá, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

### <a name="Step1"></a>Passo 1 - Planear os intervalos de endereços IP

Olá os passos seguintes, vamos criar duas redes virtuais juntamente com as respetivas sub-redes de gateway e configurações. Em seguida, criamos uma ligação VPN entre Olá duas VNets. É importante tooplan intervalos de endereços IP Olá para a sua configuração de rede. Nota: precisa confirmar que nenhum dos intervalos de VNet ou intervalos de rede local se sobrepõe de modo algum. Nestes exemplos, não incluímos um servidor DNS. Se pretender a resolução de nomes para as suas redes virtuais, veja [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Resolução de nomes).

Podemos utilizar Olá valores nos exemplos de Olá os seguintes:

**Valores da TestVNet1:**

* Nome da VNet: TestVNet1
* Grupo de Recursos: TestRG1
* Localização: EUA Leste
* TestVNet1: 10.11.0.0/16 e 10.12.0.0/16
* Front-End: 10.11.0.0/24
* Back-End: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* IP Público: VNet1GWIP
* VPNType: RouteBased
* Ligação (1 a 4): VNet1toVNet4
* Ligação (1 a 5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Valores da TestVNet4:**

* Nome da VNet: TestVNet4
* TestVNet2: 10.41.0.0/16 e 10.42.0.0/16
* Front-End: 10.41.0.0/24
* Back-End: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Grupo de Recursos: TestRG4
* Localização: EUA Oeste
* GatewayName: VNet4GW
* IP Público: VNet4GWIP
* VPNType: RouteBased
* Ligação: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Step2"></a>Passo 2 - Criar e configurar a TestVNet1

1. Declarar as variáveis. Neste exemplo declara as variáveis de Olá utilizando valores de Olá para este exercício. Na maioria dos casos, deve substituir os valores de Olá com os seus próprios. No entanto, pode utilizar estas variáveis se estiver a executar através de Olá passos toobecome familiarizado com este tipo de configuração. Modificar variáveis de Olá, se necessário, em seguida, copie e cole-os para a consola do PowerShell.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
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
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Ligar a tooyour conta. Utilize Olá toohelp de exemplo, ligar os seguintes:

  ```powershell
  Login-AzureRmAccount
  ```

  Verifique Olá subscrições para a conta de Olá.

  ```powershell
  Get-AzureRmSubscription
  ```

  Especifique que pretende que o toouse de subscrição de Olá.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. Crie um novo grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. Crie Olá configurações de sub-rede da TestVNet1. Este exemplo cria uma rede virtual com o nome TestVNet1 e três sub-redes, uma chamada GatewaySubnet, outra FrontEnd e a última BackEnd. Quando estiver a substituir os valores, é importante que dê sempre à sub-rede do gateway o nome específico GatewaySubnet. Se der outro nome, a criação da gateway falha.

  Olá exemplo seguinte utiliza variáveis de Olá que configurou anteriormente. Neste exemplo, a sub-rede do gateway Olá é utilizar/27. Embora seja possível toocreate uma sub-rede do gateway tão pequena como/29, recomendamos que crie uma sub-rede maior que inclua endereços mais ao selecionar, pelo menos, / 28 ou /27. Isto permitirá para suficiente endereços tooaccommodate possíveis configurações adicionais que poderá ser útil no Olá futuras.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. Criar a TestVNet1.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. Pedir um público IP endereço toobe toohello alocado gateway que será criado para a sua VNet. Repare que Olá AllocationMethod é dinâmico. Não é possível especificar o endereço IP Olá que pretende que o toouse. É gateway tooyour alocada dinamicamente. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Crie a configuração do gateway Olá. configuração do gateway de Olá define uma sub-rede de Olá e Olá toouse de endereço IP público. Utilize toocreate de exemplo de Olá a configuração do gateway.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. Crie gateway de Olá da TestVNet1. Neste passo, vai criar gateway de rede virtual Olá para a TestVNet1. As configurações VNet a VNet requerem um VpnType RouteBased. Criar um gateway, muitas vezes, pode demorar 45 minutos ou mais, dependendo do SKU de gateway selecionado Olá.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>Passo 3 – Criar e configurar a TestVNet4

Assim que tiver configurado a TestVNet1, crie a TestVNet4. Siga os passos de Olá abaixo, substituindo os valores de Olá com os seus próprios quando necessário. Este passo pode ser feito na Olá mesma sessão do PowerShell porque está a ser Olá mesma subscrição.

1. Declarar as variáveis. Ser tooreplace se valores Olá com Olá aqueles que pretende que toouse para a sua configuração.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. Crie um novo grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Crie Olá configurações de sub-rede da TestVNet4.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. Criar a TestVNet4.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. Solicitar um endereço IP público.

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Crie a configuração do gateway Olá.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Crie Olá TestVNet4 gateway. Criar um gateway, muitas vezes, pode demorar 45 minutos ou mais, dependendo do SKU de gateway selecionado Olá.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>Passo 4 – criar ligações Olá

1. Obter os gateways da rede virtual. Se ambas as gateways de Olá no Olá mesma subscrição, conforme forem no exemplo de Olá, pode concluir este passo na Olá mesma sessão do PowerShell.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Crie Olá TestVNet1 tooTestVNet4 ligação. Neste passo, criará Olá ligação da TestVNet1 tooTestVNet4. Verá uma chave partilhada referenciada nos exemplos de Olá. Pode utilizar os seus próprios valores para a chave partilhada Olá. Olá coisa que essa chave partilhada Olá, é importante tem de corresponder ao ambas as ligações. Criar uma ligação pode demorar uns toocomplete breves instantes.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Crie Olá TestVNet4 tooTestVNet1 ligação. Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet4 tooTestVNet1. Certifique-se de chaves de Olá partilhada correspondem. será possível estabelecer a ligação de Olá após alguns minutos.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. Verifique a ligação. Consulte a secção de Olá [como tooverify a ligação](#verify).

## <a name="difsub"></a>Como tooconnect VNets que estão em subscrições diferentes

![Diagrama v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

Neste cenário, vamos ligar TestVNet1 e TestVNet5. TestVNet1 e TestVNet5 residem em subscrições diferentes. subscrições de Olá não é necessário toobe associado Olá mesmo inquilino do Active Directory. diferença Olá entre estes passos e o conjunto anterior Olá é que alguns dos passos de configuração de Olá necessitam toobe efetuada numa sessão separada do PowerShell no contexto de Olá da subscrição segundo Olá. Especialmente quando Olá duas subscrições pertencem toodifferent organizações.

### <a name="step-5---create-and-configure-testvnet1"></a>Passo 5 - Criar e configurar a TestVNet1

Tem de concluir [passo 1](#Step1) e [passo 2](#Step2) de Olá anterior secção toocreate e configurar a TestVNet1 e hello do VPN Gateway da TestVNet1. Para esta configuração, não são necessária toocreate TestVNet4 da secção anterior Olá, embora se criá-la, este será não entrar em conflito com estes passos. Depois de concluir o passo 1 e o passo 2, prosseguir para o passo 6 toocreate TestVNet5. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>Passo 6 – Certifique-se de intervalos de endereços IP Olá

É importante toomake certificar-se de que espaço de endereços IP Olá de Olá nova rede virtual, TestVNet5, não se sobreponha a nenhum dos intervalos de Vnets ou intervalos de gateway de rede local. Neste exemplo, redes virtuais Olá poderão pertencer toodifferent organizações. Para este exercício, pode utilizar Olá os seguintes valores para Olá TestVNet5:

**Valores da TestVNet5:**

* Nome da VNet: TestVNet5
* Grupo de Recursos: TestRG5
* Localização: Leste do Japão
* TestVNet5: 10.51.0.0/16 e 10.52.0.0/16
* Front-End: 10.51.0.0/24
* Back-End: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* IP Público: VNet5GWIP
* VPNType: RouteBased
* Ligação: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>Passo 7 – Criar e configurar a TestVNet5

Este passo tem de ser efetuado no contexto de Olá da nova subscrição de Olá. Esta parte pode ser realizada pelo administrador de Olá numa organização diferente proprietária da subscrição Olá.

1. Declarar as variáveis. Ser tooreplace se valores Olá com Olá aqueles que pretende que toouse para a sua configuração.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Ligar toosubscription 5. Abra a consola do PowerShell e ligue tooyour conta. Utilize Olá toohelp de exemplo, ligar os seguintes:

  ```powershell
  Login-AzureRmAccount
  ```

  Verifique Olá subscrições para a conta de Olá.

  ```powershell
  Get-AzureRmSubscription
  ```

  Especifique que pretende que o toouse de subscrição de Olá.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. Crie um novo grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Crie Olá configurações de sub-rede para a TestVNet5.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. Criar a TestVNet5.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. Solicitar um endereço IP público.

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Crie a configuração do gateway Olá.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Crie Olá TestVNet5 gateway.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>Passo 8 - criar ligações Olá

Neste exemplo, porque os gateways de Olá estão em subscrições diferentes Olá, iremos tiver dividir este passo em duas sessões do PowerShell marcadas como [subscrição 1] e [subscrição 5].

1. **[Subscrição 1]**  Gateway de rede virtual Olá get da subscrição 1. Iniciar sessão e ligar tooSubscription 1 antes de executar o seguinte exemplo de Olá:

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Copiar resultado Olá Olá seguintes elementos e envie estes administrador toohello da subscrição 5 por e-mail ou outro método.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  Estes dois elementos terão valores toohello semelhante, saída de exemplo a seguir:

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[Subscrição 5]**  Gateway de rede virtual Olá get da subscrição 5. Iniciar sessão e ligar tooSubscription 5 antes de executar o seguinte exemplo de Olá:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Copiar resultado Olá Olá seguintes elementos e envie estes administrador toohello da subscrição 1 por e-mail ou outro método.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  Estes dois elementos terão valores toohello semelhante, saída de exemplo a seguir:

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[Subscrição 1]**  Criar ligação Olá TestVNet1 tooTestVNet5. Neste passo, criará Olá ligação da TestVNet1 tooTestVNet5. diferença de Olá aqui é que $vnet5gw não pode ser obtido diretamente porque está numa subscrição diferente. Precisa de toocreate um novo objeto do PowerShell com valores de Olá comunicados da subscrição 1 nos passos Olá acima. Utilize o exemplo de Olá abaixo. Substitua os seus próprios valores Olá nome, a Id e a chave partilhada. Olá coisa que essa chave partilhada Olá, é importante tem de corresponder ao ambas as ligações. Criar uma ligação pode demorar uns toocomplete breves instantes.

  Ligar tooSubscription 1 antes de executar o seguinte exemplo de Olá:

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[Subscrição 5]**  Criar ligação Olá TestVNet5 tooTestVNet1. Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet5 tooTestVNet1. Olá mesmo processo de criação de um objeto do PowerShell com base nos valores de Olá obtidos na subscrição 1 aplica-se aqui bem. Neste passo, lembre-se de que as chaves de Olá partilhada correspondem.

  Ligar tooSubscription 5 antes de executar o seguinte exemplo de Olá:

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>Como tooverify uma ligação

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>FAQ da ligação VNet a VNet

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Passos seguintes

* Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais. Consulte Olá [documentação de Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para obter mais informações.
* Para informações sobre o BGP, consulte Olá [descrição geral do BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
