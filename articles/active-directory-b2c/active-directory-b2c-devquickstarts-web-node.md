---
title: "aplicação web de Node.js de início de sessão tooa do aaaAdd para o Azure B2C | Microsoft Docs"
description: "Como toobuild uma aplicação web Node.js que inicia sessão dos utilizadores através da utilização de um inquilino do B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>O Azure AD B2C: Adicionar início de sessão tooa aplicação de web de Node.js

**Passport** é o middleware de autenticação do Node.js. Extremamente flexível e modular, o Passport pode ser instalado discretamente em qualquer aplicação Web baseada em Express ou Restify. Um conjunto abrangente de estratégias suporta a autenticação utilizando um nome de utilizador e palavra-passe, o Facebook, o Twitter e muito mais.

Desenvolvemos uma estratégia para o Azure Active Directory (Azure AD). Instalará este módulo e, em seguida, adicionar Olá do Azure AD `passport-azure-ad` Plug-in.

toodo, tem de:

1. Registar uma aplicação utilizando o Azure AD.
2. Configurar a sua Olá de toouse aplicação `passport-azure-ad` Plug-in.
3. Utilize Passport tooissue início de sessão e fim de sessão pedidos tooAzure AD.
4. Imprimir os dados de utilizador.

Olá código para este tutorial [é mantido no GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS). toofollow ao longo, pode [transferir a estrutura da aplicação de Olá como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip). Também pode clonar a estrutura de Olá:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

aplicação Olá concluída é fornecida no final deste tutorial Olá.

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório do Azure AD B2C

Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.  Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos, etc. Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.

## <a name="create-an-application"></a>Criar uma aplicação

Em seguida, terá de toocreate uma aplicação no diretório do B2C. Isto dá-informações do Azure AD que necessita de toocommunicate em segurança com a sua aplicação. Olá ambas as aplicações cliente e a web API será representada por um único **ID da aplicação**, uma vez que compõem uma aplicação lógica. toocreate uma aplicação, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário:

- Incluir um **aplicação web**/**web API** na aplicação Olá.
- Introduzir `http://localhost:3000/auth/openid/return` como um **URL de resposta**. É Olá predefinido URL para este exemplo de código.
- Criar um **Segredo de aplicação** para a aplicação e copiá-lo. Precisará dele mais tarde. Tenha em atenção que este valor tem de toobe [XML de escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de o utilizar.
- Olá cópia **ID da aplicação** que é atribuído tooyour aplicação. Também irá precisar deste mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar as políticas

No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md). Esta aplicação contém três experiências de identidade: inscrição, início de sessão e início de sessão utilizando o Facebook. Terá de toocreate esta política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Quando criar as três políticas, não se esqueça de:

- Escolha Olá **nome a apresentar** e outros atributos de inscrição na política de inscrição.
- Escolha Olá **nome a apresentar** e **ID de objeto** afirmações de aplicação em cada política. Também pode escolher outras afirmações.
- Olá cópia **nome** de cada política depois de a criar. Deve ter o prefixo de Olá `b2c_1_`.  Precisará destes nomes de políticas mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois de criar as três políticas, está pronto toobuild a aplicação.

Tenha em atenção que este artigo não abrange como as políticas de Olá toouse que acabou de criar. toolearn sobre como funcionam as políticas no Azure AD B2C, comece com Olá [.NET introdução à aplicação web tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="add-prerequisites-tooyour-directory"></a>Adicionar pré-requisitos tooyour diretório

Olá linha de comandos, altere a pasta de raiz tooyour diretórios, se não estiver já existe. Execute Olá os seguintes comandos:

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

Além disso, utilizámos `passport-azure-ad` para a nossa pré-visualização na estrutura de Olá de Olá início rápido.

- `npm install passport-azure-ad`

Esta ação instalará bibliotecas Olá que `passport-azure-ad` depende.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>Configurar a sua Olá toouse de aplicação estratégia Passport-node.js
Configure Olá do Olá rápida middleware toouse protocolo de autenticação OpenID Connect. O Passport será utilizado tooissue pedidos de início de sessão e fim de sessão, gerir sessões de utilizador e obter informações sobre utilizadores, entre outras ações.

Abra Olá `config.js` ficheiro na raiz de Olá do projeto de Olá e introduza os valores de configuração da sua aplicação no Olá `exports.creds` secção.
- `clientID`: Olá **ID da aplicação** atribuído tooyour aplicação no portal de registo Olá.
- `returnURL`: Olá **URI de redirecionamento** que introduziu no portal de Olá.
- `tenantName`: nome do inquilino Olá da sua aplicação, por exemplo, **contoso.onmicrosoft.com**.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Abra Olá `app.js` ficheiro na raiz de Olá do projeto de Olá. Adicionar Olá seguir chamada tooinvoke Olá `OIDCStrategy` estratégia que vem com `passport-azure-ad`.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

Utilize a estratégia de Olá acabou de referenciar pedidos de início de sessão toohandle.

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
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
O Passport utiliza um padrão semelhante para todos as respetivas estratégias (incluindo o Twitter e o Facebook). Todos os escritores aderem toothis padrão. Quando observa a estratégia de Olá, pode ver que transmite um `function()` que tem um token e um `done` como parâmetros de Olá. estratégia de Olá volta a tooyou depois-tem de fazer todo o trabalho. Armazene o utilizador Olá e guarde o token de Olá, de modo que não seja necessário tooask-lo novamente.

> [!IMPORTANT]
Olá código anterior entra em todos os utilizadores a quem Olá servidor autentica. Este é registo automático. Quando utiliza servidores de produção, que não pretende toolet sessão dos utilizadores, a menos que tenham passado por um processo de registo que configurou. Muitas vezes, pode ver este padrão nas aplicações de consumidor. Estas permitem-lhe tooregister utilizando o Facebook, mas, em seguida, solicitam-lhe toofill informações adicionais. Se a nossa aplicação não era uma amostra, iremos foi extrair um endereço de e-mail do objeto token Olá que é devolvido e, em seguida, peça ao Olá utilizador toofill informações adicionais. Porque se trata de um servidor de teste, adicionamos simplesmente utilizadores toohello dentro da memória da base de dados.

Adicionar métodos de Olá que lhe permitem controlar tookeep de utilizadores que tenham iniciado sessão, conforme requerido pelo Passport. Isto inclui informações de utilizador de serialização e não serialização:

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
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

Adicione o motor do Olá código tooload Olá Express. No seguinte Olá, pode ver que utilizamos a predefinição de Olá `/views` e `/routes` padrão que o Express fornece.

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

Adicionar Olá `POST` Olá de rotas que entregam os pedidos de início de sessão real toohello `passport-azure-ad` motor:

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Utilizar Passport tooissue início de sessão e fim de sessão pedidos tooAzure AD

A aplicação está agora toocommunicate configurado corretamente com o ponto final de v 2.0 Olá através do protocolo de autenticação OpenID Connect Olá. `passport-azure-ad`tem Tratado dos detalhes de Olá de mensagens de autenticação de composição, tokens de validação do Azure AD e manutenção de sessão do utilizador. Tudo o que resta é toogive os seus utilizadores uma forma toosign no e início de sessão fora e toogather informações adicionais sobre os utilizadores que têm sessão iniciada.

Primeiro, adicione Olá predefinição, início de sessão, conta e fim de sessão métodos tooyour `app.js` ficheiro:

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in hello Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

tooreview estes métodos em detalhe:
- Olá `/` rota redireciona toohello `index.ejs` vista transferindo o utilizador Olá no pedido de Olá (se existir).
- Olá `/account` rota verifica primeiro se está autenticado (Olá implementação para esta situação é abaixo). -Lo, em seguida, transmite utilizador Olá no pedido de Olá, de modo a que pode obter informações adicionais sobre o utilizador Olá.
- Olá `/login` rota chamadas Olá `azuread-openidconnect` autenticador de `passport-azure-ad`. Se não for bem-sucedida, rota Olá redireciona volta a utilizador Olá demasiado`/login`.
- `logout.ejs` chama simplesmente `/logout` (e a respetiva rota). Isto limpa cookies e, em seguida, devolve Olá utilizador volta demasiado`index.ejs`.


Para Olá última parte `app.js`, adicionar Olá `EnsureAuthenticated` método que é utilizado no Olá `/account` rota.

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

Por fim, crie o próprio servidor de Olá no `app.js`.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Criar Olá vistas e rotas no Express toocall as políticas

O `app.js` está agora concluído. Basta rotas de Olá tooadd e vistas que lhe permitem toocall Olá início de sessão e inscrição as políticas. Estas também processar Olá `/logout` e `/login` rotas que criou.

Criar Olá `/routes/index.js` rota no diretório de raiz de Olá.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Criar Olá `/routes/user.js` rota no diretório de raiz de Olá.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

Estas rotas simples transferem vistas de tooyour de pedidos. Incluem utilizador Olá, se estiver presente.

Criar Olá `/views/index.ejs` vista no diretório de raiz de Olá. Esta é uma página simples que chama as políticas para o início de sessão e fim de sessão. Também pode utilizá-la toograb informações da conta. Tenha em atenção que pode utilizar Olá condicional `if (!user)` como utilizador Olá é transferido no pedido de Olá tooprovide evidence esse utilizador Olá tem sessão iniciado.

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

Criar Olá `/views/account.ejs` ver no diretório de raiz de Olá, para que possa visualizar informações adicionais que `passport-azure-ad` colocar no pedido do utilizador Olá.

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
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

Agora pode criar e executar a aplicação.

Executar `node app.js` e navegue demasiado`http://localhost:3000`


Inscrever-se ou iniciar sessão na aplicação toohello através de e-mail ou o Facebook. Termine sessão e inicie sessão novamente como um utilizador diferente.

##<a name="next-steps"></a>Passos seguintes

Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Também pode clonar a partir do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

Agora pode passar toomore avançadas tópicos. Pode experimentar:

[Proteger uma API web utilizando o modelo de Olá B2C no Node.js](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
