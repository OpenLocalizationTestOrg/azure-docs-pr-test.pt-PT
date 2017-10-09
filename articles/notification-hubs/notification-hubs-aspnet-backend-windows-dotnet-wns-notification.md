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
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>Azure notificar utilizadores dos Notification Hubs com back-end .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Descrição geral
Suporte de notificação push no Azure permite-lhe tooaccess uma fácil de utilizar, multiplatform e infraestrutura push ampliada, o que simplifica bastante a implementação de Olá de notificações push para aplicações de consumidor e enterprise Mobile plataformas. Este tutorial mostra como toouse Notification Hubs do Azure toosend push utilizador de aplicação específica tooa de notificações num dispositivo específico. Um back-end de ASP.NET WebAPI end é utilizado tooauthenticate clientes. Olá autenticadas utilizador do cliente e etiqueta será adicionada automaticamente pelo registo de toonotification Olá back-end. Esta etiqueta será toosend utilizado por notificações de toogenerate Olá back-end para um utilizador específico. Para obter mais informações sobre a registar notificações utilizando um back-end da aplicação, consulte o tópico de documentação de orientação de Olá [registar de back-end da aplicação](http://msdn.microsoft.com/library/dn743807.aspx). Este tutorial baseia-se Olá notification hub e o projeto que criou no Olá [introdução aos Hubs de notificação] tutorial.

Este tutorial também é toohello pré-requisitos Olá [Secure Push] tutorial. Depois de concluir os passos de Olá neste tutorial, pode avançar toohello [Secure Push] tutorial, que mostra como toomodify Olá código neste tutorial toosend uma notificação push em segurança.

## <a name="before-you-begin"></a>Antes de começar
Levamos muito a sério os seus comentários. Se tiver dificuldades em concluir este tópico ou tiver recomendações para melhorar este conteúdo, Agradecemos os seus comentários na Olá parte inferior da página Olá.

código de Olá concluída para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). 

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, tem de ter já concluído estes tutoriais de Mobile Services:

* [introdução aos Hubs de notificação]<br/>Criar o seu hub de notificação e reservar nome da aplicação Olá e registar notificações tooreceive neste tutorial. Este tutorial parte do princípio de que já ter concluído estes passos. Se não estiver, siga os passos de Olá em [introdução aos Notification Hubs (loja Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); especificamente, Olá secções [registar a aplicação para Olá loja Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) e [configurar o Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Em particular, certifique-se de que introduziu Olá **SID do pacote** e **segredo do cliente** valores no portal de Olá, no Olá **configurar** separador para o seu hub de notificação. Este procedimento de configuração está descrito na secção de Olá [configurar o Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Este é um passo importante: se Olá as credenciais no portal de Olá não correspondem às especificadas para o nome da aplicação Olá que escolher, notificação push de Olá não será bem sucedida.

> [!NOTE]
> Se estiver a utilizar Mobile Apps no App Service do Azure como o serviço de back-end, consulte Olá [versão Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) deste tutorial.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Código de Olá de atualização para o projeto de cliente Olá
Nesta secção, atualize o código de Olá no projeto Olá concluída para Olá [introdução aos Hubs de notificação] tutorial. Olá já estar associado a loja de Olá e configurado para o seu hub de notificação. Nesta secção, irá adicionar código toocall Olá novo back-end WebAPI e utilizá-lo para registar e enviar notificações.

1. No Visual Studio, abra a solução de Olá de Olá que criou para Olá [introdução aos Hubs de notificação] tutorial.
2. No Explorador de soluções, faça duplo clique Olá **(Windows 8.1)** projeto e, em seguida, clique em **gerir pacotes NuGet**.
3. No lado esquerdo Olá, clique em **Online**.
4. No Olá **pesquisa** caixa, escreva **cliente Http**.
5. Na lista de resultados de Olá, clique em **bibliotecas de cliente do Microsoft HTTP**e, em seguida, clique em **instalar**. Concluir a instalação de Olá.
6. Novamente no Olá NuGet **pesquisa** caixa, escreva **Json.net**. Instalar Olá **Json.NET** pacote e a janela do Gestor de pacotes NuGet Olá, em seguida, feche.
7. Repita os passos de Olá acima para Olá **(Windows Phone 8.1)** Olá do projeto tooinstall **JSON.NET** pacote NuGet para o projeto do Windows Phone Olá.
8. No Explorador de soluções, na Olá **(Windows 8.1)** do projeto, faça duplo clique **MainPage.xaml** tooopen-lo no editor do Visual Studio Olá.
9. No Olá **MainPage.xaml** código XML, substituir Olá `<Grid>` secção com Olá seguinte código. Este código adiciona o nome de utilizador e palavra-passe a caixa de texto que Olá utilizador irá autenticar com. Também adiciona caixas de texto de mensagem de notificação de saudação e etiqueta de nome de utilizador de Olá que deve receber uma notificação de Olá:
   
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
10. No Explorador de soluções, na Olá **(Windows Phone 8.1)** projeto, abra **MainPage.xaml** e substitua Olá Windows Phone 8.1 `<Grid>` secção com esse mesmo código acima. interface de Olá deverá ter um aspeto semelhante toowhats mostrado abaixo.
    
    ![][13]
11. No Explorador de soluções, abra Olá **MainPage.xaml.cs** ficheiro para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos. Adicione Olá seguinte `using` declarações na parte superior de Olá de ambos os ficheiros:
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. No **MainPage.xaml.cs** para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos, adicionar Olá seguinte membro toohello `MainPage` classe. Ser tooreplace se `<Enter Your Backend Endpoint>` com Olá o ponto final de back-end real obtido anteriormente. Por exemplo, `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Adicione o código de Olá abaixo toohello MainPage a classe **MainPage.xaml.cs** para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos.
    
    Olá `PushClick` método é Olá clique processador para Olá **enviar Push** botão. Chama Olá back-end tootrigger tooall uma notificação dispositivos com uma etiqueta de nome de utilizador que corresponda ao hello `to_tag` parâmetro. mensagem de notificação de saudação é enviada como conteúdo JSON no corpo do pedido de Olá.
    
    Olá `LoginAndRegisterClick` método é Olá clique processador para Olá **iniciar sessão e registar** botão. Armazena básico Olá token de autenticação no armazenamento local (tenha em atenção que isto representa qualquer token utiliza o seu esquema de autenticação), em seguida, utiliza `RegisterClient` tooregister para notificações através de back-end de Olá.

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



1. No Explorador de soluções, em Olá **partilhados** projeto, abra Olá **App.xaml.cs** ficheiro. Localizar chamada Olá demasiado`InitNotificationsAsync()` no Olá `OnLaunched()` processador de eventos. Comente ou eliminar chamada Olá demasiado`InitNotificationsAsync()`. registos de notificação será inicializar o processador de botão de Olá adicionado acima.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. No Explorador de soluções, faça duplo clique Olá **partilhados** do projeto, em seguida, clique em **adicionar**e, em seguida, clique em **classe**. Nome de classe de Olá **RegisterClient.cs**, em seguida, clique em **OK** classe de Olá toogenerate.
   
   Esta classe irá encapsular Olá REST chamadas toocontact necessário Olá aplicação back-end, na ordem tooregister para notificações push. Também localmente armazena Olá *registrationIds* criado pelo Olá Notification Hub, conforme detalhado em [registar de back-end da aplicação](http://msdn.microsoft.com/library/dn743807.aspx). Tenha em atenção que utiliza um token de autorização armazenado no armazenamento local quando clicar em Olá **iniciar sessão e registar** botão.
2. Adicione Olá seguinte `using` declarações, Olá parte superior do ficheiro de RegisterClient.cs Olá:
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Adicionar Olá seguinte código dentro de Olá `RegisterClient` definição de classe.
   
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
4. Guarde todas as alterações.

## <a name="testing-hello-application"></a>Testar Olá aplicação
1. Inicie a aplicação Olá no Windows 8.1 e Windows Phone 8.1. Para Windows Phone 8.1 pode executar a instância de Olá no emulador de Olá ou um dispositivo real.
2. Na instância de Olá Windows 8.1 da aplicação Olá, introduza um **Username** e **palavra-passe** conforme mostrado no ecrã de Olá abaixo. Deve ser é diferente do nome de utilizador de Olá e a palavra-passe que introduzir no Windows Phone.
3. Clique em **iniciar sessão e registar** e certifique-se de uma caixa de diálogo mostra de que iniciou sessão. Isto também irá ativar Olá **enviar Push** botão.
   
    ![][14]
4. Na instância de Olá Windows Phone 8.1, introduza uma cadeia de nome de utilizador em ambas as Olá **Username** e **palavra-passe** campos, em seguida, clique em **início de sessão e registar**.
5. Em seguida, no Olá **etiqueta de nome de utilizador de destinatário** campo, introduza o nome de utilizador de Olá registado no Windows 8.1. Introduza uma mensagem de notificação e clique em **enviar Push**.
   
    ![][16]
6. Apenas os dispositivos de Olá que registou com etiqueta de nome de utilizador correspondente Olá recebem a mensagem de notificação de saudação.
   
    ![][15]

## <a name="next-steps"></a>Passos Seguintes
* Se quiser toosegment os seus utilizadores por grupos de interesses, consulte [toosend utilizar Notification Hubs notícias de última hora].
* mais informações sobre como toolearn toouse Notification Hubs, consulte [documentação de orientação dos Notification Hubs].

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
