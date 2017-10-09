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
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="5c553-104">Enviar notificações push com Notification Hubs do Azure e o Node.js</span><span class="sxs-lookup"><span data-stu-id="5c553-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="5c553-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="5c553-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5c553-106">toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5c553-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="5c553-107">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5c553-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5c553-108">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="5c553-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="5c553-109">Este guia irá mostrar como toosend notificações push com a ajuda de Olá dos Notification Hubs do Azure diretamente a partir de uma aplicação Node.js.</span><span class="sxs-lookup"><span data-stu-id="5c553-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="5c553-110">cenários de Olá abrangidos incluem a enviar tooapplications de notificações push no Olá seguintes plataformas:</span><span class="sxs-lookup"><span data-stu-id="5c553-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="5c553-111">Android</span><span class="sxs-lookup"><span data-stu-id="5c553-111">Android</span></span>
* <span data-ttu-id="5c553-112">iOS</span><span class="sxs-lookup"><span data-stu-id="5c553-112">iOS</span></span>
* <span data-ttu-id="5c553-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="5c553-113">Windows Phone</span></span>
* <span data-ttu-id="5c553-114">Plataforma universal do Windows</span><span class="sxs-lookup"><span data-stu-id="5c553-114">Universal Windows Platform</span></span> 

<span data-ttu-id="5c553-115">Para obter mais informações sobre os notification hubs, consulte Olá [passos](#next) secção.</span><span class="sxs-lookup"><span data-stu-id="5c553-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="5c553-116">O que são os Hubs de Notificação?</span><span class="sxs-lookup"><span data-stu-id="5c553-116">What are Notification Hubs?</span></span>
<span data-ttu-id="5c553-117">Os Hubs de notificação do Azure fornecem uma infraestrutura de fácil utilização, várias plataforma, dimensionável para envio de dispositivos de toomobile de notificações push.</span><span class="sxs-lookup"><span data-stu-id="5c553-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="5c553-118">Para obter detalhes sobre a infraestrutura de serviço Olá, consulte Olá [Notification Hubs do Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="5c553-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="5c553-119">Criar uma aplicação Node.js</span><span class="sxs-lookup"><span data-stu-id="5c553-119">Create a Node.js Application</span></span>
<span data-ttu-id="5c553-120">Olá primeiro passo para este tutorial está a criar uma nova aplicação Node.js em branco.</span><span class="sxs-lookup"><span data-stu-id="5c553-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="5c553-121">Para obter instruções sobre como criar uma aplicação Node.js, consulte [criar e implementar uma tooAzure de aplicação Node.js do Web Site][nodejswebsite], [serviço em nuvem de Node.js] [ Node.js Cloud Service] através do Windows PowerShell, ou [Web Site com o WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="5c553-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="5c553-122">Configurar a sua aplicação tooUse Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="5c553-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="5c553-123">toouse Notification Hubs do Azure, terá de toodownload e utilize Olá Node.js [pacote do azure](https://www.npmjs.com/package/azure), que inclui um conjunto de bibliotecas de programa auxiliar que comunicam com os serviços de REST de notificação de push Olá incorporado.</span><span class="sxs-lookup"><span data-stu-id="5c553-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="5c553-124">Utilizar o Gestor de pacote de nó (NPM) tooobtain Olá pacote</span><span class="sxs-lookup"><span data-stu-id="5c553-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="5c553-125">Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Linux) e navegue pasta toohello onde criou a aplicação em branco .</span><span class="sxs-lookup"><span data-stu-id="5c553-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="5c553-126">Tipo **npm instalar azure sb** na janela de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="5c553-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="5c553-127">Pode executar manualmente Olá **ls** ou **dir** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="5c553-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="5c553-128">Dentro dessa pasta, determinar Olá **azure** pacote, que contém as bibliotecas de Olá terá tooaccess Olá Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="5c553-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="5c553-129">Pode saber mais sobre a instalação de NPM no oficial Olá [NPM blogue](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="5c553-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="5c553-130">Módulo Olá de importação</span><span class="sxs-lookup"><span data-stu-id="5c553-130">Import hello module</span></span>
<span data-ttu-id="5c553-131">Com um editor de texto, adicionar Olá seguir toohello superior de Olá **server.js** ficheiro da aplicação Olá:</span><span class="sxs-lookup"><span data-stu-id="5c553-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="5c553-132">Configurar uma ligação do Hub de notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="5c553-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="5c553-133">Olá **NotificationHubService** objeto permite-lhe trabalhar com os notification hubs.</span><span class="sxs-lookup"><span data-stu-id="5c553-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="5c553-134">Olá código seguinte cria um **NotificationHubService** objeto para o hub de nofication Olá denominado **hubname**.</span><span class="sxs-lookup"><span data-stu-id="5c553-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="5c553-135">Adicionar perto Olá parte superior do Olá **server.js** ficheiro, após o módulo do Olá instrução tooimport Olá do azure:</span><span class="sxs-lookup"><span data-stu-id="5c553-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="5c553-136">Olá ligação **connectionstring** Olá pode obter o valor [Portal do Azure] efetuando Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5c553-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="5c553-137">No painel de navegação esquerdo Olá, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="5c553-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="5c553-138">Selecione **Notification Hubs**e, em seguida, o hub de Olá localizar desejar toouse para exemplo Olá.</span><span class="sxs-lookup"><span data-stu-id="5c553-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="5c553-139">Pode consultar toohello [Windows Store introdução tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) se precisar de ajuda para criar um novo Hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="5c553-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="5c553-140">Selecione **definições**.</span><span class="sxs-lookup"><span data-stu-id="5c553-140">Select **Settings**.</span></span>
4. <span data-ttu-id="5c553-141">Clique em **políticas de acesso**.</span><span class="sxs-lookup"><span data-stu-id="5c553-141">Click on **Access Policies**.</span></span> <span data-ttu-id="5c553-142">Verá ambas as cadeias de ligação de acesso partilhado e completa.</span><span class="sxs-lookup"><span data-stu-id="5c553-142">You will see both shared and full access connection strings.</span></span>

![Portal do Azure – os Hubs de notificação](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="5c553-144">Também pode obter a cadeia de ligação de Olá utilizando Olá **Get-AzureSbNamespace** cmdlet fornecida pelo [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou Olá **mostrar de espaço de nomes do azure sb** comando com Olá [Interface de linha de comandos do Azure (CLI do Azure)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5c553-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="5c553-145">Arquitetura geral</span><span class="sxs-lookup"><span data-stu-id="5c553-145">General architecture</span></span>
<span data-ttu-id="5c553-146">Olá **NotificationHubService** objeto expõe Olá seguintes instâncias de objeto para envio de dispositivos de toospecific de notificações push e de aplicações:</span><span class="sxs-lookup"><span data-stu-id="5c553-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="5c553-147">**Android** -utilizar Olá **GcmService** objeto que está disponível em **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="5c553-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="5c553-148">**iOS** -utilizar Olá **ApnsService** objeto que está acessível na **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="5c553-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="5c553-149">**Windows Phone** -utilizar Olá **MpnsService** objeto que está disponível em **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="5c553-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="5c553-150">**Plataforma universal do Windows** -utilizar Olá **WnsService** objeto que está disponível em **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="5c553-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="5c553-151">Como: enviar aplicações tooAndroid de notificações de push</span><span class="sxs-lookup"><span data-stu-id="5c553-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="5c553-152">Olá **GcmService** objeto fornece um **enviar** método que pode ser utilizado toosend push notificações tooAndroid aplicações.</span><span class="sxs-lookup"><span data-stu-id="5c553-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="5c553-153">Olá **enviar** método aceita Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5c553-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="5c553-154">**Etiquetas** -Olá identificador da etiqueta.</span><span class="sxs-lookup"><span data-stu-id="5c553-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="5c553-155">Se não for fornecido nenhum tag, Olá notificação será enviada tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="5c553-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="5c553-156">**Payload** -Olá JSON ou payload de cadeia não processados da mensagem.</span><span class="sxs-lookup"><span data-stu-id="5c553-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="5c553-157">**Chamada de retorno** -Olá a função de chamada de retorno.</span><span class="sxs-lookup"><span data-stu-id="5c553-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="5c553-158">Para obter mais informações sobre o formato de payload Olá, consulte Olá **Payload** secção Olá [implementar o servidor do GCM](http://developer.android.com/google/gcm/server.html#payload) documento.</span><span class="sxs-lookup"><span data-stu-id="5c553-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="5c553-159">Olá código seguinte utiliza Olá **GcmService** instância exposta pelo Olá **NotificationHubService** toosend um tooall de notificação push registado clientes.</span><span class="sxs-lookup"><span data-stu-id="5c553-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

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

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="5c553-160">Como: enviar aplicações tooiOS de notificações de push</span><span class="sxs-lookup"><span data-stu-id="5c553-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="5c553-161">Mesmo tal como acontece com as aplicações Android descrita acima, Olá **ApnsService** objeto fornece um **enviar** método que pode ser utilizado toosend push notificações tooiOS aplicações.</span><span class="sxs-lookup"><span data-stu-id="5c553-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="5c553-162">Olá **enviar** método aceita Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5c553-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="5c553-163">**Etiquetas** -Olá identificador da etiqueta.</span><span class="sxs-lookup"><span data-stu-id="5c553-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="5c553-164">Se não for fornecido nenhum tag, Olá notificação será enviada tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="5c553-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="5c553-165">**Payload** - Olá JSON da mensagem ou payload de cadeia.</span><span class="sxs-lookup"><span data-stu-id="5c553-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="5c553-166">**Chamada de retorno** -Olá a função de chamada de retorno.</span><span class="sxs-lookup"><span data-stu-id="5c553-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="5c553-167">Para o formato de payload de Olá de mais informações, consulte Olá **notificação Payload** secção Olá [guia de programação de notificações de Push e Local](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) documento.</span><span class="sxs-lookup"><span data-stu-id="5c553-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="5c553-168">Olá código seguinte utiliza Olá **ApnsService** instância exposta pelo Olá **NotificationHubService** toosend um alerta mensagem tooall clientes:</span><span class="sxs-lookup"><span data-stu-id="5c553-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="5c553-169">Como: enviar aplicações de Phone tooWindows notificações de push</span><span class="sxs-lookup"><span data-stu-id="5c553-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="5c553-170">Olá **MpnsService** objeto fornece um **enviar** método que pode ser utilizado toosend push notificações tooWindows aplicações Phone.</span><span class="sxs-lookup"><span data-stu-id="5c553-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="5c553-171">Olá **enviar** método aceita Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5c553-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="5c553-172">**Etiquetas** -Olá identificador da etiqueta.</span><span class="sxs-lookup"><span data-stu-id="5c553-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="5c553-173">Se não for fornecido nenhum tag, Olá notificação será enviada tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="5c553-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="5c553-174">**Payload** -Olá payload XML da mensagem.</span><span class="sxs-lookup"><span data-stu-id="5c553-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="5c553-175">**TargetName**  -  `toast` para notificações de alerta.</span><span class="sxs-lookup"><span data-stu-id="5c553-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="5c553-176">`token`Para obter notificações do mosaico.</span><span class="sxs-lookup"><span data-stu-id="5c553-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="5c553-177">**NotificationClass** -Olá prioridade de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c553-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="5c553-178">Consulte Olá **elementos de cabeçalho de HTTP** secção Olá [notificações Push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx) documento para os valores válidos.</span><span class="sxs-lookup"><span data-stu-id="5c553-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="5c553-179">**Opções de** - opcional cabeçalhos de pedido.</span><span class="sxs-lookup"><span data-stu-id="5c553-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="5c553-180">**Chamada de retorno** -Olá a função de chamada de retorno.</span><span class="sxs-lookup"><span data-stu-id="5c553-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="5c553-181">Para obter uma lista válida de **TargetName**, **NotificationClass** e opções de cabeçalho, veja Olá [notificações Push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="5c553-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="5c553-182">Olá, código de exemplo a seguir utiliza Olá **MpnsService** instância exposta pelo Olá **NotificationHubService** toosend uma notificação push de alerta:</span><span class="sxs-lookup"><span data-stu-id="5c553-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="5c553-183">Como: enviar aplicações de plataforma do Windows (UWP) de tooUniversal notificações de push</span><span class="sxs-lookup"><span data-stu-id="5c553-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="5c553-184">Olá **WnsService** objeto fornece um **enviar** método que pode ser utilizado toosend push notificações tooUniversal plataforma Windows aplicações.</span><span class="sxs-lookup"><span data-stu-id="5c553-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="5c553-185">Olá **enviar** método aceita Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5c553-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="5c553-186">**Etiquetas** -Olá identificador da etiqueta.</span><span class="sxs-lookup"><span data-stu-id="5c553-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="5c553-187">Se não for fornecido nenhum tag, Olá notificação será enviada clientes tooall registado.</span><span class="sxs-lookup"><span data-stu-id="5c553-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="5c553-188">**Payload** -payload da mensagem Olá XML.</span><span class="sxs-lookup"><span data-stu-id="5c553-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="5c553-189">**Tipo** -Olá o tipo de notificação.</span><span class="sxs-lookup"><span data-stu-id="5c553-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="5c553-190">**Opções de** - opcional cabeçalhos de pedido.</span><span class="sxs-lookup"><span data-stu-id="5c553-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="5c553-191">**Chamada de retorno** -Olá a função de chamada de retorno.</span><span class="sxs-lookup"><span data-stu-id="5c553-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="5c553-192">Para obter uma lista de tipos válidos e cabeçalhos de pedido, consulte [Push cabeçalhos de pedido e resposta do serviço de notificação](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c553-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="5c553-193">Olá código seguinte utiliza Olá **WnsService** instância exposta pelo Olá **NotificationHubService** toosend uma aplicação UWP tooa de notificação de push de alerta:</span><span class="sxs-lookup"><span data-stu-id="5c553-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="5c553-194">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="5c553-194">Next Steps</span></span>
<span data-ttu-id="5c553-195">fragmentos de exemplo de Olá acima permitem tooeasily compilação serviço infraestrutura toodeliver push notificações tooa ampla variedade de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5c553-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="5c553-196">Agora que aprendeu as noções básicas de Olá de utilizar os Notification Hubs com o node.js, siga estas toolearn ligações mais informações sobre como pode expandir ainda mais estas capacidades.</span><span class="sxs-lookup"><span data-stu-id="5c553-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="5c553-197">Consulte Olá referência do MSDN para [Notification Hubs do Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c553-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="5c553-198">Visite Olá [Azure SDK para o nó] repositório no GitHub para obter mais exemplos e detalhes de implementação.</span><span class="sxs-lookup"><span data-stu-id="5c553-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

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
