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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Utilizar Olá biblioteca de autenticação da Microsoft (MSAL) tooget um token para Olá Microsoft Graph API

Esta secção mostra como toouse MSAL tooget um token Olá Microsoft Graph API.

1.  No `MainWindow.xaml.cs`, adicione Olá referência para a classe de toohello MSAL biblioteca:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Substitua <code>MainWindow</code> classe código com:
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
### <a name="more-information"></a>Mais Informações
#### <a name="getting-a-user-token-interactive"></a>Obter um token de utilizador interativa
Chamar Olá `AcquireTokenAsync` resultados de método numa janela solicitando Olá toosign de utilizador no. Aplicações normalmente necessitam de um utilizador toosign no interativamente Olá pela primeira vez que precisam tooaccess um recurso protegido ou quando uma operação automática tooacquire um token de falha (por exemplo, palavra-passe do utilizador Olá expirou).

#### <a name="getting-a-user-token-silently"></a>A obter um utilizador token automaticamente
`AcquireTokenSilentAsync`processa aquisições token e a renovação sem qualquer interação do utilizador. Depois de `AcquireTokenAsync` é executado para Olá pela primeira vez, `AcquireTokenSilentAsync` Olá método habitual utilizado tooobtain tokens utilizados tooaccess protegido recursos para as chamadas subsequentes - como toorequest chamadas ou renovar tokens são efetuadas automaticamente.
Eventualmente, `AcquireTokenSilentAsync` falhará – por exemplo, o utilizador Olá foi terminada, ou foi alterada a palavra-passe noutro dispositivo. Quando MSAL Deteta que é possível resolver o problema de Olá exigindo uma ação interativa, é acionado um `MsalUiRequiredException`. A aplicação pode processar esta exceção de duas formas:

1.  Efetuar uma chamada contra `AcquireTokenAsync` imediatamente, que resulta num utilizador Olá toosign-na pedir. Este padrão é normalmente utilizado nas aplicações online em que não existe nenhum conteúdo offline na aplicação Olá disponíveis para Olá utilizador. Olá exemplo gerado por esta configuração orientada utiliza este padrão: pode vê-lo na Olá ação pela primeira vez que executar o exemplo de Olá: porque nenhum utilizador alguma vez utilizado a aplicação Olá, `PublicClientApp.Users.FirstOrDefault()` irá conter um valor nulo e um `MsalUiRequiredException` exceção será emitida. Olá, código de exemplo de Olá, em seguida, identificadores Olá exceção ao chamar `AcquireTokenAsync` resultando num utilizador Olá toosign-na pedir.

2.  Aplicações podem também efetuar um utilizador de toohello indicação visual que um interativa início de sessão é necessário, para que o utilizador Olá pode seleccionar Olá momento toosign no, ou pode tentar novamente a aplicação Olá `AcquireTokenSilentAsync` numa altura posterior. Isto é normalmente utilizado quando o utilizador Olá pode utilizar outras funcionalidades da aplicação Olá sem ser interrompidos, por exemplo, não há conteúdo offline na aplicação Olá. Neste caso, o utilizador Olá pode decidir quando pretendem toosign no recurso de Olá protegido tooaccess, toorefresh Olá desatualizada informações ou para a aplicação pode decidir tooretry `AcquireTokenSilentAsync` quando a rede é restaurada após está temporariamente indisponível.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chamar Olá Microsoft Graph API a utilizar o token de Olá que apenas obteve

1. Adicionar novo método de Olá abaixo tooyour `MainWindow.xaml.cs`. Olá método é toomake utilizado um `GET` pedido em relação a Graph API utilizando um cabeçalho de autorizar:

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Obter mais informações sobre como efetuar uma chamada REST em relação a uma API protegida

Esta aplicação de exemplo Olá `GetHttpContentWithToken` método é utilizado toomake um HTTP `GET` pedido contra um recurso protegido que necessita de um autor da chamada do token e, em seguida, retorno Olá toohello conteúdo. Este método adiciona ao token de Olá adquirida Olá *cabeçalho de autorização de HTTP*. Para este exemplo, o recurso de Olá é Olá Microsoft Graph API *-me* ponto final – apresenta informações de perfil do utilizador Olá.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Adicionar um toosign método saída utilizador Olá

1. Adicionar Olá seguinte método tooyour `MainWindow.xaml.cs` toosign saída utilizador Olá:

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
### <a name="more-info-on-sign-out"></a>Obter mais informações sobre o fim de sessão

`SignOutButton_Click`Remove Olá utilizador da cache de utilizador MSAL – isto eficazmente informará o utilizador atual do MSAL tooforget Olá para que um pedido futuras tooacquire um token apenas terá êxito se este for efetuada toobe interativo.
Embora a aplicação Olá neste exemplo suporta um único utilizador, MSAL suporta cenários em que várias contas podem ser com sessão iniciada em Olá simultâneo – um exemplo é uma aplicação de e-mail em que um utilizador tem várias contas.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>Apresentar as informações do Token básicas

1. Adicionar Olá seguinte método tootooyour `MainWindow.xaml.cs` toodisplay informações básicas sobre o token de Olá:

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
### <a name="more-information"></a>Mais Informações

Tokens adquirido através de *OpenID Connect* também conter um pequeno subconjunto de utilizadores de toohello pertinentes de informações. `DisplayBasicTokenInfo`Mostra informações básicas contidas no token de Olá: por exemplo, do utilizador Olá apresentar o nome e o ID, bem como Olá cadeia de data e Olá de expiração do token que representa o token de acesso de Olá próprio. Estas informações são apresentadas para toosee. Pode clicar em Olá *chamar Microsoft Graph API* botão várias vezes e ver que Olá mesmo token foi reutilizado em pedidos subsequentes. Também pode ver a data de expiração de Olá a ser expandida quando MSAL decide é token de Olá toorenew de tempo.
<!--end-collapse-->

