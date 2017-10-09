---
title: "aaaAzure FAQ de proteção de identidade do Active Directory | Microsoft Docs"
description: Perguntas mais frequentes sobre o Azure AD Identity Protection
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6a053ce02bf7a248a284f482f20f96a312f1c204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="a6458-103">Proteção de identidade do Azure Active Directory FAQ</span><span class="sxs-lookup"><span data-stu-id="a6458-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="a6458-104">Por que razão é que alguns eventos de risco tem o estado de "Fechado (sistema)"?</span><span class="sxs-lookup"><span data-stu-id="a6458-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="a6458-105">**R:** estes são os eventos que o Azure Active Directory Identity Protection detetado e mais tarde fechado porque eventos Olá foram já não considera duvidosos.</span><span class="sxs-lookup"><span data-stu-id="a6458-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because hello events were no longer considered risky.</span></span> <span data-ttu-id="a6458-106">Estes eventos não contam para o nível de risco do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="a6458-106">These events do not count towards hello user’s risk level.</span></span> 

---

## <a name="do-i-need-toobe-a-global-admin-toouse-identity-protection-in-hello-azure-portal"></a><span data-ttu-id="a6458-107">É necessário toobe um administrador global de toouse Identity Protection na Olá portal do Azure?</span><span class="sxs-lookup"><span data-stu-id="a6458-107">Do I need toobe a global admin toouse Identity Protection in hello Azure portal?</span></span>
<span data-ttu-id="a6458-108">**R:** **não**.</span><span class="sxs-lookup"><span data-stu-id="a6458-108">**A:** **No**.</span></span> <span data-ttu-id="a6458-109">Pode ser um leitor de segurança, um administrador de segurança ou um Administrador Global de toouse Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="a6458-109">You can either be a Security Reader, a Security Admin or a Global Admin toouse Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="a6458-110">Como devo proceder para proteção de identidade?</span><span class="sxs-lookup"><span data-stu-id="a6458-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="a6458-111">**R:** consulte [introdução ao Azure Active Directory Premium](active-directory-get-started-premium.md) para uma questão de toothis de resposta.</span><span class="sxs-lookup"><span data-stu-id="a6458-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="a6458-112">O que acontece quando expira a versão de avaliação do Azure Active Directory Premium 2?</span><span class="sxs-lookup"><span data-stu-id="a6458-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="a6458-113">**R:** se sua edição de avaliação do Azure Active Directory Premium 2 expirou na sua edição gratuito do Azure Active Directory, Basic ou Premium 1 e tiver Identity Protection ativada, tem acesso tooit, apesar de não são compliance com licenciamento.</span><span class="sxs-lookup"><span data-stu-id="a6458-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access tooit even though you are not in compliance with licensing.</span></span>

---
