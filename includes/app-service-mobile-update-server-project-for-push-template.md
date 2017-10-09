Nesta secção, atualizar código na sua toosend de projeto de back-end das Mobile Apps existente uma notificação push sempre que é adicionado um novo item. Esta utiliza a tecnologia de Olá [modelo](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) funcionalidade dos Notification Hubs do Azure, permitindo pushes de várias plataformas. Olá vários clientes estão registados para notificações push através de modelos e um único push universal pode obter tooall plataformas de cliente.

Escolha uma das Olá seguindo os procedimentos que corresponde ao seu tipo de projeto de back-end&mdash;ou [.NET back-end](#dotnet) ou [back-end Node.js](#nodejs).

### <a name="dotnet"></a>Projeto de back-end do .NET
1. No Visual Studio, clique no projeto de servidor Olá e clique em **gerir pacotes NuGet**. Procurar `Microsoft.Azure.NotificationHubs`e, em seguida, clique em **instalar**. Esta ação instala a biblioteca de Notification Hubs Olá para enviar notificações a partir do seu back-end.
2. No projeto de servidor Olá, abra **controladores** > **TodoItemController.cs**e adicione Olá seguintes instruções de utilização:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. No Olá **PostTodoItem** método, adicione o seguinte código após a chamada de Olá demasiado de Olá**InsertAsync**:  

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Esta ação envia uma notificação de modelo contém item de Olá. Texto quando é inserido um novo item.
4. Voltar a publicar o projeto de servidor Olá.

### <a name="nodejs"></a>Projeto de back-end do node.js
1. Se ainda não o tiver feito deste modo, [transferir o projeto de back-end de início rápido Olá](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), ou utilize senão Olá [editor online no portal do Azure de Olá](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Substitua o código existente do Olá no todoitem.js com seguinte Olá:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    Esta ação envia uma notificação de modelo contém Olá item.text Quando é inserido um novo item.
3. Ao editar o ficheiro de Olá no seu computador local, voltar a publicar o projeto de servidor Olá.
