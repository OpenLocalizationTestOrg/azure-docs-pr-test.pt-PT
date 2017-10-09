<span data-ttu-id="2035c-101">Utilize o procedimento de Olá que corresponde ao seu tipo de projeto de back-end&mdash;ou [.NET back-end](#dotnet) ou [back-end Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="2035c-101">Use hello procedure that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="2035c-102"><a name="dotnet"></a>Projeto de back-end do .NET</span><span class="sxs-lookup"><span data-stu-id="2035c-102"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="2035c-103">No Visual Studio, clique no projeto de servidor Olá e clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2035c-103">In Visual Studio, right-click hello server project, and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="2035c-104">Procurar `Microsoft.Azure.NotificationHubs`e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="2035c-104">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="2035c-105">Esta ação instala a biblioteca de clientes Olá Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="2035c-105">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="2035c-106">Na pasta de controladores Olá, abra TodoItemController.cs e adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="2035c-106">In hello Controllers folder, open TodoItemController.cs and add hello following `using` statements:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. <span data-ttu-id="2035c-107">Substitua Olá `PostTodoItem` método com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="2035c-107">Replace hello `PostTodoItem` method with hello following code:</span></span>  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
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

            // Android payload
            var androidNotificationPayload = "{ \"data\" : {\"message\":\"" + item.Text + "\"}}";

            try
            {
                // Send hello push notification and log hello results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write hello success result toohello logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write hello failure result toohello logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. <span data-ttu-id="2035c-108">Voltar a publicar o projeto de servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="2035c-108">Republish hello server project.</span></span>

### <span data-ttu-id="2035c-109"><a name="nodejs"></a>Projeto de back-end do node.js</span><span class="sxs-lookup"><span data-stu-id="2035c-109"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="2035c-110">Se ainda não o tiver feito deste modo, [transferir o projeto de início rápido Olá](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), ou utilize senão Olá [editor online no portal do Azure de Olá](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="2035c-110">If you haven't already done so, [download hello quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="2035c-111">Substitua o código existente do Olá no ficheiro de todoitem.js Olá com seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="2035c-111">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a GCM native notification.
                    context.push.gcm.send(null, payload, function (error) {
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

    <span data-ttu-id="2035c-112">Esta ação envia uma notificação de GCM que contém Olá item.text Quando é inserido um novo item de todo.</span><span class="sxs-lookup"><span data-stu-id="2035c-112">This sends a GCM notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="2035c-113">Ao editar o ficheiro de Olá no seu computador local, voltar a publicar o projeto de servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="2035c-113">When editing hello file in your local computer, republish hello server project.</span></span>
