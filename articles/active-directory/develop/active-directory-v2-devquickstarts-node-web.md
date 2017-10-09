---
title: "v 2.0 do Active Directory aaaAzure sessão-in de aplicação de web de Node.js | Microsoft Docs"
description: "Saiba como toobuild um Node.js web de aplicação que inicia sessão um utilizador através de uma conta Microsoft pessoal e uma conta escolar ou profissional."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a>Adicionar a aplicação de web de Node.js tooa início de sessão

> [!NOTE]
> Nem todos os cenários do Azure Active Directory e funcionalidades funcionam com o ponto final de v 2.0 Olá. toodetermine se deve utilizar o ponto final de v 2.0 Olá ou o ponto final de v 1.0 Olá, leia sobre [limitações de v 2.0](active-directory-v2-limitations.md).
> 

Neste tutorial, utilizamos Olá do Passport toodo seguintes tarefas:

* Numa aplicação web, inicie sessão no utilizador Olá utilizando o Azure Active Directory (Azure AD) e Olá ponto final v 2.0.
* Apresentar informações sobre Olá utilizador.
* Início de sessão Olá utilizador fora da aplicação Olá.

**Passport** é o middleware de autenticação do Node.js. Flexível e modulares, Passport pode ser removido discretamente em qualquer baseada em Express ou restify aplicação web. No Passport, um conjunto abrangente de estratégias suporta a autenticação utilizando um nome de utilizador e palavra-passe, Facebook, Twitter ou outras opções. Desenvolvemos uma estratégia para o Azure AD. Neste artigo, vamos mostrar-lhe como tooinstall Olá módulo e, em seguida, adicione Olá do Azure AD `passport-azure-ad` Plug-in.

## <a name="download"></a>Transferência
código Olá deste tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs). tutorial de Olá toofollow, pode [transferir a estrutura da aplicação de Olá como um ficheiro. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) ou estrutura de Olá do clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Também pode obter a aplicação Olá concluído no final deste tutorial Olá.

## <a name="1-register-an-app"></a>1: registar uma aplicação
Criar uma nova aplicação em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou seguir [detalhadas destes passos](active-directory-v2-app-registration.md) tooregister uma aplicação. Certifique-se de que:

* Olá cópia **Id da aplicação** atribuído tooyour aplicação. É necessário para este tutorial.
* Adicionar Olá **Web** plataforma para a sua aplicação.
* Olá cópia **URI de redirecionamento** do portal de Olá. Tem de utilizar Olá URI o valor predefinido do `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-add-prerequisities-tooyour-directory"></a>2: Adicionar prerequisities tooyour diretório
Numa linha de comandos, altere os diretórios toogo tooyour a pasta raiz, se não estiver já existe. Execute Olá os seguintes comandos:

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

Além disso, utilizamos `passport-azure-ad` na estrutura de Olá do início rápido de Olá:

* `npm install passport-azure-ad`

Esta ação instala bibliotecas Olá que `passport-azure-ad` utiliza.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3: configurar a aplicação toouse Olá passport-nó-js estratégia
Configure Olá do Olá rápida middleware toouse protocolo de autenticação OpenID Connect. Utilize os pedidos de início de sessão e fim de sessão de tooissue do Passport, gerir Olá da sessão de utilizador e obter informações sobre o utilizador Olá, entre outros.

1.  Na raiz de Olá do projeto de Olá, abra o ficheiro de Config.js Olá. No Olá `exports.creds` secção, introduza os valores de configuração da sua aplicação.
  
  * `clientID`: Olá **Id da aplicação** que é atribuído tooyour aplicação no Olá portal do Azure.
  * `returnURL`: Olá **URI de redirecionamento** que introduziu no portal de Olá.
  * `clientSecret`: segredo Olá que gerou no portal de Olá.

2.  Na raiz de Olá do projeto de Olá, abra o ficheiro de App.js Olá. tooinvoke Olá OIDCStrategy stratey vem com `passport-azure-ad`, adicionar Olá seguinte chamada:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle os pedidos de início de sessão, utilize a estratégia de Olá acabou de referenciar:

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
      process.nextTick(function () {
        findByEmail(profile.email, function(err, user) {
          if (err) {
            return done(err);
          }
          if (!user) {
            // "Auto-registration"
            users.push(profile);
            return done(null, profile);
          }
          return done(null, user);
        });
      });
    }
  ));
  ```

O Passport utiliza um padrão semelhante para todas as respetivas estratégias (Twitter, Facebook e assim sucessivamente). Todos os escritores aderem toohello padrão. Passar a estratégia de Olá um `function()` que utiliza um token e `done` como parâmetros. estratégia de Olá é devolvida após faz todos os respetivo trabalho. Utilizador de Olá do arquivo e um token de Olá stash por isso não terá tooask-lo novamente.

  > [!IMPORTANT]
  > Olá código anterior entra em qualquer utilizador que pode autenticar o servidor de tooyour. Isto é conhecido como registo automático. Num servidor de produção, que não pretende toolet qualquer pessoa sem primeiro passá-los através de um processo de registo que escolher. Isto é normalmente padrão Olá que veem nas aplicações de consumidor. aplicação Olá pode permitir-lhe tooregister com o Facebook, mas, em seguida, este pede-lhe tooenter obter informações adicionais. Se não utilizar um programa da linha de comandos para este tutorial, foi possível extrair o e-mail Olá do objeto token Olá que é devolvido. Em seguida, poderá pedir-lhe as informações de Olá utilizador tooenter adicionais. Porque se trata de um servidor de teste, adicione o utilizador Olá diretamente toohello dentro da memória base de dados.
  > 
  > 

4.  Adicione os métodos de Olá que utilize tookeep controlar de utilizadores tem sessão iniciada, conforme requerido pelo Passport. Isto inclui informações do utilizador Olá de serialização e:

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
  var users = [];

  var findByEmail = function(email, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
      var user = users[i];
      log.info('we are using user: ', user);
      if (user.email === email) {
        return fn(null, user);
      }
    }
    return fn(null, null);
  };
  ```

5.  Adicione o código de Olá que carrega o motor de Express de Olá. Utilizar Olá predefinido /views e padrão de /routes Express fornece:

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  Adicionar Olá POST encaminha esse mão desativar Olá real pedidos de início de sessão toohello `passport-azure-ad` motor:

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4: utilizar o Passport tooissue início de sessão e fim de sessão pedidos tooAzure AD
A aplicação está agora configurada toocommunicate com o ponto final de v 2.0 Olá através do protocolo de autenticação OpenID Connect Olá. Olá `passport-azure-ad` estratégia encarrega-se de todos os detalhes de Olá de mensagens de autenticação de composição, tokens de validação do Azure AD e manutenção de sessão do utilizador Olá. Tudo o que for deixado toodo é toogive aos utilizadores uma forma toosign no e início de sessão fora e toogather mais informações sobre o utilizador Olá que tenha sessão iniciada.

1.  Adicionar Olá **predefinido**, **início de sessão**, **conta**, e **terminar** ficheiro de App.js tooyour métodos:

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  Seguem-se detalhes Olá:
    
    * Olá `/` rota redireciona toohello index.ejs vista. Transmite os utilizador Olá no pedido de Olá (se existir).
    * Olá `/account` encaminhar primeiro *garante que sejam autenticados* (implementar que no Olá código a seguir). Em seguida, transmite utilizador Olá no pedido de Olá. Isto é, pelo que pode obter mais informações sobre o utilizador Olá.
    * Olá `/login` encaminhar chamadas a `azuread-openidconnect` autenticador de `passport-azuread`. Se o que não for bem sucedido, será redirecionado novamente a utilizador Olá demasiado`/login`.
    * Olá `/logout` rota chama Olá logout.ejs vista (e rota). Isto limpa cookies e, em seguida, devolve Olá tooindex.ejs back do utilizador.

2.  Adicionar Olá **EnsureAuthenticated** método que utilizou anteriormente no `/account`:

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  Crie App.js, servidor Olá:

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5: criar Olá vistas e rotas no Express que mostram o utilizador no Web site de Olá
Adicione rotas Olá e vistas que apresentam o utilizador de toohello de informações. Olá rotas e vistas também processam Olá `/logout` e `/login` rotas que criou.

1. No diretório de raiz de Olá, criar Olá `/routes/index.js` rota.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  No diretório de raiz de Olá, criar Olá `/routes/user.js` rota.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`e `/routes/user.js` são rotas simples transferem Olá pedido tooyour das vistas, incluindo utilizador Olá, se estiver presente.

3.  No diretório de raiz de Olá, criar Olá `/views/index.ejs` vista. Esta página chama o **início de sessão** e **terminar** métodos. Também é utilizar Olá `/views/index.ejs` ver informações de conta toocapture. Pode utilizar Olá condicional `if (!user)` como utilizador Olá que está a ser transferido no pedido de Olá. É uma prova que tem um utilizador com sessão iniciado.

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  No diretório de raiz de Olá, criar Olá `/views/account.ejs` vista. Olá `/views/account.ejs` vista permite-lhe tooview obter informações adicionais que `passport-azuread` coloca no pedido do utilizador Olá.

  ```Javascript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
  <p>displayName: <%= user.displayName %></p>
  <p>givenName: <%= user.name.givenName %></p>
  <p>familyName: <%= user.name.familyName %></p>
  <p>UPN: <%= user._json.upn %></p>
  <p>Profile ID: <%= user.id %></p>
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  Adicione um esquema. No diretório de raiz de Olá, criar Olá `/views/layout.ejs` vista.

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  toobuild e executar a aplicação, executar `node app.js`. Em seguida, aceda demasiado`http://localhost:3000`.

7.  Inicie sessão com uma conta Microsoft pessoal ou uma conta escolar ou profissional. Tenha em atenção que a identidade do utilizador Olá é refletida na lista de /account Olá. 

Tem agora uma aplicação web que está protegida pela utilização de protocolos padrão da indústria. Pode autenticar utilizadores na sua aplicação através das respetivas contas pessoais, profissionais ou escolares.

## <a name="next-steps"></a>Passos seguintes
Para referência, o exemplo de Olá concluído (sem os valores de configuração) é fornecido tal como [um ficheiro. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip). Também pode cloná-lo a partir do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Em seguida, pode passar toomore avançadas tópicos. Poderá querer tootry:

[Proteger uma API web do Node.js utilizando o ponto final de v 2.0 Olá](active-directory-v2-devquickstarts-node-api.md)

Seguem-se alguns recursos adicionais:

* [Guia para programadores do Azure AD v 2.0](active-directory-appmodel-v2-overview.md)
* [Etiqueta de "azure-active-directory" capacidade excedida da pilha](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Obter atualizações de segurança dos nossos produtos
Aconselhamo-toosign segurança toobe notificado quando ocorrem incidentes de segurança. No Olá [as notificações de segurança técnica Microsoft](https://technet.microsoft.com/security/dd252948) página, tooSecurity Advisories alertas de subscrição.

