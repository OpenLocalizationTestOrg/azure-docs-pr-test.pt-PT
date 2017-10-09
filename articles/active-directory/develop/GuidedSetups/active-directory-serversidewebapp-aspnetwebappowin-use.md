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
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a><span data-ttu-id="5546c-103">Adicione um pedidos de início de sessão e fim de sessão de toohandle do controlador</span><span class="sxs-lookup"><span data-stu-id="5546c-103">Add a controller toohandle sign-in and sign-out requests</span></span>

<span data-ttu-id="5546c-104">Este passo mostra como toocreate um tooexpose controlador novo início de sessão e fim de sessão métodos.</span><span class="sxs-lookup"><span data-stu-id="5546c-104">This step shows how toocreate a new controller tooexpose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="5546c-105">Clique com o botão direito do rato em Olá `Controllers` pastas e selecione`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="5546c-105">Right click hello `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="5546c-106">Selecione `MVC (.NET version) Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="5546c-106">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="5546c-107">Clique em *adicionar*</span><span class="sxs-lookup"><span data-stu-id="5546c-107">Click *Add*</span></span>
4.  <span data-ttu-id="5546c-108">Nome `HomeController` e clique em *adicionar*</span><span class="sxs-lookup"><span data-stu-id="5546c-108">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="5546c-109">Adicionar *OWIN* referencia toohello classe:</span><span class="sxs-lookup"><span data-stu-id="5546c-109">Add *OWIN* references toohello class:</span></span>

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="5546c-110">Adicione dois métodos de Olá abaixo toohandle início de sessão e fim de sessão tooyour controlador iniciando um desafio de autenticação através de código:</span><span class="sxs-lookup"><span data-stu-id="5546c-110">Add hello two methods below toohandle sign-in and sign-out tooyour controller by initiating an authentication challenge via code:</span></span>
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

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a><span data-ttu-id="5546c-111">Criar toosign de página inicial da aplicação Olá sessão dos utilizadores através de um botão de início de sessão</span><span class="sxs-lookup"><span data-stu-id="5546c-111">Create hello app's home page toosign in users via a sign-in button</span></span>

<span data-ttu-id="5546c-112">No Visual Studio, crie um nova vista tooadd Olá início de sessão botão e apresentar informações de utilizador após a autenticação:</span><span class="sxs-lookup"><span data-stu-id="5546c-112">In Visual Studio, create a new view tooadd hello sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="5546c-113">Clique com o botão direito do rato em Olá `Views\Home` pastas e selecione`Add View`</span><span class="sxs-lookup"><span data-stu-id="5546c-113">Right click hello `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="5546c-114">Dê-lhe o nome `Index`.</span><span class="sxs-lookup"><span data-stu-id="5546c-114">Name it `Index`.</span></span>
3.  <span data-ttu-id="5546c-115">Adicione Olá HTML, que inclui Olá início de sessão botão, o ficheiro de toohello os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5546c-115">Add hello following HTML, which includes hello sign-in button, toohello file:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="5546c-116">Mais Informações</span><span class="sxs-lookup"><span data-stu-id="5546c-116">More Information</span></span>
> <span data-ttu-id="5546c-117">Esta página adiciona um botão de início de sessão no formato SVG com um fundo preto:</span><span class="sxs-lookup"><span data-stu-id="5546c-117">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="5546c-118">![Início de sessão com a Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="5546c-118">![Sign-in with Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="5546c-119">Para obter mais início de sessão botões, visite toohello [nesta página](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "diretrizes de imagem corporativa").</span><span class="sxs-lookup"><span data-stu-id="5546c-119">For more sign-in buttons, please go toohello [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a><span data-ttu-id="5546c-120">Adicionar afirmações de um utilizador de toodisplay de controlador</span><span class="sxs-lookup"><span data-stu-id="5546c-120">Add a controller toodisplay user's claims</span></span>
<span data-ttu-id="5546c-121">Este controlador demonstra Olá utilizações de Olá `[Authorize]` tooprotect um controlador de atributos.</span><span class="sxs-lookup"><span data-stu-id="5546c-121">This controller demonstrates hello uses of hello `[Authorize]` attribute tooprotect a controller.</span></span> <span data-ttu-id="5546c-122">Este atributo restringe o controlador de toohello de acesso, permitindo apenas que os utilizadores autenticados.</span><span class="sxs-lookup"><span data-stu-id="5546c-122">This attribute restricts access toohello controller by only allowing authenticated users.</span></span> <span data-ttu-id="5546c-123">Olá código abaixo utilizam Olá atributo toodisplay afirmações de utilizador que foram obtidas como parte da Olá início de sessão.</span><span class="sxs-lookup"><span data-stu-id="5546c-123">hello code below makes use of hello attribute toodisplay user claims that were retrieved as part of hello sign-in.</span></span>

1.  <span data-ttu-id="5546c-124">Clique com o botão direito do rato em Olá `Controllers` pasta:`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="5546c-124">Right click hello `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="5546c-125">Selecione `MVC {version} Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="5546c-125">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="5546c-126">Clique em *adicionar*</span><span class="sxs-lookup"><span data-stu-id="5546c-126">Click *Add*</span></span>
4.  <span data-ttu-id="5546c-127">Nome`ClaimsController`</span><span class="sxs-lookup"><span data-stu-id="5546c-127">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="5546c-128">Substitua o código de Olá da sua classe de controlador com o código de Olá abaixo - esta ação adiciona Olá `[Authorize]` toohello classe de atributo:</span><span class="sxs-lookup"><span data-stu-id="5546c-128">Replace hello code of your controller class with hello code below - this adds hello `[Authorize]` attribute toohello class:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="5546c-129">Mais Informações</span><span class="sxs-lookup"><span data-stu-id="5546c-129">More Information</span></span>
> <span data-ttu-id="5546c-130">Devido à utilização de Olá de Olá `[Authorize]` atributo, todos os métodos deste controlador só pode ser executado se Olá utilizador ser autenticado.</span><span class="sxs-lookup"><span data-stu-id="5546c-130">Because of hello use of hello `[Authorize]` attribute, all methods of this controller can only be executed if hello user is authenticated.</span></span> <span data-ttu-id="5546c-131">Se o utilizador Olá não é autenticado e tenta tooaccess controlador de Olá, OWIN irá iniciar um desafio de autenticação e forçar Olá tooauthenticate de utilizador.</span><span class="sxs-lookup"><span data-stu-id="5546c-131">If hello user is not authenticated and tries tooaccess hello controller, OWIN will initiate an authentication challenge and force hello user tooauthenticate.</span></span> <span data-ttu-id="5546c-132">coleção de Olá de afirmações de código Olá acima procura em Olá `ClaimsPrincipal.Current` instância para atributos de utilizador específico incluídas no token de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="5546c-132">hello code above looks at hello claims collection of hello `ClaimsPrincipal.Current` instance for specific user attributes included in hello user’s token.</span></span> <span data-ttu-id="5546c-133">Estes atributos incluem o nome completo do utilizador Olá e o nome de utilizador, bem como o requerente de identificador do utilizador global Olá.</span><span class="sxs-lookup"><span data-stu-id="5546c-133">These attributes include hello user’s full name and username, as well as hello global user identifier subject.</span></span> <span data-ttu-id="5546c-134">Também contém Olá *ID do inquilino*, que representa o ID de Olá para a organização do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="5546c-134">It also contains hello *Tenant ID*, which represents hello ID for hello user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a><span data-ttu-id="5546c-135">Criar uma vista de afirmações do utilizador Olá toodisplay</span><span class="sxs-lookup"><span data-stu-id="5546c-135">Create a view toodisplay hello user's claims</span></span>

<span data-ttu-id="5546c-136">No Visual Studio, crie uma nova vista de afirmações do utilizador Olá toodisplay numa página web:</span><span class="sxs-lookup"><span data-stu-id="5546c-136">In Visual Studio, create a new view toodisplay hello user's claims in a web page:</span></span>

1.  <span data-ttu-id="5546c-137">Clique com o botão direito do rato em Olá `Views\Claims` pasta e:`Add View`</span><span class="sxs-lookup"><span data-stu-id="5546c-137">Right click hello `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="5546c-138">Dê-lhe o nome `Index`.</span><span class="sxs-lookup"><span data-stu-id="5546c-138">Name it `Index`.</span></span>
3.  <span data-ttu-id="5546c-139">Adicione Olá seguintes HTML toohello ficheiro:</span><span class="sxs-lookup"><span data-stu-id="5546c-139">Add hello following HTML toohello file:</span></span>

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
