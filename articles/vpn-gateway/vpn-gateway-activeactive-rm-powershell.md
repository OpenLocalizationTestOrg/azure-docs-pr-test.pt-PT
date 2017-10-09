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
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="1f3c9-103">Configurar ligações de S2S VPN de ativo-ativo com Gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="1f3c9-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="1f3c9-104">Este artigo explica Olá passos toocreate ativo-ativo em vários locais e ligações VNet a VNet com o modelo de implementação do Resource Manager Olá e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="1f3c9-105">Acerca das ligações em vários locais elevada</span><span class="sxs-lookup"><span data-stu-id="1f3c9-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="1f3c9-106">tooachieve elevada disponibilidade para conectividade de VNet a VNet e em vários locais, deve implementar vários gateways VPN e estabelecer várias ligações paralelas entre as suas redes e do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="1f3c9-107">Consulte [altamente disponível em vários locais e VNet a VNet conectividade](vpn-gateway-highlyavailable.md) para uma descrição geral da topologia e as opções de conectividade.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="1f3c9-108">Este artigo fornece instruções de Olá tooset segurança de um ativo-ativo em vários locais ligação VPN e ligação de ativo-ativo entre duas redes virtuais:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="1f3c9-109">Parte 1 – criar e configurar o gateway de VPN do Azure no modo ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="1f3c9-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="1f3c9-110">Parte 2 - estabelecer ligações de ativo-ativo em vários locais</span><span class="sxs-lookup"><span data-stu-id="1f3c9-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="1f3c9-111">Parte 3 - estabelecer ligações VNet a VNet de ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="1f3c9-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="1f3c9-112">Parte 4 - atualizar gateway existente entre ativo-ativo e modo de espera ativo</span><span class="sxs-lookup"><span data-stu-id="1f3c9-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="1f3c9-113">Pode combinar estas toobuild em conjunto uma topologia de rede mais complexa, altamente disponíveis que satisfaça as suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f3c9-114">Tenha em atenção de que modo de ativo-ativo Olá utiliza Olá apenas SKUs os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="1f3c9-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="1f3c9-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="1f3c9-116">HighPerformance (para SKUs legados antigos)</span><span class="sxs-lookup"><span data-stu-id="1f3c9-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="1f3c9-117"><a name ="aagateway"></a>Parte 1 – criar e configurar os gateways de VPN de ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="1f3c9-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="1f3c9-118">Olá, os passos seguintes irá configurar o gateway de VPN do Azure nos modos de ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="1f3c9-119">Olá principais diferenças entre os gateways de ativo-ativo e modo de espera ativo Olá:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="1f3c9-120">Terá de toocreate configurações de IP do Gateway dois com dois endereços IP públicos</span><span class="sxs-lookup"><span data-stu-id="1f3c9-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="1f3c9-121">Precisa de definir o sinalizador de EnableActiveActiveFeature Olá</span><span class="sxs-lookup"><span data-stu-id="1f3c9-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="1f3c9-122">SKU de gateway Olá tem de ser VpnGw1, VpnGw2, VpnGw3 ou HighPerformance (legado SKU).</span><span class="sxs-lookup"><span data-stu-id="1f3c9-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="1f3c9-123">Olá outras propriedades são Olá igual a gateways do Olá não ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="1f3c9-124">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="1f3c9-124">Before you begin</span></span>
* <span data-ttu-id="1f3c9-125">Verifique se tem uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="1f3c9-126">Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f3c9-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1f3c9-127">Irá precisar de tooinstall Olá Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="1f3c9-128">Consulte [descrição geral do Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre a instalação de cmdlets do PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="1f3c9-129">Passo 1 – criar e configurar VNet1</span><span class="sxs-lookup"><span data-stu-id="1f3c9-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="1f3c9-130">1. Declarar as variáveis</span><span class="sxs-lookup"><span data-stu-id="1f3c9-130">1. Declare your variables</span></span>
<span data-ttu-id="1f3c9-131">Para este exercício, vamos começar por declarar as nossas variáveis.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="1f3c9-132">exemplo de Olá abaixo declara as variáveis de Olá utilizando valores de Olá para este exercício.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="1f3c9-133">Quando configurar para produção de ser valores de Olá tooreplace se com os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="1f3c9-134">Pode utilizar estas variáveis se estiver a executar através de Olá passos toobecome familiarizado com este tipo de configuração.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="1f3c9-135">Modificar variáveis de Olá e, em seguida, copie e cole a consola do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="1f3c9-136">2. Ligar tooyour subscrição e crie um novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1f3c9-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="1f3c9-137">Certifique-se de que muda tooPowerShell-Olá modo toouse cmdlets do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="1f3c9-138">Para obter mais informações, veja [Utilizar o Windows PowerShell com o Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1f3c9-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="1f3c9-139">Abra a consola do PowerShell e ligue tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="1f3c9-140">Utilize Olá toohelp de exemplo, ligar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="1f3c9-141">3. Criar a TestVNet1</span><span class="sxs-lookup"><span data-stu-id="1f3c9-141">3. Create TestVNet1</span></span>
<span data-ttu-id="1f3c9-142">exemplo de Olá abaixo cria uma rede virtual denominada TestVNet1 e três sub-redes, um GatewaySubnet chamado, um front-end e um back-end.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="1f3c9-143">Quando estiver a substituir os valores, é importante que dê sempre à sub-rede do gateway o nome específico GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="1f3c9-144">Se der outro nome, a criação da gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="1f3c9-145">Passo 2 - Criar gateway de VPN Olá da TestVNet1 com modo ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="1f3c9-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="1f3c9-146">1. Criar os endereços IP públicos Olá e configurações de IP do gateway</span><span class="sxs-lookup"><span data-stu-id="1f3c9-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="1f3c9-147">Pedido de dois pública IP endereços toobe toohello alocado gateway que será criado para a sua VNet.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="1f3c9-148">Também irá definir sub-rede Olá e configurações de IP necessárias.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="1f3c9-149">2. Criar gateway de VPN de Olá com a configuração de ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="1f3c9-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="1f3c9-150">Crie gateway de rede virtual Olá da TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="1f3c9-151">Tenha em atenção que existem duas entradas GatewayIpConfig e Olá EnableActiveActiveFeature sinalizador está definido.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="1f3c9-152">Criar um gateway pode demorar algum tempo (45 minutos ou mais toocomplete).</span><span class="sxs-lookup"><span data-stu-id="1f3c9-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="1f3c9-153">3. Obter Olá gateway os endereços IP públicos e endereço de IP do elemento BGP Olá</span><span class="sxs-lookup"><span data-stu-id="1f3c9-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="1f3c9-154">Assim que for criado o gateway de Olá, terá de endereço de IP do elemento BGP Olá tooobtain no Olá Gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="1f3c9-155">Este endereço é necessário tooconfigure Olá Gateway de VPN do Azure como um elemento de rede BGP para os seus dispositivos VPN no local.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="1f3c9-156">Utilize os seguintes cmdlets tooshow Olá dois endereços IP públicos alocados para o gateway de VPN e os respetivos endereços de IP do elemento BGP correspondentes para cada instância de gateway de Olá:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

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

<span data-ttu-id="1f3c9-157">ordem de Olá dos endereços IP públicos do Olá para instâncias de gateway Olá e Olá endereços de Peering de BGP correspondentes são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="1f3c9-158">Neste exemplo, o gateway de Olá VM com o IP público de 40.112.190.5 utilizará 10.12.255.4 como o respetivo endereço de Peering de BGP e gateway Olá com 138.91.156.129 utilizará 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="1f3c9-159">Esta informação é necessária quando configura um local em dispositivos VPN a ligar o gateway de ativo-ativo toohello.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="1f3c9-160">gateway de Olá é mostrado no diagrama de Olá abaixo com todos os endereços:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![gateway de ativo-ativo](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="1f3c9-162">Assim que for criado o gateway de Olá, pode utilizar esta ligação de VNet a VNet ou gateway tooestablish ativo-ativo em vários locais.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="1f3c9-163">Olá secções a seguir irá guiá-Olá passos toocomplete Olá exercício.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="1f3c9-164"><a name ="aacrossprem"></a>Parte 2 - estabelecer uma ligação de ativo-ativo em vários locais</span><span class="sxs-lookup"><span data-stu-id="1f3c9-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="1f3c9-165">tooestablish uma ligação entre locais, terá de toocreate toorepresent um Gateway de rede Local o dispositivo VPN no local e um ligação tooconnect Olá VPN gateway do Azure com o gateway de rede local Olá.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="1f3c9-166">Neste exemplo, o gateway de VPN do Azure Olá está no modo de ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="1f3c9-167">Como resultado, mesmo apesar de não existir apenas um no local o dispositivo VPN (gateway de rede local) e de recursos de uma ligação, ambas as instâncias de gateway de VPN do Azure irão estabelecer túneis S2S VPN com o dispositivo do Olá no local.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="1f3c9-168">Antes de continuar, certifique-se de que concluiu [parte 1](#aagateway) neste exercício.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="1f3c9-169">Passo 1 – criar e configurar o gateway de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="1f3c9-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="1f3c9-170">1. Declarar as variáveis</span><span class="sxs-lookup"><span data-stu-id="1f3c9-170">1. Declare your variables</span></span>
<span data-ttu-id="1f3c9-171">Neste exercício irá continuar a configuração de Olá toobuild mostrada no diagrama de Olá.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="1f3c9-172">Ser tooreplace se valores Olá com Olá aqueles que pretende que toouse para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="1f3c9-173">Alguns aspetos toonote sobre os parâmetros de gateway de rede local Olá:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="1f3c9-174">gateway de rede local Olá pode ter Olá mesmo ou outra localização e recursos de grupo como Olá gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="1f3c9-175">Este exemplo mostra-los em grupos de recursos diferente, mas Olá mesma localização do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="1f3c9-176">Se houver apenas um dispositivo VPN no local, conforme mostrado acima, a ligação de ativo-ativo Olá pode trabalhar com ou sem protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="1f3c9-177">Este exemplo utiliza o BGP para ligação do Olá em vários locais.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="1f3c9-178">Se o BGP está ativado, o prefixo de Olá precisa toodeclare para gateway de rede local Olá é endereço do anfitrião Olá do seu endereço de IP do elemento BGP no seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="1f3c9-179">Neste caso, é um /32 prefixo do nome de "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="1f3c9-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="1f3c9-180">Como um lembrete, tem de utilizar ASNs diferentes de BGP entre as redes no local e a VNet do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="1f3c9-181">Se são hello iguais, é necessário toochange o ASN de VNet se o dispositivo VPN no local utiliza já Olá ASN toopeer com outros vizinhos BGP.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="1f3c9-182">2. Criar gateway de rede local Olá para Site5</span><span class="sxs-lookup"><span data-stu-id="1f3c9-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="1f3c9-183">Antes de continuar, certifique-se de que estão ligado ainda tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="1f3c9-184">Crie grupo de recursos de Olá se ainda não é criado.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="1f3c9-185">Passo 2 - ligar o gateway de VNet Olá e gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="1f3c9-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="1f3c9-186">1. Obter Olá dois gateways</span><span class="sxs-lookup"><span data-stu-id="1f3c9-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="1f3c9-187">2. Criar a ligação de tooSite5 Olá TestVNet1</span><span class="sxs-lookup"><span data-stu-id="1f3c9-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="1f3c9-188">Neste passo, vai criar Olá ligação da TestVNet1 tooSite5_1 com "EnableBGP" definido demasiado$ True.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="1f3c9-189">3. Parâmetros VPN e BGP para o dispositivo VPN no local</span><span class="sxs-lookup"><span data-stu-id="1f3c9-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="1f3c9-190">exemplo de Olá abaixo apresenta uma lista de parâmetros de Olá que vai introduzir no Olá secção de configuração de BGP no dispositivo VPN no local para este exercício:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="1f3c9-191">Site5 ASN: 65050</span><span class="sxs-lookup"><span data-stu-id="1f3c9-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="1f3c9-192">IP do BGP Site5: 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="1f3c9-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="1f3c9-193">Prefixos tooannounce: (por exemplo) 10.51.0.0/16 e 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="1f3c9-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="1f3c9-194">ASN de VNet do Azure: 65010</span><span class="sxs-lookup"><span data-stu-id="1f3c9-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="1f3c9-195">IP de BGP do Azure VNet 1: 10.12.255.4 para too40.112.190.5 de túnel</span><span class="sxs-lookup"><span data-stu-id="1f3c9-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="1f3c9-196">IP de BGP do Azure VNet 2: 10.12.255.5 para too138.91.156.129 de túnel</span><span class="sxs-lookup"><span data-stu-id="1f3c9-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="1f3c9-197">Rotas estáticas: destino 10.12.255.4/32, nexthop Olá VPN túnel interface too40.112.190.5 destino 10.12.255.5/32, too138.91.156.129 de interface de túnel do nexthop Olá VPN</span><span class="sxs-lookup"><span data-stu-id="1f3c9-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="1f3c9-198">eBGP Multihop: Certifique-se de opção de "multihop" Olá para eBGP está ativado no seu dispositivo, se for necessário</span><span class="sxs-lookup"><span data-stu-id="1f3c9-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="1f3c9-199">deve ser estabelecida a ligação de Olá após alguns minutos e a sessão de peering de BGP de Olá serão iniciado depois de é estabelecido Olá ligação IPsec.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="1f3c9-200">Neste exemplo, até ao momento configurou o dispositivo VPN no local apenas uma, resultando no diagrama de Olá mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![ativo-ativo-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="1f3c9-202">Passo 3 – ligar os dois locais VPN dispositivos toohello ativo-ativo do VPN gateway</span><span class="sxs-lookup"><span data-stu-id="1f3c9-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="1f3c9-203">Se tiver dois dispositivos VPN no Olá mesmo local rede, pode conseguir redundância dupla por ligação Olá VPN do Azure toohello segundo VPN dispositivo de gateway.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="1f3c9-204">1. Criar gateway de rede local segundo Olá para Site5</span><span class="sxs-lookup"><span data-stu-id="1f3c9-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="1f3c9-205">Tenha em atenção que o endereço IP do gateway Olá, prefixo de endereço e endereço de peering de BGP de gateway de rede local segundo Olá não podem sobrepor com gateway rede local anterior Olá para Olá mesmo rede no local.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="1f3c9-206">2. Ligar o gateway de VNet Olá e gateway de rede local segundo Olá</span><span class="sxs-lookup"><span data-stu-id="1f3c9-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="1f3c9-207">Criar ligação Olá da TestVNet1 tooSite5_2 com "EnableBGP" definido demasiado$ True</span><span class="sxs-lookup"><span data-stu-id="1f3c9-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="1f3c9-208">3. Parâmetros VPN e BGP para o segundo dispositivo VPN no local</span><span class="sxs-lookup"><span data-stu-id="1f3c9-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="1f3c9-209">Da mesma forma, abaixo apresenta uma lista de parâmetros de Olá irá introduzir no dispositivo VPN segundo Olá:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

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

<span data-ttu-id="1f3c9-210">Assim que são estabelecida a ligação de Olá (túneis), terá duplos dispositivos VPN redundantes e túneis ligar a rede no local e o Azure:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![Dual-redundância-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="1f3c9-212"><a name ="aav2v"></a>Parte 3 - estabelecer uma ligação de VNet a VNet ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="1f3c9-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="1f3c9-213">Esta secção cria uma ligação de VNet a VNet ativo-ativo com o BGP.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="1f3c9-214">instruções de Olá abaixo continuam dos passos anteriores Olá listados acima.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="1f3c9-215">Tem de concluir [parte 1](#aagateway) toocreate e configurar a TestVNet1 e Olá Gateway de VPN com o BGP.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="1f3c9-216">Passo 1 – criar gateway VPN TestVNet2 e Olá</span><span class="sxs-lookup"><span data-stu-id="1f3c9-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="1f3c9-217">É importante toomake certificar-se de que espaço de endereços IP Olá de Olá nova rede virtual, TestVNet2, não se sobreponha a nenhum dos intervalos sua VNet.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="1f3c9-218">Neste exemplo, redes virtuais Olá pertencem toohello mesma subscrição.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="1f3c9-219">Pode configurar ligações VNet a VNet entre subscrições diferentes; Consulte demasiado[configurar uma ligação VNet a VNet](vpn-gateway-vnet-vnet-rm-ps.md) toolearn mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="1f3c9-220">Certifique-se de adicionar Olá "-EnableBgp $True" quando criar Olá tooenable ligações BGP.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="1f3c9-221">1. Declarar as variáveis</span><span class="sxs-lookup"><span data-stu-id="1f3c9-221">1. Declare your variables</span></span>
<span data-ttu-id="1f3c9-222">Ser tooreplace se valores Olá com Olá aqueles que pretende que toouse para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="1f3c9-223">2. Criar TestVNet2 no novo grupo de recursos Olá</span><span class="sxs-lookup"><span data-stu-id="1f3c9-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="1f3c9-224">3. Criar gateway de VPN do Olá ativo-ativo para TestVNet2</span><span class="sxs-lookup"><span data-stu-id="1f3c9-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="1f3c9-225">Pedido de dois pública IP endereços toobe toohello alocado gateway que será criado para a sua VNet.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="1f3c9-226">Também irá definir sub-rede Olá e configurações de IP necessárias.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="1f3c9-227">Crie gateway de VPN Olá com Olá como número e Olá sinalizador "EnableActiveActiveFeature".</span><span class="sxs-lookup"><span data-stu-id="1f3c9-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="1f3c9-228">Tenha em atenção que tem de substituir a predefinição de Olá ASN em gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="1f3c9-229">Olá ASNs para Olá ligados a VNets tem de ser diferentes tooenable BGP e o encaminhamento de trânsito.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="1f3c9-230">Passo 2 – ligar os gateways de TestVNet1 e TestVNet2 Olá</span><span class="sxs-lookup"><span data-stu-id="1f3c9-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="1f3c9-231">Neste exemplo, ambas as gateways estão na Olá mesma subscrição.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="1f3c9-232">Pode concluir este passo na Olá mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="1f3c9-233">1. Obter ambas as gateways</span><span class="sxs-lookup"><span data-stu-id="1f3c9-233">1. Get both gateways</span></span>
<span data-ttu-id="1f3c9-234">Certifique-se de que iniciar sessão e ligar tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="1f3c9-235">2. Criar ambas as ligações</span><span class="sxs-lookup"><span data-stu-id="1f3c9-235">2. Create both connections</span></span>
<span data-ttu-id="1f3c9-236">Neste passo, irá criar a ligação Olá da TestVNet1 tooTestVNet2 e ligação Olá de TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="1f3c9-237">Ser tooenable se BGP para ambas as ligações.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="1f3c9-238">Depois de concluir estes passos, será possível estabelecer ligação Olá dentro de alguns minutos e sessões de peering de BGP de Olá serão cópias de segurança depois de concluída a ligação de Olá VNet a VNet com redundância dupla:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![ativo-ativo-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="1f3c9-240"><a name ="aaupdate"></a>Parte 4 - atualizar gateway existente entre ativo-ativo e modo de espera ativo</span><span class="sxs-lookup"><span data-stu-id="1f3c9-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="1f3c9-241">última seção do Olá descrevem como configurar um gateway de VPN do Azure existente do modo de tooactive-Active Directory de modo de espera ativo, ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="1f3c9-242">Esta secção inclui os passos de Olá tooresize um SKU legado (antigo SKU) de um gateway VPN já criou de tooHighPerformance padrão.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="1f3c9-243">Estes passos não atualizar um tooone SKU legado antigo de Olá SKUs de novo.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="1f3c9-244">Configurar um gateway do gateway de modo de espera ativo tooactive-Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f3c9-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="1f3c9-245">1. Parâmetros de gateway</span><span class="sxs-lookup"><span data-stu-id="1f3c9-245">1. Gateway parameters</span></span>
<span data-ttu-id="1f3c9-246">Olá seguinte o exemplo converte um gateway de modo de espera ativo de um gateway de ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="1f3c9-247">É necessário toocreate outro endereço IP público, em seguida, adicionar uma segunda configuração de IP do Gateway.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="1f3c9-248">Abaixo mostra hello utilizados parâmetros:</span><span class="sxs-lookup"><span data-stu-id="1f3c9-248">Below shows hello parameters used:</span></span>

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

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="1f3c9-249">2. Criar endereço IP público do Olá, em seguida, adicionar configuração de IP do gateway segundo Olá</span><span class="sxs-lookup"><span data-stu-id="1f3c9-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="1f3c9-250">3. Ativar o gateway de Olá de modo e de atualização de ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="1f3c9-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="1f3c9-251">Tem de definir o objeto do gateway Olá na atualização do PowerShell tootrigger Olá real.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="1f3c9-252">Olá SKU do gateway de rede virtual Olá tem também de ser alterada tooHighPerformance (redimensionado), uma vez que foi criada anteriormente como padrão.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="1f3c9-253">Esta atualização pode demorar too45 de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="1f3c9-254">Configurar um gateway de tooactive-modo de espera ativo-ativo gateway</span><span class="sxs-lookup"><span data-stu-id="1f3c9-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="1f3c9-255">1. Parâmetros de gateway</span><span class="sxs-lookup"><span data-stu-id="1f3c9-255">1. Gateway parameters</span></span>
<span data-ttu-id="1f3c9-256">Utilize Olá mesmo parâmetros acima, como obter o nome de Olá Olá da configuração de IP que pretende tooremove.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="1f3c9-257">2. Remova a configuração de IP do gateway Olá e desativar o modo de ativo-ativo Olá</span><span class="sxs-lookup"><span data-stu-id="1f3c9-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="1f3c9-258">Da mesma forma, é necessário definir o objeto do gateway Olá na atualização do PowerShell tootrigger Olá real.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="1f3c9-259">Esta atualização pode demorar até too30 demasiado 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f3c9-260">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1f3c9-260">Next steps</span></span>
<span data-ttu-id="1f3c9-261">Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="1f3c9-262">Veja [Criar uma Máquina Virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter os passos.</span><span class="sxs-lookup"><span data-stu-id="1f3c9-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
