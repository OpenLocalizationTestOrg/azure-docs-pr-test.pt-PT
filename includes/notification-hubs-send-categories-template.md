
Esta secção mostra como toosend notícias como de última hora etiquetados notificações de modelo a partir de uma aplicação de consola .NET.

Se estiver a utilizar Mobile Apps, consulte toohello [adicionar notificações push para Mobile Apps] tutorial e selecione a sua plataforma na parte superior do Olá.

Se quiser toouse Java ou PHP Consulte demasiado[como toouse Notification Hubs de Java/PHP]. Pode enviar notificações a partir de qualquer back-end utilizando a [interface REST de Hubs de notificação].

Ignorar os passos 1 a 3 se criou a aplicação de consola Olá para enviar notificações quando concluído [introdução aos Hubs de notificação].

1. No Visual Studio, crie uma nova aplicação de consola do Visual c#:
   
       ![][13]
2. No menu principal do Visual Studio Olá, clique em **ferramentas**, **Gestor de pacotes de biblioteca**, e **consola do Gestor de pacotes**, em seguida, na janela de consola Olá escreva o seguinte e prima **Introduza**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Esta ação adiciona uma referência toohello SDK dos Notification Hubs do Azure utilizando Olá [pacote NuGet do Microsoft Hubs].
3. Abra o ficheiro de Olá Program.cs e adicione o seguinte Olá `using` instrução:
   
        using Microsoft.Azure.NotificationHubs;
4. No Olá `Program` classe, adicione Olá seguinte método ou substituí-lo se já existir:
   
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
   
    Este código envia uma notificação de modelo para cada uma das etiquetas de seis Olá na matriz da cadeia de Olá. utilização de Olá etiquetas certifica-se de que os dispositivos recebem notificações apenas para as categorias de Olá registado.
5. No Olá acima código, substitua Olá `<hub name>` e `<connection string with full access>` marcadores com o notification hub nome e Olá cadeia de ligação para *DefaultFullSharedAccessSignature* a partir do dashboard de Olá do seu hub de notificação .
6. Adicionar Olá seguintes linhas no Olá **Main** método:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Crie aplicação de consola Olá.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[introdução aos Hubs de notificação]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[interface REST de Hubs de notificação]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[adicionar notificações push para Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[como toouse Notification Hubs de Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[pacote NuGet do Microsoft Hubs]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
