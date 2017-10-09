---
title: "aaaAzure AD AngularJS introdução | Microsoft Docs"
description: "Como toobuild uma aplicação de página única AngularJS que se integra com o Azure AD para início de sessão e chama APIs do Azure AD protegida utilizando OAuth."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="ce025-103">Ajudar a proteger as aplicações de página única AngularJS por utilizar o Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce025-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ce025-104">Azure Active Directory (Azure AD) torna simples e fácil para tooadd início de sessão, fim de sessão, e segura OAuth API chama tooyour aplicações de página única.</span><span class="sxs-lookup"><span data-stu-id="ce025-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="ce025-105">Isto permite que os utilizadores de tooauthenticate aplicações com as respetivas contas do Windows Server Active Directory e consumir quaisquer web API do Azure AD ajuda a proteger, tais como Olá APIs do Office 365 ou Olá API do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce025-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="ce025-106">Para aplicações de JavaScript em execução num browser, o Azure AD fornece Olá Active Directory Authentication Library (ADAL) ou adal.js.</span><span class="sxs-lookup"><span data-stu-id="ce025-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="ce025-107">Olá único objetivo adal.js é toomake-lo mais fácil para os tokens de acesso de tooget de aplicação.</span><span class="sxs-lookup"><span data-stu-id="ce025-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="ce025-108">é, tal como fácil toodemonstrate aqui irá criar uma aplicação de lista de tooDo AngularJS que:</span><span class="sxs-lookup"><span data-stu-id="ce025-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="ce025-109">Sinais Olá utilizador na aplicação toohello através da utilização do Azure AD como fornecedor de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="ce025-110">Mostra algumas informações sobre o utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="ce025-111">Em segurança chamadas Olá tooDo da aplicação API da lista, utilizando os tokens de portador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce025-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="ce025-112">Sinais Olá utilizador fora da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="ce025-113">toobuild Olá concluída, aplicação de trabalho, tem de:</span><span class="sxs-lookup"><span data-stu-id="ce025-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="ce025-114">Registe a sua aplicação com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce025-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="ce025-115">Instale o ADAL e configure a aplicação de página única Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="ce025-116">Utilize páginas segura ADAL toohelp na aplicação de página única Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="ce025-117">tooget iniciado, [transferir a estrutura de aplicação Olá](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) ou [transferir exemplo Olá concluída](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ce025-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="ce025-118">Também precisa de um inquilino do Azure AD, onde pode criar utilizadores e registar uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="ce025-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="ce025-119">Se ainda não tiver um inquilino, [Saiba como tooget um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ce025-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="ce025-120">Passo 1: Registar a aplicação de DirectorySearcher Olá</span><span class="sxs-lookup"><span data-stu-id="ce025-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="ce025-121">tooenable dos seus utilizadores tooauthenticate de aplicação e obter tokens, primeiro tem de inquilino do tooregistê-lo no seu Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ce025-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="ce025-122">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ce025-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ce025-123">Se tem sessão iniciada toomultiple diretórios, poderá ser necessário tooensure está a visualizar correta do diretório Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="ce025-124">toodo por isso, na barra superior Olá, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="ce025-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="ce025-125">Em Olá **diretório** lista, escolha inquilino Olá do Azure AD, onde pretende tooregister a aplicação.</span><span class="sxs-lookup"><span data-stu-id="ce025-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="ce025-126">Clique em **mais serviços** no Olá painel esquerdo e, em seguida, selecione **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce025-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ce025-127">Clique em **registos de aplicação**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ce025-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="ce025-128">Siga as instruções de Olá e crie uma nova aplicação web e/ou web API:</span><span class="sxs-lookup"><span data-stu-id="ce025-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="ce025-129">**Nome** descreve toousers sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="ce025-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="ce025-130">**Uri de redirecionamento** é Olá toowhich de localização do Azure AD irá devolver tokens.</span><span class="sxs-lookup"><span data-stu-id="ce025-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="ce025-131">Olá a localização predefinida para este exemplo é `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="ce025-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="ce025-132">Depois de concluir o registo, o Azure AD atribui uma aplicação de tooyour de ID de aplicação único.</span><span class="sxs-lookup"><span data-stu-id="ce025-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="ce025-133">Irá precisar deste valor nas secções seguintes Olá, por isso, copiá-lo a partir do separador de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="ce025-134">Adal.js utiliza toocommunicate de fluxo implícito de OAuth Olá com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce025-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="ce025-135">Tem de ativar o fluxo implícito Olá para a sua aplicação:</span><span class="sxs-lookup"><span data-stu-id="ce025-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="ce025-136">Clique em aplicação Olá e selecione **manifesto** editor de manifesto tooopen Olá inline.</span><span class="sxs-lookup"><span data-stu-id="ce025-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="ce025-137">Localizar Olá `oauth2AllowImplicitFlow` propriedade.</span><span class="sxs-lookup"><span data-stu-id="ce025-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="ce025-138">Defina o respetivo valor demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="ce025-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="ce025-139">Clique em **guardar** manifesto de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="ce025-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="ce025-140">Conceder permissões em seu inquilino para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="ce025-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="ce025-141">Aceda demasiado**definições** > **propriedades** > **permissões obrigatórias**e clique em Olá **conceder permissões**botão na barra superior Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="ce025-142">Clique em **Sim** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="ce025-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="ce025-143">Passo 2: Instalar ADAL e configure a aplicação de página única Olá</span><span class="sxs-lookup"><span data-stu-id="ce025-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="ce025-144">Agora que tem uma aplicação no Azure AD, pode instalar adal.js e escrever o seu código relacionadas com identidade.</span><span class="sxs-lookup"><span data-stu-id="ce025-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="ce025-145">Configurar o cliente de JavaScript Olá</span><span class="sxs-lookup"><span data-stu-id="ce025-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="ce025-146">Comece por adicionar adal.js toohello TodoSPA projeto utilizando Olá consola do Gestor de pacotes:</span><span class="sxs-lookup"><span data-stu-id="ce025-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="ce025-147">Transferir [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) e adicioná-la toohello `App/Scripts/` diretório de projeto.</span><span class="sxs-lookup"><span data-stu-id="ce025-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="ce025-148">Transferir [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) e adicioná-la toohello `App/Scripts/` diretório de projeto.</span><span class="sxs-lookup"><span data-stu-id="ce025-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="ce025-149">Carregar cada script antes de fim de Olá do Olá `</body>` no `index.html`:</span><span class="sxs-lookup"><span data-stu-id="ce025-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="ce025-150">Configurar o servidor de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="ce025-150">Configure hello back end server</span></span>
<span data-ttu-id="ce025-151">Para tooDo de back-end lista API tooaccept tokens da aplicação de página única Olá a partir do browser Olá, o back-end Olá tem informações de configuração sobre o registo de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="ce025-152">No projeto de TodoSPA Olá, abra `web.config`.</span><span class="sxs-lookup"><span data-stu-id="ce025-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="ce025-153">Substitua os valores de Olá de elementos Olá Olá `<appSettings>` Olá de secção tooreflect Olá valores que utilizou no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce025-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="ce025-154">O código será referenciar estes valores, sempre que utilizar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="ce025-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="ce025-155">`ida:Tenant`é Olá domínio de inquilino do Azure AD – por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="ce025-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="ce025-156">`ida:Audience`é o ID de cliente Olá da sua aplicação que copiou do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="ce025-157">Passo 3: Utilize ADAL toohelp seguras as páginas na aplicação de página única Olá</span><span class="sxs-lookup"><span data-stu-id="ce025-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="ce025-158">Adal.js integra AngularJS rota e fornecedores de HTTP, para que possa ajudar vistas individuais seguras na sua aplicação de página única.</span><span class="sxs-lookup"><span data-stu-id="ce025-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="ce025-159">No `App/Scripts/app.js`, coloque do módulo de adal.js Olá:</span><span class="sxs-lookup"><span data-stu-id="ce025-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="ce025-160">Inicializar `adalProvider` utilizando valores de configuração de Olá de registo da aplicação, também `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="ce025-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. <span data-ttu-id="ce025-161">Ajudar a proteger Olá `TodoList` vista na aplicação Olá utilizando apenas uma linha de código: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="ce025-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="ce025-162">Resumo</span><span class="sxs-lookup"><span data-stu-id="ce025-162">Summary</span></span>
<span data-ttu-id="ce025-163">Tem agora uma aplicação de página única segura, que pode iniciar sessão em utilizadores e emitir pedidos protegidos de token de portador tooits back-end API.</span><span class="sxs-lookup"><span data-stu-id="ce025-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="ce025-164">Quando um utilizador clica Olá **TodoList** ligação, adal.js será automaticamente redirecionado tooAzure AD para início de sessão se necessário.</span><span class="sxs-lookup"><span data-stu-id="ce025-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="ce025-165">Além disso, adal.js ligará automaticamente um acesso token tooany Ajax pedidos que são enviadas de back-end da aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="ce025-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="ce025-166">Olá passos anteriores são Olá bare mínimo necessário toobuild uma aplicação de página única com adal.js.</span><span class="sxs-lookup"><span data-stu-id="ce025-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="ce025-167">Mas algumas outras funcionalidades são úteis na aplicação de página única:</span><span class="sxs-lookup"><span data-stu-id="ce025-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="ce025-168">tooexplicitly emitir pedidos de início de sessão e fim de sessão, pode definir funções os controladores que invocam adal.js.</span><span class="sxs-lookup"><span data-stu-id="ce025-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="ce025-169">No `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="ce025-169">In `App/Scripts/homeCtrl.js`:</span></span>

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* <span data-ttu-id="ce025-170">Pode querer toopresent informações de utilizador na IU da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="ce025-171">Olá serviço ADAL já foi adicionado toohello `userDataCtrl` controlador, para que possa aceder Olá `userInfo` objeto no Olá associado à vista, `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="ce025-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="ce025-172">Existem muitos cenários em que poderá ser útil tooknow se o utilizador Olá tem sessão iniciada ou não.</span><span class="sxs-lookup"><span data-stu-id="ce025-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="ce025-173">Também pode utilizar Olá `userInfo` objeto toogather estas informações.</span><span class="sxs-lookup"><span data-stu-id="ce025-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="ce025-174">Por exemplo, no `index.html`, pode mostrar o Olá **início de sessão** ou **terminar** botão com base no estado de autenticação:</span><span class="sxs-lookup"><span data-stu-id="ce025-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="ce025-175">A aplicação de página única integrada no AD do Azure pode autenticar os utilizadores, em segurança chamar o back-end através da utilização de OAuth 2.0 e obter informações básicas sobre utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="ce025-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="ce025-176">Se ainda não o fez, agora é Olá tempo toopopulate do inquilino com alguns utilizadores.</span><span class="sxs-lookup"><span data-stu-id="ce025-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="ce025-177">Executar a aplicação de página única lista tooDo e inicie sessão com uma esses utilizadores.</span><span class="sxs-lookup"><span data-stu-id="ce025-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="ce025-178">Adicionar a lista de tarefas do utilizador toohello tarefas, termine e inicie sessão novamente.</span><span class="sxs-lookup"><span data-stu-id="ce025-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="ce025-179">Adal.js torna as funcionalidades de identidade tooincorporate fácil comuns na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="ce025-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="ce025-180">-Trata da todo Olá dirty trabalho por si: gestão de cache, o suporte de protocolo de OAuth, apresentando utilizador Olá com uma início de sessão da IU, atualizar tokens expirados e muito mais.</span><span class="sxs-lookup"><span data-stu-id="ce025-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="ce025-181">Para referência, está disponível no exemplo de Olá concluído (sem os valores de configuração) [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ce025-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce025-182">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ce025-182">Next steps</span></span>
<span data-ttu-id="ce025-183">Agora pode passar tooadditional cenários.</span><span class="sxs-lookup"><span data-stu-id="ce025-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="ce025-184">É aconselhável tootry: [chamar uma API web CORS a partir de uma aplicação de página única](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="ce025-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
