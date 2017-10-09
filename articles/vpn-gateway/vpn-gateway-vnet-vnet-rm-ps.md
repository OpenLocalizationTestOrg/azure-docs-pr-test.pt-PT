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
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="dcbba-103">Configurar uma ligação de gateway de VPN de VNet a VNet com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcbba-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="dcbba-104">Este artigo mostra como toocreate uma ligação de gateway VPN entre redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="dcbba-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="dcbba-105">Olá redes virtuais podem estar em Olá regiões idêntica ou diferentes e de Olá mesmo ou subscrições diferentes.</span><span class="sxs-lookup"><span data-stu-id="dcbba-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="dcbba-106">Quando ao ligar VNets de diferentes subscrições, subscrições Olá não é necessário toobe associado Olá mesmo inquilino do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dcbba-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="dcbba-107">passos de Olá neste artigo aplicam-se modelo de implementação do Resource Manager toohello e utilizam o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcbba-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="dcbba-108">Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcbba-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dcbba-109">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dcbba-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="dcbba-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcbba-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="dcbba-111">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="dcbba-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="dcbba-112">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="dcbba-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="dcbba-113">Ligue diferentes modelos de implementação - portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dcbba-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="dcbba-114">Ligue diferentes modelos de implementação - PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcbba-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="dcbba-115">Ligar a rede virtual tooanother rede virtual (VNet a VNet) é semelhante tooconnecting uma localização de site do VNet tooan no local.</span><span class="sxs-lookup"><span data-stu-id="dcbba-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="dcbba-116">Ambos os tipos de conetividade utilizam um tooprovide de gateway VPN um túnel seguro através de IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="dcbba-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="dcbba-117">Se as suas VNets estiverem na Olá mesma região, poderá ser útil tooconsider ligá-las a utilização de VNet Peering.</span><span class="sxs-lookup"><span data-stu-id="dcbba-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="dcbba-118">O VNet peering não utiliza um gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="dcbba-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="dcbba-119">Para obter mais informações, veja [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dcbba-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="dcbba-120">A comunicação VNet a VNet pode ser combinada com configurações multilocal.</span><span class="sxs-lookup"><span data-stu-id="dcbba-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="dcbba-121">Isto permite-lhe estabelecer topologias de rede que combinam uma conectividade entre instalações com conectividade de rede intervirtual, como mostrado na Olá diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcbba-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Acerca das ligações](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="dcbba-123">Por que motivo ligar redes virtuais?</span><span class="sxs-lookup"><span data-stu-id="dcbba-123">Why connect virtual networks?</span></span>

<span data-ttu-id="dcbba-124">Poderá pretender redes virtuais tooconnect para Olá seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="dcbba-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="dcbba-125">**Geopresença e georredundância entre várias regiões**</span><span class="sxs-lookup"><span data-stu-id="dcbba-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="dcbba-126">Pode configurar a sua própria georreplicação ou sincronização com uma conetividade segura sem passar por pontos finais com acesso à Internet.</span><span class="sxs-lookup"><span data-stu-id="dcbba-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="dcbba-127">Com o Gestor de Tráfego e o Balanceador de Carga do Azure, pode configurar uma carga de trabalho de elevada disponibilidade com georredundância em várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbba-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="dcbba-128">Um exemplo importante consiste tooset cópias de segurança SQL Always On com grupos de disponibilidade propagando-se em várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbba-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="dcbba-129">**Aplicações multicamadas regionais com isolamento ou limites administrativos**</span><span class="sxs-lookup"><span data-stu-id="dcbba-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="dcbba-130">Olá da mesma região, pode configurar aplicações de várias camadas com várias redes virtuais ligadas em conjunto devido tooisolation ou a requisitos administrativos.</span><span class="sxs-lookup"><span data-stu-id="dcbba-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="dcbba-131">Para obter mais informações sobre ligações VNet a VNet, consulte Olá [FAQ de VNet a VNet](#faq) no fim de Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="dcbba-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="dcbba-132">Que conjunto de passos devo utilizar?</span><span class="sxs-lookup"><span data-stu-id="dcbba-132">Which set of steps should I use?</span></span>

<span data-ttu-id="dcbba-133">Neste artigo, verá dois conjuntos de passos diferentes.</span><span class="sxs-lookup"><span data-stu-id="dcbba-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="dcbba-134">Um conjunto de passos para [Olá de VNets que residem na mesma subscrição](#samesub)e outra para [VNets que residem em subscrições diferentes](#difsub).</span><span class="sxs-lookup"><span data-stu-id="dcbba-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="dcbba-135">Olá principal diferença entre conjuntos de Olá é se pode criar e configurar todos os gateway de rede e recursos virtuais no Olá mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcbba-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="dcbba-136">Olá passos neste artigo utilizam as variáveis que são declaradas no início de Olá de cada secção.</span><span class="sxs-lookup"><span data-stu-id="dcbba-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="dcbba-137">Se já estiver a trabalhar com as VNets existentes, modifique Olá variáveis tooreflect Olá as definições no seu próprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="dcbba-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="dcbba-138">Se pretender a resolução de nomes para as suas redes virtuais, veja [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Resolução de nomes).</span><span class="sxs-lookup"><span data-stu-id="dcbba-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="dcbba-139"><a name="samesub"></a>Como tooconnect VNets que estão em Olá mesma subscrição</span><span class="sxs-lookup"><span data-stu-id="dcbba-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![Diagrama v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="dcbba-141">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="dcbba-141">Before you begin</span></span>

<span data-ttu-id="dcbba-142">Antes de começar, terá de versão mais recente de Olá tooinstall Olá do Azure Resource Manager de cmdlets do PowerShell, pelo menos 4.0 ou posteriores.</span><span class="sxs-lookup"><span data-stu-id="dcbba-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="dcbba-143">Para obter mais informações sobre a instalação de cmdlets do PowerShell Olá, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcbba-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="dcbba-144"><a name="Step1"></a>Passo 1 - Planear os intervalos de endereços IP</span><span class="sxs-lookup"><span data-stu-id="dcbba-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="dcbba-145">Olá os passos seguintes, vamos criar duas redes virtuais juntamente com as respetivas sub-redes de gateway e configurações.</span><span class="sxs-lookup"><span data-stu-id="dcbba-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="dcbba-146">Em seguida, criamos uma ligação VPN entre Olá duas VNets.</span><span class="sxs-lookup"><span data-stu-id="dcbba-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="dcbba-147">É importante tooplan intervalos de endereços IP Olá para a sua configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="dcbba-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="dcbba-148">Nota: precisa confirmar que nenhum dos intervalos de VNet ou intervalos de rede local se sobrepõe de modo algum.</span><span class="sxs-lookup"><span data-stu-id="dcbba-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="dcbba-149">Nestes exemplos, não incluímos um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="dcbba-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="dcbba-150">Se pretender a resolução de nomes para as suas redes virtuais, veja [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Resolução de nomes).</span><span class="sxs-lookup"><span data-stu-id="dcbba-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="dcbba-151">Podemos utilizar Olá valores nos exemplos de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="dcbba-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="dcbba-152">**Valores da TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="dcbba-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="dcbba-153">Nome da VNet: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="dcbba-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="dcbba-154">Grupo de Recursos: TestRG1</span><span class="sxs-lookup"><span data-stu-id="dcbba-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="dcbba-155">Localização: EUA Leste</span><span class="sxs-lookup"><span data-stu-id="dcbba-155">Location: East US</span></span>
* <span data-ttu-id="dcbba-156">TestVNet1: 10.11.0.0/16 e 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="dcbba-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="dcbba-157">Front-End: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="dcbba-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="dcbba-158">Back-End: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="dcbba-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="dcbba-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="dcbba-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="dcbba-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="dcbba-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="dcbba-161">IP Público: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="dcbba-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="dcbba-162">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="dcbba-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="dcbba-163">Ligação (1 a 4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="dcbba-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="dcbba-164">Ligação (1 a 5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="dcbba-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="dcbba-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="dcbba-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="dcbba-166">**Valores da TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="dcbba-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="dcbba-167">Nome da VNet: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="dcbba-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="dcbba-168">TestVNet2: 10.41.0.0/16 e 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="dcbba-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="dcbba-169">Front-End: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="dcbba-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="dcbba-170">Back-End: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="dcbba-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="dcbba-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="dcbba-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="dcbba-172">Grupo de Recursos: TestRG4</span><span class="sxs-lookup"><span data-stu-id="dcbba-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="dcbba-173">Localização: EUA Oeste</span><span class="sxs-lookup"><span data-stu-id="dcbba-173">Location: West US</span></span>
* <span data-ttu-id="dcbba-174">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="dcbba-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="dcbba-175">IP Público: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="dcbba-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="dcbba-176">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="dcbba-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="dcbba-177">Ligação: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="dcbba-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="dcbba-178">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="dcbba-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="dcbba-179"><a name="Step2"></a>Passo 2 - Criar e configurar a TestVNet1</span><span class="sxs-lookup"><span data-stu-id="dcbba-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="dcbba-180">Declarar as variáveis.</span><span class="sxs-lookup"><span data-stu-id="dcbba-180">Declare your variables.</span></span> <span data-ttu-id="dcbba-181">Neste exemplo declara as variáveis de Olá utilizando valores de Olá para este exercício.</span><span class="sxs-lookup"><span data-stu-id="dcbba-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="dcbba-182">Na maioria dos casos, deve substituir os valores de Olá com os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="dcbba-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="dcbba-183">No entanto, pode utilizar estas variáveis se estiver a executar através de Olá passos toobecome familiarizado com este tipo de configuração.</span><span class="sxs-lookup"><span data-stu-id="dcbba-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="dcbba-184">Modificar variáveis de Olá, se necessário, em seguida, copie e cole-os para a consola do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcbba-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

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

2. <span data-ttu-id="dcbba-185">Ligar a tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="dcbba-185">Connect tooyour account.</span></span> <span data-ttu-id="dcbba-186">Utilize Olá toohelp de exemplo, ligar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="dcbba-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="dcbba-187">Verifique Olá subscrições para a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="dcbba-188">Especifique que pretende que o toouse de subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="dcbba-189">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dcbba-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="dcbba-190">Crie Olá configurações de sub-rede da TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="dcbba-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="dcbba-191">Este exemplo cria uma rede virtual com o nome TestVNet1 e três sub-redes, uma chamada GatewaySubnet, outra FrontEnd e a última BackEnd.</span><span class="sxs-lookup"><span data-stu-id="dcbba-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="dcbba-192">Quando estiver a substituir os valores, é importante que dê sempre à sub-rede do gateway o nome específico GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="dcbba-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="dcbba-193">Se der outro nome, a criação da gateway falha.</span><span class="sxs-lookup"><span data-stu-id="dcbba-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="dcbba-194">Olá exemplo seguinte utiliza variáveis de Olá que configurou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dcbba-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="dcbba-195">Neste exemplo, a sub-rede do gateway Olá é utilizar/27.</span><span class="sxs-lookup"><span data-stu-id="dcbba-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="dcbba-196">Embora seja possível toocreate uma sub-rede do gateway tão pequena como/29, recomendamos que crie uma sub-rede maior que inclua endereços mais ao selecionar, pelo menos, / 28 ou /27.</span><span class="sxs-lookup"><span data-stu-id="dcbba-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="dcbba-197">Isto permitirá para suficiente endereços tooaccommodate possíveis configurações adicionais que poderá ser útil no Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="dcbba-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="dcbba-198">Criar a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="dcbba-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="dcbba-199">Pedir um público IP endereço toobe toohello alocado gateway que será criado para a sua VNet.</span><span class="sxs-lookup"><span data-stu-id="dcbba-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="dcbba-200">Repare que Olá AllocationMethod é dinâmico.</span><span class="sxs-lookup"><span data-stu-id="dcbba-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="dcbba-201">Não é possível especificar o endereço IP Olá que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="dcbba-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="dcbba-202">É gateway tooyour alocada dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="dcbba-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="dcbba-203">Crie a configuração do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-203">Create hello gateway configuration.</span></span> <span data-ttu-id="dcbba-204">configuração do gateway de Olá define uma sub-rede de Olá e Olá toouse de endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="dcbba-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="dcbba-205">Utilize toocreate de exemplo de Olá a configuração do gateway.</span><span class="sxs-lookup"><span data-stu-id="dcbba-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="dcbba-206">Crie gateway de Olá da TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="dcbba-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="dcbba-207">Neste passo, vai criar gateway de rede virtual Olá para a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="dcbba-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="dcbba-208">As configurações VNet a VNet requerem um VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="dcbba-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="dcbba-209">Criar um gateway, muitas vezes, pode demorar 45 minutos ou mais, dependendo do SKU de gateway selecionado Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="dcbba-210">Passo 3 – Criar e configurar a TestVNet4</span><span class="sxs-lookup"><span data-stu-id="dcbba-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="dcbba-211">Assim que tiver configurado a TestVNet1, crie a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="dcbba-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="dcbba-212">Siga os passos de Olá abaixo, substituindo os valores de Olá com os seus próprios quando necessário.</span><span class="sxs-lookup"><span data-stu-id="dcbba-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="dcbba-213">Este passo pode ser feito na Olá mesma sessão do PowerShell porque está a ser Olá mesma subscrição.</span><span class="sxs-lookup"><span data-stu-id="dcbba-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="dcbba-214">Declarar as variáveis.</span><span class="sxs-lookup"><span data-stu-id="dcbba-214">Declare your variables.</span></span> <span data-ttu-id="dcbba-215">Ser tooreplace se valores Olá com Olá aqueles que pretende que toouse para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="dcbba-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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
2. <span data-ttu-id="dcbba-216">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dcbba-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="dcbba-217">Crie Olá configurações de sub-rede da TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="dcbba-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="dcbba-218">Criar a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="dcbba-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="dcbba-219">Solicitar um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="dcbba-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="dcbba-220">Crie a configuração do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="dcbba-221">Crie Olá TestVNet4 gateway.</span><span class="sxs-lookup"><span data-stu-id="dcbba-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="dcbba-222">Criar um gateway, muitas vezes, pode demorar 45 minutos ou mais, dependendo do SKU de gateway selecionado Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="dcbba-223">Passo 4 – criar ligações Olá</span><span class="sxs-lookup"><span data-stu-id="dcbba-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="dcbba-224">Obter os gateways da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="dcbba-224">Get both virtual network gateways.</span></span> <span data-ttu-id="dcbba-225">Se ambas as gateways de Olá no Olá mesma subscrição, conforme forem no exemplo de Olá, pode concluir este passo na Olá mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcbba-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="dcbba-226">Crie Olá TestVNet1 tooTestVNet4 ligação.</span><span class="sxs-lookup"><span data-stu-id="dcbba-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="dcbba-227">Neste passo, criará Olá ligação da TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="dcbba-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="dcbba-228">Verá uma chave partilhada referenciada nos exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="dcbba-229">Pode utilizar os seus próprios valores para a chave partilhada Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="dcbba-230">Olá coisa que essa chave partilhada Olá, é importante tem de corresponder ao ambas as ligações.</span><span class="sxs-lookup"><span data-stu-id="dcbba-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="dcbba-231">Criar uma ligação pode demorar uns toocomplete breves instantes.</span><span class="sxs-lookup"><span data-stu-id="dcbba-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="dcbba-232">Crie Olá TestVNet4 tooTestVNet1 ligação.</span><span class="sxs-lookup"><span data-stu-id="dcbba-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="dcbba-233">Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="dcbba-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="dcbba-234">Certifique-se de chaves de Olá partilhada correspondem.</span><span class="sxs-lookup"><span data-stu-id="dcbba-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="dcbba-235">será possível estabelecer a ligação de Olá após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="dcbba-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="dcbba-236">Verifique a ligação.</span><span class="sxs-lookup"><span data-stu-id="dcbba-236">Verify your connection.</span></span> <span data-ttu-id="dcbba-237">Consulte a secção de Olá [como tooverify a ligação](#verify).</span><span class="sxs-lookup"><span data-stu-id="dcbba-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="dcbba-238"><a name="difsub"></a>Como tooconnect VNets que estão em subscrições diferentes</span><span class="sxs-lookup"><span data-stu-id="dcbba-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![Diagrama v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="dcbba-240">Neste cenário, vamos ligar TestVNet1 e TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="dcbba-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="dcbba-241">TestVNet1 e TestVNet5 residem em subscrições diferentes.</span><span class="sxs-lookup"><span data-stu-id="dcbba-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="dcbba-242">subscrições de Olá não é necessário toobe associado Olá mesmo inquilino do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dcbba-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="dcbba-243">diferença Olá entre estes passos e o conjunto anterior Olá é que alguns dos passos de configuração de Olá necessitam toobe efetuada numa sessão separada do PowerShell no contexto de Olá da subscrição segundo Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="dcbba-244">Especialmente quando Olá duas subscrições pertencem toodifferent organizações.</span><span class="sxs-lookup"><span data-stu-id="dcbba-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="dcbba-245">Passo 5 - Criar e configurar a TestVNet1</span><span class="sxs-lookup"><span data-stu-id="dcbba-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="dcbba-246">Tem de concluir [passo 1](#Step1) e [passo 2](#Step2) de Olá anterior secção toocreate e configurar a TestVNet1 e hello do VPN Gateway da TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="dcbba-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="dcbba-247">Para esta configuração, não são necessária toocreate TestVNet4 da secção anterior Olá, embora se criá-la, este será não entrar em conflito com estes passos.</span><span class="sxs-lookup"><span data-stu-id="dcbba-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="dcbba-248">Depois de concluir o passo 1 e o passo 2, prosseguir para o passo 6 toocreate TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="dcbba-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="dcbba-249">Passo 6 – Certifique-se de intervalos de endereços IP Olá</span><span class="sxs-lookup"><span data-stu-id="dcbba-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="dcbba-250">É importante toomake certificar-se de que espaço de endereços IP Olá de Olá nova rede virtual, TestVNet5, não se sobreponha a nenhum dos intervalos de Vnets ou intervalos de gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="dcbba-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="dcbba-251">Neste exemplo, redes virtuais Olá poderão pertencer toodifferent organizações.</span><span class="sxs-lookup"><span data-stu-id="dcbba-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="dcbba-252">Para este exercício, pode utilizar Olá os seguintes valores para Olá TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="dcbba-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="dcbba-253">**Valores da TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="dcbba-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="dcbba-254">Nome da VNet: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="dcbba-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="dcbba-255">Grupo de Recursos: TestRG5</span><span class="sxs-lookup"><span data-stu-id="dcbba-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="dcbba-256">Localização: Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="dcbba-256">Location: Japan East</span></span>
* <span data-ttu-id="dcbba-257">TestVNet5: 10.51.0.0/16 e 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="dcbba-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="dcbba-258">Front-End: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="dcbba-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="dcbba-259">Back-End: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="dcbba-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="dcbba-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="dcbba-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="dcbba-261">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="dcbba-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="dcbba-262">IP Público: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="dcbba-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="dcbba-263">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="dcbba-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="dcbba-264">Ligação: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="dcbba-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="dcbba-265">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="dcbba-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="dcbba-266">Passo 7 – Criar e configurar a TestVNet5</span><span class="sxs-lookup"><span data-stu-id="dcbba-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="dcbba-267">Este passo tem de ser efetuado no contexto de Olá da nova subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="dcbba-268">Esta parte pode ser realizada pelo administrador de Olá numa organização diferente proprietária da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="dcbba-269">Declarar as variáveis.</span><span class="sxs-lookup"><span data-stu-id="dcbba-269">Declare your variables.</span></span> <span data-ttu-id="dcbba-270">Ser tooreplace se valores Olá com Olá aqueles que pretende que toouse para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="dcbba-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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
2. <span data-ttu-id="dcbba-271">Ligar toosubscription 5.</span><span class="sxs-lookup"><span data-stu-id="dcbba-271">Connect toosubscription 5.</span></span> <span data-ttu-id="dcbba-272">Abra a consola do PowerShell e ligue tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="dcbba-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="dcbba-273">Utilize Olá toohelp de exemplo, ligar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="dcbba-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="dcbba-274">Verifique Olá subscrições para a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="dcbba-275">Especifique que pretende que o toouse de subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="dcbba-276">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dcbba-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="dcbba-277">Crie Olá configurações de sub-rede para a TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="dcbba-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="dcbba-278">Criar a TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="dcbba-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="dcbba-279">Solicitar um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="dcbba-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="dcbba-280">Crie a configuração do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="dcbba-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="dcbba-281">Crie Olá TestVNet5 gateway.</span><span class="sxs-lookup"><span data-stu-id="dcbba-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="dcbba-282">Passo 8 - criar ligações Olá</span><span class="sxs-lookup"><span data-stu-id="dcbba-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="dcbba-283">Neste exemplo, porque os gateways de Olá estão em subscrições diferentes Olá, iremos tiver dividir este passo em duas sessões do PowerShell marcadas como [subscrição 1] e [subscrição 5].</span><span class="sxs-lookup"><span data-stu-id="dcbba-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="dcbba-284">**[Subscrição 1]**  Gateway de rede virtual Olá get da subscrição 1.</span><span class="sxs-lookup"><span data-stu-id="dcbba-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="dcbba-285">Iniciar sessão e ligar tooSubscription 1 antes de executar o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="dcbba-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="dcbba-286">Copiar resultado Olá Olá seguintes elementos e envie estes administrador toohello da subscrição 5 por e-mail ou outro método.</span><span class="sxs-lookup"><span data-stu-id="dcbba-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="dcbba-287">Estes dois elementos terão valores toohello semelhante, saída de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcbba-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="dcbba-288">**[Subscrição 5]**  Gateway de rede virtual Olá get da subscrição 5.</span><span class="sxs-lookup"><span data-stu-id="dcbba-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="dcbba-289">Iniciar sessão e ligar tooSubscription 5 antes de executar o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="dcbba-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="dcbba-290">Copiar resultado Olá Olá seguintes elementos e envie estes administrador toohello da subscrição 1 por e-mail ou outro método.</span><span class="sxs-lookup"><span data-stu-id="dcbba-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="dcbba-291">Estes dois elementos terão valores toohello semelhante, saída de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcbba-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="dcbba-292">**[Subscrição 1]**  Criar ligação Olá TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="dcbba-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="dcbba-293">Neste passo, criará Olá ligação da TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="dcbba-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="dcbba-294">diferença de Olá aqui é que $vnet5gw não pode ser obtido diretamente porque está numa subscrição diferente.</span><span class="sxs-lookup"><span data-stu-id="dcbba-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="dcbba-295">Precisa de toocreate um novo objeto do PowerShell com valores de Olá comunicados da subscrição 1 nos passos Olá acima.</span><span class="sxs-lookup"><span data-stu-id="dcbba-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="dcbba-296">Utilize o exemplo de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="dcbba-296">Use hello example below.</span></span> <span data-ttu-id="dcbba-297">Substitua os seus próprios valores Olá nome, a Id e a chave partilhada.</span><span class="sxs-lookup"><span data-stu-id="dcbba-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="dcbba-298">Olá coisa que essa chave partilhada Olá, é importante tem de corresponder ao ambas as ligações.</span><span class="sxs-lookup"><span data-stu-id="dcbba-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="dcbba-299">Criar uma ligação pode demorar uns toocomplete breves instantes.</span><span class="sxs-lookup"><span data-stu-id="dcbba-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="dcbba-300">Ligar tooSubscription 1 antes de executar o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="dcbba-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="dcbba-301">**[Subscrição 5]**  Criar ligação Olá TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="dcbba-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="dcbba-302">Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="dcbba-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="dcbba-303">Olá mesmo processo de criação de um objeto do PowerShell com base nos valores de Olá obtidos na subscrição 1 aplica-se aqui bem.</span><span class="sxs-lookup"><span data-stu-id="dcbba-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="dcbba-304">Neste passo, lembre-se de que as chaves de Olá partilhada correspondem.</span><span class="sxs-lookup"><span data-stu-id="dcbba-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="dcbba-305">Ligar tooSubscription 5 antes de executar o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="dcbba-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="dcbba-306"><a name="verify"></a>Como tooverify uma ligação</span><span class="sxs-lookup"><span data-stu-id="dcbba-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="dcbba-307"><a name="faq"></a>FAQ da ligação VNet a VNet</span><span class="sxs-lookup"><span data-stu-id="dcbba-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="dcbba-308">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dcbba-308">Next steps</span></span>

* <span data-ttu-id="dcbba-309">Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="dcbba-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="dcbba-310">Consulte Olá [documentação de Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="dcbba-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="dcbba-311">Para informações sobre o BGP, consulte Olá [descrição geral do BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="dcbba-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
