---
title: "utilizar o início de sessão tooa API web de MVC do .NET aaaAdd Olá ponto final de v 2.0 do Azure AD | Microsoft Docs"
description: Como toobuild uma Api de Web de MVC do .NET que aceita tokens a partir de ambos os Account Microsoft pessoal e contas profissionais ou escolares.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="e1dc6-103">Proteger uma API web MVC</span><span class="sxs-lookup"><span data-stu-id="e1dc6-103">Secure an MVC web API</span></span>
<span data-ttu-id="e1dc6-104">Com o ponto final v 2.0 do Azure Active Directory Olá, pode proteger uma Web API utilizando [OAuth 2.0](active-directory-v2-protocols.md) tokens de acesso, os utilizadores com ambos os conta pessoal da Microsoft e contas profissionais ou escolares toosecurely aceder à sua API Web.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="e1dc6-105">Nem todos os cenários do Azure Active Directory e funcionalidades são suportadas pelo ponto final de v 2.0 Olá.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="e1dc6-106">toodetermine se deve utilizar o ponto final de v 2.0 Olá, leia sobre [limitações de v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="e1dc6-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="e1dc6-107">Nas ASP.NET web APIs, isto é possível utilizar o middleware OWIN da Microsoft incluído no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="e1dc6-108">Aqui iremos utilizar OWIN toobuild uma API de Web MVC "tooDo lista" que permite aos clientes toocreate e ler tarefas da lista de tarefas de um utilizador.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="e1dc6-109">API web do Olá irá validar que os pedidos recebidos contém um token de acesso válido e rejeitar quaisquer pedidos que não são transmitidas validação numa rota protegida.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="e1dc6-110">Este exemplo foi criado com o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="e1dc6-111">Transferência</span><span class="sxs-lookup"><span data-stu-id="e1dc6-111">Download</span></span>
<span data-ttu-id="e1dc6-112">código Olá deste tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="e1dc6-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="e1dc6-113">toofollow ao longo, pode [transferir a estrutura da aplicação Olá como um. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou estrutura de Olá do clone:</span><span class="sxs-lookup"><span data-stu-id="e1dc6-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="e1dc6-114">aplicação de estrutura de Olá inclui todo o código automático Olá para uma API simple, mas está em falta todas as partes de relacionadas com identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="e1dc6-115">Se não quiser toofollow ao longo, em vez disso, pode clonar ou [transferir exemplo Olá concluída](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e1dc6-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="e1dc6-116">Registar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="e1dc6-116">Register an app</span></span>
<span data-ttu-id="e1dc6-117">Criar uma nova aplicação em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga estas [detalhadas passos](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="e1dc6-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="e1dc6-118">Certifique-se de que:</span><span class="sxs-lookup"><span data-stu-id="e1dc6-118">Make sure to:</span></span>

* <span data-ttu-id="e1dc6-119">Copie Olá **Id da aplicação** atribuído tooyour aplicação, irá precisar das mesmas em breve.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="e1dc6-120">Esta solução do visual studio também contém um "TodoListClient", que é uma simple aplicação WPF.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="e1dc6-121">Olá TodoListClient é toodemonstrate utilizado como um utilizador inicia sessão e como um cliente pode emitir pedidos tooyour Web API.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="e1dc6-122">Neste caso, Olá TodoListClient e Olá TodoListService são representados por Olá mesma aplicação.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="e1dc6-123">tooconfigure Olá TodoListClient, deve também:</span><span class="sxs-lookup"><span data-stu-id="e1dc6-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="e1dc6-124">Adicionar Olá **Mobile** plataforma para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="e1dc6-125">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="e1dc6-125">Install OWIN</span></span>
<span data-ttu-id="e1dc6-126">Agora que já registou uma aplicação, terá de tooset cópias de segurança sua toocommunicate de aplicação com o ponto final de v 2.0 Olá na ordem toovalidate os pedidos recebidos & tokens.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="e1dc6-127">toobegin, abra a solução Olá e adicione Olá OWIN middleware NuGet pacotes toohello TodoListService projeto Olá consola do Gestor de pacotes a utilizar.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="e1dc6-128">Configurar a autenticação do OAuth</span><span class="sxs-lookup"><span data-stu-id="e1dc6-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="e1dc6-129">Adicionar um projeto de toohello classe do arranque de OWIN TodoListService chamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="e1dc6-130">Clique direito no projeto Olá--> **adicionar** --> **Novo Item** --> procure "OWIN".</span><span class="sxs-lookup"><span data-stu-id="e1dc6-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="e1dc6-131">Olá OWIN middleware serão invocados Olá `Configuration(…)` método quando a aplicação for iniciada.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="e1dc6-132">Alterar a declaração de classe de Olá demasiado`public partial class Startup` -iremos já tiver implementado parte desta classe para si no outro ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="e1dc6-133">No Olá `Configuration(…)` método, certifique-tooset de tooConfgureAuth(...) uma chamada de configurar a autenticação para a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="e1dc6-134">Ficheiro aberto Olá `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(…)` método, o que irá configurar tokens de tooaccept Olá Web API a partir do ponto final de v 2.0 Olá.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="e1dc6-135">Agora, pode utilizar `[Authorize]` tooprotect de atributos, os controladores e ações com autenticação de portador do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="e1dc6-136">OptionalFieldAttribute Olá `Controllers\TodoListController.cs` classe com uma etiqueta de autorizar.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="e1dc6-137">Isto irá forçar Olá utilizador toosign no antes de aceder a essa página.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="e1dc6-138">Quando um autor da chamada autorizado com êxito invoca um Olá `TodoListController` APIs, ação Olá pode precisar de aceder a tooinformation sobre chamador Olá.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="e1dc6-139">OWIN fornece acesso toohello afirmações dentro de token de portador Olá através de Olá `ClaimsPrincpal` objeto.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="e1dc6-140">Por fim, abra Olá `web.config` ficheiro na raiz de Olá do projeto de TodoListService Olá e introduza os valores de configuração no Olá `<appSettings>` secção.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="e1dc6-141">O `ida:Audience` é Olá **Id da aplicação** da aplicação Olá que introduziu no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="e1dc6-142">Configure a aplicação de cliente Olá</span><span class="sxs-lookup"><span data-stu-id="e1dc6-142">Configure hello client app</span></span>
<span data-ttu-id="e1dc6-143">Antes de poder ver Olá serviço de lista de tarefas em ação, terá tooconfigure Olá cliente de lista de tarefas para que possa obter os tokens a partir do ponto final de v 2.0 Olá e efetuar chamadas toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="e1dc6-144">No projeto de TodoListClient Olá, abra `App.config` e introduza os valores de configuração no Olá `<appSettings>` secção.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="e1dc6-145">O `ida:ClientId` Id da aplicação que copiou a partir do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="e1dc6-146">Por fim, apagar, criar e executar cada projeto!</span><span class="sxs-lookup"><span data-stu-id="e1dc6-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="e1dc6-147">Tem agora uma API de Web de MVC do .NET que aceita tokens a partir de ambas as contas pessoais da Microsoft e contas profissionais ou escolares.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="e1dc6-148">Inicie sessão no Olá TodoListClient e chamar a lista de tarefas web api tooadd tarefas toohello dos seus utilizadores.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="e1dc6-149">Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como um. zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), ou pode cloná-la a partir do GitHub:</span><span class="sxs-lookup"><span data-stu-id="e1dc6-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="e1dc6-150">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e1dc6-150">Next steps</span></span>
<span data-ttu-id="e1dc6-151">Agora pode mover para tópicos adicionais.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="e1dc6-152">Poderá ser útil tootry:</span><span class="sxs-lookup"><span data-stu-id="e1dc6-152">You may want tootry:</span></span>

[<span data-ttu-id="e1dc6-153">Chamar uma API Web a partir de uma aplicação Web >></span><span class="sxs-lookup"><span data-stu-id="e1dc6-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="e1dc6-154">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="e1dc6-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="e1dc6-155">Guia para programadores do Olá v 2.0 >></span><span class="sxs-lookup"><span data-stu-id="e1dc6-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="e1dc6-156">Etiqueta de StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="e1dc6-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="e1dc6-157">Obter atualizações de segurança dos nossos produtos</span><span class="sxs-lookup"><span data-stu-id="e1dc6-157">Get security updates for our products</span></span>
<span data-ttu-id="e1dc6-158">Aconselhamo-lo tooget notificações de quando os incidentes de segurança ocorrem, visitando [nesta página](https://technet.microsoft.com/security/dd252948) e subscrever tooSecurity SUBSCREVENDO os alertas.</span><span class="sxs-lookup"><span data-stu-id="e1dc6-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
