---
title: "aaaAssign um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory | Microsoft Docs"
description: "Como tooselect um tooassign de aplicação empresarial um tooit de utilizador ou grupo no Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="0c90a-103">Atribuir um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c90a-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="0c90a-104">É fácil tooassign um utilizador ou um aplicações da empresa tooyour grupo no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0c90a-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0c90a-105">Tem de ter Olá as permissões adequadas toomanage Olá de aplicações e tem de ser um administrador global para o diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="0c90a-106">Como atribuir acesso de utilizador tooan aplicações de empresa?</span><span class="sxs-lookup"><span data-stu-id="0c90a-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="0c90a-107">Inicie sessão no toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="0c90a-108">Selecione **mais serviços**, introduza Azure Active Directory na caixa de texto Olá e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="0c90a-109">No Olá **Azure Active Directory - *directoryname***  painel (ou seja, Olá do Azure AD painel diretório Olá estiver a gerir), selecione **aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Aplicações da empresa ao abrir](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="0c90a-111">No Olá **aplicações empresariais** painel, selecione **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="0c90a-112">Verá uma lista de aplicações de Olá que pode gerir.</span><span class="sxs-lookup"><span data-stu-id="0c90a-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="0c90a-113">No Olá **aplicações da empresa - todas as aplicações** painel, selecione uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="0c90a-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="0c90a-114">No Olá ***appname*** painel (ou seja, Olá painel com o nome Olá Olá aplicação selecionada no título de Olá), selecione **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Selecionar Olá todos os comandos de aplicações](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="0c90a-116">No Olá ***appname*** **-atribuição de grupos de & utilizador** painel, selecione de Olá **adicionar** comando.</span><span class="sxs-lookup"><span data-stu-id="0c90a-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="0c90a-117">No Olá **adicionar atribuição** painel, selecione **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Atribuir um utilizador ou grupo toohello uma aplicação](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="0c90a-119">No Olá **utilizadores e grupos** painel, selecione um ou mais utilizadores ou grupos de Olá lista e, em seguida, selecione Olá **selecione** botão na Olá parte inferior do painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="0c90a-120">No Olá **adicionar atribuição** painel, selecione **função**.</span><span class="sxs-lookup"><span data-stu-id="0c90a-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="0c90a-121">Em seguida, no Olá **selecionar função** painel, selecione um toohello de tooapply função selecionado de utilizadores ou grupos e, em seguida, selecione Olá **OK** botão na Olá parte inferior do painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="0c90a-122">No Olá **adicionar atribuição** painel, selecione de Olá **atribuir** botão na Olá parte inferior do painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c90a-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="0c90a-123">Olá atribuídos a utilizadores ou grupos serão tem permissões de Olá definidas pela função selecionada de Olá para esta aplicação empresarial.</span><span class="sxs-lookup"><span data-stu-id="0c90a-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c90a-124">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0c90a-124">Next steps</span></span>
* [<span data-ttu-id="0c90a-125">Ver todos os meus grupos</span><span class="sxs-lookup"><span data-stu-id="0c90a-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="0c90a-126">Remover uma atribuição de utilizador ou grupo a partir de uma aplicação empresarial</span><span class="sxs-lookup"><span data-stu-id="0c90a-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="0c90a-127">Desativar o utilizador inícios de sessão para uma aplicação empresarial</span><span class="sxs-lookup"><span data-stu-id="0c90a-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="0c90a-128">Alterar o nome de Olá ou logótipo de uma aplicação empresarial</span><span class="sxs-lookup"><span data-stu-id="0c90a-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
