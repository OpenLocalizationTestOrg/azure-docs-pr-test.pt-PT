---
title: "aaaAzure AD v2 ASP.NET Web Server introdução - utilização | Microsoft Docs"
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
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>Adicione um pedidos de início de sessão e fim de sessão de toohandle do controlador

Este passo mostra como toocreate um tooexpose controlador novo início de sessão e fim de sessão métodos.

1.  Clique com o botão direito do rato em Olá `Controllers` pastas e selecione`Add` > `Controller`
2.  Selecione `MVC (.NET version) Controller – Empty`.
3.  Clique em *adicionar*
4.  Nome `HomeController` e clique em *adicionar*
5.  Adicionar *OWIN* referencia toohello classe:

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Adicione dois métodos de Olá abaixo toohandle início de sessão e fim de sessão tooyour controlador iniciando um desafio de autenticação através de código:
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>Criar toosign de página inicial da aplicação Olá sessão dos utilizadores através de um botão de início de sessão

No Visual Studio, crie um nova vista tooadd Olá início de sessão botão e apresentar informações de utilizador após a autenticação:

1.  Clique com o botão direito do rato em Olá `Views\Home` pastas e selecione`Add View`
2.  Dê-lhe o nome `Index`.
3.  Adicione Olá HTML, que inclui Olá início de sessão botão, o ficheiro de toohello os seguintes:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a>Mais Informações
> Esta página adiciona um botão de início de sessão no formato SVG com um fundo preto:<br/>![Início de sessão com a Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> Para obter mais início de sessão botões, visite toohello [nesta página](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "diretrizes de imagem corporativa").
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>Adicionar afirmações de um utilizador de toodisplay de controlador
Este controlador demonstra Olá utilizações de Olá `[Authorize]` tooprotect um controlador de atributos. Este atributo restringe o controlador de toohello de acesso, permitindo apenas que os utilizadores autenticados. Olá código abaixo utilizam Olá atributo toodisplay afirmações de utilizador que foram obtidas como parte da Olá início de sessão.

1.  Clique com o botão direito do rato em Olá `Controllers` pasta:`Add` > `Controller`
2.  Selecione `MVC {version} Controller – Empty`.
3.  Clique em *adicionar*
4.  Nome`ClaimsController`
5.  Substitua o código de Olá da sua classe de controlador com o código de Olá abaixo - esta ação adiciona Olá `[Authorize]` toohello classe de atributo:

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Mais Informações
> Devido à utilização de Olá de Olá `[Authorize]` atributo, todos os métodos deste controlador só pode ser executado se Olá utilizador ser autenticado. Se o utilizador Olá não é autenticado e tenta tooaccess controlador de Olá, OWIN irá iniciar um desafio de autenticação e forçar Olá tooauthenticate de utilizador. coleção de Olá de afirmações de código Olá acima procura em Olá `ClaimsPrincipal.Current` instância para atributos de utilizador específico incluídas no token de utilizador Olá. Estes atributos incluem o nome completo do utilizador Olá e o nome de utilizador, bem como o requerente de identificador do utilizador global Olá. Também contém Olá *ID do inquilino*, que representa o ID de Olá para a organização do utilizador Olá. 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>Criar uma vista de afirmações do utilizador Olá toodisplay

No Visual Studio, crie uma nova vista de afirmações do utilizador Olá toodisplay numa página web:

1.  Clique com o botão direito do rato em Olá `Views\Claims` pasta e:`Add View`
2.  Dê-lhe o nome `Index`.
3.  Adicione Olá seguintes HTML toohello ficheiro:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
