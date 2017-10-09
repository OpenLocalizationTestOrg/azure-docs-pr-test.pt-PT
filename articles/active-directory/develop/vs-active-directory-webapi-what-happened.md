---
title: aaaChanges efetuadas tooa end WebApi projeto quando se liga tooAzure AD | Microsoft Docs
description: Descreve o que acontece tooyour end WebApi projeto quando se liga tooAzure AD utilizando o Visual Studio
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>Projeto de end WebApi que tenham acontecido toomy (serviço ligado da Visual Studio do Azure Active Directory)
> [!div class="op_single_selector"]
> * [Introdução](vs-active-directory-webapi-getting-started.md)
> * [O que aconteceu](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Foram adicionadas referências
### <a name="nuget-package-references"></a>Referências de pacote NuGet
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>Referências de .NET
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Alterações do código
### <a name="code-files-were-added-tooyour-project"></a>Ficheiros de código foram adicionados tooyour projeto
Uma classe de startup da autenticação, **App_Start/Startup.Auth.cs** foi adicionado o projeto de tooyour que contém a lógica de arranque para a autenticação do Azure AD.

### <a name="startup-code-was-added-tooyour-project"></a>Código de arranque foi adicionado tooyour projeto
Se já tiver uma classe de Startup no seu projeto, Olá **configuração** método demasiado tooinclude atualizado uma chamada`ConfigureAuth(app)`. Caso contrário, uma classe de Startup foi adicionada tooyour projeto.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>O ficheiro App. config ou Web. config tem valores de configuração de novo.
foram adicionada Olá seguintes entradas de configuração.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>Foi criada uma aplicação do Azure AD
Aplicação do Azure AD foi criada no diretório de Olá que selecionou no Assistente de Olá.

[Saiba mais sobre o Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Se a opção posso marcada *desativar a autenticação de contas de utilizador individuais*, as alterações adicionais foram efetuadas toomy projeto?
As referências de pacote NuGet foram removidas e os ficheiros foram removidos e cópia de segurança. Dependendo do Estado de Olá do seu projeto, pode ter toomanually remover referências adicionais ou ficheiros, ou modificar o código conforme apropriado.

### <a name="nuget-package-references-removed-for-those-present"></a>Referências de pacote NuGet removidas (para as presente)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Ficheiros de código de uma cópia de segurança e remover (para as presente)
Cada um dos seguintes ficheiros foi uma cópia de segurança e removida do projeto de Olá. Ficheiros de cópia de segurança estão localizados numa pasta raiz de Olá do diretório do projeto Olá "Cópia de segurança".

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>Ficheiros de código de cópia de segurança (para as presente)
Cada um dos seguintes ficheiros tiver sido feita antes de a ser substituído. Ficheiros de cópia de segurança estão localizados numa pasta raiz de Olá do diretório do projeto Olá "Cópia de segurança".

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Se a opção posso marcada *ler os dados de diretório*, as alterações adicionais foram efetuadas toomy projeto?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Foram feitas alterações adicionais tooyour config ou Web. config
Olá seguintes entradas de configuração adicionais foram adicionadas.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>A aplicação do Active Directory do Azure foi atualizada
A aplicação do Active Directory do Azure foi atualizado tooinclude Olá *ler os dados de diretório* permissão e uma chave de adicional que foi criado, em seguida, que utilizou como Olá *ida: palavra-passe* no Olá `web.config` ficheiro.

## <a name="next-steps"></a>Passos seguintes
- [Saiba mais sobre o Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

