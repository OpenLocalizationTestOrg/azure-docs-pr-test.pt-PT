---
title: "aaaTroubleshooting colaboração B2B do Azure Active Directory do | Microsoft Docs"
description: "Responsabilidade para problemas comuns com a colaboração B2B do Azure Active Directory do"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="52223-103">Resolução de problemas de colaboração B2B do Azure Active Directory do</span><span class="sxs-lookup"><span data-stu-id="52223-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="52223-104">Seguem-se algumas responsabilidade para problemas comuns com a colaboração B2B do Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52223-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="52223-105">Posso adicionar um utilizador externo, mas não vê-los no meu livro de endereços Global ou no selecionador de pessoas Olá</span><span class="sxs-lookup"><span data-stu-id="52223-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="52223-106">Em casos onde os utilizadores externos não são preenchidos na lista de Olá, objeto Olá poderá demorar alguns minutos tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="52223-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="52223-107">Um utilizador de convidado B2B não está visível no seleccionador do SharePoint Online/OneDrive pessoas</span><span class="sxs-lookup"><span data-stu-id="52223-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="52223-108">Olá toosearch de capacidade dos utilizadores convidados existente no selecionador de pessoas do SharePoint Online (SPO) Olá está OFF ao comportamento de legado de toomatch predefinido.</span><span class="sxs-lookup"><span data-stu-id="52223-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="52223-109">Pode ativar esta funcionalidade utilizando Olá definição 'ShowPeoplePickerSuggestionsForGuestUsers' na coleção de Olá inquilino e o site de nível.</span><span class="sxs-lookup"><span data-stu-id="52223-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="52223-110">Pode definir a funcionalidade de Olá utilizando Olá SPOTenant conjunto e SPOSite do conjunto de cmdlets que permite que os membros toosearch todos os utilizadores convidados existentes no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="52223-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="52223-111">As alterações no âmbito de inquilino Olá não afetam os sites SPO já aprovisionadas.</span><span class="sxs-lookup"><span data-stu-id="52223-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="52223-112">Foram desativadas convites para o diretório</span><span class="sxs-lookup"><span data-stu-id="52223-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="52223-113">Se for notificado de que não tiver permissões tooinvite utilizadores, certifique-se de que a sua conta de utilizador é autorizado tooinvite utilizadores externos em definições de utilizador:</span><span class="sxs-lookup"><span data-stu-id="52223-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="52223-114">Se tiver modificado estas definições ou Olá convidado Inviter função tooa utilizador atribuído recentemente, poderão existir um atraso de 15-60 minutos antes de Olá alterações entram em vigor.</span><span class="sxs-lookup"><span data-stu-id="52223-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="52223-115">utilizador Olá que posso convidado está a receber um erro durante a resgate</span><span class="sxs-lookup"><span data-stu-id="52223-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="52223-116">Erros comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="52223-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="52223-117">Administrador do invitee não permitiu a EmailVerified utilizadores de que está a ser criada no seu inquilino</span><span class="sxs-lookup"><span data-stu-id="52223-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="52223-118">Quando inviting utilizadores cuja organização está a utilizar o Azure Active Directory, mas olá onde a conta de utilizador específica não existe (por exemplo, Olá utilizador não existe no Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="52223-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="52223-119">administrador de Olá de contoso.com pode ter uma política no local a impedir que os utilizadores a ser criada.</span><span class="sxs-lookup"><span data-stu-id="52223-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="52223-120">utilizador Olá tem de verificar com os respetivos toodetermine admin se são permitidos a utilizadores externos.</span><span class="sxs-lookup"><span data-stu-id="52223-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="52223-121">Olá admin externo utilizador poderá ter tooallow verificar E-mail aos utilizadores no respetivo domínio (consulte este [artigo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) em permitir aos utilizadores verificar de E-Mail).</span><span class="sxs-lookup"><span data-stu-id="52223-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="52223-122">Utilizador externo não existe já num domínio federado</span><span class="sxs-lookup"><span data-stu-id="52223-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="52223-123">Se estiver a utilizar a autenticação de Federação e o utilizador Olá ainda não existir no Azure Active Directory, o utilizador Olá não pode ser convidado.</span><span class="sxs-lookup"><span data-stu-id="52223-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="52223-124">tooresolve este problema, hello admin de utilizador externo tem de sincronizar tooAzure de conta de utilizador Olá do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52223-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="52223-125">Como dos does\#', que não é normalmente um caráter válido, a sincronização com o Azure AD?</span><span class="sxs-lookup"><span data-stu-id="52223-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="52223-126">"\#" é um caráter reservado UPNs para colaboração B2B do Azure AD ou utilizadores externos, porque a conta de convidado de Olá user@contoso.com fica user_contoso.com#EXT@fabrikam.onmicrosoft.com. Por conseguinte, \# UPNs feitos no local não são permitidas toosign no toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52223-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="52223-127">Recebo um erro ao adicionar utilizadores externos tooa sincronizados grupo</span><span class="sxs-lookup"><span data-stu-id="52223-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="52223-128">Os utilizadores externos podem ser adicionados apenas demasiado "atribuído" ou grupos de "Segurança" e não toogroups são controlado no local.</span><span class="sxs-lookup"><span data-stu-id="52223-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="52223-129">Os meus utilizadores externos não recebeu um e-mail tooredeem</span><span class="sxs-lookup"><span data-stu-id="52223-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="52223-130">invitee Olá deve verificar junto do seu ISP ou é permitido tooensure de filtro de spam Olá seguinte endereço:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="52223-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="52223-131">Reparar que essa mensagem personalizada de saudação não obter incluída com mensagens convite por vezes</span><span class="sxs-lookup"><span data-stu-id="52223-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="52223-132">toocomply com as leis de privacidade, os APIs não incluir mensagens personalizadas no convite de correio eletrónico Olá quando:</span><span class="sxs-lookup"><span data-stu-id="52223-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="52223-133">inviter Olá não tiver um endereço de e-mail no Olá inviting inquilino</span><span class="sxs-lookup"><span data-stu-id="52223-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="52223-134">Quando um principal de serviço aplicacional envia convite Olá</span><span class="sxs-lookup"><span data-stu-id="52223-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="52223-135">Se este cenário é importante tooyou, pode suprimir os nosso e-mail de convite de API e enviá-lo através do mecanismo de correio eletrónico Olá à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="52223-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="52223-136">Consulte toomake counsel legais da sua organização se qualquer e-mail que enviar desta forma também estas estejam em conformidade com as leis de privacidade.</span><span class="sxs-lookup"><span data-stu-id="52223-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52223-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="52223-137">Next steps</span></span>

<span data-ttu-id="52223-138">Consulte os nossos outros artigos sobre a colaboração B2B do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="52223-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="52223-139">O que é a colaboração B2B do Azure AD?</span><span class="sxs-lookup"><span data-stu-id="52223-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="52223-140">Como é que os administradores de Azure Active Directory adicionar utilizadores de colaboração do B2B?</span><span class="sxs-lookup"><span data-stu-id="52223-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="52223-141">Como é que os infotrabalhadores adicionar utilizadores de colaboração do B2B?</span><span class="sxs-lookup"><span data-stu-id="52223-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="52223-142">elementos de Olá de Olá e-mail de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="52223-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="52223-143">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="52223-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="52223-144">Licenciamento e colaboração do Azure AD B2B</span><span class="sxs-lookup"><span data-stu-id="52223-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="52223-145">Colaboração do Azure Active Directory B2B perguntas mais frequentes (FAQ)</span><span class="sxs-lookup"><span data-stu-id="52223-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="52223-146">Colaboração B2B do Active Directory Azure API e personalização</span><span class="sxs-lookup"><span data-stu-id="52223-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="52223-147">Autenticação multifator para os utilizadores da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="52223-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="52223-148">Adicionar utilizadores de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="52223-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="52223-149">Índice de Artigos da Gestão da Aplicação no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52223-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
