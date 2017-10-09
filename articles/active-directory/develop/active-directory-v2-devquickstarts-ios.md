---
title: "utilizando a aplicação aaaAdd início de sessão tooan iOS Olá ponto final de v 2.0 do Azure AD | Microsoft Docs"
description: "Como toobuild uma aplicação iOS que inicia sessão utilizadores com ambos os conta pessoal da Microsoft e contas profissionais ou escolares através da utilização de bibliotecas de terceiros."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="80254-103">Adicionar a aplicação do iOS de início de sessão tooan utilizando uma biblioteca de terceiros com Graph API utilizando o ponto final de v 2.0 Olá</span><span class="sxs-lookup"><span data-stu-id="80254-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="80254-104">plataforma de identidade do Microsoft Olá utiliza as normas de abertura, como o OAuth2 e o OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="80254-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="80254-105">Os programadores podem utilizar qualquer biblioteca que pretendem toointegrate aos nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="80254-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="80254-106">os programadores de toohelp utilizam nossa plataforma com outras bibliotecas, escrevemos algumas instruções como esta um toodemonstrate como plataforma de identidade do Microsoft tooconnect toohello tooconfigure bibliotecas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="80254-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="80254-107">A maioria das bibliotecas que implementam [spec Olá especificação RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) pode ligar-se a plataforma de identidade do Microsoft toohello.</span><span class="sxs-lookup"><span data-stu-id="80254-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="80254-108">Com a aplicação Olá que cria esta explicação passo a passo, os utilizadores podem iniciar sessão tootheir organização e, em seguida, procure outras pessoas na sua organização utilizando Olá Graph API.</span><span class="sxs-lookup"><span data-stu-id="80254-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="80254-109">Se tiver tooOAuth2 novo ou o OpenID Connect, muito este exemplo de configuração poderá não fazer sentido tooyou.</span><span class="sxs-lookup"><span data-stu-id="80254-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="80254-110">Recomendamos que leia [protocolos de v 2.0 - fluxo de código do OAuth 2.0 autorização](active-directory-v2-protocols-oauth-code.md) para em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="80254-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="80254-111">Algumas funcionalidades da nossa plataforma que têm uma expressão num Olá OAuth2 ou o OpenID Connect normas, como o acesso condicional e gestão de políticas do Intune, requerem toouse nosso bibliotecas de identidade do Microsoft Azure de código aberto.</span><span class="sxs-lookup"><span data-stu-id="80254-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="80254-112">ponto final de v 2.0 Olá não suporta todos os cenários do Azure Active Directory e funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="80254-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="80254-113">toodetermine se deve utilizar o ponto final de v 2.0 Olá, leia sobre [limitações de v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="80254-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="80254-114">Transferir o código a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="80254-114">Download code from GitHub</span></span>
<span data-ttu-id="80254-115">código Olá deste tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="80254-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="80254-116">toofollow ao longo, pode [transferir a estrutura da aplicação Olá como um. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou estrutura de Olá do clone:</span><span class="sxs-lookup"><span data-stu-id="80254-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="80254-117">Pode também simplesmente transferir exemplo Olá e começar imediatamente:</span><span class="sxs-lookup"><span data-stu-id="80254-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="80254-118">Registar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="80254-118">Register an app</span></span>
<span data-ttu-id="80254-119">Criar uma nova aplicação Olá [portal de registo de aplicação](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga Olá os passos detalhados em [como tooregister uma aplicação com o ponto final de v 2.0 Olá](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="80254-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="80254-120">Certifique-se de que:</span><span class="sxs-lookup"><span data-stu-id="80254-120">Make sure to:</span></span>

* <span data-ttu-id="80254-121">Olá cópia **Id da aplicação** que é atribuído tooyour aplicação porque irá precisar das mesmas em breve.</span><span class="sxs-lookup"><span data-stu-id="80254-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="80254-122">Adicionar Olá **Mobile** plataforma para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="80254-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="80254-123">Olá cópia **URI de redirecionamento** do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="80254-124">Tem de utilizar o valor predefinido Olá `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="80254-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="80254-125">Transferir Olá terceiros NXOAuth2 biblioteca e criar uma área de trabalho</span><span class="sxs-lookup"><span data-stu-id="80254-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="80254-126">Nestas instruções, irá utilizar Olá OAuth2Client do GitHub, o que é uma biblioteca OAuth2 para Mac OS X e iOS (Cocoa e Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="80254-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="80254-127">Esta biblioteca é baseada no rascunho 10 da especificação do OAuth2 de Olá. Implementa o perfil de aplicação nativa Olá e suporta o ponto final de autorização de Olá do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="80254-128">Estes são todos os aspetos de Olá, terá de toointegrate com a plataforma de identidade do Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="80254-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="80254-129">Adicione o projeto de tooyour da biblioteca de Olá utilizando o CocoaPods</span><span class="sxs-lookup"><span data-stu-id="80254-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="80254-130">O CocoaPods é um gestor de dependência para projetos do Xcode.</span><span class="sxs-lookup"><span data-stu-id="80254-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="80254-131">Gere automaticamente os passos de instalação anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="80254-132">Adicione Olá toothis podfile os seguintes:</span><span class="sxs-lookup"><span data-stu-id="80254-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="80254-133">Carregue o podfile Olá utilizando o CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="80254-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="80254-134">Isto irá criar uma área de trabalho Xcode nova que irá carregar.</span><span class="sxs-lookup"><span data-stu-id="80254-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="80254-135">Explorar a estrutura de Olá do projeto de Olá</span><span class="sxs-lookup"><span data-stu-id="80254-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="80254-136">Olá seguir a estrutura está configurado para o nosso projeto na estrutura de Olá:</span><span class="sxs-lookup"><span data-stu-id="80254-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="80254-137">Uma vista principal com uma pesquisa UPN</span><span class="sxs-lookup"><span data-stu-id="80254-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="80254-138">Uma vista de detalhes para os dados de Olá sobre o utilizador selecionado Olá</span><span class="sxs-lookup"><span data-stu-id="80254-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="80254-139">Uma vista de início de sessão em que um utilizador pode iniciar sessão no gráfico de Olá toohello aplicação tooquery</span><span class="sxs-lookup"><span data-stu-id="80254-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="80254-140">Iremos irá mover ficheiros toovarious na autenticação de estrutura tooadd Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="80254-141">Outras partes do código Olá, tais como o código visual Olá, não dizem respeito tooidentity mas são fornecidas por si.</span><span class="sxs-lookup"><span data-stu-id="80254-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="80254-142">Configurar o ficheiro de settings.plst Olá na biblioteca de Olá</span><span class="sxs-lookup"><span data-stu-id="80254-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="80254-143">No projeto de início rápido de Olá, abra Olá `settings.plist` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="80254-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="80254-144">Substitua os valores de Olá de elementos Olá Olá secção tooreflect Olá os valores que utilizou na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="80254-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="80254-145">O código será referenciar estes valores, sempre que utiliza Olá biblioteca de autenticação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="80254-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="80254-146">Olá `clientId` é Olá ID de cliente da aplicação que copiou do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="80254-147">Olá `redirectUri` é o URL de redirecionamento Olá desse portal Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="80254-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="80254-148">Configurar a biblioteca NXOAuth2Client de Olá no seu LoginViewController</span><span class="sxs-lookup"><span data-stu-id="80254-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="80254-149">biblioteca de NXOAuth2Client Olá requer tooget alguns valores de multimédia.</span><span class="sxs-lookup"><span data-stu-id="80254-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="80254-150">Depois de concluir essa tarefa, pode utilizar Olá de adquiridas toocall token Olá Graph API.</span><span class="sxs-lookup"><span data-stu-id="80254-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="80254-151">Porque `LoginView` será chamado sempre que precisamos tooauthenticate, faz sentido tooput valores de configuração no ficheiro toothat.</span><span class="sxs-lookup"><span data-stu-id="80254-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="80254-152">Vamos adicionar alguns valores toohello `LoginViewController.m` contexto de Olá ficheiro tooset para autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="80254-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="80254-153">Detalhes sobre os valores de Olá siga código Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-153">Details about hello values follow hello code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="80254-154">Vamos ver detalhes sobre o código de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="80254-155">destina-se a primeira cadeia de Olá `scopes`.</span><span class="sxs-lookup"><span data-stu-id="80254-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="80254-156">Olá `User.Read` valor permite-lhe tooread Olá básico perfil Olá sessão do utilizador.</span><span class="sxs-lookup"><span data-stu-id="80254-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="80254-157">Pode saber mais sobre todos os âmbitos disponíveis Olá em [âmbitos de permissões de Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="80254-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="80254-158">Para `authURL`, `loginURL`, `bhh`, e `tokenURL`, deve utilizar valores de Olá fornecidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="80254-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="80254-159">Se utilizar a open source para Olá bibliotecas de identidade do Microsoft Azure, iremos importar estes dados para si através do nosso ponto final de metadados.</span><span class="sxs-lookup"><span data-stu-id="80254-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="80254-160">Iremos tiver terminado Olá trabalho de extrair estes valores para si.</span><span class="sxs-lookup"><span data-stu-id="80254-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="80254-161">Olá `keychain` valor é o contentor de Olá Olá biblioteca NXOAuth2Client irá utilizar toocreate toostore um keychain os tokens.</span><span class="sxs-lookup"><span data-stu-id="80254-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="80254-162">Se quiser tooget-início de sessão único (SSO) em várias aplicações, pode especificar Olá mesmo keychain em cada uma das suas aplicações e solicitar a utilização de Olá desse keychain na elegibilidade do Xcode.</span><span class="sxs-lookup"><span data-stu-id="80254-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="80254-163">Isto é explicado no Olá documentação da Apple.</span><span class="sxs-lookup"><span data-stu-id="80254-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="80254-164">rest Olá destes valores são biblioteca de Olá toouse necessária e criar locais para si contexto de toohello toocarry valores.</span><span class="sxs-lookup"><span data-stu-id="80254-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="80254-165">Criar uma cache de URL</span><span class="sxs-lookup"><span data-stu-id="80254-165">Create a URL cache</span></span>
<span data-ttu-id="80254-166">Dentro de `(void)viewDidLoad()`, sempre que é chamado após o carregamento da vista de Olá, hello seguinte código primes uma cache para utilização.</span><span class="sxs-lookup"><span data-stu-id="80254-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="80254-167">Adicione Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="80254-167">Add hello following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="80254-168">Criar um WebView para início de sessão</span><span class="sxs-lookup"><span data-stu-id="80254-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="80254-169">Um WebView pode pedir ao utilizador Olá fatores adicionais, como mensagem de texto SMS (se configurada) ou utilizador de toohello de mensagens de erro de retorno.</span><span class="sxs-lookup"><span data-stu-id="80254-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="80254-170">Aqui configure Olá WebView e, em seguida, posterior escrita Olá código toohandle Olá chamadas de retorno que irão surgir no WebView do Olá dos serviços de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="80254-171">Ignorar a autenticação de toohandle de métodos de WebView Olá</span><span class="sxs-lookup"><span data-stu-id="80254-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="80254-172">Olá tootell WebView o que acontece quando um utilizador precisa toosign no, tal como abordado anteriormente, pode colar Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="80254-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="80254-173">Resultado do pedido de OAuth2 Olá Olá da toohandle do código de escrita</span><span class="sxs-lookup"><span data-stu-id="80254-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="80254-174">Olá seguinte código irá processar o redirectURL Olá devolve de Olá WebView.</span><span class="sxs-lookup"><span data-stu-id="80254-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="80254-175">Se a autenticação não foi concluída com êxito, o código Olá tentará novamente.</span><span class="sxs-lookup"><span data-stu-id="80254-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="80254-176">Entretanto, a biblioteca de Olá fornecerá erro Olá que pode ver na consola de Olá ou processar de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="80254-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="80254-177">Configurar Olá contexto OAuth (denominada conta arquivo)</span><span class="sxs-lookup"><span data-stu-id="80254-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="80254-178">Aqui pode chamar `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` no arquivo de conta partilhada Olá para cada serviço que quiser Olá aplicação toobe capaz de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="80254-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="80254-179">tipo de conta Olá é uma cadeia que é utilizada como um identificador para um determinado serviço.</span><span class="sxs-lookup"><span data-stu-id="80254-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="80254-180">Porque estão a aceder Olá Graph API, o código de Olá refere-se tooit como `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="80254-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="80254-181">Em seguida, configure um observador que informará quando ocorrem alterações com o token de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="80254-182">Depois de obter o token de Olá, devolver Olá utilizador back toohello `masterView`.</span><span class="sxs-lookup"><span data-stu-id="80254-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="80254-183">Configurar Olá toosearch vista principal e apresentar utilizadores Olá Olá Graph API</span><span class="sxs-lookup"><span data-stu-id="80254-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="80254-184">Uma aplicação Master-View-Controller (MVC) que apresenta Olá devolvida dados na grelha de Olá ultrapassa o âmbito de Olá destas instruções e muitos tutoriais online explicam como toobuild um.</span><span class="sxs-lookup"><span data-stu-id="80254-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="80254-185">Todos os este código é no ficheiro de estrutura de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="80254-186">No entanto, terá de toodeal com algumas coisas nesta aplicação MVC:</span><span class="sxs-lookup"><span data-stu-id="80254-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="80254-187">Intercetar quando um utilizador tipos algo no campo de pesquisa de Olá</span><span class="sxs-lookup"><span data-stu-id="80254-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="80254-188">Fornecer um objeto de dados back-toohello MasterView para poder apresentar os resultados de Olá na grelha de Olá</span><span class="sxs-lookup"><span data-stu-id="80254-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="80254-189">Iremos executará as abaixo.</span><span class="sxs-lookup"><span data-stu-id="80254-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="80254-190">Adicionar um toosee de verificação se estiver a ser iniciado a sessão</span><span class="sxs-lookup"><span data-stu-id="80254-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="80254-191">aplicação Olá efetua pouco se utilizador Olá não está assinada, pelo que é toocheck inteligente se já existir um token na cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="80254-192">Se não, redireciona toohello LoginView para Olá utilizador toosign no.</span><span class="sxs-lookup"><span data-stu-id="80254-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="80254-193">Se recorda, Olá melhor forma toodo ações quando carrega uma vista é toouse Olá `viewDidLoad()` método Apple fornece-nos.</span><span class="sxs-lookup"><span data-stu-id="80254-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="80254-194">Atualizar Olá vista em tabela quando são recebidos dados</span><span class="sxs-lookup"><span data-stu-id="80254-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="80254-195">Quando Olá Graph API devolve dados, terá de dados de Olá toodisplay.</span><span class="sxs-lookup"><span data-stu-id="80254-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="80254-196">De simplicidade, segue-se todos os tabela de Olá do Olá código tooupdate.</span><span class="sxs-lookup"><span data-stu-id="80254-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="80254-197">Apenas pode colar valores direita Olá no seu código automático MVC.</span><span class="sxs-lookup"><span data-stu-id="80254-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="80254-198">Fornecer um Olá toocall de forma Graph API quando alguém tipos de campo de procura Olá</span><span class="sxs-lookup"><span data-stu-id="80254-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="80254-199">Quando um utilizador tipos uma pesquisa na caixa de Olá, terá de tooshove que através de toohello Graph API.</span><span class="sxs-lookup"><span data-stu-id="80254-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="80254-200">Olá `GraphAPICaller` classe, que se compilam Olá código a seguir, separa a funcionalidade de pesquisa de Olá da apresentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="80254-201">Por agora, vamos escrever código Olá feeds qualquer toohello de carateres de pesquisa Graph API.</span><span class="sxs-lookup"><span data-stu-id="80254-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="80254-202">Podemos fazê-lo, fornecendo um método chamado `lookupInGraph`, que demora a cadeia de Olá que queremos toosearch para.</span><span class="sxs-lookup"><span data-stu-id="80254-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="80254-203">Escrever um Olá de tooaccess de classe de programa auxiliar Graph API</span><span class="sxs-lookup"><span data-stu-id="80254-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="80254-204">Este é o principal de Olá da nossa aplicação.</span><span class="sxs-lookup"><span data-stu-id="80254-204">This is hello core of our application.</span></span> <span data-ttu-id="80254-205">Enquanto o resto Olá foi inserir o código no padrão MVC Olá predefinido da Apple, aqui é escrever gráfico do código tooquery Olá como utilizador Olá tipos e, em seguida, devolver os dados.</span><span class="sxs-lookup"><span data-stu-id="80254-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="80254-206">Eis o código de Olá e uma explicação detalhada seguinte.</span><span class="sxs-lookup"><span data-stu-id="80254-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="80254-207">Criar um novo ficheiro de cabeçalho de Objective C</span><span class="sxs-lookup"><span data-stu-id="80254-207">Create a new Objective C header file</span></span>
<span data-ttu-id="80254-208">Ficheiro de Olá nome `GraphAPICaller.h`e adicione Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="80254-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="80254-209">Aqui pode ver que um método especificado demora uma cadeia e devolve um completionBlock.</span><span class="sxs-lookup"><span data-stu-id="80254-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="80254-210">Este completionBlock, como o poderá ter adivinhado, irá atualizar Olá tabela, fornecendo um objeto com a dados preenchidos em tempo real como Olá pesquisas de utilizador.</span><span class="sxs-lookup"><span data-stu-id="80254-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="80254-211">Criar um novo ficheiro de Objective C</span><span class="sxs-lookup"><span data-stu-id="80254-211">Create a new Objective C file</span></span>
<span data-ttu-id="80254-212">Ficheiro de Olá nome `GraphAPICaller.m`e adicione Olá seguinte método.</span><span class="sxs-lookup"><span data-stu-id="80254-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

<span data-ttu-id="80254-213">Passemos através deste método em detalhe.</span><span class="sxs-lookup"><span data-stu-id="80254-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="80254-214">núcleo de Olá deste código é no Olá `NXOAuth2Request`, método que utiliza parâmetros de Olá que que já definiu no ficheiro de settings.plist Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="80254-215">Step-by-Olá primeiro passo é tooconstruct Olá direita gráfico na chamada à API.</span><span class="sxs-lookup"><span data-stu-id="80254-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="80254-216">Porque está a chamar `/users`, especificar que acrescentando-resource de Graph API toohello juntamente com a versão de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="80254-217">Faz sentido tooput estes num ficheiro de definições externo porque estes podem alterar-se à medida que evolui de Olá API.</span><span class="sxs-lookup"><span data-stu-id="80254-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="80254-218">Em seguida, terá de parâmetros de toospecify que também irá fornecer toohello chamada de API de gráfico.</span><span class="sxs-lookup"><span data-stu-id="80254-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="80254-219">É *muito importante* que coloque os parâmetros de Olá num ponto final de recursos de Olá porque que é removida de todos os carateres conforming não URI no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="80254-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="80254-220">Todo o código de consulta tem de ser fornecido nos parâmetros de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="80254-221">É possível que repare isto chama um `convertParamsToDictionary` método que ainda não escritas ainda.</span><span class="sxs-lookup"><span data-stu-id="80254-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="80254-222">Vamos fazer agora, por isso, no fim de Olá do ficheiro de Olá:</span><span class="sxs-lookup"><span data-stu-id="80254-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="80254-223">Em seguida, vamos utilizar Olá `NXOAuth2Request` fazer uma cópia de dados do método tooget de Olá API no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="80254-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="80254-224">Por fim, vamos ver como regressar Olá dados toohello MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="80254-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="80254-225">dados de Olá devolve conforme serializado e tem de anular a serialização de toobe e carregar um objeto que Olá MainViewController pode consumir.</span><span class="sxs-lookup"><span data-stu-id="80254-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="80254-226">Para esta finalidade, a estrutura de Olá tem um `User.m/h` ficheiro que cria um objeto de utilizador.</span><span class="sxs-lookup"><span data-stu-id="80254-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="80254-227">Preencher esse objeto de utilizador com as informações de gráfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="80254-227">You populate that User object with information from hello graph.</span></span>

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a><span data-ttu-id="80254-228">Executar o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="80254-228">Run hello sample</span></span>
<span data-ttu-id="80254-229">Se tiver utilizado a estrutura de Olá ou seguidas juntamente com instruções de Olá que agora deve ser executada a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="80254-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="80254-230">Iniciar o simulador de Olá e clique em **sessão** aplicação de Olá toouse.</span><span class="sxs-lookup"><span data-stu-id="80254-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="80254-231">Obter as atualizações de segurança para o nosso produto</span><span class="sxs-lookup"><span data-stu-id="80254-231">Get security updates for our product</span></span>
<span data-ttu-id="80254-232">Aconselhamo-lo tooget notificações de quando os incidentes de segurança ocorrem, visitando Olá [TechCenter de segurança](https://technet.microsoft.com/security/dd252948) e subscrever tooSecurity SUBSCREVENDO os alertas.</span><span class="sxs-lookup"><span data-stu-id="80254-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

