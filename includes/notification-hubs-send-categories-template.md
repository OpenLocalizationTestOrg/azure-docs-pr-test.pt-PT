
<span data-ttu-id="c60e5-101">Esta secção mostra como toosend notícias como de última hora etiquetados notificações de modelo a partir de uma aplicação de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="c60e5-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="c60e5-102">Se estiver a utilizar Mobile Apps, consulte toohello [adicionar notificações push para Mobile Apps] tutorial e selecione a sua plataforma na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="c60e5-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="c60e5-103">Se quiser toouse Java ou PHP Consulte demasiado[como toouse Notification Hubs de Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="c60e5-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="c60e5-104">Pode enviar notificações a partir de qualquer back-end utilizando a [interface REST de Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="c60e5-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="c60e5-105">Ignorar os passos 1 a 3 se criou a aplicação de consola Olá para enviar notificações quando concluído [introdução aos Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="c60e5-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="c60e5-106">No Visual Studio, crie uma nova aplicação de consola do Visual c#:</span><span class="sxs-lookup"><span data-stu-id="c60e5-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="c60e5-107">No menu principal do Visual Studio Olá, clique em **ferramentas**, **Gestor de pacotes de biblioteca**, e **consola do Gestor de pacotes**, em seguida, na janela de consola Olá escreva o seguinte e prima **Introduza**:</span><span class="sxs-lookup"><span data-stu-id="c60e5-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="c60e5-108">Esta ação adiciona uma referência toohello SDK dos Notification Hubs do Azure utilizando Olá [pacote NuGet do Microsoft Hubs].</span><span class="sxs-lookup"><span data-stu-id="c60e5-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="c60e5-109">Abra o ficheiro de Olá Program.cs e adicione o seguinte Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="c60e5-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="c60e5-110">No Olá `Program` classe, adicione Olá seguinte método ou substituí-lo se já existir:</span><span class="sxs-lookup"><span data-stu-id="c60e5-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="c60e5-111">Este código envia uma notificação de modelo para cada uma das etiquetas de seis Olá na matriz da cadeia de Olá.</span><span class="sxs-lookup"><span data-stu-id="c60e5-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="c60e5-112">utilização de Olá etiquetas certifica-se de que os dispositivos recebem notificações apenas para as categorias de Olá registado.</span><span class="sxs-lookup"><span data-stu-id="c60e5-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="c60e5-113">No Olá acima código, substitua Olá `<hub name>` e `<connection string with full access>` marcadores com o notification hub nome e Olá cadeia de ligação para *DefaultFullSharedAccessSignature* a partir do dashboard de Olá do seu hub de notificação .</span><span class="sxs-lookup"><span data-stu-id="c60e5-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="c60e5-114">Adicionar Olá seguintes linhas no Olá **Main** método:</span><span class="sxs-lookup"><span data-stu-id="c60e5-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="c60e5-115">Crie aplicação de consola Olá.</span><span class="sxs-lookup"><span data-stu-id="c60e5-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[introdução aos Hubs de notificação]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[interface REST de Hubs de notificação]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[adicionar notificações push para Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[como toouse Notification Hubs de Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[pacote NuGet do Microsoft Hubs]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
