---
title: "Enviar notificações push para aplicações do Chrome com Hubs de Notificação do Azure | Microsoft Docs"
description: "Aprenda a utilizar os Notification Hubs do Azure para enviar notificações push para uma Aplicação do Chrome."
services: notification-hubs
keywords: "notificações push móveis, notificações push, notificação push, notificações push do chrome"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 107c001f1b02874adfdc53856f18e6bfcbcb0cf4
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/12/2017
---
# <a name="send-push-notifications-to-chrome-apps-with-azure-notification-hubs"></a>Enviar notificações push para aplicações do Chrome com Notification Hubs do Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

Este tópico mostra-lhe como utilizar os Notification Hubs do Azure para enviar notificações push para uma Aplicação do Chrome, que será apresentada dentro do contexto do browser Google Chrome. Neste tutorial, vamos criar uma aplicação do Chrome que recebe notificações push através do [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/). 

> [!NOTE]
> Para concluir este tutorial, tem de ter uma conta ativa do Azure. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).
> 
> 

O tutorial descreve os passos básicos para ativar as notificações push:

* [Ativar o Google Cloud Messaging](#register)
* [Configurar o hub de notificação](#configure-hub)
* [Ligar a Aplicação do Chrome ao hub de notificação](#connect-app)
* [Enviar uma notificação push para a Aplicação do Chrome](#send)
* [Funcionalidades e capacidades adicionais](#next-steps)

> [!NOTE]
> As notificações push da aplicação do Chrome não são notificações genéricas no browser, são específicas para o modelo de extensibilidade do browser (consulte [Descrição Geral das Aplicações do Chrome] para obter mais detalhes). Para além do browser do ambiente de trabalho, as aplicações do Chrome também podem ser executadas em telemóveis (Android e iOS) através do Apache Cordova. Consulte [Aplicações do Chrome no Telemóvel] para saber mais.
> 
> 

A configuração do GCM e dos Notification Hubs do Azure é idêntica à configuração do Android, uma vez que o [Google Cloud Messaging para Chrome] foi preterido e o mesmo GCM suporta agora dispositivos Android e instâncias do Chrome.

## <a id="register"></a>Ativar o Google Cloud Messaging
1. Navegue para o site [Google Cloud Console], inicie sessão com as credenciais da conta Google e clique no botão **Criar Projeto**. Forneça um **Nome do Projeto** adequado e clique no botão **Criar**.
   
       ![Google Cloud Console - Create Project][1]
2. Anote o **Número do Projeto** na página **Projetos** do projeto que acabou de criar. Irá utilizá-lo como **ID do Remetente do GCM** na Aplicação do Chrome para se registar no GCM.
   
       ![Google Cloud Console - Project Number][2]
3. No painel esquerdo, clique em **APIs e autenticação**, desloque o ecrã para baixo e clique no botão de alternar para ativar o **Google Cloud Messaging para Android**. Não tem de ativar o **Google Cloud Messaging para Chrome**.
   
       ![Google Cloud Console - Server Key][3]
4. No painel esquerdo, clique em **Credenciais** > **Criar Nova Chave** > **Chave de Servidor** > **Criar**.
   
       ![Google Cloud Console - Credentials][4]
5. Tome nota da **Chave de API** do servidor. Vai configura-la a seguir no Notification Hub para o ativar para enviar notificações push para o GCM.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>Configurar o hub de notificação
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   No painel **Definições**, selecione **Serviços de Notificação** e, em seguida, **Google (GCM)**. Introduza a chave de API e clique em guardar.

&emsp;&emsp;![Notification Hubs do Azure – Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>Ligar a Aplicação do Chrome ao hub de notificação
O Notification Hub está agora configurado para trabalhar com o GCM e tem as cadeias de ligação para registar a aplicação para receber e enviar notificações push. LK

### <a name="create-a-new-chrome-app"></a>Criar uma nova Aplicação do Chrome
O exemplo abaixo baseia-se no [Exemplo de GCM para Aplicações do Chrome] e utiliza o modo recomendado para criar uma Aplicação do Chrome. Vamos dar destaque aos passos especificamente relacionados com os Notification Hubs do Azure. 

> [!NOTE]
> Recomendamos que transfira a origem para esta Aplicação do Chrome a partir do [Exemplo de Notification Hub da Aplicação do Chrome].
> 
> 

A Aplicação do Chrome é criada através de JavaScript e pode utilizar qualquer um dos seus editores de texto preferidos para a sua criação. Veja a seguir o aspeto desta Aplicação do Chrome.

![Aplicação do Google Chrome][15]

1. Crie uma pasta e dê-lhe nome `ChromePushApp`. Obviamente, o nome é arbitrário. Se lhe der um nome diferente, certifique-se de que substitui o caminho nos segmentos de código necessários.
2. Transfira a [biblioteca crypto-js]para a pasta que criou no segundo passo. Esta pasta de biblioteca irá conter duas subpastas: `components` e `rollups`.
3. Crie um ficheiro `manifest.json`. Todas as Aplicações do Chrome são acompanhadas por um ficheiro de manifesto que contém os metadados da aplicação e, mais importante ainda, todas as permissões que são concedidas à aplicação quando o utilizador a instala.
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    Repare no elemento `permissions`, que especifica que esta Aplicação do Chrome conseguirá receber notificações push do GCM. Deve também especificar o URI dos Notification Hubs do Azure em que a Aplicação do Chrome irá efetuar uma chamada REST para se registar.
    A nossa aplicação de exemplo utiliza também um ficheiro de ícone, `gcm_128.png`, que encontrará na origem, e que é reutilizado do exemplo GCM original. Pode substitui-lo por qualquer imagem que esteja em conformidade com os [critérios de ícones](https://developer.chrome.com/apps/manifest/icons).
4. Crie um ficheiro chamado `background.js` com o seguinte código:
   
        // Returns a new notification ID used in the notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs to form a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification to show the GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners to trigger the first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    Este é o ficheiro que faz aparecer a janela de HTML da Aplicação do Chrome (**register.html**) e que define também o processador **messageReceived** para processar a notificação push que chega.
5. Crie um ficheiro chamado `register.html` – isto define a IU da Aplicação do Chrome. 
   
   > [!NOTE]
   > Este exemplo utiliza **CryptoJS v3.1.2**. Se tiver transferido outra versão da biblioteca, certifique-se de que substitui corretamente a versão no caminho `src`.
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. Crie um ficheiro chamado `register.js` com o seguinte código. Este ficheiro especifica o script por detrás de `register.html`. As Aplicações do Chrome não permitem a execução inline, terá pois de criar um script de segurança separado para a IU.
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before the registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When the registration fails, handle the error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that the first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update the payload with the registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    O script acima tem os seguintes parâmetros de chave:
   
   * **window.onload** define os eventos de clique no botão dos dois botões na IU. Um é registado com o GCM e o outro utiliza o ID de registo que é devolvido após o registo com o GCM para se registar com os Notification Hubs do Azure.
   * **updateLog** é a função que nos permite lidar com capacidades de registo simples.
   * **registerWithGCM** é o processador do primeiro clique no botão, o que faz a chamada `chrome.gcm.register` para o GCM para registar a instância atual da Aplicação do Chrome.
   * **registerCallback** é a função de chamada de retorno que é chamada quando a chamada de registo do GCM é devolvida.
   * **registerWithNH** é o processador do segundo clique no botão, que regista com Notification Hubs. Obtém `hubName` e `connectionString` (que o utilizador especificou) e cria a chamada da API REST de Registo dos Notification Hubs.
   * **splitConnectionString** e **generateSaSToken** são programas de ajuda que representam a implementação JavaScript de um processo de criação de token SaS, que tem de ser utilizado em todas as chamadas da API REST. Para obter mais informações, consulte [Conceitos Comuns](http://msdn.microsoft.com/library/dn495627.aspx).
   * **sendNHRegistrationRequest** é a função que faz uma chamada REST de HTTP para os Notification Hubs do Azure.
   * **registrationPayload** define o payload XML de registo. Para obter mais informações, consulte [Criar API REST dos NH de Registo]. O ID de registo é atualizado com o que foi recebido do GCM.
   * **client** é uma instância do **XMLHttpRequest** que utilizamos para efetuar o pedido POST de HTTP. Tenha em atenção que o cabeçalho é atualizado de `Authorization` para `sasToken`. Ao concluir esta chamada com êxito registará esta instância da Aplicação do Chrome nos Notification Hubs do Azure.

A estrutura geral das pastas deste projeto deve assemelhar-se a isto: ![Aplicação do Google Chrome – Estrutura de Pastas][21]

### <a name="set-up-and-test-your-chrome-app"></a>Configurar e testar a Aplicação do Chrome
1. Abra o browser Chrome. Abra **Extensões do Chrome** e ative **Modo de programador**.
   
       ![Google Chrome - Enable Developer Mode][16]
2. Clique em **Carregar a extensão descompactada** e navegue para a pasta onde criou os ficheiros. Opcionalmente, pode também utilizar a **Ferramenta do Programador de Aplicações e Extensões do Chrome**. Esta ferramenta é ela própria uma Aplicação do Chrome (instalada a partir do Loja Online do Chrome) e fornece capacidades avançadas de depuração para o desenvolvimento da Aplicação do Chrome.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. Se a Aplicação do Chrome for criada sem erros, verá aparecer a sua Aplicação do Chrome.
   
       ![Google Chrome - Chrome App Display][18]
4. Introduza o **Número de Projeto** que obteve anteriormente da **Google Cloud Console** como ID do remetente e clique em **Registar com o GCM**. Deverá ver a mensagem **Registo com o GCM concluído com êxito.**
   
       ![Google Chrome - Chrome App Customization][19]
5. Introduza o **Nome do Notification Hub** e o **DefaultListenSharedAccessSignature** que obteve anteriormente do portal e clique em **Registar Notification Hub do Azure**. Deverá ver a mensagem **Registo do Notification Hub concluído com êxito!** e os detalhes da resposta do registo, que contém o ID de registo dos Notification Hubs do Azure.
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>Enviar uma notificação à Aplicação do Chrome
Para fins de teste, enviaremos notificações push do Chrome utilizando uma aplicação de consola do .NET. 

> [!NOTE]
> Pode enviar notificações push com Notification Hubs de qualquer back-end através da nossa <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">Interface REST</a> pública. Consulte o nosso [Portal de documentação](https://azure.microsoft.com/documentation/services/notification-hubs/) para obter mais exemplos em diferentes plataformas.
> 
> 

1. No Visual Studio, no menu **Ficheiro**, selecione **Novo** e, em seguida, **Projeto**. Em **Visual c#**, clique em **Windows**, **Aplicação de Consola** e em **OK**.  Esta ação cria um novo projeto de aplicação de consola.
2. No menu **Ferramentas**, clique em **Gestor de Pacotes de Biblioteca** e, em seguida, em **Consola do Gestor de Pacotes**. Esta ação exibe a Consola do Gestor de Pacotes.
3. Na janela da consola, execute o seguinte comando:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference to the Azure Service Bus SDK with the <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. Abra `Program.cs` e adicione a seguinte instrução `using`:
   
        using Microsoft.Azure.NotificationHubs;
5. Na classe `Program`, adicione o método seguinte:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace the connection string placeholder with the connection string called `DefaultFullSharedAccessSignature` that you obtained in the notification hub configuration section.
   
   > [!NOTE]
   > Certifique-se de que utiliza a cadeia de ligação com acesso **Completo** e não com acesso de **Escuta**. A cadeia de ligação de acesso de **Escuta** não concede permissões para enviar notificações push.
   > 
   > 
6. Adicionar o seguinte, chama o método `Main`:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Certifique-se de que o Chrome está em execução e execute a aplicação de consola.
8. Deverá ver a seguinte notificação de pop-up no ambiente de trabalho.
   
       ![Google Chrome - Notification][13]
9. Poderá ver também todas as suas notificações utilizando a janela de Notificações do Chrome na barra de tarefas (no Windows) quando estiver a executar o Chrome.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> Não precisa de ter a Aplicação do Chrome em execução ou aberta no browser (mas o browser Chrome em si deve estar em execução). Pode, também, ter uma vista consolidada de todas as suas notificações na janela de Notificações do Chrome.
> 
> 

## <a name="next-steps"> </a>Passos seguintes
Saiba mais sobre os Notification Hubs em [Descrição Geral dos Notification Hubs].

Para utilizadores específicos, consulte o tutorial [Notificar Utilizadores dos Notification Hubs do Azure]. 

Se pretender segmentar os utilizadores por grupos de interesse, pode acompanhar o tutorial [Notícias de Última Hora dos Notification Hubs do Azure].

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[Exemplo de Notification Hub da Aplicação do Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Descrição Geral dos Notification Hubs]: notification-hubs-push-notification-overview.md
[Descrição Geral das Aplicações do Chrome]: https://developer.chrome.com/apps/about_apps
[Exemplo de GCM para Aplicações do Chrome]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[Aplicações do Chrome no Telemóvel]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Criar API REST dos NH de Registo]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[biblioteca crypto-js]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging para Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Notificar Utilizadores dos Notification Hubs do Azure]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Notícias de Última Hora dos Notification Hubs do Azure]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
