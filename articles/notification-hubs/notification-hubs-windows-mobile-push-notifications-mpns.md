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
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="4f51b-104">Enviar notificações push com os Notification Hubs do Azure no Windows Phone</span><span class="sxs-lookup"><span data-stu-id="4f51b-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="4f51b-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="4f51b-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="4f51b-106">toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4f51b-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="4f51b-107">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="4f51b-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4f51b-108">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="4f51b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="4f51b-109">Este tutorial mostra como toouse Notification Hubs do Azure toosend push notificações tooa Windows Phone 8 ou Windows Phone 8.1 Silverlight a aplicação.</span><span class="sxs-lookup"><span data-stu-id="4f51b-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="4f51b-110">Se tiver como objetivo o Windows Phone 8.1 (não Silverlight), consulte toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versão.</span><span class="sxs-lookup"><span data-stu-id="4f51b-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="4f51b-111">Neste tutorial, crie uma aplicação Windows Phone 8 em branco que recebe notificações push utilizando Olá serviço de notificação Push da Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="4f51b-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using hello Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="4f51b-112">Quando tiver terminado, será capaz de toouse sua toobroadcast de hub de notificação push dispositivos Olá tooall de notificações executar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="4f51b-112">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="4f51b-113">Olá Windows Phone SDK dos Notification Hubs não suporta a utilização Olá Push notificação serviço Windows (WNS) com aplicações do Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="4f51b-113">hello Notification Hubs Windows Phone SDK does not support using hello Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="4f51b-114">toouse WNS (em vez do MPNS) com aplicações do Windows Phone 8.1 Silverlight, siga Olá [Notification Hubs – Windows Phone Silverlight tutorial], que utiliza a REST APIs.</span><span class="sxs-lookup"><span data-stu-id="4f51b-114">toouse WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow hello [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="4f51b-115">tutorial de Olá demonstra Olá cenário de difusão simples utilizando Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="4f51b-115">hello tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f51b-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4f51b-116">Prerequisites</span></span>
<span data-ttu-id="4f51b-117">Este tutorial requer o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="4f51b-117">This tutorial requires hello following:</span></span>

* <span data-ttu-id="4f51b-118">[Visual Studio 2012 Express para Windows Phone] ou uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="4f51b-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="4f51b-119">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais de Notification Hubs para aplicações Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="4f51b-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="4f51b-120">Criar o Notification Hub</span><span class="sxs-lookup"><span data-stu-id="4f51b-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="4f51b-121">Clique em Olá <b>serviços de notificação</b> secção (dentro <i>definições</i>), clique em <b>Windows Phone (MPNS)</b> e, em seguida, clique em Olá <b>ativar push não autenticado </b> caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="4f51b-121">Click hello <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click hello <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Portal do Azure – Ativar notificações push não autenticadas](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="4f51b-123">O hub está agora criado e configurado toosend não autenticado de notificação para o Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="4f51b-123">Your hub is now created and configured toosend unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="4f51b-124">Este tutorial utiliza MPNS no modo não autenticado.</span><span class="sxs-lookup"><span data-stu-id="4f51b-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="4f51b-125">O modo MPNS não autenticado vem com restrições sobre as notificações que pode enviar tooeach canal.</span><span class="sxs-lookup"><span data-stu-id="4f51b-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send tooeach channel.</span></span> <span data-ttu-id="4f51b-126">Os Notification Hubs suportam [modo MPNS autenticado](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) , permitindo-lhe tooupload o certificado.</span><span class="sxs-lookup"><span data-stu-id="4f51b-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you tooupload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a><span data-ttu-id="4f51b-127">Ligar o seu hub de notificação de toohello de aplicação</span><span class="sxs-lookup"><span data-stu-id="4f51b-127">Connecting your app toohello notification hub</span></span>
1. <span data-ttu-id="4f51b-128">No Visual Studio, crie uma nova aplicação do Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="4f51b-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="4f51b-129">No Visual Studio 2013 Update 2 ou posterior crie, em vez disso, uma aplicação Silverlight do Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="4f51b-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio – Novo Projeto – Aplicação em Branco – Windows Phone Silverlight][11]
2. <span data-ttu-id="4f51b-131">No Visual Studio, faça duplo clique solução Olá e, em seguida, clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4f51b-131">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="4f51b-132">Esta ação apresenta Olá **gerir pacotes NuGet** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f51b-132">This displays hello **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="4f51b-133">Procurar `WindowsAzure.Messaging.Managed` e clique em **instalar**e, em seguida, aceite os termos de Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="4f51b-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept hello terms of use.</span></span>
   
    ![Visual Studio – Gestor de Pacotes NuGet][20]
   
    <span data-ttu-id="4f51b-135">Isto transfere, instala e adiciona uma biblioteca de mensagens do Azure de toohello de referência para o Windows utilizando o Olá <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacote NuGet Windowsazure</a>.</span><span class="sxs-lookup"><span data-stu-id="4f51b-135">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="4f51b-136">Abra o ficheiro de Olá App.xaml.cs e adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="4f51b-136">Open hello file App.xaml.cs and add hello following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="4f51b-137">Adicionar Olá seguinte código na parte superior de Olá de **Application_Launching** método em App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="4f51b-137">Add hello following code at hello top of **Application_Launching** method in App.xaml.cs:</span></span>
   
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
   > <span data-ttu-id="4f51b-138">Olá valor **MyPushChannel** é um índice que é utilizado toolookup um canal existente na Olá [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) coleção.</span><span class="sxs-lookup"><span data-stu-id="4f51b-138">hello value **MyPushChannel** is an index that is used toolookup an existing channel in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="4f51b-139">Se não existir, crie uma nova entrada com esse nome.</span><span class="sxs-lookup"><span data-stu-id="4f51b-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="4f51b-140">Certifique-se tooinsert Olá nome da cadeia de ligação do hub e Olá chamado **DefaultListenSharedAccessSignature** que obteve na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="4f51b-140">Make sure tooinsert hello name of your hub and hello connection string called **DefaultListenSharedAccessSignature** that you obtained in hello previous section.</span></span>
    <span data-ttu-id="4f51b-141">Este código obtém Olá URI do canal para aplicação Olá do MPNS e, em seguida, regista esse URI de canal no notification hub.</span><span class="sxs-lookup"><span data-stu-id="4f51b-141">This code retrieves hello channel URI for hello app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="4f51b-142">Esta ação garante também que Olá URI do canal que é registado no notification hub que é iniciada a cada aplicação Olá do tempo.</span><span class="sxs-lookup"><span data-stu-id="4f51b-142">It also guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4f51b-143">Este tutorial envia um dispositivo de toohello de notificação de alerta.</span><span class="sxs-lookup"><span data-stu-id="4f51b-143">This tutorial sends a toast notification toohello device.</span></span> <span data-ttu-id="4f51b-144">Enviar uma notificação de mosaico, em vez disso, tem de chamar Olá **BindToShellTile** método no canal Olá.</span><span class="sxs-lookup"><span data-stu-id="4f51b-144">When you send a tile notification, you must instead call hello **BindToShellTile** method on hello channel.</span></span> <span data-ttu-id="4f51b-145">toosupport notificações de alerta e o mosaico, chame **BindToShellTile** e **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="4f51b-145">toosupport both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="4f51b-146">No Explorador de soluções, expanda **propriedades**, abra Olá `WMAppManifest.xml` de ficheiros, clique em Olá **capacidades** separador e certifique-se de que Olá **ID_CAP_PUSH_NOTIFICATION** está selecionada.</span><span class="sxs-lookup"><span data-stu-id="4f51b-146">In Solution Explorer, expand **Properties**, open hello `WMAppManifest.xml` file, click hello **Capabilities** tab, and make sure that hello **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. <span data-ttu-id="4f51b-147">Olá prima `F5` toorun chave Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="4f51b-147">Press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="4f51b-148">É apresentada uma mensagem de registo na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="4f51b-148">A registration message is displayed in hello app.</span></span>
8. <span data-ttu-id="4f51b-149">Aplicação Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="4f51b-149">Close hello app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="4f51b-150">tooreceive uma alerta de notificação push, aplicação Olá deve não estar em execução em primeiro plano do Olá.</span><span class="sxs-lookup"><span data-stu-id="4f51b-150">tooreceive a toast push notification, hello application must not be running in hello foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="4f51b-151">Enviar notificações push a partir do back-end</span><span class="sxs-lookup"><span data-stu-id="4f51b-151">Send push notifications from your backend</span></span>
<span data-ttu-id="4f51b-152">Pode enviar notificações push com os Notification Hubs de qualquer back-end através de public Olá <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span><span class="sxs-lookup"><span data-stu-id="4f51b-152">You can send push notifications by using Notification Hubs from any backend via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="4f51b-153">Neste tutorial, enviará notificações push utilizando uma aplicação .NET de consola.</span><span class="sxs-lookup"><span data-stu-id="4f51b-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="4f51b-154">Para obter um exemplo de como toosend notificações push de um back-end de ASP.NET WebAPI que esteja integrado com Notification Hubs, consulte [Azure Notification Hubs notificam os utilizadores com back-end .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="4f51b-154">For an example of how toosend push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="4f51b-155">Para obter um exemplo de como notificações de push toosend utilizando Olá [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), veja [como toouse Notification Hubs de Java](notification-hubs-java-push-notification-tutorial.md) e [como toouse Notification Hubs de PHP](notification-hubs-php-push-notification-tutorial.md) .</span><span class="sxs-lookup"><span data-stu-id="4f51b-155">For an example of how toosend push notifications by using hello [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="4f51b-156">Solução Olá de contexto, selecione **adicionar** e **novo projeto...** e, em **Visual c#**, clique em **Windows** e **aplicação de consola**e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f51b-156">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="4f51b-157">Esta ação adiciona uma nova Visual c# consola toohello solução de aplicação.</span><span class="sxs-lookup"><span data-stu-id="4f51b-157">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="4f51b-158">Também pode fazer isto numa solução separada.</span><span class="sxs-lookup"><span data-stu-id="4f51b-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="4f51b-159">Clique em **Ferramentas**, clique em **Gestor de Pacotes de Biblioteca** e, em seguida, em **Consola do Gestor de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="4f51b-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="4f51b-160">Esta ação apresenta Olá consola do Gestor de pacotes.</span><span class="sxs-lookup"><span data-stu-id="4f51b-160">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="4f51b-161">No Olá **consola do Gestor de pacotes** janela, conjunto Olá **projeto predefinido** tooyour novo projeto de aplicação de consola e, em seguida, na janela de consola Olá, executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4f51b-161">In hello **Package Manager Console** window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="4f51b-162">Esta ação adiciona uma referência toohello SDK dos Notification Hubs do Azure utilizando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet do Microsoft Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="4f51b-162">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="4f51b-163">Abra Olá `Program.cs` de ficheiros e adicione o seguinte Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="4f51b-163">Open hello `Program.cs` file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="4f51b-164">No Olá `Program` classe, adicione Olá método os seguintes:</span><span class="sxs-lookup"><span data-stu-id="4f51b-164">In hello `Program` class, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="4f51b-165">Certifique-se de que tooreplace Olá `<hub name>` marcador de posição com nome Olá Olá notification hub que aparece no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="4f51b-165">Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello portal.</span></span> <span data-ttu-id="4f51b-166">Além disso, substitua o marcador de posição de cadeia de ligação de Olá pela cadeia de ligação de Olá chamada **DefaultFullSharedAccessSignature** que obteve na secção de Olá "Configurar o notification hub".</span><span class="sxs-lookup"><span data-stu-id="4f51b-166">Also, replace hello connection string placeholder with hello connection string called **DefaultFullSharedAccessSignature** that you obtained in hello section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4f51b-167">Certifique-se de que utiliza a cadeia de ligação de Olá com **completa** e não com acesso **escutar** acesso.</span><span class="sxs-lookup"><span data-stu-id="4f51b-167">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="4f51b-168">cadeia de ligação de acesso escuta Olá não tem as notificações de push de toosend permissões.</span><span class="sxs-lookup"><span data-stu-id="4f51b-168">hello listen-access string does not have permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="4f51b-169">Adicionar Olá seguinte linha no seu `Main` método:</span><span class="sxs-lookup"><span data-stu-id="4f51b-169">Add hello following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="4f51b-170">Com o seu Windows Phone emulador em execução e o projeto de aplicação de consola do aplicação Olá fechada, defina como Olá predefinido projeto de arranque e, em seguida, prima Olá `F5` toorun chave Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="4f51b-170">With your Windows Phone emulator running and your app closed, set hello console application project as hello default startup project, and then press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="4f51b-171">Receberá um alerta de notificação push.</span><span class="sxs-lookup"><span data-stu-id="4f51b-171">You will receive a toast push notification.</span></span> <span data-ttu-id="4f51b-172">Tocar Olá faixa do alerta carrega a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="4f51b-172">Tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="4f51b-173">Pode encontrar todos os payloads possíveis de Olá no Olá [catálogo de alertas] e [catálogo de mosaicos] tópicos no MSDN.</span><span class="sxs-lookup"><span data-stu-id="4f51b-173">You can find all hello possible payloads in hello [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f51b-174">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4f51b-174">Next steps</span></span>
<span data-ttu-id="4f51b-175">Neste exemplo simples, difundiu tooall de notificações push os seus dispositivos Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="4f51b-175">In this simple example, you broadcasted push notifications tooall your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="4f51b-176">Na ordem tootarget utilizadores específicos, consulte toohello [utilizar Notification Hubs toopush notificações toousers] tutorial.</span><span class="sxs-lookup"><span data-stu-id="4f51b-176">In order tootarget specific users, refer toohello [Use Notification Hubs toopush notifications toousers] tutorial.</span></span> 

<span data-ttu-id="4f51b-177">Se pretender que toosegment os seus utilizadores por grupos de interesse, pode ler [toosend utilizar Notification Hubs notícias de última hora].</span><span class="sxs-lookup"><span data-stu-id="4f51b-177">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="4f51b-178">Saiba mais sobre como os Hubs de notificação de toouse em [documentação de orientação dos Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="4f51b-178">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance].</span></span>

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

