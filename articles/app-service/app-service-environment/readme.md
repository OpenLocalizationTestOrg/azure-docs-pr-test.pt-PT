---
title: "Ambiente de serviço de aplicações de aaaAzure Leia-me"
description: "Apresenta uma lista de documentação de Olá que descreve o ambiente de serviço de aplicações do Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="081e9-103">Documentação de ambiente de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="081e9-103">App Service environment documentation</span></span>
 <span data-ttu-id="081e9-104">Ambiente de serviço de aplicações do Azure é uma funcionalidade do App Service do Azure que fornece um ambiente completamente isolado e dedicado para execução segura de aplicações do App Service numa escala elevada.</span><span class="sxs-lookup"><span data-stu-id="081e9-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="081e9-105">Esta capacidade pode alojar o [aplicações web][webapps], [aplicações móveis][mobileapps], [das API apps] [ APIApps], e [funções][Functions].</span><span class="sxs-lookup"><span data-stu-id="081e9-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="081e9-106">Ambientes do App Service (ASEs) são ideais para cargas de trabalho da aplicação que necessitam:</span><span class="sxs-lookup"><span data-stu-id="081e9-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="081e9-107">Muito grande escala.</span><span class="sxs-lookup"><span data-stu-id="081e9-107">Very high scale.</span></span>
* <span data-ttu-id="081e9-108">Isolamento e um acesso de rede.</span><span class="sxs-lookup"><span data-stu-id="081e9-108">Isolation and secure network access.</span></span>

<span data-ttu-id="081e9-109">Os clientes podem criar vários ASEs numa única região do Azure e em várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="081e9-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="081e9-110">Este versatility torna ASEs ideal para aumentar horizontalmente camadas da aplicação sem monitorização de estado para suportar cargas de trabalho RPS elevadas.</span><span class="sxs-lookup"><span data-stu-id="081e9-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="081e9-111">ASEs são isolada toorunning apenas aplicações de um único cliente e sempre são implementadas numa rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="081e9-111">ASEs are isolated toorunning only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="081e9-112">Os clientes têm um controlo detalhado sobre o tráfego de rede de aplicação de entrada e saída utilizando [grupos de segurança de rede][NSGs].</span><span class="sxs-lookup"><span data-stu-id="081e9-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="081e9-113">Aplicações também podem estabelecer ligações de alta velocidade seguras através de recursos da empresa tooon local redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="081e9-113">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="081e9-114">As aplicações necessitam frequentemente tooaccess recursos empresariais, tais como bases de dados internas e os serviços web.</span><span class="sxs-lookup"><span data-stu-id="081e9-114">Apps frequently need tooaccess corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="081e9-115">As aplicações que são executados no ASEs podem aceder a recursos através de [site para site] [ SiteToSite] VPN e [Azure ExpressRoute] [ ExpressRoute] ligações.</span><span class="sxs-lookup"><span data-stu-id="081e9-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="081e9-116">[O que é um ambiente de serviço de aplicações?][Intro]</span><span class="sxs-lookup"><span data-stu-id="081e9-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="081e9-117">[Criar um ambiente de serviço de aplicações][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="081e9-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="081e9-118">[Criar um ambiente de serviço de aplicações do Balanceador de carga interno][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="081e9-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="081e9-119">[Utilizar um ambiente de serviço de aplicações][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="081e9-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="081e9-120">[Considerações de redes e Olá ambiente de serviço de aplicações][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="081e9-120">[Networking considerations and hello App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="081e9-121">[Criar um ambiente de serviço de aplicações a partir de um modelo][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="081e9-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="081e9-122">Vídeos</span><span class="sxs-lookup"><span data-stu-id="081e9-122">Videos</span></span>
<span data-ttu-id="081e9-123">Mestre moderna PaaS para Olá Enterprise App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="081e9-123">Master Modern PaaS for hello Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="081e9-124">Implementar Aplicações altamente dimensionáveis e seguras</span><span class="sxs-lookup"><span data-stu-id="081e9-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="081e9-125">Executar Aplicações Móveis e Web Enterprise no Serviço de Aplicações do Azure</span><span class="sxs-lookup"><span data-stu-id="081e9-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="081e9-126">Ambiente do Serviço de Aplicações v1</span><span class="sxs-lookup"><span data-stu-id="081e9-126">App Service Environment v1</span></span> ##
<span data-ttu-id="081e9-127">Existem duas versões do ambiente de serviço de aplicações: ASEv1 e ASEv2.</span><span class="sxs-lookup"><span data-stu-id="081e9-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="081e9-128">Para obter informações sobre ASEv1, consulte [documentação do ambiente de serviço de aplicações v1][ASEv1README].</span><span class="sxs-lookup"><span data-stu-id="081e9-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
