---
title: aaaAzure AD B2C | Microsoft Docs
description: "Como toobuild uma API Web do .NET utilizando o Azure Active Directory B2C, protegida utilizando os tokens de acesso de OAuth 2.0 para autenticação."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="f2df0-103">Azure Active Directory B2C: criar uma API Web do .NET</span><span class="sxs-lookup"><span data-stu-id="f2df0-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="f2df0-104">Com o Azure Active Directory (Azure AD) B2C, pode proteger uma API web utilizando tokens de acesso de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="f2df0-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="f2df0-105">Estes tokens permitem que o cliente aplicações tooauthenticate toohello API.</span><span class="sxs-lookup"><span data-stu-id="f2df0-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="f2df0-106">Este artigo mostra como toocreate uma API de "lista de tarefas" do MVC do .NET que permite que os utilizadores do seu cliente tarefas tooCRUD de aplicações.</span><span class="sxs-lookup"><span data-stu-id="f2df0-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="f2df0-107">Olá web API está protegida com o Azure AD B2C e só permite que os utilizadores autenticados toomanage respetiva lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="f2df0-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="f2df0-108">Criar um diretório do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f2df0-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="f2df0-109">Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.</span><span class="sxs-lookup"><span data-stu-id="f2df0-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="f2df0-110">Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="f2df0-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="f2df0-111">Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="f2df0-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="f2df0-112">web API e uma aplicação de cliente Olá tem de utilizar diretório do B2C Olá mesmo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2df0-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="f2df0-113">Criar uma API Web</span><span class="sxs-lookup"><span data-stu-id="f2df0-113">Create a web API</span></span>

<span data-ttu-id="f2df0-114">Em seguida, terá de toocreate uma aplicação de API web no diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="f2df0-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="f2df0-115">Isto dá-informações do Azure AD que necessidades toosecurely comunicar com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="f2df0-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="f2df0-116">toocreate uma aplicação, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f2df0-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="f2df0-117">É necessário:</span><span class="sxs-lookup"><span data-stu-id="f2df0-117">Be sure to:</span></span>

* <span data-ttu-id="f2df0-118">Incluir um **aplicação web** ou **web API** na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f2df0-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="f2df0-119">Olá utilize **URI de redirecionamento** `https://localhost:44332/` da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="f2df0-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="f2df0-120">Esta é a localização predefinida de hello do cliente da aplicação web Olá para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="f2df0-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="f2df0-121">Olá cópia **ID da aplicação** que é atribuído tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="f2df0-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="f2df0-122">Precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f2df0-122">You'll need it later.</span></span>
* <span data-ttu-id="f2df0-123">Introduza um identificador de aplicação em **URI de ID de Aplicação**.</span><span class="sxs-lookup"><span data-stu-id="f2df0-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="f2df0-124">Adicionar permissões através de Olá **publicados âmbitos** menu.</span><span class="sxs-lookup"><span data-stu-id="f2df0-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="f2df0-125">Criar as políticas</span><span class="sxs-lookup"><span data-stu-id="f2df0-125">Create your policies</span></span>

<span data-ttu-id="f2df0-126">No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f2df0-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f2df0-127">Terá de toocreate toocommunicate uma política com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f2df0-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="f2df0-128">É recomendável utilizar Olá combinado sessão-up/início de sessão de política, conforme descrito em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f2df0-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f2df0-129">Quando criar a política, certifique-se de que:</span><span class="sxs-lookup"><span data-stu-id="f2df0-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="f2df0-130">Escolhe o **Nome a apresentar** e outros atributos de inscrição na política.</span><span class="sxs-lookup"><span data-stu-id="f2df0-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="f2df0-131">Escolher as afirmações **Nome a apresentar** e **ID de objeto** como afirmações de aplicação em cada política.</span><span class="sxs-lookup"><span data-stu-id="f2df0-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="f2df0-132">Também pode escolher outras afirmações.</span><span class="sxs-lookup"><span data-stu-id="f2df0-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="f2df0-133">Olá cópia **nome** de cada política depois de a criar.</span><span class="sxs-lookup"><span data-stu-id="f2df0-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="f2df0-134">Terá de nome da política hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f2df0-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="f2df0-135">Depois de ter criado com êxito a política de Olá, está pronto toobuild a aplicação.</span><span class="sxs-lookup"><span data-stu-id="f2df0-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="f2df0-136">Transferir o código de Olá</span><span class="sxs-lookup"><span data-stu-id="f2df0-136">Download hello code</span></span>

<span data-ttu-id="f2df0-137">código Olá deste tutorial é mantido no [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="f2df0-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="f2df0-138">Pode clonar o exemplo de Olá executando:</span><span class="sxs-lookup"><span data-stu-id="f2df0-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="f2df0-139">Depois de transferir o código de exemplo de Olá, abra Olá Visual Studio. sln ficheiro tooget foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="f2df0-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="f2df0-140">ficheiro de solução Olá contém dois projetos: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="f2df0-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="f2df0-141">`TaskWebApp`é uma aplicação de web MVC Olá utilizador interage com.</span><span class="sxs-lookup"><span data-stu-id="f2df0-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="f2df0-142">`TaskService`é API de web de back-end da aplicação Olá que armazena a lista de tarefas de cada utilizador.</span><span class="sxs-lookup"><span data-stu-id="f2df0-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="f2df0-143">Este artigo apenas abordar Olá `TaskService` aplicação.</span><span class="sxs-lookup"><span data-stu-id="f2df0-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="f2df0-144">toolearn como toobuild `TaskWebApp` utilizando o Azure AD B2C, consulte [nosso tutorial da aplicação web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="f2df0-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="f2df0-145">Atualizar a configuração de Olá, Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f2df0-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="f2df0-146">Nosso exemplo é configurado toouse Olá políticas e cliente ID do inquilino a nossa demonstração.</span><span class="sxs-lookup"><span data-stu-id="f2df0-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="f2df0-147">Se quiser toouse o seu inquilino, terá de Olá toodo seguintes:</span><span class="sxs-lookup"><span data-stu-id="f2df0-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="f2df0-148">Abra `web.config` no Olá `TaskService` projeto e substitua os valores de Olá para</span><span class="sxs-lookup"><span data-stu-id="f2df0-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="f2df0-149">`ida:Tenant` pelo nome do seu inquilino</span><span class="sxs-lookup"><span data-stu-id="f2df0-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="f2df0-150">`ida:ClientId` pelo ID da sua aplicação da API Web</span><span class="sxs-lookup"><span data-stu-id="f2df0-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="f2df0-151">`ida:SignUpSignInPolicyId` pelo nome da sua política de “Inscrição ou Início de Sessão”</span><span class="sxs-lookup"><span data-stu-id="f2df0-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="f2df0-152">Abra `web.config` no Olá `TaskWebApp` projeto e substitua os valores de Olá para</span><span class="sxs-lookup"><span data-stu-id="f2df0-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="f2df0-153">`ida:Tenant` pelo nome do seu inquilino</span><span class="sxs-lookup"><span data-stu-id="f2df0-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="f2df0-154">`ida:ClientId` pelo ID da sua aplicação Web</span><span class="sxs-lookup"><span data-stu-id="f2df0-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="f2df0-155">`ida:ClientSecret` pela chave de segredo da sua aplicação Web</span><span class="sxs-lookup"><span data-stu-id="f2df0-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="f2df0-156">`ida:SignUpSignInPolicyId` pelo nome da sua política de “Inscrição ou Início de Sessão”</span><span class="sxs-lookup"><span data-stu-id="f2df0-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="f2df0-157">`ida:EditProfilePolicyId` pelo nome da sua política de “Editar Perfil”</span><span class="sxs-lookup"><span data-stu-id="f2df0-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="f2df0-158">`ida:ResetPasswordPolicyId` pelo nome da sua política de “Repor Palavras-Passe”</span><span class="sxs-lookup"><span data-stu-id="f2df0-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="f2df0-159">Proteger Olá API</span><span class="sxs-lookup"><span data-stu-id="f2df0-159">Secure hello API</span></span>

<span data-ttu-id="f2df0-160">Quando tiver um cliente que chama a API, pode utilizar tokens de portador do OAuth 2.0 para proteger a sua API (por exemplo, `TaskService`).</span><span class="sxs-lookup"><span data-stu-id="f2df0-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="f2df0-161">Isto assegura que cada API do pedido tooyour só será válida se o pedido de Olá tem um token de portador.</span><span class="sxs-lookup"><span data-stu-id="f2df0-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="f2df0-162">A sua API pode aceitar e validar os tokens de portador através da biblioteca OWIN (Open Web Interface para .NET) da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f2df0-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="f2df0-163">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="f2df0-163">Install OWIN</span></span>

<span data-ttu-id="f2df0-164">Comece por instalar o pipeline de autenticação OAuth da OWIN Olá utilizando Olá consola do Gestor de pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2df0-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="f2df0-165">Esta ação instalará Olá OWIN middleware que irá aceitar e validar os tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="f2df0-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="f2df0-166">Adicionar uma classe de startup da OWIN</span><span class="sxs-lookup"><span data-stu-id="f2df0-166">Add an OWIN startup class</span></span>

<span data-ttu-id="f2df0-167">Adicionar um toohello de classe de arranque da OWIN API chamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="f2df0-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="f2df0-168">Clique com o botão direito no projeto Olá, selecione **adicionar** e **Novo Item**e, em seguida, pesquise OWIN.</span><span class="sxs-lookup"><span data-stu-id="f2df0-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="f2df0-169">Olá OWIN middleware serão invocados Olá `Configuration(…)` método quando a aplicação for iniciada.</span><span class="sxs-lookup"><span data-stu-id="f2df0-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="f2df0-170">No nosso exemplo, Alterámos declaração de classe de Olá demasiado`public partial class Startup` e implementados Olá outro parte da classe de Olá na `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="f2df0-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="f2df0-171">Olá interior `Configuration` método, adicionámos uma chamada demasiado`ConfigureAuth`, que está definido no `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="f2df0-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="f2df0-172">Após a modificação de Olá, `Startup.cs` se parece com Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="f2df0-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="f2df0-173">Configurar a autenticação OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="f2df0-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="f2df0-174">Ficheiro aberto Olá `App_Start\Startup.Auth.cs`e implementar Olá `ConfigureAuth(...)` método.</span><span class="sxs-lookup"><span data-stu-id="f2df0-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="f2df0-175">Por exemplo, se foi aspeto Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="f2df0-175">For example, it could look like hello following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="f2df0-176">Proteger o controlador de tarefa Olá</span><span class="sxs-lookup"><span data-stu-id="f2df0-176">Secure hello task controller</span></span>

<span data-ttu-id="f2df0-177">Após a conclusão da aplicação Olá autenticação toouse configurado OAuth 2.0, pode proteger a API web adicionando um `[Authorize]` controlador de tarefa toohello etiquetas.</span><span class="sxs-lookup"><span data-stu-id="f2df0-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="f2df0-178">Este é o controlador de olá onde manipulação de lista de todas as tarefas ocorre, pelo que deve proteger controlador na totalidade Olá ao nível de classe de Olá.</span><span class="sxs-lookup"><span data-stu-id="f2df0-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="f2df0-179">Também pode adicionar Olá `[Authorize]` tag tooindividual ações para um controlo mais detalhado.</span><span class="sxs-lookup"><span data-stu-id="f2df0-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="f2df0-180">Obter informações de utilizador de Olá token</span><span class="sxs-lookup"><span data-stu-id="f2df0-180">Get user information from hello token</span></span>

<span data-ttu-id="f2df0-181">`TasksController`armazena as tarefas numa base de dados onde cada tarefa tem um utilizador associado que é "proprietário" tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="f2df0-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="f2df0-182">proprietário de Olá é identificado por utilizador Olá **ID de objeto**.</span><span class="sxs-lookup"><span data-stu-id="f2df0-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="f2df0-183">(Esta é a razão pela qual é necessário o ID de objeto de Olá tooadd como uma aplicação afirmação em todas as suas políticas.)</span><span class="sxs-lookup"><span data-stu-id="f2df0-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="f2df0-184">Validar permissões de Olá no token de Olá</span><span class="sxs-lookup"><span data-stu-id="f2df0-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="f2df0-185">Um requisito comum para as APIs web é toovalidate Olá "âmbitos" presentes no token de Olá.</span><span class="sxs-lookup"><span data-stu-id="f2df0-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="f2df0-186">Isto garante que o utilizador Olá consentiu serviço de lista de tarefas necessária tooaccess Olá toohello permissões.</span><span class="sxs-lookup"><span data-stu-id="f2df0-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="f2df0-187">Executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="f2df0-187">Run hello sample app</span></span>

<span data-ttu-id="f2df0-188">Por último, crie e execute `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="f2df0-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="f2df0-189">Crie algumas tarefas na lista de tarefas do utilizador Olá e repare como persistem na Olá API mesmo depois de parar e reiniciar Olá cliente.</span><span class="sxs-lookup"><span data-stu-id="f2df0-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="f2df0-190">Editar as suas políticas</span><span class="sxs-lookup"><span data-stu-id="f2df0-190">Edit your policies</span></span>

<span data-ttu-id="f2df0-191">Depois de proteger uma API utilizando o Azure AD B2C, pode experimentar com a política de início de sessão-na/sessão-up e vista Olá efeitos (ou ambos falta) na Olá API.</span><span class="sxs-lookup"><span data-stu-id="f2df0-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="f2df0-192">Pode manipular afirmações de aplicação Olá nas políticas de Olá e alterar as informações de utilizador de Olá que estão disponíveis na API web do Olá.</span><span class="sxs-lookup"><span data-stu-id="f2df0-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="f2df0-193">Qualquer afirmações que adicionar estarão disponíveis tooyour API de web de MVC do .NET no Olá `ClaimsPrincipal` objeto, como descrito anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f2df0-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
