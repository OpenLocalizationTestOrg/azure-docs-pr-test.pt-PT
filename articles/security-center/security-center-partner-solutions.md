---
title: "aaaManaging soluções de parceiros no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda-o Centro de segurança do Azure lhe permite monitorizar a um Estado de funcionamento de Olá rapidamente das suas soluções de parceiros integradas na sua subscrição do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="01f6c-103">Monitorizar soluções de parceiros com o Centro de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="01f6c-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="01f6c-104">Este documento explica como como toomonitor Olá estado de funcionamento das suas soluções de parceiros no Centro de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="01f6c-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="01f6c-105">Este documento apresenta serviço Olá utilizando um exemplo de implementação.</span><span class="sxs-lookup"><span data-stu-id="01f6c-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="01f6c-106">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="01f6c-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="01f6c-107">Monitorizar soluções de parceiros</span><span class="sxs-lookup"><span data-stu-id="01f6c-107">Monitoring partner solutions</span></span>
<span data-ttu-id="01f6c-108">Olá **soluções de parceiros** mosaico Olá **Centro de segurança** permite painel monitorizar um Estado de funcionamento de Olá rapidamente das suas soluções de parceiros estão integradas na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="01f6c-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Mosaico Soluções de parceiros][1]

<span data-ttu-id="01f6c-110">Olá **soluções de parceiros** mosaico mostra o número de Olá das soluções de parceiros integradas na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="01f6c-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="01f6c-111">Se não existirem soluções integradas, o mosaico Olá mostra o número de Olá zero.</span><span class="sxs-lookup"><span data-stu-id="01f6c-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="01f6c-112">tooview Olá estado de funcionamento das suas soluções de parceiros:</span><span class="sxs-lookup"><span data-stu-id="01f6c-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="01f6c-113">Selecione Olá **soluções de parceiros** mosaico.</span><span class="sxs-lookup"><span data-stu-id="01f6c-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="01f6c-114">Olá **soluções de parceiros** é aberto o painel a apresentar uma lista das suas soluções de parceiros ligadas tooSecurity Center.</span><span class="sxs-lookup"><span data-stu-id="01f6c-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![Soluções de parceiros][3]

   <span data-ttu-id="01f6c-116">Estado de Olá de uma solução de parceiros pode ser:</span><span class="sxs-lookup"><span data-stu-id="01f6c-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="01f6c-117">Protegida (verde) – não existe nenhum problema de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="01f6c-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="01f6c-118">Mau estado de funcionamento (vermelho) – existe um problema de estado de funcionamento que exige atenção imediata.</span><span class="sxs-lookup"><span data-stu-id="01f6c-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="01f6c-119">Parado Reporting Services (cor de laranja) - solução Olá parou reporting o seu estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="01f6c-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="01f6c-120">Estado de proteção desconhecido (cor de laranja) - Estado de funcionamento de Olá da solução de Olá é desconhecido neste momento devido a tooa falhada de processo de adicionar uma nova solução de toohello do recurso existente.</span><span class="sxs-lookup"><span data-stu-id="01f6c-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="01f6c-121">Não reportada (cinzento) – solução Olá tem ainda não, o estado de uma solução pode ser não reportado se recentemente foi ligada e ainda está a implementar.</span><span class="sxs-lookup"><span data-stu-id="01f6c-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="01f6c-122">Selecione uma solução de parceiros.</span><span class="sxs-lookup"><span data-stu-id="01f6c-122">Select a partner solution.</span></span> <span data-ttu-id="01f6c-123">Neste exemplo, permite que selecione Olá **Qualys** solução.</span><span class="sxs-lookup"><span data-stu-id="01f6c-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="01f6c-124">É aberto um painel que mostra o estado de Olá da solução de parceiros de Olá e uma solução de Olá recursos associados.</span><span class="sxs-lookup"><span data-stu-id="01f6c-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="01f6c-125">Selecione **consola solução** experiência de gestão de parceiros de Olá tooopen para esta solução.</span><span class="sxs-lookup"><span data-stu-id="01f6c-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![Detalhe de solução de parceiros][4]
3. <span data-ttu-id="01f6c-127">Voltar atrás toohello **Qualys** painel e selecione **ligação VM**.</span><span class="sxs-lookup"><span data-stu-id="01f6c-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="01f6c-128">Olá **ligar aplicações** abre o painel.</span><span class="sxs-lookup"><span data-stu-id="01f6c-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="01f6c-129">Aqui pode ligar-se a solução de parceiros de toohello de recursos.</span><span class="sxs-lookup"><span data-stu-id="01f6c-129">Here you can connect resources toohello partner solution.</span></span>

   ![Ligação recursos toopartner solução][5]

## <a name="next-steps"></a><span data-ttu-id="01f6c-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="01f6c-131">Next steps</span></span>
<span data-ttu-id="01f6c-132">Neste documento, foram introduzida toohello **soluções de parceiros** mosaico no Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="01f6c-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="01f6c-133">toolearn mais acerca do Centro de segurança, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="01f6c-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="01f6c-134">[Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) — Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="01f6c-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="01f6c-135">[Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) — Saiba como recomendações ajudam a proteger os seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="01f6c-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="01f6c-136">[Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.</span><span class="sxs-lookup"><span data-stu-id="01f6c-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="01f6c-137">[Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e respondeu.</span><span class="sxs-lookup"><span data-stu-id="01f6c-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="01f6c-138">[FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="01f6c-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="01f6c-139">[Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) — obter Olá mais recentes notícias de segurança do Azure e informações.</span><span class="sxs-lookup"><span data-stu-id="01f6c-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
