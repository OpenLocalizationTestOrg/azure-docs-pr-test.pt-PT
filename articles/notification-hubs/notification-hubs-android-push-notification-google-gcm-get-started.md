---
title: "aaaSending tooAndroid de notificações push com Notification Hubs do Azure | Microsoft Docs"
description: "Neste tutorial, saiba como dispositivos de tooAndroid do toouse Notification Hubs do Azure toopush notificações."
services: notification-hubs
documentationcenter: android
keywords: "notificações push, notificação push, notificação push android"
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>Enviar tooAndroid de notificações push com Notification Hubs do Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Descrição geral
> [!IMPORTANT]
> Este tópico demonstra as notificações push com o Google Cloud Messaging (GCM). Se estiver a utilizar Firebase Cloud Messaging (FCM da Google), consulte o artigo [Sending tooAndroid de notificações push com Notification Hubs do Azure e FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).
> 
> 

Este tutorial mostra como toouse Notification Hubs do Azure toosend push aplicação Android de tooan de notificações.
Irá criar uma aplicação em branco com Android que recebe notificações push através do Google Cloud Messaging (GCM).

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

código de Olá concluída para este tutorial pode ser transferido a partir do GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).

## <a name="prerequisites"></a>Pré-requisitos
> [!IMPORTANT]
> toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

Além disso conta ativa do Azure tooan mencionado acima, este tutorial só requer a versão mais recente do Olá do [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais de Notification Hubs para aplicações com Android.

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a>Criar um projeto que suporte o Google Cloud Messaging
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Configurar um novo Notification Hub
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   No Olá **definições** painel, selecione **serviços de notificação** e, em seguida, **Google (GCM)**. Introduza a chave de Olá API e clique em **guardar**.

&emsp;&emsp;![Notification Hubs do Azure – Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

O notification hub está agora configurado toowork com o GCM e tem as cadeias de ligação do Olá tooboth registar a sua tooreceive de aplicação e enviar notificações push.

## <a id="connecting-app"></a>Ligar o seu hub de notificação de toohello de aplicação
### <a name="create-a-new-android-project"></a>Criar um novo projeto Android
1. No Android Studio, inicie um novo projeto de Android Studio.
   
   ![Android Studio - novo projeto][13]
2. Escolha Olá **telefone e Tablet** formam factor e Olá **SDK mínimo** que pretende que o toosupport. Clique depois em **Seguinte**.
   
   ![Android Studio – fluxo de trabalho da criação do projeto][14]
3. Escolha **atividade vazia** para a atividade principal Olá, clique em **seguinte**e, em seguida, clique em **concluir**.

### <a name="add-google-play-services-toohello-project"></a>Adicione o projeto de toohello de serviços do Google Play
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Adicionar bibliotecas dos Notification Hubs do Azure
1. No Olá `Build.Gradle` ficheiro para Olá **aplicação**, adicionar Olá seguintes linhas no Olá **dependências** secção.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. Adicionar Olá seguir repositório após Olá **dependências** secção.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>A atualizar Olá AndroidManifest.xml.
1. toosupport GCM, temos de implementar um serviço de escuta de ID de instância no nosso código que é utilizado demasiado[obter os tokens de registo](https://developers.google.com/cloud-messaging/android/client#sample-register) utilizando [API de ID de instância da Google](https://developers.google.com/instance-id/). Neste tutorial, iremos designar a classe de Olá `MyInstanceIDService`. 
   
    Adicionar Olá seguinte serviço definição toohello ficheiro AndroidManifest.xml, no interior Olá `<application>` etiquetas. Substitua Olá `<your package>` Olá de marcador de posição com o nome do seu pacote real indicado no topo de Olá da Olá `AndroidManifest.xml` ficheiro.
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. Depois de receber o nosso token de registo do GCM de Olá API da ID de instância, vamos utilizá-lo demasiado[registar Olá Notification Hub do Azure](notification-hubs-push-notification-registration-management.md). Iremos suportar este registo em segundo plano, Olá utilizando um `IntentService` denominado `RegistrationIntentService`. Este serviço também será responsável por [atualizar o nosso token de registo do GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).
   
    Adicionar Olá seguinte serviço definição toohello ficheiro AndroidManifest.xml, no interior Olá `<application>` etiquetas. Substitua Olá `<your package>` Olá de marcador de posição com o nome do seu pacote real indicado no topo de Olá da Olá `AndroidManifest.xml` ficheiro. 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. Iremos também definir notificações de tooreceive um recetor. Adicionar Olá seguir recetor definição toohello ficheiro AndroidManifest.xml, no interior Olá `<application>` etiquetas. Substitua Olá `<your package>` Olá de marcador de posição com o nome do seu pacote real indicado no topo de Olá da Olá `AndroidManifest.xml` ficheiro.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Adicionar Olá GCM necessário os seguintes relacionados com permissões abaixo Olá `</application>` etiquetas. Certifique-se de que tooreplace `<your package>` com nome de pacote de Olá indicado no topo de Olá da Olá `AndroidManifest.xml` ficheiro.
   
    Para obter mais informações sobre estas permissões, consulte o artigo [Configurar uma aplicação de cliente do GCM para Android](https://developers.google.com/cloud-messaging/android/client#manifest).
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a>Adicionar código
1. Na vista de projeto Olá, expanda **aplicação** > **src** > **principal** > **java**. Com o botão direito do rato, clique na pasta do pacote por baixo de **java**, clique em **Nova**, e, em seguida, clique em **Classe Java**. Adicione uma nova classe com o nome `NotificationSettings`. 
   
    ![Android Studio - nova classe Java][6]
   
    Certifique-se tooupdate Olá estes três marcadores de posição no seguinte código para Olá de Olá `NotificationSettings` classe:
   
   * **SenderId**: Olá número do projeto que obteve anteriormente no Olá [Google Cloud Console](http://cloud.google.com/console).
   * **HubListenConnectionString**: Olá **DefaultListenAccessSignature** cadeia de ligação para o seu hub. Pode copiar essa cadeia de ligação ao clicar em **políticas de acesso** no Olá **definições** painel do seu hub no Olá [Portal do Azure].
   * **HubName**: Utilize o nome de Olá do notification hub que aparece no painel do hub de Olá no Olá [Portal do Azure].
     
     Código `NotificationSettings`:
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       }
2. Utilizando os passos de Olá acima, adicione outra nova classe com o nome `MyInstanceIDService`. Esta será a nossa implementação do serviço de escuta de ID da instância.
   
    Olá código para esta classe irá chamar nosso `IntentService` demasiado[token do GCM atualização Olá](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) em segundo plano de Olá.
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. Adicione outra nova classe tooyour projeto com o nome, `RegistrationIntentService`. Esta será Olá implementação para o nosso `IntentService` que irá processar [inovadores token do GCM Olá](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e [registo no hub de notificação de Olá](notification-hubs-push-notification-registration-management.md).
   
    Utilize Olá seguinte código para esta classe.
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. No seu `MainActivity` classe, adicione o seguinte Olá `import` declarações acima Olá declaração de classe.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Adicione Olá seguintes membros privados na parte superior de Olá da classe de Olá. Utilizaremos estes [verificar a disponibilidade de Olá de serviços Google Play, tal como recomendado pela Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. No seu `MainActivity` classe, adicione Olá seguir disponibilidade toohello de método de serviços Google Play. 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. No seu `MainActivity` classe, adicione o seguinte código que irá verificar serviços do Google Play antes de chamar de Olá sua `IntentService` tooget o token de registo do GCM e registar o notification hub.
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. No Olá `OnCreate` método de Olá `MainActivity` classe, adicione Olá seguir o processo de registo do código toostart Olá quando é criada a atividade.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Adicione estes métodos adicionais toohello `MainActivity` tooverify estado e o relatório de estado de aplicações na sua aplicação.
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. Olá `ToastNotify` método utiliza Olá *"Olá mundo"* `TextView` controlar tooreport estado e as notificações de forma permanente na aplicação Olá. No seu ctivity_main.XML esquema, adicione Olá id para esse controlo seguinte.
   
       android:id="@+id/text_hello"
9. Em seguida, será adicionada uma subclasse do nosso recetor que definimos no AndroidManifest.xml de Olá. Adicionar outro projeto de tooyour de classe nova denominado `MyHandler`.
10. Adicionar Olá seguir instruções de importação na parte superior Olá `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. Adicione o seguinte código para Olá de Olá `MyHandler` classe, tornando-a numa subclasse de `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Este código substitui Olá `OnReceive` método, pelo que Olá processador comunique as notificações que são recebidas. processador de Olá também envia o Gestor de notificações Android de toohello de notificação push Olá utilizando Olá `sendNotification()` método. Olá `sendNotification()` método deve ser executado quando a aplicação Olá não está em execução e receber uma notificação.
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. No Android Studio, na barra de menus Olá, clique em **criar** > **reconstruir projeto** toomake certificar-se de que não existem erros no seu código.

## <a name="sending-push-notifications"></a>Enviar notificações push
Pode testar a receção de notificações push na sua aplicação, enviando-as através de Olá [Portal do Azure] -procurar Olá **resolução de problemas** secção no painel do hub de Olá, conforme mostrado abaixo.

![Notification Hubs do Azure – Teste de Envio](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>(Opcional) Enviar notificações push diretamente a partir da aplicação Olá
Normalmente, enviaria notificações através de um servidor de backend. Em alguns casos, pode querer toobe toosend capaz de notificações de push diretamente a partir da aplicação de cliente Olá. Esta secção explica como toosend notificações do cliente de Olá utilizando Olá [API de REST de Hub de notificação do Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).

1. Na vista de projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **esquema**. Abra Olá `activity_main.xml` esquema do ficheiro e clique em Olá **texto** separador tooupdate Olá conteúdo de texto Olá ficheiro. A atualização com o código de Olá abaixo, que adiciona novos `Button` e `EditText` controlos para o envio de push hub de notificação de toohello de mensagens de notificação. Adicione este código na parte inferior do Olá, imediatamente antes `</RelativeLayout>`.
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. Na vista de projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **valores**. Abra Olá `strings.xml` de ficheiros e adicione valores de cadeia de Olá que são referenciados pelo novo Olá `Button` e `EditText` controlos. Adicione-os na parte inferior de Olá ficheiro Olá, imediatamente antes `</resources>`.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. No seu `NotificationSetting.java` ficheiro, adicione Olá seguinte definição toohello `NotificationSettings` classe.
   
    Atualização `HubFullAccess` com Olá **DefaultFullSharedAccessSignature** cadeia de ligação para o seu hub. Esta cadeia de ligação pode ser copiada do Olá [Portal do Azure] clicando **políticas de acesso** no Olá **definições** painel do hub de notificação.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. No seu `MainActivity.java` ficheiro, adicione o seguinte Olá `import` declarações acima Olá `MainActivity` classe.
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. No seu `MainActivity.java` ficheiro, adicione Olá seguintes membros, Olá parte superior do Olá `MainActivity` classe.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Tem de criar um hub de notificação do POST pedido toosend mensagens tooyour um tooauthenticate de token de assinatura de acesso de Software (SaS). Isto é efetuado pela análise Olá dados-chave da cadeia de ligação de Olá e, em seguida, criar Olá SaS token, tal como mencionado na Olá [conceitos comuns](http://msdn.microsoft.com/library/azure/dn495627.aspx) referência da REST API. Olá seguinte código é uma implementação de exemplo.
   
    No `MainActivity.java`, adicionar Olá seguinte método toohello `MainActivity` classe tooparse a cadeia de ligação.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. No `MainActivity.java`, adicionar Olá seguinte método toohello `MainActivity` classe toocreate um token de autenticação SaS.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. No `MainActivity.java`, adicionar Olá seguinte método toohello `MainActivity` Olá toohandle de classe **Enviar notificação** botão clique e enviar notificação de push de Olá hub toohello de mensagem utilizando Olá API REST incorporada.
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a>Testar a aplicação
#### <a name="push-notifications-in-hello-emulator"></a>Notificações push no emulador Olá
Se pretender que as notificações de push tootest dentro de um emulador, certifique-se de que a imagem do emulador suporta o nível da API de Google Olá que escolheu para a sua aplicação. Se a imagem não suportar as APIs nativas da Google, irá surgir com Olá **serviço\_não\_disponível** exceção.

Além disso toohello acima, certifique-se de que adicionou o tooyour de conta Google a executar o emulador em **definições** > **contas**. Caso contrário, o tooregister tentativas com o GCM pode resultar em Olá **autenticação\_falha** exceção.

#### <a name="running-hello-application"></a>Execução da aplicação Olá
1. Execute a aplicação Olá e tenha em atenção que o ID de registo Olá é comunicada para um registo com êxito.
   
      ![Teste no Android - registo de canal][18]
2. Introduza um toobe de mensagem de notificação enviado tooall dispositivos Android que registou hub Olá.
   
      ![Teste no Android - enviar uma mensagem][19]

3. Prima **Enviar notificação**. Todos os dispositivos que tenham a execução de aplicação Olá mostram um `AlertDialog` instância com a mensagem de notificação push Olá. Dispositivos que não têm a execução de aplicação Olá, mas foram anteriormente registados para notificações push irão receber uma notificação no Olá Android Notification Manager. Estas serão visualizadas ao percorrer para baixo a partir do canto superior esquerdo de Olá.
   
      ![Teste no Android - notificações][21]

## <a name="next-steps"></a>Passos seguintes
Recomendamos Olá [utilizar Notification Hubs toopush notificações toousers] tutorial como passo seguinte Olá. Irá mostrar como toosend notificações de um back-end ASP.NET utilizando etiquetas tootarget de utilizadores específicos.

Se quiser toosegment os seus utilizadores por grupos de interesses, consulte Olá [toosend utilizar Notification Hubs notícias de última hora] tutorial.

toolearn informações mais gerais sobre Notification Hubs, consulte a nossa [documentação de orientação dos Notification Hubs].

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[documentação de orientação dos Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[utilizar Notification Hubs toopush notificações toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend utilizar Notification Hubs notícias de última hora]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Portal do Azure]: https://portal.azure.com
