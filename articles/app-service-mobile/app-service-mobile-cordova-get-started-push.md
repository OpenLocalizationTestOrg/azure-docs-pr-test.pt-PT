---
title: "aaaAdd notificações Push tooApache aplicação Cordova com Mobile Apps do Azure | Microsoft Docs"
description: "Saiba como toouse Mobile Apps do Azure toosend push notificações tooyour Apache Cordova aplicação."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="79554-103">Adicionar a aplicação de Apache Cordova de tooyour de notificações push</span><span class="sxs-lookup"><span data-stu-id="79554-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="79554-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="79554-104">Overview</span></span>
<span data-ttu-id="79554-105">Neste tutorial, adicione projeto de toohello [início rápido do Apache Cordova] de notificações push para que uma notificação push é enviada toohello dispositivo sempre que é inserido um registo.</span><span class="sxs-lookup"><span data-stu-id="79554-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="79554-106">Se não utilizar Olá transferir o projeto de servidor de início rápido, precisa de Olá o pacote de extensão de notificação push.</span><span class="sxs-lookup"><span data-stu-id="79554-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="79554-107">Para obter mais informações, consulte [trabalhar com o servidor de back-end de .NET Olá SDK de Mobile Apps do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="79554-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="79554-108"><a name="prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="79554-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="79554-109">Este tutorial abrange uma aplicação Apache Cordova desenvolvida com o Visual Studio 2015, que é executado no Olá emulador do Google Android, um dispositivo Android, um dispositivo Windows e um dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="79554-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="79554-110">toocomplete neste tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="79554-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="79554-111">Um PC com [Visual Studio Community 2015] [ 2] ou versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="79554-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="79554-112">[Visual Studio Tools para Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="79554-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="79554-113">Um [conta ativa do Azure][3].</span><span class="sxs-lookup"><span data-stu-id="79554-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="79554-114">Uma conclusão [início rápido do Apache Cordova] [ 5] projeto.</span><span class="sxs-lookup"><span data-stu-id="79554-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="79554-115">(Android) A [conta Google] [ 6] com um endereço de correio eletrónico verificado.</span><span class="sxs-lookup"><span data-stu-id="79554-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="79554-116">(iOS) Um [filiação do programa de programador Apple] [ 7] e um dispositivo iOS (simulador iOS suportam push).</span><span class="sxs-lookup"><span data-stu-id="79554-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="79554-117">(Windows) A [conta de programador da loja Windows] [ 8] e um dispositivo Windows 10.</span><span class="sxs-lookup"><span data-stu-id="79554-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="79554-118"><a name="configure-hub"></a>Configurar um hub de notificação</span><span class="sxs-lookup"><span data-stu-id="79554-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="79554-119">[Ver um vídeo que mostra os passos nesta secção][9]</span><span class="sxs-lookup"><span data-stu-id="79554-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="79554-120">Atualizar o projeto de servidor Olá</span><span class="sxs-lookup"><span data-stu-id="79554-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="79554-121"><a name="add-push-to-app"></a>Modificar a aplicação Cordova</span><span class="sxs-lookup"><span data-stu-id="79554-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="79554-122">Certifique-se o projeto de aplicação Apache Cordova notificações de push pronta toohandle por instalar Olá Cordova push Plug-in de plus quaisquer serviços push específicos da plataforma.</span><span class="sxs-lookup"><span data-stu-id="79554-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="79554-123">Atualize a versão de Cordova Olá no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="79554-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="79554-124">Se o seu projeto utiliza uma versão anterior ao v6.1.1 do Apache Cordova, atualize o projeto de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="79554-125">projeto de Olá tooupdate:</span><span class="sxs-lookup"><span data-stu-id="79554-125">tooupdate hello project:</span></span>

* <span data-ttu-id="79554-126">Clique com botão direito `config.xml` designer de configuração de Olá tooopen.</span><span class="sxs-lookup"><span data-stu-id="79554-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="79554-127">Selecione o separador de plataformas de Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="79554-128">Escolher 6.1.1 Olá **Cordova CLI** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="79554-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="79554-129">Escolha **criar**, em seguida, **compilar solução** projeto de Olá tooupdate.</span><span class="sxs-lookup"><span data-stu-id="79554-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="79554-130">Instalar o plug-in do Olá push</span><span class="sxs-lookup"><span data-stu-id="79554-130">Install hello push plugin</span></span>
<span data-ttu-id="79554-131">Aplicações do Apache Cordova não nativamente lidar com capacidades de rede ou de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="79554-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="79554-132">Estas funcionalidades são fornecidas pelo plug-ins que são publicadas um em [npm] [ 10] ou no GitHub.</span><span class="sxs-lookup"><span data-stu-id="79554-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="79554-133">Olá `phonegap-plugin-push` Plug-in é notificações de push de rede toohandle utilizados.</span><span class="sxs-lookup"><span data-stu-id="79554-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="79554-134">Pode instalar plug-in de push de Olá das seguintes formas:</span><span class="sxs-lookup"><span data-stu-id="79554-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="79554-135">**Olá-linha de comandos:**</span><span class="sxs-lookup"><span data-stu-id="79554-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="79554-136">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="79554-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="79554-137">**Do Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="79554-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="79554-138">No Explorador de soluções, abra Olá `config.xml` ficheiro clique **plug-ins** > **personalizada**, selecione **Git** como origem de instalação, em seguida, introduza `https://github.com/phonegap/phonegap-plugin-push`como origem Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="79554-139">Clique em Olá seta seguinte toohello origem da instalação.</span><span class="sxs-lookup"><span data-stu-id="79554-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="79554-140">No **SENDER_ID**, se já tiver um ID de projeto numérica para o projeto de consola de programador da Google Olá, pode adicioná-lo aqui.</span><span class="sxs-lookup"><span data-stu-id="79554-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="79554-141">Caso contrário, introduza um valor de marcador de posição, como 777777.</span><span class="sxs-lookup"><span data-stu-id="79554-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="79554-142">Se estiver a segmentar Android, pode atualizar este valor na config.xml mais tarde.</span><span class="sxs-lookup"><span data-stu-id="79554-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="79554-143">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="79554-143">Click **Add**.</span></span>

<span data-ttu-id="79554-144">Plug-in de push de Olá está agora instalado.</span><span class="sxs-lookup"><span data-stu-id="79554-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="79554-145">Instalar o plug-in dispositivo de Olá</span><span class="sxs-lookup"><span data-stu-id="79554-145">Install hello device plugin</span></span>
<span data-ttu-id="79554-146">Siga Olá mesmo procedimento utilizado tooinstall Olá push Plug-in.</span><span class="sxs-lookup"><span data-stu-id="79554-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="79554-147">Adicionar plug-in do Olá dispositivo da lista de plug-ins Olá Core (clique **plug-ins** > **Core** toofind-lo).</span><span class="sxs-lookup"><span data-stu-id="79554-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="79554-148">É necessário o nome do plataforma tooobtain Olá este plug-in.</span><span class="sxs-lookup"><span data-stu-id="79554-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="79554-149">Registar o seu dispositivo no arranque de aplicação</span><span class="sxs-lookup"><span data-stu-id="79554-149">Register your device on application start-up</span></span>
<span data-ttu-id="79554-150">Inicialmente, incluímos alguns código mínimas para Android.</span><span class="sxs-lookup"><span data-stu-id="79554-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="79554-151">Posteriormente, modifique Olá toorun de aplicações no iOS ou Windows 10.</span><span class="sxs-lookup"><span data-stu-id="79554-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="79554-152">Adicione uma chamada demasiado**registerForPushNotifications** durante a chamada de retorno de Olá para o processo de início de sessão de Olá ou na parte inferior de Olá de Olá **onDeviceReady** método:</span><span class="sxs-lookup"><span data-stu-id="79554-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="79554-153">Este exemplo mostra chamar **registerForPushNotifications** após a autenticação é concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="79554-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="79554-154">Pode chamar `registerForPushNotifications()` as vezes que é necessário.</span><span class="sxs-lookup"><span data-stu-id="79554-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="79554-155">Adicionar novo Olá **registerForPushNotifications** método da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="79554-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="79554-156">(Android) No Olá precedente código, substitua `Your_Project_ID` com numérica Olá projeto ID para a sua aplicação do [consola de programador da Google][18].</span><span class="sxs-lookup"><span data-stu-id="79554-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="79554-157">(Opcional) Configurar e executar a aplicação de Olá no Android</span><span class="sxs-lookup"><span data-stu-id="79554-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="79554-158">Conclua as notificações de push de tooenable esta secção para Android.</span><span class="sxs-lookup"><span data-stu-id="79554-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="79554-159"><a name="enable-gcm"></a>Ativar o Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="79554-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="79554-160">Uma vez que vamos como objetivo Olá plataforma Google Android inicialmente, tem de ativar Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="79554-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="79554-161"><a name="configure-backend"></a>Configurar as pedidos de push back-end de aplicação móvel do Olá toosend utilizando FCM</span><span class="sxs-lookup"><span data-stu-id="79554-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="79554-162">Configure a sua aplicação Cordova para Android</span><span class="sxs-lookup"><span data-stu-id="79554-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="79554-163">Na aplicação Cordova, abra config.xml e substitua `Your_Project_ID` com numérica Olá projeto ID para a sua aplicação de Olá [consola de programador da Google][18].</span><span class="sxs-lookup"><span data-stu-id="79554-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="79554-164">Abra index.js e atualizar Olá código toouse o ID numérico do projeto.</span><span class="sxs-lookup"><span data-stu-id="79554-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="79554-165"><a name="configure-device"></a>Configurar o seu dispositivo Android para a depuração USB</span><span class="sxs-lookup"><span data-stu-id="79554-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="79554-166">Antes de poder implementar a aplicação tooyour dispositivo Android, terá de tooenable depuração USB.</span><span class="sxs-lookup"><span data-stu-id="79554-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="79554-167">Execute os seguintes passos no seu telemóvel Android:</span><span class="sxs-lookup"><span data-stu-id="79554-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="79554-168">Aceda demasiado**definições** > **acerca do telemóvel**, em seguida, toque em Olá **número de compilação** até que o modo de programador está ativado (cerca de sete vezes).</span><span class="sxs-lookup"><span data-stu-id="79554-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="79554-169">Novamente no **definições** > **opções de programador** ativar **depuração USB**, em seguida, ligar o desenvolvimento de tooyour telemóvel Android PC com um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="79554-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="79554-170">Testamos isto através de um dispositivo de X Google 1000v 5 com o Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="79554-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="79554-171">No entanto, as técnicas de Olá são comuns a qualquer versão Android moderna.</span><span class="sxs-lookup"><span data-stu-id="79554-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="79554-172">Instalar serviços do Google Play</span><span class="sxs-lookup"><span data-stu-id="79554-172">Install Google Play Services</span></span>
<span data-ttu-id="79554-173">Plug-in de push de Olá baseia-se no Android serviços Google Play para notificações push.</span><span class="sxs-lookup"><span data-stu-id="79554-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="79554-174">No Visual Studio, clique em **ferramentas** > **Android** > **Gestor do Android SDK**, expanda Olá **Extras** pasta e verificação Olá caixa toomake se de que cada um dos seguintes SDKs de Olá está instalada.</span><span class="sxs-lookup"><span data-stu-id="79554-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="79554-175">Android 2.3 ou superior</span><span class="sxs-lookup"><span data-stu-id="79554-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="79554-176">Repositório Google revisão 27 ou superior</span><span class="sxs-lookup"><span data-stu-id="79554-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="79554-177">Serviços do Google Play 9.0.2 ou superior</span><span class="sxs-lookup"><span data-stu-id="79554-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="79554-178">Clique em **instalar pacotes** e aguarde Olá toocomplete de instalação.</span><span class="sxs-lookup"><span data-stu-id="79554-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="79554-179">Olá atual necessárias bibliotecas constam Olá [documentação de instalação push de plug-in de phonegap][19].</span><span class="sxs-lookup"><span data-stu-id="79554-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="79554-180">Notificações de push de teste na aplicação Olá no Android</span><span class="sxs-lookup"><span data-stu-id="79554-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="79554-181">Pode agora Olá de notificações de push de teste através da execução de aplicação e inserir itens na tabela TodoItem de Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="79554-182">Pode testar a partir de Olá mesmo dispositivo ou a partir de um segundo dispositivo, enquanto estiver a utilizar Olá mesmo back-end.</span><span class="sxs-lookup"><span data-stu-id="79554-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="79554-183">Teste a aplicação Cordova na plataforma Android Olá dos Olá seguintes formas:</span><span class="sxs-lookup"><span data-stu-id="79554-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="79554-184">**Num dispositivo físico:** ligar o computador de desenvolvimento do dispositivo Android tooyour com um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="79554-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="79554-185">Em vez de **emulador do Google Android**, selecione **dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="79554-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="79554-186">Visual Studio implementa o dispositivo de toohello Olá aplicação e, em seguida, executa a aplicação de Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="79554-187">Em seguida, pode interagir com a aplicação Olá no dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="79554-188">Melhore a sua experiência de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="79554-188">Improve your development experience.</span></span>  <span data-ttu-id="79554-189">Ecrã de partilha, tais como aplicações [Mobizen] [ 20] pode ajudá-lo a desenvolver uma aplicação Android.</span><span class="sxs-lookup"><span data-stu-id="79554-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="79554-190">Mobizen projetos web browser Android ecrã tooa no seu PC.</span><span class="sxs-lookup"><span data-stu-id="79554-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="79554-191">**No emulador do Android:** existem passos de configuração adicionais necessários quando em execução num emulador.</span><span class="sxs-lookup"><span data-stu-id="79554-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="79554-192">Certifique-se de que está a implementar o dispositivo virtual tooa com as APIs da Google definir como destino de Olá, conforme mostrado no Gestor do dispositivo Virtual Android (AVD) Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="79554-193">Se quiser toouse um x86 mais rápida do emulador, [instalar Olá HAXM controlador] [ 11] e configurar Olá emulador toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="79554-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="79554-194">Adicionar um dispositivo Android do Google conta toohello clicando **aplicações** > **definições** > **adicionar conta**, em seguida, siga as instruções de Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="79554-195">Executar a aplicação de todolist Olá como antes e inserir um novo item de todo.</span><span class="sxs-lookup"><span data-stu-id="79554-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="79554-196">Este tempo, um ícone de notificação é apresentado na área de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="79554-197">Pode abrir Olá notificação gaveta tooview Olá texto completo de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="79554-198">(Opcional) Configurar e executar em dispositivos iOS</span><span class="sxs-lookup"><span data-stu-id="79554-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="79554-199">Esta secção destina-se a executar o projeto Cordova de Olá em dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="79554-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="79554-200">Se não estiver a trabalhar com dispositivos iOS, pode ignorar esta secção.</span><span class="sxs-lookup"><span data-stu-id="79554-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="79554-201">Instalar e executar Olá iOS remoto criar o agente num serviço de nuvem ou Mac</span><span class="sxs-lookup"><span data-stu-id="79554-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="79554-202">Antes de poder executar uma aplicação Cordova em dispositivos iOS com o Visual Studio, efetuar os passos de Olá no Olá [iOS guia de configuração] [ 12] tooinstall e Olá execução remota Criar agente.</span><span class="sxs-lookup"><span data-stu-id="79554-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="79554-203">Certifique-se de que pode criar a aplicação de Olá para iOS.</span><span class="sxs-lookup"><span data-stu-id="79554-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="79554-204">Olá passos no guia de configuração de Olá são necessária toobuild para iOS a partir do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79554-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="79554-205">Se não tiver um Mac, pode criar para iOS com o agente de compilação remoto de Olá num serviço como MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="79554-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="79554-206">Para obter mais informações, consulte [executar a aplicação do iOS na nuvem de Olá][21].</span><span class="sxs-lookup"><span data-stu-id="79554-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="79554-207">XCode 7 ou superior, é necessário toouse Olá push Plug-in do IOS.</span><span class="sxs-lookup"><span data-stu-id="79554-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="79554-208">Localizar Olá ID toouse como o seu ID de aplicação</span><span class="sxs-lookup"><span data-stu-id="79554-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="79554-209">Antes de registar a sua aplicação para notificações push, abra config.xml na sua aplicação Cordova, determinar Olá `id` atributo valor no elemento de widget Olá e copie-a para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="79554-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="79554-210">Olá XML a seguir, Olá ID é `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="79554-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="79554-211">Mais tarde, utilize este identificador quando criar um ID de aplicação no portal de programador da Apple.</span><span class="sxs-lookup"><span data-stu-id="79554-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="79554-212">Se criar um ID de aplicação diferente no portal do programador Olá, tem de colocar alguns passos adicionais mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="79554-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="79554-213">ID de Olá no elemento widget tem de corresponder ao hello ID da aplicação no portal do programador Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="79554-214">Registar a aplicação Olá para notificações push no portal de programador da Apple</span><span class="sxs-lookup"><span data-stu-id="79554-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="79554-215">Veja um vídeo que mostra os passos semelhantes</span><span class="sxs-lookup"><span data-stu-id="79554-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="79554-216">Configurar notificações de push toosend do Azure</span><span class="sxs-lookup"><span data-stu-id="79554-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="79554-217">Certifique-se de que o ID da aplicação corresponde à sua aplicação Cordova</span><span class="sxs-lookup"><span data-stu-id="79554-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="79554-218">Se Olá ID da aplicação que criou na sua conta de programador Apple já corresponde ao ID de Olá do elemento de widget Olá no config.xml, pode ignorar este passo.</span><span class="sxs-lookup"><span data-stu-id="79554-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="79554-219">No entanto, se Olá IDs não corresponderem, siga Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="79554-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="79554-220">Elimine a pasta de plataformas de Olá do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="79554-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="79554-221">Elimine a pasta de plug-ins de Olá do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="79554-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="79554-222">Elimine a pasta de node_modules de Olá do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="79554-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="79554-223">Atualize o atributo id Olá do elemento de widget Olá no config.xml toouse Olá ID da aplicação que criou na sua conta de programador da Apple.</span><span class="sxs-lookup"><span data-stu-id="79554-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="79554-224">Reconstrua o projeto.</span><span class="sxs-lookup"><span data-stu-id="79554-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="79554-225">Notificações de push de teste na sua aplicação iOS</span><span class="sxs-lookup"><span data-stu-id="79554-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="79554-226">No Visual Studio, certifique-se de que **iOS** está selecionado como destino de implementação de Olá e, em seguida, escolha **dispositivo** toorun no seu dispositivo iOS ligado.</span><span class="sxs-lookup"><span data-stu-id="79554-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="79554-227">Pode executar em tooyour de dispositivo ligado um iOS PC utilizando iTunes.</span><span class="sxs-lookup"><span data-stu-id="79554-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="79554-228">Simulador de iOS Olá não suporta notificações push.</span><span class="sxs-lookup"><span data-stu-id="79554-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="79554-229">Olá prima **executar** botão ou **F5** no Visual Studio toobuild projeto Olá e início Olá aplicação no dispositivo iOS, em seguida, clique em **OK** tooaccept notificações de push.</span><span class="sxs-lookup"><span data-stu-id="79554-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="79554-230">aplicação Olá pede a confirmação para notificações push durante Olá executar pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="79554-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="79554-231">Na aplicação Olá, escreva uma tarefa e, em seguida, clique em Olá mais (+) ícone.</span><span class="sxs-lookup"><span data-stu-id="79554-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="79554-232">Certifique-se de que uma notificação é recebida, em seguida, clique em OK toodismiss Olá notificação.</span><span class="sxs-lookup"><span data-stu-id="79554-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="79554-233">(Opcional) Configurar e executar no Windows</span><span class="sxs-lookup"><span data-stu-id="79554-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="79554-234">Esta secção destina-se a executar o projeto de aplicação Apache Cordova Olá em dispositivos Windows 10 (Olá PhoneGap push Plug-in é suportado no Windows 10).</span><span class="sxs-lookup"><span data-stu-id="79554-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="79554-235">Se não estiver a trabalhar com dispositivos Windows, pode ignorar esta secção.</span><span class="sxs-lookup"><span data-stu-id="79554-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="79554-236">Registar a aplicação do Windows para notificações push no WNS</span><span class="sxs-lookup"><span data-stu-id="79554-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="79554-237">Opções de arquivo de Olá toouse no Visual Studio, selecione um destino de Windows a partir da lista de plataformas de solução Olá, como **Windows x64** ou **Windows x86** (evitar **Windows AnyCPU** para as notificações push).</span><span class="sxs-lookup"><span data-stu-id="79554-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="79554-238">[Ver um vídeo que mostra os passos semelhantes][13]</span><span class="sxs-lookup"><span data-stu-id="79554-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="79554-239">Configurar Olá notification hub para WNS</span><span class="sxs-lookup"><span data-stu-id="79554-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="79554-240">Configurar as notificações push da Cordova aplicação toosupport Windows</span><span class="sxs-lookup"><span data-stu-id="79554-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="79554-241">Designer de configuração de Olá abrir (com o botão direito no config.xml e selecione **estruturador de vistas**), selecione Olá **Windows** separador e escolha **Windows 10** em **Windows versão de destino**.</span><span class="sxs-lookup"><span data-stu-id="79554-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="79554-242">notificações de push toosupport na sua predefinição (debug) baseia-se, build.json abrir ficheiros.</span><span class="sxs-lookup"><span data-stu-id="79554-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="79554-243">Copie a configuração de depuração de tooyour de configuração de "release".</span><span class="sxs-lookup"><span data-stu-id="79554-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="79554-244">Após a atualização de Olá, Olá build.json deve conter Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="79554-244">After hello update, hello build.json should contain hello following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="79554-245">Criar aplicação Olá e certifique-se de que tem sem erros.</span><span class="sxs-lookup"><span data-stu-id="79554-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="79554-246">A aplicação cliente deve agora registar-se para obter notificações de Olá do back-end de aplicação móvel de Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="79554-247">Repita esta secção para cada projeto Windows na sua solução.</span><span class="sxs-lookup"><span data-stu-id="79554-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="79554-248">Notificações de push de teste na sua aplicação do Windows</span><span class="sxs-lookup"><span data-stu-id="79554-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="79554-249">No Visual Studio, certifique-se de que uma plataforma do Windows se encontra selecionada como destino de implementação de Olá, tais como **Windows x64** ou **Windows x86**.</span><span class="sxs-lookup"><span data-stu-id="79554-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="79554-250">aplicação de Olá toorun em PCs Windows 10 que aloja o Visual Studio, escolha **máquina Local**.</span><span class="sxs-lookup"><span data-stu-id="79554-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="79554-251">Olá prima executar botão toobuild Olá projeto e iniciar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="79554-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="79554-252">Na aplicação Olá, escreva um nome para um todoitem novo e, em seguida, clique em Olá mais (+) ícone tooadd-lo.</span><span class="sxs-lookup"><span data-stu-id="79554-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="79554-253">Certifique-se de que é recebida uma notificação quando o item de Olá foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="79554-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="79554-254"><a name="next-steps"></a>Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="79554-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="79554-255">Leia sobre [Notification Hubs] [ 17] toolearn sobre as notificações push.</span><span class="sxs-lookup"><span data-stu-id="79554-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="79554-256">Se ainda não o tiver feito, continuar o tutorial Olá por [adicionar a autenticação] [ 14] aplicação Apache Cordova de tooyour.</span><span class="sxs-lookup"><span data-stu-id="79554-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="79554-257">Saiba como toouse Olá SDKs.</span><span class="sxs-lookup"><span data-stu-id="79554-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="79554-258">[SDK do Apache Cordova][15]</span><span class="sxs-lookup"><span data-stu-id="79554-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="79554-259">[SDK do servidor ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="79554-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="79554-260">[SDK do servidor node.js][16]</span><span class="sxs-lookup"><span data-stu-id="79554-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
