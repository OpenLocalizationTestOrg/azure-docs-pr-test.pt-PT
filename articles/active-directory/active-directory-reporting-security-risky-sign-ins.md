---
title: "relatório de inícios de sessão aaaRisky no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Saiba mais sobre Olá arriscados inícios de sessão de relatórios no portal do Azure Active Directory Olá"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="93752-103">Relatório de risco inícios de sessão no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="93752-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="93752-104">Com Olá relatórios de segurança no Azure Active Directory (Azure AD) pode obter informações sobre a probabilidade de Olá de contas de utilizador comprometidas no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="93752-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="93752-105">Azure AD Deteta suspeitas ações que estão relacionados tooyour contas de utilizador.</span><span class="sxs-lookup"><span data-stu-id="93752-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="93752-106">Para cada ação detetada, é criado um registo denominado *evento de risco*.</span><span class="sxs-lookup"><span data-stu-id="93752-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="93752-107">Para obter mais detalhes, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="93752-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="93752-108">Olá detetou eventos de risco são toocalculate utilizado:</span><span class="sxs-lookup"><span data-stu-id="93752-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="93752-109">**Inícios de sessão arriscados** -um risco início de sessão é um indicador para uma tentativa de início de sessão que poderão ter sido executada por alguém que não é proprietário legítimos Olá uma conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="93752-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="93752-110">Para obter mais detalhes, veja [Inícios de sessão de risco](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="93752-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="93752-111">**Utilizadores sinalizados para risco** – Um utilizador de risco é um indicador de uma conta de utilizador que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="93752-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="93752-112">Para obter mais detalhes, veja [Utilizadores sinalizados para risco](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="93752-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="93752-113">No [Olá portal do Azure](https://portal.azure.com), pode encontrar os relatórios de segurança de Olá no Olá **do Azure Active Directory** painel no Olá **segurança** secção.</span><span class="sxs-lookup"><span data-stu-id="93752-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="93752-115">As licenças do Azure AD tem tooaccess um relatório de segurança?</span><span class="sxs-lookup"><span data-stu-id="93752-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="93752-116">Todas as edições do Azure Active Directory disponibilizam os relatórios de inícios de sessão de risco.</span><span class="sxs-lookup"><span data-stu-id="93752-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="93752-117">No entanto, o nível de Olá de granularidade do relatório varia entre edições Olá:</span><span class="sxs-lookup"><span data-stu-id="93752-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="93752-118">No Olá **edições gratuito do Azure Active Directory e Basic**, já a obter uma lista do risco de inícios de sessão.</span><span class="sxs-lookup"><span data-stu-id="93752-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="93752-119">Olá **do Azure Active Directory Premium 1** edição expande este modelo, permitindo também tooexamine algumas das Olá subjacente eventos de risco que foram detetados para cada relatório.</span><span class="sxs-lookup"><span data-stu-id="93752-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="93752-120">Olá **do Azure Active Directory Premium 2** edição fornece-lhe Olá mais informações detalhadas sobre todos os eventos de risco subjacente e também lhe permite tooconfigure as políticas de segurança que respondam automaticamente tooconfigured níveis de risco.</span><span class="sxs-lookup"><span data-stu-id="93752-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="93752-121">Edição gratuita e básica do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93752-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="93752-122">as edições basic e Olá do Azure Active Directory gratuito lhe fornecem uma lista de risco inícios de sessão que foram detetados para os seus utilizadores.</span><span class="sxs-lookup"><span data-stu-id="93752-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="93752-123">Este relatório lista:</span><span class="sxs-lookup"><span data-stu-id="93752-123">This report lists:</span></span>

- <span data-ttu-id="93752-124">**Utilizador** - hello nome de utilizador de Olá que foi utilizado durante a operação de início de sessão Olá</span><span class="sxs-lookup"><span data-stu-id="93752-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="93752-125">**IP** -Olá endereço IP do dispositivo Olá que foi utilizado tooconnect tooAzure do Active Directory</span><span class="sxs-lookup"><span data-stu-id="93752-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="93752-126">**Localização** -localização Olá utilizado tooconnect tooAzure do Active Directory</span><span class="sxs-lookup"><span data-stu-id="93752-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="93752-127">**Hora de início de sessão** -tempo Olá quando Olá início de sessão foi efetuado</span><span class="sxs-lookup"><span data-stu-id="93752-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="93752-128">**Estado** -Olá Estado Olá início de sessão</span><span class="sxs-lookup"><span data-stu-id="93752-128">**Status** - hello status of hello sign-in</span></span>


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="93752-130">Com base na sua investigação de Olá arriscados início de sessão, pode fornecer comentários tooAzure Active Directory no formulário de Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="93752-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="93752-131">Resolver</span><span class="sxs-lookup"><span data-stu-id="93752-131">Resolve</span></span>
- <span data-ttu-id="93752-132">Marcar como falso positivo</span><span class="sxs-lookup"><span data-stu-id="93752-132">Mark as false positive</span></span>
- <span data-ttu-id="93752-133">Ignorar</span><span class="sxs-lookup"><span data-stu-id="93752-133">Ignore</span></span>
- <span data-ttu-id="93752-134">Reativar</span><span class="sxs-lookup"><span data-stu-id="93752-134">Reactivate</span></span>

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="93752-136">Para obter mais detalhes, veja [Fechar eventos de risco manualmente](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="93752-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="93752-137">Este relatório disponibiliza uma opção para:</span><span class="sxs-lookup"><span data-stu-id="93752-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="93752-138">Pesquisar recursos</span><span class="sxs-lookup"><span data-stu-id="93752-138">Searh resources</span></span>
- <span data-ttu-id="93752-139">Transferência de dados do relatório Olá</span><span class="sxs-lookup"><span data-stu-id="93752-139">Download hello report data</span></span>


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="93752-141">Edições premium do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93752-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="93752-142">relatório de inícios de sessão arriscados Olá nas edições de premium do Azure Active Directory Olá fornece-lhe:</span><span class="sxs-lookup"><span data-stu-id="93752-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="93752-143">Agregar informações sobre Olá [tipos de eventos de risco](active-directory-identity-protection-risk-events.md) que foram detetadas</span><span class="sxs-lookup"><span data-stu-id="93752-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="93752-144">Um relatório de Olá toodownload opção</span><span class="sxs-lookup"><span data-stu-id="93752-144">An option toodownload hello report</span></span>


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="93752-146">Ao selecionar um evento de risco, obtém uma vista de relatório detalhado para este evento de risco que lhe permite:</span><span class="sxs-lookup"><span data-stu-id="93752-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="93752-147">Uma opção tooconfigure um [política de remediação de risco do utilizador](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="93752-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="93752-148">Reveja a linha cronológica de deteção de Olá para eventos de risco Olá</span><span class="sxs-lookup"><span data-stu-id="93752-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="93752-149">Reveja uma lista de utilizadores para os quais foi detetado este evento de risco</span><span class="sxs-lookup"><span data-stu-id="93752-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="93752-150">[Feche manualmente eventos de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reative um evento de risco fechado manualmente.</span><span class="sxs-lookup"><span data-stu-id="93752-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="93752-152">Ao selecionar um utilizador, obtém uma vista de relatório detalhado para este utilizador que lhe permite:</span><span class="sxs-lookup"><span data-stu-id="93752-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="93752-153">Abrir Olá que ver todos os inícios de sessão</span><span class="sxs-lookup"><span data-stu-id="93752-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="93752-154">Repor palavra-passe do utilizador Olá</span><span class="sxs-lookup"><span data-stu-id="93752-154">Reset hello user's password</span></span>

- <span data-ttu-id="93752-155">Dispensar todos os eventos</span><span class="sxs-lookup"><span data-stu-id="93752-155">Dismiss all events</span></span>

- <span data-ttu-id="93752-156">Investigue os eventos de risco comunicado para utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="93752-156">Investigate reported risk events for hello user.</span></span> 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="93752-158">tooinvestigate um evento de risco, selecione um Olá na lista.</span><span class="sxs-lookup"><span data-stu-id="93752-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="93752-159">Esta ação abre Olá **detalhes** painel para este evento de risco.</span><span class="sxs-lookup"><span data-stu-id="93752-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="93752-160">No Olá **detalhes** painel, tiver Olá opção tooeither [fechar manualmente um evento de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reativar um evento de risco fechado manualmente.</span><span class="sxs-lookup"><span data-stu-id="93752-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="93752-162">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="93752-162">Next steps</span></span>

- <span data-ttu-id="93752-163">Para obter mais informações sobre o Azure Active Directory Identity Protection, veja [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="93752-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

