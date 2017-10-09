---
title: "aaaGet aos Notification hubs do Azure para aplicações Kindle | Microsoft Docs"
description: "Neste tutorial, saiba como toouse Notification Hubs do Azure toosend push aplicação de Kindle tooa de notificações."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>Introdução aos Notification Hubs para Aplicações Kindle
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Descrição geral
Este tutorial mostra como toouse Notification Hubs do Azure toosend push aplicação de Kindle tooa de notificações.
Deverá criar uma aplicação Kindle que receba notificações push através do Amazon Device Messaging (ADM).

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte Olá:

* Obter Olá Android SDK (partimos do princípio que utiliza o Eclipse) de Olá <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site do Android</a>.
* Siga os passos Olá <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">definição se o ambiente de desenvolvimento</a> tooset configurar o ambiente de desenvolvimento para o Kindle.

## <a name="add-a-new-app-toohello-developer-portal"></a>Adicionar um novo portal de programador toohello de aplicação
1. Em primeiro lugar, criar uma aplicação no Olá [portal de programador da Amazon].
   
    ![][0]
2. Olá cópia **chave da aplicação**.
   
    ![][1]
3. No portal de Olá, clique no nome de Olá da sua aplicação e, em seguida, clique em Olá **Device Messaging** separador.
   
    ![][2]
4. Clique em **Criar um Novo Perfil de Segurança** e crie um novo perfil de segurança (por exemplo, **Perfil de segurança TestAdm**). Em seguida, clique em **Guardar**.
   
    ![][3]
5. Clique em **perfis de segurança** tooview Olá segurança perfil que acabou de criar. Olá cópia **ID de cliente** e **segredo do cliente** valores para utilização posterior.
   
    ![][4]

## <a name="create-an-api-key"></a>Criar uma chave de API
1. Abra uma linha de comandos com privilégios de administrador.
2. Navegue toohello pasta de Android SDK.
3. Introduza Olá os seguintes comandos:
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Para Olá **keystore** palavra-passe, escreva **android**.
5. Olá cópia **MD5** impressão digital.
6. No portal de programador Olá, no Olá **mensagens** separador, clique em **Android/Kindle** e introduza o nome de Olá do pacote de Olá para a sua aplicação (por exemplo, **com.sample.notificationhubtest**) e Olá **MD5** valor e, em seguida, clique em **gerar a chave de API**.

## <a name="add-credentials-toohello-hub"></a>Adicionar hub toohello de credenciais
No portal de Olá, adicionar Olá cliente segredo e cliente ID toohello **configurar** separador do notification hub.

## <a name="set-up-your-application"></a>Configurar a aplicação
> [!NOTE]
> Quando estiver a criar uma aplicação, utilize no mínimo uma API de nível 17.
> 
> 

Adicione o projeto do Olá ADM bibliotecas tooyour Eclipse:

1. tooobtain Olá biblioteca ADM, deverá [transferir Olá SDK]. Extraia o ficheiro zip do Olá SDK.
2. No Eclipse, clique com o botão direito do rato no projeto e, em seguida, clique em **Propriedades**. Selecione **criar caminho Java** em Olá à esquerda e, em seguida, selecione de Olá * * bibliotecas * * separador na parte superior do Olá. Clique em **adicionar Jar externo**e selecione Olá ficheiro `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` do diretório de olá onde extraiu Olá Amazon SDK.
3. Transferir Olá Android SDK do NotificationHubs (ligação).
4. Deszipe o pacote Olá e, em seguida, arraste o ficheiro de Olá `notification-hubs-sdk.jar` para Olá `libs` pasta no Eclipse.

Edite o toosupport manifesto de aplicação ADM:

1. Adicione espaço de nomes do Olá Amazon Olá elemento raiz do manifesto:

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. Adicione permissões como primeiro elemento de Olá no elemento manifesto Olá. Substitute **[nome do seu pacote]** com o pacote de Olá que utilizou toocreate a aplicação.
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. Inserir Olá seguinte elemento como o primeiro subordinado de Olá do elemento de aplicação Olá. Lembre-se toosubstitute **[nome do seu serviço]** com o nome do processador de mensagens ADM que criar na secção seguinte do Olá (pacote de Olá incluindo) e substitua Olá **[nome do seu pacote]** com Olá nome do pacote com a qual criou a aplicação.
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a>Criar o processador de mensagens ADM
1. Criar uma nova classe que herda de `com.amazon.device.messaging.ADMMessageHandlerBase` e dê-lhe nome `MyADMMessageHandler`, conforme apresentado na Olá figura a seguir:
   
    ![][6]
2. Adicione Olá seguinte `import` instruções:
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. Adicione Olá seguinte código na classe de Olá que criou. Não se esqueça toosubstitute Olá ligação e o nome da cadeia do hub (escutar):
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. Adicionar Olá seguinte código toohello `OnMessage()` método:
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. Adicionar Olá seguinte código toohello `OnRegistered` método:
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. Adicionar Olá seguinte código toohello `OnUnregistered` método:
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. No Olá `MainActivity` método, adicione as seguintes declarações de importação de Olá:
   
        import com.amazon.device.messaging.ADM;
8. Adicionar Olá seguinte código no final Olá Olá `OnCreate` método:
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a>Adicionar a aplicação de tooyour chave de API
1. No Eclipse, crie um novo ficheiro designado **api_key.txt** em recursos de diretório de Olá do seu projeto.
2. Abra Olá ficheiro e cópia Olá chave de API que gerou no portal de programador da Amazon Olá.

## <a name="run-hello-app"></a>Executar a aplicação Olá
1. Inicie o emulador de Olá.
2. No emulador Olá, percorra a partir da parte superior do Olá e clique em **definições**e, em seguida, clique em **minha conta** e registar uma conta válida da Amazon.
3. No Eclipse, execute a aplicação Olá.

> [!NOTE]
> Se ocorrer um problema, verifique a hora de Olá do emulador de Olá (ou dispositivo). valor de tempo de Olá tem de ser exato. tempo de Olá toochange do emulador do Kindle Olá, pode executar Olá os seguintes comandos do diretório de ferramentas de plataforma Android SDK:
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>Enviar uma mensagem
toosend uma mensagem com o .NET:

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[portal de programador da Amazon]: https://developer.amazon.com/home.html
[transferir Olá SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
