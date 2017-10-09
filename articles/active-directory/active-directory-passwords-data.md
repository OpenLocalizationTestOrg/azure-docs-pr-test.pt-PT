---
title: Requisitos de dados do Azure AD SSPR | Microsoft Docs
description: "Reposição de palavra-passe self-service do Azure AD, os requisitos de dados e como toosatisfy-las"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="fef0a-103">Implementar sem necessidade de registo de utilizador final de reposição de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="fef0a-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="fef0a-104">A implementação de reposição de palavra-passe Self-Service (SSPR) requer autenticação dados toobe presente.</span><span class="sxs-lookup"><span data-stu-id="fef0a-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="fef0a-105">Algumas organizações têm os seus utilizadores, introduza os seus dados de autenticação próprios mas, muitas organizações preferem toosynchronize com dados existentes no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fef0a-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="fef0a-106">Se tem o formato correcto dados no seu diretório no local e configurar [do Azure AD Connect utilizando as definições rápidas](./connect/active-directory-aadconnect-get-started-express.md), que os dados ficam disponível tooAzure AD e SSPR sem interação do utilizador necessárias.</span><span class="sxs-lookup"><span data-stu-id="fef0a-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="fef0a-107">Os números de telefone tem de estar no formato de Olá + indicativo do país PhoneNumber exemplo: + 1 4255551234 toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="fef0a-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="fef0a-108">Reposição de palavra-passe não suporta extensões telefónicas.</span><span class="sxs-lookup"><span data-stu-id="fef0a-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="fef0a-109">Mesmo em formato de 12345 4255551234 + 1 X Olá, as extensões são removidas antes da chamada de Olá está colocada.</span><span class="sxs-lookup"><span data-stu-id="fef0a-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="fef0a-110">Campos preenchidos</span><span class="sxs-lookup"><span data-stu-id="fef0a-110">Fields populated</span></span>

<span data-ttu-id="fef0a-111">Se utilizar predefinições Olá no Olá do Azure AD Connect seguintes são efetuados os mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="fef0a-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="fef0a-112">AD no local</span><span class="sxs-lookup"><span data-stu-id="fef0a-112">On-premises AD</span></span> | <span data-ttu-id="fef0a-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="fef0a-113">Azure AD</span></span> | <span data-ttu-id="fef0a-114">Informações de contacto de autenticação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fef0a-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fef0a-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="fef0a-115">telephoneNumber</span></span> | <span data-ttu-id="fef0a-116">Telefone do escritório</span><span class="sxs-lookup"><span data-stu-id="fef0a-116">Office phone</span></span> | <span data-ttu-id="fef0a-117">Telefone alternativo</span><span class="sxs-lookup"><span data-stu-id="fef0a-117">Alternate phone</span></span> |
| <span data-ttu-id="fef0a-118">Mobile</span><span class="sxs-lookup"><span data-stu-id="fef0a-118">mobile</span></span> | <span data-ttu-id="fef0a-119">Número de telemóvel</span><span class="sxs-lookup"><span data-stu-id="fef0a-119">Mobile phone</span></span> | <span data-ttu-id="fef0a-120">Telefone</span><span class="sxs-lookup"><span data-stu-id="fef0a-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="fef0a-121">Perguntas de segurança e respostas</span><span class="sxs-lookup"><span data-stu-id="fef0a-121">Security questions and answers</span></span>

<span data-ttu-id="fef0a-122">Perguntas de segurança e respostas são armazenadas em segurança no seu inquilino do Azure AD e são apenas acessíveis toousers através de Olá [portal de registo SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="fef0a-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="fef0a-123">Os administradores não é possível ver ou modificar o conteúdo Olá utilizadores perguntas e respostas de outro.</span><span class="sxs-lookup"><span data-stu-id="fef0a-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="fef0a-124">O que acontece quando um utilizador se regista</span><span class="sxs-lookup"><span data-stu-id="fef0a-124">What happens when a user registers</span></span>

<span data-ttu-id="fef0a-125">Quando um utilizador se regista, a página de registo Olá define Olá seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="fef0a-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="fef0a-126">Telefone de autenticação</span><span class="sxs-lookup"><span data-stu-id="fef0a-126">Authentication Phone</span></span>
* <span data-ttu-id="fef0a-127">E-Mail de autenticação</span><span class="sxs-lookup"><span data-stu-id="fef0a-127">Authentication Email</span></span>
* <span data-ttu-id="fef0a-128">Perguntas de segurança e respostas</span><span class="sxs-lookup"><span data-stu-id="fef0a-128">Security Questions and Answers</span></span>

<span data-ttu-id="fef0a-129">Se tiver fornecido um valor para **telemóvel** ou **correio eletrónico alternativo**, os utilizadores podem imediatamente utilizar esses valores tooreset as palavras-passe, mesmo que o se ainda não está registado para o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="fef0a-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="fef0a-130">Além disso, os utilizadores veem esses valores, quando a registar Olá pela primeira vez e modificá-las, se pretenderem.</span><span class="sxs-lookup"><span data-stu-id="fef0a-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="fef0a-131">Depois de se registar com êxito, estes valores serão ser persistente na Olá **telefone de autenticação** e **correio eletrónico de autenticação** campos, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="fef0a-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="fef0a-132">Definir e ler os dados de autenticação utilizando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="fef0a-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="fef0a-133">Olá seguintes campos pode ser definida com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="fef0a-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="fef0a-134">Correio eletrónico alternativo</span><span class="sxs-lookup"><span data-stu-id="fef0a-134">Alternate Email</span></span>
* <span data-ttu-id="fef0a-135">Telemóvel</span><span class="sxs-lookup"><span data-stu-id="fef0a-135">Mobile Phone</span></span>
* <span data-ttu-id="fef0a-136">Telefone do escritório - só pode ser definida se não a sincronizar com um diretório no local</span><span class="sxs-lookup"><span data-stu-id="fef0a-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="fef0a-137">Utilizar o PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="fef0a-137">Using PowerShell V1</span></span>

<span data-ttu-id="fef0a-138">tooget iniciado, terá de demasiado[transferir e instalar o módulo do Azure AD PowerShell Olá](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="fef0a-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="fef0a-139">Depois de ter instalado, pode seguir os passos de Olá que se seguem tooconfigure cada campo.</span><span class="sxs-lookup"><span data-stu-id="fef0a-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="fef0a-140">Conjunto de dados de autenticação com o PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="fef0a-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="fef0a-141">Ler os dados de autenticação com PowerShellPowerShell V1</span><span class="sxs-lookup"><span data-stu-id="fef0a-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="fef0a-142">Telefone de autenticação e o E-Mail de autenticação apenas podem ser lidos através do Powershell V1 Olá a utilizar os comandos que se seguem</span><span class="sxs-lookup"><span data-stu-id="fef0a-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="fef0a-143">Utilizar o PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="fef0a-143">Using PowerShell V2</span></span>

<span data-ttu-id="fef0a-144">tooget iniciado, terá de demasiado[transferir e instalar o módulo do PowerShell Olá, Azure AD V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="fef0a-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="fef0a-145">Depois de ter instalado, pode seguir os passos de Olá que se seguem tooconfigure cada campo.</span><span class="sxs-lookup"><span data-stu-id="fef0a-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="fef0a-146">tooinstall rapidamente a partir de versões recentes do PowerShell que suportam o módulo de instalação, execute estes comandos (primeira linha de Olá simplesmente verifica toosee se estiver já instalada):</span><span class="sxs-lookup"><span data-stu-id="fef0a-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="fef0a-147">Conjunto de dados de autenticação com o PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="fef0a-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="fef0a-148">Ler os dados de autenticação com o PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="fef0a-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="fef0a-149">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fef0a-149">Next steps</span></span>

<span data-ttu-id="fef0a-150">Olá seguintes ligações fornece informações adicionais sobre a utilizar o Azure AD de reposição de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="fef0a-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="fef0a-151">[**Guia de Introdução** ](active-directory-passwords-getting-started.md) - Começar a trabalhar com a gestão de palavras-passe self-service do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fef0a-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="fef0a-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing (Licenciamento - Configurar o Licenciamento do Azure AD)</span><span class="sxs-lookup"><span data-stu-id="fef0a-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="fef0a-153">[**Implementação** ](active-directory-passwords-best-practices.md) -planear e implementar os utilizadores de tooyour SSPR utilizando a orientação de Olá encontrada aqui</span><span class="sxs-lookup"><span data-stu-id="fef0a-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="fef0a-154">[**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aspeto e funcionalidade de Olá SSPR experiência da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="fef0a-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="fef0a-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies (Política - Compreender e definir políticas de palavras-passe do Azure AD)</span><span class="sxs-lookup"><span data-stu-id="fef0a-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="fef0a-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality (Relatórios - Descubra se, quando e a partir de onde é que os utilizadores acedem à funcionalidade SSPR)</span><span class="sxs-lookup"><span data-stu-id="fef0a-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="fef0a-157">[**Descrição detalhada da Technical** ](active-directory-passwords-how-it-works.md) -voltar atrás Olá curtain toounderstand como funciona</span><span class="sxs-lookup"><span data-stu-id="fef0a-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="fef0a-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span><span class="sxs-lookup"><span data-stu-id="fef0a-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="fef0a-159">Porquê?</span><span class="sxs-lookup"><span data-stu-id="fef0a-159">Why?</span></span> <span data-ttu-id="fef0a-160">What?</span><span class="sxs-lookup"><span data-stu-id="fef0a-160">What?</span></span> <span data-ttu-id="fef0a-161">Where?</span><span class="sxs-lookup"><span data-stu-id="fef0a-161">Where?</span></span> <span data-ttu-id="fef0a-162">Who?</span><span class="sxs-lookup"><span data-stu-id="fef0a-162">Who?</span></span> <span data-ttu-id="fef0a-163">When?</span><span class="sxs-lookup"><span data-stu-id="fef0a-163">When?</span></span> <span data-ttu-id="fef0a-164">-Atender tooquestions sempre pretendia tooask</span><span class="sxs-lookup"><span data-stu-id="fef0a-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="fef0a-165">[**Resolver problemas** ](active-directory-passwords-troubleshoot.md) -Saiba como tooresolve comuns problemas que vemos com SSPR</span><span class="sxs-lookup"><span data-stu-id="fef0a-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
