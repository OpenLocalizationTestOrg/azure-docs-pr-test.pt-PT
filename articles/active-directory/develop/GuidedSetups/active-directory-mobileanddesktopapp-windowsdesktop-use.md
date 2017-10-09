---
title: "aaaAzure AD v2 Windows Desktop introdução - utilização | Microsoft Docs"
description: "Como aplicações de .NET de ambiente de trabalho do Windows (XAML) podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
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
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="eb1f8-103">Utilizar Olá biblioteca de autenticação da Microsoft (MSAL) tooget um token para Olá Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="eb1f8-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="eb1f8-104">Esta secção mostra como toouse MSAL tooget um token Olá Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="eb1f8-105">No `MainWindow.xaml.cs`, adicione Olá referência para a classe de toohello MSAL biblioteca:</span><span class="sxs-lookup"><span data-stu-id="eb1f8-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="eb1f8-106">Substitua <code>MainWindow</code> classe código com:</span><span class="sxs-lookup"><span data-stu-id="eb1f8-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="eb1f8-107">Mais Informações</span><span class="sxs-lookup"><span data-stu-id="eb1f8-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="eb1f8-108">Obter um token de utilizador interativa</span><span class="sxs-lookup"><span data-stu-id="eb1f8-108">Getting a user token interactive</span></span>
<span data-ttu-id="eb1f8-109">Chamar Olá `AcquireTokenAsync` resultados de método numa janela solicitando Olá toosign de utilizador no.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="eb1f8-110">Aplicações normalmente necessitam de um utilizador toosign no interativamente Olá pela primeira vez que precisam tooaccess um recurso protegido ou quando uma operação automática tooacquire um token de falha (por exemplo, palavra-passe do utilizador Olá expirou).</span><span class="sxs-lookup"><span data-stu-id="eb1f8-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="eb1f8-111">A obter um utilizador token automaticamente</span><span class="sxs-lookup"><span data-stu-id="eb1f8-111">Getting a user token silently</span></span>
<span data-ttu-id="eb1f8-112">`AcquireTokenSilentAsync`processa aquisições token e a renovação sem qualquer interação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="eb1f8-113">Depois de `AcquireTokenAsync` é executado para Olá pela primeira vez, `AcquireTokenSilentAsync` Olá método habitual utilizado tooobtain tokens utilizados tooaccess protegido recursos para as chamadas subsequentes - como toorequest chamadas ou renovar tokens são efetuadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="eb1f8-114">Eventualmente, `AcquireTokenSilentAsync` falhará – por exemplo, o utilizador Olá foi terminada, ou foi alterada a palavra-passe noutro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="eb1f8-115">Quando MSAL Deteta que é possível resolver o problema de Olá exigindo uma ação interativa, é acionado um `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="eb1f8-116">A aplicação pode processar esta exceção de duas formas:</span><span class="sxs-lookup"><span data-stu-id="eb1f8-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="eb1f8-117">Efetuar uma chamada contra `AcquireTokenAsync` imediatamente, que resulta num utilizador Olá toosign-na pedir.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="eb1f8-118">Este padrão é normalmente utilizado nas aplicações online em que não existe nenhum conteúdo offline na aplicação Olá disponíveis para Olá utilizador.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="eb1f8-119">Olá exemplo gerado por esta configuração orientada utiliza este padrão: pode vê-lo na Olá ação pela primeira vez que executar o exemplo de Olá: porque nenhum utilizador alguma vez utilizado a aplicação Olá, `PublicClientApp.Users.FirstOrDefault()` irá conter um valor nulo e um `MsalUiRequiredException` exceção será emitida.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="eb1f8-120">Olá, código de exemplo de Olá, em seguida, identificadores Olá exceção ao chamar `AcquireTokenAsync` resultando num utilizador Olá toosign-na pedir.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="eb1f8-121">Aplicações podem também efetuar um utilizador de toohello indicação visual que um interativa início de sessão é necessário, para que o utilizador Olá pode seleccionar Olá momento toosign no, ou pode tentar novamente a aplicação Olá `AcquireTokenSilentAsync` numa altura posterior.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="eb1f8-122">Isto é normalmente utilizado quando o utilizador Olá pode utilizar outras funcionalidades da aplicação Olá sem ser interrompidos, por exemplo, não há conteúdo offline na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="eb1f8-123">Neste caso, o utilizador Olá pode decidir quando pretendem toosign no recurso de Olá protegido tooaccess, toorefresh Olá desatualizada informações ou para a aplicação pode decidir tooretry `AcquireTokenSilentAsync` quando a rede é restaurada após está temporariamente indisponível.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="eb1f8-124">Chamar Olá Microsoft Graph API a utilizar o token de Olá que apenas obteve</span><span class="sxs-lookup"><span data-stu-id="eb1f8-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="eb1f8-125">Adicionar novo método de Olá abaixo tooyour `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="eb1f8-126">Olá método é toomake utilizado um `GET` pedido em relação a Graph API utilizando um cabeçalho de autorizar:</span><span class="sxs-lookup"><span data-stu-id="eb1f8-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="eb1f8-127">Obter mais informações sobre como efetuar uma chamada REST em relação a uma API protegida</span><span class="sxs-lookup"><span data-stu-id="eb1f8-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="eb1f8-128">Esta aplicação de exemplo Olá `GetHttpContentWithToken` método é utilizado toomake um HTTP `GET` pedido contra um recurso protegido que necessita de um autor da chamada do token e, em seguida, retorno Olá toohello conteúdo.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="eb1f8-129">Este método adiciona ao token de Olá adquirida Olá *cabeçalho de autorização de HTTP*.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="eb1f8-130">Para este exemplo, o recurso de Olá é Olá Microsoft Graph API *-me* ponto final – apresenta informações de perfil do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="eb1f8-131">Adicionar um toosign método saída utilizador Olá</span><span class="sxs-lookup"><span data-stu-id="eb1f8-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="eb1f8-132">Adicionar Olá seguinte método tooyour `MainWindow.xaml.cs` toosign saída utilizador Olá:</span><span class="sxs-lookup"><span data-stu-id="eb1f8-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

```csharp
/// <summary>
/// Sign out hello current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="eb1f8-133">Obter mais informações sobre o fim de sessão</span><span class="sxs-lookup"><span data-stu-id="eb1f8-133">More info on Sign-Out</span></span>

<span data-ttu-id="eb1f8-134">`SignOutButton_Click`Remove Olá utilizador da cache de utilizador MSAL – isto eficazmente informará o utilizador atual do MSAL tooforget Olá para que um pedido futuras tooacquire um token apenas terá êxito se este for efetuada toobe interativo.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="eb1f8-135">Embora a aplicação Olá neste exemplo suporta um único utilizador, MSAL suporta cenários em que várias contas podem ser com sessão iniciada em Olá simultâneo – um exemplo é uma aplicação de e-mail em que um utilizador tem várias contas.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="eb1f8-136">Apresentar as informações do Token básicas</span><span class="sxs-lookup"><span data-stu-id="eb1f8-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="eb1f8-137">Adicionar Olá seguinte método tootooyour `MainWindow.xaml.cs` toodisplay informações básicas sobre o token de Olá:</span><span class="sxs-lookup"><span data-stu-id="eb1f8-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in hello token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="eb1f8-138">Mais Informações</span><span class="sxs-lookup"><span data-stu-id="eb1f8-138">More Information</span></span>

<span data-ttu-id="eb1f8-139">Tokens adquirido através de *OpenID Connect* também conter um pequeno subconjunto de utilizadores de toohello pertinentes de informações.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="eb1f8-140">`DisplayBasicTokenInfo`Mostra informações básicas contidas no token de Olá: por exemplo, do utilizador Olá apresentar o nome e o ID, bem como Olá cadeia de data e Olá de expiração do token que representa o token de acesso de Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="eb1f8-141">Estas informações são apresentadas para toosee.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="eb1f8-142">Pode clicar em Olá *chamar Microsoft Graph API* botão várias vezes e ver que Olá mesmo token foi reutilizado em pedidos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="eb1f8-143">Também pode ver a data de expiração de Olá a ser expandida quando MSAL decide é token de Olá toorenew de tempo.</span><span class="sxs-lookup"><span data-stu-id="eb1f8-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

