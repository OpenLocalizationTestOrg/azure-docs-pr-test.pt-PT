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
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="43486-103">Adicionar a aplicação de web de Node.js tooa início de sessão</span><span class="sxs-lookup"><span data-stu-id="43486-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="43486-104">Nem todos os cenários do Azure Active Directory e funcionalidades funcionam com o ponto final de v 2.0 Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="43486-105">toodetermine se deve utilizar o ponto final de v 2.0 Olá ou o ponto final de v 1.0 Olá, leia sobre [limitações de v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="43486-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="43486-106">Neste tutorial, utilizamos Olá do Passport toodo seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="43486-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="43486-107">Numa aplicação web, inicie sessão no utilizador Olá utilizando o Azure Active Directory (Azure AD) e Olá ponto final v 2.0.</span><span class="sxs-lookup"><span data-stu-id="43486-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="43486-108">Apresentar informações sobre Olá utilizador.</span><span class="sxs-lookup"><span data-stu-id="43486-108">Display information about hello user.</span></span>
* <span data-ttu-id="43486-109">Início de sessão Olá utilizador fora da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="43486-110">**Passport** é o middleware de autenticação do Node.js.</span><span class="sxs-lookup"><span data-stu-id="43486-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="43486-111">Flexível e modulares, Passport pode ser removido discretamente em qualquer baseada em Express ou restify aplicação web.</span><span class="sxs-lookup"><span data-stu-id="43486-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="43486-112">No Passport, um conjunto abrangente de estratégias suporta a autenticação utilizando um nome de utilizador e palavra-passe, Facebook, Twitter ou outras opções.</span><span class="sxs-lookup"><span data-stu-id="43486-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="43486-113">Desenvolvemos uma estratégia para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43486-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="43486-114">Neste artigo, vamos mostrar-lhe como tooinstall Olá módulo e, em seguida, adicione Olá do Azure AD `passport-azure-ad` Plug-in.</span><span class="sxs-lookup"><span data-stu-id="43486-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="43486-115">Transferência</span><span class="sxs-lookup"><span data-stu-id="43486-115">Download</span></span>
<span data-ttu-id="43486-116">código Olá deste tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="43486-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="43486-117">tutorial de Olá toofollow, pode [transferir a estrutura da aplicação de Olá como um ficheiro. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) ou estrutura de Olá do clone:</span><span class="sxs-lookup"><span data-stu-id="43486-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="43486-118">Também pode obter a aplicação Olá concluído no final deste tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="43486-119">1: registar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="43486-119">1: Register an app</span></span>
<span data-ttu-id="43486-120">Criar uma nova aplicação em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou seguir [detalhadas destes passos](active-directory-v2-app-registration.md) tooregister uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="43486-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="43486-121">Certifique-se de que:</span><span class="sxs-lookup"><span data-stu-id="43486-121">Make sure you:</span></span>

* <span data-ttu-id="43486-122">Olá cópia **Id da aplicação** atribuído tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="43486-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="43486-123">É necessário para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="43486-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="43486-124">Adicionar Olá **Web** plataforma para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="43486-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="43486-125">Olá cópia **URI de redirecionamento** do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="43486-126">Tem de utilizar Olá URI o valor predefinido do `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="43486-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="43486-127">2: Adicionar prerequisities tooyour diretório</span><span class="sxs-lookup"><span data-stu-id="43486-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="43486-128">Numa linha de comandos, altere os diretórios toogo tooyour a pasta raiz, se não estiver já existe.</span><span class="sxs-lookup"><span data-stu-id="43486-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="43486-129">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="43486-129">Run hello following commands:</span></span>

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

<span data-ttu-id="43486-130">Além disso, utilizamos `passport-azure-ad` na estrutura de Olá do início rápido de Olá:</span><span class="sxs-lookup"><span data-stu-id="43486-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="43486-131">Esta ação instala bibliotecas Olá que `passport-azure-ad` utiliza.</span><span class="sxs-lookup"><span data-stu-id="43486-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="43486-132">3: configurar a aplicação toouse Olá passport-nó-js estratégia</span><span class="sxs-lookup"><span data-stu-id="43486-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="43486-133">Configure Olá do Olá rápida middleware toouse protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="43486-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="43486-134">Utilize os pedidos de início de sessão e fim de sessão de tooissue do Passport, gerir Olá da sessão de utilizador e obter informações sobre o utilizador Olá, entre outros.</span><span class="sxs-lookup"><span data-stu-id="43486-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="43486-135">Na raiz de Olá do projeto de Olá, abra o ficheiro de Config.js Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="43486-136">No Olá `exports.creds` secção, introduza os valores de configuração da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="43486-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="43486-137">`clientID`: Olá **Id da aplicação** que é atribuído tooyour aplicação no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="43486-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="43486-138">`returnURL`: Olá **URI de redirecionamento** que introduziu no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="43486-139">`clientSecret`: segredo Olá que gerou no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="43486-140">Na raiz de Olá do projeto de Olá, abra o ficheiro de App.js Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="43486-141">tooinvoke Olá OIDCStrategy stratey vem com `passport-azure-ad`, adicionar Olá seguinte chamada:</span><span class="sxs-lookup"><span data-stu-id="43486-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="43486-142">toohandle os pedidos de início de sessão, utilize a estratégia de Olá acabou de referenciar:</span><span class="sxs-lookup"><span data-stu-id="43486-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

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

<span data-ttu-id="43486-143">O Passport utiliza um padrão semelhante para todas as respetivas estratégias (Twitter, Facebook e assim sucessivamente).</span><span class="sxs-lookup"><span data-stu-id="43486-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="43486-144">Todos os escritores aderem toohello padrão.</span><span class="sxs-lookup"><span data-stu-id="43486-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="43486-145">Passar a estratégia de Olá um `function()` que utiliza um token e `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="43486-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="43486-146">estratégia de Olá é devolvida após faz todos os respetivo trabalho.</span><span class="sxs-lookup"><span data-stu-id="43486-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="43486-147">Utilizador de Olá do arquivo e um token de Olá stash por isso não terá tooask-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="43486-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="43486-148">Olá código anterior entra em qualquer utilizador que pode autenticar o servidor de tooyour.</span><span class="sxs-lookup"><span data-stu-id="43486-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="43486-149">Isto é conhecido como registo automático.</span><span class="sxs-lookup"><span data-stu-id="43486-149">This is known as auto-registration.</span></span> <span data-ttu-id="43486-150">Num servidor de produção, que não pretende toolet qualquer pessoa sem primeiro passá-los através de um processo de registo que escolher.</span><span class="sxs-lookup"><span data-stu-id="43486-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="43486-151">Isto é normalmente padrão Olá que veem nas aplicações de consumidor.</span><span class="sxs-lookup"><span data-stu-id="43486-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="43486-152">aplicação Olá pode permitir-lhe tooregister com o Facebook, mas, em seguida, este pede-lhe tooenter obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="43486-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="43486-153">Se não utilizar um programa da linha de comandos para este tutorial, foi possível extrair o e-mail Olá do objeto token Olá que é devolvido.</span><span class="sxs-lookup"><span data-stu-id="43486-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="43486-154">Em seguida, poderá pedir-lhe as informações de Olá utilizador tooenter adicionais.</span><span class="sxs-lookup"><span data-stu-id="43486-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="43486-155">Porque se trata de um servidor de teste, adicione o utilizador Olá diretamente toohello dentro da memória base de dados.</span><span class="sxs-lookup"><span data-stu-id="43486-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="43486-156">Adicione os métodos de Olá que utilize tookeep controlar de utilizadores tem sessão iniciada, conforme requerido pelo Passport.</span><span class="sxs-lookup"><span data-stu-id="43486-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="43486-157">Isto inclui informações do utilizador Olá de serialização e:</span><span class="sxs-lookup"><span data-stu-id="43486-157">This includes serializing and deserializing hello user's information:</span></span>

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

5.  <span data-ttu-id="43486-158">Adicione o código de Olá que carrega o motor de Express de Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="43486-159">Utilizar Olá predefinido /views e padrão de /routes Express fornece:</span><span class="sxs-lookup"><span data-stu-id="43486-159">You use hello default /views and /routes pattern that Express provides:</span></span>

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

6.  <span data-ttu-id="43486-160">Adicionar Olá POST encaminha esse mão desativar Olá real pedidos de início de sessão toohello `passport-azure-ad` motor:</span><span class="sxs-lookup"><span data-stu-id="43486-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="43486-161">4: utilizar o Passport tooissue início de sessão e fim de sessão pedidos tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="43486-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="43486-162">A aplicação está agora configurada toocommunicate com o ponto final de v 2.0 Olá através do protocolo de autenticação OpenID Connect Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="43486-163">Olá `passport-azure-ad` estratégia encarrega-se de todos os detalhes de Olá de mensagens de autenticação de composição, tokens de validação do Azure AD e manutenção de sessão do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="43486-164">Tudo o que for deixado toodo é toogive aos utilizadores uma forma toosign no e início de sessão fora e toogather mais informações sobre o utilizador Olá que tenha sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="43486-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="43486-165">Adicionar Olá **predefinido**, **início de sessão**, **conta**, e **terminar** ficheiro de App.js tooyour métodos:</span><span class="sxs-lookup"><span data-stu-id="43486-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

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

  <span data-ttu-id="43486-166">Seguem-se detalhes Olá:</span><span class="sxs-lookup"><span data-stu-id="43486-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="43486-167">Olá `/` rota redireciona toohello index.ejs vista.</span><span class="sxs-lookup"><span data-stu-id="43486-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="43486-168">Transmite os utilizador Olá no pedido de Olá (se existir).</span><span class="sxs-lookup"><span data-stu-id="43486-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="43486-169">Olá `/account` encaminhar primeiro *garante que sejam autenticados* (implementar que no Olá código a seguir).</span><span class="sxs-lookup"><span data-stu-id="43486-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="43486-170">Em seguida, transmite utilizador Olá no pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="43486-171">Isto é, pelo que pode obter mais informações sobre o utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="43486-172">Olá `/login` encaminhar chamadas a `azuread-openidconnect` autenticador de `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="43486-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="43486-173">Se o que não for bem sucedido, será redirecionado novamente a utilizador Olá demasiado`/login`.</span><span class="sxs-lookup"><span data-stu-id="43486-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="43486-174">Olá `/logout` rota chama Olá logout.ejs vista (e rota).</span><span class="sxs-lookup"><span data-stu-id="43486-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="43486-175">Isto limpa cookies e, em seguida, devolve Olá tooindex.ejs back do utilizador.</span><span class="sxs-lookup"><span data-stu-id="43486-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="43486-176">Adicionar Olá **EnsureAuthenticated** método que utilizou anteriormente no `/account`:</span><span class="sxs-lookup"><span data-stu-id="43486-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

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

3.  <span data-ttu-id="43486-177">Crie App.js, servidor Olá:</span><span class="sxs-lookup"><span data-stu-id="43486-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="43486-178">5: criar Olá vistas e rotas no Express que mostram o utilizador no Web site de Olá</span><span class="sxs-lookup"><span data-stu-id="43486-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="43486-179">Adicione rotas Olá e vistas que apresentam o utilizador de toohello de informações.</span><span class="sxs-lookup"><span data-stu-id="43486-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="43486-180">Olá rotas e vistas também processam Olá `/logout` e `/login` rotas que criou.</span><span class="sxs-lookup"><span data-stu-id="43486-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="43486-181">No diretório de raiz de Olá, criar Olá `/routes/index.js` rota.</span><span class="sxs-lookup"><span data-stu-id="43486-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="43486-182">No diretório de raiz de Olá, criar Olá `/routes/user.js` rota.</span><span class="sxs-lookup"><span data-stu-id="43486-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="43486-183">`/routes/index.js`e `/routes/user.js` são rotas simples transferem Olá pedido tooyour das vistas, incluindo utilizador Olá, se estiver presente.</span><span class="sxs-lookup"><span data-stu-id="43486-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="43486-184">No diretório de raiz de Olá, criar Olá `/views/index.ejs` vista.</span><span class="sxs-lookup"><span data-stu-id="43486-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="43486-185">Esta página chama o **início de sessão** e **terminar** métodos.</span><span class="sxs-lookup"><span data-stu-id="43486-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="43486-186">Também é utilizar Olá `/views/index.ejs` ver informações de conta toocapture.</span><span class="sxs-lookup"><span data-stu-id="43486-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="43486-187">Pode utilizar Olá condicional `if (!user)` como utilizador Olá que está a ser transferido no pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="43486-188">É uma prova que tem um utilizador com sessão iniciado.</span><span class="sxs-lookup"><span data-stu-id="43486-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="43486-189">No diretório de raiz de Olá, criar Olá `/views/account.ejs` vista.</span><span class="sxs-lookup"><span data-stu-id="43486-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="43486-190">Olá `/views/account.ejs` vista permite-lhe tooview obter informações adicionais que `passport-azuread` coloca no pedido do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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

5.  <span data-ttu-id="43486-191">Adicione um esquema.</span><span class="sxs-lookup"><span data-stu-id="43486-191">Add a layout.</span></span> <span data-ttu-id="43486-192">No diretório de raiz de Olá, criar Olá `/views/layout.ejs` vista.</span><span class="sxs-lookup"><span data-stu-id="43486-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="43486-193">toobuild e executar a aplicação, executar `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="43486-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="43486-194">Em seguida, aceda demasiado`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="43486-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="43486-195">Inicie sessão com uma conta Microsoft pessoal ou uma conta escolar ou profissional.</span><span class="sxs-lookup"><span data-stu-id="43486-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="43486-196">Tenha em atenção que a identidade do utilizador Olá é refletida na lista de /account Olá.</span><span class="sxs-lookup"><span data-stu-id="43486-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="43486-197">Tem agora uma aplicação web que está protegida pela utilização de protocolos padrão da indústria.</span><span class="sxs-lookup"><span data-stu-id="43486-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="43486-198">Pode autenticar utilizadores na sua aplicação através das respetivas contas pessoais, profissionais ou escolares.</span><span class="sxs-lookup"><span data-stu-id="43486-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43486-199">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="43486-199">Next steps</span></span>
<span data-ttu-id="43486-200">Para referência, o exemplo de Olá concluído (sem os valores de configuração) é fornecido tal como [um ficheiro. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="43486-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="43486-201">Também pode cloná-lo a partir do GitHub:</span><span class="sxs-lookup"><span data-stu-id="43486-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="43486-202">Em seguida, pode passar toomore avançadas tópicos.</span><span class="sxs-lookup"><span data-stu-id="43486-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="43486-203">Poderá querer tootry:</span><span class="sxs-lookup"><span data-stu-id="43486-203">You might want tootry:</span></span>

[<span data-ttu-id="43486-204">Proteger uma API web do Node.js utilizando o ponto final de v 2.0 Olá</span><span class="sxs-lookup"><span data-stu-id="43486-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="43486-205">Seguem-se alguns recursos adicionais:</span><span class="sxs-lookup"><span data-stu-id="43486-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="43486-206">Guia para programadores do Azure AD v 2.0</span><span class="sxs-lookup"><span data-stu-id="43486-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="43486-207">Etiqueta de "azure-active-directory" capacidade excedida da pilha</span><span class="sxs-lookup"><span data-stu-id="43486-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="43486-208">Obter atualizações de segurança dos nossos produtos</span><span class="sxs-lookup"><span data-stu-id="43486-208">Get security updates for our products</span></span>
<span data-ttu-id="43486-209">Aconselhamo-toosign segurança toobe notificado quando ocorrem incidentes de segurança.</span><span class="sxs-lookup"><span data-stu-id="43486-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="43486-210">No Olá [as notificações de segurança técnica Microsoft](https://technet.microsoft.com/security/dd252948) página, tooSecurity Advisories alertas de subscrição.</span><span class="sxs-lookup"><span data-stu-id="43486-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

