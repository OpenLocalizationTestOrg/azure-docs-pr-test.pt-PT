---
title: "aaaUsing tooSaaS de acesso toomanage um grupo aplicações | Microsoft Docs"
description: "Como toouse grupos no Azure Active Directory Premium ou Basic tooassign acedam a aplicações de tooSaaS que estão integradas no Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="9f14e-103">Utilizar um grupo toomanage acesso tooSaaS aplicações</span><span class="sxs-lookup"><span data-stu-id="9f14e-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="9f14e-104">Utilizar o Azure Active Directory (Azure AD) com uma licença do Azure AD Premium ou Basic do Azure AD, pode utilizar grupos tooassign acesso tooa aplicação SaaS que está integrada com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f14e-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="9f14e-105">Por exemplo, se pretender que o acesso de tooassign para Olá marketing departamento toouse cinco diferentes aplicações SaaS, pode criar um grupo que contenha Olá os utilizadores do departamento de marketing Olá e, em seguida, atribuir esse grupo toothese cinco aplicações SaaS que são necessária pelo departamento de marketing Olá.</span><span class="sxs-lookup"><span data-stu-id="9f14e-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="9f14e-106">Desta forma pode poupar tempo ao gerir associação Olá Olá marketing departamento num único local.</span><span class="sxs-lookup"><span data-stu-id="9f14e-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="9f14e-107">Os utilizadores, em seguida, são atribuídos toohello aplicação quando estes são adicionados como membros do grupo de marketing Olá, e as respetivas atribuições removidas da aplicação Olá quando estes são removidos de Olá grupo de marketing.</span><span class="sxs-lookup"><span data-stu-id="9f14e-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f14e-108">A Microsoft recomenda que gere o Azure AD através de Olá [Centro de administração do Azure AD](https://aad.portal.azure.com) no Olá portal do Azure em vez de utilizar Olá portal clássico do Azure referenciado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9f14e-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="9f14e-109">Esta capacidade pode ser utilizada com centenas de aplicações que pode adicionar a partir de dentro de Olá Galeria de aplicações do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f14e-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="9f14e-110">**acesso de tooassign para uma aplicação SaaS de tooa de grupo**</span><span class="sxs-lookup"><span data-stu-id="9f14e-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="9f14e-111">No Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory** na barra de navegação de Olá no Olá lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="9f14e-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="9f14e-112">Selecione Olá **diretório** separador e diretório Olá, em seguida, abra em que pretende acesso tooassign para um grupo de tooa aplicação SaaS.</span><span class="sxs-lookup"><span data-stu-id="9f14e-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="9f14e-113">Selecione Olá **aplicações** separador. Selecione uma aplicação que adicionou de Olá Galeria de aplicações e, em seguida, clique em Olá **utilizadores e grupos** separador.</span><span class="sxs-lookup"><span data-stu-id="9f14e-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="9f14e-114">No Olá **utilizadores e grupos** separador, Olá **começadas** campo, introduza o nome de Olá de Olá toowhich de grupo que pretende que o acesso de tooassign e, em seguida, selecione Olá marca de verificação no canto superior direito da Olá.</span><span class="sxs-lookup"><span data-stu-id="9f14e-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="9f14e-115">Basta tootype Olá primeiro faz parte do nome do grupo.</span><span class="sxs-lookup"><span data-stu-id="9f14e-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="9f14e-116">Selecione o grupo de Olá, em seguida, em seguida, selecione Olá **atribuir acesso** botão.</span><span class="sxs-lookup"><span data-stu-id="9f14e-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="9f14e-117">Selecione **Sim** quando for apresentada a mensagem de confirmação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f14e-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="9f14e-118">Filiações aninhadas não são suportadas para a atribuição baseada em grupo tooapplications neste momento.</span><span class="sxs-lookup"><span data-stu-id="9f14e-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="9f14e-119">Também pode ver que utilizadores são atribuídos a aplicação toohello, diretamente ou através da associação num grupo.</span><span class="sxs-lookup"><span data-stu-id="9f14e-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="9f14e-120">toodo Olá, alteração **Mostrar a lista pendente de 'Grupos'** demasiado**'Todos os utilizadores'**.</span><span class="sxs-lookup"><span data-stu-id="9f14e-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="9f14e-121">lista de Olá mostra os utilizadores no diretório de Olá e se deve ou não cada utilizador atribuído toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="9f14e-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="9f14e-122">lista de Olá também mostra se os utilizadores de Olá atribuído são atribuídos diretamente aplicação toohello (tipo de atribuição apresentada como 'Direta') ou em virtude da associação de grupo (apresentada como 'Herdado'. tipo de atribuição)</span><span class="sxs-lookup"><span data-stu-id="9f14e-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="9f14e-123">Pode ver Olá utilizadores e separador grupos apenas depois de ter ativado o Azure AD Premium ou Basic do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f14e-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="9f14e-124">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9f14e-124">Next steps</span></span>
<span data-ttu-id="9f14e-125">Estes artigos fornecem informações adicionais acerca do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9f14e-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="9f14e-126">Gerir o acesso tooresources com grupos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f14e-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="9f14e-127">Índice de Artigos da Gestão da Aplicação no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f14e-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="9f14e-128">Cmdlets do Azure Active Directory para configurar definições de grupo</span><span class="sxs-lookup"><span data-stu-id="9f14e-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="9f14e-129">O que é o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f14e-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="9f14e-130">Integrar as identidades no local ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f14e-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
