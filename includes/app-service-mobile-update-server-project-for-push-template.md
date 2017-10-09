<span data-ttu-id="ca55c-101">Nesta secção, atualizar código na sua toosend de projeto de back-end das Mobile Apps existente uma notificação push sempre que é adicionado um novo item.</span><span class="sxs-lookup"><span data-stu-id="ca55c-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="ca55c-102">Esta utiliza a tecnologia de Olá [modelo](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) funcionalidade dos Notification Hubs do Azure, permitindo pushes de várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="ca55c-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="ca55c-103">Olá vários clientes estão registados para notificações push através de modelos e um único push universal pode obter tooall plataformas de cliente.</span><span class="sxs-lookup"><span data-stu-id="ca55c-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="ca55c-104">Escolha uma das Olá seguindo os procedimentos que corresponde ao seu tipo de projeto de back-end&mdash;ou [.NET back-end](#dotnet) ou [back-end Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="ca55c-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="ca55c-105"><a name="dotnet"></a>Projeto de back-end do .NET</span><span class="sxs-lookup"><span data-stu-id="ca55c-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="ca55c-106">No Visual Studio, clique no projeto de servidor Olá e clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ca55c-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="ca55c-107">Procurar `Microsoft.Azure.NotificationHubs`e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="ca55c-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="ca55c-108">Esta ação instala a biblioteca de Notification Hubs Olá para enviar notificações a partir do seu back-end.</span><span class="sxs-lookup"><span data-stu-id="ca55c-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="ca55c-109">No projeto de servidor Olá, abra **controladores** > **TodoItemController.cs**e adicione Olá seguintes instruções de utilização:</span><span class="sxs-lookup"><span data-stu-id="ca55c-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="ca55c-110">No Olá **PostTodoItem** método, adicione o seguinte código após a chamada de Olá demasiado de Olá**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="ca55c-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

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

    <span data-ttu-id="ca55c-111">Esta ação envia uma notificação de modelo contém item de Olá. Texto quando é inserido um novo item.</span><span class="sxs-lookup"><span data-stu-id="ca55c-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="ca55c-112">Voltar a publicar o projeto de servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="ca55c-112">Republish hello server project.</span></span>

### <span data-ttu-id="ca55c-113"><a name="nodejs"></a>Projeto de back-end do node.js</span><span class="sxs-lookup"><span data-stu-id="ca55c-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="ca55c-114">Se ainda não o tiver feito deste modo, [transferir o projeto de back-end de início rápido Olá](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), ou utilize senão Olá [editor online no portal do Azure de Olá](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="ca55c-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="ca55c-115">Substitua o código existente do Olá no todoitem.js com seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="ca55c-115">Replace hello existing code in todoitem.js with hello following:</span></span>

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

    <span data-ttu-id="ca55c-116">Esta ação envia uma notificação de modelo contém Olá item.text Quando é inserido um novo item.</span><span class="sxs-lookup"><span data-stu-id="ca55c-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="ca55c-117">Ao editar o ficheiro de Olá no seu computador local, voltar a publicar o projeto de servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="ca55c-117">When editing hello file on your local computer, republish hello server project.</span></span>
