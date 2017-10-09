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
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Implementar sem necessidade de registo de utilizador final de reposição de palavra-passe

A implementação de reposição de palavra-passe Self-Service (SSPR) requer autenticação dados toobe presente. Algumas organizações têm os seus utilizadores, introduza os seus dados de autenticação próprios mas, muitas organizações preferem toosynchronize com dados existentes no Active Directory. Se tem o formato correcto dados no seu diretório no local e configurar [do Azure AD Connect utilizando as definições rápidas](./connect/active-directory-aadconnect-get-started-express.md), que os dados ficam disponível tooAzure AD e SSPR sem interação do utilizador necessárias.

Os números de telefone tem de estar no formato de Olá + indicativo do país PhoneNumber exemplo: + 1 4255551234 toowork corretamente.

> [!NOTE]
> Reposição de palavra-passe não suporta extensões telefónicas. Mesmo em formato de 12345 4255551234 + 1 X Olá, as extensões são removidas antes da chamada de Olá está colocada.

## <a name="fields-populated"></a>Campos preenchidos

Se utilizar predefinições Olá no Olá do Azure AD Connect seguintes são efetuados os mapeamentos.

| AD no local | Azure AD | Informações de contacto de autenticação do AD do Azure |
| --- | --- | --- |
| telephoneNumber | Telefone do escritório | Telefone alternativo |
| Mobile | Número de telemóvel | Telefone |


## <a name="security-questions-and-answers"></a>Perguntas de segurança e respostas

Perguntas de segurança e respostas são armazenadas em segurança no seu inquilino do Azure AD e são apenas acessíveis toousers através de Olá [portal de registo SSPR](https://aka.ms/ssprsetup). Os administradores não é possível ver ou modificar o conteúdo Olá utilizadores perguntas e respostas de outro.

### <a name="what-happens-when-a-user-registers"></a>O que acontece quando um utilizador se regista

Quando um utilizador se regista, a página de registo Olá define Olá seguintes campos:

* Telefone de autenticação
* E-Mail de autenticação
* Perguntas de segurança e respostas

Se tiver fornecido um valor para **telemóvel** ou **correio eletrónico alternativo**, os utilizadores podem imediatamente utilizar esses valores tooreset as palavras-passe, mesmo que o se ainda não está registado para o serviço de Olá. Além disso, os utilizadores veem esses valores, quando a registar Olá pela primeira vez e modificá-las, se pretenderem. Depois de se registar com êxito, estes valores serão ser persistente na Olá **telefone de autenticação** e **correio eletrónico de autenticação** campos, respetivamente.

## <a name="set-and-read-authentication-data-using-powershell"></a>Definir e ler os dados de autenticação utilizando o PowerShell

Olá seguintes campos pode ser definida com o PowerShell

* Correio eletrónico alternativo
* Telemóvel
* Telefone do escritório - só pode ser definida se não a sincronizar com um diretório no local

### <a name="using-powershell-v1"></a>Utilizar o PowerShell V1

tooget iniciado, terá de demasiado[transferir e instalar o módulo do Azure AD PowerShell Olá](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). Depois de ter instalado, pode seguir os passos de Olá que se seguem tooconfigure cada campo.

#### <a name="set-authentication-data-with-powershell-v1"></a>Conjunto de dados de autenticação com o PowerShell V1

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>Ler os dados de autenticação com PowerShellPowerShell V1

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>Telefone de autenticação e o E-Mail de autenticação apenas podem ser lidos através do Powershell V1 Olá a utilizar os comandos que se seguem

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>Utilizar o PowerShell V2

tooget iniciado, terá de demasiado[transferir e instalar o módulo do PowerShell Olá, Azure AD V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). Depois de ter instalado, pode seguir os passos de Olá que se seguem tooconfigure cada campo.

tooinstall rapidamente a partir de versões recentes do PowerShell que suportam o módulo de instalação, execute estes comandos (primeira linha de Olá simplesmente verifica toosee se estiver já instalada):

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>Conjunto de dados de autenticação com o PowerShell V2

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>Ler os dados de autenticação com o PowerShell V2

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>Passos seguintes

Olá seguintes ligações fornece informações adicionais sobre a utilizar o Azure AD de reposição de palavra-passe

* [**Guia de Introdução** ](active-directory-passwords-getting-started.md) - Começar a trabalhar com a gestão de palavras-passe self-service do Azure AD 
* [**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing (Licenciamento - Configurar o Licenciamento do Azure AD)
* [**Implementação** ](active-directory-passwords-best-practices.md) -planear e implementar os utilizadores de tooyour SSPR utilizando a orientação de Olá encontrada aqui
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aspeto e funcionalidade de Olá SSPR experiência da sua empresa.
* [**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies (Política - Compreender e definir políticas de palavras-passe do Azure AD)
* [**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality (Relatórios - Descubra se, quando e a partir de onde é que os utilizadores acedem à funcionalidade SSPR)
* [**Descrição detalhada da Technical** ](active-directory-passwords-how-it-works.md) -voltar atrás Olá curtain toounderstand como funciona
* [**Frequently Asked Questions**](active-directory-passwords-faq.md) - How? Porquê? What? Where? Who? When? -Atender tooquestions sempre pretendia tooask
* [**Resolver problemas** ](active-directory-passwords-troubleshoot.md) -Saiba como tooresolve comuns problemas que vemos com SSPR
