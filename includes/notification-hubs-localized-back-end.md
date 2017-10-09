



Enviar notificações de modelo, que basta tooprovide um conjunto de propriedades, no nosso caso, irá enviar Olá conjunto de propriedades com a versão localizada do Olá do Olá atual notícias de última hora, por exemplo:

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


Esta secção mostra como notificações toosend através de uma aplicação de consola

Olá incluídos código difusões tooboth Windows Store e dispositivos iOS, uma vez que o back-end de Olá pode difusão tooany de dispositivos de Olá suportado.

### <a name="toosend-notifications-using-a-c-console-app"></a>notificações de toosend através de uma aplicação de consola c#
Modificar Olá `SendTemplateNotificationAsync` método na aplicação de consola Olá que criou anteriormente com Olá seguinte código. Repare como neste caso, há toosend sem necessidade de várias notificações para diferentes regiões e plataformas.

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


Tenha em atenção que esta chamada simple fornecerá informação de localizada Olá de notícias demasiado**todos os** os seus dispositivos, independentemente da plataforma de Olá, como o Notification Hub baseia-se e fornece Olá correto de dispositivos do payload nativo tooall Olá subscreveram tag específica tooa.

### <a name="sending-hello-notification-with-mobile-services"></a>Enviar notificação de Olá com os Mobile Services
No seu agendador do serviço móvel, pode utilizar Olá seguintes script:

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


