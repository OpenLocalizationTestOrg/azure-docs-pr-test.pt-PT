1. <span data-ttu-id="9c8a2-101">No seu **aplicação** projeto, o ficheiro de Olá abra `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="9c8a2-102">No código Olá em Olá junto dois passos, substitua  *`**my_app_package**`*  com o nome de Olá do pacote de aplicação Olá para o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="9c8a2-103">Este é o valor Olá Olá `package` atributo de Olá `manifest` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="9c8a2-104">Adicionar Olá as seguintes permissões de novo após Olá existente `uses-permission` elemento:</span><span class="sxs-lookup"><span data-stu-id="9c8a2-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="9c8a2-105">Adicionar Olá seguinte código após Olá `application` tag de início:</span><span class="sxs-lookup"><span data-stu-id="9c8a2-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="9c8a2-106">Ficheiro aberto Olá *ToDoActivity.java*e adicione as seguintes declarações de importação de Olá:</span><span class="sxs-lookup"><span data-stu-id="9c8a2-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="9c8a2-107">Adicione Olá seguinte classe toohello variável privada.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="9c8a2-108">Substitua  *`<PROJECT_NUMBER>`*  com o número do projeto Olá atribuído através da aplicação do Google tooyour no Olá precedente procedimento.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="9c8a2-109">Alterar a definição de Olá de *MobileServiceClient* de **privada** demasiado**estáticos públicos**, pelo que agora aspeto:</span><span class="sxs-lookup"><span data-stu-id="9c8a2-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="9c8a2-110">Adicione um novo toohandle notificações da classe.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="9c8a2-111">No Explorador de projeto, abra Olá **src** > **principal** > **java** nós e o nó de nome de pacote de Olá de contexto.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="9c8a2-112">Clique em **novo**e, em seguida, clique em **classe Java**.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="9c8a2-113">No **nome**, tipo `MyHandler`e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="9c8a2-114">No ficheiro de MyHandler Olá, substitua a declaração de classe de Olá com:</span><span class="sxs-lookup"><span data-stu-id="9c8a2-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="9c8a2-115">Adicionar Olá seguir instruções de importação para Olá `MyHandler` classe:</span><span class="sxs-lookup"><span data-stu-id="9c8a2-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="9c8a2-116">Em seguida, adicione este membro toohello `MyHandler` classe:</span><span class="sxs-lookup"><span data-stu-id="9c8a2-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="9c8a2-117">No Olá `MyHandler` classe, adicione Olá seguir Olá do código toooverride **onRegistered** método, que regista o dispositivo com o hub de notificação do Olá serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

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
       <span data-ttu-id="9c8a2-118">}</span><span class="sxs-lookup"><span data-stu-id="9c8a2-118">}</span></span>
13. <span data-ttu-id="9c8a2-119">No Olá `MyHandler` classe, adicione Olá seguir Olá do código toooverride **onReceive** método, o que faz com que Olá notificação toodisplay quando é recebido.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

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
       <span data-ttu-id="9c8a2-120">}</span><span class="sxs-lookup"><span data-stu-id="9c8a2-120">}</span></span>
14. <span data-ttu-id="9c8a2-121">No ficheiro TodoActivity.java de Olá, atualizar Olá **onCreate** método de Olá *ToDoActivity* classe de processador de notificação de Olá tooregister de classe.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="9c8a2-122">Certifique-se de que tooadd este código após Olá *MobileServiceClient* ser instanciado.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="9c8a2-123">A aplicação já está atualizado toosupport notificações de push.</span><span class="sxs-lookup"><span data-stu-id="9c8a2-123">Your app is now updated toosupport push notifications.</span></span>
