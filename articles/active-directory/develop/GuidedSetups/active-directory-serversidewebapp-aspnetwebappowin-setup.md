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
## <a name="set-up-your-project"></a>Configurar o projeto

Esta secção mostra Olá passos tooinstall e configurar o pipeline de autenticação de Olá através da OWIN middleware um projeto ASP.NET com OpenID Connect. 

> Prefere toodownload projeto do Visual Studio este exemplo em vez disso? [Transferir um projeto](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) e ignorar toohello [passo da configuração](#create-an-application-express) tooconfigure Olá código de exemplo antes de executar.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>Criar o projeto ASP.NET

> 1. No Visual Studio:`File` > `New` > `Project`<br/>
> 2. Em *Visual C# \Web*, selecione `ASP.NET Web Application (.NET Framework)`.
> 3. Nome da aplicação e clique em *OK*
> 4. Selecione `Empty` e Olá selecione caixa de verificação tooadd `MVC` referências
<!--end-collapse-->

## <a name="add-authentication-components"></a>Adicionar componentes de autenticação

1. No Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Adicionar *pacotes de NuGet OWIN middleware* , introduzindo seguinte Olá Olá janela consola do Gestor de pacote:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>Sobre estas bibliotecas

>Ativar bibliotecas Olá acima-início de sessão único (SSO) utilizando o OpenID Connect através da autenticação baseada no cookie. Depois de concluir a autenticação e token Olá que representa o utilizador Olá é enviado tooyour aplicação, o OWIN middleware cria um cookie de sessão. browser de Olá, em seguida, utiliza este cookie nos pedidos subsequentes pelo utilizador Olá não necessita de tooretype a palavra-passe e não é necessária nenhuma verificação adicional.
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>Configurar o pipeline de autenticação de Olá
passos de Olá abaixo são utilizado toocreate uma autenticação OpenID Connect de tooconfigure de classe de Startup middleware OWIN. Esta classe será executada automaticamente quando inicia o processo IIS.

> Se o seu projeto não tem um `Startup.cs` ficheiro na pasta raiz de Olá:<br/>
> 1. Botão direito do rato clique na pasta de raiz do projeto Olá: >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Nome`Startup.cs`

> Certifique-se a classe de Olá selecionada é uma classe de Startup da OWIN e não uma padrão c# classe. Confirmar isto, verificando se vir `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` acima Olá espaço de nomes.


1. Adicionar *OWIN* e *IdentityModel* referencia demasiado`Startup.cs`:

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
Substitua a classe de Startup com o código de Olá abaixo:
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
> ### <a name="more-information"></a>Mais Informações

> Olá parâmetros fornecem nos *OpenIDConnectAuthenticationOptions* servir como coordenadas para Olá toocommunicate de aplicação com o Azure AD. Uma vez Olá OpenID Connect middleware utiliza cookies em segundo plano de Olá, terá também tooset configurar a autenticação de cookie como código de Olá acima mostra. Olá *ValidateIssuer* valor indica OpenIdConnect toonot restringir acesso tooone específico organização.
<!--end-collapse-->

