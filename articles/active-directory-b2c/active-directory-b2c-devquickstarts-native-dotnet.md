---
title: aaaAzure Active Directory B2C | Microsoft Docs
description: "Como toobuild uma aplicação de ambiente de trabalho do Windows que inclui o início de sessão, inscrição e gestão de perfis utilizando o Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>O Azure AD B2C: Criar uma aplicação de ambiente de trabalho do Windows
Ao utilizar o Azure Active Directory (Azure AD) B2C, pode adicionar a aplicação ambiente de trabalho de tooyour funcionalidades de gestão identidade poderosas self-service em poucos passos. Este artigo irá mostrar como toocreate uma aplicação .NET Windows Presentation Foundation (WPF) "lista de tarefas", que inclui a inscrição, início de sessão de utilizador e gestão de perfis. aplicação Olá irá incluir suporte para inscrição e o início de sessão utilizando um nome de utilizador ou o e-mail. Irá também inclui suporte para inscrição e o início de sessão através da utilização de contas de redes sociais como o Facebook e Google.

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório do Azure AD B2C
Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.  Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos, etc. Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.

## <a name="create-an-application"></a>Criar uma aplicação
Em seguida, terá de toocreate uma aplicação no diretório do B2C. Isto dá-informações do Azure AD que necessidades toosecurely comunicar com a sua aplicação. toocreate uma aplicação, siga [estas instruções](active-directory-b2c-app-registration.md).  É necessário:

* Incluir um **cliente nativo** na aplicação Olá.
* Olá cópia **URI de redirecionamento** `urn:ietf:wg:oauth:2.0:oob`. É Olá predefinido URL para este exemplo de código.
* Olá cópia **ID da aplicação** que é atribuído tooyour aplicação. Precisará dele mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar as políticas
No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md). Este exemplo de código contém três experiências de identidade: inscrever-se, iniciar sessão e Editar perfil. Terá de toocreate uma política para cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Quando criar Olá três políticas, não se esqueça de:

* Escolha o **inscrição de ID de utilizador** ou **E-Mail inscrição** no painel de fornecedores de identidade Olá.
* Escolher o **Nome a apresentar** e outros atributos de inscrição na sua política de inscrição.
* Escolher as afirmações **Nome a apresentar** e **ID de objeto** como afirmações de aplicação em cada política. Também pode escolher outras afirmações.
* Olá cópia **nome** de cada política depois de a criar. Deve ter o prefixo de Olá `b2c_1_`.  Precisará destes nomes de políticas mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois de criou com êxito Olá três políticas, está pronto toobuild a aplicação.

## <a name="download-hello-code"></a>Transferir o código de Olá
Olá código para este tutorial [é mantido no GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet). exemplo de Olá toobuild como vá, pode [transferir um projeto de estrutura como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip). Também pode clonar a estrutura de Olá:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

aplicação Olá concluída está também [disponível como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) ou Olá `complete` ramo do Olá mesmo repositório.

Depois de transferir o código de exemplo de Olá, abra Olá Visual Studio. sln ficheiro tooget foi iniciado. Olá `TaskClient` projeto é Olá aplicação de ambiente de trabalho do WPF que Olá utilizador interage com. Para efeitos de Olá deste tutorial, aquele invoca uma API, alojado no Azure, que armazena a lista de tarefas de cada utilizador da web de back-end tarefas.  Não é necessário toobuild Olá web API, já que poderemos ter funcionar para si.

toolearn como uma API web de forma segura efetua a autenticação de pedidos utilizando o Azure AD B2C, veja o [web API introdução artigo](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="execute-policies"></a>Executar políticas
A aplicação comunica com o Azure AD B2C através do envio de mensagens de autenticação que especificar política de Olá pretendem tooexecute como parte do pedido de Olá HTTP. Para aplicações de ambiente de trabalho de .NET, pode utilizar Olá pré-visualizar as mensagens de autenticação do biblioteca de autenticação da Microsoft (MSAL) toosend OAuth 2.0, executar políticas e obter tokens que APIs da web de chamada.

### <a name="install-msal"></a>Instalar MSAL
Adicionar MSAL toohello `TaskClient` projeto utilizando Olá consola do Gestor de pacotes do Visual Studio.

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>Introduza os seus detalhes do B2C
Ficheiro aberto Olá `Globals.cs` e substitua cada um dos valores de propriedade Olá com os seus próprios. Esta classe é utilizada ao longo `TaskClient` valores tooreference utilizada frequentemente.

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a>Criar Olá PublicClientApplication
classe principal de Olá da MSAL `PublicClientApplication`. Esta classe representa a sua aplicação no sistema de Olá, Azure AD B2C. Quando hello initalizes de aplicação, crie uma instância de `PublicClientApplication` no `MainWindow.xaml.cs`. Isto pode ser utilizado em toda a janela de Olá.

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a>Iniciar um fluxo de inscrição
Quando um utilizador optar por participar ativamente toosigns cópias de segurança, quer tooinitiate um fluxo de inscrição que utiliza a política de inscrição Olá que criou. Ao utilizar MSAL, apenas a chamar `pca.AcquireTokenAsync(...)`. Olá parâmetros passar demasiado`AcquireTokenAsync(...)` determinar qual token receber, política de Olá utilizada no pedido de autenticação de Olá e muito mais.

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }

            MessageBox.Show(message);
        }

        return;
    }
}
```

### <a name="initiate-a-sign-in-flow"></a>Iniciar um fluxo de início de sessão
Pode iniciar um fluxo de início de sessão no Olá mesma forma, se iniciar um fluxo de inscrição. Quando um utilizador inicia sessão, certifique-Olá mesmo chamar tooMSAL, desta vez utilizando a política de início de sessão:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a>Iniciar um fluxo de edição de perfil
Novamente, pode executar uma política de perfil de edição no Olá forma mesma:

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

Todas as nestes casos, MSAL está devolve um token no `AuthenticationResult` ou emite uma exceção. Sempre que a obter um token de MSAL, pode utilizar Olá `AuthenticationResult.User` tooupdate Olá utilizador dados na aplicação Olá, tais como Olá IU de objeto. ADAL também caches Olá token para utilização em outras partes da aplicação Olá.

### <a name="check-for-tokens-on-app-start"></a>Verifique a existência de tokens no início da aplicação
Também pode utilizar controlar de tookeep MSAL Olá do início de sessão do Estado do utilizador.  Nesta aplicação, queremos Olá tooremain de utilizador com sessão iniciada, mesmo depois de serem fechar aplicação Olá & volte a abrir.  Novamente no interior de Olá `OnInitialized` substituição, utilize do MSAL `AcquireTokenSilent` toocheck de método para tokens em cache:

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
    return;
}
```

## <a name="call-hello-task-api"></a>Chamar a API de tarefa Olá
Pode agora utilizar as políticas de tooexecute MSAL e obter tokens.  Quando pretender toouse uma API de tarefa estes tokens toocall Olá, pode utilizar novamente do MSAL `AcquireTokenSilent` toocheck de método para tokens em cache:

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
        }
        else
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }
            MessageBox.Show(message);
        }

        return;
    }
    ...
```

Quando Olá chamada demasiado`AcquireTokenSilentAsync(...)` for bem sucedida e um token for encontrado na cache de Olá, pode adicionar toohello token Olá `Authorization` cabeçalho de pedido de Olá HTTP. API de web de tarefa Olá irá utilizar a lista de tarefas de cabeçalho tooauthenticate Olá pedido tooread Olá deste utilizador:

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>Utilizador de Olá de início de sessão enviados
Por fim, pode utilizar MSAL tooend uma sessão do utilizador com a aplicação Olá quando o utilizador Olá seleciona **terminar sessão**.  Quando utilizar MSAL, isto é conseguido ao desmarcar todos os tokens de Olá da cache de token de Olá:

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a>Executar a aplicação de exemplo de Olá
Por fim, crie e execute o exemplo de Olá.  Inscrever-se para a aplicação Olá utilizando um nome de utilizador ou endereço de correio eletrónico. Termine sessão e voltar a iniciar sessão no como Olá mesmo utilizador. Edite perfil desse utilizador. Termine sessão e inscrever-se através de um utilizador diferente.

## <a name="add-social-idps"></a>Adicionar IDPs redes sociais
Atualmente, a aplicação Olá suporta apenas inscrição de utilizador e início de sessão que utilizam **contas locais**. Estas são contas armazenadas no diretório do B2C que utilizam um nome de utilizador e palavra-passe. Ao utilizar o Azure AD B2C, pode adicionar suporte para outros fornecedores de identidade (IDPs) sem alterar qualquer do seu código.

tooadd social IDPs tooyour aplicação, comece por seguir Olá detalhadas instruções nestes artigos. Para cada IDP pretende toosupport, necessita tooregister uma aplicação nesse sistema e obter um ID de cliente.

* [Configurar o Facebook como um IDP](active-directory-b2c-setup-fb-app.md)
* [Configurar o Google como um IDP](active-directory-b2c-setup-goog-app.md)
* [Configurar o Amazon como um IDP](active-directory-b2c-setup-amzn-app.md)
* [Configurar LinkedIn como um IDP](active-directory-b2c-setup-li-app.md)

Depois de adicionar o diretório de tooyour B2C de fornecedores de identidade Olá, terá de tooedit cada um dos seus três políticas tooinclude Olá IDPs novo, como descrita em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md). Depois de guardar as suas políticas, execute novamente a aplicação Olá. Deverá ver Olá que idps novo adicionados como opções de início de sessão e inscrição em cada uma das suas experiências de identidade.

Pode experimentar com as políticas e observar os efeitos de Olá na sua aplicação de exemplo. Adicionar ou remover IDPs, manipular afirmações de aplicação ou altere os atributos de inscrição. Experimentação até que pode ver como MSAL, pedidos de autenticação e políticas associar em conjunto.

Para referência, Olá concluída exemplo [é fornecido como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip). Também pode clonar a partir do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
