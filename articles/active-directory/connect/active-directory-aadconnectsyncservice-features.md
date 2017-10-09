---
title: "funcionalidades e configuração de serviço de sincronização do aaaAzure AD Connect | Microsoft Docs"
description: "Descreve as funcionalidades do lado do serviço para o serviço de sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="5e974-103">Funcionalidades do serviço de sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5e974-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="5e974-104">funcionalidade de sincronização de Olá do Azure AD Connect tem dois componentes:</span><span class="sxs-lookup"><span data-stu-id="5e974-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="5e974-105">componente do Olá no local com o nome **sincronização do Azure AD Connect**, também chamado **motor de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="5e974-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="5e974-106">serviço de Olá que reside no Azure AD também conhecido como **serviço de sincronização do Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="5e974-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="5e974-107">Este tópico explica como Olá seguintes funcionalidades de Olá **serviço de sincronização do Azure AD Connect** trabalho e como pode configurá-los através do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e974-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="5e974-108">Estas definições são configuradas por Olá [módulo Azure Active Directory para Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="5e974-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="5e974-109">Transfira e instale-o em separado a partir do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="5e974-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="5e974-110">cmdlets de Olá documentados neste tópico foram introduzidos no Olá [versão de Março de 2016 (compilação 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="5e974-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="5e974-111">Se não tiver cmdlets Olá documentados neste tópico ou não produzem Olá mesmo resulta, em seguida, certifique-se, executar a versão mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="5e974-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="5e974-112">configuração de Olá toosee no diretório do Azure AD, execute `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="5e974-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="5e974-113">![Get-MsolDirSyncFeatures resultado](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="5e974-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="5e974-114">Muitas destas definições só podem ser alteradas pelo Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="5e974-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="5e974-115">Olá seguintes definições podem ser configuradas pelo `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="5e974-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="5e974-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="5e974-116">DirSyncFeature</span></span> | <span data-ttu-id="5e974-117">Comentário</span><span class="sxs-lookup"><span data-stu-id="5e974-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="5e974-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="5e974-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="5e974-119">Permite objetos toojoin no userPrincipalName endereço tooprimary SMTP de adição.</span><span class="sxs-lookup"><span data-stu-id="5e974-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="5e974-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="5e974-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="5e974-121">Permite que o atributo userPrincipalName de Olá tooupdate Olá sincronização motor para gerido/licenciado utilizadores (não federada).</span><span class="sxs-lookup"><span data-stu-id="5e974-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="5e974-122">Depois de ter ativado uma funcionalidade, não é possível desativar novamente.</span><span class="sxs-lookup"><span data-stu-id="5e974-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="5e974-123">De 24 de Agosto de 2016 Olá funcionalidade *duplicado resiliência de atributo* está ativada por predefinição para o novo Azure diretórios AD.</span><span class="sxs-lookup"><span data-stu-id="5e974-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="5e974-124">Esta funcionalidade será também revertida e ativada em diretórios criados antes desta data.</span><span class="sxs-lookup"><span data-stu-id="5e974-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="5e974-125">Receberá uma notificação por e-mail ao seu diretório é sobre tooget esta funcionalidade ativada.</span><span class="sxs-lookup"><span data-stu-id="5e974-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="5e974-126">Olá seguintes definições são configuradas pelo Azure AD Connect e não pode ser modificadas por `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="5e974-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="5e974-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="5e974-127">DirSyncFeature</span></span> | <span data-ttu-id="5e974-128">Comentário</span><span class="sxs-lookup"><span data-stu-id="5e974-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="5e974-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="5e974-129">DeviceWriteback</span></span> |[<span data-ttu-id="5e974-130">O Azure AD Connect: Ativar a repetição de escrita do dispositivo</span><span class="sxs-lookup"><span data-stu-id="5e974-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="5e974-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="5e974-131">DirectoryExtensions</span></span> |[<span data-ttu-id="5e974-132">Sincronização do Azure AD Connect: extensões de diretórios</span><span class="sxs-lookup"><span data-stu-id="5e974-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="5e974-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="5e974-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="5e974-134">Permite que um toobe atributo colocados em quarentena quando é um duplicado de outro objeto em vez de objeto Olá de toda a falhar durante a exportação.</span><span class="sxs-lookup"><span data-stu-id="5e974-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="5e974-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="5e974-135">PasswordSync</span></span> |[<span data-ttu-id="5e974-136">Implementar a sincronização de palavras-passe com a sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5e974-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="5e974-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="5e974-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="5e974-138">Pré-visualização: Repetição de escrita de grupo</span><span class="sxs-lookup"><span data-stu-id="5e974-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="5e974-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="5e974-139">UserWriteback</span></span> |<span data-ttu-id="5e974-140">Não é atualmente suportado.</span><span class="sxs-lookup"><span data-stu-id="5e974-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="5e974-141">Resiliência de atributo duplicado</span><span class="sxs-lookup"><span data-stu-id="5e974-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="5e974-142">Em vez de falhar tooprovision objetos com UPNs duplicados / proxyAddresses, atributo duplicado Olá é "colocados em quarentena" e um valor temporário está atribuído.</span><span class="sxs-lookup"><span data-stu-id="5e974-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="5e974-143">Quando o conflito de Olá for resolvido, Olá temporário UPN é alterado automaticamente o valor adequado toohello.</span><span class="sxs-lookup"><span data-stu-id="5e974-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="5e974-144">Para obter mais detalhes, consulte [resiliência de atributo de sincronização e duplicado identidade](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="5e974-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="5e974-145">Correspondência de forma recuperável UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="5e974-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="5e974-146">Quando esta funcionalidade está ativada, configuração soft-match está ativada para UPN na adição toohello [endereço SMTP principal](https://support.microsoft.com/kb/2641663), que está sempre ativada.</span><span class="sxs-lookup"><span data-stu-id="5e974-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="5e974-147">Correspondência de forma recuperável é utilizadores de nuvem existente toomatch utilizado no Azure AD com utilizadores no local.</span><span class="sxs-lookup"><span data-stu-id="5e974-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="5e974-148">Se precisar de toomatch no local Contas de anúncios com criados na nuvem de Olá de contas existentes e não estiver a utilizar Exchange Online, em seguida, esta funcionalidade é útil.</span><span class="sxs-lookup"><span data-stu-id="5e974-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="5e974-149">Neste cenário, geralmente não tiver um atributo de SMTP do motivo tooset Olá na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="5e974-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="5e974-150">Esta funcionalidade está em por predefinição para recentemente criada diretórios do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e974-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="5e974-151">Pode ver se esta funcionalidade está ativada para si, executando a aplicação:</span><span class="sxs-lookup"><span data-stu-id="5e974-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="5e974-152">Se esta funcionalidade não está ativada para o diretório do Azure AD, pode ativá-la ao executar:</span><span class="sxs-lookup"><span data-stu-id="5e974-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="5e974-153">Sincronizar atualizações de userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="5e974-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="5e974-154">Historicamente, atributo UserPrincipalName toohello de atualizações utilizando o serviço de sincronização de Olá no local foi bloqueado, exceto se ambas estas condições forem verdadeiras:</span><span class="sxs-lookup"><span data-stu-id="5e974-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="5e974-155">utilizador Olá é gerido (não federada).</span><span class="sxs-lookup"><span data-stu-id="5e974-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="5e974-156">Não foi atribuída uma licença de utilizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="5e974-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="5e974-157">Para obter mais detalhes, consulte [utilizador nomes no Office 365, Azure ou Intune não correspondem Olá UPN no local ou o ID de início de sessão alternativo](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="5e974-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="5e974-158">Ativar esta funcionalidade permite Olá sincronização motor tooupdate Olá userPrincipalName quando é alterado no local e utilizar a sincronização de palavra-passe. Se utilizar a Federação, esta funcionalidade não é suportada.</span><span class="sxs-lookup"><span data-stu-id="5e974-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="5e974-159">Esta funcionalidade está em por predefinição para recentemente criada diretórios do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e974-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="5e974-160">Pode ver se esta funcionalidade está ativada para si, executando a aplicação:</span><span class="sxs-lookup"><span data-stu-id="5e974-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="5e974-161">Se esta funcionalidade não está ativada para o diretório do Azure AD, pode ativá-la ao executar:</span><span class="sxs-lookup"><span data-stu-id="5e974-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="5e974-162">Depois de ativar esta funcionalidade, os valores de userPrincipalName existentes permanecerá como-é.</span><span class="sxs-lookup"><span data-stu-id="5e974-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="5e974-163">Na próxima alteração de Olá userPrincipalName atributo no local, a sincronização de diferenças normal Olá nos utilizadores atualizará Olá UPN.</span><span class="sxs-lookup"><span data-stu-id="5e974-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="5e974-164">Consultar também</span><span class="sxs-lookup"><span data-stu-id="5e974-164">See also</span></span>
* [<span data-ttu-id="5e974-165">Sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5e974-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="5e974-166">[Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="5e974-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

