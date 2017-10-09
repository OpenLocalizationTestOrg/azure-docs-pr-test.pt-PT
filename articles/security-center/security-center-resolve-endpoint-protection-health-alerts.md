---
title: "alertas de estado de funcionamento do aaaResolve endpoint protection no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação do Centro de segurança do Azure * * Endpoint Protection resolver o estado de funcionamento alertas * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="b859d-103">Resolver alertas de estado de funcionamento do endpoint protection no Centro de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="b859d-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="b859d-104">Centro de segurança do Azure recomendará que resolver alertas de estado de funcionamento de proteção de ponto final detetado.</span><span class="sxs-lookup"><span data-stu-id="b859d-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="b859d-105">Centro de segurança permite-lhe toosee que máquinas virtuais (VMs) ter falhas do endpoint protection e o número de falhas.</span><span class="sxs-lookup"><span data-stu-id="b859d-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="b859d-106">Este documento apresenta serviço Olá utilizando um exemplo de implementação.</span><span class="sxs-lookup"><span data-stu-id="b859d-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="b859d-107">Não se trata de um guia passo-a-passo.</span><span class="sxs-lookup"><span data-stu-id="b859d-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="b859d-108">Implementar a recomendação de Olá</span><span class="sxs-lookup"><span data-stu-id="b859d-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="b859d-109">No Olá **painel recomendações**, selecione **alertas de estado de funcionamento do Endpoint Protection resolver**.</span><span class="sxs-lookup"><span data-stu-id="b859d-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="b859d-110">![Resolver alertas de estado de funcionamento do endpoint protection][1]</span><span class="sxs-lookup"><span data-stu-id="b859d-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="b859d-111">Esta ação abre o painel de Olá **falha de Endpoint Protection** que apresenta uma lista de VMs com falhas e número de Olá de falhas para cada VM.</span><span class="sxs-lookup"><span data-stu-id="b859d-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="b859d-112">Selecione uma VM Olá lista.</span><span class="sxs-lookup"><span data-stu-id="b859d-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="b859d-113">![Falha de proteção de ponto final][2]</span><span class="sxs-lookup"><span data-stu-id="b859d-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="b859d-114">A **lista de falhas** painel abre para Olá selecionado VM, que apresenta uma lista de falhas.</span><span class="sxs-lookup"><span data-stu-id="b859d-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="b859d-115">Selecione uma falha de Olá lista toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="b859d-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="b859d-116">Esta ação abre um painel com informações sobre a falha de Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="b859d-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="b859d-117">![Lista de falhas][3]
   ![eventos de falha][4]</span><span class="sxs-lookup"><span data-stu-id="b859d-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="b859d-118">Consultar também</span><span class="sxs-lookup"><span data-stu-id="b859d-118">See also</span></span>
<span data-ttu-id="b859d-119">toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="b859d-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="b859d-120">[Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md)– Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="b859d-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b859d-121">[Gerir recomendações de segurança no Centro de Segurança do Azure](security-center-recommendations.md) – Saiba como as recomendações o ajudam a proteger os seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b859d-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b859d-122">[Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.</span><span class="sxs-lookup"><span data-stu-id="b859d-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="b859d-123">[Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e respondeu.</span><span class="sxs-lookup"><span data-stu-id="b859d-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="b859d-124">[Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="b859d-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="b859d-125">[FAQ do Centro de segurança do Azure](security-center-faq.md)– encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="b859d-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="b859d-126">[Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)-obter Olá mais recentes notícias de segurança do Azure e informações.</span><span class="sxs-lookup"><span data-stu-id="b859d-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
