---
title: 'B2C do Azure AD: Proteger uma API Web utilizando Node.js | Microsoft Docs'
description: Como a API web de toobuild um Node.js que aceita tokens a partir de um inquilino do B2C
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="a8f44-103">B2C do Azure AD: Proteger uma API Web utilizando Node.js</span><span class="sxs-lookup"><span data-stu-id="a8f44-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="a8f44-104">Com o Azure Active Directory (Azure AD) B2C, pode proteger uma API web utilizando tokens de acesso de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a8f44-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="a8f44-105">Estes tokens permitem que as aplicações de cliente que utilizam a API do Azure AD B2C tooauthenticate toohello.</span><span class="sxs-lookup"><span data-stu-id="a8f44-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="a8f44-106">Este artigo mostra como toocreate uma API de "lista de tarefas" que permite aos utilizadores tooadd e a lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="a8f44-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="a8f44-107">Olá web API está protegida com o Azure AD B2C e só permite que os utilizadores autenticados toomanage respetiva lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="a8f44-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="a8f44-108">Este exemplo foi escrito utilizando o tooby toobe ligado nosso [aplicação de exemplo de iOS B2C](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="a8f44-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="a8f44-109">Olá passagem atual pela primeira vez e, em seguida, acompanhe com esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="a8f44-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="a8f44-110">**Passport** é o middleware de autenticação do Node.js.</span><span class="sxs-lookup"><span data-stu-id="a8f44-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="a8f44-111">Flexível e modular, o Passport pode ser instalado discretamente em qualquer aplicação Web baseada no Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="a8f44-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="a8f44-112">Um conjunto abrangente de estratégias suporta a autenticação utilizando um nome de utilizador e palavra-passe, o Facebook, o Twitter e muito mais.</span><span class="sxs-lookup"><span data-stu-id="a8f44-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="a8f44-113">Desenvolvemos uma estratégia para o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8f44-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a8f44-114">Instalará este módulo e, em seguida, adicionar Olá do Azure AD `passport-azure-ad` Plug-in.</span><span class="sxs-lookup"><span data-stu-id="a8f44-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="a8f44-115">toodo neste exemplo, tem de:</span><span class="sxs-lookup"><span data-stu-id="a8f44-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="a8f44-116">Registar uma aplicação com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8f44-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="a8f44-117">Configurar a sua aplicação toouse Passport `azure-ad-passport` Plug-in.</span><span class="sxs-lookup"><span data-stu-id="a8f44-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="a8f44-118">Configure uma cliente aplicação toocall Olá "lista de tarefas" API web.</span><span class="sxs-lookup"><span data-stu-id="a8f44-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="a8f44-119">Obter um diretório do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a8f44-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="a8f44-120">Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.</span><span class="sxs-lookup"><span data-stu-id="a8f44-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="a8f44-121">Um diretório é um contentor para todos os utilizadores, aplicações, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="a8f44-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="a8f44-122">Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="a8f44-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="a8f44-123">Criar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="a8f44-123">Create an application</span></span>
<span data-ttu-id="a8f44-124">Em seguida, terá de toocreate uma aplicação no diretório do B2C que dá ao Azure AD algumas informações que necessita de toosecurely comunicar com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="a8f44-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="a8f44-125">Neste caso, a aplicação de cliente Olá e web API são representadas por um único **ID da aplicação**, uma vez que compõem uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="a8f44-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="a8f44-126">toocreate uma aplicação, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a8f44-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="a8f44-127">É necessário:</span><span class="sxs-lookup"><span data-stu-id="a8f44-127">Be sure to:</span></span>

* <span data-ttu-id="a8f44-128">Incluir um **web app/web api** na aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="a8f44-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="a8f44-129">Introduzir `http://localhost/TodoListService` como um **URL de resposta**.</span><span class="sxs-lookup"><span data-stu-id="a8f44-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="a8f44-130">É Olá predefinido URL para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="a8f44-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="a8f44-131">Criar um **Segredo de aplicação** para a aplicação e copiá-lo.</span><span class="sxs-lookup"><span data-stu-id="a8f44-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="a8f44-132">Estes dados são necessários mais tarde.</span><span class="sxs-lookup"><span data-stu-id="a8f44-132">You need this data later.</span></span> <span data-ttu-id="a8f44-133">Tenha em atenção que este valor tem de toobe [XML de escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de o utilizar.</span><span class="sxs-lookup"><span data-stu-id="a8f44-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="a8f44-134">Olá cópia **ID da aplicação** que é atribuído tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="a8f44-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="a8f44-135">Estes dados são necessários mais tarde.</span><span class="sxs-lookup"><span data-stu-id="a8f44-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="a8f44-136">Criar as políticas</span><span class="sxs-lookup"><span data-stu-id="a8f44-136">Create your policies</span></span>
<span data-ttu-id="a8f44-137">No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a8f44-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="a8f44-138">Esta aplicação contém duas experiências de identidade: registo e início de sessão.</span><span class="sxs-lookup"><span data-stu-id="a8f44-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="a8f44-139">Tem toocreate uma política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="a8f44-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="a8f44-140">Quando criar as três políticas, não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="a8f44-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="a8f44-141">Escolha Olá **nome a apresentar** e outros atributos de inscrição na política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="a8f44-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="a8f44-142">Escolha Olá **nome a apresentar** e **ID de objeto** afirmações de aplicação em cada política.</span><span class="sxs-lookup"><span data-stu-id="a8f44-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="a8f44-143">Também pode escolher outras afirmações.</span><span class="sxs-lookup"><span data-stu-id="a8f44-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="a8f44-144">Copie Olá **nome** de cada política depois de a criar.</span><span class="sxs-lookup"><span data-stu-id="a8f44-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="a8f44-145">Deve ter o prefixo de Olá `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="a8f44-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="a8f44-146">Vai necessitar destes nomes de política mais tarde.</span><span class="sxs-lookup"><span data-stu-id="a8f44-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="a8f44-147">Depois de criar as três políticas, está pronto toobuild a aplicação.</span><span class="sxs-lookup"><span data-stu-id="a8f44-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="a8f44-148">toolearn sobre como funcionam as políticas no Azure AD B2C, comece com Olá [.NET introdução à aplicação web tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a8f44-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="a8f44-149">Transferir o código de Olá</span><span class="sxs-lookup"><span data-stu-id="a8f44-149">Download hello code</span></span>
<span data-ttu-id="a8f44-150">Olá código para este tutorial [é mantido no GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="a8f44-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="a8f44-151">exemplo de Olá toobuild como vá, pode [transferir um projeto de estrutura como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="a8f44-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="a8f44-152">Também pode clonar a estrutura de Olá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="a8f44-153">aplicação Olá concluída está também [disponível como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) ou Olá `complete` ramo do Olá mesmo repositório.</span><span class="sxs-lookup"><span data-stu-id="a8f44-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="a8f44-154">Transferir Node.js para a plataforma</span><span class="sxs-lookup"><span data-stu-id="a8f44-154">Download Node.js for your platform</span></span>
<span data-ttu-id="a8f44-155">toosuccessfully utilizar este exemplo, precisa de uma instalação do Node.js.</span><span class="sxs-lookup"><span data-stu-id="a8f44-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="a8f44-156">Instalar Node.js de [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a8f44-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="a8f44-157">Instalar MongoDB para a plataforma</span><span class="sxs-lookup"><span data-stu-id="a8f44-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="a8f44-158">toosuccessfully utilizar este exemplo, precisa de uma instalação do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a8f44-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="a8f44-159">Utilizamos o MongoDB toomake a API REST persistente em instâncias de servidor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="a8f44-160">Instalar MongoDB de [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="a8f44-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="a8f44-161">Esta passagem parte do princípio de que usa Olá servidor e a instalação pontos finais predefinidos para o MongoDB, que a hora de Olá desta redação é `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="a8f44-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="a8f44-162">Instalar os módulos do Restify Olá na API web</span><span class="sxs-lookup"><span data-stu-id="a8f44-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="a8f44-163">Utilizamos o Restify toobuild a API REST.</span><span class="sxs-lookup"><span data-stu-id="a8f44-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="a8f44-164">O Restify é uma estrutura de aplicação Node.js mínima e flexível derivada do Express.</span><span class="sxs-lookup"><span data-stu-id="a8f44-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="a8f44-165">Tem um conjunto robusto de funcionalidades para a criação de APIs REST por cima do Connect.</span><span class="sxs-lookup"><span data-stu-id="a8f44-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="a8f44-166">Instalação do Restify</span><span class="sxs-lookup"><span data-stu-id="a8f44-166">Install Restify</span></span>
<span data-ttu-id="a8f44-167">Olá linha de comandos, altere o diretório demasiado`azuread`.</span><span class="sxs-lookup"><span data-stu-id="a8f44-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="a8f44-168">Se hello `azuread` diretório não existe, criá-la.</span><span class="sxs-lookup"><span data-stu-id="a8f44-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="a8f44-169">`cd azuread` ou `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="a8f44-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="a8f44-170">Introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a8f44-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="a8f44-171">Este comando instala o Restify.</span><span class="sxs-lookup"><span data-stu-id="a8f44-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="a8f44-172">Obteve um erro?</span><span class="sxs-lookup"><span data-stu-id="a8f44-172">Did you get an error?</span></span>
<span data-ttu-id="a8f44-173">Em alguns sistemas operativos, quando utiliza `npm`, poderá receber o erro de Olá `Error: EPERM, chmod '/usr/local/bin/..'` e um pedido para que execute conta Olá como administrador.</span><span class="sxs-lookup"><span data-stu-id="a8f44-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="a8f44-174">Se o problema ocorrer, utilize Olá `sudo` comando toorun `npm` a um nível de privilégio mais elevado.</span><span class="sxs-lookup"><span data-stu-id="a8f44-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="a8f44-175">Obteve um erro de DTrace?</span><span class="sxs-lookup"><span data-stu-id="a8f44-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="a8f44-176">Quando instalar o Restify, pode aparecer o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="a8f44-176">You may see something like this text when you install Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="a8f44-177">O Restify fornece um mecanismo poderoso para rastreio de chamadas REST utilizando o DTrace.</span><span class="sxs-lookup"><span data-stu-id="a8f44-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="a8f44-178">No entanto, muitos sistemas operativos não tem o DTrace disponível.</span><span class="sxs-lookup"><span data-stu-id="a8f44-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="a8f44-179">Pode ignorar com segurança estes erros.</span><span class="sxs-lookup"><span data-stu-id="a8f44-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="a8f44-180">saída de Olá do comando de Olá deve aparecer semelhante toothis texto:</span><span class="sxs-lookup"><span data-stu-id="a8f44-180">hello output of hello command should appear similar toothis text:</span></span>

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="a8f44-181">Instalar o Passport na API Web</span><span class="sxs-lookup"><span data-stu-id="a8f44-181">Install Passport in your web API</span></span>
<span data-ttu-id="a8f44-182">Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="a8f44-183">Instale o Passport utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a8f44-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="a8f44-184">saída de Olá do comando de Olá deve ser semelhante toothis texto:</span><span class="sxs-lookup"><span data-stu-id="a8f44-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="a8f44-185">Adicionar passport-azuread tooyour web API</span><span class="sxs-lookup"><span data-stu-id="a8f44-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="a8f44-186">Em seguida, adicione a estratégia de OAuth Olá utilizando `passport-azuread`, um conjunto de estratégias que ligam o Azure AD com o Passport.</span><span class="sxs-lookup"><span data-stu-id="a8f44-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="a8f44-187">Utilize esta estratégia para os tokens de portador no exemplo de REST API de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="a8f44-188">Embora o OAuth2 forneça uma estrutura onde pode ser emitido qualquer tipo de token conhecido, apenas alguns tipos de tokens passaram a ser amplamente utilizados.</span><span class="sxs-lookup"><span data-stu-id="a8f44-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="a8f44-189">tokens de Olá para proteger os pontos finais são tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="a8f44-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="a8f44-190">Estes tipos de tokens são Olá amplamente emitido no OAuth2.</span><span class="sxs-lookup"><span data-stu-id="a8f44-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="a8f44-191">Várias implementações partem do princípio de que os tokens de portador são o único tipo de Olá de token emitido.</span><span class="sxs-lookup"><span data-stu-id="a8f44-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="a8f44-192">Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="a8f44-193">Instalar Olá Passport `passport-azure-ad` módulo Olá os seguintes comandos a utilizar:</span><span class="sxs-lookup"><span data-stu-id="a8f44-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="a8f44-194">saída de Olá do comando de Olá deve ser semelhante toothis texto:</span><span class="sxs-lookup"><span data-stu-id="a8f44-194">hello output of hello command should be similar toothis text:</span></span>

``
passport-azure-ad@1.0.0 node_modules/passport-azure-ad
├── xtend@4.0.0
├── xmldom@0.1.19
├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
├── underscore@1.8.3
├── async@1.3.0
├── jsonwebtoken@5.0.2
├── xml-crypto@0.5.27 (xpath.js@1.0.6)
├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
└── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="a8f44-195">Adicionar API web do MongoDB módulos tooyour</span><span class="sxs-lookup"><span data-stu-id="a8f44-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="a8f44-196">Este exemplo utiliza o MongoDB como arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="a8f44-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="a8f44-197">Para tal, instale o Mongoose, um plug-in de gestão de modelos e esquemas muito utilizado.</span><span class="sxs-lookup"><span data-stu-id="a8f44-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="a8f44-198">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="a8f44-198">Install additional modules</span></span>
<span data-ttu-id="a8f44-199">Em seguida, instale Olá restantes módulos necessários.</span><span class="sxs-lookup"><span data-stu-id="a8f44-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="a8f44-200">Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="a8f44-201">Instalar módulos Olá no seu `node_modules` diretório:</span><span class="sxs-lookup"><span data-stu-id="a8f44-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="a8f44-202">Crie um ficheiro de server.js com as suas dependências</span><span class="sxs-lookup"><span data-stu-id="a8f44-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="a8f44-203">Olá `server.js` ficheiro fornece maioria Olá da funcionalidade de Olá para o servidor de Web API.</span><span class="sxs-lookup"><span data-stu-id="a8f44-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="a8f44-204">Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="a8f44-205">Crie um ficheiro `server.js` num editor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="a8f44-206">Adicione Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="a8f44-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="a8f44-207">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-207">Save hello file.</span></span> <span data-ttu-id="a8f44-208">Devolver tooit mais tarde.</span><span class="sxs-lookup"><span data-stu-id="a8f44-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="a8f44-209">Criar um toostore do ficheiro de config.js as definições do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8f44-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="a8f44-210">Este ficheiro de código transmite os parâmetros de configuração de Olá do seu Portal do Azure AD toohello `Passport.js` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="a8f44-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="a8f44-211">Criou estes valores de configuração quando adicionou o portal de toohello Olá web API na Olá primeira parte passagem Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="a8f44-212">Vamos explicar que tooput valores Olá destes parâmetros depois de copiar o código de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="a8f44-213">Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="a8f44-214">Crie um ficheiro `config.js` num editor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="a8f44-215">Adicione Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="a8f44-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="a8f44-216">Valores necessários</span><span class="sxs-lookup"><span data-stu-id="a8f44-216">Required values</span></span>
<span data-ttu-id="a8f44-217">`clientID`: Olá ID de cliente da aplicação Web API.</span><span class="sxs-lookup"><span data-stu-id="a8f44-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="a8f44-218">`IdentityMetadata`: Aqui é onde `passport-azure-ad` procura dos seus dados de configuração para o fornecedor de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="a8f44-219">Procura também para Olá chaves toovalidate Olá JSON web de tokens.</span><span class="sxs-lookup"><span data-stu-id="a8f44-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="a8f44-220">`audience`: Olá identificador de recurso uniforme (URI) do portal de Olá que identifica a sua aplicação de chamada.</span><span class="sxs-lookup"><span data-stu-id="a8f44-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="a8f44-221">`tenantName`: o nome do seu inquilino (por exemplo, **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="a8f44-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="a8f44-222">`policyName`: Olá política que pretende que os tokens de Olá toovalidate futuras do servidor de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a8f44-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="a8f44-223">Esta política deve ser Olá a mesma política que utiliza numa aplicação de cliente Olá para início de sessão.</span><span class="sxs-lookup"><span data-stu-id="a8f44-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="a8f44-224">Por agora, utilize Olá mesmo políticas em toda a configuração de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="a8f44-225">Se já tiver concluído uma passagem e criado estas políticas, não precisa de toodo, por isso, novamente.</span><span class="sxs-lookup"><span data-stu-id="a8f44-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="a8f44-226">Uma vez concluída a passagem de Olá, não deverá ser preciso tooset configurar novas políticas para passagens de cliente no site de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="a8f44-227">Adicione o ficheiro de server.js tooyour de configuração</span><span class="sxs-lookup"><span data-stu-id="a8f44-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="a8f44-228">valores de Olá tooread de Olá `config.js` de ficheiros que criou, adicione Olá `.config` ficheiro como um recurso necessário na sua aplicação e, em seguida, defina Olá variáveis globais toothose no Olá `config.js` documento.</span><span class="sxs-lookup"><span data-stu-id="a8f44-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="a8f44-229">Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="a8f44-230">Abra Olá `server.js` ficheiro num editor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="a8f44-231">Adicione Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="a8f44-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="a8f44-232">Adicionar uma nova secção demasiado`server.js` que inclua Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="a8f44-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="a8f44-233">Em seguida, vamos adicionar alguns marcadores de posição para os utilizadores Olá recebido do nosso aplicações chamadas.</span><span class="sxs-lookup"><span data-stu-id="a8f44-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="a8f44-234">Vamos avançar e criar também o nosso registo.</span><span class="sxs-lookup"><span data-stu-id="a8f44-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="a8f44-235">Adicionar informações de esquema e modelo do MongoDB de Olá utilizando o Mongoose</span><span class="sxs-lookup"><span data-stu-id="a8f44-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="a8f44-236">Olá preparação pays como colocar estes três ficheiros num serviço REST API.</span><span class="sxs-lookup"><span data-stu-id="a8f44-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="a8f44-237">Para esta passagem, utilize MongoDB toostore as suas tarefas, conforme debatido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a8f44-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="a8f44-238">No Olá `config.js` ficheiro, chamado a base de dados **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="a8f44-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="a8f44-239">Esse nome foi também o que colocou no final Olá Olá `mongoose_auth_local` URL de ligação.</span><span class="sxs-lookup"><span data-stu-id="a8f44-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="a8f44-240">Não precisa de toocreate esta base de dados previamente no MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a8f44-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="a8f44-241">Cria a base de dados de Olá para si na execução de primeiro Olá da aplicação de servidor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="a8f44-242">Depois de indicar servidor Olá que toouse de base de dados de MongoDB, terá de toowrite algumas modelo do código adicional toocreate Olá e o esquema para as tarefas de servidor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="a8f44-243">Expanda o modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="a8f44-243">Expand hello model</span></span>
<span data-ttu-id="a8f44-244">Este modelo de esquema é simples.</span><span class="sxs-lookup"><span data-stu-id="a8f44-244">This schema model is simple.</span></span> <span data-ttu-id="a8f44-245">Pode expandi-lo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="a8f44-245">You can expand it as required.</span></span>

<span data-ttu-id="a8f44-246">`owner`: Quem é atribuído toohello tarefas.</span><span class="sxs-lookup"><span data-stu-id="a8f44-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="a8f44-247">Este objeto é uma **cadeia**.</span><span class="sxs-lookup"><span data-stu-id="a8f44-247">This object is a **string**.</span></span>  

<span data-ttu-id="a8f44-248">`Text`: tarefa Olá propriamente dita.</span><span class="sxs-lookup"><span data-stu-id="a8f44-248">`Text`: hello task itself.</span></span> <span data-ttu-id="a8f44-249">Este objeto é uma **cadeia**.</span><span class="sxs-lookup"><span data-stu-id="a8f44-249">This object is a **string**.</span></span>

<span data-ttu-id="a8f44-250">`date`: data de Olá essa tarefa Olá deve ser concluída.</span><span class="sxs-lookup"><span data-stu-id="a8f44-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="a8f44-251">Este objeto é uma **datetime**.</span><span class="sxs-lookup"><span data-stu-id="a8f44-251">This object is a **datetime**.</span></span>

<span data-ttu-id="a8f44-252">`completed`: Se a tarefa de Olá está concluída.</span><span class="sxs-lookup"><span data-stu-id="a8f44-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="a8f44-253">Este objeto é um **Booleano**.</span><span class="sxs-lookup"><span data-stu-id="a8f44-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="a8f44-254">Criar o esquema de Olá no código Olá</span><span class="sxs-lookup"><span data-stu-id="a8f44-254">Create hello schema in hello code</span></span>
<span data-ttu-id="a8f44-255">Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="a8f44-256">Abra Olá `server.js` ficheiro num editor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="a8f44-257">Adicione Olá seguindo as informações abaixo entrada de configuração de Olá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="a8f44-258">Cria o esquema de Olá pela primeira vez e, em seguida, criar um objeto de modelo que utilize toostore os dados em todo o Olá code quando definir o **rotas**.</span><span class="sxs-lookup"><span data-stu-id="a8f44-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="a8f44-259">Adicionar rotas ao seu servidor de tarefas da API REST</span><span class="sxs-lookup"><span data-stu-id="a8f44-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="a8f44-260">Agora que tem um toowork de modelo de base de dados com, adicione rotas de Olá que utilizar para o servidor de REST API.</span><span class="sxs-lookup"><span data-stu-id="a8f44-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="a8f44-261">Sobre rotas no Restify</span><span class="sxs-lookup"><span data-stu-id="a8f44-261">About routes in Restify</span></span>
<span data-ttu-id="a8f44-262">As rotas funcionam no Restify Olá mesma maneira que funcionam quando utilizarem a pilha de Express de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="a8f44-263">Definir rotas utilizando Olá URI que espera toocall de aplicações de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="a8f44-264">Um padrão normal para uma rota do Restify é:</span><span class="sxs-lookup"><span data-stu-id="a8f44-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="a8f44-265">O Restify e o Express podem fornecer funcionalidades muito mais aprofundada, tais como, definir tipos de aplicações e efetuar encaminhamentos complexos para diferentes pontos finais.</span><span class="sxs-lookup"><span data-stu-id="a8f44-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="a8f44-266">Para efeitos de Olá deste tutorial, iremos manter estas rotas simples.</span><span class="sxs-lookup"><span data-stu-id="a8f44-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="a8f44-267">Adicionar servidor de tooyour de rotas predefinidas</span><span class="sxs-lookup"><span data-stu-id="a8f44-267">Add default routes tooyour server</span></span>
<span data-ttu-id="a8f44-268">Agora a adicionar rotas CRUD básicas Olá de **criar** e **lista** para a nossa API REST.</span><span class="sxs-lookup"><span data-stu-id="a8f44-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="a8f44-269">Podem encontrar outras rotas de Olá `complete` ramo do exemplo Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="a8f44-270">Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="a8f44-271">Abra Olá `server.js` ficheiro num editor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="a8f44-272">Abaixo entradas da base de dados de Olá efetuadas acima adicionar Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="a8f44-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err)
            return next(err);

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Add one!");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}
```


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="a8f44-273">Adicionar tratamento de erro para rotas de Olá</span><span class="sxs-lookup"><span data-stu-id="a8f44-273">Add error handling for hello routes</span></span>
<span data-ttu-id="a8f44-274">Adicione alguns processamento de erros para que possa comunicar quaisquer problemas que encontre toohello back-cliente de forma a que possa compreender.</span><span class="sxs-lookup"><span data-stu-id="a8f44-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="a8f44-275">Adicione Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="a8f44-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="create-your-server"></a><span data-ttu-id="a8f44-276">Criar o seu servidor</span><span class="sxs-lookup"><span data-stu-id="a8f44-276">Create your server</span></span>
<span data-ttu-id="a8f44-277">Agora definiu a base de dados e colocou as rotas.</span><span class="sxs-lookup"><span data-stu-id="a8f44-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="a8f44-278">Olá coisa toodo é a instância do servidor de Olá tooadd que gere as chamadas.</span><span class="sxs-lookup"><span data-stu-id="a8f44-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="a8f44-279">O restify e o Express fornecem personalização avançada para um servidor de REST API, mas vamos utilizar a configuração mais básica do Olá aqui.</span><span class="sxs-lookup"><span data-stu-id="a8f44-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="a8f44-280">Adicionar Olá rotas toohello servidor (sem autenticação)</span><span class="sxs-lookup"><span data-stu-id="a8f44-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="a8f44-281">Adicionar o servidor de REST API de tooyour de autenticação</span><span class="sxs-lookup"><span data-stu-id="a8f44-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="a8f44-282">Agora que um servidor de API REST está em execução, pode torná-lo útil em relação ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8f44-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="a8f44-283">Olá linha de comandos, altere o diretório demasiado`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="a8f44-284">Utilizar Olá OIDCBearerStrategy que está incluído no passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="a8f44-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="a8f44-285">Quando escreve APIs, deve ligar sempre Olá dados toosomething exclusivo a partir do token de Olá que Olá utilizador não pode falsificar.</span><span class="sxs-lookup"><span data-stu-id="a8f44-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="a8f44-286">Quando o servidor de Olá armazena itens ToDo, aparece, por isso, com base no Olá **oid** de utilizador de Olá no token de Olá (chamado através de token.oid), que passa no campo de proprietário"Olá".</span><span class="sxs-lookup"><span data-stu-id="a8f44-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="a8f44-287">Este valor garante que apenas esse utilizador pode aceder aos próprios itens ToDo.</span><span class="sxs-lookup"><span data-stu-id="a8f44-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="a8f44-288">Não há nenhuma exposição na Olá API de "proprietário", pelo que um utilizador externo pode pedir dos outros itens ToDo, mesmo que estejam autenticados.</span><span class="sxs-lookup"><span data-stu-id="a8f44-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="a8f44-289">Em seguida, utilize a estratégia de portador Olá que vem com `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="a8f44-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="a8f44-290">O Passport utiliza Olá mesmo padrão para todas as respetivas estratégias.</span><span class="sxs-lookup"><span data-stu-id="a8f44-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="a8f44-291">Passe-o como uma `function()` que tem `token` e `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="a8f44-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="a8f44-292">estratégia de Olá volta a tooyou depois-tem de fazer todo o trabalho.</span><span class="sxs-lookup"><span data-stu-id="a8f44-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="a8f44-293">Deve armazenar o utilizador Olá e guardar o token de Olá, de modo que não seja necessário tooask-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="a8f44-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f44-294">código de Olá acima aceita qualquer utilizador que tooauthenticate tooyour servidor.</span><span class="sxs-lookup"><span data-stu-id="a8f44-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="a8f44-295">Este processo é conhecido como registo automático.</span><span class="sxs-lookup"><span data-stu-id="a8f44-295">This process is known as autoregistration.</span></span> <span data-ttu-id="a8f44-296">Em servidores de produção, não permita que qualquer API de Olá de acesso de utilizadores sem primeiro passá-los através de um processo de registo.</span><span class="sxs-lookup"><span data-stu-id="a8f44-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="a8f44-297">Este processo é normalmente padrão de Olá normal que vemos nas aplicações de consumidor que lhe permitem tooregister utilizando o Facebook, mas, em seguida, pedir-lhe que toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="a8f44-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="a8f44-298">Se este programa não era um programa da linha de comandos, poderíamos extrair o e-mail de Olá do objeto de token de Olá que é devolvido e, em seguida, mais frequentes utilizadores toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="a8f44-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="a8f44-299">Porque se trata de uma amostra, iremos adicioná-los tooan dentro da memória da base de dados.</span><span class="sxs-lookup"><span data-stu-id="a8f44-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="a8f44-300">Execute o tooverify de aplicação de servidor que as TI a rejeita</span><span class="sxs-lookup"><span data-stu-id="a8f44-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="a8f44-301">Pode utilizar `curl` toosee se tem agora proteção do OAuth2 nos seus pontos finais.</span><span class="sxs-lookup"><span data-stu-id="a8f44-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="a8f44-302">Olá cabeçalhos devolvidos devem ser suficiente tootell que estão no caminho certo Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f44-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="a8f44-303">Certifique-se de que a instância do MongoDB está em execução:</span><span class="sxs-lookup"><span data-stu-id="a8f44-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="a8f44-304">Alterar o diretório de toohello e o servidor de execução Olá:</span><span class="sxs-lookup"><span data-stu-id="a8f44-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="a8f44-305">Numa nova janela de terminal, execute `curl`</span><span class="sxs-lookup"><span data-stu-id="a8f44-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="a8f44-306">Tente um POST básico:</span><span class="sxs-lookup"><span data-stu-id="a8f44-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="a8f44-307">Um erro 401 é resposta Olá que quiser.</span><span class="sxs-lookup"><span data-stu-id="a8f44-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="a8f44-308">Indica que camada do Passport Olá está a tentar tooredirect toohello autorizar o ponto final.</span><span class="sxs-lookup"><span data-stu-id="a8f44-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="a8f44-309">Agora tem um serviço de API REST que utiliza o OAuth2</span><span class="sxs-lookup"><span data-stu-id="a8f44-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="a8f44-310">Tem implementada uma API REST utilizando o Restify e o OAuth!</span><span class="sxs-lookup"><span data-stu-id="a8f44-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="a8f44-311">Tem agora código suficiente para que possam continuar toodevelop o serviço e criar neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="a8f44-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="a8f44-312">Fez tudo o que podia com este servidor sem utilizar um cliente compatível com o OAuth2.</span><span class="sxs-lookup"><span data-stu-id="a8f44-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="a8f44-313">Para esse passo seguinte, utilize uma passagem adicional, como o nosso [ligar tooa web API utilizando o iOS com o B2C](active-directory-b2c-devquickstarts-ios.md) explicação passo a passo.</span><span class="sxs-lookup"><span data-stu-id="a8f44-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8f44-314">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a8f44-314">Next steps</span></span>
<span data-ttu-id="a8f44-315">Agora pode mover tópicos toomore avançada, tais como:</span><span class="sxs-lookup"><span data-stu-id="a8f44-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="a8f44-316">Ligar tooa web API utilizando o iOS com o B2C</span><span class="sxs-lookup"><span data-stu-id="a8f44-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
