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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Usar Olá biblioteca de autenticação da Microsoft (MSAL) Olá toosign no utilizador

1.  Crie um ficheiro denominado `app.js`. Se estiver a utilizar o Visual Studio, o projeto de Olá selecione (pasta raiz do projeto), clique com o botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`:
2.  Adicionar Olá seguinte código tooyour `app.js` ficheiro:

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
### <a name="more-information"></a>Mais Informações

Depois de um utilizador clica Olá *'Chamar Microsoft Graph API'* botão para Olá pela primeira vez, `callGraphApi` chamadas de método `loginRedirect` toosign utilizador Olá. Este método resulta em redirecionar Olá utilizador toohello *ponto final do Microsoft Azure Active Directory v2* tooprompt e validar as credenciais do utilizador Olá. Como resultado de um bem-sucedida início de sessão, o utilizador Olá é redirecionada toohello back original *index.html* página e um token é recebida, processados pelo `msal.js` e informações de Olá contidas no token de Olá é colocado em cache. Este token é conhecido como Olá *ID token* e contém informações básicas sobre utilizador Olá, tais como o nome a apresentar do utilizador Olá. Se planear toouse todos os dados fornecidos por este token para quaisquer fins, terá de toomake se que este token é validado pelo seu tooguarantee de servidor de back-end Olá token foi emitidos tooa utilizador válido para a sua aplicação.

Olá SPA gerado por este guia não fazer utiliza diretamente o token de ID de Olá – em vez disso, aquele invoca `acquireTokenSilent` e/ou `acquireTokenRedirect` tooacquire um *token de acesso* utilizado tooquery Olá Microsoft Graph API. Se precisar de uma amostra que valida o token de ID de Olá, observe [isto](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "exemplo active-directory-javascript-singlepageapp-dotnet-webapi-v2 Github") utiliza a aplicação de exemplo no GitHub – exemplo de Olá uma API Web do ASP.NET para validação do token.

#### <a name="getting-a-user-token-interactively"></a>A obter um utilizador token interativamente

Depois de Olá inicial início de sessão, não pretender Olá peça utilizadores tooreauthenticate sempre que precisam toorequest um token tooaccess um recurso –, por isso, *acquireTokenSilent* deve ser utilizada a maioria dos tokens de tooacquire Olá tempo. Existem no entanto situações que precisa de tooforce os utilizadores interagem com o ponto final de v2 do Azure Active Directory – alguns exemplos incluem:
-   Os utilizadores podem precisar tooreenter as respetivas credenciais porque a palavra-passe de Olá expirou
-   A aplicação está a pedir o recurso de tooa de acesso que Olá tooconsent necessidades de utilizador para
-   Não é necessária autenticação de dois fatores

Chamar Olá *acquireTokenRedirect(scope)* resultar em redireccionamento de ponto final de toohello v2 do Azure Active Directory de utilizadores (ou *acquireTokenPopup(scope)* resultado de uma janela de pop-up) onde os utilizadores precisam de toointeract com as respetivas credenciais, a instalação dar Olá consentimento toohello necessários recursos ou a autenticação de dois fatores Olá concluir.

#### <a name="getting-a-user-token-silently"></a>A obter um utilizador token automaticamente
Olá ` acquireTokenSilent` método processa aquisições token e a renovação sem qualquer interação do utilizador. Depois de `loginRedirect` (ou `loginPopup`) é executado para Olá pela primeira vez, `acquireTokenSilent` Olá método utilizado normalmente tooobtain tokens utilizados tooaccess protegido recursos para as chamadas subsequentes - como toorequest chamadas ou renovar tokens são efetuadas automaticamente.
`acquireTokenSilent`poderá falhar em alguns casos-por exemplo, a palavra-passe do utilizador Olá expirou. A aplicação pode processar esta exceção de duas formas:

1.  Efetuar uma chamada demasiado`acquireTokenRedirect` imediatamente, resultando num pedir Olá toosign de utilizador no. Este padrão é normalmente utilizado em aplicações online quando o utilizador de toohello disponíveis de aplicação Olá existir nenhum conteúdo não autenticado. exemplo de Olá gerado por esta configuração orientada utiliza este padrão.

2. Aplicações podem também efetuar um utilizador de toohello indicação visual que um interativa início de sessão é necessário, para que o utilizador Olá pode seleccionar Olá momento toosign no, ou pode tentar novamente a aplicação Olá `acquireTokenSilent` numa altura posterior. Isto é normalmente utilizado quando o utilizador Olá pode utilizar outras funcionalidades da aplicação Olá sem ser interrompidos, por exemplo, não há conteúdo não autenticado na aplicação Olá. Neste caso, o utilizador Olá pode decidir quando pretendem toosign no recurso de Olá protegido tooaccess ou toorefresh Olá desatualizada informações.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chamar Olá Microsoft Graph API a utilizar o token de Olá que apenas obteve

Adicionar Olá seguinte código tooyour `app.js` ficheiro:

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Obter mais informações sobre como efetuar uma chamada REST em relação a uma API protegida

Aplicação de exemplo de Olá criados por este guia, Olá `callWebApiWithToken()` método é utilizado toomake um HTTP `GET` pedido contra um recurso protegido que necessita de um autor da chamada do token e, em seguida, retorno Olá toohello conteúdo. Este método adiciona ao token de Olá adquirida Olá *cabeçalho de autorização de HTTP*. Para a aplicação de exemplo Olá criada por este guia, o recurso de Olá é Olá Microsoft Graph API *-me* ponto final – apresenta informações de perfil do utilizador Olá.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Adicionar um toosign método saída utilizador Olá

Adicionar Olá seguinte código tooyour `app.js` ficheiro:

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
