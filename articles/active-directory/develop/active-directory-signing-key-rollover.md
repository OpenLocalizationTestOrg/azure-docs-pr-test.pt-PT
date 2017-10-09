---
title: aaaSigning Rollover de chave no Azure AD | Microsoft Docs
description: "Este artigo aborda Olá melhores práticas de rollover de chave de assinatura para o Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="047fb-103">Iniciar o rollover da chave no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="047fb-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="047fb-104">Este tópico descreve o que precisa de tooknow sobre as chaves públicas Olá que são utilizados em tokens de segurança do Azure Active Directory (Azure AD) toosign.</span><span class="sxs-lookup"><span data-stu-id="047fb-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="047fb-105">É importante toonote que estes rollover de chaves periodicamente e, numa emergência, pode ser feito imediatamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="047fb-106">Todas as aplicações que utilizam o Azure AD devem ser capaz de tooprogrammatically identificador Olá rollover de chave processo ou estabelecer um processo manual de rollover periódica.</span><span class="sxs-lookup"><span data-stu-id="047fb-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="047fb-107">Continuar a ler toounderstand como chaves Olá funcionem, como tooassess Olá impacto da aplicação do Olá rollover tooyour e como tooupdate a aplicação ou estabelecer um rollover manual periódica processo toohandle rollover da chave, se necessário.</span><span class="sxs-lookup"><span data-stu-id="047fb-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="047fb-108">Descrição geral das chaves de assinatura no Azure AD</span><span class="sxs-lookup"><span data-stu-id="047fb-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="047fb-109">Azure AD utiliza a criptografia de chave pública criada numa confiança de tooestablish normas da indústria entre si próprio e Olá aplicações que a utilizam.</span><span class="sxs-lookup"><span data-stu-id="047fb-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="047fb-110">Em termos práticos, este procedimento funciona em Olá seguinte forma: AD do Azure utiliza uma chave de assinatura que é composta por um par de chaves público e privado.</span><span class="sxs-lookup"><span data-stu-id="047fb-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="047fb-111">Quando um utilizador inicia sessão na aplicação tooan que utiliza o Azure AD para autenticação, o Azure AD cria um token de segurança que contenha informações sobre Olá utilizador.</span><span class="sxs-lookup"><span data-stu-id="047fb-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="047fb-112">Este token é assinada pelo Azure AD utilizando a respetiva chave privada antes de ser enviada back toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="047fb-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="047fb-113">tooverify Olá token é válido e, na verdade, teve origem do Azure AD, a aplicação Olá necessário validar a assinatura do token de Olá utilizando a chave pública Olá exposto pelo Azure AD que está contido no inquilino Olá [OpenID Connect documento de identificação](http://openid.net/specs/openid-connect-discovery-1_0.html) ou SAML/WS-Fed [documento de metadados de Federação](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="047fb-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="047fb-114">Por motivos de segurança, do Azure AD assinatura faz chave periodicamente e, em caso de Olá de emergência, pode ser feito imediatamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="047fb-115">Qualquer aplicação que se integra com o Azure AD deve estar preparada toohandle um evento de rollover de chave não é relevante frequência podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="047fb-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="047fb-116">Se não, e a aplicação tenta toouse uma assinatura de Olá expirada tooverify chave num token, Olá início de sessão pedido irá falhar.</span><span class="sxs-lookup"><span data-stu-id="047fb-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="047fb-117">Não há mais do que uma chave válida disponíveis no documento de identificação de OpenID Connect Olá e o documento de metadados de Federação Olá sempre.</span><span class="sxs-lookup"><span data-stu-id="047fb-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="047fb-118">A aplicação deve estar preparada toouse qualquer uma das chaves de Olá especificado no documento de Olá, uma vez que uma chave em breve, poderá ser revertida outro pode ser sua substituição e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="047fb-119">Como tooassess se a sua aplicação será afetada e que toodo sobre o assunto</span><span class="sxs-lookup"><span data-stu-id="047fb-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="047fb-120">Como a aplicação processa o rollover da chave depende de variáveis, como o tipo de Olá de aplicação ou o protocolo de identidade e a biblioteca foi utilizada.</span><span class="sxs-lookup"><span data-stu-id="047fb-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="047fb-121">secções Olá abaixo avaliar se tipos de aplicações mais comuns Olá são afetados por rollover da chave de Olá e fornecem orientações sobre como tooupdate Olá rollover automático da aplicação toosupport ou atualizar manualmente a chave de Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="047fb-122">Aplicações de cliente nativo aceder a recursos</span><span class="sxs-lookup"><span data-stu-id="047fb-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="047fb-123">As aplicações Web / APIs aceder a recursos</span><span class="sxs-lookup"><span data-stu-id="047fb-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="047fb-124">As aplicações Web / APIs proteger os recursos e compilada com serviços de aplicações do Azure</span><span class="sxs-lookup"><span data-stu-id="047fb-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="047fb-125">As aplicações Web / APIs proteger recursos com o .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="047fb-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="047fb-126">As aplicações Web / APIs proteger recursos com o middleware .NET Core OpenID Connect ou JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="047fb-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="047fb-127">As aplicações Web / APIs proteger recursos com o módulo de passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="047fb-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="047fb-128">As aplicações Web / APIs proteger os recursos e criados com o Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="047fb-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="047fb-129">Aplicações Web de proteger os recursos e criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="047fb-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="047fb-130">APIs da Web proteger os recursos e criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="047fb-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="047fb-131">Aplicações Web de proteger os recursos e criados com o Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="047fb-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="047fb-132">Aplicações Web de proteger os recursos e criados com o Visual Studio 2010, o 2008 utilizando o Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="047fb-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="047fb-133">As aplicações Web / APIs proteger os recursos a utilizar quaisquer outras bibliotecas de manualmente implementar qualquer um dos Olá suportados ou protocolos</span><span class="sxs-lookup"><span data-stu-id="047fb-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="047fb-134">Esta orientação é **não** aplicável para:</span><span class="sxs-lookup"><span data-stu-id="047fb-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="047fb-135">As aplicações adicionadas a partir da Galeria de aplicações do Azure do AD (incluindo personalizada) ter orientações separada com que diz respeito toosigning chaves.</span><span class="sxs-lookup"><span data-stu-id="047fb-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="047fb-136">Obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="047fb-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="047fb-137">No local as aplicações publicadas através do proxy da aplicação não tem tooworry sobre chaves de assinatura.</span><span class="sxs-lookup"><span data-stu-id="047fb-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="047fb-138"><a name="nativeclient"></a>Aplicações de cliente nativo aceder a recursos</span><span class="sxs-lookup"><span data-stu-id="047fb-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="047fb-139">Aplicações que só estão a aceder a recursos (revertidos</span><span class="sxs-lookup"><span data-stu-id="047fb-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="047fb-140">Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft), geralmente, apenas obter um token e transferem-o ao longo do proprietário do recurso toohello.</span><span class="sxs-lookup"><span data-stu-id="047fb-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="047fb-141">Uma vez que estes não estiver a proteger os recursos, estes não inspecionar o token de Olá e, por conseguinte, é necessário tooensure que estejam corretamente assinados.</span><span class="sxs-lookup"><span data-stu-id="047fb-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="047fb-142">As aplicações cliente nativo, se o ambiente de trabalho ou de dispositivo móvel, inseridas nesta categoria e, por conseguinte, que não são afetadas por rollover Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="047fb-143"><a name="webclient"></a>As aplicações Web / APIs aceder a recursos</span><span class="sxs-lookup"><span data-stu-id="047fb-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="047fb-144">Aplicações que só estão a aceder a recursos (revertidos</span><span class="sxs-lookup"><span data-stu-id="047fb-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="047fb-145">Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft), geralmente, apenas obter um token e transferem-o ao longo do proprietário do recurso toohello.</span><span class="sxs-lookup"><span data-stu-id="047fb-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="047fb-146">Uma vez que estes não estiver a proteger os recursos, estes não inspecionar o token de Olá e, por conseguinte, é necessário tooensure que estejam corretamente assinados.</span><span class="sxs-lookup"><span data-stu-id="047fb-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="047fb-147">As aplicações Web e APIs que estão a utilizar o fluxo de Olá só de aplicação web (credenciais de cliente / certificado de cliente), inseridas nesta categoria e, por conseguinte, que não são afetadas por rollover Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="047fb-148"><a name="appservices"></a>As aplicações Web / APIs proteger os recursos e compilada com serviços de aplicações do Azure</span><span class="sxs-lookup"><span data-stu-id="047fb-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="047fb-149">A autenticação dos serviços aplicacionais Azure / funcionalidade de autorização (EasyAuth) já Olá lógica necessária às toohandle rollover da chave de automaticamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="047fb-150"><a name="owin"></a>As aplicações Web / APIs proteger recursos com o .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication middleware</span><span class="sxs-lookup"><span data-stu-id="047fb-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="047fb-151">Se a aplicação estiver a utilizar Olá .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication middleware, já tem Olá lógica necessária às toohandle rollover da chave de automaticamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="047fb-152">Pode confirmar que a aplicação está a utilizar qualquer um destes procurando qualquer um dos seguintes fragmentos na sua aplicação Startup.cs ou Startup.Auth.cs de Olá</span><span class="sxs-lookup"><span data-stu-id="047fb-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="047fb-153"><a name="owincore"></a>As aplicações Web / APIs proteger recursos com o middleware .NET Core OpenID Connect ou JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="047fb-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="047fb-154">Se a sua aplicação utilizar Olá .NET Core OWIN OpenID Connect ou JwtBearerAuthentication middleware, já tem Olá lógica necessária às toohandle rollover da chave de automaticamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="047fb-155">Pode confirmar que a aplicação está a utilizar qualquer um destes procurando qualquer um dos seguintes fragmentos na sua aplicação Startup.cs ou Startup.Auth.cs de Olá</span><span class="sxs-lookup"><span data-stu-id="047fb-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="047fb-156"><a name="passport"></a>As aplicações Web / APIs proteger recursos com o módulo de passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="047fb-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="047fb-157">Se a aplicação estiver a utilizar o módulo de passport ad Olá Node.js, já tem Olá lógica necessária às toohandle rollover da chave de automaticamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="047fb-158">Pode confirmar que a aplicação passport-ad procurando Olá seguinte fragmento na app.js sua aplicação</span><span class="sxs-lookup"><span data-stu-id="047fb-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="047fb-159"><a name="vs2015"></a>As aplicações Web / APIs proteger os recursos e criados com o Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="047fb-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="047fb-160">Se a aplicação foi criada utilizando um modelo de aplicação web no Visual Studio 2015 ou Visual Studio 2017 e selecionado **profissional e escolar contas** de Olá **alterar autenticação** menu, já tem o rollover da chave Olá lógica necessária às toohandle automaticamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="047fb-161">Esta lógica, incorporada middleware OWIN OpenID Connect Olá, obtém e coloca em cache Olá as chaves de documento de identificação de OpenID Connect Olá e atualiza periodicamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="047fb-162">Se tiver adicionado manualmente a solução de tooyour de autenticação, a aplicação poderá não ter a lógica de rollover de chave necessário Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="047fb-163">Terá de toowrite-lo por si ou Olá siga os passos em [aplicações Web / APIs utilizar quaisquer outras bibliotecas de ou implementar manualmente a qualquer um dos Olá suportado protocolos.](#other).</span><span class="sxs-lookup"><span data-stu-id="047fb-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="047fb-164"><a name="vs2013"></a>Aplicações Web de proteger os recursos e criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="047fb-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="047fb-165">Se a aplicação foi criada utilizando um modelo de aplicação web no Visual Studio 2013 e selecionado **contas institucionais** de Olá **alterar autenticação** menu, já tem Olá necessário lógica toohandle rollover de chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="047fb-166">Esta lógica armazena o identificador exclusivo da sua organização e Olá nas duas tabelas de base de dados associado projeto Olá informações da chave de assinatura.</span><span class="sxs-lookup"><span data-stu-id="047fb-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="047fb-167">Pode encontrar cadeia de ligação de Olá da base de dados de Olá no ficheiro Web. config do projeto Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="047fb-168">Se tiver adicionado manualmente a solução de tooyour de autenticação, a aplicação poderá não ter a lógica de rollover de chave necessário Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="047fb-169">Terá de toowrite-lo por si ou Olá siga os passos em [aplicações Web / APIs utilizar quaisquer outras bibliotecas de ou implementar manualmente a qualquer um dos Olá suportado protocolos.](#other).</span><span class="sxs-lookup"><span data-stu-id="047fb-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="047fb-170">Olá, os passos seguintes irão ajudá-lo, certifique-se de que o lógica Olá está a funcionar corretamente na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="047fb-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="047fb-171">No Visual Studio 2013, abra a solução de Olá e, em seguida, clique em Olá **Explorador de servidores** separador na janela direita Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="047fb-172">Expanda **ligações de dados**, **DefaultConnection**e, em seguida, **tabelas**.</span><span class="sxs-lookup"><span data-stu-id="047fb-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="047fb-173">Localizar Olá **IssuingAuthorityKeys** tabela, faça duplo clique nele e, em seguida, clique em **Mostrar dados de tabela**.</span><span class="sxs-lookup"><span data-stu-id="047fb-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="047fb-174">No Olá **IssuingAuthorityKeys** tabela, pode haver pelo menos uma linha que corresponde ao valor do thumbprint toohello para a chave de Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="047fb-175">Elimine quaisquer linhas na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="047fb-176">Contexto Olá **inquilinos** tabela e, em seguida, clique em **Mostrar dados de tabela**.</span><span class="sxs-lookup"><span data-stu-id="047fb-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="047fb-177">No Olá **inquilinos** tabela, pode haver pelo menos uma linha que corresponde ao identificador de inquilino do tooa diretório exclusivo.</span><span class="sxs-lookup"><span data-stu-id="047fb-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="047fb-178">Elimine quaisquer linhas na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-178">Delete any rows in hello table.</span></span> <span data-ttu-id="047fb-179">Se não eliminar linhas de Olá em ambos os Olá **inquilinos** tabela e **IssuingAuthorityKeys** tabela, obterá um erro durante a execução.</span><span class="sxs-lookup"><span data-stu-id="047fb-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="047fb-180">Crie e execute a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-180">Build and run hello application.</span></span> <span data-ttu-id="047fb-181">Depois de ter a sessão iniciada numa conta tooyour, pode parar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="047fb-182">Devolver toohello **Explorador de servidores** e observe Olá valores existentes na Olá **IssuingAuthorityKeys** e **inquilinos** tabela.</span><span class="sxs-lookup"><span data-stu-id="047fb-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="047fb-183">Irá notar que tenham sido repovoados automaticamente, com informações adequadas do Olá do documento de metadados de Federação Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="047fb-184"><a name="vs2013"></a>APIs da Web proteger os recursos e criados com o Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="047fb-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="047fb-185">Se criar uma aplicação API da web no Visual Studio 2013 com o modelo de Web API Olá e, em seguida, selecionou **contas institucionais** de Olá **alterar autenticação** menu, já tenham Olá lógica necessária na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="047fb-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="047fb-186">Se tiver configurado manualmente authentication, siga as instruções de Olá abaixo toolearn como tooconfigure tooautomatically sua Web API atualizar as informações de chaves.</span><span class="sxs-lookup"><span data-stu-id="047fb-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="047fb-187">Olá fragmento de código seguinte demonstra como tooget Olá chaves mais recentes do documento de metadados de Federação Olá e, em seguida, utilize Olá [processador Token JWT](https://msdn.microsoft.com/library/dn205065.aspx) token de Olá toovalidate.</span><span class="sxs-lookup"><span data-stu-id="047fb-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="047fb-188">o fragmento de código Olá parte do princípio de que irá utilizar os seus próprios de colocação em cache mecanismo para persistentes toovalidate de chave de Olá futura tokens do Azure AD, se, ser na base de dados, o ficheiro de configuração ou noutro local.</span><span class="sxs-lookup"><span data-stu-id="047fb-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="047fb-189"><a name="vs2012"></a>Aplicações Web de proteger os recursos e criados com o Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="047fb-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="047fb-190">Se a aplicação foi criada no Visual Studio 2012, provavelmente, utilizou Olá identidade e tooconfigure da ferramenta de acesso da aplicação.</span><span class="sxs-lookup"><span data-stu-id="047fb-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="047fb-191">Também é provável que está a utilizar Olá [validar o registo de nome de emissor (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="047fb-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="047fb-192">Olá VINR é responsável pela manutenção informações sobre fornecedores de identidade fidedigna (Azure AD) e as chaves de Olá utilizadas tokens toovalidate emitidos por-los.</span><span class="sxs-lookup"><span data-stu-id="047fb-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="047fb-193">Olá VINR também torna tooautomatically fácil atualização Olá chave informações armazenadas num ficheiro Web. config, transferindo Olá mais recente Federação documento de metadados associado com o seu diretório, a verificar se a configuração de Olá está desatualizada com Olá mais recente documento e atualização Olá aplicação toouse Olá nova chave conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="047fb-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="047fb-194">Se tiver criado a sua aplicação utilizar qualquer um dos exemplos de código Olá ou documentação instruções fornecida pela Microsoft, a lógica de rollover de chave Olá já está incluída no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="047fb-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="047fb-195">Vai notar que o código de Olá abaixo já existe no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="047fb-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="047fb-196">Se a aplicação ainda não tiver esta lógica, siga os passos de Olá abaixo tooadd de-lo e tooverify que está a funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="047fb-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="047fb-197">No **Explorador de soluções**, adicione uma referência toohello **System** assemblagem de projecto adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="047fb-198">Abra Olá **Global.asax.cs** de ficheiros e adicione o seguinte Olá utilizando as diretivas de:</span><span class="sxs-lookup"><span data-stu-id="047fb-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="047fb-199">Adicionar Olá seguinte método toohello **Global.asax.cs** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="047fb-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="047fb-200">Invocar Olá **RefreshValidationSettings()** método Olá **Application_Start()** método **Global.asax.cs** conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="047fb-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="047fb-201">Depois de ter seguido estes passos, será atualizado com informações mais recentes do Olá do documento de metadados de Federação Olá, incluindo chaves mais recentes Olá Web. config da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="047fb-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="047fb-202">Esta atualização irá ocorrer sempre que o conjunto aplicacional recicla no IIS; Por predefinição, IIS está definido toorecycle aplicações cada 29 horas.</span><span class="sxs-lookup"><span data-stu-id="047fb-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="047fb-203">Siga os passos de Olá abaixo tooverify lógica de rollover de chave Olá está a funcionar.</span><span class="sxs-lookup"><span data-stu-id="047fb-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="047fb-204">Depois de ter verificado que a aplicação está a utilizar código Olá acima, abra Olá **Web. config** de ficheiros e navegue toohello  **<issuerNameRegistry>**  bloco, especificamente procura Olá seguir algumas linhas:</span><span class="sxs-lookup"><span data-stu-id="047fb-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="047fb-205">No Olá  **<add thumbprint=””>**  definição, alterar o valor do thumbprint Olá ao substituir qualquer caráter com outro.</span><span class="sxs-lookup"><span data-stu-id="047fb-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="047fb-206">Guardar Olá **Web. config** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="047fb-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="047fb-207">Criar aplicação Olá e volte a executar.</span><span class="sxs-lookup"><span data-stu-id="047fb-207">Build hello application, and then run it.</span></span> <span data-ttu-id="047fb-208">Se pode concluir o processo de início de sessão Olá, a aplicação com êxito é atualizar a chave de Olá transferindo informações Olá necessário do documento de metadados de Federação do diretório.</span><span class="sxs-lookup"><span data-stu-id="047fb-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="047fb-209">Se estiver a ter problemas em iniciar sessão, certifique-se de alterações de Olá na sua aplicação estão corretas ao ler Olá [tooYour adicionar início de sessão na aplicação do Web utilizar o Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) tópico, ou transferir e inspecionar o seguinte código de exemplo de Olá: [ Aplicação multi-inquilino de nuvem do Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="047fb-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="047fb-210"><a name="vs2010"></a>Aplicações Web de proteger os recursos e criados com o Visual Studio 2008 ou 2010 e a v 1.0 do Windows Identity Foundation (WIF) para o .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="047fb-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="047fb-211">Se criou uma aplicação no v 1.0 do WIF, não há nenhuma atualização de tooautomatically mecanismo fornecido toouse de configuração da sua aplicação uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="047fb-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="047fb-212">*A forma mais fácil* utilizar ferramentas de FedUtil Olá incluída no Olá WIF SDK, que pode obter documento de metadados Olá mais recente e atualizar a configuração.</span><span class="sxs-lookup"><span data-stu-id="047fb-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="047fb-213">Atualize o seu too.NET aplicação 4.5, que inclui a versão mais recente do Olá do WIF localizado no espaço de nomes de sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="047fb-214">Em seguida, pode utilizar Olá [validar o registo de nome de emissor (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform as atualizações automáticas de configuração da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="047fb-215">Efetue um rollover manual de acordo com as instruções de Olá no fim de Olá deste documento de orientação.</span><span class="sxs-lookup"><span data-stu-id="047fb-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="047fb-216">Instruções toouse Olá FedUtil tooupdate a configuração:</span><span class="sxs-lookup"><span data-stu-id="047fb-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="047fb-217">Certifique-se de que tem Olá WIF v 1.0 SDK instalado no computador de desenvolvimento para o Visual Studio 2008 ou 2010.</span><span class="sxs-lookup"><span data-stu-id="047fb-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="047fb-218">Pode [transferi-lo a partir daqui](https://www.microsoft.com/en-us/download/details.aspx?id=4451) se que ainda não instalou-lo.</span><span class="sxs-lookup"><span data-stu-id="047fb-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="047fb-219">No Visual Studio, abra a solução de Olá e, em seguida, clique no projeto aplicável Olá e selecione **atualizar os metadados de Federação**.</span><span class="sxs-lookup"><span data-stu-id="047fb-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="047fb-220">Se esta opção não estiver disponível, FedUtil e/ou Olá WIF v 1.0 do SDK não foi instalado.</span><span class="sxs-lookup"><span data-stu-id="047fb-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="047fb-221">A partir da linha de comandos Olá, selecione **atualização** toobegin atualizar os metadados de Federação.</span><span class="sxs-lookup"><span data-stu-id="047fb-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="047fb-222">Se tiver um ambiente de servidor acesso toohello onde está alojada aplicação Olá, opcionalmente, pode utilizar do FedUtil [Programador de atualização automática de metadados](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="047fb-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="047fb-223">Clique em **concluir** processo de atualização de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="047fb-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="047fb-224"><a name="other"></a>As aplicações Web / APIs proteger os recursos a utilizar quaisquer outras bibliotecas de manualmente implementar qualquer um dos Olá suportados ou protocolos</span><span class="sxs-lookup"><span data-stu-id="047fb-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="047fb-225">Se estiver a utilizar alguns outra biblioteca ou manualmente implementado qualquer um dos protocolos Olá suportado, terá de biblioteca de Olá tooreview ou o tooensure de implementação que Olá chave a ser obtida a partir do documento de identificação de OpenID Connect Olá ou Olá documento de metadados de Federação.</span><span class="sxs-lookup"><span data-stu-id="047fb-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="047fb-226">Toocheck unidirecional para isto é toodo uma pesquisa no seu código ou código da biblioteca de Olá para quaisquer chamadas documento de identificação do tooeither Olá OpenID ou documento de metadados de Federação Olá.</span><span class="sxs-lookup"><span data-stu-id="047fb-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="047fb-227">Se a chave que estão a ser armazenados algures ou codificado na sua aplicação, pode manualmente obter chave Olá e atualize-lo em conformidade por efetuar um rollover manual de acordo com as instruções de Olá no fim de Olá deste documento de orientação.</span><span class="sxs-lookup"><span data-stu-id="047fb-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="047fb-228">**É vivamente encouraged que melhoram o rollover automático de toosupport aplicação** utilizar qualquer um dos Olá contorno na interrupções futuras do artigo tooavoid e overhead se aproxima se o Azure AD aumenta a cadência da ou tem um rollover de fora de banda de emergência.</span><span class="sxs-lookup"><span data-stu-id="047fb-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="047fb-229">Como tootest sua toodetermine aplicação se serão afetada</span><span class="sxs-lookup"><span data-stu-id="047fb-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="047fb-230">Pode validar se a aplicação suporta o rollover de chave automático ao descarregar scripts Olá e seguir instruções Olá [este repositório do GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="047fb-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="047fb-231">Como tooperform um rollover manual se a aplicação não suporta o rollover automático</span><span class="sxs-lookup"><span data-stu-id="047fb-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="047fb-232">Se a aplicação **não** suporta rollover automático, terá tooestablish um processo que periodicamente monitores do Azure AD da assinatura de chaves e efetua um rollover manual em conformidade.</span><span class="sxs-lookup"><span data-stu-id="047fb-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="047fb-233">[Este repositório do GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contém scripts e instruções sobre como toodo isto.</span><span class="sxs-lookup"><span data-stu-id="047fb-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

