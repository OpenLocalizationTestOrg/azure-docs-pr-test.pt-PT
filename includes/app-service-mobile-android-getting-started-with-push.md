1. No seu **aplicação** projeto, o ficheiro de Olá abra `AndroidManifest.xml`. No código Olá em Olá junto dois passos, substitua  *`**my_app_package**`*  com o nome de Olá do pacote de aplicação Olá para o seu projeto. Este é o valor Olá Olá `package` atributo de Olá `manifest` etiquetas.
2. Adicionar Olá as seguintes permissões de novo após Olá existente `uses-permission` elemento:

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. Adicionar Olá seguinte código após Olá `application` tag de início:

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. Ficheiro aberto Olá *ToDoActivity.java*e adicione as seguintes declarações de importação de Olá:

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. Adicione Olá seguinte classe toohello variável privada. Substitua  *`<PROJECT_NUMBER>`*  com o número do projeto Olá atribuído através da aplicação do Google tooyour no Olá precedente procedimento.

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. Alterar a definição de Olá de *MobileServiceClient* de **privada** demasiado**estáticos públicos**, pelo que agora aspeto:

        public static MobileServiceClient mClient;
7. Adicione um novo toohandle notificações da classe. No Explorador de projeto, abra Olá **src** > **principal** > **java** nós e o nó de nome de pacote de Olá de contexto. Clique em **novo**e, em seguida, clique em **classe Java**.
8. No **nome**, tipo `MyHandler`e, em seguida, clique em **OK**.

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. No ficheiro de MyHandler Olá, substitua a declaração de classe de Olá com:

        public class MyHandler extends NotificationsHandler {
10. Adicionar Olá seguir instruções de importação para Olá `MyHandler` classe:

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. Em seguida, adicione este membro toohello `MyHandler` classe:

        public static final int NOTIFICATION_ID = 1;
12. No Olá `MyHandler` classe, adicione Olá seguir Olá do código toooverride **onRegistered** método, que regista o dispositivo com o hub de notificação do Olá serviço móvel.

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       }
13. No Olá `MyHandler` classe, adicione Olá seguir Olá do código toooverride **onReceive** método, o que faz com que Olá notificação toodisplay quando é recebido.

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       }
14. No ficheiro TodoActivity.java de Olá, atualizar Olá **onCreate** método de Olá *ToDoActivity* classe de processador de notificação de Olá tooregister de classe. Certifique-se de que tooadd este código após Olá *MobileServiceClient* ser instanciado.

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    A aplicação já está atualizado toosupport notificações de push.
