---
title: "aaaCompare B2B colaboração e B2C no Azure Active Directory | Microsoft Docs"
description: "O que é a diferença de Olá entre colaboração B2B do Active Directory do Azure e o Azure AD B2C?"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>Comparar a colaboração B2B e B2C no Azure Active Directory

Colaboração B2B do Azure Active Directory (Azure AD) e o Azure AD B2C permitem-lhe toowork com utilizadores externos no Azure AD. Mas a sua comparação?


Funcionalidades de colaboração do B2B |     Oferta de autónoma AD B2C do Azure
-------- | --------
Se destina a: as organizações que pretendem toobe tooauthenticate capaz de utilizadores da organização de parceiro, independentemente do fornecedor de identidade. | Se destina a: Inviting se os clientes do seu dispositivo móvel e as aplicações web, pessoas, os clientes institutional ou organizacionais no seu Azure AD.
Identidades suportadas: os funcionários com o trabalho ou escola contas, parceiros com contas profissionais ou escolares ou qualquer endereço de e-mail. Em breve toosupport direta Federação.  | Identidades suportadas: os utilizadores com contas de aplicação local (qualquer utilizador ou endereço de nome de e-mail) ou qualquer suportado social identidade com a Federação direta.
Quais os utilizadores de parceiro do diretório Olá estão numa: Olá, parceiro os utilizadores da organização externo Olá são geridos no mesmo diretório que os funcionários, mas anotado especial. Podem ser geridos Olá mesma forma como os funcionários, pode ser adicionado toohello mesmos grupos e assim sucessivamente  | Que são entidades de utilizador do diretório Olá cliente em: diretório de aplicação Olá. Gerido separadamente em Olá diretório da organização dos funcionários e parceiros (se aplicável.
Único início de sessão (SSO) tooall do Azure AD ligados aplicações é suportada. Por exemplo, pode fornecer acesso tooOffice 365 ou aplicações no local e tooother aplicações de SaaS, como o Salesforce ou Workday.  |  SSO toocustomer pertencentes à empresa de aplicações dentro de inquilinos Olá, Azure AD B2C é suportada. SSO tooOffice 365 ou aplicações de SaaS não Microsoft e Microsoft tooother não é suportado.
Ciclo de vida do parceiro: geridos pelo Olá anfitrião/inviting organização.  | Ciclo de vida do cliente: gerido pela aplicação Olá ou gestão personalizada.
Política de segurança e conformidade: geridos pelo Olá anfitrião/inviting organização.  | Política de segurança e conformidade: gerida pela aplicação Olá.
Imagem corporativa: É utilizada a marca do anfitrião/inviting da organização.  |    Imagem corporativa: Gerida pela aplicação. Normalmente, tende produto toobe imagem corporativa, com fading de organização Olá no fundo Olá.
Obter mais informações: [blogue](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [documentação](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | Obter mais informações: [página de produto](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [documentação](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>Passos seguintes

Consulte os nossos outros artigos sobre a colaboração B2B do Azure AD:

* [O que é a colaboração B2B do Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de utilizador de colaboração B2B](active-directory-b2b-user-properties.md)
* [Adicionar uma função de tooa de utilizador de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegar convites para colaboração do B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinâmicos e de colaboração B2B](active-directory-b2b-dynamic-groups.md)
* [Configurar aplicações SaaS colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de utilizador de colaboração B2B](active-directory-b2b-user-token.md)
* [Afirmações de utilizador de colaboração B2B mapeamento](active-directory-b2b-claims-mapping.md)
* [Partilha externa do Office 365](active-directory-b2b-o365-external-user.md)
* [Limitações atuais de colaboração B2B](active-directory-b2b-current-limitations.md)
* [Obter o suporte para colaboração B2B](active-directory-b2b-support.md)
