---
title: "Balanceador de carga aaaInternal descrição geral | Microsoft Docs"
description: "Descrição geral para o Balanceador de carga interno e as respetivas funcionalidades. Como funciona a um balanceador de carga para pontos finais internos do Azure e possíveis cenários tooconfigure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="cf6a9-103">Descrição geral do Balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="cf6a9-103">Internal load balancer overview</span></span>

<span data-ttu-id="cf6a9-104">Ao contrário Olá Internet destinado ao balanceador de carga, o Balanceador de carga interno (ILB) do Olá direciona tráfego tooresources apenas dentro de serviço de nuvem Olá ou através de VPN tooaccess Olá infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="cf6a9-105">infraestrutura de Olá restringe o acesso toohello com balanceamento de carga endereços IP virtual (VIP) de um serviço em nuvem ou de uma rede Virtual para que nunca serão tooan diretamente expostos Internet endpoint.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="cf6a9-106">Isto permite interna de linha de negócio (LOB) toorun de aplicações no Azure e acedido a partir da nuvem Olá ou recursos no local.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="cf6a9-107">Por que razão poderá ser necessário um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="cf6a9-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="cf6a9-108">Azure interno carregar balanceamento (ILB) fornece balanceamento da carga entre máquinas virtuais que residem no interior de um serviço em nuvem ou de uma rede virtual com um âmbito regional.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="cf6a9-109">Para obter informações sobre a utilização de Olá e a configuração de redes virtuais com um âmbito regional, consulte [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) no Olá blogue do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="cf6a9-110">As redes virtuais existentes que foram configuradas para um grupo de afinidades não podem utilizar o ILB.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="cf6a9-111">ILB permite Olá os seguintes tipos de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="cf6a9-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="cf6a9-112">Dentro de um serviço de nuvem de máquinas virtuais tooa conjunto de máquinas virtuais que residem no Olá mesmo serviço em nuvem (consulte a figura 1).</span><span class="sxs-lookup"><span data-stu-id="cf6a9-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="cf6a9-113">Dentro de uma rede virtual, a partir de máquinas virtuais no conjunto de tooa de rede virtuais Olá de máquinas virtuais que residem no Olá mesmo serviço em nuvem de Olá virtual de rede (consulte a figura 2).</span><span class="sxs-lookup"><span data-stu-id="cf6a9-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="cf6a9-114">Para uma rede virtual de vários locais, de conjunto de tooa de computadores no local de máquinas virtuais que residem no Olá mesmo serviço em nuvem de Olá virtual de rede (consulte a figura 3).</span><span class="sxs-lookup"><span data-stu-id="cf6a9-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="cf6a9-115">As aplicações para a Internet, multicamadas na qual camadas de back-end Olá não são para a Internet, mas requerem balanceamento de carga para tráfego de camada de acesso à Internet Olá.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="cf6a9-116">Balanceamento de carga para aplicações de LOB alojadas no Azure, sem necessidade de software ou hardware de Balanceador de carga adicional.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="cf6a9-117">Incluindo servidores no local no conjunto de Olá de computadores cujo tráfego está a carga balanceado.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="cf6a9-118">Aplicações de várias camadas de com acesso à Internet</span><span class="sxs-lookup"><span data-stu-id="cf6a9-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="cf6a9-119">camada da web de Olá tem pontos finais com acesso à Internet para clientes de Internet e faz parte de um conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="cf6a9-120">Balanceador de carga Olá distribui o tráfego recebido dos clientes web para TCP porta 443 (HTTPS) toohello servidores web.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="cf6a9-121">servidores de base de dados de Olá estejam atrás de um ponto final ILB, que os servidores de web de Olá utilizam para armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="cf6a9-122">Ponto final, o tráfego é balanceamento de carga em servidores de base de dados de Olá no conjunto ILB Olá com balanceamento de carga do serviço esta base de dados.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="cf6a9-123">Olá a seguir mostra imagem Olá com acesso à aplicação multicamadas Internet dentro Olá mesmo serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![Serviço de nuvem única de balanceamento de carga interno](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="cf6a9-125">Figura 1 - com acesso à aplicação multicamadas Internet</span><span class="sxs-lookup"><span data-stu-id="cf6a9-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="cf6a9-126">Outro uso possíveis para uma aplicação multicamada é quando Olá ILB implementado um serviço cloud diferente tooa que Olá um serviço de Olá consumo para Olá ILB.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="cf6a9-127">Nuvem ponto final ILB de toohello aceder a serviços com Olá terão a mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="cf6a9-128">Olá segue mostra de imagem são servidores web front-end num serviço cloud diferente da base de dados de Olá back-end e utilizar Olá ponto final ILB dentro Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![Interna balanceamento da carga entre serviços cloud](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="cf6a9-130">Figura 2 - servidores front-end num serviço cloud diferente</span><span class="sxs-lookup"><span data-stu-id="cf6a9-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="cf6a9-131">Intranet aplicações de linha de negócio</span><span class="sxs-lookup"><span data-stu-id="cf6a9-131">Intranet line of business applications</span></span>

<span data-ttu-id="cf6a9-132">Tráfego de clientes na rede no local de Olá obter com balanceamento de carga em conjunto Olá dos servidores LOB utilizando a rede de tooAzure de ligação VPN.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="cf6a9-133">computador de cliente Olá terão acesso tooan endereço IP do serviço de VPN do Azure através da VPN de ponto toosite.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="cf6a9-134">Permite Olá de utilização de Olá alojada por trás do ponto final ILB de Olá de aplicação de LOB.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![Através da VPN de ponto toosite de balanceamento de carga interno](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="cf6a9-136">Figura 3 - aplicações de LOB alojadas por trás do ponto final de Olá LB</span><span class="sxs-lookup"><span data-stu-id="cf6a9-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="cf6a9-137">Outro cenário para Olá LOB é toohave uma toosite toohello virtual rede de VPNs onde o ponto final ILB de Olá está configurado.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="cf6a9-138">Isto permite que a rede tráfego toobe encaminhado toohello ILB ponto final no local.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![Site toosite VPN a utilizar o balanceamento de carga interno](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="cf6a9-140">Figura 4 - tráfego de rede no local encaminhada toohello ILB endpoint</span><span class="sxs-lookup"><span data-stu-id="cf6a9-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="cf6a9-141">Limitações</span><span class="sxs-lookup"><span data-stu-id="cf6a9-141">Limitations</span></span>

<span data-ttu-id="cf6a9-142">Configurações de Balanceador de carga internas não suportam a realizar o SNAT.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="cf6a9-143">No contexto de Olá deste documento, realizar o SNAT refere-se tradução de endereços de rede tooport masquerading origem.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="cf6a9-144">Isto aplica-se tooscenarios em que uma VM com um conjunto de Balanceador de carga tem o endereço IP de front-end do tooreach Olá respetivos interno Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="cf6a9-145">Este cenário não é suportado para o Balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="cf6a9-146">Falhas de ligação irão ocorrer quando o fluxo de Olá é com balanceamento de carga toohello VM que teve origem fluxo Olá.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="cf6a9-147">Tem de utilizar um balanceador de carga de estilo de proxy para tais cenários.</span><span class="sxs-lookup"><span data-stu-id="cf6a9-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf6a9-148">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="cf6a9-148">Next Steps</span></span>

[<span data-ttu-id="cf6a9-149">Suporte do Azure Resource Manager para o Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="cf6a9-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="cf6a9-150">Começar a configurar um balanceador de carga com acesso de Internet</span><span class="sxs-lookup"><span data-stu-id="cf6a9-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="cf6a9-151">Começar a configurar um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="cf6a9-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="cf6a9-152">Configurar um modo de distribuição de Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="cf6a9-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="cf6a9-153">Configurar definições de tempo limite TCP inativo para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="cf6a9-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
