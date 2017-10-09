---
title: "notificações de push aaaSending com Hubs de notificação do Azure no Windows Phone | Microsoft Docs"
description: "Neste tutorial, saiba como notificações de toopush de Notification Hubs do Azure toouse tooa do Windows Phone 8 ou Windows Phone 8.1 Silverlight aplicação."
services: notification-hubs
documentationcenter: windows
keywords: "notificação push, notificação push, push window phone"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Enviar notificações push com os Notification Hubs do Azure no Windows Phone
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Descrição geral
> [!NOTE]
> toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).
> 
> 

Este tutorial mostra como toouse Notification Hubs do Azure toosend push notificações tooa Windows Phone 8 ou Windows Phone 8.1 Silverlight a aplicação. Se tiver como objetivo o Windows Phone 8.1 (não Silverlight), consulte toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versão.
Neste tutorial, crie uma aplicação Windows Phone 8 em branco que recebe notificações push utilizando Olá serviço de notificação Push da Microsoft (MPNS). Quando tiver terminado, será capaz de toouse sua toobroadcast de hub de notificação push dispositivos Olá tooall de notificações executar a sua aplicação.

> [!NOTE]
> Olá Windows Phone SDK dos Notification Hubs não suporta a utilização Olá Push notificação serviço Windows (WNS) com aplicações do Windows Phone 8.1 Silverlight. toouse WNS (em vez do MPNS) com aplicações do Windows Phone 8.1 Silverlight, siga Olá [Notification Hubs – Windows Phone Silverlight tutorial], que utiliza a REST APIs.
> 
> 

tutorial de Olá demonstra Olá cenário de difusão simples utilizando Notification Hubs.

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte Olá:

* [Visual Studio 2012 Express para Windows Phone] ou uma versão posterior.

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais de Notification Hubs para aplicações Windows Phone 8.

## <a name="create-your-notification-hub"></a>Criar o Notification Hub
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Clique em Olá <b>serviços de notificação</b> secção (dentro <i>definições</i>), clique em <b>Windows Phone (MPNS)</b> e, em seguida, clique em Olá <b>ativar push não autenticado </b> caixa de verificação.</p>
</li>
</ol>

&emsp;&emsp;![Portal do Azure – Ativar notificações push não autenticadas](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

O hub está agora criado e configurado toosend não autenticado de notificação para o Windows Phone.

> [!NOTE]
> Este tutorial utiliza MPNS no modo não autenticado. O modo MPNS não autenticado vem com restrições sobre as notificações que pode enviar tooeach canal. Os Notification Hubs suportam [modo MPNS autenticado](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) , permitindo-lhe tooupload o certificado.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>Ligar o seu hub de notificação de toohello de aplicação
1. No Visual Studio, crie uma nova aplicação do Windows Phone 8.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    No Visual Studio 2013 Update 2 ou posterior crie, em vez disso, uma aplicação Silverlight do Windows Phone.
   
    ![Visual Studio – Novo Projeto – Aplicação em Branco – Windows Phone Silverlight][11]
2. No Visual Studio, faça duplo clique solução Olá e, em seguida, clique em **gerir pacotes NuGet**.
   
    Esta ação apresenta Olá **gerir pacotes NuGet** caixa de diálogo.
3. Procurar `WindowsAzure.Messaging.Managed` e clique em **instalar**e, em seguida, aceite os termos de Olá de utilização.
   
    ![Visual Studio – Gestor de Pacotes NuGet][20]
   
    Isto transfere, instala e adiciona uma biblioteca de mensagens do Azure de toohello de referência para o Windows utilizando o Olá <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacote NuGet Windowsazure</a>.
4. Abra o ficheiro de Olá App.xaml.cs e adicione o seguinte Olá `using` instruções:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. Adicionar Olá seguinte código na parte superior de Olá de **Application_Launching** método em App.xaml.cs:
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > Olá valor **MyPushChannel** é um índice que é utilizado toolookup um canal existente na Olá [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) coleção. Se não existir, crie uma nova entrada com esse nome.
   > 
   > 
   
    Certifique-se tooinsert Olá nome da cadeia de ligação do hub e Olá chamado **DefaultListenSharedAccessSignature** que obteve na secção anterior Olá.
    Este código obtém Olá URI do canal para aplicação Olá do MPNS e, em seguida, regista esse URI de canal no notification hub. Esta ação garante também que Olá URI do canal que é registado no notification hub que é iniciada a cada aplicação Olá do tempo.
   
   > [!NOTE]
   > Este tutorial envia um dispositivo de toohello de notificação de alerta. Enviar uma notificação de mosaico, em vez disso, tem de chamar Olá **BindToShellTile** método no canal Olá. toosupport notificações de alerta e o mosaico, chame **BindToShellTile** e **BindToShellToast**.
   > 
   > 
6. No Explorador de soluções, expanda **propriedades**, abra Olá `WMAppManifest.xml` de ficheiros, clique em Olá **capacidades** separador e certifique-se de que Olá **ID_CAP_PUSH_NOTIFICATION** está selecionada.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. Olá prima `F5` toorun chave Olá aplicação.
   
    É apresentada uma mensagem de registo na aplicação Olá.
8. Aplicação Olá fechar.  
   
   > [!NOTE]
   > tooreceive uma alerta de notificação push, aplicação Olá deve não estar em execução em primeiro plano do Olá.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>Enviar notificações push a partir do back-end
Pode enviar notificações push com os Notification Hubs de qualquer back-end através de public Olá <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>. Neste tutorial, enviará notificações push utilizando uma aplicação .NET de consola. 

Para obter um exemplo de como toosend notificações push de um back-end de ASP.NET WebAPI que esteja integrado com Notification Hubs, consulte [Azure Notification Hubs notificam os utilizadores com back-end .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).  

Para obter um exemplo de como notificações de push toosend utilizando Olá [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), veja [como toouse Notification Hubs de Java](notification-hubs-java-push-notification-tutorial.md) e [como toouse Notification Hubs de PHP](notification-hubs-php-push-notification-tutorial.md) .

1. Solução Olá de contexto, selecione **adicionar** e **novo projeto...** e, em **Visual c#**, clique em **Windows** e **aplicação de consola**e clique em **OK**.
   
       ![Visual Studio - New Project - Console Application][6]
   
    Esta ação adiciona uma nova Visual c# consola toohello solução de aplicação. Também pode fazer isto numa solução separada.
2. Clique em **Ferramentas**, clique em **Gestor de Pacotes de Biblioteca** e, em seguida, em **Consola do Gestor de Pacotes**.
   
    Esta ação apresenta Olá consola do Gestor de pacotes.
3. No Olá **consola do Gestor de pacotes** janela, conjunto Olá **projeto predefinido** tooyour novo projeto de aplicação de consola e, em seguida, na janela de consola Olá, executar Olá os seguintes comandos:
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   Esta ação adiciona uma referência toohello SDK dos Notification Hubs do Azure utilizando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet do Microsoft Hubs</a>.
4. Abra Olá `Program.cs` de ficheiros e adicione o seguinte Olá `using` instrução:
   
        using Microsoft.Azure.NotificationHubs;
5. No Olá `Program` classe, adicione Olá método os seguintes:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    Certifique-se de que tooreplace Olá `<hub name>` marcador de posição com nome Olá Olá notification hub que aparece no portal de Olá. Além disso, substitua o marcador de posição de cadeia de ligação de Olá pela cadeia de ligação de Olá chamada **DefaultFullSharedAccessSignature** que obteve na secção de Olá "Configurar o notification hub".
   
   > [!NOTE]
   > Certifique-se de que utiliza a cadeia de ligação de Olá com **completa** e não com acesso **escutar** acesso. cadeia de ligação de acesso escuta Olá não tem as notificações de push de toosend permissões.
   > 
   > 
6. Adicionar Olá seguinte linha no seu `Main` método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Com o seu Windows Phone emulador em execução e o projeto de aplicação de consola do aplicação Olá fechada, defina como Olá predefinido projeto de arranque e, em seguida, prima Olá `F5` toorun chave Olá aplicação.
   
    Receberá um alerta de notificação push. Tocar Olá faixa do alerta carrega a aplicação Olá.

Pode encontrar todos os payloads possíveis de Olá no Olá [catálogo de alertas] e [catálogo de mosaicos] tópicos no MSDN.

## <a name="next-steps"></a>Passos seguintes
Neste exemplo simples, difundiu tooall de notificações push os seus dispositivos Windows Phone 8. 

Na ordem tootarget utilizadores específicos, consulte toohello [utilizar Notification Hubs toopush notificações toousers] tutorial. 

Se pretender que toosegment os seus utilizadores por grupos de interesse, pode ler [toosend utilizar Notification Hubs notícias de última hora]. 

Saiba mais sobre como os Hubs de notificação de toouse em [documentação de orientação dos Notification Hubs].

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express para Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[documentação de orientação dos Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[utilizar Notification Hubs toopush notificações toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend utilizar Notification Hubs notícias de última hora]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[catálogo de alertas]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[catálogo de mosaicos]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs – Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

