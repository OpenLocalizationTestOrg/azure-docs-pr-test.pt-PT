---
title: aaaOverview do BGP com Gateways de VPN do Azure | Microsoft Docs
description: "Este artigo fornece uma descrição geral do BGP com Gateways de VPN do Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="6d66d-103">Descrição geral do BGP com Gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="6d66d-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="6d66d-104">Este artigo fornece uma descrição geral do suporte BGP (Border Gateway Protocol) nos Gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d66d-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="6d66d-105">BGP é Olá protocolo de encaminhamento padrão utilizado normalmente na Olá tooexchange encaminhamento e acessibilidade informação de Internet entre duas ou mais redes.</span><span class="sxs-lookup"><span data-stu-id="6d66d-105">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="6d66d-106">Quando utilizado no contexto de Olá de redes virtuais do Azure, BGP permite que os Gateways de VPN do Azure Olá e os dispositivos VPN no local, denominados elementos BGP ou vizinhos, tooexchange "rotas" que informarão ambos os gateways no Olá disponibilidade e acessibilidade os prefixos toogo através de gateways de Olá ou routers envolvidos.</span><span class="sxs-lookup"><span data-stu-id="6d66d-106">When used in hello context of Azure Virtual Networks, BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="6d66d-107">BGP também pode ativar o encaminhamento de tráfego entre várias redes ao propagar rotas um gateway BGP aprende de um tooall de elemento de rede BGP outros elementos de rede BGP.</span><span class="sxs-lookup"><span data-stu-id="6d66d-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="6d66d-108">Porquê utilizar o BGP?</span><span class="sxs-lookup"><span data-stu-id="6d66d-108">Why use BGP?</span></span>
<span data-ttu-id="6d66d-109">O BGP é uma funcionalidade opcional que pode utilizar com os gateways de VPN do Azure Baseados na Rota.</span><span class="sxs-lookup"><span data-stu-id="6d66d-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="6d66d-110">Também deve certificar-se de que os dispositivos VPN no local suportam o BGP, antes de ativar a funcionalidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="6d66d-110">You should also make sure your on-premises VPN devices support BGP before you enable hello feature.</span></span> <span data-ttu-id="6d66d-111">Pode continuar toouse gateways de VPN do Azure e os dispositivos VPN no local sem o BGP.</span><span class="sxs-lookup"><span data-stu-id="6d66d-111">You can continue toouse Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="6d66d-112">É Olá equivalente a utilizar rotas estáticas (sem BGP) *vs* utilizar encaminhamento dinâmico com BGP entre as suas redes e do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d66d-112">It is hello equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="6d66d-113">O BGP possui várias vantagens e novas capacidades:</span><span class="sxs-lookup"><span data-stu-id="6d66d-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="6d66d-114">Suporte de atualizações de prefixos automáticas e flexíveis</span><span class="sxs-lookup"><span data-stu-id="6d66d-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="6d66d-115">Com o BGP, só precisa de toodeclare um prefixo mínimo tooa específico elemento de rede BGP túnel IPsec S2S VPN Olá.</span><span class="sxs-lookup"><span data-stu-id="6d66d-115">With BGP, you only need toodeclare a minimum prefix tooa specific BGP peer over hello IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="6d66d-116">Pode ser tão pequena como um prefixo de anfitrião (/ 32) de Olá endereço IP do elemento de rede BGP do seu dispositivo VPN no local.</span><span class="sxs-lookup"><span data-stu-id="6d66d-116">It can be as small as a host prefix (/32) of hello BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="6d66d-117">Pode controlar que prefixos no local rede pretende tooadvertise tooAzure tooallow tooaccess a rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d66d-117">You can control which on-premises network prefixes you want tooadvertise tooAzure tooallow your Azure Virtual Network tooaccess.</span></span>

<span data-ttu-id="6d66d-118">Também pode anunciar prefixos maiores, que podem incluir alguns dos seus prefixos de endereço VNet, tais como um grande privado espaço de endereços IP (por exemplo, 10.0.0.0/8).</span><span class="sxs-lookup"><span data-stu-id="6d66d-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="6d66d-119">Tenha em atenção que os prefixos de Olá não podem ser idênticos a nenhum dos seus prefixos VNet.</span><span class="sxs-lookup"><span data-stu-id="6d66d-119">Note though hello prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="6d66d-120">As rotas idênticas tooyour prefixos de VNet serão rejeitados.</span><span class="sxs-lookup"><span data-stu-id="6d66d-120">Those routes identical tooyour VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="6d66d-121">Suporte de vários túneis entre uma VNet e um site no local, com ativação pós-falha automática baseada no BGP</span><span class="sxs-lookup"><span data-stu-id="6d66d-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="6d66d-122">Pode estabelecer várias ligações entre a VNet do Azure e os dispositivos VPN no local na Olá mesma localização.</span><span class="sxs-lookup"><span data-stu-id="6d66d-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in hello same location.</span></span> <span data-ttu-id="6d66d-123">Esta capacidade proporciona vários túneis (caminhos) entre duas redes de Olá uma configuração de ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="6d66d-123">This capability provides multiple tunnels (paths) between hello two networks in an active-active configuration.</span></span> <span data-ttu-id="6d66d-124">Se um dos túneis Olá estiver desligado, rotas Olá de correspondentes serão retiradas através do BGP e tráfego de Olá automaticamente desvia toohello restantes túneis.</span><span class="sxs-lookup"><span data-stu-id="6d66d-124">If one of hello tunnels is disconnected, hello corresponding routes will be withdrawn via BGP and hello traffic automatically shifts toohello remaining tunnels.</span></span>

<span data-ttu-id="6d66d-125">Olá diagrama a seguir mostra um exemplo simples desta configuração de elevada disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="6d66d-125">hello following diagram shows a simple example of this highly available setup:</span></span>

![Vários caminhos ativos](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="6d66d-127">Suporte do encaminhamento do tráfego entre as suas redes no local e várias VNets do Azure</span><span class="sxs-lookup"><span data-stu-id="6d66d-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="6d66d-128">BGP permite que vários gateways toolearn e propaguem os prefixos a partir de redes diferentes, se estiverem direta ou indiretamente ligados.</span><span class="sxs-lookup"><span data-stu-id="6d66d-128">BGP enables multiple gateways toolearn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="6d66d-129">Esta opção pode ativar o encaminhamento de tráfego com os gateways de VPN do Azure entre os sites no local ou entre várias Redes Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d66d-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="6d66d-130">Olá diagrama seguinte mostra um exemplo de uma topologia multi-HOP com vários caminhos em que o tráfego pode transitar entre Olá duas redes no local através de gateways de VPN do Azure dentro Olá Networks Microsoft:</span><span class="sxs-lookup"><span data-stu-id="6d66d-130">hello following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between hello two on-premises networks through Azure VPN gateways within hello Microsoft Networks:</span></span>

![Tráfego multi-hop](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="6d66d-132">FAQ SOBRE O BGP</span><span class="sxs-lookup"><span data-stu-id="6d66d-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="6d66d-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6d66d-133">Next steps</span></span>
<span data-ttu-id="6d66d-134">Consulte [introdução ao BGP nos gateways de VPN do Azure](vpn-gateway-bgp-resource-manager-ps.md) para passos tooconfigure BGP para as ligações de VNet a VNet e em vários locais.</span><span class="sxs-lookup"><span data-stu-id="6d66d-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps tooconfigure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

