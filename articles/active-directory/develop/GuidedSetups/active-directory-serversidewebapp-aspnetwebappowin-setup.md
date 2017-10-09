---
title: "aaaAzure AD v2 ASP.NET Web Server introdução - configuração | Microsoft Docs"
description: "Implementar Microsoft início de sessão numa solução ASP.NET com uma aplicação de baseadas no browser web tradicional utilizando o padrão de OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="ea892-103">Configurar o projeto</span><span class="sxs-lookup"><span data-stu-id="ea892-103">Set up your project</span></span>

<span data-ttu-id="ea892-104">Esta secção mostra Olá passos tooinstall e configurar o pipeline de autenticação de Olá através da OWIN middleware um projeto ASP.NET com OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="ea892-104">This section shows hello steps tooinstall and configure hello authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="ea892-105">Prefere toodownload projeto do Visual Studio este exemplo em vez disso?</span><span class="sxs-lookup"><span data-stu-id="ea892-105">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="ea892-106">[Transferir um projeto](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) e ignorar toohello [passo da configuração](#create-an-application-express) tooconfigure Olá código de exemplo antes de executar.</span><span class="sxs-lookup"><span data-stu-id="ea892-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="ea892-107">Criar o projeto ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ea892-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="ea892-108">No Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="ea892-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="ea892-109">Em *Visual C# \Web*, selecione `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="ea892-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="ea892-110">Nome da aplicação e clique em *OK*</span><span class="sxs-lookup"><span data-stu-id="ea892-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="ea892-111">Selecione `Empty` e Olá selecione caixa de verificação tooadd `MVC` referências</span><span class="sxs-lookup"><span data-stu-id="ea892-111">Select `Empty` and select hello checkbox tooadd `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="ea892-112">Adicionar componentes de autenticação</span><span class="sxs-lookup"><span data-stu-id="ea892-112">Add authentication components</span></span>

1. <span data-ttu-id="ea892-113">No Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="ea892-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="ea892-114">Adicionar *pacotes de NuGet OWIN middleware* , introduzindo seguinte Olá Olá janela consola do Gestor de pacote:</span><span class="sxs-lookup"><span data-stu-id="ea892-114">Add *OWIN middleware NuGet packages* by typing hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="ea892-115">Sobre estas bibliotecas</span><span class="sxs-lookup"><span data-stu-id="ea892-115">About these libraries</span></span>

><span data-ttu-id="ea892-116">Ativar bibliotecas Olá acima-início de sessão único (SSO) utilizando o OpenID Connect através da autenticação baseada no cookie.</span><span class="sxs-lookup"><span data-stu-id="ea892-116">hello libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="ea892-117">Depois de concluir a autenticação e token Olá que representa o utilizador Olá é enviado tooyour aplicação, o OWIN middleware cria um cookie de sessão.</span><span class="sxs-lookup"><span data-stu-id="ea892-117">After authentication is completed and hello token representing hello user is sent tooyour application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="ea892-118">browser de Olá, em seguida, utiliza este cookie nos pedidos subsequentes pelo utilizador Olá não necessita de tooretype a palavra-passe e não é necessária nenhuma verificação adicional.</span><span class="sxs-lookup"><span data-stu-id="ea892-118">hello browser then uses this cookie on subsequent requests so hello user doesn't need tooretype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a><span data-ttu-id="ea892-119">Configurar o pipeline de autenticação de Olá</span><span class="sxs-lookup"><span data-stu-id="ea892-119">Configure hello authentication pipeline</span></span>
<span data-ttu-id="ea892-120">passos de Olá abaixo são utilizado toocreate uma autenticação OpenID Connect de tooconfigure de classe de Startup middleware OWIN.</span><span class="sxs-lookup"><span data-stu-id="ea892-120">hello steps below are used toocreate an OWIN middleware Startup Class tooconfigure OpenID Connect authentication.</span></span> <span data-ttu-id="ea892-121">Esta classe será executada automaticamente quando inicia o processo IIS.</span><span class="sxs-lookup"><span data-stu-id="ea892-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="ea892-122">Se o seu projeto não tem um `Startup.cs` ficheiro na pasta raiz de Olá:</span><span class="sxs-lookup"><span data-stu-id="ea892-122">If your project doesn't have a `Startup.cs` file in hello root folder:</span></span><br/>
> 1. <span data-ttu-id="ea892-123">Botão direito do rato clique na pasta de raiz do projeto Olá: >`Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="ea892-123">Right click on hello project's root folder: >  `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="ea892-124">Nome`Startup.cs`</span><span class="sxs-lookup"><span data-stu-id="ea892-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="ea892-125">Certifique-se a classe de Olá selecionada é uma classe de Startup da OWIN e não uma padrão c# classe.</span><span class="sxs-lookup"><span data-stu-id="ea892-125">Make sure hello class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="ea892-126">Confirmar isto, verificando se vir `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` acima Olá espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="ea892-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above hello namespace.</span></span>


1. <span data-ttu-id="ea892-127">Adicionar *OWIN* e *IdentityModel* referencia demasiado`Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="ea892-127">Add *OWIN* and *Microsoft.IdentityModel* references too`Startup.cs`:</span></span>

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="ea892-128">Substitua a classe de Startup com o código de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="ea892-128">Replace Startup class with hello code below:</span></span>
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a><span data-ttu-id="ea892-129">Mais Informações</span><span class="sxs-lookup"><span data-stu-id="ea892-129">More Information</span></span>

> <span data-ttu-id="ea892-130">Olá parâmetros fornecem nos *OpenIDConnectAuthenticationOptions* servir como coordenadas para Olá toocommunicate de aplicação com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea892-130">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello application toocommunicate with Azure AD.</span></span> <span data-ttu-id="ea892-131">Uma vez Olá OpenID Connect middleware utiliza cookies em segundo plano de Olá, terá também tooset configurar a autenticação de cookie como código de Olá acima mostra.</span><span class="sxs-lookup"><span data-stu-id="ea892-131">Because hello OpenID Connect middleware uses cookies in hello background, you also need tooset up cookie authentication as hello code above shows.</span></span> <span data-ttu-id="ea892-132">Olá *ValidateIssuer* valor indica OpenIdConnect toonot restringir acesso tooone específico organização.</span><span class="sxs-lookup"><span data-stu-id="ea892-132">hello *ValidateIssuer* value tells OpenIdConnect toonot restrict access tooone specific organization.</span></span>
<!--end-collapse-->

