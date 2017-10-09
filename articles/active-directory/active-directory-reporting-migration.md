---
title: "atividade aaaFind relatórios no portal do Azure de Olá | Microsoft Docs"
description: "Saiba como toofind atividade do Azure Active Directory relatórios no Olá portal do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="0111c-103">Localizar os relatórios de atividade no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0111c-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="0111c-104">Se estiver a mover de Olá toohello de portal clássico do Azure portal do Azure, obtenha uma nova vista de olhos registos de atividade do Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0111c-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="0111c-105">Num recente [blogue](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), vamos explicar como pode ver os registos de atividade no contexto de Olá do recurso de Olá está a trabalhar no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0111c-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="0111c-106">Neste artigo, vamos descrever como toofind relatórios que utilizou no portal clássico do Azure no portal do Azure de Olá de Olá.</span><span class="sxs-lookup"><span data-stu-id="0111c-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="0111c-107">Novidades</span><span class="sxs-lookup"><span data-stu-id="0111c-107">What's new</span></span>

<span data-ttu-id="0111c-108">Relatórios no portal clássico do Azure de Olá estão separados em categorias:</span><span class="sxs-lookup"><span data-stu-id="0111c-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="0111c-109">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="0111c-109">Security reports</span></span>
2.  <span data-ttu-id="0111c-110">Relatórios de atividade</span><span class="sxs-lookup"><span data-stu-id="0111c-110">Activity reports</span></span>
3.  <span data-ttu-id="0111c-111">Relatórios de aplicação integrada</span><span class="sxs-lookup"><span data-stu-id="0111c-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="0111c-112">Atividade e os relatórios de aplicação integrada</span><span class="sxs-lookup"><span data-stu-id="0111c-112">Activity and integrated app reports</span></span>

<span data-ttu-id="0111c-113">Para baseado no contexto de relatórios no Olá portal do Azure, os relatórios existentes são intercalados numa única vista.</span><span class="sxs-lookup"><span data-stu-id="0111c-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="0111c-114">Uma API único, subjacente fornece Olá dados toohello.</span><span class="sxs-lookup"><span data-stu-id="0111c-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="0111c-115">toosee esta vista, no Olá **do Azure Active Directory** painel, em **ATIVIDADE**, selecione **registos de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="0111c-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="0111c-116">![Registos de auditoria](./media/active-directory-reporting-migration/482.png "Registos de auditoria")</span><span class="sxs-lookup"><span data-stu-id="0111c-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="0111c-117">Olá, os seguintes relatórios é consolidado nesta vista:</span><span class="sxs-lookup"><span data-stu-id="0111c-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="0111c-118">Relatório de auditoria</span><span class="sxs-lookup"><span data-stu-id="0111c-118">Audit report</span></span>
-   <span data-ttu-id="0111c-119">Atividade de reposição de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="0111c-119">Password reset activity</span></span>
-   <span data-ttu-id="0111c-120">Atividade de registo de reposição de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="0111c-120">Password reset registration activity</span></span>
-   <span data-ttu-id="0111c-121">Atividade de grupos self-service</span><span class="sxs-lookup"><span data-stu-id="0111c-121">Self-service groups activity</span></span>
-   <span data-ttu-id="0111c-122">Alterações de nome de grupo do Office 365</span><span class="sxs-lookup"><span data-stu-id="0111c-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="0111c-123">Atividade de aprovisionamento de contas</span><span class="sxs-lookup"><span data-stu-id="0111c-123">Account provisioning activity</span></span>
-   <span data-ttu-id="0111c-124">Estado de rollover de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="0111c-124">Password rollover status</span></span>
-   <span data-ttu-id="0111c-125">Erros de aprovisionamento de contas</span><span class="sxs-lookup"><span data-stu-id="0111c-125">Account provisioning errors</span></span>


<span data-ttu-id="0111c-126">Olá relatório de utilização da aplicação foi melhorado e está incluído no Olá **inícios de sessão** vista.</span><span class="sxs-lookup"><span data-stu-id="0111c-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="0111c-127">toosee esta vista, no Olá **do Azure Active Directory** painel, em **ATIVIDADE**, selecione **inícios de sessão**.</span><span class="sxs-lookup"><span data-stu-id="0111c-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="0111c-128">![Vista de inícios de sessão](./media/active-directory-reporting-migration/483.png "ver inícios de sessão")</span><span class="sxs-lookup"><span data-stu-id="0111c-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="0111c-129">Olá **inícios de sessão** vista inclui todos os utilizadores inícios de sessão. Pode utilizar estas informações de utilização de aplicação de tooget de informações.</span><span class="sxs-lookup"><span data-stu-id="0111c-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="0111c-130">Também pode ver informações de utilização da aplicação no Olá **aplicações empresariais** descrição geral, no Olá **GERIR** secção.</span><span class="sxs-lookup"><span data-stu-id="0111c-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="0111c-131">![As aplicações empresariais](./media/active-directory-reporting-migration/484.png "aplicações da empresa")</span><span class="sxs-lookup"><span data-stu-id="0111c-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="0111c-132">Aceder a um relatório específico</span><span class="sxs-lookup"><span data-stu-id="0111c-132">Access a specific report</span></span>

<span data-ttu-id="0111c-133">Embora Olá portal do Azure oferece uma vista única, também pode ver relatórios específicos.</span><span class="sxs-lookup"><span data-stu-id="0111c-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="0111c-134">Registos de auditoria</span><span class="sxs-lookup"><span data-stu-id="0111c-134">Audit logs</span></span>

<span data-ttu-id="0111c-135">Em comentários de toocustomer de resposta, no Olá portal do Azure, pode utilizar avançada filtragem tooaccess Olá de dados que pretende.</span><span class="sxs-lookup"><span data-stu-id="0111c-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="0111c-136">É um filtro pode utilizar um *categoria de atividade*, que apresenta uma lista de tipos diferentes de Olá da atividade de registo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0111c-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="0111c-137">toonarrow resulta toowhat que procura, pode selecionar uma categoria.</span><span class="sxs-lookup"><span data-stu-id="0111c-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="0111c-138">Por exemplo, se estiver interessado apenas em atividades reposições de relacionados tooself de palavra-passe, pode escolher Olá **gestão de palavras-passe Self-Service** categoria.</span><span class="sxs-lookup"><span data-stu-id="0111c-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="0111c-139">categorias Olá que vir baseiam-se no recurso de Olá que está a trabalhar.</span><span class="sxs-lookup"><span data-stu-id="0111c-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="0111c-140">![Opções de categorias na página de registos de auditoria de filtro de Olá](./media/active-directory-reporting-migration/06.png "opções de categorias na página de registos de auditoria de filtro de Olá")</span><span class="sxs-lookup"><span data-stu-id="0111c-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="0111c-141">Categorias de atividade incluem:</span><span class="sxs-lookup"><span data-stu-id="0111c-141">Activity categories include:</span></span>

- <span data-ttu-id="0111c-142">Diretório do Núcleo</span><span class="sxs-lookup"><span data-stu-id="0111c-142">Core Directory</span></span>
- <span data-ttu-id="0111c-143">Gestão de Palavra-passe Personalizada</span><span class="sxs-lookup"><span data-stu-id="0111c-143">Self-service Password Management</span></span>
- <span data-ttu-id="0111c-144">Gestão de Grupos Personalizada</span><span class="sxs-lookup"><span data-stu-id="0111c-144">Self-service Group Management</span></span>
- <span data-ttu-id="0111c-145">Aprovisionamento de Contas</span><span class="sxs-lookup"><span data-stu-id="0111c-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="0111c-146">Utilização da aplicação</span><span class="sxs-lookup"><span data-stu-id="0111c-146">Application usage</span></span>

<span data-ttu-id="0111c-147">tooview detalhes sobre a utilização de aplicação para todas as aplicações ou para uma única aplicação em **ATIVIDADE**, selecione **inícios de sessão**. os resultados de Olá toonarrow, pode filtrar por nome de utilizador ou nome da aplicação.</span><span class="sxs-lookup"><span data-stu-id="0111c-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="0111c-148">![Página de início de sessão de eventos de filtro](./media/active-directory-reporting-migration/07.png "página Eventos de início de sessão de filtragem")</span><span class="sxs-lookup"><span data-stu-id="0111c-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="0111c-149">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="0111c-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="0111c-150">Relatórios de atividade anómala do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0111c-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="0111c-151">Segurança de atividade anómala do Azure AD relatórios a partir do portal clássico do Azure de Olá foram consolidado tooprovide-lhe uma, vista central.</span><span class="sxs-lookup"><span data-stu-id="0111c-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="0111c-152">Esta vista mostra todos os eventos de risco relacionado com a segurança de que o do Azure AD pode detetar e comunicar.</span><span class="sxs-lookup"><span data-stu-id="0111c-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="0111c-153">Olá, a tabela seguinte apresenta uma lista de relatórios de segurança de atividade anómala Olá do Azure AD e tipos de eventos de risco correspondentes no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0111c-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="0111c-154">Relatório de atividade anómala do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0111c-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="0111c-155">Tipo de evento de risco de proteção de identidade</span><span class="sxs-lookup"><span data-stu-id="0111c-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="0111c-156">Utilizadores com credenciais obtidas ilicitamente</span><span class="sxs-lookup"><span data-stu-id="0111c-156">Users with leaked credentials</span></span> | <span data-ttu-id="0111c-157">Credenciais obtidas ilicitamente</span><span class="sxs-lookup"><span data-stu-id="0111c-157">Leaked credentials</span></span> |
| <span data-ttu-id="0111c-158">Atividades irregulares de início de sessão</span><span class="sxs-lookup"><span data-stu-id="0111c-158">Irregular sign-in activity</span></span> | <span data-ttu-id="0111c-159">Impossível tooatypical localizações</span><span class="sxs-lookup"><span data-stu-id="0111c-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="0111c-160">Inícios de sessão de dispositivos possivelmente infetados</span><span class="sxs-lookup"><span data-stu-id="0111c-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="0111c-161">Inícios de sessão a partir de dispositivos infetados</span><span class="sxs-lookup"><span data-stu-id="0111c-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="0111c-162">Inícios de sessão de fontes desconhecidas</span><span class="sxs-lookup"><span data-stu-id="0111c-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="0111c-163">Inícios de sessão de endereços IP anónimos</span><span class="sxs-lookup"><span data-stu-id="0111c-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="0111c-164">Inícios de sessão de endereços IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="0111c-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="0111c-165">Inícios de sessão de endereços IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="0111c-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="0111c-166">Inícios de sessão a partir de localizações desconhecidas</span><span class="sxs-lookup"><span data-stu-id="0111c-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="0111c-167">Olá segurança do Azure AD atividade anómala os seguintes relatórios não estão incluídos como eventos de risco no Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="0111c-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="0111c-168">Inícios de sessão após várias falhas</span><span class="sxs-lookup"><span data-stu-id="0111c-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="0111c-169">Inícios de sessão de várias localizações geográficas</span><span class="sxs-lookup"><span data-stu-id="0111c-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="0111c-170">Estes relatórios ainda estão disponíveis Olá portal clássico do Azure, mas que vão ser preteridas momento no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="0111c-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="0111c-171">Para obter mais informações, consulte [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="0111c-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="0111c-172">Eventos de risco detetados</span><span class="sxs-lookup"><span data-stu-id="0111c-172">Detected risk events</span></span>

<span data-ttu-id="0111c-173">No portal do Azure Olá, pode aceder a relatórios sobre eventos de risco detetados no Olá **do Azure Active Directory** painel, em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="0111c-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="0111c-174">Eventos de risco detetados são controlados na Olá os seguintes relatórios:</span><span class="sxs-lookup"><span data-stu-id="0111c-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="0111c-175">Utilizadores em risco</span><span class="sxs-lookup"><span data-stu-id="0111c-175">Users at Risk</span></span>
- <span data-ttu-id="0111c-176">Inícios de Sessão de Risco</span><span class="sxs-lookup"><span data-stu-id="0111c-176">Risky Sign-ins</span></span>

<span data-ttu-id="0111c-177">![Relatórios de segurança](./media/active-directory-reporting-migration/04.png "relatórios de segurança")</span><span class="sxs-lookup"><span data-stu-id="0111c-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="0111c-178">Para obter mais informações sobre os relatórios de segurança, consulte:</span><span class="sxs-lookup"><span data-stu-id="0111c-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="0111c-179">Utilizadores no relatório de segurança de risco no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="0111c-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="0111c-180">Risco relatório de inícios de sessão no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="0111c-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="0111c-181">Relatórios de atividade no Olá portal clássico do Azure vs Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0111c-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="0111c-182">tabela de Olá nesta secção apresenta uma lista de relatórios existentes no Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="0111c-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="0111c-183">Também descreve como obter Olá mesmas informações em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0111c-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="0111c-184">tooview todos os dados no Olá de auditoria **do Azure Active Directory** painel, em **ATIVIDADE**, aceda demasiado**registos de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="0111c-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="0111c-185">![Registos de auditoria](./media/active-directory-reporting-migration/61.png "Registos de auditoria")</span><span class="sxs-lookup"><span data-stu-id="0111c-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="0111c-186">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="0111c-186">Azure classic portal</span></span>                 | <span data-ttu-id="0111c-187">toofind no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0111c-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="0111c-188">Registos de auditoria</span><span class="sxs-lookup"><span data-stu-id="0111c-188">Audit logs</span></span>                           | <span data-ttu-id="0111c-189">Para **categoria de atividade**, selecione **Core diretório**.</span><span class="sxs-lookup"><span data-stu-id="0111c-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="0111c-190">Atividade de reposição de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="0111c-190">Password reset activity</span></span>              | <span data-ttu-id="0111c-191">Para **categoria de atividade**, selecione **gestão de palavras-passe Self-Service**.</span><span class="sxs-lookup"><span data-stu-id="0111c-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="0111c-192">Atividade de registo de reposição de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="0111c-192">Password reset registration activity</span></span> | <span data-ttu-id="0111c-193">Para **categoria de atividade**, selecione **gestão de palavras-passe Self-Service**.</span><span class="sxs-lookup"><span data-stu-id="0111c-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="0111c-194">Atividade de grupos self-service</span><span class="sxs-lookup"><span data-stu-id="0111c-194">Self-service groups activity</span></span>         | <span data-ttu-id="0111c-195">Para **categoria de atividade**, selecione **Self-Service de grupo de gestão**.</span><span class="sxs-lookup"><span data-stu-id="0111c-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="0111c-196">Atividade de aprovisionamento de contas</span><span class="sxs-lookup"><span data-stu-id="0111c-196">Account provisioning activity</span></span>        | <span data-ttu-id="0111c-197">Para **categoria de atividade**, selecione **aprovisionamento de utilizador da conta**.</span><span class="sxs-lookup"><span data-stu-id="0111c-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="0111c-198">Estado de rollover de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="0111c-198">Password rollover status</span></span>             | <span data-ttu-id="0111c-199">Para **categoria de atividade**, selecione **Rollover de palavra-passe de aplicação automática**.</span><span class="sxs-lookup"><span data-stu-id="0111c-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="0111c-200">Erros de aprovisionamento de contas</span><span class="sxs-lookup"><span data-stu-id="0111c-200">Account provisioning errors</span></span>          | <span data-ttu-id="0111c-201">Para **categoria de atividade**, selecione **aprovisionamento de utilizador da conta**.</span><span class="sxs-lookup"><span data-stu-id="0111c-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="0111c-202">Alterações de nome de grupo do Office 365</span><span class="sxs-lookup"><span data-stu-id="0111c-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="0111c-203">Para **categoria de atividade**, selecione **gestão de palavras-passe Self-Service**.</span><span class="sxs-lookup"><span data-stu-id="0111c-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="0111c-204">Para **tipo de recurso de atividade**, selecione **grupo**.</span><span class="sxs-lookup"><span data-stu-id="0111c-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="0111c-205">Para **atividade origem**, selecione **grupos do Office 365**.</span><span class="sxs-lookup"><span data-stu-id="0111c-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="0111c-206">Olá tooview **utilização da aplicação** relatório, no Olá **do Azure Active Directory** painel, em **GERIR**, selecione **aplicações da empresa**e, em seguida, selecione **inícios de sessão**.</span><span class="sxs-lookup"><span data-stu-id="0111c-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="0111c-207">![Relatório de inícios de sessão do aplicações empresariais](./media/active-directory-reporting-migration/199.png "relatório Enterprise aplicações inícios de sessão")</span><span class="sxs-lookup"><span data-stu-id="0111c-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="0111c-208">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0111c-208">Next steps</span></span>

<span data-ttu-id="0111c-209">Para obter uma descrição geral de criação de relatórios, consulte Olá [relatórios do Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0111c-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
