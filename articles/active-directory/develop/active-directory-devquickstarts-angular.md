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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>Ajudar a proteger as aplicações de página única AngularJS por utilizar o Azure AD

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD) torna simples e fácil para tooadd início de sessão, fim de sessão, e segura OAuth API chama tooyour aplicações de página única.  Isto permite que os utilizadores de tooauthenticate aplicações com as respetivas contas do Windows Server Active Directory e consumir quaisquer web API do Azure AD ajuda a proteger, tais como Olá APIs do Office 365 ou Olá API do Azure.

Para aplicações de JavaScript em execução num browser, o Azure AD fornece Olá Active Directory Authentication Library (ADAL) ou adal.js. Olá único objetivo adal.js é toomake-lo mais fácil para os tokens de acesso de tooget de aplicação. é, tal como fácil toodemonstrate aqui irá criar uma aplicação de lista de tooDo AngularJS que:

* Sinais Olá utilizador na aplicação toohello através da utilização do Azure AD como fornecedor de identidade Olá.

* Mostra algumas informações sobre o utilizador Olá.
* Em segurança chamadas Olá tooDo da aplicação API da lista, utilizando os tokens de portador do Azure AD.
* Sinais Olá utilizador fora da aplicação Olá.

toobuild Olá concluída, aplicação de trabalho, tem de:

1. Registe a sua aplicação com o Azure AD.
2. Instale o ADAL e configure a aplicação de página única Olá.
3. Utilize páginas segura ADAL toohelp na aplicação de página única Olá.

tooget iniciado, [transferir a estrutura de aplicação Olá](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) ou [transferir exemplo Olá concluída](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). Também precisa de um inquilino do Azure AD, onde pode criar utilizadores e registar uma aplicação. Se ainda não tiver um inquilino, [Saiba como tooget um](active-directory-howto-tenant.md).

## <a name="step-1-register-hello-directorysearcher-application"></a>Passo 1: Registar a aplicação de DirectorySearcher Olá
tooenable dos seus utilizadores tooauthenticate de aplicação e obter tokens, primeiro tem de inquilino do tooregistê-lo no seu Azure AD:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Se tem sessão iniciada toomultiple diretórios, poderá ser necessário tooensure está a visualizar correta do diretório Olá. toodo por isso, na barra superior Olá, clique em sua conta. Em Olá **diretório** lista, escolha inquilino Olá do Azure AD, onde pretende tooregister a aplicação.
3. Clique em **mais serviços** no Olá painel esquerdo e, em seguida, selecione **do Azure Active Directory**.
4. Clique em **registos de aplicação**e, em seguida, selecione **adicionar**.
5. Siga as instruções de Olá e crie uma nova aplicação web e/ou web API:
  * **Nome** descreve toousers sua aplicação.
  * **Uri de redirecionamento** é Olá toowhich de localização do Azure AD irá devolver tokens. Olá a localização predefinida para este exemplo é `https://localhost:44326/`.
6. Depois de concluir o registo, o Azure AD atribui uma aplicação de tooyour de ID de aplicação único.  Irá precisar deste valor nas secções seguintes Olá, por isso, copiá-lo a partir do separador de aplicação Olá.
7. Adal.js utiliza toocommunicate de fluxo implícito de OAuth Olá com o Azure AD. Tem de ativar o fluxo implícito Olá para a sua aplicação:
  1. Clique em aplicação Olá e selecione **manifesto** editor de manifesto tooopen Olá inline.
  2. Localizar Olá `oauth2AllowImplicitFlow` propriedade. Defina o respetivo valor demasiado`true`.
  3. Clique em **guardar** manifesto de Olá toosave.
8. Conceder permissões em seu inquilino para a sua aplicação. Aceda demasiado**definições** > **propriedades** > **permissões obrigatórias**e clique em Olá **conceder permissões**botão na barra superior Olá. Clique em **Sim** tooconfirm.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>Passo 2: Instalar ADAL e configure a aplicação de página única Olá
Agora que tem uma aplicação no Azure AD, pode instalar adal.js e escrever o seu código relacionadas com identidade.

### <a name="configure-hello-javascript-client"></a>Configurar o cliente de JavaScript Olá
Comece por adicionar adal.js toohello TodoSPA projeto utilizando Olá consola do Gestor de pacotes:
  1. Transferir [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) e adicioná-la toohello `App/Scripts/` diretório de projeto.
  2. Transferir [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) e adicioná-la toohello `App/Scripts/` diretório de projeto.
  3. Carregar cada script antes de fim de Olá do Olá `</body>` no `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Configurar o servidor de back-end Olá
Para tooDo de back-end lista API tooaccept tokens da aplicação de página única Olá a partir do browser Olá, o back-end Olá tem informações de configuração sobre o registo de aplicação Olá. No projeto de TodoSPA Olá, abra `web.config`. Substitua os valores de Olá de elementos Olá Olá `<appSettings>` Olá de secção tooreflect Olá valores que utilizou no portal do Azure. O código será referenciar estes valores, sempre que utilizar a ADAL.
  * `ida:Tenant`é Olá domínio de inquilino do Azure AD – por exemplo, contoso.onmicrosoft.com.
  * `ida:Audience`é o ID de cliente Olá da sua aplicação que copiou do portal de Olá.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>Passo 3: Utilize ADAL toohelp seguras as páginas na aplicação de página única Olá
Adal.js integra AngularJS rota e fornecedores de HTTP, para que possa ajudar vistas individuais seguras na sua aplicação de página única.

1. No `App/Scripts/app.js`, coloque do módulo de adal.js Olá:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Inicializar `adalProvider` utilizando valores de configuração de Olá de registo da aplicação, também `App/Scripts/app.js`:

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
3. Ajudar a proteger Olá `TodoList` vista na aplicação Olá utilizando apenas uma linha de código: `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Resumo
Tem agora uma aplicação de página única segura, que pode iniciar sessão em utilizadores e emitir pedidos protegidos de token de portador tooits back-end API. Quando um utilizador clica Olá **TodoList** ligação, adal.js será automaticamente redirecionado tooAzure AD para início de sessão se necessário. Além disso, adal.js ligará automaticamente um acesso token tooany Ajax pedidos que são enviadas de back-end da aplicação toohello.  

Olá passos anteriores são Olá bare mínimo necessário toobuild uma aplicação de página única com adal.js. Mas algumas outras funcionalidades são úteis na aplicação de página única:

* tooexplicitly emitir pedidos de início de sessão e fim de sessão, pode definir funções os controladores que invocam adal.js.  No `App/Scripts/homeCtrl.js`:

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
* Pode querer toopresent informações de utilizador na IU da aplicação Olá. Olá serviço ADAL já foi adicionado toohello `userDataCtrl` controlador, para que possa aceder Olá `userInfo` objeto no Olá associado à vista, `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* Existem muitos cenários em que poderá ser útil tooknow se o utilizador Olá tem sessão iniciada ou não. Também pode utilizar Olá `userInfo` objeto toogather estas informações.  Por exemplo, no `index.html`, pode mostrar o Olá **início de sessão** ou **terminar** botão com base no estado de autenticação:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

A aplicação de página única integrada no AD do Azure pode autenticar os utilizadores, em segurança chamar o back-end através da utilização de OAuth 2.0 e obter informações básicas sobre utilizador Olá. Se ainda não o fez, agora é Olá tempo toopopulate do inquilino com alguns utilizadores. Executar a aplicação de página única lista tooDo e inicie sessão com uma esses utilizadores. Adicionar a lista de tarefas do utilizador toohello tarefas, termine e inicie sessão novamente.

Adal.js torna as funcionalidades de identidade tooincorporate fácil comuns na sua aplicação. -Trata da todo Olá dirty trabalho por si: gestão de cache, o suporte de protocolo de OAuth, apresentando utilizador Olá com uma início de sessão da IU, atualizar tokens expirados e muito mais.

Para referência, está disponível no exemplo de Olá concluído (sem os valores de configuração) [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Passos seguintes
Agora pode passar tooadditional cenários. É aconselhável tootry: [chamar uma API web CORS a partir de uma aplicação de página única](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
