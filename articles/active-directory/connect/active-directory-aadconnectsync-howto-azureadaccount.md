---
title: "Sincronização do Azure AD Connect: como conta de serviço toomanage Olá do Azure AD | Microsoft Docs"
description: "Este tópico documenta como conta de serviço toorestore Olá do Azure AD."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, como tooreset Olá palavra-passe para Olá sincronização do Azure AD Connect conta de serviço do conector"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="f1fa4-104">Sincronização do Azure AD Connect: como conta de serviço toomanage Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1fa4-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="f1fa4-105">conta de serviço de Olá utilizada pelo conector do Azure AD de Olá deveria toobe serviço gratuito.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="f1fa4-106">Se precisar de tooreset as respetivas credenciais, em seguida, este tópico é que o utilizador.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="f1fa4-107">Por exemplo, se um Administrador Global tiver por erro reposição Olá palavra-passe na conta de serviço Olá através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="f1fa4-108">Repor as credenciais de Olá</span><span class="sxs-lookup"><span data-stu-id="f1fa4-108">Reset hello credentials</span></span>
<span data-ttu-id="f1fa4-109">Se a conta de serviço Olá definida na Olá conector do Azure AD não consegue contactar o Azure AD devido a problemas de tooauthentication, é possível repor a palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="f1fa4-110">Inicie sessão no servidor de sincronização do Azure AD Connect toohello e inicie o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="f1fa4-111">Execute `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="f1fa4-112">![Addadsyncaadserviceaccount de cmdlet do PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="f1fa4-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="f1fa4-113">Forneça as credenciais de Administrador Global do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="f1fa4-114">Este cmdlet repõe Olá palavra-passe da conta de serviço Olá e atualizá-lo no Azure AD e no motor de sincronização de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="f1fa4-115">Estes passos podem resolver os problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="f1fa4-115">Known issues these steps can solve</span></span>
<span data-ttu-id="f1fa4-116">Esta secção se uma lista de erros comunicados pelos clientes que foram corrigidos por um credenciais repor em Olá conta de serviço do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="f1fa4-117">Evento 6900</span><span class="sxs-lookup"><span data-stu-id="f1fa4-117">Event 6900</span></span>  
<span data-ttu-id="f1fa4-118">servidor de Olá encontrou um erro inesperado ao processar uma notificação de alteração de palavra-passe:</span><span class="sxs-lookup"><span data-stu-id="f1fa4-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="f1fa4-119">AADSTS70002: Erro a validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="f1fa4-120">AADSTS50054: Palavra-passe antiga é utilizado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="f1fa4-121">Evento 659</span><span class="sxs-lookup"><span data-stu-id="f1fa4-121">Event 659</span></span>  
<span data-ttu-id="f1fa4-122">Erro ao obter a configuração de sincronização da política de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="f1fa4-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="f1fa4-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="f1fa4-124">AADSTS70002: Erro a validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="f1fa4-125">AADSTS50054: Palavra-passe antiga é utilizado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="f1fa4-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1fa4-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f1fa4-126">Next steps</span></span>
<span data-ttu-id="f1fa4-127">**Tópicos de descrição geral**</span><span class="sxs-lookup"><span data-stu-id="f1fa4-127">**Overview topics**</span></span>

* [<span data-ttu-id="f1fa4-128">Sincronização do Azure AD Connect: Noções e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="f1fa4-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="f1fa4-129">Integrar as identidades no local ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1fa4-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

