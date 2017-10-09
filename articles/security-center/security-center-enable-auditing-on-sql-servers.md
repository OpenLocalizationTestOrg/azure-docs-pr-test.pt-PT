---
title: "aaaEnable auditoria e deteção de ameaças em SQL servers no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação do Centro de segurança do Azure * * deteção de ameaças e ativar a auditoria em servidores SQL *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="ed3e6-103">Ativar a auditoria e deteção de ameaças em SQL servers no Centro de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="ed3e6-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="ed3e6-104">Centro de segurança do Azure recomendará que ativar a auditoria e deteção de ameaças para todas as bases de dados em servidores SQL do Azure se auditoria já não está ativada.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="ed3e6-105">Auditoria e ameaças deteção pode ajudar a manter a conformidade de regulamentação, compreender a atividade de base de dados e obter informações sobre discrepâncias e anomalias que poderão indicar preocupações para a empresa ou suspeitas de violação de segurança.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="ed3e6-106">Uma vez que ativou a auditoria, pode configurar a deteção de ameaças definições e os e-mails tooreceive alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="ed3e6-107">A deteção de ameaças Deteta atividades de base de dados anómalas, indicando potenciais segurança ameaças toohello base de dados do.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="ed3e6-108">Isto permite-lhe toodetect e responder a ameaças toopotential à medida que ocorrem.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="ed3e6-109">Esta recomendação aplica-se toohello apenas; serviço do SQL do Azure não inclui o SQL Server em execução em máquinas virtuais nos serviços de infraestrutura do Azure (IaaS do Azure).</span><span class="sxs-lookup"><span data-stu-id="ed3e6-109">This recommendation applies toohello Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="ed3e6-110">Este documento apresenta serviço Olá utilizando um exemplo de implementação.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="ed3e6-111">Não se trata de um guia passo-a-passo.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="ed3e6-112">Implementar a recomendação de Olá</span><span class="sxs-lookup"><span data-stu-id="ed3e6-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="ed3e6-113">No Olá **recomendações** painel, selecione **deteção de ameaças e ativar a auditoria em servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="ed3e6-114">Esta ação abre Olá **deteção de ameaças e ativar a auditoria em servidores SQL** painel.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-114">This opens hello **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Ativar a auditoria em servidores SQL][1]
2. <span data-ttu-id="ed3e6-116">Selecione uma SQL server tooenable auditoria e deteção de ameaças no.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-116">Select a SQL server tooenable auditing and threat detection on.</span></span> <span data-ttu-id="ed3e6-117">Esta ação abre Olá **a deteção de ameaças e auditoria** painel.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="ed3e6-118">No Olá **a deteção de ameaças e auditoria** painel, selecione **ON** em **auditoria**.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Ativar definições de auditoria][2]
4. <span data-ttu-id="ed3e6-120">Siga os passos Olá [Olá, a auditoria de base de dados SQL no portal do Azure](../sql-database/sql-database-auditing-portal.md) armazenamento tooconfigure onde serão armazenados os registos de auditoria.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-120">Follow hello steps in [SQL database auditing in hello Azure portal](../sql-database/sql-database-auditing-portal.md) tooconfigure storage where your audit logs will be stored.</span></span> <span data-ttu-id="ed3e6-121">Olá conta de armazenamento da subscrição para recolha de dados é conta do storage predefinida Olá.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-121">hello subscription's storage account for data collection is hello default storage account.</span></span>
5. <span data-ttu-id="ed3e6-122">Siga os passos Olá [começar com deteção de ameaças de base de dados do SQL Server](../sql-database/sql-database-threat-detection.md) tooturn no e configurar a deteção de ameaças e a lista de Olá tooconfigure de e-mails que vão receber alertas de segurança mediante a deteção de atividades anómalas.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-122">Follow hello steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="ed3e6-123">Consultar também</span><span class="sxs-lookup"><span data-stu-id="ed3e6-123">See also</span></span>
<span data-ttu-id="ed3e6-124">Este artigo mostrou como tooimplement Olá recomendação do Centro de segurança "Ativar a auditoria e Deteção em SQL servers de ameaças."</span><span class="sxs-lookup"><span data-stu-id="ed3e6-124">This article showed you how tooimplement hello Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="ed3e6-125">toolearn mais informações sobre a proteger a sua base de dados do SQL Server, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="ed3e6-125">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="ed3e6-126">Securing your SQL Database (Proteger a sua Base de Dados SQL)</span><span class="sxs-lookup"><span data-stu-id="ed3e6-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="ed3e6-127">toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="ed3e6-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="ed3e6-128">[Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) – Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ed3e6-129">[Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) – Saiba como recomendações ajudam a proteger os seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ed3e6-130">[Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="ed3e6-131">[Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e respondeu.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ed3e6-132">[Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="ed3e6-133">[FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ed3e6-134">[Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) -obter Olá mais recentes notícias de segurança do Azure e informações.</span><span class="sxs-lookup"><span data-stu-id="ed3e6-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
