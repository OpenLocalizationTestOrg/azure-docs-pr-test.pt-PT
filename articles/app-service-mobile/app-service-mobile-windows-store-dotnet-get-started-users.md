---
title: "aplicação plataforma Universal do Windows (UWP) do aaaAdd authentication tooyour | Microsoft Docs"
description: "Saiba como os utilizadores de tooauthenticate de Mobile Apps do Azure App Service toouse da sua aplicação plataforma Universal do Windows (UWP) utilizando uma variedade de fornecedores de identidade, incluindo: AAD, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="3b733-103">Adicionar autenticação tooyour Windows aplicação</span><span class="sxs-lookup"><span data-stu-id="3b733-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="3b733-104">Este tópico mostra como tooadd tooyour de autenticação baseada em nuvem aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="3b733-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="3b733-105">Neste tutorial, é possível adicionar projeto de início rápido da plataforma Universal do Windows (UWP) de toohello de autenticação para Mobile Apps utilizando um fornecedor de identidade que é suportado pelo App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b733-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="3b733-106">Após com êxito a ser autenticado e autorizado pelo seu back-end de aplicação móvel, é apresentado o valor de ID de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="3b733-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="3b733-107">Este tutorial é baseado no início rápido de aplicações móveis Olá.</span><span class="sxs-lookup"><span data-stu-id="3b733-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="3b733-108">Tem de concluir primeiro tutorial Olá [introdução às Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b733-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="3b733-109"><a name="register"></a>Registar a aplicação para autenticação e configurar Olá do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="3b733-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="3b733-110"><a name="redirecturl"></a>Adicionar os URLs de redirecionamento de externo permitido de toohello de aplicação</span><span class="sxs-lookup"><span data-stu-id="3b733-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="3b733-111">Autenticação segura requer que defina um novo esquema de URL para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="3b733-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="3b733-112">Isto permite Olá autenticação sistema tooredirect back tooyour aplicação após a conclusão do processo de autenticação de Olá.</span><span class="sxs-lookup"><span data-stu-id="3b733-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="3b733-113">Neste tutorial, utilizamos o esquema de URL Olá _appname_ ao longo.</span><span class="sxs-lookup"><span data-stu-id="3b733-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="3b733-114">No entanto, pode utilizar qualquer esquema de URL que escolher.</span><span class="sxs-lookup"><span data-stu-id="3b733-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="3b733-115">Deve ser exclusivo tooyour aplicações móveis.</span><span class="sxs-lookup"><span data-stu-id="3b733-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="3b733-116">redirecionamento de Olá tooenable no lado do servidor de Olá:</span><span class="sxs-lookup"><span data-stu-id="3b733-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="3b733-117">No [portal do Azure] Olá, selecione o serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="3b733-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="3b733-118">Clique em Olá **autenticação / autorização** opção do menu.</span><span class="sxs-lookup"><span data-stu-id="3b733-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="3b733-119">No Olá **permitidos URLs de redirecionamento externos**, introduza `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="3b733-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="3b733-120">Olá **url_scheme_of_your_app** esta cadeia é Olá esquema de URL para a sua aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="3b733-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="3b733-121">Deve seguir a especificação de URL normal para um protocolo (utilize letras e números apenas e começar com uma letra).</span><span class="sxs-lookup"><span data-stu-id="3b733-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="3b733-122">Deve efetuar uma nota da cadeia de Olá que escolher pois terá tooadjust código da aplicação móvel com Olá esquema de URL em vários locais.</span><span class="sxs-lookup"><span data-stu-id="3b733-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="3b733-123">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b733-123">Click **OK**.</span></span>

5. <span data-ttu-id="3b733-124">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3b733-124">Click **Save**.</span></span>

## <span data-ttu-id="3b733-125"><a name="permissions"></a>Restringir os utilizadores tooauthenticated de permissões</span><span class="sxs-lookup"><span data-stu-id="3b733-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="3b733-126">Agora, pode verificar que back-end do acesso anónimo tooyour foi desativada.</span><span class="sxs-lookup"><span data-stu-id="3b733-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="3b733-127">Com Olá projeto de aplicação UWP definir como projeto de arranque Olá, implementar e executar a aplicação de Olá; Certifique-se de que uma exceção não processada com um código de estado de 401 (não autorizado) é desencadeada depois de Olá aplicação for iniciada.</span><span class="sxs-lookup"><span data-stu-id="3b733-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="3b733-128">Isto acontece porque a aplicação Olá tenta tooaccess o código de aplicação móvel como um utilizador não autorizado, mas Olá *TodoItem* tabela agora requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="3b733-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="3b733-129">Em seguida, irá atualizar utilizadores de tooauthenticate Olá aplicações antes de solicitar recursos a partir do seu serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="3b733-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="3b733-130"><a name="add-authentication"></a>Adicionar autenticação toohello aplicação</span><span class="sxs-lookup"><span data-stu-id="3b733-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="3b733-131">No projeto de aplicação UWP Olá ficheiro MainPage.xaml.cs e adicionar Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="3b733-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="3b733-132">Este código autentica o utilizador de Olá com um início de sessão do Facebook.</span><span class="sxs-lookup"><span data-stu-id="3b733-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="3b733-133">Se estiver a utilizar um fornecedor de identidade que não seja o Facebook, altere o valor de Olá de **MobileServiceAuthenticationProvider** acima toohello valor para o seu fornecedor.</span><span class="sxs-lookup"><span data-stu-id="3b733-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="3b733-134">Substitua Olá **OnNavigatedTo()** método no MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="3b733-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="3b733-135">Em seguida, irá adicionar um **sessão** botão toohello aplicação que aciona a autenticação.</span><span class="sxs-lookup"><span data-stu-id="3b733-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="3b733-136">Adicione Olá seguinte fragmento de código toohello MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="3b733-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="3b733-137">Abra o ficheiro de projeto MainPage.xaml Olá, localizar o elemento de Olá que define Olá **guardar** botão e substitua-o por Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="3b733-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. <span data-ttu-id="3b733-138">Adicione Olá seguinte fragmento de código toohello App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="3b733-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. <span data-ttu-id="3b733-139">Abra o ficheiro Package. appxmanifest, navegue demasiado**declarações**, na **declarações disponíveis** na lista pendente, selecione **protocolo** e clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="3b733-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="3b733-140">Configurar agora Olá **propriedades** de Olá **protocolo** declaração.</span><span class="sxs-lookup"><span data-stu-id="3b733-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="3b733-141">No **nome a apresentar**, adicionar nome Olá desejar toodisplay toousers da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="3b733-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="3b733-142">No **nome**, adicione o {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="3b733-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="3b733-143">Prima Olá F5 toorun chave Olá aplicação, clique em Olá **sessão** botão e inicie sessão na aplicação Olá com o seu fornecedor de identidade que escolheu.</span><span class="sxs-lookup"><span data-stu-id="3b733-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="3b733-144">Após o início de sessão, aplicação Olá é executado sem erros e são tooquery capaz de back-end e tornar toodata de atualizações.</span><span class="sxs-lookup"><span data-stu-id="3b733-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="3b733-145"><a name="tokens"></a>Armazenar o token de autenticação de Olá no cliente Olá</span><span class="sxs-lookup"><span data-stu-id="3b733-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="3b733-146">Exemplo Olá de anterior mostrou um padrão início de sessão, que necessita de Olá cliente toocontact ambos os fornecedor de identidade Olá e hello do serviço de aplicações, sempre que essa aplicação Olá é iniciado.</span><span class="sxs-lookup"><span data-stu-id="3b733-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="3b733-147">Não só é ineficaz, pode executar este método para utilização-relacionado com problemas de muitos clientes tente toostart aplicação em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="3b733-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="3b733-148">Uma abordagem de melhor é o token de autorização de Olá toocache devolvido pelo seu serviço de aplicações e tente toouse este primeiro antes de utilizar um fornecedor com base no início de sessão.</span><span class="sxs-lookup"><span data-stu-id="3b733-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="3b733-149">Pode colocar em cache o token de Olá emitido por serviços aplicacionais independentemente se estão a utilizar autenticação geridos pelo cliente ou serviço gerido.</span><span class="sxs-lookup"><span data-stu-id="3b733-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="3b733-150">Este tutorial utiliza a autenticação de serviço gerido.</span><span class="sxs-lookup"><span data-stu-id="3b733-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="3b733-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3b733-151">Next steps</span></span>
<span data-ttu-id="3b733-152">Agora que concluiu este tutorial de autenticação básica, considere continuar em tooone de Olá seguintes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="3b733-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="3b733-153">Adicionar a aplicação de tooyour de notificações push</span><span class="sxs-lookup"><span data-stu-id="3b733-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="3b733-154">Saiba como notificações de push tooadd suportam tooyour aplicação e configurar a sua aplicação móvel back-end toouse Notification Hubs do Azure toosend as notificações push.</span><span class="sxs-lookup"><span data-stu-id="3b733-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="3b733-155">Permitir sincronização offline para a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="3b733-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="3b733-156">Saiba como tooadd offline suportam a sua aplicação utilizando um back-end de aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="3b733-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="3b733-157">Sincronização offline permite que os utilizadores finais toointeract com uma aplicação móvel&mdash;visualizar, adicionar ou modificar dados&mdash;, mesmo quando não existe nenhuma ligação de rede.</span><span class="sxs-lookup"><span data-stu-id="3b733-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
