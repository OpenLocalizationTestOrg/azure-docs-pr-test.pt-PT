## <a name="create-hello-webapi-project"></a>Criar Olá end WebAPI projeto
Será criado um novo back-end de ASP.NET WebAPI end nas secções Olá que se seguem e terá três objetivos principais:

1. **Os clientes em autenticação**: o processador de mensagens será adicionado pedidos de cliente tooauthenticate posteriores e o utilizador de Olá associar com pedido de Olá.
2. **Registos de notificação de cliente**: mais tarde, irá adicionar um controlador toohandle novos registos para um notificações de tooreceive de dispositivo do cliente. Olá nome de utilizador autenticado será automaticamente adicionada toohello registo como um [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **Enviar notificações tooClients**: posterior, também irá adicionar um controlador tooprovide uma forma de um utilizador de tootrigger toodevices um push segura e clientes associados a tag de Olá. 

Olá, os passos seguintes mostra como toocreate Olá novo back-end de ASP.NET WebAPI end: 

> [!IMPORTANT]
> Se estiver a utilizar o Visual Studio 2015 ou anterior, antes de começar este tutorial, certifique-se que instalou a versão mais recente do Olá do Olá Gestor de pacotes NuGet. toocheck, início Visual Studio. De Olá **ferramentas** menu, clique em **extensões e atualizações**. Procurar **Gestor de pacotes NuGet** para a sua versão do Visual Studio e certifique-se de que tem a versão mais recente Olá. Se não estiver, desinstale e reinstale Olá Gestor de pacotes NuGet.
> 
> ![][B4]
> 
> [!NOTE]
> Certifique-se de que instalou o Visual Studio do Olá [Azure SDK](https://azure.microsoft.com/downloads/) para a implementação de Web site.
> 
> 

1. Inicie o Visual Studio ou o Visual Studio Express. Clique em **Explorador de servidores** e iniciar sessão tooyour conta do Azure. Visual Studio terá de sessão em recursos de web site Olá toocreate na sua conta.
2. No Visual Studio, clique em **ficheiro**, em seguida, clique em **novo**, em seguida, **projeto**, expanda **modelos**, **Visual c#**, em seguida, clique em **Web** e **aplicação Web ASP.NET**, nome do tipo Olá **AppBackend**e, em seguida, clique em **OK**. 
   
    ![][B1]
3. No Olá **novo projeto ASP.NET** caixa de diálogo, clique em **Web API**, em seguida, clique em **OK**.
   
    ![][B2]
4. No Olá **configurar aplicação da Web do Microsoft Azure** caixa de diálogo, escolha uma subscrição e um **plano do App Service** que já criou. Também pode optar por **criar um novo plano do app service** e criar uma caixa de diálogo de Olá. Não precisa de uma base de dados para este tutorial. Assim que tiver selecionado o plano do app service, clique em **OK** projeto de Olá toocreate.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>Autenticação de clientes toohello back-end WebAPI
Nesta secção, irá criar uma nova classe de processador de mensagens com o nome **AuthenticationTestHandler** para Olá novo back-end. Esta classe é derivada de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) e adicionado como um processador de mensagens, pelo que pode processar todos os pedidos entra de back-end de Olá. 

1. No Explorador de soluções, faça duplo clique Olá **AppBackend** do projeto, clique em **adicionar**, em seguida, clique em **classe**. Nome da nova classe de Olá **AuthenticationTestHandler.cs**e clique em **adicionar** classe de Olá toogenerate. Esta classe será utilizado tooauthenticate utilizadores utilizando o *autenticação básica* de simplicidade. Tenha em atenção que a sua aplicação pode utilizar qualquer esquema de autenticação.
2. No AuthenticationTestHandler.cs, adicione o seguinte de Olá `using` instruções:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. No AuthenticationTestHandler.cs, substituindo Olá `AuthenticationTestHandler` definição de classe com Olá seguinte código. 
   
    Este processador autorizará pedido Olá quando Olá seguintes três condições se verificarem todas as:
   
   * pedido de Olá incluído um *autorização* cabeçalho. 
   * pedido de Olá utiliza *básico* autenticação. 
   * cadeia de nome de utilizador Olá e a cadeia de palavra-passe de Olá são Olá mesma cadeia.
     
     Caso contrário, o pedido de Olá será rejeitado. Esta não é uma verdadeira abordagem de autenticação e autorização. É apenas um exemplo muito simples para este tutorial.
     
     Se a mensagem de pedido de saudação é autenticada e autorizada por Olá `AuthenticationTestHandler`, utilizador de autenticação básica Olá será anexado toohello pedido atual no Olá [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). Informações do utilizador no Olá HttpContext serão utilizadas por outro controlador (RegisterController) tooadd posterior um [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello pedido de registo de notificação.
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **Nota de segurança**: Olá `AuthenticationTestHandler` classe não fornecer autenticação verdadeira. É utilizado toomimic apenas a autenticação básica e não é segura. Tem de implementar um mecanismo de autenticação segura nos seus serviços e aplicações de produção.                
     > 
     > 
4. Adicionar Olá seguinte código no final Olá Olá `Register` método Olá **App_Start/WebApiConfig.cs** o processador de mensagens de Olá classe tooregister:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Guarde as alterações.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>A registar notificações utilizando Olá back-end WebAPI
Nesta secção, iremos adicionar que um novo back-end toohandle do controlador toohello end WebAPI pedidos tooregister um utilizador e dispositivo para as notificações com a biblioteca de cliente de Olá para os notification hubs. controlador Olá irá adicionar uma etiqueta de utilizador para o utilizador Olá que foi autenticado e anexado toohello HttpContext por Olá `AuthenticationTestHandler`. etiqueta de Olá terão o formato de cadeia Olá, `"username:<actual username>"`.

1. No Explorador de soluções, faça duplo clique Olá **AppBackend** projeto e, em seguida, clique em **gerir pacotes NuGet**.
2. No lado esquerdo Olá, clique em **Online**e procure **notificationhubs** no Olá **pesquisa** caixa.
3. Na lista de resultados de Olá, clique em **os Notification Hubs do Microsoft Azure**e, em seguida, clique em **instalar**. Concluir a instalação de Olá, em seguida, feche a janela do Gestor de pacotes de NuGet de Olá.
   
    Esta ação adiciona uma referência toohello SDK dos Notification Hubs do Azure utilizando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet do Microsoft Hubs</a>.
4. Iremos agora criar um novo ficheiro de classe que representa a ligação de Olá com o notification hub utilizado toosend notificações. No Explorador de soluções Olá, faça duplo clique Olá **modelos** pasta, clique em **adicionar**, em seguida, clique em **classe**. Nome da nova classe de Olá **Notifications.cs**, em seguida, clique em **adicionar** classe de Olá toogenerate. 
   
    ![][B6]
5. No Notifications.cs, adicione o seguinte de Olá `using` declaração, Olá parte superior do ficheiro de Olá:
   
        using Microsoft.Azure.NotificationHubs;
6. Substitua Olá `Notifications` definição com o seguinte Olá de classe, certifique-se tooreplace Olá dois marcadores de posição pelo cadeia de ligação de Olá (com acesso total) para o seu hub de notificação e Olá nome do hub (disponível em [Portal clássico do Azure ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. Em seguida, vamos criar um controlador novo com o nome **RegisterController**. No Explorador de soluções, faça duplo clique Olá **controladores** pasta, em seguida, clique em **adicionar**, em seguida, clique em **controlador**. Clique em Olá **controlador no Web API 2 – vazio** item e, em seguida, clique em **adicionar**. Nome da nova classe de Olá **RegisterController**e, em seguida, clique em **adicionar** novamente o controlador de Olá toogenerate.
   
    ![][B7]
   
    ![][B8]
8. No RegisterController.cs, adicione o seguinte de Olá `using` instruções:
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Adicionar Olá seguinte código dentro de Olá `RegisterController` definição de classe. Tenha em atenção que neste código, iremos adicionar uma etiqueta de utilizador para o utilizador Olá é anexado toohello HttpContext. utilizador Olá foi autenticado e anexado toohello HttpContext pelo filtro de mensagem de Olá adicionámos, `AuthenticationTestHandler`. Também pode adicionar tooverify verificações opcional que Olá utilizador tem direitos tooregister para Olá pedida etiquetas.
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. Guarde as alterações.

## <a name="sending-notifications-from-hello-webapi-backend"></a>Enviar notificações de Olá back-end WebAPI
Nesta secção, pode adiciona um novo controlador que expõe uma forma de dispositivos de cliente toosend uma notificação com base na etiqueta de nome de utilizador de Olá utilizando a biblioteca de gestão de serviço do Azure Notification Hubs no Olá back-end de ASP.NET WebAPI.

1. Crie outro controlador novo com o nome **NotificationsController**. Criá-la Olá mesma forma que criou Olá **RegisterController** na secção anterior Olá.
2. No NotificationsController.cs, adicione o seguinte de Olá `using` instruções:
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Adicionar Olá seguinte método toohello **NotificationsController** classe.
   
    Este código de enviar um tipo de notificação com base no serviço de notificação de plataforma (PNS) de Olá `pns` parâmetro. Olá valor `to_tag` é utilizado tooset Olá *username* tag na mensagem de saudação. Esta etiqueta tem de corresponder a uma etiqueta de nome de utilizador de um registo de hub de notificação ativo. mensagem de notificação de saudação é retirada da corpo Olá de pedido POST Olá e formatada para o destino de Olá PNS. 
   
    Dependendo do serviço de notificação de plataforma (PNS) que os dispositivos suportados utilizam notificações de tooreceive Olá, diferentes notificações são suportadas com diferentes formatos. Por exemplo, em dispositivos Windows, pode utilizar uma [notificação de alerta com WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) que não seja diretamente suportada por outro PNS. Planear toosupport pelo seu back-end seria necessita de notificação de Olá tooformat para uma notificação suportada para Olá PNS dos dispositivos. Em seguida, utilize Olá envio adequado API no Olá [NotificationHubClient classe](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. Prima **F5** toorun Olá aplicação e tooensure Olá precisão do seu trabalho até ao momento. aplicação Olá deve iniciar um browser e apresentar a home page do Olá ASP.NET. 

## <a name="publish-hello-new-webapi-backend"></a>Publicar Olá novo back-end WebAPI
1. Agora iremos implementar esta tooan de aplicação Web site do Azure na ordem toomake-lo acessível a partir de todos os dispositivos. Clique com o botão direito no Olá **AppBackend** projeto e selecione **publicar**.
2. Selecione **Serviço de Aplicações do Microsoft Azure** como o destino da publicação e clique em **Publicar**. Esta ação abre Olá criar App Service caixa de diálogo, que ajuda a criar todos os Olá recursos do Azure necessários toorun Olá aplicação web do ASP.NET no Azure.

    ![][B15]
3. No Olá **criar App Service** caixa de diálogo, selecione a sua conta do Azure. Clique em **Alterar Tipo** e selecione **Aplicação Web**. Manter Olá **nome da aplicação Web** Olá indicado e selecione **subscrição**, **grupo de recursos**, e **plano do App Service**.  Clique em **Criar**.

4. Tome nota do Olá **URL do Site** propriedade no Olá **resumo** secção. Iremos dar toothis URL como o *ponto final de back-end* mais à frente neste tutorial. Clique em **Publicar**.

5. Após a conclusão do Assistente de Olá, publica Olá ASP.NET web app tooAzure e, em seguida, inicia Olá aplicação no browser predefinido de Olá.  A aplicação estará visualizável no Serviço de Aplicações do Azure.

URL de Olá utiliza Olá nome da aplicação web que especificou anteriormente, com Olá formato http://<app_name>.azurewebsites.net.

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
