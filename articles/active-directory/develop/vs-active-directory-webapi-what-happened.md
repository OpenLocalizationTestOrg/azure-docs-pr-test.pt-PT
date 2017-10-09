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
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="2cbdc-103">Projeto de end WebApi que tenham acontecido toomy (serviço ligado da Visual Studio do Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="2cbdc-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2cbdc-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="2cbdc-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="2cbdc-105">O que aconteceu</span><span class="sxs-lookup"><span data-stu-id="2cbdc-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="2cbdc-106">Foram adicionadas referências</span><span class="sxs-lookup"><span data-stu-id="2cbdc-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="2cbdc-107">Referências de pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="2cbdc-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="2cbdc-108">Referências de .NET</span><span class="sxs-lookup"><span data-stu-id="2cbdc-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="2cbdc-109">Alterações do código</span><span class="sxs-lookup"><span data-stu-id="2cbdc-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="2cbdc-110">Ficheiros de código foram adicionados tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="2cbdc-110">Code files were added tooyour project</span></span>
<span data-ttu-id="2cbdc-111">Uma classe de startup da autenticação, **App_Start/Startup.Auth.cs** foi adicionado o projeto de tooyour que contém a lógica de arranque para a autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="2cbdc-112">Código de arranque foi adicionado tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="2cbdc-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="2cbdc-113">Se já tiver uma classe de Startup no seu projeto, Olá **configuração** método demasiado tooinclude atualizado uma chamada`ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="2cbdc-114">Caso contrário, uma classe de Startup foi adicionada tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="2cbdc-115">O ficheiro App. config ou Web. config tem valores de configuração de novo.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="2cbdc-116">foram adicionada Olá seguintes entradas de configuração.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="2cbdc-117">Foi criada uma aplicação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2cbdc-117">An Azure AD App was created</span></span>
<span data-ttu-id="2cbdc-118">Aplicação do Azure AD foi criada no diretório de Olá que selecionou no Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="2cbdc-119">Saiba mais sobre o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2cbdc-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="2cbdc-120">Se a opção posso marcada *desativar a autenticação de contas de utilizador individuais*, as alterações adicionais foram efetuadas toomy projeto?</span><span class="sxs-lookup"><span data-stu-id="2cbdc-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="2cbdc-121">As referências de pacote NuGet foram removidas e os ficheiros foram removidos e cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="2cbdc-122">Dependendo do Estado de Olá do seu projeto, pode ter toomanually remover referências adicionais ou ficheiros, ou modificar o código conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="2cbdc-123">Referências de pacote NuGet removidas (para as presente)</span><span class="sxs-lookup"><span data-stu-id="2cbdc-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="2cbdc-124">Ficheiros de código de uma cópia de segurança e remover (para as presente)</span><span class="sxs-lookup"><span data-stu-id="2cbdc-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="2cbdc-125">Cada um dos seguintes ficheiros foi uma cópia de segurança e removida do projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="2cbdc-126">Ficheiros de cópia de segurança estão localizados numa pasta raiz de Olá do diretório do projeto Olá "Cópia de segurança".</span><span class="sxs-lookup"><span data-stu-id="2cbdc-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="2cbdc-127">Ficheiros de código de cópia de segurança (para as presente)</span><span class="sxs-lookup"><span data-stu-id="2cbdc-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="2cbdc-128">Cada um dos seguintes ficheiros tiver sido feita antes de a ser substituído.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="2cbdc-129">Ficheiros de cópia de segurança estão localizados numa pasta raiz de Olá do diretório do projeto Olá "Cópia de segurança".</span><span class="sxs-lookup"><span data-stu-id="2cbdc-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="2cbdc-130">Se a opção posso marcada *ler os dados de diretório*, as alterações adicionais foram efetuadas toomy projeto?</span><span class="sxs-lookup"><span data-stu-id="2cbdc-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="2cbdc-131">Foram feitas alterações adicionais tooyour config ou Web. config</span><span class="sxs-lookup"><span data-stu-id="2cbdc-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="2cbdc-132">Olá seguintes entradas de configuração adicionais foram adicionadas.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="2cbdc-133">A aplicação do Active Directory do Azure foi atualizada</span><span class="sxs-lookup"><span data-stu-id="2cbdc-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="2cbdc-134">A aplicação do Active Directory do Azure foi atualizado tooinclude Olá *ler os dados de diretório* permissão e uma chave de adicional que foi criado, em seguida, que utilizou como Olá *ida: palavra-passe* no Olá `web.config` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2cbdc-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cbdc-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2cbdc-135">Next steps</span></span>
- [<span data-ttu-id="2cbdc-136">Saiba mais sobre o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2cbdc-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

