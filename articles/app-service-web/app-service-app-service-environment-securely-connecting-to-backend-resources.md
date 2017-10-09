---
title: "aaaSecurely ligação tooBackEnd recursos a partir de um ambiente de serviço de aplicações"
description: "Saiba mais sobre como o toosecurely ligar toobackend recursos a partir de um ambiente de serviço de aplicações."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="7d0dd-103">Em segurança ligar tooBackend recursos a partir de um ambiente de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="7d0dd-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="7d0dd-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="7d0dd-104">Overview</span></span>
<span data-ttu-id="7d0dd-105">Uma vez que um ambiente de serviço de aplicações é sempre criado no **ou** uma rede virtual do Azure Resource Manager, **ou** um modelo de implementação clássica [rede virtual] [ virtualnetwork], ligações de saída a partir dos recursos de back-end de tooother ambiente de serviço de aplicações possam circular exclusivamente através de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="7d0dd-106">Com uma alteração recente efetuada em Junho de 2016, ASEs também podem ser implementados em redes virtuais que utilizam os intervalos de endereços público ou espaços de endereços RFC1918 (ou seja, endereços privados).</span><span class="sxs-lookup"><span data-stu-id="7d0dd-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="7d0dd-107">Por exemplo, poderá ser um SQL Server em execução num cluster de máquinas virtuais com a porta 1433 bloqueados.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="7d0dd-108">ponto final de Olá poderá ACLd tooonly permitir o acesso a partir de outros recursos em Olá a mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="7d0dd-109">Outro exemplo, pontos finais confidenciais podem executar no local e ser tooAzure ligado através de um [Site a Site] [ SiteToSite] ou [Azure ExpressRoute] [ ExpressRoute] ligações.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="7d0dd-110">Como resultado, apenas recursos nas redes virtuais ligadas toohello Site para Site ou ExpressRoute túneis serão pontos finais do tooaccess consegue no local.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="7d0dd-111">Para todos estes cenários, as aplicações em execução no ambiente de serviço de aplicações irá ser toosecurely capaz de ligar toohello vários servidores e recursos.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="7d0dd-112">Tráfego de saída de aplicações em execução num pontos finais tooprivate de ambiente de serviço de aplicações no Olá mesma rede virtual (ou ligado toohello mesma rede virtual), será apenas fluxo através de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="7d0dd-113">Pontos finais não irão fluir através de tooprivate de tráfego de saída Olá Internet pública.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="7d0dd-114">Uma advertência aplica-se a tráfego toooutbound de tooendpoints um ambiente de serviço de aplicações dentro de uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="7d0dd-115">Ambientes do App Service não é possível aceder a pontos finais de máquinas virtuais localizadas em Olá **mesmo** como Olá ambiente de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="7d0dd-116">Isto normalmente não deve ser um problema, desde que os ambientes de serviço de aplicações são implementados para uma sub-rede reservada para utilização exclusiva por Olá apenas ambiente de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="7d0dd-117">Conectividade de saída e os requisitos de DNS</span><span class="sxs-lookup"><span data-stu-id="7d0dd-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="7d0dd-118">Para um ambiente de serviço de aplicações toofunction corretamente, requer pontos finais de toovarious de acesso de saída.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="7d0dd-119">Uma lista completa das Olá pontos finais externos utilizados pelo ASE consta Olá secção "Necessárias conectividade de rede" Olá [configuração de rede para o ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artigo.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="7d0dd-120">Ambientes do App Service necessitam de uma infraestrutura de DNS válida configurada para a rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="7d0dd-121">Se para qualquer Olá razão a configuração de DNS é alterada depois de criar um ambiente de serviço de aplicações, os programadores de podem forçar toopick um ambiente de serviço de aplicações, a configuração de DNS novo Olá.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="7d0dd-122">Acionar um reinício de ambiente graduais com ícone de "Restart" Olá, localizado em Olá parte superior do ambiente de serviço de aplicações de Olá painel de gestão no portal de Olá fará com que Olá ambiente toopick a configuração de DNS novo Olá.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="7d0dd-123">Também é recomendável que todos os servidores DNS personalizados Olá vnet ser configurado antes da hora anterior toocreating um ambiente de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="7d0dd-124">Se a configuração de DNS de uma rede virtual é alterada durante a criação de um ambiente de serviço de aplicações, que resultará na falha de processo de criação de ambiente de serviço de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="7d0dd-125">Um vein semelhante, se existir um servidor DNS personalizado no Olá outra extremidade de um gateway de VPN e o servidor DNS Olá é Olá inacessível ou não está disponível, também irá falhar o processo de criação do ambiente de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="7d0dd-126">Ligar tooa do SQL Server</span><span class="sxs-lookup"><span data-stu-id="7d0dd-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="7d0dd-127">Uma configuração comum do SQL Server tem um ponto final à escuta na porta 1433:</span><span class="sxs-lookup"><span data-stu-id="7d0dd-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Ponto final do SQL Server][SqlServerEndpoint]

<span data-ttu-id="7d0dd-129">Existem duas abordagens para restringir o ponto final de toothis de tráfego:</span><span class="sxs-lookup"><span data-stu-id="7d0dd-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="7d0dd-130">[Listas de controlo de acesso de rede] [ NetworkAccessControlLists] (ACLs de rede)</span><span class="sxs-lookup"><span data-stu-id="7d0dd-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="7d0dd-131">[Grupos de segurança de rede][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="7d0dd-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="7d0dd-132">Restringir o acesso com uma ACL de rede</span><span class="sxs-lookup"><span data-stu-id="7d0dd-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="7d0dd-133">A porta 1433 pode ser protegida utilizando uma lista de controlo de acesso de rede.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="7d0dd-134">exemplo de Olá abaixo whitelists cliente endereços originadas a partir de dentro de uma rede virtual e bloquear o acesso tooall outros clientes.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![Exemplo de lista de controlo de acesso de rede][NetworkAccessControlListExample]

<span data-ttu-id="7d0dd-136">Olá, todas as aplicações em execução no ambiente de serviço de aplicações na mesma rede virtual como Olá do SQL Server será a instância do SQL Server toohello de tooconnect consegue utilizar Olá **VNet interno** endereço IP para a máquina de virtual Olá do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="7d0dd-137">cadeia de ligação de exemplo de Olá abaixo referências hello do SQL Server utilizando o respetivo endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="7d0dd-138">Embora a máquina virtual de Olá tem um ponto de final público bem, as tentativas de ligação com o endereço IP público Olá serão rejeitadas devido a rede de Olá ACL.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="7d0dd-139">Restringir o acesso a um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="7d0dd-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="7d0dd-140">É uma abordagem alternativa para proteger o acesso a um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="7d0dd-141">Grupos de segurança de rede podem ser aplicado tooindividual virtual machines ou sub-rede tooa que contêm máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="7d0dd-142">Primeiro um grupo de segurança de rede necessita de toobe criada:</span><span class="sxs-lookup"><span data-stu-id="7d0dd-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="7d0dd-143">Restringir o acesso tooonly tráfego interno de VNet é muito simple com um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="7d0dd-144">regras de predefinidas Olá num grupo de segurança de rede permitem apenas o acesso a partir de outros clientes de rede no Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="7d0dd-145">Como resultado bloquear acesso tooSQL servidor é tão simple como aplicar um grupo de segurança de rede com as predefinição regras tooeither Olá máquinas virtuais em execução do SQL Server, ou a sub-rede de Olá contendo máquinas de virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="7d0dd-146">exemplo de Olá abaixo aplica-se uma segurança grupo toohello contentora sub-rede da rede:</span><span class="sxs-lookup"><span data-stu-id="7d0dd-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="7d0dd-147">resultado final de Olá é um conjunto de regras de segurança que bloquear o acesso externo, ao permitir o acesso interno da VNet:</span><span class="sxs-lookup"><span data-stu-id="7d0dd-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Regras de segurança de rede predefinida][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="7d0dd-149">Introdução</span><span class="sxs-lookup"><span data-stu-id="7d0dd-149">Getting started</span></span>
<span data-ttu-id="7d0dd-150">Todos os artigos e como-a para ambientes de serviço de aplicações estão disponíveis no Olá [Leia-me para ambientes de serviço de aplicações](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="7d0dd-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="7d0dd-151">tooget começar a utilizar ambientes do App Service, consulte [introdução tooApp ambiente de serviço][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="7d0dd-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="7d0dd-152">Para obter mais detalhes em torno de controlar o tráfego de entrada tooyour ambiente de serviço de aplicações, consulte [controlar o tráfego de entrada tooan ambiente de serviço de aplicações][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="7d0dd-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="7d0dd-153">Para obter mais informações sobre a plataforma do App Service do Azure de Olá, consulte [App Service do Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="7d0dd-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
