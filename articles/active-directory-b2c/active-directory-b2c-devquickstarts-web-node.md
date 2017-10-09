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
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="884ad-103">O Azure AD B2C: Adicionar início de sessão tooa aplicação de web de Node.js</span><span class="sxs-lookup"><span data-stu-id="884ad-103">Azure AD B2C: Add sign-in tooa Node.js web app</span></span>

<span data-ttu-id="884ad-104">**Passport** é o middleware de autenticação do Node.js.</span><span class="sxs-lookup"><span data-stu-id="884ad-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="884ad-105">Extremamente flexível e modular, o Passport pode ser instalado discretamente em qualquer aplicação Web baseada em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="884ad-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="884ad-106">Um conjunto abrangente de estratégias suporta a autenticação utilizando um nome de utilizador e palavra-passe, o Facebook, o Twitter e muito mais.</span><span class="sxs-lookup"><span data-stu-id="884ad-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="884ad-107">Desenvolvemos uma estratégia para o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="884ad-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="884ad-108">Instalará este módulo e, em seguida, adicionar Olá do Azure AD `passport-azure-ad` Plug-in.</span><span class="sxs-lookup"><span data-stu-id="884ad-108">You will install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="884ad-109">toodo, tem de:</span><span class="sxs-lookup"><span data-stu-id="884ad-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="884ad-110">Registar uma aplicação utilizando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="884ad-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="884ad-111">Configurar a sua Olá de toouse aplicação `passport-azure-ad` Plug-in.</span><span class="sxs-lookup"><span data-stu-id="884ad-111">Set up your app toouse hello `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="884ad-112">Utilize Passport tooissue início de sessão e fim de sessão pedidos tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="884ad-112">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="884ad-113">Imprimir os dados de utilizador.</span><span class="sxs-lookup"><span data-stu-id="884ad-113">Print user data.</span></span>

<span data-ttu-id="884ad-114">Olá código para este tutorial [é mantido no GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="884ad-114">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="884ad-115">toofollow ao longo, pode [transferir a estrutura da aplicação de Olá como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="884ad-115">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="884ad-116">Também pode clonar a estrutura de Olá:</span><span class="sxs-lookup"><span data-stu-id="884ad-116">You can also clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="884ad-117">aplicação Olá concluída é fornecida no final deste tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-117">hello completed application is provided at hello end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="884ad-118">Obter um diretório do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="884ad-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="884ad-119">Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.</span><span class="sxs-lookup"><span data-stu-id="884ad-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="884ad-120">Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="884ad-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="884ad-121">Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="884ad-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="884ad-122">Criar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="884ad-122">Create an application</span></span>

<span data-ttu-id="884ad-123">Em seguida, terá de toocreate uma aplicação no diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="884ad-123">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="884ad-124">Isto dá-informações do Azure AD que necessita de toocommunicate em segurança com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="884ad-124">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="884ad-125">Olá ambas as aplicações cliente e a web API será representada por um único **ID da aplicação**, uma vez que compõem uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="884ad-125">Both hello client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="884ad-126">toocreate uma aplicação, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="884ad-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="884ad-127">É necessário:</span><span class="sxs-lookup"><span data-stu-id="884ad-127">Be sure to:</span></span>

- <span data-ttu-id="884ad-128">Incluir um **aplicação web**/**web API** na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-128">Include a **web app**/**web API** in hello application.</span></span>
- <span data-ttu-id="884ad-129">Introduzir `http://localhost:3000/auth/openid/return` como um **URL de resposta**.</span><span class="sxs-lookup"><span data-stu-id="884ad-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="884ad-130">É Olá predefinido URL para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="884ad-130">It is hello default URL for this code sample.</span></span>
- <span data-ttu-id="884ad-131">Criar um **Segredo de aplicação** para a aplicação e copiá-lo.</span><span class="sxs-lookup"><span data-stu-id="884ad-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="884ad-132">Precisará dele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="884ad-132">You will need it later.</span></span> <span data-ttu-id="884ad-133">Tenha em atenção que este valor tem de toobe [XML de escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de o utilizar.</span><span class="sxs-lookup"><span data-stu-id="884ad-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="884ad-134">Olá cópia **ID da aplicação** que é atribuído tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="884ad-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="884ad-135">Também irá precisar deste mais tarde.</span><span class="sxs-lookup"><span data-stu-id="884ad-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="884ad-136">Criar as políticas</span><span class="sxs-lookup"><span data-stu-id="884ad-136">Create your policies</span></span>

<span data-ttu-id="884ad-137">No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="884ad-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="884ad-138">Esta aplicação contém três experiências de identidade: inscrição, início de sessão e início de sessão utilizando o Facebook.</span><span class="sxs-lookup"><span data-stu-id="884ad-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="884ad-139">Terá de toocreate esta política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="884ad-139">You need toocreate this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="884ad-140">Quando criar as três políticas, não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="884ad-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="884ad-141">Escolha Olá **nome a apresentar** e outros atributos de inscrição na política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="884ad-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="884ad-142">Escolha Olá **nome a apresentar** e **ID de objeto** afirmações de aplicação em cada política.</span><span class="sxs-lookup"><span data-stu-id="884ad-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="884ad-143">Também pode escolher outras afirmações.</span><span class="sxs-lookup"><span data-stu-id="884ad-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="884ad-144">Olá cópia **nome** de cada política depois de a criar.</span><span class="sxs-lookup"><span data-stu-id="884ad-144">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="884ad-145">Deve ter o prefixo de Olá `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="884ad-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="884ad-146">Precisará destes nomes de políticas mais tarde.</span><span class="sxs-lookup"><span data-stu-id="884ad-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="884ad-147">Depois de criar as três políticas, está pronto toobuild a aplicação.</span><span class="sxs-lookup"><span data-stu-id="884ad-147">After you create your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="884ad-148">Tenha em atenção que este artigo não abrange como as políticas de Olá toouse que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="884ad-148">Note that this article does not cover how toouse hello policies you just created.</span></span> <span data-ttu-id="884ad-149">toolearn sobre como funcionam as políticas no Azure AD B2C, comece com Olá [.NET introdução à aplicação web tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="884ad-149">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-tooyour-directory"></a><span data-ttu-id="884ad-150">Adicionar pré-requisitos tooyour diretório</span><span class="sxs-lookup"><span data-stu-id="884ad-150">Add prerequisites tooyour directory</span></span>

<span data-ttu-id="884ad-151">Olá linha de comandos, altere a pasta de raiz tooyour diretórios, se não estiver já existe.</span><span class="sxs-lookup"><span data-stu-id="884ad-151">From hello command line, change directories tooyour root folder, if you're not already there.</span></span> <span data-ttu-id="884ad-152">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="884ad-152">Run hello following commands:</span></span>

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

<span data-ttu-id="884ad-153">Além disso, utilizámos `passport-azure-ad` para a nossa pré-visualização na estrutura de Olá de Olá início rápido.</span><span class="sxs-lookup"><span data-stu-id="884ad-153">In addition, we used `passport-azure-ad` for our preview in hello skeleton of hello Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="884ad-154">Esta ação instalará bibliotecas Olá que `passport-azure-ad` depende.</span><span class="sxs-lookup"><span data-stu-id="884ad-154">This will install hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a><span data-ttu-id="884ad-155">Configurar a sua Olá toouse de aplicação estratégia Passport-node.js</span><span class="sxs-lookup"><span data-stu-id="884ad-155">Set up your app toouse hello Passport-Node.js strategy</span></span>
<span data-ttu-id="884ad-156">Configure Olá do Olá rápida middleware toouse protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="884ad-156">Configure hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="884ad-157">O Passport será utilizado tooissue pedidos de início de sessão e fim de sessão, gerir sessões de utilizador e obter informações sobre utilizadores, entre outras ações.</span><span class="sxs-lookup"><span data-stu-id="884ad-157">Passport will be used tooissue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="884ad-158">Abra Olá `config.js` ficheiro na raiz de Olá do projeto de Olá e introduza os valores de configuração da sua aplicação no Olá `exports.creds` secção.</span><span class="sxs-lookup"><span data-stu-id="884ad-158">Open hello `config.js` file in hello root of hello project and enter your app's configuration values in hello `exports.creds` section.</span></span>
- <span data-ttu-id="884ad-159">`clientID`: Olá **ID da aplicação** atribuído tooyour aplicação no portal de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-159">`clientID`: hello **Application ID** assigned tooyour app in hello registration portal.</span></span>
- <span data-ttu-id="884ad-160">`returnURL`: Olá **URI de redirecionamento** que introduziu no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-160">`returnURL`: hello **Redirect URI** you entered in hello portal.</span></span>
- <span data-ttu-id="884ad-161">`tenantName`: nome do inquilino Olá da sua aplicação, por exemplo, **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="884ad-161">`tenantName`: hello tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="884ad-162">Abra Olá `app.js` ficheiro na raiz de Olá do projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-162">Open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="884ad-163">Adicionar Olá seguir chamada tooinvoke Olá `OIDCStrategy` estratégia que vem com `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="884ad-163">Add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="884ad-164">Utilize a estratégia de Olá acabou de referenciar pedidos de início de sessão toohandle.</span><span class="sxs-lookup"><span data-stu-id="884ad-164">Use hello strategy you just referenced toohandle sign-in requests.</span></span>

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
<span data-ttu-id="884ad-165">O Passport utiliza um padrão semelhante para todos as respetivas estratégias (incluindo o Twitter e o Facebook).</span><span class="sxs-lookup"><span data-stu-id="884ad-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="884ad-166">Todos os escritores aderem toothis padrão.</span><span class="sxs-lookup"><span data-stu-id="884ad-166">All strategy writers adhere toothis pattern.</span></span> <span data-ttu-id="884ad-167">Quando observa a estratégia de Olá, pode ver que transmite um `function()` que tem um token e um `done` como parâmetros de Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-167">When you look at hello strategy, you can see that you pass it a `function()` that has a token and a `done` as hello parameters.</span></span> <span data-ttu-id="884ad-168">estratégia de Olá volta a tooyou depois-tem de fazer todo o trabalho.</span><span class="sxs-lookup"><span data-stu-id="884ad-168">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="884ad-169">Armazene o utilizador Olá e guarde o token de Olá, de modo que não seja necessário tooask-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="884ad-169">Store hello user and stash hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="884ad-170">Olá código anterior entra em todos os utilizadores a quem Olá servidor autentica.</span><span class="sxs-lookup"><span data-stu-id="884ad-170">hello preceding code takes all users whom hello server authenticates.</span></span> <span data-ttu-id="884ad-171">Este é registo automático.</span><span class="sxs-lookup"><span data-stu-id="884ad-171">This is autoregistration.</span></span> <span data-ttu-id="884ad-172">Quando utiliza servidores de produção, que não pretende toolet sessão dos utilizadores, a menos que tenham passado por um processo de registo que configurou.</span><span class="sxs-lookup"><span data-stu-id="884ad-172">When you use production servers, you don’t want toolet in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="884ad-173">Muitas vezes, pode ver este padrão nas aplicações de consumidor.</span><span class="sxs-lookup"><span data-stu-id="884ad-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="884ad-174">Estas permitem-lhe tooregister utilizando o Facebook, mas, em seguida, solicitam-lhe toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="884ad-174">These allow you tooregister by using Facebook, but then they ask you toofill out additional information.</span></span> <span data-ttu-id="884ad-175">Se a nossa aplicação não era uma amostra, iremos foi extrair um endereço de e-mail do objeto token Olá que é devolvido e, em seguida, peça ao Olá utilizador toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="884ad-175">If our application wasn’t a sample, we could extract an email address from hello token object that is returned, and then ask hello user toofill out additional information.</span></span> <span data-ttu-id="884ad-176">Porque se trata de um servidor de teste, adicionamos simplesmente utilizadores toohello dentro da memória da base de dados.</span><span class="sxs-lookup"><span data-stu-id="884ad-176">Because this is a test server, we simply add users toohello in-memory database.</span></span>

<span data-ttu-id="884ad-177">Adicionar métodos de Olá que lhe permitem controlar tookeep de utilizadores que tenham iniciado sessão, conforme requerido pelo Passport.</span><span class="sxs-lookup"><span data-stu-id="884ad-177">Add hello methods that allow you tookeep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="884ad-178">Isto inclui informações de utilizador de serialização e não serialização:</span><span class="sxs-lookup"><span data-stu-id="884ad-178">This includes serializing and deserializing user information:</span></span>

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

<span data-ttu-id="884ad-179">Adicione o motor do Olá código tooload Olá Express.</span><span class="sxs-lookup"><span data-stu-id="884ad-179">Add hello code tooload hello Express engine.</span></span> <span data-ttu-id="884ad-180">No seguinte Olá, pode ver que utilizamos a predefinição de Olá `/views` e `/routes` padrão que o Express fornece.</span><span class="sxs-lookup"><span data-stu-id="884ad-180">In hello following, you can see that we use hello default `/views` and `/routes` pattern that Express provides.</span></span>

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

<span data-ttu-id="884ad-181">Adicionar Olá `POST` Olá de rotas que entregam os pedidos de início de sessão real toohello `passport-azure-ad` motor:</span><span class="sxs-lookup"><span data-stu-id="884ad-181">Add hello `POST` routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="884ad-182">Utilizar Passport tooissue início de sessão e fim de sessão pedidos tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="884ad-182">Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>

<span data-ttu-id="884ad-183">A aplicação está agora toocommunicate configurado corretamente com o ponto final de v 2.0 Olá através do protocolo de autenticação OpenID Connect Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-183">Your app is now properly configured toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="884ad-184">`passport-azure-ad`tem Tratado dos detalhes de Olá de mensagens de autenticação de composição, tokens de validação do Azure AD e manutenção de sessão do utilizador.</span><span class="sxs-lookup"><span data-stu-id="884ad-184">`passport-azure-ad` has taken care of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="884ad-185">Tudo o que resta é toogive os seus utilizadores uma forma toosign no e início de sessão fora e toogather informações adicionais sobre os utilizadores que têm sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="884ad-185">All that remains is toogive your users a way toosign in and sign out, and toogather additional information on users who have signed in.</span></span>

<span data-ttu-id="884ad-186">Primeiro, adicione Olá predefinição, início de sessão, conta e fim de sessão métodos tooyour `app.js` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="884ad-186">First, add hello default, sign-in, account, and sign-out methods tooyour `app.js` file:</span></span>

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

<span data-ttu-id="884ad-187">tooreview estes métodos em detalhe:</span><span class="sxs-lookup"><span data-stu-id="884ad-187">tooreview these methods in detail:</span></span>
- <span data-ttu-id="884ad-188">Olá `/` rota redireciona toohello `index.ejs` vista transferindo o utilizador Olá no pedido de Olá (se existir).</span><span class="sxs-lookup"><span data-stu-id="884ad-188">hello `/` route redirects toohello `index.ejs` view by passing hello user in hello request (if it exists).</span></span>
- <span data-ttu-id="884ad-189">Olá `/account` rota verifica primeiro se está autenticado (Olá implementação para esta situação é abaixo).</span><span class="sxs-lookup"><span data-stu-id="884ad-189">hello `/account` route first verifies that you are authenticated (hello implementation for this is below).</span></span> <span data-ttu-id="884ad-190">-Lo, em seguida, transmite utilizador Olá no pedido de Olá, de modo a que pode obter informações adicionais sobre o utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-190">It then passes hello user in hello request so that you can get additional information about hello user.</span></span>
- <span data-ttu-id="884ad-191">Olá `/login` rota chamadas Olá `azuread-openidconnect` autenticador de `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="884ad-191">hello `/login` route calls hello `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="884ad-192">Se não for bem-sucedida, rota Olá redireciona volta a utilizador Olá demasiado`/login`.</span><span class="sxs-lookup"><span data-stu-id="884ad-192">If it doesn't succeed, hello route redirects hello user back too`/login`.</span></span>
- <span data-ttu-id="884ad-193">`logout.ejs` chama simplesmente `/logout` (e a respetiva rota).</span><span class="sxs-lookup"><span data-stu-id="884ad-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="884ad-194">Isto limpa cookies e, em seguida, devolve Olá utilizador volta demasiado`index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="884ad-194">This clears cookies and then returns hello user back too`index.ejs`.</span></span>


<span data-ttu-id="884ad-195">Para Olá última parte `app.js`, adicionar Olá `EnsureAuthenticated` método que é utilizado no Olá `/account` rota.</span><span class="sxs-lookup"><span data-stu-id="884ad-195">For hello last part of `app.js`, add hello `EnsureAuthenticated` method that is used in hello `/account` route.</span></span>

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

<span data-ttu-id="884ad-196">Por fim, crie o próprio servidor de Olá no `app.js`.</span><span class="sxs-lookup"><span data-stu-id="884ad-196">Finally, create hello server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a><span data-ttu-id="884ad-197">Criar Olá vistas e rotas no Express toocall as políticas</span><span class="sxs-lookup"><span data-stu-id="884ad-197">Create hello views and routes in Express toocall your policies</span></span>

<span data-ttu-id="884ad-198">O `app.js` está agora concluído.</span><span class="sxs-lookup"><span data-stu-id="884ad-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="884ad-199">Basta rotas de Olá tooadd e vistas que lhe permitem toocall Olá início de sessão e inscrição as políticas.</span><span class="sxs-lookup"><span data-stu-id="884ad-199">You just need tooadd hello routes and views that allow you toocall hello sign-in and sign-up policies.</span></span> <span data-ttu-id="884ad-200">Estas também processar Olá `/logout` e `/login` rotas que criou.</span><span class="sxs-lookup"><span data-stu-id="884ad-200">These also handle hello `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="884ad-201">Criar Olá `/routes/index.js` rota no diretório de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-201">Create hello `/routes/index.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="884ad-202">Criar Olá `/routes/user.js` rota no diretório de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-202">Create hello `/routes/user.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="884ad-203">Estas rotas simples transferem vistas de tooyour de pedidos.</span><span class="sxs-lookup"><span data-stu-id="884ad-203">These simple routes pass along requests tooyour views.</span></span> <span data-ttu-id="884ad-204">Incluem utilizador Olá, se estiver presente.</span><span class="sxs-lookup"><span data-stu-id="884ad-204">They include hello user, if one is present.</span></span>

<span data-ttu-id="884ad-205">Criar Olá `/views/index.ejs` vista no diretório de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-205">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="884ad-206">Esta é uma página simples que chama as políticas para o início de sessão e fim de sessão. Também pode utilizá-la toograb informações da conta.</span><span class="sxs-lookup"><span data-stu-id="884ad-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it toograb account information.</span></span> <span data-ttu-id="884ad-207">Tenha em atenção que pode utilizar Olá condicional `if (!user)` como utilizador Olá é transferido no pedido de Olá tooprovide evidence esse utilizador Olá tem sessão iniciado.</span><span class="sxs-lookup"><span data-stu-id="884ad-207">Note that you can use hello conditional `if (!user)` as hello user is passed through in hello request tooprovide evidence that hello user is signed in.</span></span>

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

<span data-ttu-id="884ad-208">Criar Olá `/views/account.ejs` ver no diretório de raiz de Olá, para que possa visualizar informações adicionais que `passport-azure-ad` colocar no pedido do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="884ad-208">Create hello `/views/account.ejs` view under hello root directory so that you can view additional information that `passport-azure-ad` put in hello user request.</span></span>

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

<span data-ttu-id="884ad-209">Agora pode criar e executar a aplicação.</span><span class="sxs-lookup"><span data-stu-id="884ad-209">You can now build and run your app.</span></span>

<span data-ttu-id="884ad-210">Executar `node app.js` e navegue demasiado`http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="884ad-210">Run `node app.js` and navigate too`http://localhost:3000`</span></span>


<span data-ttu-id="884ad-211">Inscrever-se ou iniciar sessão na aplicação toohello através de e-mail ou o Facebook.</span><span class="sxs-lookup"><span data-stu-id="884ad-211">Sign up or sign in toohello app by using email or Facebook.</span></span> <span data-ttu-id="884ad-212">Termine sessão e inicie sessão novamente como um utilizador diferente.</span><span class="sxs-lookup"><span data-stu-id="884ad-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="884ad-213">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="884ad-213">Next steps</span></span>

<span data-ttu-id="884ad-214">Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="884ad-214">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="884ad-215">Também pode clonar a partir do GitHub:</span><span class="sxs-lookup"><span data-stu-id="884ad-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="884ad-216">Agora pode passar toomore avançadas tópicos.</span><span class="sxs-lookup"><span data-stu-id="884ad-216">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="884ad-217">Pode experimentar:</span><span class="sxs-lookup"><span data-stu-id="884ad-217">You might try:</span></span>

[<span data-ttu-id="884ad-218">Proteger uma API web utilizando o modelo de Olá B2C no Node.js</span><span class="sxs-lookup"><span data-stu-id="884ad-218">Secure a web API by using hello B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
