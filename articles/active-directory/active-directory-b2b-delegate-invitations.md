---
title: "aaaDelegate convites para colaboração B2B do Azure Active Directory do | Microsoft Docs"
description: "Propriedades de utilizador de colaboração B2B do Active Directory do Azure são configuráveis"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="f6d24-103">Delegar convites para colaboração B2B do Azure Active Directory do</span><span class="sxs-lookup"><span data-stu-id="f6d24-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="f6d24-104">Com a colaboração de empresa-empresa (B2B) do Azure Active Directory (Azure AD), não dispõe de toobe convites de toosend um administrador global.</span><span class="sxs-lookup"><span data-stu-id="f6d24-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="f6d24-105">Em vez disso, pode utilizar as políticas e delegar toousers convites para cujas funções permitam-lhes toosend convites.</span><span class="sxs-lookup"><span data-stu-id="f6d24-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="f6d24-106">É um importante novos forma toodelegate convidado utilizador convites através da função de convidado Inviter Olá.</span><span class="sxs-lookup"><span data-stu-id="f6d24-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="f6d24-107">Função de convidado Inviter</span><span class="sxs-lookup"><span data-stu-id="f6d24-107">Guest Inviter role</span></span>
<span data-ttu-id="f6d24-108">Iremos pode atribuir Olá utilizador tooGuest convites de toosend Inviter função.</span><span class="sxs-lookup"><span data-stu-id="f6d24-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="f6d24-109">Não tem membro toobe convites para do toosend de função de administrador global do Olá.</span><span class="sxs-lookup"><span data-stu-id="f6d24-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="f6d24-110">Por predefinição, os utilizadores regulares podem também invocar Olá convite API a menos que um administrador global desativado convites para os utilizadores regulares.</span><span class="sxs-lookup"><span data-stu-id="f6d24-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="f6d24-111">Um utilizador pode também invocar a API de Olá utilizando Olá portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6d24-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="f6d24-112">Eis um exemplo que mostra como toouse PowerShell tooadd uma função do utilizador toohello Inviter convidado:</span><span class="sxs-lookup"><span data-stu-id="f6d24-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="f6d24-113">Controlar quem pode convidar</span><span class="sxs-lookup"><span data-stu-id="f6d24-113">Control who can invite</span></span>

![Controlo como tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="f6d24-115">Com a colaboração B2B do Azure AD, um administrador de inquilino pode definir Olá políticas convite a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6d24-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="f6d24-116">Desativar convites para</span><span class="sxs-lookup"><span data-stu-id="f6d24-116">Turn off invitations</span></span>
- <span data-ttu-id="f6d24-117">Apenas administradores e utilizadores da função de convidado Inviter Olá podem convidar</span><span class="sxs-lookup"><span data-stu-id="f6d24-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="f6d24-118">Podem convidar Admins, função de convidado Inviter Olá e membros</span><span class="sxs-lookup"><span data-stu-id="f6d24-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="f6d24-119">Todos os utilizadores, incluindo nos convidados, podem convidar</span><span class="sxs-lookup"><span data-stu-id="f6d24-119">All users, including guests, can invite</span></span>

<span data-ttu-id="f6d24-120">Por predefinição, os inquilinos estão definidos demasiado #4.</span><span class="sxs-lookup"><span data-stu-id="f6d24-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="f6d24-121">(Todos os utilizadores, incluindo nos convidados, podem convidar os utilizadores de B2B).</span><span class="sxs-lookup"><span data-stu-id="f6d24-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6d24-122">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f6d24-122">Next steps</span></span>

<span data-ttu-id="f6d24-123">Consulte os nossos outros artigos sobre a colaboração B2B do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="f6d24-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f6d24-124">O que é a colaboração B2B do Azure AD?</span><span class="sxs-lookup"><span data-stu-id="f6d24-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="f6d24-125">Propriedades de utilizador de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="f6d24-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="f6d24-126">Adicionar uma função de tooa de utilizador de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="f6d24-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="f6d24-127">Grupos dinâmicos e de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="f6d24-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="f6d24-128">Código de colaboração do B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6d24-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="f6d24-129">Configurar aplicações SaaS colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="f6d24-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="f6d24-130">Tokens de utilizador de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="f6d24-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="f6d24-131">Afirmações de utilizador de colaboração B2B mapeamento</span><span class="sxs-lookup"><span data-stu-id="f6d24-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="f6d24-132">Partilha externa do Office 365</span><span class="sxs-lookup"><span data-stu-id="f6d24-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="f6d24-133">Limitações atuais de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="f6d24-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
