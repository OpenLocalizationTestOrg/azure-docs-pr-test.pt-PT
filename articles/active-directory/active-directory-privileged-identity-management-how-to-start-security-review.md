---
title: "aaaHow toostart uma revisão do acesso | Microsoft Docs"
description: "Saiba como toocreate acesso rever de identidades privilegiadas com Olá aplicação Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="b1ff8-103">Como toostart acesso consultar no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="b1ff8-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="b1ff8-104">Atribuições de função ficam "obsoletas" quando os utilizadores com acesso privilegiado que não precisam de já.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="b1ff8-105">Na ordem de risco Olá tooreduce associado estas atribuições de funções obsoletos, os administradores de com função privilegiada regularmente devem rever funções Olá que atribuiu utilizadores.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="b1ff8-106">Este documento aborda os passos de Olá para iniciar uma revisão do acesso no Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="b1ff8-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="b1ff8-107">Iniciar uma revisão do acesso</span><span class="sxs-lookup"><span data-stu-id="b1ff8-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="b1ff8-108">Se ainda não adicionou o dashboard de tooyour de aplicações Olá PIM em Olá portal do Azure, consulte passos Olá [introdução ao Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="b1ff8-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="b1ff8-109">Do PIM aplicação principal página Olá, existem três formas toostart uma revisão do acesso:</span><span class="sxs-lookup"><span data-stu-id="b1ff8-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="b1ff8-110">**Aceder revisões** > **adicionar**</span><span class="sxs-lookup"><span data-stu-id="b1ff8-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="b1ff8-111">**Funções** > **revisão** botão</span><span class="sxs-lookup"><span data-stu-id="b1ff8-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="b1ff8-112">Selecione Olá função específica toobe revistos na lista de funções de Olá > **revisão** botão</span><span class="sxs-lookup"><span data-stu-id="b1ff8-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="b1ff8-113">Quando clica em Olá **rever** botão, hello **iniciar uma revisão do acesso** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="b1ff8-114">Neste painel, está curso tooconfigure Olá Reveja com um nome e tempo limite, escolha um tooreview de função e decidir que executará a revisão Olá.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![Iniciar uma revisão do acesso - captura de ecrã][1]

### <a name="configure-hello-review"></a><span data-ttu-id="b1ff8-116">Configurar revisão Olá</span><span class="sxs-lookup"><span data-stu-id="b1ff8-116">Configure hello review</span></span>
<span data-ttu-id="b1ff8-117">Reveja do toocreate acesso, tem de tooname e defina uma data de início e de fim.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![Configurar revisão - captura de ecrã][2]

<span data-ttu-id="b1ff8-119">Certifique-Olá comprimento Olá rever suficientemente longo para os utilizadores toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="b1ff8-120">Se concluir antes da data de fim de Olá, pode sempre parar a revisão Olá antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="b1ff8-121">Escolha um tooreview de função</span><span class="sxs-lookup"><span data-stu-id="b1ff8-121">Choose a role tooreview</span></span>
<span data-ttu-id="b1ff8-122">Cada revisão centra-se apenas uma função.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-122">Each review focuses on only one role.</span></span> <span data-ttu-id="b1ff8-123">Exceto se tiver iniciado o Olá revisão do acesso a partir do painel de uma função específica, terá agora toochoose uma função.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="b1ff8-124">Navegue demasiado**rever membro da função**</span><span class="sxs-lookup"><span data-stu-id="b1ff8-124">Navigate too**Review role membership**</span></span>
   
    ![Reveja o membro da função - captura de ecrã][3]
2. <span data-ttu-id="b1ff8-126">Escolha uma função Olá lista.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="b1ff8-127">Decidir que executará a revisão Olá</span><span class="sxs-lookup"><span data-stu-id="b1ff8-127">Decide who will perform hello review</span></span>
<span data-ttu-id="b1ff8-128">Existem três opções para executar uma revisão.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-128">There are three options for performing a review.</span></span> <span data-ttu-id="b1ff8-129">Pode atribuir Olá revisão toosomeone toocomplete pessoa, pode fazê-lo por si ou pode fazer com que cada utilizador, reveja os suas próprias acesso.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="b1ff8-130">Navegue demasiado**selecione revisores**</span><span class="sxs-lookup"><span data-stu-id="b1ff8-130">Navigate too**Select reviewers**</span></span>
   
    ![Selecione os revisores - captura de ecrã][4]
2. <span data-ttu-id="b1ff8-132">Escolha uma das opções de Olá:</span><span class="sxs-lookup"><span data-stu-id="b1ff8-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="b1ff8-133">**Selecione revisor**: Utilize esta opção se não souber quem tem acesso.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="b1ff8-134">Com esta opção, pode atribuir proprietário do recurso Olá revisão tooa ou toocomplete do Gestor de grupo.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="b1ff8-135">**Enviar-me**: útil se pretender que toopreview como acesso revê o trabalho ou se quiser tooreview em nome de pessoas que não é possível.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="b1ff8-136">**Membros reveja próprios**: Utilize esta opção toohave Olá utilizadores rever as suas próprias atribuições de funções.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="b1ff8-137">Iniciar Olá revisão</span><span class="sxs-lookup"><span data-stu-id="b1ff8-137">Start hello review</span></span>
<span data-ttu-id="b1ff8-138">Por fim, terá de Olá opção toorequire que os utilizadores forneçam um motivo se estes aprovar o acesso.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="b1ff8-139">Adicionar uma descrição da revisão de Olá se assim o desejar e selecione **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="b1ff8-140">Certifique-se de que permite aos utilizadores saber que existe uma revisão do acesso a aguardar para os mesmos e apresentar [como tooperform rever um acesso](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="b1ff8-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="b1ff8-141">Gerir a revisão do acesso Olá</span><span class="sxs-lookup"><span data-stu-id="b1ff8-141">Manage hello access review</span></span>
<span data-ttu-id="b1ff8-142">Pode controlar o progresso de Olá como revisores Olá concluir as revisões em Olá dashboard do Azure AD PIM, no Olá acesso revê secção.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="b1ff8-143">Sem direitos de acesso serão alterados no diretório de Olá até [concluir a revisão Olá](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="b1ff8-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="b1ff8-144">Até que o período de avaliação de Olá está acima, pode notificar utilizadores toocomplete respetiva revisão ou parar Olá revisão numa fase inicial do acesso Olá revê secção.</span><span class="sxs-lookup"><span data-stu-id="b1ff8-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="b1ff8-145">Tabela PIM de conteúdo</span><span class="sxs-lookup"><span data-stu-id="b1ff8-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
