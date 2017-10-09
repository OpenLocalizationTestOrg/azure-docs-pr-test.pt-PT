## <a name="webapi-project"></a>End WebAPI projeto
1. No Visual Studio, abra Olá **AppBackend** projeto que criou no Olá **notificam os utilizadores** tutorial.
2. No Notifications.cs, substituir Olá todo **notificações** classe com Olá seguinte código. Ser se tooreplace Olá marcadores de posição pela cadeia de ligação (com acesso total) para o seu hub de notificação e o nome do hub Olá. Pode obter estes valores de Olá [Portal clássico do Azure](http://manage.windowsazure.com). Este módulo representa agora Olá diferentes segura notificações que serão enviadas. Uma implementação completa, as notificações de Olá serão armazenadas numa base de dados; de simplicidade, neste caso, iremos armazená-las na memória.
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. No NotificationsController.cs, substitua o código de Olá dentro de Olá **NotificationsController** definição de classe com Olá seguinte código. Este componente implementa uma forma de notificação de Olá Olá dispositivo tooretrieve de forma segura e também fornece uma forma (para fins de Olá deste tutorial) tootrigger um dispositivos de tooyour push segura. Tenha em atenção que ao enviar o hub de notificação de toohello de notificação de Olá, apenas Enviámos uma notificação não processada, com o ID de Olá de notificação de Olá (e não existem mensagens real):
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


Tenha em atenção que Olá `Post` método agora não enviar uma notificação de alerta. Envia uma notificação em bruto que contém o ID de notificação de Olá apenas e não a qualquer conteúdo confidencial. Além disso, certifique-Olá toocomment se de que a operação para plataformas de Olá para os quais não tem credenciais configuradas no seu hub de notificação, conforme irá causar erros de envio.

1. Agora vamos reimplementar esta tooan de aplicação Web site do Azure na ordem toomake-lo acessível a partir de todos os dispositivos. Clique com o botão direito no Olá **AppBackend** projeto e selecione **publicar**.
2. Selecione o Web site do Azure como o destino da publicação. Iniciar sessão com a sua conta do Azure e selecione um Web site existente ou novo e anote Olá **URL de destino** propriedade no Olá **ligação** separador. Iremos dar toothis URL como o *ponto final de back-end* mais à frente neste tutorial. Clique em **Publicar**.

