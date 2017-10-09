---
title: "pedido de consentimento de aaaUnexpected quando iniciar sessão na aplicação tooan | Microsoft Docs"
description: "Como tootroubleshoot quando um utilizador verá um pedido de consentimento para uma aplicação tiver integrado com o Azure AD que não era esperado"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="d67b5-103">Pedido de consentimento inesperado quando iniciar sessão na aplicação tooan</span><span class="sxs-lookup"><span data-stu-id="d67b5-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="d67b5-104">Muitas aplicações que se integram com o Azure Active Directory requerem recursos toovarious permissões toorun de ordem.</span><span class="sxs-lookup"><span data-stu-id="d67b5-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="d67b5-105">Quando estes recursos também estão integrados no Azure Active Directory, tooaccess permissões-lhes é pedida utilizando Olá do Azure AD consentimento framework.</span><span class="sxs-lookup"><span data-stu-id="d67b5-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="d67b5-106">Isto resulta num pedido de consentimento a ser mostrado Olá pela primeira vez que é utilizada uma aplicação, que é, muitas vezes, uma operação única.</span><span class="sxs-lookup"><span data-stu-id="d67b5-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="d67b5-107">Cenários em que os utilizadores veem consentimento dos avisos</span><span class="sxs-lookup"><span data-stu-id="d67b5-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="d67b5-108">Avisos adicionais podem ser esperados em vários cenários:</span><span class="sxs-lookup"><span data-stu-id="d67b5-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="d67b5-109">Olá de permissões necessárias pela aplicação Olá ter alterado.</span><span class="sxs-lookup"><span data-stu-id="d67b5-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="d67b5-110">Olá utilizador autorizado originalmente toohello aplicação não era um administrador e agora um utilizador diferente (não-administrador) está a utilizar a aplicação de Olá Olá pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="d67b5-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="d67b5-111">Olá utilizador autorizado originalmente toohello aplicação foi um administrador, mas não consentimento em nome da organização inteira Olá.</span><span class="sxs-lookup"><span data-stu-id="d67b5-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="d67b5-112">está a utilizar a aplicação Olá [consentimento incremental e dinâmico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest permissões adicionais depois de consentimento inicialmente foi concedido.</span><span class="sxs-lookup"><span data-stu-id="d67b5-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="d67b5-113">Isto é frequentemente utilizado quando funcionalidades opcionais de uma aplicação adicional requerem permissões para além daquelas necessário para a funcionalidade de linha de base.</span><span class="sxs-lookup"><span data-stu-id="d67b5-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="d67b5-114">Consentimento foi revogado depois de ser concedido inicialmente.</span><span class="sxs-lookup"><span data-stu-id="d67b5-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="d67b5-115">Programador Olá configurou Olá aplicação toorequire um pedido de consentimento sempre que é utilizada (Nota: não é recomendado).</span><span class="sxs-lookup"><span data-stu-id="d67b5-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d67b5-116">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d67b5-116">Next steps</span></span>

-   [<span data-ttu-id="d67b5-117">As aplicações, permissões e consentimento no Azure Active Directory (v 1.0 ponto final)</span><span class="sxs-lookup"><span data-stu-id="d67b5-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="d67b5-118">Âmbitos, permissões e consentimento no Olá Azure Active Directory (ponto final v 2.0)</span><span class="sxs-lookup"><span data-stu-id="d67b5-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


