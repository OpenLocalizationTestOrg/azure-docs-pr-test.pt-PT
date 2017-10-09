
* <span data-ttu-id="97fcb-101">**Back-end do .NET (c#)**:</span><span class="sxs-lookup"><span data-stu-id="97fcb-101">**.NET backend (C#)**:</span></span>      
  
  1. <span data-ttu-id="97fcb-102">No Visual Studio, clique no projeto de servidor Olá e clique em **gerir pacotes NuGet**, procure `Microsoft.Azure.NotificationHubs`, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="97fcb-102">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.NotificationHubs`, then click **Install**.</span></span> <span data-ttu-id="97fcb-103">Esta ação instala a biblioteca de Notification Hubs Olá para enviar notificações de back-end.</span><span class="sxs-lookup"><span data-stu-id="97fcb-103">This installs hello Notification Hubs library for sending notifications from your backend.</span></span>
  2. <span data-ttu-id="97fcb-104">No projeto do Visual Studio do Olá back-end, abra **controladores** > **TodoItemController.cs**.</span><span class="sxs-lookup"><span data-stu-id="97fcb-104">In hello backend's Visual Studio project, open **Controllers** > **TodoItemController.cs**.</span></span> <span data-ttu-id="97fcb-105">Olá parte superior do ficheiro de Olá, adicione o seguinte de Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="97fcb-105">At hello top of hello file, add hello following `using` statement:</span></span>
     
          using Microsoft.Azure.Mobile.Server.Config;
          using Microsoft.Azure.NotificationHubs;

    3. <span data-ttu-id="97fcb-106">Substitua Olá `PostTodoItem` método com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="97fcb-106">Replace hello `PostTodoItem` method with hello following code:</span></span>  

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

                // iOS payload
                var appleNotificationPayload = "{\"aps\":{\"alert\":\"" + item.Text + "\"}}";

                try
                {
                    // Send hello push notification and log hello results.
                    var result = await hub.SendAppleNativeNotificationAsync(appleNotificationPayload);

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

    4. <span data-ttu-id="97fcb-107">Voltar a publicar o projeto de servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="97fcb-107">Republish hello server project.</span></span>

* <span data-ttu-id="97fcb-108">**Back-end node.js** :</span><span class="sxs-lookup"><span data-stu-id="97fcb-108">**Node.js backend** :</span></span> 
  
  1. <span data-ttu-id="97fcb-109">Se ainda não o tiver feito deste modo, [transferir o projeto de início rápido Olá](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) ou utilize senão Olá [editor online no portal do Azure de Olá](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="97fcb-109">If you haven't already done so, [download hello quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>    
  2. <span data-ttu-id="97fcb-110">Substitua o script de tabela Olá todoitem.js com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="97fcb-110">Replace hello todoitem.js table script with hello following code:</span></span>

            var azureMobileApps = require('azure-mobile-apps'),
                promises = require('azure-mobile-apps/src/utilities/promises'),
                logger = require('azure-mobile-apps/src/logger');

            var table = azureMobileApps.table();

            // When adding record, send a push notification via APNS
            table.insert(function (context) {
                // For details of hello Notification Hubs JavaScript SDK, 
                // see http://aka.ms/nodejshubs
                logger.info('Running TodoItem.insert');

                // Create a payload that contains hello new item Text.
                var payload = "{\"aps\":{\"alert\":\"" + context.item.text + "\"}}";

                // Execute hello insert; Push as a post-execute action when results are returned as a Promise.
                return context.execute()
                    .then(function (results) {
                        // Only do hello push if configured
                        if (context.push) {
                            context.push.apns.send(null, payload, function (error) {
                                if (error) {
                                    logger.error('Error while sending push notification: ', error);
                                } else {
                                    logger.info('Push notification sent successfully!');
                                }
                            });
                        }
                        return results;
                    })
                    .catch(function (error) {
                        logger.error('Error while running context.execute: ', error);
                    });
            });

            module.exports = table;

    2. <span data-ttu-id="97fcb-111">Ao editar o ficheiro de Olá no seu computador local, voltar a publicar o projeto de servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="97fcb-111">When editing hello file on your local computer, republish hello server project.</span></span>
