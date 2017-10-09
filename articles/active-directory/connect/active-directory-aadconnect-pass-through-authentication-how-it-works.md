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
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="12d60-105">Authentication do Azure Active Directory pass-through: Descrição profunda técnica</span><span class="sxs-lookup"><span data-stu-id="12d60-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="12d60-106">Autenticação de pass-through do Azure AD está atualmente em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="12d60-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="12d60-107">Como funciona a autenticação pass-through do Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="12d60-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="12d60-108">Quando um utilizador tenta toosign para uma aplicação protegida pelo Azure Active Directory (Azure AD) e se a autenticação pass-through estiver ativada no inquilino Olá, Olá ocorrem os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="12d60-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="12d60-109">utilizador Olá tenta tooaccess uma aplicação (por exemplo, Olá Outlook Web App - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="12d60-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="12d60-110">Se o utilizador Olá não está já iniciou sessão, o utilizador Olá é redirecionada toohello do Azure AD. o início de sessão página.</span><span class="sxs-lookup"><span data-stu-id="12d60-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="12d60-111">utilizador Olá introduz o respetivo nome de utilizador e palavra-passe no Azure AD início de sessão página Olá e clica no botão "Iniciar sessão" de Olá.</span><span class="sxs-lookup"><span data-stu-id="12d60-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="12d60-112">Azure AD, na receção Olá início de sessão pedido, coloca Olá nome de utilizador e palavra-passe (encriptadas com uma chave pública) numa fila.</span><span class="sxs-lookup"><span data-stu-id="12d60-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="12d60-113">Um agente de autenticação pass-through no local faz com que uma fila de toohello de chamada de saída e obtém Olá nome de utilizador e palavra-passe encriptada.</span><span class="sxs-lookup"><span data-stu-id="12d60-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="12d60-114">agente de Olá desencripta a palavra-passe de Olá utilizando a respetiva chave privada.</span><span class="sxs-lookup"><span data-stu-id="12d60-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="12d60-115">agente de Olá, em seguida, valida Olá nome de utilizador e palavra-passe no Active Directory utilizando APIs padrão do Windows (um toowhat mecanismo semelhante é utilizado por serviços de Federação do Active Directory).</span><span class="sxs-lookup"><span data-stu-id="12d60-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="12d60-116">Olá nome de utilizador pode ser qualquer nome de utilizador do Olá no local predefinido (normalmente `userPrincipalName`) ou outro atributo configurado no Azure AD Connect (conhecido como `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="12d60-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="12d60-117">Olá controlador de domínio do Active Directory (DC) no local, em seguida, avalia Olá pedido e devolve Olá resposta adequada (êxito, falha, palavra-passe expirou ou utilizador bloqueadas) toohello agente.</span><span class="sxs-lookup"><span data-stu-id="12d60-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="12d60-118">agente de Olá, por sua vez, devolve este tooAzure de back-resposta AD.</span><span class="sxs-lookup"><span data-stu-id="12d60-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="12d60-119">Azure AD avalia resposta Olá e responde toohello utilizador conforme apropriado - por exemplo, este inicia imediatamente utilizador Olá sessão ou pedidos para o multi-factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="12d60-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="12d60-120">Se Olá utilizador inicie sessão com êxito, o utilizador Olá é tooaccess capaz de aplicação de Olá.</span><span class="sxs-lookup"><span data-stu-id="12d60-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="12d60-121">Olá diagrama seguinte ilustra todos os componentes de Olá e passos de Olá envolvidos.</span><span class="sxs-lookup"><span data-stu-id="12d60-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Autenticação pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="12d60-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="12d60-123">Next steps</span></span>
- <span data-ttu-id="12d60-124">[**Limitações atuais** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -esta funcionalidade está atualmente em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="12d60-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="12d60-125">Saiba os cenários suportados e aqueles que não são.</span><span class="sxs-lookup"><span data-stu-id="12d60-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="12d60-126">[**Início Rápido** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - obter cópias de segurança e executar a autenticação pass-through do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12d60-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="12d60-127">[**Perguntas mais frequentes** ](active-directory-aadconnect-pass-through-authentication-faq.md) -atender toofrequently mais frequentes sobre o.</span><span class="sxs-lookup"><span data-stu-id="12d60-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="12d60-128">[**Resolver problemas** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Saiba como tooresolve comuns problemas com a funcionalidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="12d60-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="12d60-129">[**Azure SSO totalmente integrada de AD** ](active-directory-aadconnect-sso.md) -Saiba mais sobre esta funcionalidade complementares.</span><span class="sxs-lookup"><span data-stu-id="12d60-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="12d60-130">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - para apresentação de pedidos de funcionalidades de novo.</span><span class="sxs-lookup"><span data-stu-id="12d60-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
