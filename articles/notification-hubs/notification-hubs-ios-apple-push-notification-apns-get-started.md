---
title: "aaaSending tooiOS de notificações push com Notification Hubs do Azure | Microsoft Docs"
description: "Neste tutorial, saiba como toouse Notification Hubs do Azure toosend push aplicações de iOS tooan de notificações."
services: notification-hubs
documentationcenter: ios
keywords: "notificação push, notificações push, notificações push do ios"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="d390a-104">Enviar tooiOS de notificações push com Notification Hubs do Azure</span><span class="sxs-lookup"><span data-stu-id="d390a-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="d390a-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="d390a-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="d390a-106">toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d390a-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d390a-107">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d390a-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d390a-108">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="d390a-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="d390a-109">Este tutorial mostra como toouse Notification Hubs do Azure toosend push aplicações de iOS tooan de notificações.</span><span class="sxs-lookup"><span data-stu-id="d390a-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="d390a-110">Irá criar uma aplicação iOS em branco que recebe notificações push utilizando Olá [serviço Apple Push Notification (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="d390a-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="d390a-111">Quando tiver terminado, será capaz de toouse sua toobroadcast de hub de notificação push dispositivos Olá tooall de notificações executar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d390a-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d390a-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d390a-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="d390a-113">código de Olá concluída para este tutorial pode ser encontrado [no GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="d390a-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d390a-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d390a-114">Prerequisites</span></span>
<span data-ttu-id="d390a-115">Este tutorial requer o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="d390a-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="d390a-116">[iOS dos Mobile Services versão 1.2.4 do SDK]</span><span class="sxs-lookup"><span data-stu-id="d390a-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="d390a-117">Versão mais recente do [Xcode].</span><span class="sxs-lookup"><span data-stu-id="d390a-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="d390a-118">Um dispositivo compatível com iOS 8 (ou versão posterior)</span><span class="sxs-lookup"><span data-stu-id="d390a-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="d390a-119">Associação ao [Programa de Programador da Apple](https://developer.apple.com/programs/)</span><span class="sxs-lookup"><span data-stu-id="d390a-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d390a-120">Devido aos requisitos de configuração para notificações push, tem de implementar e testar as notificações de push num dispositivo iOS físico (iPhone ou iPad) em vez do simulador de iOS Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="d390a-121">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais dos Notification Hubs para aplicações iOS.</span><span class="sxs-lookup"><span data-stu-id="d390a-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="d390a-122">Configurar o Notification Hub para notificações push do iOS</span><span class="sxs-lookup"><span data-stu-id="d390a-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="d390a-123">Esta secção explica-lhe como criar um novo notification hub e configurar a autenticação com APNS utilizando Olá **. p12** certificado push que criou.</span><span class="sxs-lookup"><span data-stu-id="d390a-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="d390a-124">Se quiser toouse um notification hub que já tenha criado, pode ignorar toostep 5.</span><span class="sxs-lookup"><span data-stu-id="d390a-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="d390a-125">Clique em Olá <b>serviços de notificação</b> botão no Olá <b>definições</b> painel, em seguida, selecione <b>Apple (APNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="d390a-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="d390a-126">Clique em <b>carregar certificado</b> e selecione Olá <b>. p12</b> ficheiro que exportou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d390a-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="d390a-127">Certifique-se que também de especificar palavra-passe correta Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="d390a-128">Certifique-se de que tooselect <b>Sandbox</b> modo, uma vez que se destina ao desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="d390a-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="d390a-129">Utilize apenas Olá <b>produção</b> se quiser toousers de notificações de push toosend que já tenham adquirido a aplicação da loja de Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="d390a-130">&emsp;&emsp;&emsp;&emsp;![Configurar o APNS no Portal do Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="d390a-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configurar certificação APNS no Portal do Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="d390a-132">O notification hub está agora configurado toowork com APNS e ter tooregister de cadeias de ligação de Olá a aplicação e enviar notificações push.</span><span class="sxs-lookup"><span data-stu-id="d390a-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="d390a-133">Ligar o seu tooNotification de aplicação iOS Hubs</span><span class="sxs-lookup"><span data-stu-id="d390a-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="d390a-134">No Xcode, crie um novo projeto do iOS e selecione Olá **aplicação de vista única** modelo.</span><span class="sxs-lookup"><span data-stu-id="d390a-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode – Aplicação de Vista Única][8]
    
2. <span data-ttu-id="d390a-136">Quando definir opções de Olá para o novo projeto, certifique-se toouse Olá mesmo **nome de produto** e **identificador de organização** que utilizou quando definiu anteriormente o ID de pacote Olá no Olá programador da Apple Portal.</span><span class="sxs-lookup"><span data-stu-id="d390a-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode – opções do projeto][11]
    
3. <span data-ttu-id="d390a-138">Em **destinos**, clique no nome do projeto, clique em Olá **definições de criação** separador e expanda **a identidade de assinatura de código**e, em **depurar**, defina a identidade de assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="d390a-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="d390a-139">Ativar/desativar **níveis** de **básico** demasiado**todos os**e definir **perfil de aprovisionamento** toohello perfil que criou anteriormente de aprovisionamento .</span><span class="sxs-lookup"><span data-stu-id="d390a-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="d390a-140">Se não vir Olá aprovisionamento novo perfil que criou no Xcode, tente atualizar perfis Olá para a sua identidade de assinatura.</span><span class="sxs-lookup"><span data-stu-id="d390a-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="d390a-141">Clique em **Xcode** na barra de menus Olá, clique em **preferências**, clique em Olá **conta** separador, clique em Olá **ver detalhes** botão, clique em sua identidade de assinatura e, em seguida, clique no botão Atualizar Olá no canto inferior direito de Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode – perfil de aprovisionamento][9]
4. <span data-ttu-id="d390a-143">Transferir Olá [iOS dos Mobile Services versão 1.2.4 do SDK] e deszipe o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="d390a-144">No Xcode, clique no seu projeto e clique em Olá **adicionar ficheiros a** Olá tooadd de opção **Windowsazuremessaging** projeto do pasta tooyour Xcode.</span><span class="sxs-lookup"><span data-stu-id="d390a-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="d390a-145">Selecione **Copiar itens, se necessário** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d390a-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d390a-146">Olá SDK dos notification hubs não suporta atualmente bitcode no Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="d390a-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="d390a-147">Tem de definir **ativar Bitcode** demasiado**não** no Olá **criar opções** para o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="d390a-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Deszipar o Azure SDK][10]
5. <span data-ttu-id="d390a-149">Adicionar um novo cabeçalho ficheiro tooyour projeto com o nome `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="d390a-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="d390a-150">Este ficheiro vai deter as constantes de Olá para o seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="d390a-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="d390a-151">Adicione Olá seguintes definições e substitua Olá cadeia literal marcadores de posição pelo seu *nome do hub* e Olá *DefaultListenSharedAccessSignature* que anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d390a-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="d390a-152">Abra o `AppDelegate.h` ficheiro adicionar Olá seguir diretivas de importação:</span><span class="sxs-lookup"><span data-stu-id="d390a-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="d390a-153">No seu `AppDelegate.m file`, adicionar Olá seguinte código no Olá `didFinishLaunchingWithOptions` método com base na sua versão do iOS.</span><span class="sxs-lookup"><span data-stu-id="d390a-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="d390a-154">Este código regista o seu identificador de dispositivo com APNs:</span><span class="sxs-lookup"><span data-stu-id="d390a-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="d390a-155">Para iOS 8:</span><span class="sxs-lookup"><span data-stu-id="d390a-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="d390a-156">Para versões do iOS too8 anterior:</span><span class="sxs-lookup"><span data-stu-id="d390a-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="d390a-157">No Olá mesmo ficheiro, adicione os seguintes métodos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="d390a-158">Este código liga-se o hub de notificação de toohello utilizando as informações da ligação Olá que especificou em Hubinfo.</span><span class="sxs-lookup"><span data-stu-id="d390a-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="d390a-159">Em seguida, atribui hub de notificação de token toohello de dispositivo Olá para que hello hub de notificação pode enviar notificações:</span><span class="sxs-lookup"><span data-stu-id="d390a-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="d390a-160">No Olá mesmo ficheiro, adicione Olá seguinte método toodisplay um **UIAlert** se notificação de Olá seja recebida enquanto a aplicação Olá está ativa:</span><span class="sxs-lookup"><span data-stu-id="d390a-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="d390a-161">Crie e execute a aplicação Olá no seu tooverify de dispositivo que não existem sem falhas.</span><span class="sxs-lookup"><span data-stu-id="d390a-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="d390a-162">Enviar notificações push de teste</span><span class="sxs-lookup"><span data-stu-id="d390a-162">Send test push notifications</span></span>
<span data-ttu-id="d390a-163">Pode testar a receção das notificações na sua aplicação através do envio de notificações push no Olá [Portal do Azure] através de Olá **resolução de problemas** secção no painel do hub de Olá (utilizar Olá *deenviodeteste* opção).</span><span class="sxs-lookup"><span data-stu-id="d390a-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Portal do Azure – Envio de Teste][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="d390a-165">(Opcional) Enviar notificações push da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="d390a-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d390a-166">Este exemplo de envio de notificações da aplicação de cliente Olá é fornecido para efeitos apenas de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="d390a-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="d390a-167">Uma vez que tal exige Olá `DefaultFullSharedAccessSignature` toobe presente na aplicação de cliente Olá, expõe o risco de toohello de hub de notificação de um utilizador obter acesso não autorizado de toosend notificações tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="d390a-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="d390a-168">Se quiser toosend notificações de push a partir de uma aplicação, esta secção fornece um exemplo de como toodo esta utilizando Olá REST interface.</span><span class="sxs-lookup"><span data-stu-id="d390a-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="d390a-169">No Xcode, abra `Main.storyboard` e adicione Olá seguintes componentes de IU de Olá objeto biblioteca tooallow Olá utilizador toosend notificações push na aplicação Olá:</span><span class="sxs-lookup"><span data-stu-id="d390a-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="d390a-170">Uma etiqueta sem texto da etiqueta.</span><span class="sxs-lookup"><span data-stu-id="d390a-170">A label with no label text.</span></span> <span data-ttu-id="d390a-171">Será utilizado tooreport erros no envio de notificações.</span><span class="sxs-lookup"><span data-stu-id="d390a-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="d390a-172">Olá **linhas** propriedade deve ser definida demasiado**0** , de modo a que será redimensionada automaticamente toohello restrita margens direita e esquerdas e Olá parte superior da vista de Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="d390a-173">Um campo de texto com **marcador de posição** texto definido demasiado**introduzir mensagem de notificação**.</span><span class="sxs-lookup"><span data-stu-id="d390a-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="d390a-174">Restrinja o campo de Olá imediatamente por baixo etiqueta Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d390a-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="d390a-175">Defina Olá controlador de vista como delegado da saída Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="d390a-176">Um botão intitulado **Enviar notificação** restringido imediatamente por baixo campo de texto Olá e no centro horizontal Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="d390a-177">Vista de Olá deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="d390a-177">hello view should look as follows:</span></span>
     
     ![Estruturador do Xcode][32]
2. <span data-ttu-id="d390a-179">[Adicione saídas](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) para campo de texto e a etiqueta de Olá ligados à sua vista e atualize a sua `interface` definição toosupport `UITextFieldDelegate` e `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="d390a-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="d390a-180">Adicione Olá três declarações de propriedades mostradas abaixo toohelp suporte chamar Olá REST API e ao analisar a resposta de Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="d390a-181">O ficheiro ViewController.h deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="d390a-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="d390a-182">Abra `HubInfo.h` e adicione Olá seguintes constantes, que serão utilizadas para enviar o hub de tooyour de notificações.</span><span class="sxs-lookup"><span data-stu-id="d390a-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="d390a-183">Substitua o literal de cadeia do marcador de posição Olá com real *DefaultFullSharedAccessSignature* cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="d390a-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="d390a-184">Adicione Olá seguinte `#import` instruções tooyour `ViewController.h` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="d390a-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="d390a-185">No `ViewController.m` adicionar Olá após a implementação de interface de toohello de código.</span><span class="sxs-lookup"><span data-stu-id="d390a-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="d390a-186">Este código analisará a cadeia de ligação *DefaultFullSharedAccessSignature*.</span><span class="sxs-lookup"><span data-stu-id="d390a-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="d390a-187">Tal como mencionado na Olá [referência da REST API](http://msdn.microsoft.com/library/azure/dn495627.aspx), estas informações analisadas serão utilizada toogenerate um token SaS para Olá **autorização** cabeçalho do pedido.</span><span class="sxs-lookup"><span data-stu-id="d390a-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="d390a-188">No `ViewController.m`, atualização Olá `viewDidLoad` cadeia de ligação de Olá do método tooparse quando carrega Olá vista.</span><span class="sxs-lookup"><span data-stu-id="d390a-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="d390a-189">Também adicionar métodos de utilitário Olá, abaixo, implementação de interface toohello.</span><span class="sxs-lookup"><span data-stu-id="d390a-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="d390a-190">No `ViewController.m`, adicionar Olá seguinte código toohello interface implementação toogenerate Olá SaS token de autorização que irá ser fornecido no Olá **autorização** cabeçalho, tal como mencionado na Olá [REST API Referência](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="d390a-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="d390a-191">Prima CTRL e arraste do Olá **Enviar notificação** botão demasiado`ViewController.m` tooadd uma ação com o nome **SendNotificationMessage** para Olá **Touch baixo** eventos.</span><span class="sxs-lookup"><span data-stu-id="d390a-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="d390a-192">Atualize o método com Olá seguir notificação Olá toosend de código utilizando Olá REST API.</span><span class="sxs-lookup"><span data-stu-id="d390a-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="d390a-193">No `ViewController.m`, adicionar Olá toosupport de método de delegado fecho Olá teclado para o campo de texto Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="d390a-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="d390a-194">Prima CTRL e arraste do Olá texto campo toohello controlador de vista ícone Olá de tooset estruturador de interface de Olá visualizar controlador como delegado da saída Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="d390a-195">No `ViewController.m`, adicione a seguinte Olá delegar a resposta de Olá análise toosupport métodos utilizando `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="d390a-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="d390a-196">Compilar o projeto de Olá e certifique-se de que não existirem erros.</span><span class="sxs-lookup"><span data-stu-id="d390a-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="d390a-197">Se ocorrer um erro de compilação no xcode7 relativo ao suporte de bitcode, deve alterar Olá **definições de criação** > **ativar Bitcode (ENABLE_BITCODE)** demasiado**não** no Xcode.</span><span class="sxs-lookup"><span data-stu-id="d390a-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="d390a-198">Olá SDK dos Notification Hubs não suporta atualmente bitcode.</span><span class="sxs-lookup"><span data-stu-id="d390a-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="d390a-199">Pode encontrar todos os Olá payloads possíveis no Olá Apple [guia de programação de notificações de Push e Local].</span><span class="sxs-lookup"><span data-stu-id="d390a-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="d390a-200">Verificar se a aplicação pode receber notificações push</span><span class="sxs-lookup"><span data-stu-id="d390a-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="d390a-201">tootest as notificações push no iOS, tem de implementar o dispositivo iOS físico do Olá aplicação tooa.</span><span class="sxs-lookup"><span data-stu-id="d390a-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="d390a-202">Não é possível enviar notificações push da Apple utilizando o simulador de iOS Olá.</span><span class="sxs-lookup"><span data-stu-id="d390a-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="d390a-203">Execute a aplicação Olá, verifique se o registo é concluída com êxito e, em seguida, prima **OK**.</span><span class="sxs-lookup"><span data-stu-id="d390a-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Teste do Registo de Notificações Push da Aplicação iOS][33]
2. <span data-ttu-id="d390a-205">Pode enviar uma notificação push de teste de Olá [Portal do Azure], conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="d390a-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="d390a-206">Se tiver adicionado o código para enviar notificações push na aplicação Olá, toque no dentro tooenter de campo de texto Olá uma mensagem de notificação.</span><span class="sxs-lookup"><span data-stu-id="d390a-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="d390a-207">Em seguida, prima Olá **enviar** botão no teclado Olá ou Olá **Enviar notificação** botão na mensagem de notificação de saudação do Olá vista toosend.</span><span class="sxs-lookup"><span data-stu-id="d390a-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![Teste de Envio de Notificações Push da Aplicação iOS][34]
3. <span data-ttu-id="d390a-209">Olá notificação push é enviada tooall dispositivos registado tooreceive notificações Olá de Olá Notification Hub específico.</span><span class="sxs-lookup"><span data-stu-id="d390a-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![Teste de Receção de Notificações Push da Aplicação iOS][35]

## <a name="next-steps"></a><span data-ttu-id="d390a-211">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d390a-211">Next steps</span></span>
<span data-ttu-id="d390a-212">Neste exemplo simples, difundiu tooall de notificações push dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="d390a-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="d390a-213">Sugerimos como passo seguinte na sua aprendizagem que passe toohello [Azure Notification Hubs notificam utilizadores do iOS com back-end .NET] tutorial, o que irá guiá-lo a criar um push toosend de back-end notificações utilizando etiquetas.</span><span class="sxs-lookup"><span data-stu-id="d390a-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="d390a-214">Se quiser toosegment os seus utilizadores por grupos de interesse, pode, adicionalmente no toohello [toosend utilizar Notification Hubs notícias de última hora] tutorial.</span><span class="sxs-lookup"><span data-stu-id="d390a-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="d390a-215">Para obter informações gerais sobre os Notification Hubs, consulte a nossa [Documentação de Orientação dos Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="d390a-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[iOS dos Mobile Services versão 1.2.4 do SDK]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Documentação de Orientação dos Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs notificam utilizadores do iOS com back-end .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend utilizar Notification Hubs notícias de última hora]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[guia de programação de notificações de Push e Local]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Portal do Azure]: https://portal.azure.com
