---
title: "Configurar a imposição do túnel para ligações do Azure Site a Site: clássico | Microsoft Docs"
description: "Como tooyour do tráfego de Internet vinculados back do tooredirect ou 'force' todos os localização no local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="84210-103">Configurar a imposição do túnel utilizando o modelo de implementação clássica Olá</span><span class="sxs-lookup"><span data-stu-id="84210-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="84210-104">Imposição do túnel permite redirecionar ou "forçar" todos os vinculado à Internet tráfego back tooyour localização no local através de um túnel VPN Site a Site para inspeção e auditoria.</span><span class="sxs-lookup"><span data-stu-id="84210-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="84210-105">Este é um requisito de segurança críticas para TI empresariais de maioria das políticas.</span><span class="sxs-lookup"><span data-stu-id="84210-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="84210-106">Sem a imposição do túnel, o tráfego vinculado à Internet do seu VMs no Azure serão sempre atravessar da infraestrutura de rede do Azure diretamente saída toohello Internet, sem Olá opção tooallow, tráfego de Olá tooinspect ou auditoria.</span><span class="sxs-lookup"><span data-stu-id="84210-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="84210-107">Acesso à Internet não autorizado pode provocar potencialmente tooinformation divulgação ou outros tipos de falhas de segurança.</span><span class="sxs-lookup"><span data-stu-id="84210-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="84210-108">Este artigo explica como configurar forçado túnel para redes virtuais criadas com o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="84210-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="84210-109">Imposição do túnel pode ser configurado utilizando o PowerShell, não através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="84210-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="84210-110">Se quiser tooconfigure imposição do túnel para o modelo de implementação do Resource Manager Olá, selecione artigo clássico Olá na lista pendente a seguir:</span><span class="sxs-lookup"><span data-stu-id="84210-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="84210-111">PowerShell – Clássica</span><span class="sxs-lookup"><span data-stu-id="84210-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="84210-112">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="84210-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="84210-113">Requisitos e considerações</span><span class="sxs-lookup"><span data-stu-id="84210-113">Requirements and considerations</span></span>
<span data-ttu-id="84210-114">Imposição do túnel no Azure está configurado através de rotas definidas pelo utilizador da rede virtual (UDR).</span><span class="sxs-lookup"><span data-stu-id="84210-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="84210-115">Redirecionar o tráfego tooan no local site é expresso como um gateway de VPN do Azure de toohello de rota predefinida.</span><span class="sxs-lookup"><span data-stu-id="84210-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="84210-116">Olá secção seguinte apresenta uma lista de limitação atual Olá de rotas e tabela de encaminhamento de Olá para uma rede Virtual do Azure:</span><span class="sxs-lookup"><span data-stu-id="84210-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="84210-117">Cada sub-rede da rede virtual tem uma tabela de encaminhamento incorporada, do sistema.</span><span class="sxs-lookup"><span data-stu-id="84210-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="84210-118">tabela de encaminhamento de sistema de Olá tem Olá seguintes três grupos de rotas:</span><span class="sxs-lookup"><span data-stu-id="84210-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="84210-119">**Rotas de VNet locais:** diretamente toohello destino VMs no Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="84210-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="84210-120">**No local rotas:** toohello VPN gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="84210-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="84210-121">**Rota predefinida:** toohello diretamente à Internet.</span><span class="sxs-lookup"><span data-stu-id="84210-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="84210-122">Pacotes destinados a toohello endereços IP privados não abrangidos por rotas Olá dois anterior serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="84210-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="84210-123">Com a versão de Olá de rotas definidas pelo utilizador, pode criar um encaminhamento tooadd de tabela uma rota predefinida e, em seguida, associar Olá encaminhamento tabela tooyour VNet subnet(s) tooenable forçado túnel nessas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="84210-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="84210-124">É necessário tooset "site predefinido" entre a rede virtual do Olá em vários locais sites locais toohello ligado.</span><span class="sxs-lookup"><span data-stu-id="84210-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="84210-125">Imposição do túnel tem de ser associado a uma VNet com um gateway VPN encaminhamento dinâmico (não um gateway estático).</span><span class="sxs-lookup"><span data-stu-id="84210-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="84210-126">ExpressRoute imposição do túnel não está configurada através desta mecanismo, mas em vez disso, é ativado por uma rota predefinida através de Olá BGP de ExpressRoute de publicidade sessões de peering.</span><span class="sxs-lookup"><span data-stu-id="84210-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="84210-127">Consulte Olá [documentação do ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="84210-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="84210-128">Descrição geral de configuração</span><span class="sxs-lookup"><span data-stu-id="84210-128">Configuration overview</span></span>
<span data-ttu-id="84210-129">No seguinte exemplo de Olá, Olá front-end sub-rede não está a ser forçada em túnel.</span><span class="sxs-lookup"><span data-stu-id="84210-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="84210-130">Olá cargas de trabalho na sub-rede do front-end de Olá podem continuar tooaccept e responder a pedidos de toocustomer de Olá Internet diretamente.</span><span class="sxs-lookup"><span data-stu-id="84210-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="84210-131">Olá sub-redes de camada média dimensão que e back-end são forçadas em túnel.</span><span class="sxs-lookup"><span data-stu-id="84210-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="84210-132">Quaisquer ligações de saída do toohello duas sub-redes Internet será tooan forçada ou redirecionado novamente o site de no local através de um dos Olá que túneis S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="84210-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="84210-133">Isto permite-lhe toorestrict e inspecionar o acesso à Internet das suas máquinas virtuais ou serviços em nuvem na Azure, ao continuar tooenable a arquitetura do serviço de várias camadas necessárias.</span><span class="sxs-lookup"><span data-stu-id="84210-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="84210-134">Também pode aplicar forçada túnel toohello todo redes virtuais se existirem não cargas de trabalho para a Internet nas suas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="84210-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Túnel Forçado](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="84210-136">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="84210-136">Before you begin</span></span>
<span data-ttu-id="84210-137">Certifique-se de que tem Olá seguintes itens antes da configuração do início.</span><span class="sxs-lookup"><span data-stu-id="84210-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="84210-138">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="84210-138">An Azure subscription.</span></span> <span data-ttu-id="84210-139">Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84210-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="84210-140">Uma rede virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="84210-140">A configured virtual network.</span></span> 
* <span data-ttu-id="84210-141">versão mais recente Olá do Olá cmdlets Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84210-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="84210-142">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre a instalação de cmdlets do PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="84210-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="84210-143">Configurar túnel forçado</span><span class="sxs-lookup"><span data-stu-id="84210-143">Configure forced tunneling</span></span>
<span data-ttu-id="84210-144">Olá seguir o procedimento irá ajudar a especificar a imposição do túnel para uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="84210-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="84210-145">passos de configuração de Olá correspondem o ficheiro de configuração de rede toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="84210-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="84210-146">Neste exemplo, Olá a rede virtual 'MultiTier VNet' tem três sub-redes: 'Front-end', 'Midtier' e 'Back-end' sub-redes, com ligações quatro locais cruzado: 'DefaultSiteHQ' e três ramos.</span><span class="sxs-lookup"><span data-stu-id="84210-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="84210-147">passos de Olá irão definir Olá 'DefaultSiteHQ' como ligação de site Olá predefinido para a imposição do túnel e configurar Olá Midtier e back-end sub-redes toouse imposição do túnel.</span><span class="sxs-lookup"><span data-stu-id="84210-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="84210-148">Crie uma tabela de encaminhamento.</span><span class="sxs-lookup"><span data-stu-id="84210-148">Create a routing table.</span></span> <span data-ttu-id="84210-149">Utilize Olá seguintes cmdlet toocreate a tabela de rota.</span><span class="sxs-lookup"><span data-stu-id="84210-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="84210-150">Adicione uma tabela de encaminhamento de toohello de rotas predefinidas.</span><span class="sxs-lookup"><span data-stu-id="84210-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="84210-151">Olá exemplo seguinte adiciona uma rota toohello tabela de encaminhamento predefinido criada no passo 1.</span><span class="sxs-lookup"><span data-stu-id="84210-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="84210-152">Tenha em atenção que Olá apenas rota suportada é o prefixo de destino Olá de "0.0.0.0/0" toohello NextHop "O VPNGateway".</span><span class="sxs-lookup"><span data-stu-id="84210-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="84210-153">Associe sub-redes de toohello de tabela Olá encaminhamento.</span><span class="sxs-lookup"><span data-stu-id="84210-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="84210-154">Depois de uma tabela de encaminhamento é criada e adicionado uma rota, utilize Olá tooadd de exemplo a seguir ou associar a sub-rede do Olá rota tabela tooa VNet.</span><span class="sxs-lookup"><span data-stu-id="84210-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="84210-155">exemplo de Olá adiciona Olá rota tabela "MyRouteTable" toohello Midtier e back-end sub-redes da VNet MultiTier VNet.</span><span class="sxs-lookup"><span data-stu-id="84210-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="84210-156">Atribua um site predefinido para a imposição do túnel.</span><span class="sxs-lookup"><span data-stu-id="84210-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="84210-157">Olá precedente passo, scripts de cmdlet de exemplo de Olá criado Olá tabela de encaminhamento em associados Olá tootwo de tabela de rota de sub-redes de VNet Olá.</span><span class="sxs-lookup"><span data-stu-id="84210-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="84210-158">passo restantes Olá é tooselect um site local entre as ligações de vários sites Olá da rede virtual do Olá como site de predefinido Olá ou túnel.</span><span class="sxs-lookup"><span data-stu-id="84210-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="84210-159">Cmdlets do PowerShell adicionais</span><span class="sxs-lookup"><span data-stu-id="84210-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="84210-160">toodelete uma tabela de rota</span><span class="sxs-lookup"><span data-stu-id="84210-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="84210-161">toolist uma tabela de rota</span><span class="sxs-lookup"><span data-stu-id="84210-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="84210-162">toodelete uma rota de uma tabela de rota</span><span class="sxs-lookup"><span data-stu-id="84210-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="84210-163">tooremove uma rota de sub-rede</span><span class="sxs-lookup"><span data-stu-id="84210-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="84210-164">tabela de rotas toolist Olá associada uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="84210-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="84210-165">tooremove um site predefinido de um gateway de VPN da VNet</span><span class="sxs-lookup"><span data-stu-id="84210-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```