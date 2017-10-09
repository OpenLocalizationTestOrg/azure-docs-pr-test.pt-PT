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
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="8aa1f-103">Introdução aos Notification Hubs para Aplicações Kindle</span><span class="sxs-lookup"><span data-stu-id="8aa1f-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="8aa1f-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="8aa1f-104">Overview</span></span>
<span data-ttu-id="8aa1f-105">Este tutorial mostra como toouse Notification Hubs do Azure toosend push aplicação de Kindle tooa de notificações.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="8aa1f-106">Deverá criar uma aplicação Kindle que receba notificações push através do Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="8aa1f-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8aa1f-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8aa1f-107">Prerequisites</span></span>
<span data-ttu-id="8aa1f-108">Este tutorial requer o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="8aa1f-109">Obter Olá Android SDK (partimos do princípio que utiliza o Eclipse) de Olá <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site do Android</a>.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="8aa1f-110">Siga os passos Olá <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">definição se o ambiente de desenvolvimento</a> tooset configurar o ambiente de desenvolvimento para o Kindle.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="8aa1f-111">Adicionar um novo portal de programador toohello de aplicação</span><span class="sxs-lookup"><span data-stu-id="8aa1f-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="8aa1f-112">Em primeiro lugar, criar uma aplicação no Olá [portal de programador da Amazon].</span><span class="sxs-lookup"><span data-stu-id="8aa1f-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="8aa1f-113">Olá cópia **chave da aplicação**.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="8aa1f-114">No portal de Olá, clique no nome de Olá da sua aplicação e, em seguida, clique em Olá **Device Messaging** separador.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="8aa1f-115">Clique em **Criar um Novo Perfil de Segurança** e crie um novo perfil de segurança (por exemplo, **Perfil de segurança TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="8aa1f-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="8aa1f-116">Em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="8aa1f-117">Clique em **perfis de segurança** tooview Olá segurança perfil que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="8aa1f-118">Olá cópia **ID de cliente** e **segredo do cliente** valores para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="8aa1f-119">Criar uma chave de API</span><span class="sxs-lookup"><span data-stu-id="8aa1f-119">Create an API key</span></span>
1. <span data-ttu-id="8aa1f-120">Abra uma linha de comandos com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="8aa1f-121">Navegue toohello pasta de Android SDK.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="8aa1f-122">Introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="8aa1f-123">Para Olá **keystore** palavra-passe, escreva **android**.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="8aa1f-124">Olá cópia **MD5** impressão digital.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="8aa1f-125">No portal de programador Olá, no Olá **mensagens** separador, clique em **Android/Kindle** e introduza o nome de Olá do pacote de Olá para a sua aplicação (por exemplo, **com.sample.notificationhubtest**) e Olá **MD5** valor e, em seguida, clique em **gerar a chave de API**.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="8aa1f-126">Adicionar hub toohello de credenciais</span><span class="sxs-lookup"><span data-stu-id="8aa1f-126">Add credentials toohello hub</span></span>
<span data-ttu-id="8aa1f-127">No portal de Olá, adicionar Olá cliente segredo e cliente ID toohello **configurar** separador do notification hub.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="8aa1f-128">Configurar a aplicação</span><span class="sxs-lookup"><span data-stu-id="8aa1f-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="8aa1f-129">Quando estiver a criar uma aplicação, utilize no mínimo uma API de nível 17.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="8aa1f-130">Adicione o projeto do Olá ADM bibliotecas tooyour Eclipse:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="8aa1f-131">tooobtain Olá biblioteca ADM, deverá [transferir Olá SDK].</span><span class="sxs-lookup"><span data-stu-id="8aa1f-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="8aa1f-132">Extraia o ficheiro zip do Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="8aa1f-133">No Eclipse, clique com o botão direito do rato no projeto e, em seguida, clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="8aa1f-134">Selecione **criar caminho Java** em Olá à esquerda e, em seguida, selecione de Olá * * bibliotecas * * separador na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="8aa1f-135">Clique em **adicionar Jar externo**e selecione Olá ficheiro `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` do diretório de olá onde extraiu Olá Amazon SDK.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="8aa1f-136">Transferir Olá Android SDK do NotificationHubs (ligação).</span><span class="sxs-lookup"><span data-stu-id="8aa1f-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="8aa1f-137">Deszipe o pacote Olá e, em seguida, arraste o ficheiro de Olá `notification-hubs-sdk.jar` para Olá `libs` pasta no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="8aa1f-138">Edite o toosupport manifesto de aplicação ADM:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="8aa1f-139">Adicione espaço de nomes do Olá Amazon Olá elemento raiz do manifesto:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="8aa1f-140">Adicione permissões como primeiro elemento de Olá no elemento manifesto Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="8aa1f-141">Substitute **[nome do seu pacote]** com o pacote de Olá que utilizou toocreate a aplicação.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
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
2. <span data-ttu-id="8aa1f-142">Inserir Olá seguinte elemento como o primeiro subordinado de Olá do elemento de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="8aa1f-143">Lembre-se toosubstitute **[nome do seu serviço]** com o nome do processador de mensagens ADM que criar na secção seguinte do Olá (pacote de Olá incluindo) e substitua Olá **[nome do seu pacote]** com Olá nome do pacote com a qual criou a aplicação.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
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

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="8aa1f-144">Criar o processador de mensagens ADM</span><span class="sxs-lookup"><span data-stu-id="8aa1f-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="8aa1f-145">Criar uma nova classe que herda de `com.amazon.device.messaging.ADMMessageHandlerBase` e dê-lhe nome `MyADMMessageHandler`, conforme apresentado na Olá figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="8aa1f-146">Adicione Olá seguinte `import` instruções:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="8aa1f-147">Adicione Olá seguinte código na classe de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="8aa1f-148">Não se esqueça toosubstitute Olá ligação e o nome da cadeia do hub (escutar):</span><span class="sxs-lookup"><span data-stu-id="8aa1f-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="8aa1f-149">Adicionar Olá seguinte código toohello `OnMessage()` método:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="8aa1f-150">Adicionar Olá seguinte código toohello `OnRegistered` método:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="8aa1f-151">Adicionar Olá seguinte código toohello `OnUnregistered` método:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="8aa1f-152">No Olá `MainActivity` método, adicione as seguintes declarações de importação de Olá:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="8aa1f-153">Adicionar Olá seguinte código no final Olá Olá `OnCreate` método:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="8aa1f-154">Adicionar a aplicação de tooyour chave de API</span><span class="sxs-lookup"><span data-stu-id="8aa1f-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="8aa1f-155">No Eclipse, crie um novo ficheiro designado **api_key.txt** em recursos de diretório de Olá do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="8aa1f-156">Abra Olá ficheiro e cópia Olá chave de API que gerou no portal de programador da Amazon Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="8aa1f-157">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="8aa1f-157">Run hello app</span></span>
1. <span data-ttu-id="8aa1f-158">Inicie o emulador de Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-158">Start hello emulator.</span></span>
2. <span data-ttu-id="8aa1f-159">No emulador Olá, percorra a partir da parte superior do Olá e clique em **definições**e, em seguida, clique em **minha conta** e registar uma conta válida da Amazon.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="8aa1f-160">No Eclipse, execute a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="8aa1f-161">Se ocorrer um problema, verifique a hora de Olá do emulador de Olá (ou dispositivo).</span><span class="sxs-lookup"><span data-stu-id="8aa1f-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="8aa1f-162">valor de tempo de Olá tem de ser exato.</span><span class="sxs-lookup"><span data-stu-id="8aa1f-162">hello time value must be accurate.</span></span> <span data-ttu-id="8aa1f-163">tempo de Olá toochange do emulador do Kindle Olá, pode executar Olá os seguintes comandos do diretório de ferramentas de plataforma Android SDK:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="8aa1f-164">Enviar uma mensagem</span><span class="sxs-lookup"><span data-stu-id="8aa1f-164">Send a message</span></span>
<span data-ttu-id="8aa1f-165">toosend uma mensagem com o .NET:</span><span class="sxs-lookup"><span data-stu-id="8aa1f-165">toosend a message by using .NET:</span></span>

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
