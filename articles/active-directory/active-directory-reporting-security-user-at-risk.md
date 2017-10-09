---
title: "aaaUsers sinalizados para o relatório de segurança de risco no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Saiba mais sobre os utilizadores Olá sinalizados para o relatório de segurança de risco no portal do Azure Active Directory Olá"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="c9244-103">Utilizadores sinalizados para o relatório de segurança de risco no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="c9244-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="c9244-104">Com os relatórios de segurança de Olá no Olá Azure Active Directory (Azure AD), pode obter informações acerca da probabilidade Olá de contas de utilizador comprometidas no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="c9244-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="c9244-105">Azure Active Directory Deteta suspeitas ações que estão relacionados tooyour contas de utilizador.</span><span class="sxs-lookup"><span data-stu-id="c9244-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="c9244-106">Para cada ação detetada, é criado um registo denominado *evento de risco*.</span><span class="sxs-lookup"><span data-stu-id="c9244-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="c9244-107">Para obter mais informações, consulte [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="c9244-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="c9244-108">Olá detetou eventos de risco são toocalculate utilizado:</span><span class="sxs-lookup"><span data-stu-id="c9244-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="c9244-109">**Inícios de sessão arriscados** -um risco início de sessão é um indicador para uma tentativa de início de sessão que poderão ter sido executada por alguém que não é proprietário legítimos Olá uma conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="c9244-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="c9244-110">Para obter mais informações, veja [Inícios de sessão arriscados](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="c9244-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="c9244-111">**Utilizadores sinalizados para risco** – Um utilizador de risco é um indicador de uma conta de utilizador que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="c9244-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="c9244-112">Para obter mais informações, veja [Utilizadores sinalizados para risco](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="c9244-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="c9244-113">Olá portal do Azure, pode encontrar os relatórios de segurança de Olá no Olá **do Azure Active Directory** painel no Olá **segurança** secção.</span><span class="sxs-lookup"><span data-stu-id="c9244-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="c9244-115">As licenças do Azure AD tem tooaccess um relatório de segurança?</span><span class="sxs-lookup"><span data-stu-id="c9244-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="c9244-116">Todas as edições do Azure Active Directory disponibilizam os relatórios de utilizadores sinalizados para risco.</span><span class="sxs-lookup"><span data-stu-id="c9244-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="c9244-117">No entanto, o nível de Olá de granularidade do relatório varia entre edições Olá:</span><span class="sxs-lookup"><span data-stu-id="c9244-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="c9244-118">No Olá **edições gratuito do Azure Active Directory e Basic**, já a obter uma lista de utilizadores sinalizados para risco.</span><span class="sxs-lookup"><span data-stu-id="c9244-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="c9244-119">Olá **do Azure Active Directory Premium 1** edição expande este modelo, permitindo também tooexamine algumas das Olá subjacente eventos de risco que foram detetados para cada relatório.</span><span class="sxs-lookup"><span data-stu-id="c9244-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="c9244-120">Olá **do Azure Active Directory Premium 2** edição fornece-lhe Olá informações mais detalhadas sobre todos os eventos de risco subjacente e permite-lhe tooconfigure as políticas de segurança que respondam automaticamente tooconfigured risco níveis.</span><span class="sxs-lookup"><span data-stu-id="c9244-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="c9244-121">Edição gratuita e básica do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9244-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="c9244-122">os utilizadores Olá sinalizados para o relatório de risco nas edições de livres e básicos do Azure Active Directory de Olá fornece uma lista de contas de utilizador que poderá ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="c9244-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="c9244-124">Seleção de um utilizador abre o painel de dados de utilizador relacionadas Olá.</span><span class="sxs-lookup"><span data-stu-id="c9244-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="c9244-125">Para os utilizadores que estão em risco, pode rever o histórico de início de sessão do utilizador Olá e repor a palavra-passe de Olá, se necessário.</span><span class="sxs-lookup"><span data-stu-id="c9244-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="c9244-127">Esta caixa de diálogo disponibiliza uma opção para:</span><span class="sxs-lookup"><span data-stu-id="c9244-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="c9244-128">Transferir Olá relatório</span><span class="sxs-lookup"><span data-stu-id="c9244-128">Download hello report</span></span>

- <span data-ttu-id="c9244-129">Procurar utilizadores</span><span class="sxs-lookup"><span data-stu-id="c9244-129">Search users</span></span>

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="c9244-131">Edições premium do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9244-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="c9244-132">os utilizadores Olá sinalizados para o relatório de risco nas edições de premium do Azure Active Directory Olá fornece-lhe:</span><span class="sxs-lookup"><span data-stu-id="c9244-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="c9244-133">Uma [lista de contas de utilizador](active-directory-identityprotection.md#users-flagged-for-risk) que poderão ter sido comprometidas</span><span class="sxs-lookup"><span data-stu-id="c9244-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="c9244-134">Agregar informações sobre Olá [tipos de eventos de risco](active-directory-identity-protection-risk-events.md) que foram detetadas</span><span class="sxs-lookup"><span data-stu-id="c9244-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="c9244-135">Um relatório de Olá toodownload opção</span><span class="sxs-lookup"><span data-stu-id="c9244-135">An option toodownload hello report</span></span>

- <span data-ttu-id="c9244-136">Uma opção tooconfigure um [política de remediação de risco do utilizador](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="c9244-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="c9244-138">Ao selecionar um utilizador, obtém uma vista de relatório detalhado para este utilizador que lhe permite:</span><span class="sxs-lookup"><span data-stu-id="c9244-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="c9244-139">Abrir Olá que ver todos os inícios de sessão</span><span class="sxs-lookup"><span data-stu-id="c9244-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="c9244-140">Repor palavra-passe do utilizador Olá</span><span class="sxs-lookup"><span data-stu-id="c9244-140">Reset hello user's password</span></span>

- <span data-ttu-id="c9244-141">Dispensar todos os eventos</span><span class="sxs-lookup"><span data-stu-id="c9244-141">Dismiss all events</span></span>

- <span data-ttu-id="c9244-142">Investigue os eventos de risco comunicado para utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="c9244-142">Investigate reported risk events for hello user.</span></span> 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="c9244-144">tooinvestigate um evento de risco, selecione um Olá do Olá lista tooopen **detalhes** painel para este evento de risco.</span><span class="sxs-lookup"><span data-stu-id="c9244-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="c9244-145">No Olá **detalhes** painel, tiver Olá opção tooeither [fechar manualmente um evento de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reativar um evento de risco fechado manualmente.</span><span class="sxs-lookup"><span data-stu-id="c9244-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="c9244-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c9244-147">Next steps</span></span>

- <span data-ttu-id="c9244-148">Para obter mais informações sobre o Azure Active Directory Identity Protection, veja [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="c9244-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

