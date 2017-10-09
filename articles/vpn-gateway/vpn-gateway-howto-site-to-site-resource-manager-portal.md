---
title: 'Ligar o seu tooan de rede no local rede virtual do Azure: VPN Site a Site: Portal | Microsoft Docs'
description: "Uma ligação de IPsec do seu local de rede tooan rede virtual do Azure através de toocreate de passos Olá Internet pública. Estes passos irão ajudá-lo a criar uma ligação de Gateway de VPN de Site para Site em vários locais através do portal Olá."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="00045-104">Criar uma ligação Site a Site no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="00045-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="00045-105">Este artigo mostra como toouse Olá toocreate portal do Azure uma ligação de gateway VPN de Site para Site da sua toohello de rede no local VNet.</span><span class="sxs-lookup"><span data-stu-id="00045-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="00045-106">passos de Olá neste artigo aplicam-se o modelo de implementação do Resource Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="00045-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="00045-107">Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="00045-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="00045-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="00045-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="00045-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00045-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="00045-110">CLI</span><span class="sxs-lookup"><span data-stu-id="00045-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="00045-111">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="00045-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="00045-112">Uma ligação de gateway VPN de Site a Site é utilizado tooconnect tooan rede virtual do Azure de rede no local através de um túnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="00045-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="00045-113">Este tipo de ligação requer uma VPN dispositivos localizado no local que tenha um tooit de atribuída de endereço IP público com acesso exterior.</span><span class="sxs-lookup"><span data-stu-id="00045-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="00045-114">Para obter mais informações sobre o gateways de VPN, veja [About VPN gateway (Acerca do gateway de VPN)](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="00045-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagrama da ligação de Gateway de Rede de VPNs em vários sites](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="00045-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="00045-116">Before you begin</span></span>

<span data-ttu-id="00045-117">Certifique-se de que cumpriu Olá os seguintes critérios antes de iniciar a configuração:</span><span class="sxs-lookup"><span data-stu-id="00045-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="00045-118">Certifique-se de um dispositivo VPN compatível e alguém que seja capaz de tooconfigure-lo.</span><span class="sxs-lookup"><span data-stu-id="00045-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="00045-119">Para obter mais informações sobre os dispositivos VPN compatíveis e a configuração do dispositivo, consulte [About VPN Devices (Acerca dos Dispositivos VPN)](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="00045-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="00045-120">Verifique se tem um endereço IP IPv4 público com acesso exterior para o seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="00045-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="00045-121">Este endereço IP não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="00045-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="00045-122">Se não estiver familiarizado com intervalos de endereços IP Olá localizados na configuração de rede no local, tem de toocoordinate com alguém que consiga fornecer esses detalhes.</span><span class="sxs-lookup"><span data-stu-id="00045-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="00045-123">Ao criar esta configuração, tem de especificar que o Azure irá encaminhar localização no local de tooyour dos prefixos de intervalo de endereços para IP Olá.</span><span class="sxs-lookup"><span data-stu-id="00045-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="00045-124">Nenhuma das sub-redes Olá da sua rede no local pode através de lap com sub-redes da rede virtual Olá que pretende que sejam tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="00045-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="00045-125"><a name="values"></a>Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="00045-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="00045-126">Exemplos de Olá neste artigo utilizam Olá os seguintes valores.</span><span class="sxs-lookup"><span data-stu-id="00045-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="00045-127">Pode utilizar estes toocreate de valores num ambiente de teste, ou consulte toothem toobetter compreender exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="00045-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="00045-128">**Nome da VNet:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="00045-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="00045-129">**Espaço de Endereços:**</span><span class="sxs-lookup"><span data-stu-id="00045-129">**Address Space:**</span></span> 
  * <span data-ttu-id="00045-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="00045-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="00045-131">10.12.0.0/16 (opcional para este exercício)</span><span class="sxs-lookup"><span data-stu-id="00045-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="00045-132">**Sub-redes:**</span><span class="sxs-lookup"><span data-stu-id="00045-132">**Subnets:**</span></span>
  * <span data-ttu-id="00045-133">Front-End: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="00045-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="00045-134">Back-End: 10.12.0.0/24 (opcional para este exercício)</span><span class="sxs-lookup"><span data-stu-id="00045-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="00045-135">**GatewaySubnet:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="00045-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="00045-136">**Grupo de Recursos:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="00045-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="00045-137">**Localização:** E.U.A. Leste</span><span class="sxs-lookup"><span data-stu-id="00045-137">**Location:** East US</span></span>
* <span data-ttu-id="00045-138">**Servidor DNS:** Opcional.</span><span class="sxs-lookup"><span data-stu-id="00045-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="00045-139">endereço IP Hello do servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="00045-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="00045-140">**Nome do Gateway de Rede Virtual:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="00045-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="00045-141">**IP Público:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="00045-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="00045-142">**Tipo de VPN:** Baseada na rota</span><span class="sxs-lookup"><span data-stu-id="00045-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="00045-143">**Tipo de Ligação:** Ste a site (IPsec)</span><span class="sxs-lookup"><span data-stu-id="00045-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="00045-144">**Tipo de Gateway:** VPN</span><span class="sxs-lookup"><span data-stu-id="00045-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="00045-145">**Nome do Gateway de Rede Local:** Site2</span><span class="sxs-lookup"><span data-stu-id="00045-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="00045-146">**Nome da Ligação:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="00045-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="00045-147"><a name="CreatVNet"></a>1. Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="00045-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="00045-148"><a name="dns"></a>2. Especificar um servidor DNS</span><span class="sxs-lookup"><span data-stu-id="00045-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="00045-149">DNS não é necessário toocreate um Site para Site ligação.</span><span class="sxs-lookup"><span data-stu-id="00045-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="00045-150">No entanto, se quiser toohave resolução de nomes de recursos que são implementadas tooyour rede virtual, deve especificar um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="00045-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="00045-151">Esta definição permite-lhe especificar o servidor DNS Olá que pretende que toouse para a resolução de nome para esta rede virtual.</span><span class="sxs-lookup"><span data-stu-id="00045-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="00045-152">Não cria um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="00045-152">It does not create a DNS server.</span></span> <span data-ttu-id="00045-153">Para obter mais informações sobre a resolução de nomes, veja [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Resolução de Nomes para VMs e instâncias de função).</span><span class="sxs-lookup"><span data-stu-id="00045-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="00045-154"><a name="gatewaysubnet"></a>3. Criar a sub-rede do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="00045-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="00045-155"><a name="VNetGateway"></a>4. Criar gateway de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="00045-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="00045-156"><a name="LocalNetworkGateway"></a>5. Criar gateway de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="00045-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="00045-157">gateway de rede local Olá refere-se normalmente localização do tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="00045-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="00045-158">Dê site Olá um nome pelo qual Azure pode consulte tooit, em seguida, especifique o endereço IP Olá de toowhich de dispositivo VPN do Olá no local, irá criar uma ligação.</span><span class="sxs-lookup"><span data-stu-id="00045-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="00045-159">Também especificar prefixos de endereços IP Olá serão encaminhados através de um dispositivo VPN do Olá VPN gateway toohello.</span><span class="sxs-lookup"><span data-stu-id="00045-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="00045-160">especificar prefixos de endereços de Olá são prefixos Olá localizados na sua rede no local.</span><span class="sxs-lookup"><span data-stu-id="00045-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="00045-161">Se as alterações de rede no local ou precisar de endereço IP público do toochange Olá para o dispositivo VPN Olá, pode atualizar facilmente valores hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="00045-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="00045-162"><a name="VPNDevice"></a>6. Configurar o dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="00045-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="00045-163">Rede do ligações site a Site tooan no local requer um dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="00045-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="00045-164">Neste passo, configure o seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="00045-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="00045-165">Quando configurar o seu dispositivo VPN, terá de seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="00045-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="00045-166">Uma chave partilhada.</span><span class="sxs-lookup"><span data-stu-id="00045-166">A shared key.</span></span> <span data-ttu-id="00045-167">Isto é Olá mesmo partilhado chave que especificar ao criar a ligação de VPN de Site para Site.</span><span class="sxs-lookup"><span data-stu-id="00045-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="00045-168">Nos nossos exemplos, iremos utilizar uma chave partilhada básica.</span><span class="sxs-lookup"><span data-stu-id="00045-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="00045-169">Recomendamos que geram um toouse chave mais complexa.</span><span class="sxs-lookup"><span data-stu-id="00045-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="00045-170">Olá endereço IP público do gateway da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="00045-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="00045-171">Pode ver o endereço IP público Olá utilizando Olá portal do Azure, PowerShell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="00045-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="00045-172">Olá toofind endereço IP público do seu gateway VPN utilizando Olá portal do Azure, navegue até demasiado**gateways da rede Virtual**, em seguida, clique no nome de Olá do seu gateway.</span><span class="sxs-lookup"><span data-stu-id="00045-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="00045-173"><a name="CreateConnection"></a>7. Criar a ligação de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="00045-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="00045-174">Crie a ligação de VPN de Olá Site a Site entre o gateway de rede virtual e o dispositivo VPN no local.</span><span class="sxs-lookup"><span data-stu-id="00045-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="00045-175"><a name="VerifyConnection"></a>8. Certifique-se a ligação de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="00045-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="00045-176"><a name="connectVM"></a>tooconnect tooa máquina</span><span class="sxs-lookup"><span data-stu-id="00045-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="00045-177"><a name="reset"></a>Como tooreset um gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="00045-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="00045-178">Repor o gateway de VPN do Azure é útil se perder a conectividade VPN em vários locais num ou mais túneis de rede de VPNs.</span><span class="sxs-lookup"><span data-stu-id="00045-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="00045-179">Nesta situação, os dispositivos VPN no local estão todos os a funcionar corretamente, mas são tooestablish não é possível túneis IPsec com gateways de VPN do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="00045-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="00045-180">Para obter os passos, veja [Reset a VPN gateway](vpn-gateway-resetgw-classic.md) (Repor um gateway de VPN).</span><span class="sxs-lookup"><span data-stu-id="00045-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="00045-181"><a name="resize"></a>Como toochange um gateway de SKU (redimensionar um gateway)</span><span class="sxs-lookup"><span data-stu-id="00045-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="00045-182">Para obter Olá passos toochange um SKU de gateway, consulte [SKUs de Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="00045-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00045-183">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="00045-183">Next steps</span></span>

* <span data-ttu-id="00045-184">Para informações sobre o BGP, consulte Olá [descrição geral do BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="00045-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="00045-185">Para obter informações sobre o Túnel Forçado, veja [Acerca do Túnel Forçado](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="00045-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="00045-186">Para obter informações sobre ligações Altamente Disponíveis Ativo-Ativo, veja [Premissas cruzadas de disponibilidade elevada e ligação VNet para VNet](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="00045-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
