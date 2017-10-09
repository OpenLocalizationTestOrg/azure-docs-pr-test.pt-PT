



<span data-ttu-id="db8a6-101">Enviar notificações de modelo, que basta tooprovide um conjunto de propriedades, no nosso caso, irá enviar Olá conjunto de propriedades com a versão localizada do Olá do Olá atual notícias de última hora, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="db8a6-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="db8a6-102">Esta secção mostra como notificações toosend através de uma aplicação de consola</span><span class="sxs-lookup"><span data-stu-id="db8a6-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="db8a6-103">Olá incluídos código difusões tooboth Windows Store e dispositivos iOS, uma vez que o back-end de Olá pode difusão tooany de dispositivos de Olá suportado.</span><span class="sxs-lookup"><span data-stu-id="db8a6-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="db8a6-104">notificações de toosend através de uma aplicação de consola c#</span><span class="sxs-lookup"><span data-stu-id="db8a6-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="db8a6-105">Modificar Olá `SendTemplateNotificationAsync` método na aplicação de consola Olá que criou anteriormente com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="db8a6-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="db8a6-106">Repare como neste caso, há toosend sem necessidade de várias notificações para diferentes regiões e plataformas.</span><span class="sxs-lookup"><span data-stu-id="db8a6-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


<span data-ttu-id="db8a6-107">Tenha em atenção que esta chamada simple fornecerá informação de localizada Olá de notícias demasiado**todos os** os seus dispositivos, independentemente da plataforma de Olá, como o Notification Hub baseia-se e fornece Olá correto de dispositivos do payload nativo tooall Olá subscreveram tag específica tooa.</span><span class="sxs-lookup"><span data-stu-id="db8a6-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="db8a6-108">Enviar notificação de Olá com os Mobile Services</span><span class="sxs-lookup"><span data-stu-id="db8a6-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="db8a6-109">No seu agendador do serviço móvel, pode utilizar Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="db8a6-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


