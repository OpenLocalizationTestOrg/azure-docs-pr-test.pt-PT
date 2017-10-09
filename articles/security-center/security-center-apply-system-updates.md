---
title: "atualizações do sistema aaaApply no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá as recomendações do Centro de segurança do Azure * * aplicar sistema atualizações * * e * * reinício após atualizações do sistema *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="4d3f1-103">Aplicar atualizações do sistema no Centro de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="4d3f1-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="4d3f1-104">Centro de segurança do Azure diariamente monitoriza Windows e Linux as máquinas virtuais (VMs) em falta atualizações do sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="4d3f1-105">Centro de segurança obtém uma lista de atualizações críticas e de segurança disponíveis do Windows Update ou Windows Server Update Services (WSUS), dependendo de que o serviço está configurado numa VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="4d3f1-106">Centro de segurança também verifica a existência de atualizações mais recentes Olá nos sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="4d3f1-107">Se a VM está em falta uma atualização do sistema, o Centro de segurança recomendará que aplique a atualizações do sistema</span><span class="sxs-lookup"><span data-stu-id="4d3f1-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="4d3f1-108">Este documento apresenta serviço Olá utilizando um exemplo de implementação.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="4d3f1-109">Não se trata de um guia passo-a-passo.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="4d3f1-110">Implementar a recomendação de Olá</span><span class="sxs-lookup"><span data-stu-id="4d3f1-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="4d3f1-111">No Olá **recomendações** painel, selecione **aplicar atualizações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Aplicar atualizações do Sistema][1]
2. <span data-ttu-id="4d3f1-113">Olá **aplicar atualizações do sistema** painel abre-apresentar uma lista de VMs em falta atualizações do sistema.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="4d3f1-114">Selecione uma VM.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-114">Select a VM.</span></span>

   ![Selecione uma VM][2]
3. <span data-ttu-id="4d3f1-116">É aberto um painel a apresentar uma lista de atualizações em falta para essa VM.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="4d3f1-117">Selecione uma atualização do sistema.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-117">Select a system update.</span></span> <span data-ttu-id="4d3f1-118">Neste exemplo, vamos selecione KB3156016.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-118">In this example, let’s select KB3156016.</span></span>

   ![Atualizações de segurança em falta][3]

4. <span data-ttu-id="4d3f1-120">Siga os passos de Olá Olá **de atualizações de segurança** painel tooapply Olá atualização em falta.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![Atualização de segurança][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="4d3f1-122">Reiniciar após atualizações do sistema</span><span class="sxs-lookup"><span data-stu-id="4d3f1-122">Reboot after system updates</span></span>
1. <span data-ttu-id="4d3f1-123">Devolver toohello **recomendações** painel.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="4d3f1-124">Uma nova entrada foi gerada depois de aplicar atualizações do sistema, denominadas **reinício após atualizações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="4d3f1-125">Esta entrada permite-lhe saber que precisa de processo do tooreboot Olá VM toocomplete Olá de aplicar atualizações do sistema.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![Reiniciar após atualizações do sistema][5]
2. <span data-ttu-id="4d3f1-127">Selecione **reinício após atualizações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="4d3f1-128">Esta ação abre **é de um reinício pendente toocomplete atualizações do sistema** painel a apresentar uma lista de VMs que precisa de toorestart toocomplete Olá aplicam-se o processo de atualizações do sistema.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![Reinício pendente][6]

<span data-ttu-id="4d3f1-130">Reinicie Olá VM do processo de Olá toocomplete do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="4d3f1-131">Consultar também</span><span class="sxs-lookup"><span data-stu-id="4d3f1-131">See also</span></span>
<span data-ttu-id="4d3f1-132">toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="4d3f1-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="4d3f1-133">[Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) – Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4d3f1-134">[Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) – Saiba como recomendações ajudam a proteger os seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4d3f1-135">[Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="4d3f1-136">[Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e respondeu.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="4d3f1-137">[Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="4d3f1-138">[FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="4d3f1-139">[Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre mensagens do Blogue acerca da segurança do Azure e conformidade.</span><span class="sxs-lookup"><span data-stu-id="4d3f1-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
