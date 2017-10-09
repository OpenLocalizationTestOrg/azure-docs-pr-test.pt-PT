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
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="758d7-103">O Azure AD B2C: Criar uma aplicação de ambiente de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="758d7-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="758d7-104">Ao utilizar o Azure Active Directory (Azure AD) B2C, pode adicionar a aplicação ambiente de trabalho de tooyour funcionalidades de gestão identidade poderosas self-service em poucos passos.</span><span class="sxs-lookup"><span data-stu-id="758d7-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="758d7-105">Este artigo irá mostrar como toocreate uma aplicação .NET Windows Presentation Foundation (WPF) "lista de tarefas", que inclui a inscrição, início de sessão de utilizador e gestão de perfis.</span><span class="sxs-lookup"><span data-stu-id="758d7-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="758d7-106">aplicação Olá irá incluir suporte para inscrição e o início de sessão utilizando um nome de utilizador ou o e-mail.</span><span class="sxs-lookup"><span data-stu-id="758d7-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="758d7-107">Irá também inclui suporte para inscrição e o início de sessão através da utilização de contas de redes sociais como o Facebook e Google.</span><span class="sxs-lookup"><span data-stu-id="758d7-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="758d7-108">Obter um diretório do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="758d7-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="758d7-109">Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.</span><span class="sxs-lookup"><span data-stu-id="758d7-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="758d7-110">Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="758d7-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="758d7-111">Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="758d7-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="758d7-112">Criar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="758d7-112">Create an application</span></span>
<span data-ttu-id="758d7-113">Em seguida, terá de toocreate uma aplicação no diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="758d7-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="758d7-114">Isto dá-informações do Azure AD que necessidades toosecurely comunicar com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="758d7-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="758d7-115">toocreate uma aplicação, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="758d7-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="758d7-116">É necessário:</span><span class="sxs-lookup"><span data-stu-id="758d7-116">Be sure to:</span></span>

* <span data-ttu-id="758d7-117">Incluir um **cliente nativo** na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="758d7-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="758d7-118">Olá cópia **URI de redirecionamento** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="758d7-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="758d7-119">É Olá predefinido URL para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="758d7-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="758d7-120">Olá cópia **ID da aplicação** que é atribuído tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="758d7-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="758d7-121">Precisará dele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="758d7-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="758d7-122">Criar as políticas</span><span class="sxs-lookup"><span data-stu-id="758d7-122">Create your policies</span></span>
<span data-ttu-id="758d7-123">No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="758d7-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="758d7-124">Este exemplo de código contém três experiências de identidade: inscrever-se, iniciar sessão e Editar perfil.</span><span class="sxs-lookup"><span data-stu-id="758d7-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="758d7-125">Terá de toocreate uma política para cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="758d7-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="758d7-126">Quando criar Olá três políticas, não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="758d7-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="758d7-127">Escolha o **inscrição de ID de utilizador** ou **E-Mail inscrição** no painel de fornecedores de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="758d7-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="758d7-128">Escolher o **Nome a apresentar** e outros atributos de inscrição na sua política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="758d7-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="758d7-129">Escolher as afirmações **Nome a apresentar** e **ID de objeto** como afirmações de aplicação em cada política.</span><span class="sxs-lookup"><span data-stu-id="758d7-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="758d7-130">Também pode escolher outras afirmações.</span><span class="sxs-lookup"><span data-stu-id="758d7-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="758d7-131">Olá cópia **nome** de cada política depois de a criar.</span><span class="sxs-lookup"><span data-stu-id="758d7-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="758d7-132">Deve ter o prefixo de Olá `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="758d7-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="758d7-133">Precisará destes nomes de políticas mais tarde.</span><span class="sxs-lookup"><span data-stu-id="758d7-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="758d7-134">Depois de criou com êxito Olá três políticas, está pronto toobuild a aplicação.</span><span class="sxs-lookup"><span data-stu-id="758d7-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="758d7-135">Transferir o código de Olá</span><span class="sxs-lookup"><span data-stu-id="758d7-135">Download hello code</span></span>
<span data-ttu-id="758d7-136">Olá código para este tutorial [é mantido no GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="758d7-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="758d7-137">exemplo de Olá toobuild como vá, pode [transferir um projeto de estrutura como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="758d7-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="758d7-138">Também pode clonar a estrutura de Olá:</span><span class="sxs-lookup"><span data-stu-id="758d7-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="758d7-139">aplicação Olá concluída está também [disponível como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) ou Olá `complete` ramo do Olá mesmo repositório.</span><span class="sxs-lookup"><span data-stu-id="758d7-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="758d7-140">Depois de transferir o código de exemplo de Olá, abra Olá Visual Studio. sln ficheiro tooget foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="758d7-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="758d7-141">Olá `TaskClient` projeto é Olá aplicação de ambiente de trabalho do WPF que Olá utilizador interage com.</span><span class="sxs-lookup"><span data-stu-id="758d7-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="758d7-142">Para efeitos de Olá deste tutorial, aquele invoca uma API, alojado no Azure, que armazena a lista de tarefas de cada utilizador da web de back-end tarefas.</span><span class="sxs-lookup"><span data-stu-id="758d7-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="758d7-143">Não é necessário toobuild Olá web API, já que poderemos ter funcionar para si.</span><span class="sxs-lookup"><span data-stu-id="758d7-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="758d7-144">toolearn como uma API web de forma segura efetua a autenticação de pedidos utilizando o Azure AD B2C, veja o [web API introdução artigo](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="758d7-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="758d7-145">Executar políticas</span><span class="sxs-lookup"><span data-stu-id="758d7-145">Execute policies</span></span>
<span data-ttu-id="758d7-146">A aplicação comunica com o Azure AD B2C através do envio de mensagens de autenticação que especificar política de Olá pretendem tooexecute como parte do pedido de Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="758d7-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="758d7-147">Para aplicações de ambiente de trabalho de .NET, pode utilizar Olá pré-visualizar as mensagens de autenticação do biblioteca de autenticação da Microsoft (MSAL) toosend OAuth 2.0, executar políticas e obter tokens que APIs da web de chamada.</span><span class="sxs-lookup"><span data-stu-id="758d7-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="758d7-148">Instalar MSAL</span><span class="sxs-lookup"><span data-stu-id="758d7-148">Install MSAL</span></span>
<span data-ttu-id="758d7-149">Adicionar MSAL toohello `TaskClient` projeto utilizando Olá consola do Gestor de pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="758d7-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="758d7-150">Introduza os seus detalhes do B2C</span><span class="sxs-lookup"><span data-stu-id="758d7-150">Enter your B2C details</span></span>
<span data-ttu-id="758d7-151">Ficheiro aberto Olá `Globals.cs` e substitua cada um dos valores de propriedade Olá com os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="758d7-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="758d7-152">Esta classe é utilizada ao longo `TaskClient` valores tooreference utilizada frequentemente.</span><span class="sxs-lookup"><span data-stu-id="758d7-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

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

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="758d7-153">Criar Olá PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="758d7-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="758d7-154">classe principal de Olá da MSAL `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="758d7-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="758d7-155">Esta classe representa a sua aplicação no sistema de Olá, Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="758d7-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="758d7-156">Quando hello initalizes de aplicação, crie uma instância de `PublicClientApplication` no `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="758d7-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="758d7-157">Isto pode ser utilizado em toda a janela de Olá.</span><span class="sxs-lookup"><span data-stu-id="758d7-157">This can be used throughout hello window.</span></span>

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

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="758d7-158">Iniciar um fluxo de inscrição</span><span class="sxs-lookup"><span data-stu-id="758d7-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="758d7-159">Quando um utilizador optar por participar ativamente toosigns cópias de segurança, quer tooinitiate um fluxo de inscrição que utiliza a política de inscrição Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="758d7-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="758d7-160">Ao utilizar MSAL, apenas a chamar `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="758d7-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="758d7-161">Olá parâmetros passar demasiado`AcquireTokenAsync(...)` determinar qual token receber, política de Olá utilizada no pedido de autenticação de Olá e muito mais.</span><span class="sxs-lookup"><span data-stu-id="758d7-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="758d7-162">Iniciar um fluxo de início de sessão</span><span class="sxs-lookup"><span data-stu-id="758d7-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="758d7-163">Pode iniciar um fluxo de início de sessão no Olá mesma forma, se iniciar um fluxo de inscrição.</span><span class="sxs-lookup"><span data-stu-id="758d7-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="758d7-164">Quando um utilizador inicia sessão, certifique-Olá mesmo chamar tooMSAL, desta vez utilizando a política de início de sessão:</span><span class="sxs-lookup"><span data-stu-id="758d7-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="758d7-165">Iniciar um fluxo de edição de perfil</span><span class="sxs-lookup"><span data-stu-id="758d7-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="758d7-166">Novamente, pode executar uma política de perfil de edição no Olá forma mesma:</span><span class="sxs-lookup"><span data-stu-id="758d7-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

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

<span data-ttu-id="758d7-167">Todas as nestes casos, MSAL está devolve um token no `AuthenticationResult` ou emite uma exceção.</span><span class="sxs-lookup"><span data-stu-id="758d7-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="758d7-168">Sempre que a obter um token de MSAL, pode utilizar Olá `AuthenticationResult.User` tooupdate Olá utilizador dados na aplicação Olá, tais como Olá IU de objeto.</span><span class="sxs-lookup"><span data-stu-id="758d7-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="758d7-169">ADAL também caches Olá token para utilização em outras partes da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="758d7-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="758d7-170">Verifique a existência de tokens no início da aplicação</span><span class="sxs-lookup"><span data-stu-id="758d7-170">Check for tokens on app start</span></span>
<span data-ttu-id="758d7-171">Também pode utilizar controlar de tookeep MSAL Olá do início de sessão do Estado do utilizador.</span><span class="sxs-lookup"><span data-stu-id="758d7-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="758d7-172">Nesta aplicação, queremos Olá tooremain de utilizador com sessão iniciada, mesmo depois de serem fechar aplicação Olá & volte a abrir.</span><span class="sxs-lookup"><span data-stu-id="758d7-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="758d7-173">Novamente no interior de Olá `OnInitialized` substituição, utilize do MSAL `AcquireTokenSilent` toocheck de método para tokens em cache:</span><span class="sxs-lookup"><span data-stu-id="758d7-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

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

## <a name="call-hello-task-api"></a><span data-ttu-id="758d7-174">Chamar a API de tarefa Olá</span><span class="sxs-lookup"><span data-stu-id="758d7-174">Call hello task API</span></span>
<span data-ttu-id="758d7-175">Pode agora utilizar as políticas de tooexecute MSAL e obter tokens.</span><span class="sxs-lookup"><span data-stu-id="758d7-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="758d7-176">Quando pretender toouse uma API de tarefa estes tokens toocall Olá, pode utilizar novamente do MSAL `AcquireTokenSilent` toocheck de método para tokens em cache:</span><span class="sxs-lookup"><span data-stu-id="758d7-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

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

<span data-ttu-id="758d7-177">Quando Olá chamada demasiado`AcquireTokenSilentAsync(...)` for bem sucedida e um token for encontrado na cache de Olá, pode adicionar toohello token Olá `Authorization` cabeçalho de pedido de Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="758d7-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="758d7-178">API de web de tarefa Olá irá utilizar a lista de tarefas de cabeçalho tooauthenticate Olá pedido tooread Olá deste utilizador:</span><span class="sxs-lookup"><span data-stu-id="758d7-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="758d7-179">Utilizador de Olá de início de sessão enviados</span><span class="sxs-lookup"><span data-stu-id="758d7-179">Sign hello user out</span></span>
<span data-ttu-id="758d7-180">Por fim, pode utilizar MSAL tooend uma sessão do utilizador com a aplicação Olá quando o utilizador Olá seleciona **terminar sessão**.  Quando utilizar MSAL, isto é conseguido ao desmarcar todos os tokens de Olá da cache de token de Olá:</span><span class="sxs-lookup"><span data-stu-id="758d7-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

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

## <a name="run-hello-sample-app"></a><span data-ttu-id="758d7-181">Executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="758d7-181">Run hello sample app</span></span>
<span data-ttu-id="758d7-182">Por fim, crie e execute o exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="758d7-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="758d7-183">Inscrever-se para a aplicação Olá utilizando um nome de utilizador ou endereço de correio eletrónico.</span><span class="sxs-lookup"><span data-stu-id="758d7-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="758d7-184">Termine sessão e voltar a iniciar sessão no como Olá mesmo utilizador.</span><span class="sxs-lookup"><span data-stu-id="758d7-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="758d7-185">Edite perfil desse utilizador.</span><span class="sxs-lookup"><span data-stu-id="758d7-185">Edit that user's profile.</span></span> <span data-ttu-id="758d7-186">Termine sessão e inscrever-se através de um utilizador diferente.</span><span class="sxs-lookup"><span data-stu-id="758d7-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="758d7-187">Adicionar IDPs redes sociais</span><span class="sxs-lookup"><span data-stu-id="758d7-187">Add social IDPs</span></span>
<span data-ttu-id="758d7-188">Atualmente, a aplicação Olá suporta apenas inscrição de utilizador e início de sessão que utilizam **contas locais**.</span><span class="sxs-lookup"><span data-stu-id="758d7-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="758d7-189">Estas são contas armazenadas no diretório do B2C que utilizam um nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="758d7-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="758d7-190">Ao utilizar o Azure AD B2C, pode adicionar suporte para outros fornecedores de identidade (IDPs) sem alterar qualquer do seu código.</span><span class="sxs-lookup"><span data-stu-id="758d7-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="758d7-191">tooadd social IDPs tooyour aplicação, comece por seguir Olá detalhadas instruções nestes artigos.</span><span class="sxs-lookup"><span data-stu-id="758d7-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="758d7-192">Para cada IDP pretende toosupport, necessita tooregister uma aplicação nesse sistema e obter um ID de cliente.</span><span class="sxs-lookup"><span data-stu-id="758d7-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="758d7-193">Configurar o Facebook como um IDP</span><span class="sxs-lookup"><span data-stu-id="758d7-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="758d7-194">Configurar o Google como um IDP</span><span class="sxs-lookup"><span data-stu-id="758d7-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="758d7-195">Configurar o Amazon como um IDP</span><span class="sxs-lookup"><span data-stu-id="758d7-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="758d7-196">Configurar LinkedIn como um IDP</span><span class="sxs-lookup"><span data-stu-id="758d7-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="758d7-197">Depois de adicionar o diretório de tooyour B2C de fornecedores de identidade Olá, terá de tooedit cada um dos seus três políticas tooinclude Olá IDPs novo, como descrita em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="758d7-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="758d7-198">Depois de guardar as suas políticas, execute novamente a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="758d7-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="758d7-199">Deverá ver Olá que idps novo adicionados como opções de início de sessão e inscrição em cada uma das suas experiências de identidade.</span><span class="sxs-lookup"><span data-stu-id="758d7-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="758d7-200">Pode experimentar com as políticas e observar os efeitos de Olá na sua aplicação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="758d7-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="758d7-201">Adicionar ou remover IDPs, manipular afirmações de aplicação ou altere os atributos de inscrição.</span><span class="sxs-lookup"><span data-stu-id="758d7-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="758d7-202">Experimentação até que pode ver como MSAL, pedidos de autenticação e políticas associar em conjunto.</span><span class="sxs-lookup"><span data-stu-id="758d7-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="758d7-203">Para referência, Olá concluída exemplo [é fornecido como um ficheiro. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="758d7-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="758d7-204">Também pode clonar a partir do GitHub:</span><span class="sxs-lookup"><span data-stu-id="758d7-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
