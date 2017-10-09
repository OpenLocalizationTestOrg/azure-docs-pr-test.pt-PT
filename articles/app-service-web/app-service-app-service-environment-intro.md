---
title: "aaaIntroduction tooApp v1 de ambiente de serviço"
description: "Saiba mais sobre a funcionalidade de Olá v1 de ambiente de serviço de aplicações que fornece unidades de escala segura, associados a VNet, dedicada para executar todas as suas aplicações."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a><span data-ttu-id="6e0d4-103">Introdução tooApp v1 de ambiente de serviço</span><span class="sxs-lookup"><span data-stu-id="6e0d4-103">Introduction tooApp Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="6e0d4-104">Este artigo é sobre Olá v1 de ambiente de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="6e0d4-105">Há uma versão mais recente Olá ambiente de serviço de aplicações que é mais fácil toouse e é executada na infraestrutura mais poderosa.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="6e0d4-106">toolearn mais informações sobre a nova versão de Olá começar a utilizar Olá [introdução toohello ambiente de serviço de aplicações](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="6e0d4-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="6e0d4-107">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="6e0d4-107">Overview</span></span>
<span data-ttu-id="6e0d4-108">Um ambiente de serviço de aplicações é um [Premium] [ PremiumTier] service opção plano do App Service do Azure fornece um ambiente completamente isolado e dedicado para execução segura de aplicações do App Service do Azure numa escala elevada, incluindo [Web Apps][WebApps], [Mobile Apps][MobileApps], e [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="6e0d4-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="6e0d4-109">Ambientes de serviço de aplicações são ideais para cargas de trabalho de aplicações que requerem:</span><span class="sxs-lookup"><span data-stu-id="6e0d4-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="6e0d4-110">Muito grande escala</span><span class="sxs-lookup"><span data-stu-id="6e0d4-110">Very high scale</span></span>
* <span data-ttu-id="6e0d4-111">Isolamento e de acesso à rede segura</span><span class="sxs-lookup"><span data-stu-id="6e0d4-111">Isolation and secure network access</span></span>

<span data-ttu-id="6e0d4-112">Os clientes podem criar vários ambientes do App Service numa única região do Azure, bem como em várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="6e0d4-113">Isto faz com que ambientes do App Service ideal para aumentar horizontalmente camadas de aplicações sem estado para suportar cargas de trabalho RPS elevadas.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="6e0d4-114">Ambientes do App Service são toorunning isolado apenas aplicações de um único cliente e são sempre implementados numa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-114">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="6e0d4-115">Os clientes não têm controlo detalhado sobre o tráfego de rede de aplicação de entrada e saída e as aplicações podem estabelecer ligações seguras de alta velocidade através de recursos da empresa tooon local redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="6e0d4-116">Todos os artigos e como-a da sobre ambientes de serviço de aplicações estão disponíveis no Olá [Leia-me para ambientes de serviço de aplicações](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="6e0d4-116">All articles and How-To's about App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="6e0d4-117">Para uma descrição geral de como ambientes do App Service permitem escala elevada e proteger o acesso de rede, consulte Olá [descrição profunda AzureCon] [ AzureConDeepDive] em ambientes do App Service!</span><span class="sxs-lookup"><span data-stu-id="6e0d4-117">For an overview of how App Service Environments enable high scale and secure network access, see hello [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="6e0d4-118">Para uma descrição profunda horizontalmente da receção utilizando o vários ambientes do App Service Consulte o artigo de Olá sobre toosetup um [requisitos de espaço de aplicação geo-distribuição][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="6e0d4-118">For a deep-dive on horizontally scaling using multiple App Service Environments see hello article on how toosetup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="6e0d4-119">toosee como mostrada na Olá AzureCon detalhada da arquitetura de segurança de Olá foi configurada, consulte o artigo de Olá na implementação de um [em camadas a arquitetura de segurança](app-service-app-service-environment-layered-security.md) com ambientes do App Service.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-119">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="6e0d4-120">Aplicações em execução em ambientes do App Service podem ter o respetivo acesso gated pelos dispositivos a montante, tais como firewalls de aplicação web (WAF).</span><span class="sxs-lookup"><span data-stu-id="6e0d4-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="6e0d4-121">artigo Olá [configurar uma WAF para ambientes do App Service](app-service-app-service-environment-web-application-firewall.md) abrange neste cenário.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-121">hello article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="6e0d4-122">Recursos de computação dedicada</span><span class="sxs-lookup"><span data-stu-id="6e0d4-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="6e0d4-123">Todos os recursos num ambiente de serviço de aplicações estão de computação de Olá dedicado exclusivamente tooa única subscrição e um ambiente de serviço de aplicações pode ser configurado com recursos de computação toofifty (50) para utilização exclusiva por uma única aplicação.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-123">All of hello compute resources in an App Service Environment are dedicated exclusively tooa single subscription, and an App Service Environment can be configured with up toofifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="6e0d4-124">Um ambiente de serviço de aplicações é composto por um agrupamento de recursos de computação de front-end, bem como agrupamentos de recursos de computação do um toothree trabalho.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-124">An App Service Environment is composed of a front-end compute resource pool, as well as one toothree worker compute resource pools.</span></span> 

<span data-ttu-id="6e0d4-125">conjunto de front-end Olá contém recursos de computação responsável por terminação de SSL como balanceamento de carga bem automático de pedidos de aplicações dentro de um ambiente de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-125">hello front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="6e0d4-126">Cada conjunto de trabalho contém recursos de computação alocados demasiado[planos do App Service][AppServicePlan], que por sua vez, conter uma ou mais aplicações do App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-126">Each worker pool contains compute resources allocated too[App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="6e0d4-127">Uma vez que podem existir dos conjuntos de trabalho diferentes toothree num ambiente de serviço de aplicações, dispõe de recursos de computação diferentes do Olá flexibilidade toochoose para cada conjunto de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-127">Since there can be up toothree different worker pools in an App Service Environment, you have hello flexibility toochoose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="6e0d4-128">Por exemplo, isto permite-lhe toocreate agrupamento de um trabalho com menos eficiente recursos de computação para planos do App Service pretendido para aplicações de desenvolvimento ou teste.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-128">For example, this allows you toocreate one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="6e0d4-129">Um conjunto de trabalho segundo (ou mesmo terceiro) utilizar recursos de computação mais poderosos, concebidos para planos de serviço de aplicações a executar aplicações de produção.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="6e0d4-130">Para obter mais detalhes sobre a quantidade de Olá de computação recursos obter toohello disponíveis front-end e os conjuntos de trabalho, consulte [como tooConfigure um ambiente de serviço de aplicações][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="6e0d4-130">For more details on hello quantity of compute resources available toohello front-end and worker pools, see [How tooConfigure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="6e0d4-131">Para obter detalhes sobre Olá disponível computação tamanhos de recurso suportados num ambiente de serviço de aplicações, consulte Olá [preços do App Service] [ AppServicePricing] página e reveja Olá opções disponíveis para ambientes do App Service no escalão de preço Premium Olá.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-131">For details on hello available compute resource sizes supported in an App Service Environment, consult hello [App Service Pricing][AppServicePricing] page and review hello available options for App Service Environments in hello Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="6e0d4-132">Suporte de rede virtual</span><span class="sxs-lookup"><span data-stu-id="6e0d4-132">Virtual Network Support</span></span>
<span data-ttu-id="6e0d4-133">Um ambiente de serviço de aplicações podem ser criado na **ou** uma rede virtual do Azure Resource Manager, **ou** uma rede virtual do modelo de implementação clássica ([obter mais informações sobre redes virtuais][MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="6e0d4-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="6e0d4-134">Uma vez que um ambiente de serviço de aplicações sempre existe numa rede virtual e mais precisamente dentro de uma sub-rede de uma rede virtual, pode tirar partido das funcionalidades de segurança de Olá de redes virtuais toocontrol ambas as comunicações de rede de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage hello security features of virtual networks toocontrol both inbound and outbound network communications.</span></span>  

<span data-ttu-id="6e0d4-135">Um ambiente de serviço de aplicações pode ser qualquer um dos Internet com um endereço IP público ou interno com acesso com apenas um endereço de Azure Balanceador de carga interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="6e0d4-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="6e0d4-136">Pode utilizar [grupos de segurança de rede] [ NetworkSecurityGroups] toorestrict sub-rede toohello comunicações de rede onde reside um ambiente de serviço de aplicação de entrada.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-136">You can use [network security groups][NetworkSecurityGroups] toorestrict inbound network communications toohello subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="6e0d4-137">Isto permite que aplicações toorun atrás montante dispositivos e serviços, tais como firewalls de aplicação web e fornecedores de SaaS de rede.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-137">This allows you toorun apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="6e0d4-138">As aplicações necessitam frequentemente também tooaccess recursos empresariais, tais como bases de dados internas e os serviços web.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-138">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="6e0d4-139">Uma abordagem comum é toomake estes pontos finais disponíveis toointernal apenas o tráfego de rede que circulam dentro de uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-139">A common approach is toomake these endpoints available only toointernal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="6e0d4-140">Depois de um ambiente de serviço de aplicações associados a um toohello mesma rede virtual que Olá interno dos serviços, aplicações em execução no ambiente de Olá possa aceder aos mesmos, incluindo acessíveis através de pontos finais [Site a Site] [ SiteToSite]e [Azure ExpressRoute] [ ExpressRoute] ligações.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-140">Once an App Service Environment is joined toohello same virtual network as hello internal services, apps running in hello environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="6e0d4-141">Para obter mais detalhes sobre como funcionam os ambientes do App Service com redes virtuais e redes no local Consulte Olá os seguintes artigos [arquitetura de rede][NetworkArchitectureOverview], [controlar de entrada Tráfego][ControllingInboundTraffic], e [ligar de forma segura tooBackends][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="6e0d4-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult hello following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting tooBackends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="6e0d4-142">Introdução</span><span class="sxs-lookup"><span data-stu-id="6e0d4-142">Getting started</span></span>
<span data-ttu-id="6e0d4-143">tooget começar a utilizar ambientes do App Service, consulte [como tooCreate um ambiente de serviço de aplicações][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="6e0d4-143">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="6e0d4-144">Todos os artigos e como-a para ambientes de serviço de aplicações estão disponíveis no Olá [Leia-me para ambientes de serviço de aplicações](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="6e0d4-144">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="6e0d4-145">Para obter mais informações sobre a plataforma do App Service do Azure de Olá, consulte [App Service do Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="6e0d4-145">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="6e0d4-146">Para obter uma descrição geral de Olá arquitetura de rede do ambiente de serviço de aplicações, consulte Olá [descrição geral da arquitetura de rede] [ NetworkArchitectureOverview] artigo.</span><span class="sxs-lookup"><span data-stu-id="6e0d4-146">For an overview of hello App Service Environment network architecture, see hello [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="6e0d4-147">Para obter detalhes sobre como utilizar um ambiente de serviço de aplicações com o ExpressRoute, consulte Olá seguinte artigo [Express Route e ambientes do App Service][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="6e0d4-147">For details on using an App Service Environment with ExpressRoute, see hello following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


