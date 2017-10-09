---
title: "Do Azure AD Connect: A autenticação pass-through - como funciona? | Microsoft Docs"
description: Este artigo descreve como funciona o Azure Active Directory pass-through Authentication.
services: active-directory
keywords: "Authentication do Azure AD Connect pass-through, a instalação do Active Directory, os componentes necessários para o Azure AD, SSO, o início de sessão único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Authentication do Azure Active Directory pass-through: Descrição profunda técnica

>[!IMPORTANT]
>Autenticação de pass-through do Azure AD está atualmente em pré-visualização. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Como funciona a autenticação pass-through do Active Directory do Azure?

Quando um utilizador tenta toosign para uma aplicação protegida pelo Azure Active Directory (Azure AD) e se a autenticação pass-through estiver ativada no inquilino Olá, Olá ocorrem os seguintes passos:

1. utilizador Olá tenta tooaccess uma aplicação (por exemplo, Olá Outlook Web App - https://outlook.office365.com/owa/).
2. Se o utilizador Olá não está já iniciou sessão, o utilizador Olá é redirecionada toohello do Azure AD. o início de sessão página.
3. utilizador Olá introduz o respetivo nome de utilizador e palavra-passe no Azure AD início de sessão página Olá e clica no botão "Iniciar sessão" de Olá.
4. Azure AD, na receção Olá início de sessão pedido, coloca Olá nome de utilizador e palavra-passe (encriptadas com uma chave pública) numa fila.
5. Um agente de autenticação pass-through no local faz com que uma fila de toohello de chamada de saída e obtém Olá nome de utilizador e palavra-passe encriptada.
6. agente de Olá desencripta a palavra-passe de Olá utilizando a respetiva chave privada.
7. agente de Olá, em seguida, valida Olá nome de utilizador e palavra-passe no Active Directory utilizando APIs padrão do Windows (um toowhat mecanismo semelhante é utilizado por serviços de Federação do Active Directory). Olá nome de utilizador pode ser qualquer nome de utilizador do Olá no local predefinido (normalmente `userPrincipalName`) ou outro atributo configurado no Azure AD Connect (conhecido como `Alternate ID`).
8. Olá controlador de domínio do Active Directory (DC) no local, em seguida, avalia Olá pedido e devolve Olá resposta adequada (êxito, falha, palavra-passe expirou ou utilizador bloqueadas) toohello agente.
9. agente de Olá, por sua vez, devolve este tooAzure de back-resposta AD.
10. Azure AD avalia resposta Olá e responde toohello utilizador conforme apropriado - por exemplo, este inicia imediatamente utilizador Olá sessão ou pedidos para o multi-factor Authentication (MFA).
11. Se Olá utilizador inicie sessão com êxito, o utilizador Olá é tooaccess capaz de aplicação de Olá.

Olá diagrama seguinte ilustra todos os componentes de Olá e passos de Olá envolvidos.

![Autenticação pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>Passos seguintes
- [**Limitações atuais** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -esta funcionalidade está atualmente em pré-visualização. Saiba os cenários suportados e aqueles que não são.
- [**Início Rápido** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - obter cópias de segurança e executar a autenticação pass-through do Azure AD.
- [**Perguntas mais frequentes** ](active-directory-aadconnect-pass-through-authentication-faq.md) -atender toofrequently mais frequentes sobre o.
- [**Resolver problemas** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Saiba como tooresolve comuns problemas com a funcionalidade de Olá.
- [**Azure SSO totalmente integrada de AD** ](active-directory-aadconnect-sso.md) -Saiba mais sobre esta funcionalidade complementares.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - para apresentação de pedidos de funcionalidades de novo.
