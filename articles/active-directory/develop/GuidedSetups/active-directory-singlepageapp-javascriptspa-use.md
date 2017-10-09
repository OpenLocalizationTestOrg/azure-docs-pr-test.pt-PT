---
title: "aaaAzure AD v2 JS SPA orientado configuração - utilização | Microsoft Docs"
description: "Como aplicações de JavaScript SPA podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="36d22-103">Usar Olá biblioteca de autenticação da Microsoft (MSAL) Olá toosign no utilizador</span><span class="sxs-lookup"><span data-stu-id="36d22-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="36d22-104">Crie um ficheiro denominado `app.js`.</span><span class="sxs-lookup"><span data-stu-id="36d22-104">Create a file named `app.js`.</span></span> <span data-ttu-id="36d22-105">Se estiver a utilizar o Visual Studio, o projeto de Olá selecione (pasta raiz do projeto), clique com o botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="36d22-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="36d22-106">Adicionar Olá seguinte código tooyour `app.js` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="36d22-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="36d22-107">Mais Informações</span><span class="sxs-lookup"><span data-stu-id="36d22-107">More Information</span></span>

<span data-ttu-id="36d22-108">Depois de um utilizador clica Olá *'Chamar Microsoft Graph API'* botão para Olá pela primeira vez, `callGraphApi` chamadas de método `loginRedirect` toosign utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="36d22-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="36d22-109">Este método resulta em redirecionar Olá utilizador toohello *ponto final do Microsoft Azure Active Directory v2* tooprompt e validar as credenciais do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="36d22-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="36d22-110">Como resultado de um bem-sucedida início de sessão, o utilizador Olá é redirecionada toohello back original *index.html* página e um token é recebida, processados pelo `msal.js` e informações de Olá contidas no token de Olá é colocado em cache.</span><span class="sxs-lookup"><span data-stu-id="36d22-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="36d22-111">Este token é conhecido como Olá *ID token* e contém informações básicas sobre utilizador Olá, tais como o nome a apresentar do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="36d22-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="36d22-112">Se planear toouse todos os dados fornecidos por este token para quaisquer fins, terá de toomake se que este token é validado pelo seu tooguarantee de servidor de back-end Olá token foi emitidos tooa utilizador válido para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="36d22-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="36d22-113">Olá SPA gerado por este guia não fazer utiliza diretamente o token de ID de Olá – em vez disso, aquele invoca `acquireTokenSilent` e/ou `acquireTokenRedirect` tooacquire um *token de acesso* utilizado tooquery Olá Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="36d22-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="36d22-114">Se precisar de uma amostra que valida o token de ID de Olá, observe [isto](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "exemplo active-directory-javascript-singlepageapp-dotnet-webapi-v2 Github") utiliza a aplicação de exemplo no GitHub – exemplo de Olá uma API Web do ASP.NET para validação do token.</span><span class="sxs-lookup"><span data-stu-id="36d22-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="36d22-115">A obter um utilizador token interativamente</span><span class="sxs-lookup"><span data-stu-id="36d22-115">Getting a user token interactively</span></span>

<span data-ttu-id="36d22-116">Depois de Olá inicial início de sessão, não pretender Olá peça utilizadores tooreauthenticate sempre que precisam toorequest um token tooaccess um recurso –, por isso, *acquireTokenSilent* deve ser utilizada a maioria dos tokens de tooacquire Olá tempo.</span><span class="sxs-lookup"><span data-stu-id="36d22-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="36d22-117">Existem no entanto situações que precisa de tooforce os utilizadores interagem com o ponto final de v2 do Azure Active Directory – alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="36d22-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="36d22-118">Os utilizadores podem precisar tooreenter as respetivas credenciais porque a palavra-passe de Olá expirou</span><span class="sxs-lookup"><span data-stu-id="36d22-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="36d22-119">A aplicação está a pedir o recurso de tooa de acesso que Olá tooconsent necessidades de utilizador para</span><span class="sxs-lookup"><span data-stu-id="36d22-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="36d22-120">Não é necessária autenticação de dois fatores</span><span class="sxs-lookup"><span data-stu-id="36d22-120">Two factor authentication is required</span></span>

<span data-ttu-id="36d22-121">Chamar Olá *acquireTokenRedirect(scope)* resultar em redireccionamento de ponto final de toohello v2 do Azure Active Directory de utilizadores (ou *acquireTokenPopup(scope)* resultado de uma janela de pop-up) onde os utilizadores precisam de toointeract com as respetivas credenciais, a instalação dar Olá consentimento toohello necessários recursos ou a autenticação de dois fatores Olá concluir.</span><span class="sxs-lookup"><span data-stu-id="36d22-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="36d22-122">A obter um utilizador token automaticamente</span><span class="sxs-lookup"><span data-stu-id="36d22-122">Getting a user token silently</span></span>
<span data-ttu-id="36d22-123">Olá ` acquireTokenSilent` método processa aquisições token e a renovação sem qualquer interação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="36d22-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="36d22-124">Depois de `loginRedirect` (ou `loginPopup`) é executado para Olá pela primeira vez, `acquireTokenSilent` Olá método utilizado normalmente tooobtain tokens utilizados tooaccess protegido recursos para as chamadas subsequentes - como toorequest chamadas ou renovar tokens são efetuadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="36d22-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="36d22-125">`acquireTokenSilent`poderá falhar em alguns casos-por exemplo, a palavra-passe do utilizador Olá expirou.</span><span class="sxs-lookup"><span data-stu-id="36d22-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="36d22-126">A aplicação pode processar esta exceção de duas formas:</span><span class="sxs-lookup"><span data-stu-id="36d22-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="36d22-127">Efetuar uma chamada demasiado`acquireTokenRedirect` imediatamente, resultando num pedir Olá toosign de utilizador no.</span><span class="sxs-lookup"><span data-stu-id="36d22-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="36d22-128">Este padrão é normalmente utilizado em aplicações online quando o utilizador de toohello disponíveis de aplicação Olá existir nenhum conteúdo não autenticado.</span><span class="sxs-lookup"><span data-stu-id="36d22-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="36d22-129">exemplo de Olá gerado por esta configuração orientada utiliza este padrão.</span><span class="sxs-lookup"><span data-stu-id="36d22-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="36d22-130">Aplicações podem também efetuar um utilizador de toohello indicação visual que um interativa início de sessão é necessário, para que o utilizador Olá pode seleccionar Olá momento toosign no, ou pode tentar novamente a aplicação Olá `acquireTokenSilent` numa altura posterior.</span><span class="sxs-lookup"><span data-stu-id="36d22-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="36d22-131">Isto é normalmente utilizado quando o utilizador Olá pode utilizar outras funcionalidades da aplicação Olá sem ser interrompidos, por exemplo, não há conteúdo não autenticado na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="36d22-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="36d22-132">Neste caso, o utilizador Olá pode decidir quando pretendem toosign no recurso de Olá protegido tooaccess ou toorefresh Olá desatualizada informações.</span><span class="sxs-lookup"><span data-stu-id="36d22-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="36d22-133">Chamar Olá Microsoft Graph API a utilizar o token de Olá que apenas obteve</span><span class="sxs-lookup"><span data-stu-id="36d22-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="36d22-134">Adicionar Olá seguinte código tooyour `app.js` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="36d22-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in hello page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in hello page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="36d22-135">Obter mais informações sobre como efetuar uma chamada REST em relação a uma API protegida</span><span class="sxs-lookup"><span data-stu-id="36d22-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="36d22-136">Aplicação de exemplo de Olá criados por este guia, Olá `callWebApiWithToken()` método é utilizado toomake um HTTP `GET` pedido contra um recurso protegido que necessita de um autor da chamada do token e, em seguida, retorno Olá toohello conteúdo.</span><span class="sxs-lookup"><span data-stu-id="36d22-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="36d22-137">Este método adiciona ao token de Olá adquirida Olá *cabeçalho de autorização de HTTP*.</span><span class="sxs-lookup"><span data-stu-id="36d22-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="36d22-138">Para a aplicação de exemplo Olá criada por este guia, o recurso de Olá é Olá Microsoft Graph API *-me* ponto final – apresenta informações de perfil do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="36d22-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="36d22-139">Adicionar um toosign método saída utilizador Olá</span><span class="sxs-lookup"><span data-stu-id="36d22-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="36d22-140">Adicionar Olá seguinte código tooyour `app.js` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="36d22-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
