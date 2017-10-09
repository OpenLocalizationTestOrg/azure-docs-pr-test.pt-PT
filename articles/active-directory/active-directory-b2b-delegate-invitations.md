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
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Delegar convites para colaboração B2B do Azure Active Directory do

Com a colaboração de empresa-empresa (B2B) do Azure Active Directory (Azure AD), não dispõe de toobe convites de toosend um administrador global. Em vez disso, pode utilizar as políticas e delegar toousers convites para cujas funções permitam-lhes toosend convites. É um importante novos forma toodelegate convidado utilizador convites através da função de convidado Inviter Olá.

## <a name="guest-inviter-role"></a>Função de convidado Inviter
Iremos pode atribuir Olá utilizador tooGuest convites de toosend Inviter função. Não tem membro toobe convites para do toosend de função de administrador global do Olá. Por predefinição, os utilizadores regulares podem também invocar Olá convite API a menos que um administrador global desativado convites para os utilizadores regulares. Um utilizador pode também invocar a API de Olá utilizando Olá portal do Azure ou o PowerShell.

Eis um exemplo que mostra como toouse PowerShell tooadd uma função do utilizador toohello Inviter convidado:

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>Controlar quem pode convidar

![Controlo como tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Com a colaboração B2B do Azure AD, um administrador de inquilino pode definir Olá políticas convite a seguir:

- Desativar convites para
- Apenas administradores e utilizadores da função de convidado Inviter Olá podem convidar
- Podem convidar Admins, função de convidado Inviter Olá e membros
- Todos os utilizadores, incluindo nos convidados, podem convidar

Por predefinição, os inquilinos estão definidos demasiado #4. (Todos os utilizadores, incluindo nos convidados, podem convidar os utilizadores de B2B).

## <a name="next-steps"></a>Passos seguintes

Consulte os nossos outros artigos sobre a colaboração B2B do Azure AD:

* [O que é a colaboração B2B do Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de utilizador de colaboração B2B](active-directory-b2b-user-properties.md)
* [Adicionar uma função de tooa de utilizador de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Grupos dinâmicos e de colaboração B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboração do B2B e exemplos do PowerShell](active-directory-b2b-code-samples.md)
* [Configurar aplicações SaaS colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de utilizador de colaboração B2B](active-directory-b2b-user-token.md)
* [Afirmações de utilizador de colaboração B2B mapeamento](active-directory-b2b-claims-mapping.md)
* [Partilha externa do Office 365](active-directory-b2b-o365-external-user.md)
* [Limitações atuais de colaboração B2B](active-directory-b2b-current-limitations.md)
