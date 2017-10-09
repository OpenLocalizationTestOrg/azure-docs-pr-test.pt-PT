---
title: "aaaSending notificações de push com Notification Hubs do Azure e o Node.js"
description: "Saiba como toouse Notification Hubs toosend notificações push a partir de uma aplicação Node.js."
keywords: "notificação push, push notifications,node.js push, push de ios"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Enviar notificações push com Notification Hubs do Azure e o Node.js
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Descrição geral
> [!IMPORTANT]
> toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).
> 
> 

Este guia irá mostrar como toosend notificações push com a ajuda de Olá dos Notification Hubs do Azure diretamente a partir de uma aplicação Node.js. 

cenários de Olá abrangidos incluem a enviar tooapplications de notificações push no Olá seguintes plataformas:

* Android
* iOS
* Windows Phone
* Plataforma universal do Windows 

Para obter mais informações sobre os notification hubs, consulte Olá [passos](#next) secção.

## <a name="what-are-notification-hubs"></a>O que são os Hubs de Notificação?
Os Hubs de notificação do Azure fornecem uma infraestrutura de fácil utilização, várias plataforma, dimensionável para envio de dispositivos de toomobile de notificações push. Para obter detalhes sobre a infraestrutura de serviço Olá, consulte Olá [Notification Hubs do Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) página.

## <a name="create-a-nodejs-application"></a>Criar uma aplicação Node.js
Olá primeiro passo para este tutorial está a criar uma nova aplicação Node.js em branco. Para obter instruções sobre como criar uma aplicação Node.js, consulte [criar e implementar uma tooAzure de aplicação Node.js do Web Site][nodejswebsite], [serviço em nuvem de Node.js] [ Node.js Cloud Service] através do Windows PowerShell, ou [Web Site com o WebMatrix].

## <a name="configure-your-application-toouse-notification-hubs"></a>Configurar a sua aplicação tooUse Notification Hubs
toouse Notification Hubs do Azure, terá de toodownload e utilize Olá Node.js [pacote do azure](https://www.npmjs.com/package/azure), que inclui um conjunto de bibliotecas de programa auxiliar que comunicam com os serviços de REST de notificação de push Olá incorporado.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utilizar o Gestor de pacote de nó (NPM) tooobtain Olá pacote
1. Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Linux) e navegue pasta toohello onde criou a aplicação em branco .
2. Tipo **npm instalar azure sb** na janela de comandos Olá.
3. Pode executar manualmente Olá **ls** ou **dir** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta, determinar Olá **azure** pacote, que contém as bibliotecas de Olá terá tooaccess Olá Notification Hub.

> [!NOTE]
> Pode saber mais sobre a instalação de NPM no oficial Olá [NPM blogue](http://blog.npmjs.org/post/85484771375/how-to-install-npm). 
> 
> 

### <a name="import-hello-module"></a>Módulo Olá de importação
Com um editor de texto, adicionar Olá seguir toohello superior de Olá **server.js** ficheiro da aplicação Olá:

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Configurar uma ligação do Hub de notificação do Azure
Olá **NotificationHubService** objeto permite-lhe trabalhar com os notification hubs. Olá código seguinte cria um **NotificationHubService** objeto para o hub de nofication Olá denominado **hubname**. Adicionar perto Olá parte superior do Olá **server.js** ficheiro, após o módulo do Olá instrução tooimport Olá do azure:

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Olá ligação **connectionstring** Olá pode obter o valor [Portal do Azure] efetuando Olá os seguintes passos:

1. No painel de navegação esquerdo Olá, clique em **procurar**.
2. Selecione **Notification Hubs**e, em seguida, o hub de Olá localizar desejar toouse para exemplo Olá. Pode consultar toohello [Windows Store introdução tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) se precisar de ajuda para criar um novo Hub de notificação.
3. Selecione **definições**.
4. Clique em **políticas de acesso**. Verá ambas as cadeias de ligação de acesso partilhado e completa.

![Portal do Azure – os Hubs de notificação](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> Também pode obter a cadeia de ligação de Olá utilizando Olá **Get-AzureSbNamespace** cmdlet fornecida pelo [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou Olá **mostrar de espaço de nomes do azure sb** comando com Olá [Interface de linha de comandos do Azure (CLI do Azure)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Arquitetura geral
Olá **NotificationHubService** objeto expõe Olá seguintes instâncias de objeto para envio de dispositivos de toospecific de notificações push e de aplicações:

* **Android** -utilizar Olá **GcmService** objeto que está disponível em **notificationHubService.gcm**
* **iOS** -utilizar Olá **ApnsService** objeto que está acessível na **notificationHubService.apns**
* **Windows Phone** -utilizar Olá **MpnsService** objeto que está disponível em **notificationHubService.mpns**
* **Plataforma universal do Windows** -utilizar Olá **WnsService** objeto que está disponível em **notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>Como: enviar aplicações tooAndroid de notificações de push
Olá **GcmService** objeto fornece um **enviar** método que pode ser utilizado toosend push notificações tooAndroid aplicações. Olá **enviar** método aceita Olá os seguintes parâmetros:

* **Etiquetas** -Olá identificador da etiqueta. Se não for fornecido nenhum tag, Olá notificação será enviada tooall clientes.
* **Payload** -Olá JSON ou payload de cadeia não processados da mensagem.
* **Chamada de retorno** -Olá a função de chamada de retorno.

Para obter mais informações sobre o formato de payload Olá, consulte Olá **Payload** secção Olá [implementar o servidor do GCM](http://developer.android.com/google/gcm/server.html#payload) documento.

Olá código seguinte utiliza Olá **GcmService** instância exposta pelo Olá **NotificationHubService** toosend um tooall de notificação push registado clientes.

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>Como: enviar aplicações tooiOS de notificações de push
Mesmo tal como acontece com as aplicações Android descrita acima, Olá **ApnsService** objeto fornece um **enviar** método que pode ser utilizado toosend push notificações tooiOS aplicações. Olá **enviar** método aceita Olá os seguintes parâmetros:

* **Etiquetas** -Olá identificador da etiqueta. Se não for fornecido nenhum tag, Olá notificação será enviada tooall clientes.
* **Payload** - Olá JSON da mensagem ou payload de cadeia.
* **Chamada de retorno** -Olá a função de chamada de retorno.

Para o formato de payload de Olá de mais informações, consulte Olá **notificação Payload** secção Olá [guia de programação de notificações de Push e Local](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) documento.

Olá código seguinte utiliza Olá **ApnsService** instância exposta pelo Olá **NotificationHubService** toosend um alerta mensagem tooall clientes:

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>Como: enviar aplicações de Phone tooWindows notificações de push
Olá **MpnsService** objeto fornece um **enviar** método que pode ser utilizado toosend push notificações tooWindows aplicações Phone. Olá **enviar** método aceita Olá os seguintes parâmetros:

* **Etiquetas** -Olá identificador da etiqueta. Se não for fornecido nenhum tag, Olá notificação será enviada tooall clientes.
* **Payload** -Olá payload XML da mensagem.
* **TargetName**  -  `toast` para notificações de alerta. `token`Para obter notificações do mosaico.
* **NotificationClass** -Olá prioridade de notificação de Olá. Consulte Olá **elementos de cabeçalho de HTTP** secção Olá [notificações Push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx) documento para os valores válidos.
* **Opções de** - opcional cabeçalhos de pedido.
* **Chamada de retorno** -Olá a função de chamada de retorno.

Para obter uma lista válida de **TargetName**, **NotificationClass** e opções de cabeçalho, veja Olá [notificações Push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx) página.

Olá, código de exemplo a seguir utiliza Olá **MpnsService** instância exposta pelo Olá **NotificationHubService** toosend uma notificação push de alerta:

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>Como: enviar aplicações de plataforma do Windows (UWP) de tooUniversal notificações de push
Olá **WnsService** objeto fornece um **enviar** método que pode ser utilizado toosend push notificações tooUniversal plataforma Windows aplicações.  Olá **enviar** método aceita Olá os seguintes parâmetros:

* **Etiquetas** -Olá identificador da etiqueta. Se não for fornecido nenhum tag, Olá notificação será enviada clientes tooall registado.
* **Payload** -payload da mensagem Olá XML.
* **Tipo** -Olá o tipo de notificação.
* **Opções de** - opcional cabeçalhos de pedido.
* **Chamada de retorno** -Olá a função de chamada de retorno.

Para obter uma lista de tipos válidos e cabeçalhos de pedido, consulte [Push cabeçalhos de pedido e resposta do serviço de notificação](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Olá código seguinte utiliza Olá **WnsService** instância exposta pelo Olá **NotificationHubService** toosend uma aplicação UWP tooa de notificação de push de alerta:

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Passos Seguintes
fragmentos de exemplo de Olá acima permitem tooeasily compilação serviço infraestrutura toodeliver push notificações tooa ampla variedade de dispositivos. Agora que aprendeu as noções básicas de Olá de utilizar os Notification Hubs com o node.js, siga estas toolearn ligações mais informações sobre como pode expandir ainda mais estas capacidades.

* Consulte Olá referência do MSDN para [Notification Hubs do Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Visite Olá [Azure SDK para o nó] repositório no GitHub para obter mais exemplos e detalhes de implementação.

[Azure SDK para o nó]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[Web Site com o WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Portal do Azure]: https://portal.azure.com
