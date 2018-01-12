---
title: 'B2C do Azure AD: Proteger uma API Web utilizando Node.js | Microsoft Docs'
description: Como criar uma API Web de Node.js que aceita tokens de um inquilino do B2C
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
ms.openlocfilehash: 6480be75c314ede1b786e959a79c0385dd2edea8
ms.sourcegitcommit: 73f159cdbc122ffe42f3e1f7a3de05f77b6a4725
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="e667d-103">B2C do Azure AD: Proteger uma API Web utilizando Node.js</span><span class="sxs-lookup"><span data-stu-id="e667d-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="e667d-104">Com o Azure Active Directory (Azure AD) B2C, pode proteger uma API web utilizando tokens de acesso de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="e667d-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="e667d-105">Estes tokens permitem que as aplicações de cliente que utilizam o Azure AD B2C se autentiquem na API.</span><span class="sxs-lookup"><span data-stu-id="e667d-105">These tokens allow your client apps that use Azure AD B2C to authenticate to the API.</span></span> <span data-ttu-id="e667d-106">Este artigo mostra-lhe como criar uma API de "lista de tarefas" que permite aos utilizadores adicionar e listar tarefas.</span><span class="sxs-lookup"><span data-stu-id="e667d-106">This article shows you how to create a "to-do list" API that allows users to add and list tasks.</span></span> <span data-ttu-id="e667d-107">A API Web é protegida ao utilizar o Azure AD B2C e só permite que os utilizadores autenticados façam a gestão da respetiva lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e667d-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="e667d-108">Este exemplo foi escrito para fazer uma ligação utilizando a nossa [aplicação de exemplo B2C para iOS](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="e667d-108">This sample was written to be connected to by using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="e667d-109">Primeiro, explore esta passagem e, em seguida, acompanhe com esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="e667d-109">Do the current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="e667d-110">**Passport** é o middleware de autenticação do Node.js.</span><span class="sxs-lookup"><span data-stu-id="e667d-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="e667d-111">Flexível e modular, o Passport pode ser instalado discretamente em qualquer aplicação Web baseada no Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="e667d-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="e667d-112">Um conjunto abrangente de estratégias suporta a autenticação utilizando um nome de utilizador e palavra-passe, o Facebook, o Twitter e muito mais.</span><span class="sxs-lookup"><span data-stu-id="e667d-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="e667d-113">Desenvolvemos uma estratégia para o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e667d-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e667d-114">Instale este módulo e, em seguida, adicione o plug-in `passport-azure-ad` do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e667d-114">You install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="e667d-115">Para efetuar este exemplo, tem de:</span><span class="sxs-lookup"><span data-stu-id="e667d-115">To do this sample, you need to:</span></span>

1. <span data-ttu-id="e667d-116">Registar uma aplicação com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e667d-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="e667d-117">Configure a aplicação para utilizar o plug-in `azure-ad-passport` do Passport.</span><span class="sxs-lookup"><span data-stu-id="e667d-117">Set up your application to use Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="e667d-118">Configure uma aplicação de cliente para chamar a API Web da “lista de ações a fazer”.</span><span class="sxs-lookup"><span data-stu-id="e667d-118">Configure a client application to call the "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="e667d-119">Obter um diretório do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e667d-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="e667d-120">Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.</span><span class="sxs-lookup"><span data-stu-id="e667d-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="e667d-121">Um diretório é um contentor para todos os utilizadores, aplicações, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="e667d-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="e667d-122">Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="e667d-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="e667d-123">Criar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="e667d-123">Create an application</span></span>
<span data-ttu-id="e667d-124">Em seguida, precisa de criar uma aplicação no seu diretório do B2C que dá ao Azure AD algumas informações necessárias para comunicar de forma segura com a aplicação.</span><span class="sxs-lookup"><span data-stu-id="e667d-124">Next, you need to create an app in your B2C directory that gives Azure AD some information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="e667d-125">Neste caso, a aplicação cliente e a API Web são representadas por um único **ID de Aplicação** porque compõem uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="e667d-125">In this case, both the client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="e667d-126">Para criar uma aplicação, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="e667d-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="e667d-127">É necessário:</span><span class="sxs-lookup"><span data-stu-id="e667d-127">Be sure to:</span></span>

* <span data-ttu-id="e667d-128">Incluir uma **aplicação Web/API Web** na aplicação</span><span class="sxs-lookup"><span data-stu-id="e667d-128">Include a **web app/web api** in the application</span></span>
* <span data-ttu-id="e667d-129">Introduzir `http://localhost/TodoListService` como um **URL de resposta**.</span><span class="sxs-lookup"><span data-stu-id="e667d-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="e667d-130">É o URL predefinido para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="e667d-130">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="e667d-131">Criar um **Segredo de aplicação** para a aplicação e copiá-lo.</span><span class="sxs-lookup"><span data-stu-id="e667d-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="e667d-132">Estes dados são necessários mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e667d-132">You need this data later.</span></span> <span data-ttu-id="e667d-133">Tenha em atenção que este valor de ser [XML de escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de o utilizar.</span><span class="sxs-lookup"><span data-stu-id="e667d-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="e667d-134">Copiar a **ID da Aplicação** atribuída à aplicação.</span><span class="sxs-lookup"><span data-stu-id="e667d-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="e667d-135">Estes dados são necessários mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e667d-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="e667d-136">Criar as políticas</span><span class="sxs-lookup"><span data-stu-id="e667d-136">Create your policies</span></span>
<span data-ttu-id="e667d-137">No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e667d-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="e667d-138">Esta aplicação contém duas experiências de identidade: registo e início de sessão.</span><span class="sxs-lookup"><span data-stu-id="e667d-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="e667d-139">Tem de criar uma política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="e667d-139">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="e667d-140">Quando criar as três políticas, não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="e667d-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="e667d-141">Escolher o **Nome a apresentar** e os atributos de inscrição na política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="e667d-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="e667d-142">Escolher as afirmações de aplicação **Nome a apresentar** e **ID de objeto** em cada política.</span><span class="sxs-lookup"><span data-stu-id="e667d-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="e667d-143">Também pode escolher outras afirmações.</span><span class="sxs-lookup"><span data-stu-id="e667d-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="e667d-144">Copie o **Nome** de cada política depois de criá-la.</span><span class="sxs-lookup"><span data-stu-id="e667d-144">Copy down the **Name** of each policy after you create it.</span></span> <span data-ttu-id="e667d-145">Deve ter o prefixo `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="e667d-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="e667d-146">Vai necessitar destes nomes de política mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e667d-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="e667d-147">Depois de criar as três políticas, está pronto para criar a aplicação.</span><span class="sxs-lookup"><span data-stu-id="e667d-147">After you have created your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="e667d-148">Para saber mais sobre como funcionam as políticas no Azure AD B2C, comece com o [Tutorial de introdução da aplicação Web do .NET](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e667d-148">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-the-code"></a><span data-ttu-id="e667d-149">Transferir o código</span><span class="sxs-lookup"><span data-stu-id="e667d-149">Download the code</span></span>
<span data-ttu-id="e667d-150">O código deste tutorial [é mantido no GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="e667d-150">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="e667d-151">Para criar o exemplo à medida que avança, pode [transferir o projeto de estrutura como um ficheiro .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="e667d-151">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="e667d-152">Também pode clonar a estrutura:</span><span class="sxs-lookup"><span data-stu-id="e667d-152">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="e667d-153">A aplicação concluída está também [disponível como um ficheiro .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) ou no ramo `complete` do mesmo repositório.</span><span class="sxs-lookup"><span data-stu-id="e667d-153">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="e667d-154">Transferir Node.js para a plataforma</span><span class="sxs-lookup"><span data-stu-id="e667d-154">Download Node.js for your platform</span></span>
<span data-ttu-id="e667d-155">Para utilizar este exemplo com êxito, tem de ter uma instalação do Node.js em execução.</span><span class="sxs-lookup"><span data-stu-id="e667d-155">To successfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="e667d-156">Instalar Node.js de [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="e667d-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="e667d-157">Instalar MongoDB para a plataforma</span><span class="sxs-lookup"><span data-stu-id="e667d-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="e667d-158">Para utilizar este exemplo com êxito, tem de ter uma instalação do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e667d-158">To successfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="e667d-159">Utilizamos o MongoDB para tornar a API REST persistente em várias instâncias de servidor.</span><span class="sxs-lookup"><span data-stu-id="e667d-159">We use MongoDB to make your REST API persistent across server instances.</span></span>

<span data-ttu-id="e667d-160">Instalar MongoDB de [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="e667d-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="e667d-161">Esta passagem parte do princípio de que irá utilizar os pontos finais do servidor e a instalação predefinida para o MongoDB, que de momento é `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="e667d-161">This walk-through assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="e667d-162">Instalar os módulos Restify na API Web</span><span class="sxs-lookup"><span data-stu-id="e667d-162">Install the Restify modules in your web API</span></span>
<span data-ttu-id="e667d-163">Utilizamos o Restify para criar a API REST.</span><span class="sxs-lookup"><span data-stu-id="e667d-163">We use Restify to build your REST API.</span></span> <span data-ttu-id="e667d-164">O Restify é uma estrutura de aplicação Node.js mínima e flexível derivada do Express.</span><span class="sxs-lookup"><span data-stu-id="e667d-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="e667d-165">Tem um conjunto robusto de funcionalidades para a criação de APIs REST por cima do Connect.</span><span class="sxs-lookup"><span data-stu-id="e667d-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="e667d-166">Instalação do Restify</span><span class="sxs-lookup"><span data-stu-id="e667d-166">Install Restify</span></span>
<span data-ttu-id="e667d-167">Na linha de comandos, altere o diretório para `azuread`.</span><span class="sxs-lookup"><span data-stu-id="e667d-167">From the command line, change your directory to `azuread`.</span></span> <span data-ttu-id="e667d-168">Se o diretório `azuread` não existe, crie-o.</span><span class="sxs-lookup"><span data-stu-id="e667d-168">If the `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="e667d-169">`cd azuread` ou `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="e667d-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="e667d-170">Introduza o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="e667d-170">Enter the following command:</span></span>

`npm install restify`

<span data-ttu-id="e667d-171">Este comando instala o Restify.</span><span class="sxs-lookup"><span data-stu-id="e667d-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="e667d-172">Obteve um erro?</span><span class="sxs-lookup"><span data-stu-id="e667d-172">Did you get an error?</span></span>
<span data-ttu-id="e667d-173">Em alguns sistemas operativos, quando utiliza `npm`, poderá receber o erro `Error: EPERM, chmod '/usr/local/bin/..'` e um pedido para que execute a conta como administrador.</span><span class="sxs-lookup"><span data-stu-id="e667d-173">In some operating systems, when you use `npm`, you may receive the error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run the account as an administrator.</span></span> <span data-ttu-id="e667d-174">Se este problema ocorrer, utilize o comando `sudo` para executar `npm` a um nível de privilégio mais elevado.</span><span class="sxs-lookup"><span data-stu-id="e667d-174">If this problem occurs, use the `sudo` command to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="e667d-175">Obteve um erro de DTrace?</span><span class="sxs-lookup"><span data-stu-id="e667d-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="e667d-176">Quando instalar o Restify, pode aparecer o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="e667d-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="e667d-177">O Restify fornece um mecanismo poderoso para rastreio de chamadas REST utilizando o DTrace.</span><span class="sxs-lookup"><span data-stu-id="e667d-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="e667d-178">No entanto, muitos sistemas operativos não tem o DTrace disponível.</span><span class="sxs-lookup"><span data-stu-id="e667d-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="e667d-179">Pode ignorar com segurança estes erros.</span><span class="sxs-lookup"><span data-stu-id="e667d-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="e667d-180">O resultado do comando deve ter um aspeto semelhante ao que se segue:</span><span class="sxs-lookup"><span data-stu-id="e667d-180">The output of the command should appear similar to this text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="e667d-181">Instalar o Passport na API Web</span><span class="sxs-lookup"><span data-stu-id="e667d-181">Install Passport in your web API</span></span>
<span data-ttu-id="e667d-182">Na linha de comandos, altere o diretório para `azuread`, caso ainda não esteja aí.</span><span class="sxs-lookup"><span data-stu-id="e667d-182">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="e667d-183">Introduza o comando seguinte para instalar o Passport:</span><span class="sxs-lookup"><span data-stu-id="e667d-183">Install Passport using the following command:</span></span>

`npm install passport`

<span data-ttu-id="e667d-184">O resultado do comando deve ser semelhante ao texto que se segue:</span><span class="sxs-lookup"><span data-stu-id="e667d-184">The output of the command should be similar to this text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-to-your-web-api"></a><span data-ttu-id="e667d-185">Adicionar passport-azuread à API Web </span><span class="sxs-lookup"><span data-stu-id="e667d-185">Add passport-azuread to your web API</span></span>
<span data-ttu-id="e667d-186">Em seguida, adicione a estratégia de OAuth utilizando `passport-azuread`, um conjunto de estratégias que ligam o Azure AD com o Passport.</span><span class="sxs-lookup"><span data-stu-id="e667d-186">Next, add the OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="e667d-187">Utilize esta estratégia para os tokens de portador no exemplo API REST.</span><span class="sxs-lookup"><span data-stu-id="e667d-187">Use this strategy for bearer tokens in the REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="e667d-188">Embora o OAuth2 forneça uma estrutura onde pode ser emitido qualquer tipo de token conhecido, apenas alguns tipos de tokens passaram a ser amplamente utilizados.</span><span class="sxs-lookup"><span data-stu-id="e667d-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="e667d-189">Os tokens para proteger os pontos finais são tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="e667d-189">The tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="e667d-190">Estes tipos de tokens são os mais emitidos no OAuth2.</span><span class="sxs-lookup"><span data-stu-id="e667d-190">These types of tokens are the most widely issued in OAuth2.</span></span> <span data-ttu-id="e667d-191">Várias implementações partem do princípio de que os tokens de portador são o único tipo de token emitido.</span><span class="sxs-lookup"><span data-stu-id="e667d-191">Many implementations assume that bearer tokens are the only type of token issued.</span></span>
>
>

<span data-ttu-id="e667d-192">Na linha de comandos, altere o diretório para `azuread`, caso ainda não esteja aí.</span><span class="sxs-lookup"><span data-stu-id="e667d-192">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="e667d-193">Introduza o comando seguinte para instalar o módulo `passport-azure-ad` do Passport:</span><span class="sxs-lookup"><span data-stu-id="e667d-193">Install the Passport `passport-azure-ad` module using the following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="e667d-194">O resultado do comando deve ser semelhante ao texto que se segue:</span><span class="sxs-lookup"><span data-stu-id="e667d-194">The output of the command should be similar to this text:</span></span>

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

## <a name="add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="e667d-195">Adicione módulos do MongoDB à API Web</span><span class="sxs-lookup"><span data-stu-id="e667d-195">Add MongoDB modules to your web API</span></span>
<span data-ttu-id="e667d-196">Este exemplo utiliza o MongoDB como arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="e667d-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="e667d-197">Para tal, instale o Mongoose, um plug-in de gestão de modelos e esquemas muito utilizado.</span><span class="sxs-lookup"><span data-stu-id="e667d-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="e667d-198">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="e667d-198">Install additional modules</span></span>
<span data-ttu-id="e667d-199">Em seguida, instale os restantes módulos necessários.</span><span class="sxs-lookup"><span data-stu-id="e667d-199">Next, install the remaining required modules.</span></span>

<span data-ttu-id="e667d-200">Na linha de comandos, altere o diretório para `azuread`, caso ainda não esteja aí:</span><span class="sxs-lookup"><span data-stu-id="e667d-200">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e667d-201">Instale os módulos no diretório `node_modules`:</span><span class="sxs-lookup"><span data-stu-id="e667d-201">Install the modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="e667d-202">Crie um ficheiro de server.js com as suas dependências</span><span class="sxs-lookup"><span data-stu-id="e667d-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="e667d-203">O ficheiro `server.js` proporciona a maior parte das funcionalidades do seu servidor de API Web.</span><span class="sxs-lookup"><span data-stu-id="e667d-203">The `server.js` file provides the majority of the functionality for your Web API server.</span></span>

<span data-ttu-id="e667d-204">Na linha de comandos, altere o diretório para `azuread`, caso ainda não esteja aí:</span><span class="sxs-lookup"><span data-stu-id="e667d-204">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e667d-205">Crie um ficheiro `server.js` num editor.</span><span class="sxs-lookup"><span data-stu-id="e667d-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="e667d-206">Adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="e667d-206">Add the following information:</span></span>

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

<span data-ttu-id="e667d-207">Guarde o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e667d-207">Save the file.</span></span> <span data-ttu-id="e667d-208">Regressará a este mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e667d-208">You return to it later.</span></span>

## <a name="create-a-configjs-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="e667d-209">Criar um ficheiro de config.js para armazenar as suas definições do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e667d-209">Create a config.js file to store your Azure AD settings</span></span>
<span data-ttu-id="e667d-210">Este ficheiro de código transmite os parâmetros de configuração a partir do Portal do Azure AD para o ficheiro `Passport.js`.</span><span class="sxs-lookup"><span data-stu-id="e667d-210">This code file passes the configuration parameters from your Azure AD Portal to the `Passport.js` file.</span></span> <span data-ttu-id="e667d-211">Criou estes valores de configuração quando adicionou a API Web ao portal na primeira parte da passagem.</span><span class="sxs-lookup"><span data-stu-id="e667d-211">You created these configuration values when you added the web API to the portal in the first part of the walk-through.</span></span> <span data-ttu-id="e667d-212">Vamos explicar o que deve introduzir nos valores destes parâmetros depois de copiar o código.</span><span class="sxs-lookup"><span data-stu-id="e667d-212">We explain what to put in the values of these parameters after you copy the code.</span></span>

<span data-ttu-id="e667d-213">Na linha de comandos, altere o diretório para `azuread`, caso ainda não esteja aí:</span><span class="sxs-lookup"><span data-stu-id="e667d-213">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e667d-214">Crie um ficheiro `config.js` num editor.</span><span class="sxs-lookup"><span data-stu-id="e667d-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="e667d-215">Adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="e667d-215">Add the following information:</span></span>

```Javascript
// Don't commit this file to your public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in the portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // the Client ID of the application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add the B2C tenant name in the <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is the policy you'll want to validate against in B2C. Usually this is your Sign-in policy (as users sign in to this API)
passReqToCallback: false // This is a node.js construct that lets you pass the req all the way back to any upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="e667d-216">Valores necessários</span><span class="sxs-lookup"><span data-stu-id="e667d-216">Required values</span></span>
<span data-ttu-id="e667d-217">`clientID`: o ID de cliente da aplicação API Web.</span><span class="sxs-lookup"><span data-stu-id="e667d-217">`clientID`: The client ID of your Web API application.</span></span>

<span data-ttu-id="e667d-218">`IdentityMetadata`: este é o local onde o `passport-azure-ad` vai procurar os seus dados de configuração para o fornecedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="e667d-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for the identity provider.</span></span> <span data-ttu-id="e667d-219">Também vai procurar aqui as chaves para validar os tokens Web JSON.</span><span class="sxs-lookup"><span data-stu-id="e667d-219">It also looks for the keys to validate the JSON web tokens.</span></span>

<span data-ttu-id="e667d-220">`audience`: o URI (Uniform Resource Identifier) do portal que identifica a sua aplicação de chamada.</span><span class="sxs-lookup"><span data-stu-id="e667d-220">`audience`: The uniform resource identifier (URI) from the portal that identifies your calling application.</span></span>

<span data-ttu-id="e667d-221">`tenantName`: o nome do seu inquilino (por exemplo, **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="e667d-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="e667d-222">`policyName`: a política que pretende que valide os tokens recebidos pelo seu servidor.</span><span class="sxs-lookup"><span data-stu-id="e667d-222">`policyName`: The policy that you want to validate the tokens coming in to your server.</span></span> <span data-ttu-id="e667d-223">Esta política deve ser igual à utilizada na aplicação cliente para iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="e667d-223">This policy should be the same policy that you use on the client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="e667d-224">Por agora, utilize as mesmas políticas para configurar o cliente e o servidor.</span><span class="sxs-lookup"><span data-stu-id="e667d-224">For now, use the same policies across both client and server setup.</span></span> <span data-ttu-id="e667d-225">Se já tiver concluído uma passagem e criado estas políticas, não terá de fazê-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="e667d-225">If you have already completed a walk-through and created these policies, you don't need to do so again.</span></span> <span data-ttu-id="e667d-226">Uma vez concluída a passagem, não deverá ser necessário configurar novas políticas para passagens de cliente no site.</span><span class="sxs-lookup"><span data-stu-id="e667d-226">Because you completed the walk-through, you shouldn't need to set up new policies for client walk-throughs on the site.</span></span>
>
>

## <a name="add-configuration-to-your-serverjs-file"></a><span data-ttu-id="e667d-227">Adicionar configuração ao seu ficheiro server.js</span><span class="sxs-lookup"><span data-stu-id="e667d-227">Add configuration to your server.js file</span></span>
<span data-ttu-id="e667d-228">Para ler os valores do ficheiro `config.js` que criou, adicione o ficheiro `.config` como recurso pretendido na sua aplicação e, em seguida, defina as variáveis globais para as existentes no documento `config.js`.</span><span class="sxs-lookup"><span data-stu-id="e667d-228">To read the values from the `config.js` file you created, add the `.config` file as a required resource in your application, and then set the global variables to those in the `config.js` document.</span></span>

<span data-ttu-id="e667d-229">Na linha de comandos, altere o diretório para `azuread`, caso ainda não esteja aí:</span><span class="sxs-lookup"><span data-stu-id="e667d-229">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e667d-230">Crie o ficheiro `server.js` num editor.</span><span class="sxs-lookup"><span data-stu-id="e667d-230">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="e667d-231">Adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="e667d-231">Add the following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="e667d-232">Adicione uma nova secção a `server.js` que inclua o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="e667d-232">Add a new section to `server.js` that includes the following code:</span></span>

```Javascript
// We pass these options in to the ODICBearerStrategy.

var options = {
    // The URL of the metadata document for your app. We put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="e667d-233">Em seguida, vamos adicionar alguns marcadores de posição para os utilizadores que recebemos a partir das nossas aplicações de chamada.</span><span class="sxs-lookup"><span data-stu-id="e667d-233">Next, let's add some placeholders for the users we receive from our calling applications.</span></span>

```Javascript
// array to hold logged in users and the current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="e667d-234">Vamos avançar e criar também o nosso registo.</span><span class="sxs-lookup"><span data-stu-id="e667d-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="e667d-235">Adicionar as informações de esquema e modelo MongoDB utilizando o Mongoose</span><span class="sxs-lookup"><span data-stu-id="e667d-235">Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="e667d-236">A preparação prévia funciona se juntar estes três ficheiros num serviço API REST.</span><span class="sxs-lookup"><span data-stu-id="e667d-236">The earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="e667d-237">Para esta passagem, utilize o MongoDB para armazenar as suas tarefas, como mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e667d-237">For this walk-through, use MongoDB to store your tasks, as discussed earlier.</span></span>

<span data-ttu-id="e667d-238">No ficheiro `config.js`, atribuiu o nome **tasklist** à base de dados.</span><span class="sxs-lookup"><span data-stu-id="e667d-238">In the `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="e667d-239">Esse nome foi também o que colocou no final da URL da ligação `mongoose_auth_local`.</span><span class="sxs-lookup"><span data-stu-id="e667d-239">That name was also what you put at the end of the `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="e667d-240">Não precisa de criar esta base de dados previamente no MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e667d-240">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="e667d-241">Cria a base de dados para si na primeira execução da sua aplicação de servidor.</span><span class="sxs-lookup"><span data-stu-id="e667d-241">It creates the database for you on the first run of your server application.</span></span>

<span data-ttu-id="e667d-242">Depois de indicar ao servidor qual a base de dados de MongoDB a utilizar, precisa de escrever alguns códigos adicionais para criar o modelo e o esquema das suas tarefas de servidor.</span><span class="sxs-lookup"><span data-stu-id="e667d-242">After you tell the server which MongoDB database to use, you need to write some additional code to create the model and schema for your server tasks.</span></span>

### <a name="expand-the-model"></a><span data-ttu-id="e667d-243">Expandir o modelo</span><span class="sxs-lookup"><span data-stu-id="e667d-243">Expand the model</span></span>
<span data-ttu-id="e667d-244">Este modelo de esquema é simples.</span><span class="sxs-lookup"><span data-stu-id="e667d-244">This schema model is simple.</span></span> <span data-ttu-id="e667d-245">Pode expandi-lo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="e667d-245">You can expand it as required.</span></span>

<span data-ttu-id="e667d-246">`owner`: quem é atribuído à tarefa.</span><span class="sxs-lookup"><span data-stu-id="e667d-246">`owner`: Who is assigned to the task.</span></span> <span data-ttu-id="e667d-247">Este objeto é uma **cadeia**.</span><span class="sxs-lookup"><span data-stu-id="e667d-247">This object is a **string**.</span></span>  

<span data-ttu-id="e667d-248">`Text`: a tarefa propriamente dita.</span><span class="sxs-lookup"><span data-stu-id="e667d-248">`Text`: The task itself.</span></span> <span data-ttu-id="e667d-249">Este objeto é uma **cadeia**.</span><span class="sxs-lookup"><span data-stu-id="e667d-249">This object is a **string**.</span></span>

<span data-ttu-id="e667d-250">`date`: a data em que a tarefa deve ser concluída.</span><span class="sxs-lookup"><span data-stu-id="e667d-250">`date`: The date that the task is due.</span></span> <span data-ttu-id="e667d-251">Este objeto é uma **datetime**.</span><span class="sxs-lookup"><span data-stu-id="e667d-251">This object is a **datetime**.</span></span>

<span data-ttu-id="e667d-252">`completed`: se a tarefa está concluída.</span><span class="sxs-lookup"><span data-stu-id="e667d-252">`completed`: If the task is complete.</span></span> <span data-ttu-id="e667d-253">Este objeto é um **Booleano**.</span><span class="sxs-lookup"><span data-stu-id="e667d-253">This object is a **Boolean**.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="e667d-254">Criar o esquema no código</span><span class="sxs-lookup"><span data-stu-id="e667d-254">Create the schema in the code</span></span>
<span data-ttu-id="e667d-255">Na linha de comandos, altere o diretório para `azuread`, caso ainda não esteja aí:</span><span class="sxs-lookup"><span data-stu-id="e667d-255">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e667d-256">Crie o ficheiro `server.js` num editor.</span><span class="sxs-lookup"><span data-stu-id="e667d-256">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="e667d-257">Adicione a informação seguinte abaixo da entrada de configuração:</span><span class="sxs-lookup"><span data-stu-id="e667d-257">Add the following information below the configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect to MongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema to store our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use the schema to register a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="e667d-258">Crie primeiro o esquema e, em seguida, crie um objeto de modelo que utilizará para armazenar os dados em todo o código, quando definir as suas **rotas**.</span><span class="sxs-lookup"><span data-stu-id="e667d-258">You first create the schema, and then you create a model object that you use to store your data throughout the code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="e667d-259">Adicionar rotas ao seu servidor de tarefas da API REST</span><span class="sxs-lookup"><span data-stu-id="e667d-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="e667d-260">Agora que tem um modelo de base de dados com o qual trabalhar, adicione as rotas que vai utilizar com o servidor da API REST.</span><span class="sxs-lookup"><span data-stu-id="e667d-260">Now that you have a database model to work with, add the routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="e667d-261">Sobre rotas no Restify</span><span class="sxs-lookup"><span data-stu-id="e667d-261">About routes in Restify</span></span>
<span data-ttu-id="e667d-262">As rotas funcionam no Restify da mesma maneira que funcionam quando utilizam a pilha Express.</span><span class="sxs-lookup"><span data-stu-id="e667d-262">Routes work in Restify in the same way that they work when they use the Express stack.</span></span> <span data-ttu-id="e667d-263">Definem-se rotas utilizando o URI que se espera que as aplicações de cliente chamem.</span><span class="sxs-lookup"><span data-stu-id="e667d-263">You define routes by using the URI that you expect the client applications to call.</span></span>

<span data-ttu-id="e667d-264">Um padrão normal para uma rota do Restify é:</span><span class="sxs-lookup"><span data-stu-id="e667d-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep the server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="e667d-265">O Restify e o Express podem fornecer funcionalidades muito mais aprofundada, tais como, definir tipos de aplicações e efetuar encaminhamentos complexos para diferentes pontos finais.</span><span class="sxs-lookup"><span data-stu-id="e667d-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="e667d-266">Para este tutorial, mantemos estas rotas simples.</span><span class="sxs-lookup"><span data-stu-id="e667d-266">For the purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="e667d-267">Adicionar rotas predefinidas ao seu servidor</span><span class="sxs-lookup"><span data-stu-id="e667d-267">Add default routes to your server</span></span>
<span data-ttu-id="e667d-268">Em seguida, adicione as rotas CRUD básicas de **criar** e **listar** para a nossa API REST.</span><span class="sxs-lookup"><span data-stu-id="e667d-268">You now add the basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="e667d-269">Outras rotas estão disponíveis no ramo `complete` do exemplo.</span><span class="sxs-lookup"><span data-stu-id="e667d-269">Other routes can be found in the `complete` branch of the sample.</span></span>

<span data-ttu-id="e667d-270">Na linha de comandos, altere o diretório para `azuread`, caso ainda não esteja aí:</span><span class="sxs-lookup"><span data-stu-id="e667d-270">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e667d-271">Crie o ficheiro `server.js` num editor.</span><span class="sxs-lookup"><span data-stu-id="e667d-271">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="e667d-272">Adicione as informações seguintes abaixo das entradas da base de dados que criou acima:</span><span class="sxs-lookup"><span data-stu-id="e667d-272">Below the database entries you made above add the following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it to Mongodb
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
            req.log.warn(err, 'createTask: unable to save');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

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
            log.warn(err, "There is no tasks in the database. Add one!");
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


#### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="e667d-273">Adicionar tratamento de erro para as rotas</span><span class="sxs-lookup"><span data-stu-id="e667d-273">Add error handling for the routes</span></span>
<span data-ttu-id="e667d-274">Adicione tratamento de erros para que possa comunicar quaisquer problemas que encontre de forma a que o cliente possa compreender.</span><span class="sxs-lookup"><span data-stu-id="e667d-274">Add some error handling so that you can communicate any problems you encounter back to the client in a way that it can understand.</span></span>

<span data-ttu-id="e667d-275">Adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="e667d-275">Add the following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back to the client
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


## <a name="create-your-server"></a><span data-ttu-id="e667d-276">Criar o seu servidor</span><span class="sxs-lookup"><span data-stu-id="e667d-276">Create your server</span></span>
<span data-ttu-id="e667d-277">Agora definiu a base de dados e colocou as rotas.</span><span class="sxs-lookup"><span data-stu-id="e667d-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="e667d-278">A última coisa que tem de fazer consiste em adicionar a instância de servidor que gere as suas chamadas.</span><span class="sxs-lookup"><span data-stu-id="e667d-278">The last thing for you to do is to add the server instance that manages your calls.</span></span>

<span data-ttu-id="e667d-279">O Restify e o Express fornecem personalização avançada para um servidor de API REST, mas nós utilizamos a configuração mais básica.</span><span class="sxs-lookup"><span data-stu-id="e667d-279">Restify and Express provide deep customization for a REST API server, but we use the most basic setup here.</span></span>

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

// Allow 5 requests/second by IP, and burst to 10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping to REST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-the-routes-to-the-server-without-authentication"></a><span data-ttu-id="e667d-280">Adicionar as rotas ao servidor (sem autenticação)</span><span class="sxs-lookup"><span data-stu-id="e667d-280">Add the routes to the server (without authentication)</span></span>
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
    consoleMessage += '\n Open your browser to %s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-to-your-rest-api-server"></a><span data-ttu-id="e667d-281">Adicionar autenticação ao seu servidor de API REST</span><span class="sxs-lookup"><span data-stu-id="e667d-281">Add authentication to your REST API server</span></span>
<span data-ttu-id="e667d-282">Agora que um servidor de API REST está em execução, pode torná-lo útil em relação ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e667d-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="e667d-283">Na linha de comandos, altere o diretório para `azuread`, caso ainda não esteja aí:</span><span class="sxs-lookup"><span data-stu-id="e667d-283">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="e667d-284">Utilize o OIDCBearerStrategy que está incluído no passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="e667d-284">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="e667d-285">Quando escreve APIs, deve ligar sempre os dados a algo especial do token que o utilizador não pode falsificar.</span><span class="sxs-lookup"><span data-stu-id="e667d-285">When you write APIs, you should always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="e667d-286">Quando o servidor armazena itens ToDo, fá-lo com base no **oid** do utilizador no token (chamado de token.oid) que é incluído no campo “proprietário”.</span><span class="sxs-lookup"><span data-stu-id="e667d-286">When the server stores ToDo items, it does so based on the **oid** of the user in the token (called through token.oid), which goes in the “owner” field.</span></span> <span data-ttu-id="e667d-287">Este valor garante que apenas esse utilizador pode aceder aos próprios itens ToDo.</span><span class="sxs-lookup"><span data-stu-id="e667d-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="e667d-288">Não existe nenhuma exposição na API de “proprietário”, de modo que um utilizador externo pode pedir itens ToDo de outras pessoas, mesmo que estejam autenticados.</span><span class="sxs-lookup"><span data-stu-id="e667d-288">There is no exposure in the API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="e667d-289">Em seguida, utilize a estratégia de portador que vem com `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="e667d-289">Next, use the bearer strategy that comes with `passport-azure-ad`.</span></span>

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
        log.info('verifying the user');
        log.info(token, 'was the token retreived');
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

<span data-ttu-id="e667d-290">O Passport utiliza o mesmo padrão para todas as respetivas estratégias.</span><span class="sxs-lookup"><span data-stu-id="e667d-290">Passport uses the same pattern for all its strategies.</span></span> <span data-ttu-id="e667d-291">Passe-o como uma `function()` que tem `token` e `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e667d-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="e667d-292">A estratégia é-lhe devolvida depois de fazer todo o trabalho.</span><span class="sxs-lookup"><span data-stu-id="e667d-292">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="e667d-293">Em seguida, deve armazenar o utilizador e guardar o token para que não seja necessário voltar a pedi-lo.</span><span class="sxs-lookup"><span data-stu-id="e667d-293">You should then store the user and save the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e667d-294">O código acima aceita qualquer utilizador que se autentique com o seu servidor.</span><span class="sxs-lookup"><span data-stu-id="e667d-294">The code above takes any user who happens to authenticate to your server.</span></span> <span data-ttu-id="e667d-295">Este processo é conhecido como registo automático.</span><span class="sxs-lookup"><span data-stu-id="e667d-295">This process is known as autoregistration.</span></span> <span data-ttu-id="e667d-296">Em servidores de produção, não permita que quaisquer utilizadores acedam à API sem passarem primeiro por um processo de registo.</span><span class="sxs-lookup"><span data-stu-id="e667d-296">In production servers, don't let in any users access the API without first having them go through a registration process.</span></span> <span data-ttu-id="e667d-297">Este processo é normalmente o padrão normal que vê nas aplicações de consumidor que lhe permitem fazer o registo através do Facebook, mas que em seguida lhe pedem para preencher informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="e667d-297">This process is usually the pattern you see in consumer apps that allow you to register by using Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="e667d-298">Se este programa não fosse um programa de linha de comandos, poderíamos extrair o e-mail do objeto do token que é devolvido e, em seguida, pedir aos utilizadores para preencher informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="e667d-298">If this program wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked users to fill out additional information.</span></span> <span data-ttu-id="e667d-299">Uma vez que este é um exemplo, vamos adicioná-los a uma base de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="e667d-299">Because this is a sample, we add them to an in-memory database.</span></span>
>
>

## <a name="run-your-server-application-to-verify-that-it-rejects-you"></a><span data-ttu-id="e667d-300">Execute a aplicação de servidor para verificar se esta o rejeita</span><span class="sxs-lookup"><span data-stu-id="e667d-300">Run your server application to verify that it rejects you</span></span>
<span data-ttu-id="e667d-301">Pode utilizar `curl` para ver se tem agora proteção do OAuth2 em relação aos pontos finais.</span><span class="sxs-lookup"><span data-stu-id="e667d-301">You can use `curl` to see if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="e667d-302">Os cabeçalhos devolvidos devem ser suficientes para lhe indicar que está no caminho certo.</span><span class="sxs-lookup"><span data-stu-id="e667d-302">The headers returned should be enough to tell you that you are on the right path.</span></span>

<span data-ttu-id="e667d-303">Certifique-se de que a instância do MongoDB está em execução:</span><span class="sxs-lookup"><span data-stu-id="e667d-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="e667d-304">Mude para o diretório e execute o servidor:</span><span class="sxs-lookup"><span data-stu-id="e667d-304">Change to the directory and run the server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="e667d-305">Numa nova janela de terminal, execute `curl`</span><span class="sxs-lookup"><span data-stu-id="e667d-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="e667d-306">Tente um POST básico:</span><span class="sxs-lookup"><span data-stu-id="e667d-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="e667d-307">A resposta pretendida é um erro 401.</span><span class="sxs-lookup"><span data-stu-id="e667d-307">A 401 error is the response you want.</span></span> <span data-ttu-id="e667d-308">Indica que a camada do Passport está a tentar redirecionar para o ponto final de autorização.</span><span class="sxs-lookup"><span data-stu-id="e667d-308">It indicates that the Passport layer is trying to redirect to the authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="e667d-309">Agora tem um serviço de API REST que utiliza o OAuth2</span><span class="sxs-lookup"><span data-stu-id="e667d-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="e667d-310">Tem implementada uma API REST utilizando o Restify e o OAuth!</span><span class="sxs-lookup"><span data-stu-id="e667d-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="e667d-311">Tem agora código suficiente para que possa continuar a desenvolver o seu serviço e compilação neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="e667d-311">You now have sufficient code so that you can continue to develop your service and build on this example.</span></span> <span data-ttu-id="e667d-312">Fez tudo o que podia com este servidor sem utilizar um cliente compatível com o OAuth2.</span><span class="sxs-lookup"><span data-stu-id="e667d-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="e667d-313">Para esse passo seguinte, utilize uma passagem walk-through adicional como a nossa passagem [Ligar a uma API web utilizando iOS com B2C](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="e667d-313">For that next step use an additional walk-through like our [Connect to a web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e667d-314">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="e667d-314">Next steps</span></span>
<span data-ttu-id="e667d-315">Agora pode aceder a tópicos mais avançados, como:</span><span class="sxs-lookup"><span data-stu-id="e667d-315">You can now move to more advanced topics, such as:</span></span>

[<span data-ttu-id="e667d-316">Ligar a uma API Web utilizando o iOS com o B2C</span><span class="sxs-lookup"><span data-stu-id="e667d-316">Connect to a web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
