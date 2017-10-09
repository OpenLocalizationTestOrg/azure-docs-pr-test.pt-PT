## <a name="webapi-project"></a><span data-ttu-id="4df7c-101">End WebAPI projeto</span><span class="sxs-lookup"><span data-stu-id="4df7c-101">WebAPI Project</span></span>
1. <span data-ttu-id="4df7c-102">No Visual Studio, abra Olá **AppBackend** projeto que criou no Olá **notificam os utilizadores** tutorial.</span><span class="sxs-lookup"><span data-stu-id="4df7c-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="4df7c-103">No Notifications.cs, substituir Olá todo **notificações** classe com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="4df7c-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="4df7c-104">Ser se tooreplace Olá marcadores de posição pela cadeia de ligação (com acesso total) para o seu hub de notificação e o nome do hub Olá.</span><span class="sxs-lookup"><span data-stu-id="4df7c-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="4df7c-105">Pode obter estes valores de Olá [Portal clássico do Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4df7c-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="4df7c-106">Este módulo representa agora Olá diferentes segura notificações que serão enviadas.</span><span class="sxs-lookup"><span data-stu-id="4df7c-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="4df7c-107">Uma implementação completa, as notificações de Olá serão armazenadas numa base de dados; de simplicidade, neste caso, iremos armazená-las na memória.</span><span class="sxs-lookup"><span data-stu-id="4df7c-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
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

1. <span data-ttu-id="4df7c-108">No NotificationsController.cs, substitua o código de Olá dentro de Olá **NotificationsController** definição de classe com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="4df7c-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="4df7c-109">Este componente implementa uma forma de notificação de Olá Olá dispositivo tooretrieve de forma segura e também fornece uma forma (para fins de Olá deste tutorial) tootrigger um dispositivos de tooyour push segura.</span><span class="sxs-lookup"><span data-stu-id="4df7c-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="4df7c-110">Tenha em atenção que ao enviar o hub de notificação de toohello de notificação de Olá, apenas Enviámos uma notificação não processada, com o ID de Olá de notificação de Olá (e não existem mensagens real):</span><span class="sxs-lookup"><span data-stu-id="4df7c-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
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


<span data-ttu-id="4df7c-111">Tenha em atenção que Olá `Post` método agora não enviar uma notificação de alerta.</span><span class="sxs-lookup"><span data-stu-id="4df7c-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="4df7c-112">Envia uma notificação em bruto que contém o ID de notificação de Olá apenas e não a qualquer conteúdo confidencial.</span><span class="sxs-lookup"><span data-stu-id="4df7c-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="4df7c-113">Além disso, certifique-Olá toocomment se de que a operação para plataformas de Olá para os quais não tem credenciais configuradas no seu hub de notificação, conforme irá causar erros de envio.</span><span class="sxs-lookup"><span data-stu-id="4df7c-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="4df7c-114">Agora vamos reimplementar esta tooan de aplicação Web site do Azure na ordem toomake-lo acessível a partir de todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4df7c-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="4df7c-115">Clique com o botão direito no Olá **AppBackend** projeto e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="4df7c-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="4df7c-116">Selecione o Web site do Azure como o destino da publicação.</span><span class="sxs-lookup"><span data-stu-id="4df7c-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="4df7c-117">Iniciar sessão com a sua conta do Azure e selecione um Web site existente ou novo e anote Olá **URL de destino** propriedade no Olá **ligação** separador. Iremos dar toothis URL como o *ponto final de back-end* mais à frente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="4df7c-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="4df7c-118">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="4df7c-118">Click **Publish**.</span></span>

