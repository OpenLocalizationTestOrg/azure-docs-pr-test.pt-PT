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
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>Adicionar a aplicação de Apache Cordova de tooyour de notificações push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Descrição geral
Neste tutorial, adicione projeto de toohello [início rápido do Apache Cordova] de notificações push para que uma notificação push é enviada toohello dispositivo sempre que é inserido um registo.

Se não utilizar Olá transferir o projeto de servidor de início rápido, precisa de Olá o pacote de extensão de notificação push. Para obter mais informações, consulte [trabalhar com o servidor de back-end de .NET Olá SDK de Mobile Apps do Azure][1].

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial abrange uma aplicação Apache Cordova desenvolvida com o Visual Studio 2015, que é executado no Olá emulador do Google Android, um dispositivo Android, um dispositivo Windows e um dispositivo iOS.

toocomplete neste tutorial, precisa de:

* Um PC com [Visual Studio Community 2015] [ 2] ou versões posteriores.
* [Visual Studio Tools para Apache Cordova][4].
* Um [conta ativa do Azure][3].
* Uma conclusão [início rápido do Apache Cordova] [ 5] projeto.
* (Android) A [conta Google] [ 6] com um endereço de correio eletrónico verificado.
* (iOS) Um [filiação do programa de programador Apple] [ 7] e um dispositivo iOS (simulador iOS suportam push).
* (Windows) A [conta de programador da loja Windows] [ 8] e um dispositivo Windows 10.

## <a name="configure-hub"></a>Configurar um hub de notificação
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[Ver um vídeo que mostra os passos nesta secção][9]

## <a name="update-hello-server-project"></a>Atualizar o projeto de servidor Olá
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Modificar a aplicação Cordova
Certifique-se o projeto de aplicação Apache Cordova notificações de push pronta toohandle por instalar Olá Cordova push Plug-in de plus quaisquer serviços push específicos da plataforma.

#### <a name="update-hello-cordova-version-in-your-project"></a>Atualize a versão de Cordova Olá no seu projeto.
Se o seu projeto utiliza uma versão anterior ao v6.1.1 do Apache Cordova, atualize o projeto de cliente Olá. projeto de Olá tooupdate:

* Clique com botão direito `config.xml` designer de configuração de Olá tooopen.
* Selecione o separador de plataformas de Olá.
* Escolher 6.1.1 Olá **Cordova CLI** caixa de texto.
* Escolha **criar**, em seguida, **compilar solução** projeto de Olá tooupdate.

#### <a name="install-hello-push-plugin"></a>Instalar o plug-in do Olá push
Aplicações do Apache Cordova não nativamente lidar com capacidades de rede ou de dispositivo.  Estas funcionalidades são fornecidas pelo plug-ins que são publicadas um em [npm] [ 10] ou no GitHub.  Olá `phonegap-plugin-push` Plug-in é notificações de push de rede toohandle utilizados.

Pode instalar plug-in de push de Olá das seguintes formas:

**Olá-linha de comandos:**

Execute Olá os seguintes comandos:

    cordova plugin add phonegap-plugin-push

**Do Visual Studio:**

1. No Explorador de soluções, abra Olá `config.xml` ficheiro clique **plug-ins** > **personalizada**, selecione **Git** como origem de instalação, em seguida, introduza `https://github.com/phonegap/phonegap-plugin-push`como origem Olá.

   ![][img1]

2. Clique em Olá seta seguinte toohello origem da instalação.
3. No **SENDER_ID**, se já tiver um ID de projeto numérica para o projeto de consola de programador da Google Olá, pode adicioná-lo aqui. Caso contrário, introduza um valor de marcador de posição, como 777777.  Se estiver a segmentar Android, pode atualizar este valor na config.xml mais tarde.
4. Clique em **Adicionar**.

Plug-in de push de Olá está agora instalado.

#### <a name="install-hello-device-plugin"></a>Instalar o plug-in dispositivo de Olá
Siga Olá mesmo procedimento utilizado tooinstall Olá push Plug-in.  Adicionar plug-in do Olá dispositivo da lista de plug-ins Olá Core (clique **plug-ins** > **Core** toofind-lo). É necessário o nome do plataforma tooobtain Olá este plug-in.

#### <a name="register-your-device-on-application-start-up"></a>Registar o seu dispositivo no arranque de aplicação
Inicialmente, incluímos alguns código mínimas para Android. Posteriormente, modifique Olá toorun de aplicações no iOS ou Windows 10.

1. Adicione uma chamada demasiado**registerForPushNotifications** durante a chamada de retorno de Olá para o processo de início de sessão de Olá ou na parte inferior de Olá de Olá **onDeviceReady** método:

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

    Este exemplo mostra chamar **registerForPushNotifications** após a autenticação é concluída com êxito.  Pode chamar `registerForPushNotifications()` as vezes que é necessário.

2. Adicionar novo Olá **registerForPushNotifications** método da seguinte forma:

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
3. (Android) No Olá precedente código, substitua `Your_Project_ID` com numérica Olá projeto ID para a sua aplicação do [consola de programador da Google][18].

## <a name="optional-configure-and-run-hello-app-on-android"></a>(Opcional) Configurar e executar a aplicação de Olá no Android
Conclua as notificações de push de tooenable esta secção para Android.

#### <a name="enable-gcm"></a>Ativar o Firebase Cloud Messaging
Uma vez que vamos como objetivo Olá plataforma Google Android inicialmente, tem de ativar Firebase Cloud Messaging.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Configurar as pedidos de push back-end de aplicação móvel do Olá toosend utilizando FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Configure a sua aplicação Cordova para Android
Na aplicação Cordova, abra config.xml e substitua `Your_Project_ID` com numérica Olá projeto ID para a sua aplicação de Olá [consola de programador da Google][18].

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

Abra index.js e atualizar Olá código toouse o ID numérico do projeto.

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>Configurar o seu dispositivo Android para a depuração USB
Antes de poder implementar a aplicação tooyour dispositivo Android, terá de tooenable depuração USB.  Execute os seguintes passos no seu telemóvel Android:

1. Aceda demasiado**definições** > **acerca do telemóvel**, em seguida, toque em Olá **número de compilação** até que o modo de programador está ativado (cerca de sete vezes).
2. Novamente no **definições** > **opções de programador** ativar **depuração USB**, em seguida, ligar o desenvolvimento de tooyour telemóvel Android PC com um cabo USB.

Testamos isto através de um dispositivo de X Google 1000v 5 com o Android 6.0 (Marshmallow).  No entanto, as técnicas de Olá são comuns a qualquer versão Android moderna.

#### <a name="install-google-play-services"></a>Instalar serviços do Google Play
Plug-in de push de Olá baseia-se no Android serviços Google Play para notificações push.

1. No Visual Studio, clique em **ferramentas** > **Android** > **Gestor do Android SDK**, expanda Olá **Extras** pasta e verificação Olá caixa toomake se de que cada um dos seguintes SDKs de Olá está instalada.

   * Android 2.3 ou superior
   * Repositório Google revisão 27 ou superior
   * Serviços do Google Play 9.0.2 ou superior

2. Clique em **instalar pacotes** e aguarde Olá toocomplete de instalação.

Olá atual necessárias bibliotecas constam Olá [documentação de instalação push de plug-in de phonegap][19].

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Notificações de push de teste na aplicação Olá no Android
Pode agora Olá de notificações de push de teste através da execução de aplicação e inserir itens na tabela TodoItem de Olá. Pode testar a partir de Olá mesmo dispositivo ou a partir de um segundo dispositivo, enquanto estiver a utilizar Olá mesmo back-end. Teste a aplicação Cordova na plataforma Android Olá dos Olá seguintes formas:

* **Num dispositivo físico:** ligar o computador de desenvolvimento do dispositivo Android tooyour com um cabo USB.  Em vez de **emulador do Google Android**, selecione **dispositivo**. Visual Studio implementa o dispositivo de toohello Olá aplicação e, em seguida, executa a aplicação de Olá.  Em seguida, pode interagir com a aplicação Olá no dispositivo Olá.

  Melhore a sua experiência de desenvolvimento.  Ecrã de partilha, tais como aplicações [Mobizen] [ 20] pode ajudá-lo a desenvolver uma aplicação Android.  Mobizen projetos web browser Android ecrã tooa no seu PC.

* **No emulador do Android:** existem passos de configuração adicionais necessários quando em execução num emulador.

    Certifique-se de que está a implementar o dispositivo virtual tooa com as APIs da Google definir como destino de Olá, conforme mostrado no Gestor do dispositivo Virtual Android (AVD) Olá.

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Se quiser toouse um x86 mais rápida do emulador, [instalar Olá HAXM controlador] [ 11] e configurar Olá emulador toouse-lo.

    Adicionar um dispositivo Android do Google conta toohello clicando **aplicações** > **definições** > **adicionar conta**, em seguida, siga as instruções de Olá.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    Executar a aplicação de todolist Olá como antes e inserir um novo item de todo. Este tempo, um ícone de notificação é apresentado na área de notificação de Olá. Pode abrir Olá notificação gaveta tooview Olá texto completo de notificação de Olá.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(Opcional) Configurar e executar em dispositivos iOS
Esta secção destina-se a executar o projeto Cordova de Olá em dispositivos iOS. Se não estiver a trabalhar com dispositivos iOS, pode ignorar esta secção.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Instalar e executar Olá iOS remoto criar o agente num serviço de nuvem ou Mac
Antes de poder executar uma aplicação Cordova em dispositivos iOS com o Visual Studio, efetuar os passos de Olá no Olá [iOS guia de configuração] [ 12] tooinstall e Olá execução remota Criar agente.

Certifique-se de que pode criar a aplicação de Olá para iOS. Olá passos no guia de configuração de Olá são necessária toobuild para iOS a partir do Visual Studio. Se não tiver um Mac, pode criar para iOS com o agente de compilação remoto de Olá num serviço como MacInCloud. Para obter mais informações, consulte [executar a aplicação do iOS na nuvem de Olá][21].

> [!NOTE]
> XCode 7 ou superior, é necessário toouse Olá push Plug-in do IOS.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>Localizar Olá ID toouse como o seu ID de aplicação
Antes de registar a sua aplicação para notificações push, abra config.xml na sua aplicação Cordova, determinar Olá `id` atributo valor no elemento de widget Olá e copie-a para utilização posterior. Olá XML a seguir, Olá ID é `io.cordova.myapp7777777`.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

Mais tarde, utilize este identificador quando criar um ID de aplicação no portal de programador da Apple. Se criar um ID de aplicação diferente no portal do programador Olá, tem de colocar alguns passos adicionais mais tarde no tutorial. ID de Olá no elemento widget tem de corresponder ao hello ID da aplicação no portal do programador Olá.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Registar a aplicação Olá para notificações push no portal de programador da Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[Veja um vídeo que mostra os passos semelhantes](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Configurar notificações de push toosend do Azure
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>Certifique-se de que o ID da aplicação corresponde à sua aplicação Cordova
Se Olá ID da aplicação que criou na sua conta de programador Apple já corresponde ao ID de Olá do elemento de widget Olá no config.xml, pode ignorar este passo. No entanto, se Olá IDs não corresponderem, siga Olá os seguintes passos:

1. Elimine a pasta de plataformas de Olá do seu projeto.
2. Elimine a pasta de plug-ins de Olá do seu projeto.
3. Elimine a pasta de node_modules de Olá do seu projeto.
4. Atualize o atributo id Olá do elemento de widget Olá no config.xml toouse Olá ID da aplicação que criou na sua conta de programador da Apple.
5. Reconstrua o projeto.

##### <a name="test-push-notifications-in-your-ios-app"></a>Notificações de push de teste na sua aplicação iOS
1. No Visual Studio, certifique-se de que **iOS** está selecionado como destino de implementação de Olá e, em seguida, escolha **dispositivo** toorun no seu dispositivo iOS ligado.

    Pode executar em tooyour de dispositivo ligado um iOS PC utilizando iTunes. Simulador de iOS Olá não suporta notificações push.

2. Olá prima **executar** botão ou **F5** no Visual Studio toobuild projeto Olá e início Olá aplicação no dispositivo iOS, em seguida, clique em **OK** tooaccept notificações de push.

   > [!NOTE]
   > aplicação Olá pede a confirmação para notificações push durante Olá executar pela primeira vez.

3. Na aplicação Olá, escreva uma tarefa e, em seguida, clique em Olá mais (+) ícone.
4. Certifique-se de que uma notificação é recebida, em seguida, clique em OK toodismiss Olá notificação.

## <a name="optional-configure-and-run-on-windows"></a>(Opcional) Configurar e executar no Windows
Esta secção destina-se a executar o projeto de aplicação Apache Cordova Olá em dispositivos Windows 10 (Olá PhoneGap push Plug-in é suportado no Windows 10). Se não estiver a trabalhar com dispositivos Windows, pode ignorar esta secção.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>Registar a aplicação do Windows para notificações push no WNS
Opções de arquivo de Olá toouse no Visual Studio, selecione um destino de Windows a partir da lista de plataformas de solução Olá, como **Windows x64** ou **Windows x86** (evitar **Windows AnyCPU** para as notificações push).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[Ver um vídeo que mostra os passos semelhantes][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>Configurar Olá notification hub para WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Configurar as notificações push da Cordova aplicação toosupport Windows
Designer de configuração de Olá abrir (com o botão direito no config.xml e selecione **estruturador de vistas**), selecione Olá **Windows** separador e escolha **Windows 10** em **Windows versão de destino**.

notificações de push toosupport na sua predefinição (debug) baseia-se, build.json abrir ficheiros. Copie a configuração de depuração de tooyour de configuração de "release".

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Após a atualização de Olá, Olá build.json deve conter Olá seguinte código:

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

Criar aplicação Olá e certifique-se de que tem sem erros. A aplicação cliente deve agora registar-se para obter notificações de Olá do back-end de aplicação móvel de Olá. Repita esta secção para cada projeto Windows na sua solução.

#### <a name="test-push-notifications-in-your-windows-app"></a>Notificações de push de teste na sua aplicação do Windows
No Visual Studio, certifique-se de que uma plataforma do Windows se encontra selecionada como destino de implementação de Olá, tais como **Windows x64** ou **Windows x86**. aplicação de Olá toorun em PCs Windows 10 que aloja o Visual Studio, escolha **máquina Local**.

Olá prima executar botão toobuild Olá projeto e iniciar a aplicação Olá.

Na aplicação Olá, escreva um nome para um todoitem novo e, em seguida, clique em Olá mais (+) ícone tooadd-lo.

Certifique-se de que é recebida uma notificação quando o item de Olá foi adicionado.

## <a name="next-steps"></a>Passos Seguintes
* Leia sobre [Notification Hubs] [ 17] toolearn sobre as notificações push.
* Se ainda não o tiver feito, continuar o tutorial Olá por [adicionar a autenticação] [ 14] aplicação Apache Cordova de tooyour.

Saiba como toouse Olá SDKs.

* [SDK do Apache Cordova][15]
* [SDK do servidor ASP.NET][1]
* [SDK do servidor node.js][16]

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
