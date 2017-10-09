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
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a><span data-ttu-id="5bf10-103">Configurar a imposição do túnel utilizando o modelo de implementação Azure Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="5bf10-103">Configure forced tunneling using hello Azure Resource Manager deployment model</span></span>

<span data-ttu-id="5bf10-104">Imposição do túnel permite redirecionar ou "forçar" todos os vinculado à Internet tráfego back tooyour localização no local através de um túnel VPN Site a Site para inspeção e auditoria.</span><span class="sxs-lookup"><span data-stu-id="5bf10-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="5bf10-105">Este é um requisito de segurança críticas para TI empresariais de maioria das políticas.</span><span class="sxs-lookup"><span data-stu-id="5bf10-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="5bf10-106">Sem a imposição do túnel, o tráfego vinculado à Internet do seu VMs no Azure sempre atravessa da infraestrutura de rede do Azure diretamente saída toohello Internet, sem Olá opção tooallow, tráfego de Olá tooinspect ou de auditoria.</span><span class="sxs-lookup"><span data-stu-id="5bf10-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="5bf10-107">Acesso à Internet não autorizado pode provocar potencialmente tooinformation divulgação ou outros tipos de falhas de segurança.</span><span class="sxs-lookup"><span data-stu-id="5bf10-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="5bf10-108">Este artigo explica como configurar forçado túnel para redes virtuais criadas com o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf10-108">This article walks you through configuring forced tunneling for virtual networks created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="5bf10-109">Imposição do túnel pode ser configurado utilizando o PowerShell, não através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf10-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="5bf10-110">Se quiser tooconfigure imposição do túnel para o modelo de implementação clássica Olá, selecione artigo clássico Olá na lista pendente a seguir:</span><span class="sxs-lookup"><span data-stu-id="5bf10-110">If you want tooconfigure forced tunneling for hello classic deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5bf10-111">PowerShell – Clássica</span><span class="sxs-lookup"><span data-stu-id="5bf10-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="5bf10-112">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5bf10-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="5bf10-113">Prestes imposição do túnel</span><span class="sxs-lookup"><span data-stu-id="5bf10-113">About forced tunneling</span></span>

<span data-ttu-id="5bf10-114">Olá seguinte diagrama ilustra funciona como imposição de túnel.</span><span class="sxs-lookup"><span data-stu-id="5bf10-114">hello following diagram illustrates how forced tunneling works.</span></span> 

![Túnel Forçado](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="5bf10-116">No exemplo de Olá acima, Olá front-end sub-rede não está a ser forçada em túnel.</span><span class="sxs-lookup"><span data-stu-id="5bf10-116">In hello example above, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="5bf10-117">Olá cargas de trabalho na sub-rede do front-end de Olá podem continuar tooaccept e responder a pedidos de toocustomer de Olá Internet diretamente.</span><span class="sxs-lookup"><span data-stu-id="5bf10-117">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="5bf10-118">Olá sub-redes de camada média dimensão que e back-end são forçadas em túnel.</span><span class="sxs-lookup"><span data-stu-id="5bf10-118">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="5bf10-119">Quaisquer ligações de saída do toohello duas sub-redes Internet será tooan forçada ou redirecionado novamente o site de no local através de um dos Olá que túneis S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="5bf10-119">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="5bf10-120">Isto permite-lhe toorestrict e inspecionar o acesso à Internet das suas máquinas virtuais ou serviços em nuvem na Azure, ao continuar tooenable a arquitetura do serviço de várias camadas necessárias.</span><span class="sxs-lookup"><span data-stu-id="5bf10-120">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="5bf10-121">Se não houver nenhuma cargas de trabalho para a Internet nas suas redes virtuais, também pode aplicar forçada túnel toohello todo redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="5bf10-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling toohello entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="5bf10-122">Requisitos e considerações</span><span class="sxs-lookup"><span data-stu-id="5bf10-122">Requirements and considerations</span></span>

<span data-ttu-id="5bf10-123">Imposição do túnel no Azure está configurado através de rotas definidas pelo utilizador de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5bf10-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="5bf10-124">Redirecionar o tráfego tooan no local site é expresso como um gateway de VPN do Azure de toohello de rota predefinida.</span><span class="sxs-lookup"><span data-stu-id="5bf10-124">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="5bf10-125">Para obter mais informações sobre o encaminhamento definido pelo utilizador e redes virtuais, consulte [rotas definidas pelo utilizador e reencaminhamento IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bf10-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="5bf10-126">Cada sub-rede da rede virtual tem uma tabela de encaminhamento incorporada, do sistema.</span><span class="sxs-lookup"><span data-stu-id="5bf10-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="5bf10-127">tabela de encaminhamento de sistema de Olá tem Olá seguintes três grupos de rotas:</span><span class="sxs-lookup"><span data-stu-id="5bf10-127">hello system routing table has hello following three groups of routes:</span></span>
  
  * <span data-ttu-id="5bf10-128">**Rotas de VNet locais:** diretamente toohello destino VMs no Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5bf10-128">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="5bf10-129">**No local rotas:** toohello VPN gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bf10-129">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="5bf10-130">**Rota predefinida:** toohello diretamente à Internet.</span><span class="sxs-lookup"><span data-stu-id="5bf10-130">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="5bf10-131">Pacotes destinados a toohello endereços IP privados não abrangidos por rotas Olá dois anteriores são ignorados.</span><span class="sxs-lookup"><span data-stu-id="5bf10-131">Packets destined toohello private IP addresses not covered by hello previous two routes are dropped.</span></span>
* <span data-ttu-id="5bf10-132">Este procedimento utiliza rotas definidas pelo utilizador (UDR) toocreate um tooadd de tabela de encaminhamento uma rota predefinida e, em seguida, associar Olá encaminhamento tabela tooyour VNet subnet(s) tooenable forçado túnel em dessas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="5bf10-132">This procedure uses user-defined routes (UDR) toocreate a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="5bf10-133">Imposição do túnel tem de ser associado a uma VNet com um gateway de VPN baseado na rota.</span><span class="sxs-lookup"><span data-stu-id="5bf10-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="5bf10-134">É necessário tooset "site predefinido" entre a rede virtual do Olá em vários locais sites locais toohello ligado.</span><span class="sxs-lookup"><span data-stu-id="5bf10-134">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span> <span data-ttu-id="5bf10-135">Além disso, Olá no local do dispositivo VPN tem de ser configurado utilizando 0.0.0.0/0 como seletores de tráfego.</span><span class="sxs-lookup"><span data-stu-id="5bf10-135">Also, hello on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="5bf10-136">ExpressRoute imposição do túnel não está configurada através desta mecanismo, mas em vez disso, é ativado por uma rota predefinida através de Olá BGP de ExpressRoute de publicidade sessões de peering.</span><span class="sxs-lookup"><span data-stu-id="5bf10-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="5bf10-137">Para obter mais informações, consulte Olá [documentação do ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="5bf10-137">For more information, see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="5bf10-138">Descrição geral de configuração</span><span class="sxs-lookup"><span data-stu-id="5bf10-138">Configuration overview</span></span>

<span data-ttu-id="5bf10-139">Olá, seguindo o procedimento ajuda a criar um grupo de recursos e uma VNet.</span><span class="sxs-lookup"><span data-stu-id="5bf10-139">hello following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="5bf10-140">Em seguida, irá criar um gateway de VPN e configurar a imposição do túnel.</span><span class="sxs-lookup"><span data-stu-id="5bf10-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="5bf10-141">Neste procedimento, Olá a rede virtual 'MultiTier VNet' tem três sub-redes: 'Front-end', 'Midtier' e 'Back-end', com quatro em vários locais ligações: 'DefaultSiteHQ' e três ramos.</span><span class="sxs-lookup"><span data-stu-id="5bf10-141">In this procedure, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="5bf10-142">passos do procedimento de Olá definidas Olá 'DefaultSiteHQ' como ligação de site Olá predefinido para a imposição do túnel e configurar Olá 'Midtier' e 'Back-end' sub-redes toouse imposição do túnel.</span><span class="sxs-lookup"><span data-stu-id="5bf10-142">hello procedure steps set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello 'Midtier' and 'Backend' subnets toouse forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5bf10-143">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="5bf10-143">Before you begin</span></span>

<span data-ttu-id="5bf10-144">Instale a versão mais recente do Olá do Olá cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5bf10-144">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5bf10-145">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre a instalação de cmdlets do PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf10-145">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="toolog-in"></a><span data-ttu-id="5bf10-146">toolog no</span><span class="sxs-lookup"><span data-stu-id="5bf10-146">toolog in</span></span>

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="5bf10-147">Configurar túnel forçado</span><span class="sxs-lookup"><span data-stu-id="5bf10-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="5bf10-148">Crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5bf10-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="5bf10-149">Criar uma rede virtual e especificar sub-redes.</span><span class="sxs-lookup"><span data-stu-id="5bf10-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="5bf10-150">Crie Olá gateways de rede local.</span><span class="sxs-lookup"><span data-stu-id="5bf10-150">Create hello local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="5bf10-151">Crie Regra de rota e tabela de rota de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf10-151">Create hello route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="5bf10-152">Associe toohello de tabela de rota Olá Midtier e sub-redes de back-end.</span><span class="sxs-lookup"><span data-stu-id="5bf10-152">Associate hello route table toohello Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="5bf10-153">Crie Olá Gateway com um site predefinido.</span><span class="sxs-lookup"><span data-stu-id="5bf10-153">Create hello Gateway with a default site.</span></span> <span data-ttu-id="5bf10-154">Este passo demora alguns toocomplete de tempo, por vezes, 45 minutos ou mais, porque são criar e configurar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bf10-154">This step takes some time toocomplete, sometimes 45 minutes or more, because you are creating and configuring hello gateway.</span></span><br> <span data-ttu-id="5bf10-155">Olá **- GatewayDefaultSite** é Olá parâmetros do cmdlet que lhe permite Olá forçado encaminhamento toowork de configuração, por isso, demorar cuidado tooconfigure esta definição corretamente.</span><span class="sxs-lookup"><span data-stu-id="5bf10-155">hello **-GatewayDefaultSite** is hello cmdlet parameter that allows hello forced routing configuration toowork, so take care tooconfigure this setting properly.</span></span> <span data-ttu-id="5bf10-156">Este parâmetro é disponíveis no PowerShell 1.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5bf10-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="5bf10-157">Estabelece ligações de VPN Olá Site para Site.</span><span class="sxs-lookup"><span data-stu-id="5bf10-157">Establish hello Site-to-Site VPN connections.</span></span>

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