---
title: "aaaAzure do serviço de aplicações e o respetivo impacto nos serviços do Azure existentes"
description: "Explica como Olá novo serviço de aplicações do Azure e as respetivas funcionalidades afetam existentes serviços no Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="85098-103">Serviço de Aplicações do Azure e serviços do Azure existentes</span><span class="sxs-lookup"><span data-stu-id="85098-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="85098-104">Este artigo descreve Olá alterações tooexisting Azure services como parte da Olá alteração toobring em conjunto vários serviços do Azure para [App Service do Azure](https://azure.microsoft.com/services/app-service/), uma nova oferta integrada.</span><span class="sxs-lookup"><span data-stu-id="85098-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="85098-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="85098-105">Overview</span></span>
<span data-ttu-id="85098-106">[App Service do Azure](https://azure.microsoft.com/services/app-service/) é um serviço de nuvem novos e únicos que permite aos programadores toocreate web apps e móveis para qualquer plataforma e de qualquer dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85098-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="85098-107">Serviço de aplicações é que uma solução integrada concebida toostreamline repetido funções de codificação, integrar com sistemas de SaaS e enterprise e automatizar processos empresariais ao satisfazer as suas necessidades de segurança, escalabilidade e fiabilidade.</span><span class="sxs-lookup"><span data-stu-id="85098-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="85098-108">Serviço de aplicações reúne Olá seguir existente do Azure serviços - [sites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), e [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) numa única combinado serviço, enquanto adicionar novas capacidades poderosas.</span><span class="sxs-lookup"><span data-stu-id="85098-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="85098-109">Serviço de aplicações permite-lhe Olá toohost os seguintes tipos de aplicações:</span><span class="sxs-lookup"><span data-stu-id="85098-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="85098-110">Aplicações Web</span><span class="sxs-lookup"><span data-stu-id="85098-110">Web Apps</span></span>
* <span data-ttu-id="85098-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="85098-111">Mobile Apps</span></span>
* <span data-ttu-id="85098-112">Aplicações API</span><span class="sxs-lookup"><span data-stu-id="85098-112">API Apps</span></span>
* <span data-ttu-id="85098-113">Aplicações Lógicas</span><span class="sxs-lookup"><span data-stu-id="85098-113">Logic Apps</span></span>

<span data-ttu-id="85098-114">Olá tabela seguinte explica como existente do Azure serviços mapeiam tooApp serviço e Olá tipos de aplicações disponíveis dentro da mesma.</span><span class="sxs-lookup"><span data-stu-id="85098-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="85098-115">Serviço do Azure existente</span><span class="sxs-lookup"><span data-stu-id="85098-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="85098-116">Serviço de Aplicações do Azure</span><span class="sxs-lookup"><span data-stu-id="85098-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="85098-117">O que foi alterado</span><span class="sxs-lookup"><span data-stu-id="85098-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="85098-118">Web Sites do Azure</span><span class="sxs-lookup"><span data-stu-id="85098-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="85098-119">Aplicações Web</span><span class="sxs-lookup"><span data-stu-id="85098-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="85098-120">Para Web sites do Azure, o serviço de aplicações é estritamente limitado toochanging Olá nome sites tooWeb aplicações.</span><span class="sxs-lookup"><span data-stu-id="85098-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="85098-121">Todas as instâncias existentes de Web sites estão agora Web Apps no App Service.</span><span class="sxs-lookup"><span data-stu-id="85098-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="85098-122">Pode aceder ao seus sites existentes através de Olá <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Portal do Azure</a>, onde poderá encontrar todos os sites existentes em <em>Web Apps</em>.</span><span class="sxs-lookup"><span data-stu-id="85098-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="85098-123"><em>Planear o alojamento de Web</em> está agora <em>plano do App Service</em>.</span><span class="sxs-lookup"><span data-stu-id="85098-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="85098-124">Um <em>plano do App Service</em> pode alojar qualquer tipo de aplicação de serviço de aplicações, tais como aplicações Web, móveis, lógicas ou API.</span><span class="sxs-lookup"><span data-stu-id="85098-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="85098-125">Serviço Web Apps do App do Azure em geral é disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="85098-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="85098-126"><a href="http://azure.microsoft.com/services/app-service/web/">Saiba mais sobre as aplicações Web</a>.</span><span class="sxs-lookup"><span data-stu-id="85098-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="85098-127">Serviços Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="85098-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="85098-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="85098-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="85098-129">Mobile Services continuar toobe disponível como um serviço autónomo e permanecem totalmente suportados.</span><span class="sxs-lookup"><span data-stu-id="85098-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="85098-130">As Mobile Apps é um tipo de aplicação no App Service, integra-se a todas as funcionalidades de Olá do Mobile Services e muito mais.</span><span class="sxs-lookup"><span data-stu-id="85098-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="85098-131">É fácil demasiado<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrar a partir dos Mobile Services tooMobile aplicações</a>.</span><span class="sxs-lookup"><span data-stu-id="85098-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="85098-132">Como parte do serviço de aplicações, as Mobile Apps obter novas capacidades para além dos Mobile Services, tais como a integração no local e sistemas de SaaS, ranhuras, WebJobs, opções de dimensionamento melhor e mais de teste.</span><span class="sxs-lookup"><span data-stu-id="85098-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="85098-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Saiba mais sobre as Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="85098-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="85098-134">Aplicações API</span><span class="sxs-lookup"><span data-stu-id="85098-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="85098-135">As API Apps é um novo tipo de aplicação no App Service permite-lhe criar e consumir APIs na nuvem de Olá facilmente.</span><span class="sxs-lookup"><span data-stu-id="85098-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="85098-136"><a href="http://azure.microsoft.com/services/app-service/api/">Saiba mais sobre API Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="85098-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="85098-137">Aplicações Lógicas</span><span class="sxs-lookup"><span data-stu-id="85098-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="85098-138">As Logic Apps é um novo tipo de aplicação no App Service permite-lhe automatizar facilmente os processos de negócios.</span><span class="sxs-lookup"><span data-stu-id="85098-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="85098-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Saiba mais sobre Logic Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="85098-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="85098-140">Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="85098-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="85098-141">BizTalk API Apps</span><span class="sxs-lookup"><span data-stu-id="85098-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="85098-142">BizTalk Services continuar toobe disponível como um serviço autónomo e permanecem totalmente suportados.</span><span class="sxs-lookup"><span data-stu-id="85098-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="85098-143">Todos os Olá capacidades do BizTalk Services estão integradas no serviço de aplicações como API Apps ativar utilizadores tooperform enterprise integração de aplicações e cenários de integração de B2B com qualquer um dos tipos de aplicação Olá no App Service.</span><span class="sxs-lookup"><span data-stu-id="85098-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="85098-144">Com as Logic Apps, agora pode automatizar os processos de negócios através de um visual conceber experiência toocreate fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="85098-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="85098-145">toolearn mais, visite [documentação do App Service](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="85098-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

