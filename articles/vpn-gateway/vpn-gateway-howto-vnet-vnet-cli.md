---
title: 'Ligar a rede virtual tooanother VNet: CLI do Azure | Microsoft Docs'
description: "Este artigo explica como ligar redes virtuais entre si através do Azure Resource Manager e da CLI do Azure."
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
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="d99e3-103">Configurar uma ligação de gateway de VPN de VNet a VNet com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d99e3-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="d99e3-104">Este artigo mostra como toocreate uma ligação de gateway VPN entre redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="d99e3-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="d99e3-105">Olá redes virtuais podem estar em Olá regiões idêntica ou diferentes e de Olá mesmo ou subscrições diferentes.</span><span class="sxs-lookup"><span data-stu-id="d99e3-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="d99e3-106">Quando ao ligar VNets de diferentes subscrições, subscrições Olá não é necessário toobe associado Olá mesmo inquilino do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d99e3-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="d99e3-107">passos de Olá neste artigo aplicam-se modelo de implementação do Resource Manager toohello e utilizam a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d99e3-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="d99e3-108">Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="d99e3-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d99e3-109">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d99e3-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="d99e3-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d99e3-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="d99e3-111">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d99e3-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="d99e3-112">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="d99e3-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="d99e3-113">Ligue diferentes modelos de implementação - portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d99e3-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="d99e3-114">Ligue diferentes modelos de implementação - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d99e3-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="d99e3-115">Ligar a rede virtual tooanother rede virtual (VNet a VNet) é semelhante tooconnecting uma localização de site do VNet tooan no local.</span><span class="sxs-lookup"><span data-stu-id="d99e3-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="d99e3-116">Ambos os tipos de conetividade utilizam um tooprovide de gateway VPN um túnel seguro através de IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="d99e3-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="d99e3-117">Se as suas VNets estiverem na Olá mesma região, poderá ser útil tooconsider ligá-las a utilização de VNet Peering.</span><span class="sxs-lookup"><span data-stu-id="d99e3-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="d99e3-118">O VNet peering não utiliza um gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="d99e3-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="d99e3-119">Para obter mais informações, veja [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d99e3-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="d99e3-120">A comunicação VNet a VNet pode ser combinada com configurações multilocal.</span><span class="sxs-lookup"><span data-stu-id="d99e3-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="d99e3-121">Isto permite-lhe estabelecer topologias de rede que combinam uma conectividade entre instalações com conectividade de rede intervirtual, como mostrado na Olá diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="d99e3-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Acerca das ligações](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="d99e3-123"><a name="why"></a>Por que motivo ligar redes virtuais?</span><span class="sxs-lookup"><span data-stu-id="d99e3-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="d99e3-124">Poderá pretender redes virtuais tooconnect para Olá seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="d99e3-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="d99e3-125">**Geopresença e georredundância entre várias regiões**</span><span class="sxs-lookup"><span data-stu-id="d99e3-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="d99e3-126">Pode configurar a sua própria georreplicação ou sincronização com uma conetividade segura sem passar por pontos finais com acesso à Internet.</span><span class="sxs-lookup"><span data-stu-id="d99e3-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="d99e3-127">Com o Gestor de Tráfego e o Balanceador de Carga do Azure, pode configurar uma carga de trabalho de elevada disponibilidade com georredundância em várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="d99e3-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="d99e3-128">Um exemplo importante consiste tooset cópias de segurança SQL Always On com grupos de disponibilidade propagando-se em várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="d99e3-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="d99e3-129">**Aplicações multicamadas regionais com isolamento ou limites administrativos**</span><span class="sxs-lookup"><span data-stu-id="d99e3-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="d99e3-130">Olá da mesma região, pode configurar aplicações de várias camadas com várias redes virtuais ligadas em conjunto devido tooisolation ou a requisitos administrativos.</span><span class="sxs-lookup"><span data-stu-id="d99e3-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="d99e3-131">Para obter mais informações sobre ligações VNet a VNet, consulte Olá [FAQ de VNet a VNet](#faq) no fim de Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="d99e3-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="d99e3-132">Que conjunto de passos devo utilizar?</span><span class="sxs-lookup"><span data-stu-id="d99e3-132">Which set of steps should I use?</span></span>

<span data-ttu-id="d99e3-133">Neste artigo, verá dois conjuntos de passos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d99e3-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="d99e3-134">Um conjunto de passos para [Olá de VNets que residem na mesma subscrição](#samesub)e outra para [VNets que residem em subscrições diferentes](#difsub).</span><span class="sxs-lookup"><span data-stu-id="d99e3-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="d99e3-135"><a name="samesub"></a>Ligar VNets que estão no Olá mesma subscrição</span><span class="sxs-lookup"><span data-stu-id="d99e3-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![Diagrama v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="d99e3-137">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d99e3-137">Before you begin</span></span>

<span data-ttu-id="d99e3-138">Antes de começar, instale a versão mais recente do Olá dos comandos da CLI Olá (2.0 ou posteriores).</span><span class="sxs-lookup"><span data-stu-id="d99e3-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="d99e3-139">Para obter informações sobre a instalação de comandos da CLI Olá, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d99e3-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="d99e3-140"><a name="Plan"></a>Planear os intervalos de endereços IP</span><span class="sxs-lookup"><span data-stu-id="d99e3-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="d99e3-141">Olá os passos seguintes, vamos criar duas redes virtuais juntamente com as respetivas sub-redes de gateway e configurações.</span><span class="sxs-lookup"><span data-stu-id="d99e3-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="d99e3-142">Em seguida, criamos uma ligação VPN entre Olá duas VNets.</span><span class="sxs-lookup"><span data-stu-id="d99e3-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="d99e3-143">É importante tooplan intervalos de endereços IP Olá para a sua configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="d99e3-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="d99e3-144">Nota: precisa confirmar que nenhum dos intervalos de VNet ou intervalos de rede local se sobrepõe de modo algum.</span><span class="sxs-lookup"><span data-stu-id="d99e3-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="d99e3-145">Nestes exemplos, não incluímos um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="d99e3-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="d99e3-146">Se pretender a resolução de nomes para as suas redes virtuais, veja [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Resolução de nomes).</span><span class="sxs-lookup"><span data-stu-id="d99e3-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="d99e3-147">Podemos utilizar Olá valores nos exemplos de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d99e3-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="d99e3-148">**Valores da TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="d99e3-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="d99e3-149">Nome da VNet: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d99e3-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="d99e3-150">Grupo de Recursos: TestRG1</span><span class="sxs-lookup"><span data-stu-id="d99e3-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="d99e3-151">Localização: EUA Leste</span><span class="sxs-lookup"><span data-stu-id="d99e3-151">Location: East US</span></span>
* <span data-ttu-id="d99e3-152">TestVNet1: 10.11.0.0/16 e 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d99e3-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="d99e3-153">Front-End: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d99e3-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="d99e3-154">Back-End: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d99e3-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="d99e3-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="d99e3-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="d99e3-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="d99e3-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="d99e3-157">IP Público: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="d99e3-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="d99e3-158">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="d99e3-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="d99e3-159">Ligação (1 a 4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="d99e3-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="d99e3-160">Ligação (1 a 5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="d99e3-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="d99e3-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="d99e3-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="d99e3-162">**Valores da TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="d99e3-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="d99e3-163">Nome da VNet: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="d99e3-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="d99e3-164">TestVNet2: 10.41.0.0/16 e 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d99e3-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="d99e3-165">Front-End: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d99e3-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="d99e3-166">Back-End: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d99e3-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="d99e3-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="d99e3-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="d99e3-168">Grupo de Recursos: TestRG4</span><span class="sxs-lookup"><span data-stu-id="d99e3-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="d99e3-169">Localização: EUA Oeste</span><span class="sxs-lookup"><span data-stu-id="d99e3-169">Location: West US</span></span>
* <span data-ttu-id="d99e3-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="d99e3-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="d99e3-171">IP Público: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="d99e3-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="d99e3-172">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="d99e3-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="d99e3-173">Ligação: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="d99e3-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="d99e3-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="d99e3-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="d99e3-175"><a name="Connect"></a>Passo 1 – ligar tooyour subscrição</span><span class="sxs-lookup"><span data-stu-id="d99e3-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="d99e3-176"><a name="TestVNet1"></a>Passo 2 - Criar e configurar a TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d99e3-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="d99e3-177">Crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d99e3-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="d99e3-178">Crie a TestVNet1 e Olá sub-redes da TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d99e3-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="d99e3-179">Este exemplo cria uma rede virtual com o nome TestVNet1 e uma sub-rede, com o nome FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="d99e3-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="d99e3-180">Crie um espaço de endereços adicionais para a sub-rede de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="d99e3-181">Tenha em atenção que neste passo, vamos especificar ambos os espaços de endereços de Olá criamos anteriormente e Olá espaço de endereços adicionais que queremos tooadd.</span><span class="sxs-lookup"><span data-stu-id="d99e3-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="d99e3-182">Isto acontece porque Olá [atualização de vnet az rede](https://docs.microsoft.com/cli/azure/network/vnet#update) comando substitui definições anteriores Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="d99e3-183">Certifique-se toospecify todos os prefixos de endereço Olá quando utilizar este comando.</span><span class="sxs-lookup"><span data-stu-id="d99e3-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="d99e3-184">Crie a sub-rede de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="d99e3-185">Crie a sub-rede do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-185">Create hello gateway subnet.</span></span> <span data-ttu-id="d99e3-186">Tenha em atenção de que essa sub-rede de gateway Olá com o nome "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="d99e3-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="d99e3-187">Este nome é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d99e3-187">This name is required.</span></span> <span data-ttu-id="d99e3-188">Neste exemplo, a sub-rede do gateway Olá é utilizar/27.</span><span class="sxs-lookup"><span data-stu-id="d99e3-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="d99e3-189">Embora seja possível toocreate uma sub-rede do gateway tão pequena como/29, recomendamos que crie uma sub-rede maior que inclua endereços mais ao selecionar, pelo menos, / 28 ou /27.</span><span class="sxs-lookup"><span data-stu-id="d99e3-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="d99e3-190">Isto permitirá para suficiente endereços tooaccommodate possíveis configurações adicionais que poderá ser útil no Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="d99e3-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="d99e3-191">Pedir um público IP endereço toobe toohello alocado gateway que será criado para a sua VNet.</span><span class="sxs-lookup"><span data-stu-id="d99e3-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="d99e3-192">Repare que Olá AllocationMethod é dinâmico.</span><span class="sxs-lookup"><span data-stu-id="d99e3-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="d99e3-193">Não é possível especificar o endereço IP Olá que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="d99e3-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="d99e3-194">É gateway tooyour alocada dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="d99e3-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="d99e3-195">Crie gateway de rede virtual Olá da TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d99e3-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="d99e3-196">As configurações VNet a VNet requerem um VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="d99e3-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="d99e3-197">Se executar este comando utilizando Olá parâmetro '- sem - espera', não vir quaisquer comentários ou saída.</span><span class="sxs-lookup"><span data-stu-id="d99e3-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="d99e3-198">Olá '- sem - espera' parâmetro permite que Olá gateway toocreate em segundo plano de Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="d99e3-199">Não significa desse gateway VPN Olá acaba de criar de imediato.</span><span class="sxs-lookup"><span data-stu-id="d99e3-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="d99e3-200">Criar um gateway, muitas vezes, pode demorar 45 minutos ou mais, dependendo Olá SKU de gateway que utilizar.</span><span class="sxs-lookup"><span data-stu-id="d99e3-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="d99e3-201"><a name="TestVNet4"></a>Passo 3 – Criar e configurar TestVNet4</span><span class="sxs-lookup"><span data-stu-id="d99e3-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="d99e3-202">Crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d99e3-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="d99e3-203">Criar a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d99e3-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="d99e3-204">Crie sub-redes adicionais para TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d99e3-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="d99e3-205">Crie a sub-rede do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="d99e3-206">Peça um Endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="d99e3-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="d99e3-207">Crie gateway de rede virtual Olá TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d99e3-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="d99e3-208"><a name="createconnect"></a>Passo 4 – criar ligações Olá</span><span class="sxs-lookup"><span data-stu-id="d99e3-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="d99e3-209">Agora, tem duas VNets com gateways de VPN.</span><span class="sxs-lookup"><span data-stu-id="d99e3-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="d99e3-210">Olá passo seguinte consiste em ligações de gateway VPN toocreate entre os gateways de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="d99e3-211">Se utilizou exemplos Olá acima, os gateways de VNet estão em grupos de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="d99e3-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="d99e3-212">Quando gateways estão em grupos de recursos diferente, tem de tooidentify e especifique os IDs de recurso Olá para cada gateway quando efetuar uma nova ligação.</span><span class="sxs-lookup"><span data-stu-id="d99e3-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="d99e3-213">Se as suas VNets estiverem na Olá mesmo grupo de recursos, pode utilizar Olá [segundo conjunto de instruções](#samerg) porque não precisa de IDs de recurso de Olá toospecify.</span><span class="sxs-lookup"><span data-stu-id="d99e3-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="d99e3-214"><a name="diffrg"></a>tooconnect VNets que residem nos grupos de recursos diferente</span><span class="sxs-lookup"><span data-stu-id="d99e3-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="d99e3-215">Obter Olá ID de recurso dos VNet1GW do resultado Olá Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d99e3-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="d99e3-216">No resultado de Olá, determinar Olá "id:" linha.</span><span class="sxs-lookup"><span data-stu-id="d99e3-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="d99e3-217">os valores de Olá nos aspas Olá são toocreate necessários Olá ligação na secção seguinte, Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="d99e3-218">Copie o editor de texto de tooa estes valores, como o Notepad, para que pode facilmente cole-os ao criar a ligação.</span><span class="sxs-lookup"><span data-stu-id="d99e3-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="d99e3-219">Exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="d99e3-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="d99e3-220">Copie os valores de Olá após **"id":** dentro de aspas Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="d99e3-221">Obter Olá ID de recurso dos VNet4GW e copie Olá valores tooa editor de texto.</span><span class="sxs-lookup"><span data-stu-id="d99e3-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="d99e3-222">Crie Olá TestVNet1 tooTestVNet4 ligação.</span><span class="sxs-lookup"><span data-stu-id="d99e3-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="d99e3-223">Neste passo, criará Olá ligação da TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d99e3-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="d99e3-224">Há uma chave partilhada referenciada nos exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="d99e3-225">Pode utilizar os seus próprios valores para a chave partilhada Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="d99e3-226">Olá coisa que essa chave partilhada Olá, é importante tem de corresponder ao ambas as ligações.</span><span class="sxs-lookup"><span data-stu-id="d99e3-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="d99e3-227">Criar uma ligação demora uns toocomplete breves instantes.</span><span class="sxs-lookup"><span data-stu-id="d99e3-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="d99e3-228">Crie Olá TestVNet4 tooTestVNet1 ligação.</span><span class="sxs-lookup"><span data-stu-id="d99e3-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="d99e3-229">Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d99e3-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="d99e3-230">Certifique-se de chaves de Olá partilhada correspondem.</span><span class="sxs-lookup"><span data-stu-id="d99e3-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="d99e3-231">Demora alguns minutos ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="d99e3-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="d99e3-232">Verifique as suas ligações.</span><span class="sxs-lookup"><span data-stu-id="d99e3-232">Verify your connections.</span></span> <span data-ttu-id="d99e3-233">Veja [Verificar a ligação](#verify).</span><span class="sxs-lookup"><span data-stu-id="d99e3-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="d99e3-234"><a name="samerg"></a>tooconnect VNets que residem no Olá mesmo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d99e3-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="d99e3-235">Crie Olá TestVNet1 tooTestVNet4 ligação.</span><span class="sxs-lookup"><span data-stu-id="d99e3-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="d99e3-236">Neste passo, criará Olá ligação da TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d99e3-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="d99e3-237">Grupos de recursos do aviso Olá são Olá mesmo nos exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="d99e3-238">Pode também ver uma chave partilhada referenciada nos exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="d99e3-239">Pode utilizar os seus próprios valores para a chave partilhada Olá, no entanto, tem de corresponder chave partilhada Olá ambas as ligações.</span><span class="sxs-lookup"><span data-stu-id="d99e3-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="d99e3-240">Criar uma ligação demora uns toocomplete breves instantes.</span><span class="sxs-lookup"><span data-stu-id="d99e3-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="d99e3-241">Crie Olá TestVNet4 tooTestVNet1 ligação.</span><span class="sxs-lookup"><span data-stu-id="d99e3-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="d99e3-242">Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d99e3-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="d99e3-243">Certifique-se de chaves de Olá partilhada correspondem.</span><span class="sxs-lookup"><span data-stu-id="d99e3-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="d99e3-244">Demora alguns minutos ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="d99e3-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="d99e3-245">Verifique as suas ligações.</span><span class="sxs-lookup"><span data-stu-id="d99e3-245">Verify your connections.</span></span> <span data-ttu-id="d99e3-246">Veja [Verificar a ligação](#verify).</span><span class="sxs-lookup"><span data-stu-id="d99e3-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="d99e3-247"><a name="difsub"></a>Ligar VNets que estão em subscrições diferentes</span><span class="sxs-lookup"><span data-stu-id="d99e3-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![Diagrama v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="d99e3-249">Neste cenário, vamos ligar TestVNet1 e TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d99e3-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="d99e3-250">Olá VNets residirem subscrições diferentes.</span><span class="sxs-lookup"><span data-stu-id="d99e3-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="d99e3-251">subscrições de Olá não é necessário toobe associado Olá mesmo inquilino do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d99e3-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="d99e3-252">Olá os passos para esta configuração de adicionar uma ligação VNet a VNet adicional na ordem tooconnect TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d99e3-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="d99e3-253"><a name="TestVNet1diff"></a>Passo 5 - Criar e configurar TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d99e3-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="d99e3-254">Estas instruções continuam dos passos de Olá no Olá precedente secções.</span><span class="sxs-lookup"><span data-stu-id="d99e3-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="d99e3-255">Tem de concluir [passo 1](#Connect) e [passo 2](#TestVNet1) toocreate e configurar a TestVNet1 e hello do VPN Gateway da TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d99e3-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="d99e3-256">Para esta configuração, não são necessária toocreate TestVNet4 da secção anterior Olá, embora se criá-la, este será não entrar em conflito com estes passos.</span><span class="sxs-lookup"><span data-stu-id="d99e3-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="d99e3-257">Depois de concluir o Passo 1 e o Passo 2, avance para o Passo 6 (abaixo).</span><span class="sxs-lookup"><span data-stu-id="d99e3-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="d99e3-258"><a name="verifyranges"></a>Passo 6 – Certifique-se de intervalos de endereços IP Olá</span><span class="sxs-lookup"><span data-stu-id="d99e3-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="d99e3-259">Ao criar ligações adicionais, é importante tooverify que o espaço de endereços IP Olá da nova rede virtual Olá não se sobreponha a nenhum dos outros intervalos de Vnets ou intervalos de gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="d99e3-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="d99e3-260">Para este exercício, pode utilizar Olá os seguintes valores para Olá TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="d99e3-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="d99e3-261">**Valores da TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="d99e3-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="d99e3-262">Nome da VNet: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="d99e3-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="d99e3-263">Grupo de Recursos: TestRG5</span><span class="sxs-lookup"><span data-stu-id="d99e3-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="d99e3-264">Localização: Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="d99e3-264">Location: Japan East</span></span>
* <span data-ttu-id="d99e3-265">TestVNet5: 10.51.0.0/16 e 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d99e3-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="d99e3-266">Front-End: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d99e3-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="d99e3-267">Back-End: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d99e3-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="d99e3-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="d99e3-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="d99e3-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="d99e3-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="d99e3-270">IP Público: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="d99e3-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="d99e3-271">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="d99e3-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="d99e3-272">Ligação: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="d99e3-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="d99e3-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="d99e3-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="d99e3-274"><a name="TestVNet5"></a>Passo 7 – Criar e configurar TestVNet5</span><span class="sxs-lookup"><span data-stu-id="d99e3-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="d99e3-275">Este passo tem de ser efetuado no contexto de Olá de Olá nova subscrição, subscrição 5.</span><span class="sxs-lookup"><span data-stu-id="d99e3-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="d99e3-276">Esta parte pode ser realizada pelo administrador de Olá numa organização diferente proprietária da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="d99e3-277">tooswitch entre subscrições utilize ' lista de contas az – todos os ' toolist Olá conta tooyour disponíveis de subscrições, em seguida, utilize ' az conta set - subscrição <subscriptionID>' tooswitch toohello subscrição que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="d99e3-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="d99e3-278">Certifique-se de que está ligado tooSubscription 5, em seguida, cria um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d99e3-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="d99e3-279">Criar a TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d99e3-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="d99e3-280">Adicione sub-redes.</span><span class="sxs-lookup"><span data-stu-id="d99e3-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="d99e3-281">Adicione sub-rede do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="d99e3-282">Solicitar um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="d99e3-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="d99e3-283">Criar o gateway da TestVNet5 de Olá</span><span class="sxs-lookup"><span data-stu-id="d99e3-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="d99e3-284"><a name="connections5"></a>Passo 8 - criar ligações Olá</span><span class="sxs-lookup"><span data-stu-id="d99e3-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="d99e3-285">Iremos dividir este passo para duas sessões CLI marcada como **[subscrição 1]**, e **[subscrição 5]** porque gateways Olá estão em subscrições diferentes Olá.</span><span class="sxs-lookup"><span data-stu-id="d99e3-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="d99e3-286">tooswitch entre subscrições utilize ' lista de contas az – todos os ' toolist Olá conta tooyour disponíveis de subscrições, em seguida, utilize ' az conta set - subscrição <subscriptionID>' tooswitch toohello subscrição que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="d99e3-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="d99e3-287">**[Subscrição 1]**  Iniciar sessão e ligar tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="d99e3-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="d99e3-288">Seguinte Olá executar comando tooget Olá nome e um ID de Olá Gateway da saída de Olá:</span><span class="sxs-lookup"><span data-stu-id="d99e3-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="d99e3-289">Copiar resultado da Olá para "id:".</span><span class="sxs-lookup"><span data-stu-id="d99e3-289">Copy hello output for "id:".</span></span> <span data-ttu-id="d99e3-290">Envie Olá ID e nome de Olá de Olá VNet gateway (VNet1GW) toohello administrador da subscrição 5 por e-mail ou outro método.</span><span class="sxs-lookup"><span data-stu-id="d99e3-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="d99e3-291">Exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="d99e3-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="d99e3-292">**[Subscrição 5]**  Iniciar sessão e ligar tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="d99e3-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="d99e3-293">Seguinte Olá executar comando tooget Olá nome e um ID de Olá Gateway da saída de Olá:</span><span class="sxs-lookup"><span data-stu-id="d99e3-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="d99e3-294">Copiar resultado da Olá para "id:".</span><span class="sxs-lookup"><span data-stu-id="d99e3-294">Copy hello output for "id:".</span></span> <span data-ttu-id="d99e3-295">Envie Olá ID e nome de Olá de Olá VNet gateway (VNet5GW) toohello administrador da subscrição 1 por e-mail ou outro método.</span><span class="sxs-lookup"><span data-stu-id="d99e3-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="d99e3-296">**[Subscrição 1]**  Neste passo, poderá cria Olá ligação da TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d99e3-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="d99e3-297">Pode utilizar os seus próprios valores para a chave partilhada Olá, no entanto, tem de corresponder chave partilhada Olá ambas as ligações.</span><span class="sxs-lookup"><span data-stu-id="d99e3-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="d99e3-298">Criar uma ligação pode demorar uns toocomplete breves instantes.</span><span class="sxs-lookup"><span data-stu-id="d99e3-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="d99e3-299">Certifique-se que ligar tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="d99e3-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="d99e3-300">**[Subscrição 5]**  Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d99e3-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="d99e3-301">Certifique-se de que Olá partilhado chaves correspondem e que o se ligar tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="d99e3-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="d99e3-302"><a name="verify"></a>Verifique as ligações de Olá</span><span class="sxs-lookup"><span data-stu-id="d99e3-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="d99e3-303"><a name="faq"></a>FAQ da ligação VNet a VNet</span><span class="sxs-lookup"><span data-stu-id="d99e3-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d99e3-304">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d99e3-304">Next steps</span></span>

* <span data-ttu-id="d99e3-305">Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d99e3-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="d99e3-306">Para obter mais informações, consulte Olá [documentação de Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="d99e3-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="d99e3-307">Para informações sobre o BGP, consulte Olá [descrição geral do BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d99e3-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
