---
title: aaaAzure notificar utilizadores dos Notification Hubs com back-end .NET
description: "Saiba como toosend segura notificações push no Azure. Exemplos de código escrito em c# utilizando Olá .NET API."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="5b629-104">Azure notificar utilizadores dos Notification Hubs com back-end .NET</span><span class="sxs-lookup"><span data-stu-id="5b629-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="5b629-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="5b629-105">Overview</span></span>
<span data-ttu-id="5b629-106">Suporte de notificação push no Azure permite-lhe tooaccess uma fácil de utilizar, multiplatform e infraestrutura push ampliada, o que simplifica bastante a implementação de Olá de notificações push para aplicações de consumidor e enterprise Mobile plataformas.</span><span class="sxs-lookup"><span data-stu-id="5b629-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="5b629-107">Este tutorial mostra como toouse Notification Hubs do Azure toosend push utilizador de aplicação específica tooa de notificações num dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="5b629-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="5b629-108">Um back-end de ASP.NET WebAPI end é utilizado tooauthenticate clientes.</span><span class="sxs-lookup"><span data-stu-id="5b629-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="5b629-109">Olá autenticadas utilizador do cliente e etiqueta será adicionada automaticamente pelo registo de toonotification Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="5b629-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="5b629-110">Esta etiqueta será toosend utilizado por notificações de toogenerate Olá back-end para um utilizador específico.</span><span class="sxs-lookup"><span data-stu-id="5b629-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="5b629-111">Para obter mais informações sobre a registar notificações utilizando um back-end da aplicação, consulte o tópico de documentação de orientação de Olá [registar de back-end da aplicação](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b629-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="5b629-112">Este tutorial baseia-se Olá notification hub e o projeto que criou no Olá [introdução aos Hubs de notificação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b629-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="5b629-113">Este tutorial também é toohello pré-requisitos Olá [Secure Push] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b629-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="5b629-114">Depois de concluir os passos de Olá neste tutorial, pode avançar toohello [Secure Push] tutorial, que mostra como toomodify Olá código neste tutorial toosend uma notificação push em segurança.</span><span class="sxs-lookup"><span data-stu-id="5b629-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5b629-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="5b629-115">Before you begin</span></span>
<span data-ttu-id="5b629-116">Levamos muito a sério os seus comentários.</span><span class="sxs-lookup"><span data-stu-id="5b629-116">We do take your feedback seriously.</span></span> <span data-ttu-id="5b629-117">Se tiver dificuldades em concluir este tópico ou tiver recomendações para melhorar este conteúdo, Agradecemos os seus comentários na Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="5b629-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="5b629-118">código de Olá concluída para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="5b629-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5b629-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5b629-119">Prerequisites</span></span>
<span data-ttu-id="5b629-120">Antes de começar este tutorial, tem de ter já concluído estes tutoriais de Mobile Services:</span><span class="sxs-lookup"><span data-stu-id="5b629-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="5b629-121">[introdução aos Hubs de notificação]</span><span class="sxs-lookup"><span data-stu-id="5b629-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="5b629-122">Criar o seu hub de notificação e reservar nome da aplicação Olá e registar notificações tooreceive neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b629-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="5b629-123">Este tutorial parte do princípio de que já ter concluído estes passos.</span><span class="sxs-lookup"><span data-stu-id="5b629-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="5b629-124">Se não estiver, siga os passos de Olá em [introdução aos Notification Hubs (loja Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); especificamente, Olá secções [registar a aplicação para Olá loja Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) e [configurar o Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="5b629-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="5b629-125">Em particular, certifique-se de que introduziu Olá **SID do pacote** e **segredo do cliente** valores no portal de Olá, no Olá **configurar** separador para o seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="5b629-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="5b629-126">Este procedimento de configuração está descrito na secção de Olá [configurar o Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="5b629-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="5b629-127">Este é um passo importante: se Olá as credenciais no portal de Olá não correspondem às especificadas para o nome da aplicação Olá que escolher, notificação push de Olá não será bem sucedida.</span><span class="sxs-lookup"><span data-stu-id="5b629-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="5b629-128">Se estiver a utilizar Mobile Apps no App Service do Azure como o serviço de back-end, consulte Olá [versão Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b629-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="5b629-129">Código de Olá de atualização para o projeto de cliente Olá</span><span class="sxs-lookup"><span data-stu-id="5b629-129">Update hello code for hello client project</span></span>
<span data-ttu-id="5b629-130">Nesta secção, atualize o código de Olá no projeto Olá concluída para Olá [introdução aos Hubs de notificação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b629-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="5b629-131">Olá já estar associado a loja de Olá e configurado para o seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="5b629-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="5b629-132">Nesta secção, irá adicionar código toocall Olá novo back-end WebAPI e utilizá-lo para registar e enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="5b629-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="5b629-133">No Visual Studio, abra a solução de Olá de Olá que criou para Olá [introdução aos Hubs de notificação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b629-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="5b629-134">No Explorador de soluções, faça duplo clique Olá **(Windows 8.1)** projeto e, em seguida, clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5b629-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="5b629-135">No lado esquerdo Olá, clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="5b629-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="5b629-136">No Olá **pesquisa** caixa, escreva **cliente Http**.</span><span class="sxs-lookup"><span data-stu-id="5b629-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="5b629-137">Na lista de resultados de Olá, clique em **bibliotecas de cliente do Microsoft HTTP**e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="5b629-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="5b629-138">Concluir a instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b629-138">Complete hello installation.</span></span>
6. <span data-ttu-id="5b629-139">Novamente no Olá NuGet **pesquisa** caixa, escreva **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="5b629-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="5b629-140">Instalar Olá **Json.NET** pacote e a janela do Gestor de pacotes NuGet Olá, em seguida, feche.</span><span class="sxs-lookup"><span data-stu-id="5b629-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="5b629-141">Repita os passos de Olá acima para Olá **(Windows Phone 8.1)** Olá do projeto tooinstall **JSON.NET** pacote NuGet para o projeto do Windows Phone Olá.</span><span class="sxs-lookup"><span data-stu-id="5b629-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="5b629-142">No Explorador de soluções, na Olá **(Windows 8.1)** do projeto, faça duplo clique **MainPage.xaml** tooopen-lo no editor do Visual Studio Olá.</span><span class="sxs-lookup"><span data-stu-id="5b629-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="5b629-143">No Olá **MainPage.xaml** código XML, substituir Olá `<Grid>` secção com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="5b629-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="5b629-144">Este código adiciona o nome de utilizador e palavra-passe a caixa de texto que Olá utilizador irá autenticar com.</span><span class="sxs-lookup"><span data-stu-id="5b629-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="5b629-145">Também adiciona caixas de texto de mensagem de notificação de saudação e etiqueta de nome de utilizador de Olá que deve receber uma notificação de Olá:</span><span class="sxs-lookup"><span data-stu-id="5b629-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="5b629-146">No Explorador de soluções, na Olá **(Windows Phone 8.1)** projeto, abra **MainPage.xaml** e substitua Olá Windows Phone 8.1 `<Grid>` secção com esse mesmo código acima.</span><span class="sxs-lookup"><span data-stu-id="5b629-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="5b629-147">interface de Olá deverá ter um aspeto semelhante toowhats mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5b629-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="5b629-148">No Explorador de soluções, abra Olá **MainPage.xaml.cs** ficheiro para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos.</span><span class="sxs-lookup"><span data-stu-id="5b629-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="5b629-149">Adicione Olá seguinte `using` declarações na parte superior de Olá de ambos os ficheiros:</span><span class="sxs-lookup"><span data-stu-id="5b629-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="5b629-150">No **MainPage.xaml.cs** para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos, adicionar Olá seguinte membro toohello `MainPage` classe.</span><span class="sxs-lookup"><span data-stu-id="5b629-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="5b629-151">Ser tooreplace se `<Enter Your Backend Endpoint>` com Olá o ponto final de back-end real obtido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5b629-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="5b629-152">Por exemplo, `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5b629-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="5b629-153">Adicione o código de Olá abaixo toohello MainPage a classe **MainPage.xaml.cs** para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos.</span><span class="sxs-lookup"><span data-stu-id="5b629-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="5b629-154">Olá `PushClick` método é Olá clique processador para Olá **enviar Push** botão.</span><span class="sxs-lookup"><span data-stu-id="5b629-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="5b629-155">Chama Olá back-end tootrigger tooall uma notificação dispositivos com uma etiqueta de nome de utilizador que corresponda ao hello `to_tag` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5b629-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="5b629-156">mensagem de notificação de saudação é enviada como conteúdo JSON no corpo do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b629-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="5b629-157">Olá `LoginAndRegisterClick` método é Olá clique processador para Olá **iniciar sessão e registar** botão.</span><span class="sxs-lookup"><span data-stu-id="5b629-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="5b629-158">Armazena básico Olá token de autenticação no armazenamento local (tenha em atenção que isto representa qualquer token utiliza o seu esquema de autenticação), em seguida, utiliza `RegisterClient` tooregister para notificações através de back-end de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b629-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="5b629-159">No Explorador de soluções, em Olá **partilhados** projeto, abra Olá **App.xaml.cs** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="5b629-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="5b629-160">Localizar chamada Olá demasiado`InitNotificationsAsync()` no Olá `OnLaunched()` processador de eventos.</span><span class="sxs-lookup"><span data-stu-id="5b629-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="5b629-161">Comente ou eliminar chamada Olá demasiado`InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="5b629-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="5b629-162">registos de notificação será inicializar o processador de botão de Olá adicionado acima.</span><span class="sxs-lookup"><span data-stu-id="5b629-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="5b629-163">No Explorador de soluções, faça duplo clique Olá **partilhados** do projeto, em seguida, clique em **adicionar**e, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="5b629-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="5b629-164">Nome de classe de Olá **RegisterClient.cs**, em seguida, clique em **OK** classe de Olá toogenerate.</span><span class="sxs-lookup"><span data-stu-id="5b629-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="5b629-165">Esta classe irá encapsular Olá REST chamadas toocontact necessário Olá aplicação back-end, na ordem tooregister para notificações push.</span><span class="sxs-lookup"><span data-stu-id="5b629-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="5b629-166">Também localmente armazena Olá *registrationIds* criado pelo Olá Notification Hub, conforme detalhado em [registar de back-end da aplicação](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b629-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="5b629-167">Tenha em atenção que utiliza um token de autorização armazenado no armazenamento local quando clicar em Olá **iniciar sessão e registar** botão.</span><span class="sxs-lookup"><span data-stu-id="5b629-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="5b629-168">Adicione Olá seguinte `using` declarações, Olá parte superior do ficheiro de RegisterClient.cs Olá:</span><span class="sxs-lookup"><span data-stu-id="5b629-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="5b629-169">Adicionar Olá seguinte código dentro de Olá `RegisterClient` definição de classe.</span><span class="sxs-lookup"><span data-stu-id="5b629-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="5b629-170">Guarde todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="5b629-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="5b629-171">Testar Olá aplicação</span><span class="sxs-lookup"><span data-stu-id="5b629-171">Testing hello Application</span></span>
1. <span data-ttu-id="5b629-172">Inicie a aplicação Olá no Windows 8.1 e Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="5b629-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="5b629-173">Para Windows Phone 8.1 pode executar a instância de Olá no emulador de Olá ou um dispositivo real.</span><span class="sxs-lookup"><span data-stu-id="5b629-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="5b629-174">Na instância de Olá Windows 8.1 da aplicação Olá, introduza um **Username** e **palavra-passe** conforme mostrado no ecrã de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="5b629-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="5b629-175">Deve ser é diferente do nome de utilizador de Olá e a palavra-passe que introduzir no Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="5b629-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="5b629-176">Clique em **iniciar sessão e registar** e certifique-se de uma caixa de diálogo mostra de que iniciou sessão.</span><span class="sxs-lookup"><span data-stu-id="5b629-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="5b629-177">Isto também irá ativar Olá **enviar Push** botão.</span><span class="sxs-lookup"><span data-stu-id="5b629-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="5b629-178">Na instância de Olá Windows Phone 8.1, introduza uma cadeia de nome de utilizador em ambas as Olá **Username** e **palavra-passe** campos, em seguida, clique em **início de sessão e registar**.</span><span class="sxs-lookup"><span data-stu-id="5b629-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="5b629-179">Em seguida, no Olá **etiqueta de nome de utilizador de destinatário** campo, introduza o nome de utilizador de Olá registado no Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="5b629-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="5b629-180">Introduza uma mensagem de notificação e clique em **enviar Push**.</span><span class="sxs-lookup"><span data-stu-id="5b629-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="5b629-181">Apenas os dispositivos de Olá que registou com etiqueta de nome de utilizador correspondente Olá recebem a mensagem de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b629-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="5b629-182">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="5b629-182">Next Steps</span></span>
* <span data-ttu-id="5b629-183">Se quiser toosegment os seus utilizadores por grupos de interesses, consulte [toosend utilizar Notification Hubs notícias de última hora].</span><span class="sxs-lookup"><span data-stu-id="5b629-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="5b629-184">mais informações sobre como toolearn toouse Notification Hubs, consulte [documentação de orientação dos Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="5b629-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[introdução aos Hubs de notificação]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[toosend utilizar Notification Hubs notícias de última hora]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[documentação de orientação dos Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
