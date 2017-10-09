---
title: "erros de toodiagnose aaaHow Olá Assistente de ligação do Azure Active Directory"
description: "Assistente de ligação do Active Directory Olá detetou um tipo de autenticação incompatível"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="5c9f8-103">Diagnosticar erros com Olá Assistente de ligação do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c9f8-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="5c9f8-104">Ao detetar o código de autenticação anterior, o Assistente de Olá detetou um tipo de autenticação incompatível.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="5c9f8-105">O que está a ser modificado?</span><span class="sxs-lookup"><span data-stu-id="5c9f8-105">What is being checked?</span></span>
<span data-ttu-id="5c9f8-106">**Nota:** toocorrectly detetar anterior código de autenticação num projeto, projeto Olá tem de ser criado.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="5c9f8-107">Se encontrou o erro e não tiver um código de autenticação anterior no seu projeto, reconstruir e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="5c9f8-108">Tipos de projeto</span><span class="sxs-lookup"><span data-stu-id="5c9f8-108">Project Types</span></span>
<span data-ttu-id="5c9f8-109">Assistente de Olá verifica tipo Olá do projeto que está a desenvolver, de modo que pode inserir lógica de autenticação direita Olá no projeto Olá.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="5c9f8-110">Se não houver qualquer controlador que derive `ApiController` no projeto Olá, projeto Olá é considerado um projeto de end WebAPI.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="5c9f8-111">Se existirem apenas os controladores que derivem de `MVC.Controller` no projeto Olá, projeto Olá é considerado um projeto MVC.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="5c9f8-112">Tudo o resto não é suportado pelo Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="5c9f8-113">Código de autenticação compatível</span><span class="sxs-lookup"><span data-stu-id="5c9f8-113">Compatible Authentication Code</span></span>
<span data-ttu-id="5c9f8-114">Assistente de Olá também verifica a existência de definições de autenticação que foram anteriormente configuradas com o Assistente de Olá ou que são compatíveis com o Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="5c9f8-115">Se todas as definições estiverem presentes, é considerada um caso re-entrant e será apresentado o assistente Olá apresenta as definições de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="5c9f8-116">Se apenas algumas das definições de Olá estiverem presentes, é considerada um caso de erro.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="5c9f8-117">Num projeto MVC, o Assistente de Olá verifica a existência de qualquer um dos Olá definições, o que resultam da utilização anterior do Assistente de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5c9f8-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="5c9f8-118">Além disso, o Assistente de Olá verifica a existência de qualquer um dos Olá definições num projeto Web API, que resultam da utilização anterior do Assistente de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5c9f8-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="5c9f8-119">Código de autenticação incompatível</span><span class="sxs-lookup"><span data-stu-id="5c9f8-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="5c9f8-120">Por fim, o Assistente de Olá tenta versões de toodetect do código de autenticação que foram configuradas com versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="5c9f8-121">Se receber este erro, significa que projecto contém um tipo de autenticação incompatível.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="5c9f8-122">Assistente de Olá Deteta Olá seguintes tipos de autenticação de versões anteriores do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5c9f8-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="5c9f8-123">Autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="5c9f8-123">Windows Authentication</span></span> 
* <span data-ttu-id="5c9f8-124">Contas de utilizador individuais</span><span class="sxs-lookup"><span data-stu-id="5c9f8-124">Individual User Accounts</span></span> 
* <span data-ttu-id="5c9f8-125">Contas organizacionais</span><span class="sxs-lookup"><span data-stu-id="5c9f8-125">Organizational Accounts</span></span> 

<span data-ttu-id="5c9f8-126">toodetect autenticação do Windows num projeto MVC, o Assistente de Olá procura Olá `authentication` elemento a partir do seu **Web. config** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="5c9f8-127">toodetect autenticação do Windows num projeto Web API, o Assistente de Olá procura Olá `IISExpressWindowsAuthentication` elemento a partir do seu projeto **. csproj** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="5c9f8-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="5c9f8-128">autenticação de contas de utilizador individuais toodetect, assistente Olá procura do elemento de pacote Olá a partir do seu **Packages** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="5c9f8-129">toodetect um formulário antigo de autenticação da conta institucional, o Assistente de Olá procura Olá seguinte elemento a partir do **Web. config**:</span><span class="sxs-lookup"><span data-stu-id="5c9f8-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="5c9f8-130">tipo de autenticação do toochange Olá, remova o tipo de autenticação incompatível Olá e execute novamente o Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c9f8-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="5c9f8-131">Para obter mais informações, consulte [cenários de autenticação para o Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="5c9f8-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="5c9f8-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5c9f8-132">Next steps</span></span>
- [<span data-ttu-id="5c9f8-133">Cenários de autenticação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c9f8-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)