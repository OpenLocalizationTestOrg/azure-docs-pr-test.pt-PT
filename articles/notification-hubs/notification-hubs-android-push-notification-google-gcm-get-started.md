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
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="b5266-104">Enviar tooAndroid de notificações push com Notification Hubs do Azure</span><span class="sxs-lookup"><span data-stu-id="b5266-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="b5266-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="b5266-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b5266-106">Este tópico demonstra as notificações push com o Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="b5266-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="b5266-107">Se estiver a utilizar Firebase Cloud Messaging (FCM da Google), consulte o artigo [Sending tooAndroid de notificações push com Notification Hubs do Azure e FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b5266-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="b5266-108">Este tutorial mostra como toouse Notification Hubs do Azure toosend push aplicação Android de tooan de notificações.</span><span class="sxs-lookup"><span data-stu-id="b5266-108">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="b5266-109">Irá criar uma aplicação em branco com Android que recebe notificações push através do Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="b5266-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="b5266-110">código de Olá concluída para este tutorial pode ser transferido a partir do GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="b5266-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5266-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b5266-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b5266-112">toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5266-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="b5266-113">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="b5266-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b5266-114">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="b5266-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="b5266-115">Além disso conta ativa do Azure tooan mencionado acima, este tutorial só requer a versão mais recente do Olá do [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="b5266-115">In addition tooan active Azure account mentioned above, this tutorial only requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="b5266-116">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais de Notification Hubs para aplicações com Android.</span><span class="sxs-lookup"><span data-stu-id="b5266-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="b5266-117">Criar um projeto que suporte o Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="b5266-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="b5266-118">Configurar um novo Notification Hub</span><span class="sxs-lookup"><span data-stu-id="b5266-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="b5266-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="b5266-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="b5266-120">No Olá **definições** painel, selecione **serviços de notificação** e, em seguida, **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="b5266-120">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="b5266-121">Introduza a chave de Olá API e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="b5266-121">Enter hello API key and click **Save**.</span></span>

&emsp;&emsp;![Notification Hubs do Azure – Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="b5266-123">O notification hub está agora configurado toowork com o GCM e tem as cadeias de ligação do Olá tooboth registar a sua tooreceive de aplicação e enviar notificações push.</span><span class="sxs-lookup"><span data-stu-id="b5266-123">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="b5266-124"><a id="connecting-app"></a>Ligar o seu hub de notificação de toohello de aplicação</span><span class="sxs-lookup"><span data-stu-id="b5266-124"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="b5266-125">Criar um novo projeto Android</span><span class="sxs-lookup"><span data-stu-id="b5266-125">Create a new Android project</span></span>
1. <span data-ttu-id="b5266-126">No Android Studio, inicie um novo projeto de Android Studio.</span><span class="sxs-lookup"><span data-stu-id="b5266-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio - novo projeto][13]
2. <span data-ttu-id="b5266-128">Escolha Olá **telefone e Tablet** formam factor e Olá **SDK mínimo** que pretende que o toosupport.</span><span class="sxs-lookup"><span data-stu-id="b5266-128">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="b5266-129">Clique depois em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="b5266-129">Then click **Next**.</span></span>
   
   ![Android Studio – fluxo de trabalho da criação do projeto][14]
3. <span data-ttu-id="b5266-131">Escolha **atividade vazia** para a atividade principal Olá, clique em **seguinte**e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="b5266-131">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="b5266-132">Adicione o projeto de toohello de serviços do Google Play</span><span class="sxs-lookup"><span data-stu-id="b5266-132">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="b5266-133">Adicionar bibliotecas dos Notification Hubs do Azure</span><span class="sxs-lookup"><span data-stu-id="b5266-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="b5266-134">No Olá `Build.Gradle` ficheiro para Olá **aplicação**, adicionar Olá seguintes linhas no Olá **dependências** secção.</span><span class="sxs-lookup"><span data-stu-id="b5266-134">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="b5266-135">Adicionar Olá seguir repositório após Olá **dependências** secção.</span><span class="sxs-lookup"><span data-stu-id="b5266-135">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="b5266-136">A atualizar Olá AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="b5266-136">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="b5266-137">toosupport GCM, temos de implementar um serviço de escuta de ID de instância no nosso código que é utilizado demasiado[obter os tokens de registo](https://developers.google.com/cloud-messaging/android/client#sample-register) utilizando [API de ID de instância da Google](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="b5266-137">toosupport GCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="b5266-138">Neste tutorial, iremos designar a classe de Olá `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="b5266-138">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="b5266-139">Adicionar Olá seguinte serviço definição toohello ficheiro AndroidManifest.xml, no interior Olá `<application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="b5266-139">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="b5266-140">Substitua Olá `<your package>` Olá de marcador de posição com o nome do seu pacote real indicado no topo de Olá da Olá `AndroidManifest.xml` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b5266-140">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="b5266-141">Depois de receber o nosso token de registo do GCM de Olá API da ID de instância, vamos utilizá-lo demasiado[registar Olá Notification Hub do Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="b5266-141">Once we have received our GCM registration token from hello Instance ID API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="b5266-142">Iremos suportar este registo em segundo plano, Olá utilizando um `IntentService` denominado `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="b5266-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="b5266-143">Este serviço também será responsável por [atualizar o nosso token de registo do GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="b5266-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="b5266-144">Adicionar Olá seguinte serviço definição toohello ficheiro AndroidManifest.xml, no interior Olá `<application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="b5266-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="b5266-145">Substitua Olá `<your package>` Olá de marcador de posição com o nome do seu pacote real indicado no topo de Olá da Olá `AndroidManifest.xml` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b5266-145">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="b5266-146">Iremos também definir notificações de tooreceive um recetor.</span><span class="sxs-lookup"><span data-stu-id="b5266-146">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="b5266-147">Adicionar Olá seguir recetor definição toohello ficheiro AndroidManifest.xml, no interior Olá `<application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="b5266-147">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="b5266-148">Substitua Olá `<your package>` Olá de marcador de posição com o nome do seu pacote real indicado no topo de Olá da Olá `AndroidManifest.xml` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b5266-148">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="b5266-149">Adicionar Olá GCM necessário os seguintes relacionados com permissões abaixo Olá `</application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="b5266-149">Add hello following necessary GCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="b5266-150">Certifique-se de que tooreplace `<your package>` com nome de pacote de Olá indicado no topo de Olá da Olá `AndroidManifest.xml` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b5266-150">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="b5266-151">Para obter mais informações sobre estas permissões, consulte o artigo [Configurar uma aplicação de cliente do GCM para Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span><span class="sxs-lookup"><span data-stu-id="b5266-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="b5266-152">Adicionar código</span><span class="sxs-lookup"><span data-stu-id="b5266-152">Adding code</span></span>
1. <span data-ttu-id="b5266-153">Na vista de projeto Olá, expanda **aplicação** > **src** > **principal** > **java**.</span><span class="sxs-lookup"><span data-stu-id="b5266-153">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="b5266-154">Com o botão direito do rato, clique na pasta do pacote por baixo de **java**, clique em **Nova**, e, em seguida, clique em **Classe Java**.</span><span class="sxs-lookup"><span data-stu-id="b5266-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="b5266-155">Adicione uma nova classe com o nome `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="b5266-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - nova classe Java][6]
   
    <span data-ttu-id="b5266-157">Certifique-se tooupdate Olá estes três marcadores de posição no seguinte código para Olá de Olá `NotificationSettings` classe:</span><span class="sxs-lookup"><span data-stu-id="b5266-157">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="b5266-158">**SenderId**: Olá número do projeto que obteve anteriormente no Olá [Google Cloud Console](http://cloud.google.com/console).</span><span class="sxs-lookup"><span data-stu-id="b5266-158">**SenderId**: hello project number you obtained earlier in hello [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="b5266-159">**HubListenConnectionString**: Olá **DefaultListenAccessSignature** cadeia de ligação para o seu hub.</span><span class="sxs-lookup"><span data-stu-id="b5266-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="b5266-160">Pode copiar essa cadeia de ligação ao clicar em **políticas de acesso** no Olá **definições** painel do seu hub no Olá [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="b5266-160">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="b5266-161">**HubName**: Utilize o nome de Olá do notification hub que aparece no painel do hub de Olá no Olá [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="b5266-161">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="b5266-162">Código `NotificationSettings`:</span><span class="sxs-lookup"><span data-stu-id="b5266-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="b5266-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="b5266-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="b5266-164">}</span><span class="sxs-lookup"><span data-stu-id="b5266-164">}</span></span>
2. <span data-ttu-id="b5266-165">Utilizando os passos de Olá acima, adicione outra nova classe com o nome `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="b5266-165">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="b5266-166">Esta será a nossa implementação do serviço de escuta de ID da instância.</span><span class="sxs-lookup"><span data-stu-id="b5266-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="b5266-167">Olá código para esta classe irá chamar nosso `IntentService` demasiado[token do GCM atualização Olá](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) em segundo plano de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5266-167">hello code for this class will call our `IntentService` too[refresh hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
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


1. <span data-ttu-id="b5266-168">Adicione outra nova classe tooyour projeto com o nome, `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="b5266-168">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="b5266-169">Esta será Olá implementação para o nosso `IntentService` que irá processar [inovadores token do GCM Olá](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e [registo no hub de notificação de Olá](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="b5266-169">This will be hello implementation for our `IntentService` that will handle [refreshing hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="b5266-170">Utilize Olá seguinte código para esta classe.</span><span class="sxs-lookup"><span data-stu-id="b5266-170">Use hello following code for this class.</span></span>
   
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
2. <span data-ttu-id="b5266-171">No seu `MainActivity` classe, adicione o seguinte Olá `import` declarações acima Olá declaração de classe.</span><span class="sxs-lookup"><span data-stu-id="b5266-171">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="b5266-172">Adicione Olá seguintes membros privados na parte superior de Olá da classe de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5266-172">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="b5266-173">Utilizaremos estes [verificar a disponibilidade de Olá de serviços Google Play, tal como recomendado pela Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="b5266-173">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="b5266-174">No seu `MainActivity` classe, adicione Olá seguir disponibilidade toohello de método de serviços Google Play.</span><span class="sxs-lookup"><span data-stu-id="b5266-174">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
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
5. <span data-ttu-id="b5266-175">No seu `MainActivity` classe, adicione o seguinte código que irá verificar serviços do Google Play antes de chamar de Olá sua `IntentService` tooget o token de registo do GCM e registar o notification hub.</span><span class="sxs-lookup"><span data-stu-id="b5266-175">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="b5266-176">No Olá `OnCreate` método de Olá `MainActivity` classe, adicione Olá seguir o processo de registo do código toostart Olá quando é criada a atividade.</span><span class="sxs-lookup"><span data-stu-id="b5266-176">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="b5266-177">Adicione estes métodos adicionais toohello `MainActivity` tooverify estado e o relatório de estado de aplicações na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="b5266-177">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="b5266-178">Olá `ToastNotify` método utiliza Olá *"Olá mundo"* `TextView` controlar tooreport estado e as notificações de forma permanente na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="b5266-178">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="b5266-179">No seu ctivity_main.XML esquema, adicione Olá id para esse controlo seguinte.</span><span class="sxs-lookup"><span data-stu-id="b5266-179">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="b5266-180">Em seguida, será adicionada uma subclasse do nosso recetor que definimos no AndroidManifest.xml de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5266-180">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="b5266-181">Adicionar outro projeto de tooyour de classe nova denominado `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="b5266-181">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="b5266-182">Adicionar Olá seguir instruções de importação na parte superior Olá `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="b5266-182">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="b5266-183">Adicione o seguinte código para Olá de Olá `MyHandler` classe, tornando-a numa subclasse de `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="b5266-183">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="b5266-184">Este código substitui Olá `OnReceive` método, pelo que Olá processador comunique as notificações que são recebidas.</span><span class="sxs-lookup"><span data-stu-id="b5266-184">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="b5266-185">processador de Olá também envia o Gestor de notificações Android de toohello de notificação push Olá utilizando Olá `sendNotification()` método.</span><span class="sxs-lookup"><span data-stu-id="b5266-185">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="b5266-186">Olá `sendNotification()` método deve ser executado quando a aplicação Olá não está em execução e receber uma notificação.</span><span class="sxs-lookup"><span data-stu-id="b5266-186">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="b5266-187">No Android Studio, na barra de menus Olá, clique em **criar** > **reconstruir projeto** toomake certificar-se de que não existem erros no seu código.</span><span class="sxs-lookup"><span data-stu-id="b5266-187">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="b5266-188">Enviar notificações push</span><span class="sxs-lookup"><span data-stu-id="b5266-188">Sending push notifications</span></span>
<span data-ttu-id="b5266-189">Pode testar a receção de notificações push na sua aplicação, enviando-as através de Olá [Portal do Azure] -procurar Olá **resolução de problemas** secção no painel do hub de Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="b5266-189">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Notification Hubs do Azure – Teste de Envio](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="b5266-191">(Opcional) Enviar notificações push diretamente a partir da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="b5266-191">(Optional) Send push notifications directly from hello app</span></span>
<span data-ttu-id="b5266-192">Normalmente, enviaria notificações através de um servidor de backend.</span><span class="sxs-lookup"><span data-stu-id="b5266-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="b5266-193">Em alguns casos, pode querer toobe toosend capaz de notificações de push diretamente a partir da aplicação de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="b5266-193">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="b5266-194">Esta secção explica como toosend notificações do cliente de Olá utilizando Olá [API de REST de Hub de notificação do Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5266-194">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="b5266-195">Na vista de projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **esquema**.</span><span class="sxs-lookup"><span data-stu-id="b5266-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="b5266-196">Abra Olá `activity_main.xml` esquema do ficheiro e clique em Olá **texto** separador tooupdate Olá conteúdo de texto Olá ficheiro.</span><span class="sxs-lookup"><span data-stu-id="b5266-196">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="b5266-197">A atualização com o código de Olá abaixo, que adiciona novos `Button` e `EditText` controlos para o envio de push hub de notificação de toohello de mensagens de notificação.</span><span class="sxs-lookup"><span data-stu-id="b5266-197">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="b5266-198">Adicione este código na parte inferior do Olá, imediatamente antes `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="b5266-198">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="b5266-199">Na vista de projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **valores**.</span><span class="sxs-lookup"><span data-stu-id="b5266-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="b5266-200">Abra Olá `strings.xml` de ficheiros e adicione valores de cadeia de Olá que são referenciados pelo novo Olá `Button` e `EditText` controlos.</span><span class="sxs-lookup"><span data-stu-id="b5266-200">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="b5266-201">Adicione-os na parte inferior de Olá ficheiro Olá, imediatamente antes `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="b5266-201">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="b5266-202">No seu `NotificationSetting.java` ficheiro, adicione Olá seguinte definição toohello `NotificationSettings` classe.</span><span class="sxs-lookup"><span data-stu-id="b5266-202">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="b5266-203">Atualização `HubFullAccess` com Olá **DefaultFullSharedAccessSignature** cadeia de ligação para o seu hub.</span><span class="sxs-lookup"><span data-stu-id="b5266-203">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="b5266-204">Esta cadeia de ligação pode ser copiada do Olá [Portal do Azure] clicando **políticas de acesso** no Olá **definições** painel do hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="b5266-204">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="b5266-205">No seu `MainActivity.java` ficheiro, adicione o seguinte Olá `import` declarações acima Olá `MainActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="b5266-205">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="b5266-206">No seu `MainActivity.java` ficheiro, adicione Olá seguintes membros, Olá parte superior do Olá `MainActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="b5266-206">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="b5266-207">Tem de criar um hub de notificação do POST pedido toosend mensagens tooyour um tooauthenticate de token de assinatura de acesso de Software (SaS).</span><span class="sxs-lookup"><span data-stu-id="b5266-207">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="b5266-208">Isto é efetuado pela análise Olá dados-chave da cadeia de ligação de Olá e, em seguida, criar Olá SaS token, tal como mencionado na Olá [conceitos comuns](http://msdn.microsoft.com/library/azure/dn495627.aspx) referência da REST API.</span><span class="sxs-lookup"><span data-stu-id="b5266-208">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="b5266-209">Olá seguinte código é uma implementação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b5266-209">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="b5266-210">No `MainActivity.java`, adicionar Olá seguinte método toohello `MainActivity` classe tooparse a cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="b5266-210">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
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
7. <span data-ttu-id="b5266-211">No `MainActivity.java`, adicionar Olá seguinte método toohello `MainActivity` classe toocreate um token de autenticação SaS.</span><span class="sxs-lookup"><span data-stu-id="b5266-211">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
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
8. <span data-ttu-id="b5266-212">No `MainActivity.java`, adicionar Olá seguinte método toohello `MainActivity` Olá toohandle de classe **Enviar notificação** botão clique e enviar notificação de push de Olá hub toohello de mensagem utilizando Olá API REST incorporada.</span><span class="sxs-lookup"><span data-stu-id="b5266-212">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
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

## <a name="testing-your-app"></a><span data-ttu-id="b5266-213">Testar a aplicação</span><span class="sxs-lookup"><span data-stu-id="b5266-213">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="b5266-214">Notificações push no emulador Olá</span><span class="sxs-lookup"><span data-stu-id="b5266-214">Push notifications in hello emulator</span></span>
<span data-ttu-id="b5266-215">Se pretender que as notificações de push tootest dentro de um emulador, certifique-se de que a imagem do emulador suporta o nível da API de Google Olá que escolheu para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="b5266-215">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="b5266-216">Se a imagem não suportar as APIs nativas da Google, irá surgir com Olá **serviço\_não\_disponível** exceção.</span><span class="sxs-lookup"><span data-stu-id="b5266-216">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="b5266-217">Além disso toohello acima, certifique-se de que adicionou o tooyour de conta Google a executar o emulador em **definições** > **contas**.</span><span class="sxs-lookup"><span data-stu-id="b5266-217">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="b5266-218">Caso contrário, o tooregister tentativas com o GCM pode resultar em Olá **autenticação\_falha** exceção.</span><span class="sxs-lookup"><span data-stu-id="b5266-218">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="b5266-219">Execução da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="b5266-219">Running hello application</span></span>
1. <span data-ttu-id="b5266-220">Execute a aplicação Olá e tenha em atenção que o ID de registo Olá é comunicada para um registo com êxito.</span><span class="sxs-lookup"><span data-stu-id="b5266-220">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
      ![Teste no Android - registo de canal][18]
2. <span data-ttu-id="b5266-222">Introduza um toobe de mensagem de notificação enviado tooall dispositivos Android que registou hub Olá.</span><span class="sxs-lookup"><span data-stu-id="b5266-222">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
      ![Teste no Android - enviar uma mensagem][19]

3. <span data-ttu-id="b5266-224">Prima **Enviar notificação**.</span><span class="sxs-lookup"><span data-stu-id="b5266-224">Press **Send Notification**.</span></span> <span data-ttu-id="b5266-225">Todos os dispositivos que tenham a execução de aplicação Olá mostram um `AlertDialog` instância com a mensagem de notificação push Olá.</span><span class="sxs-lookup"><span data-stu-id="b5266-225">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="b5266-226">Dispositivos que não têm a execução de aplicação Olá, mas foram anteriormente registados para notificações push irão receber uma notificação no Olá Android Notification Manager.</span><span class="sxs-lookup"><span data-stu-id="b5266-226">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="b5266-227">Estas serão visualizadas ao percorrer para baixo a partir do canto superior esquerdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5266-227">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
      ![Teste no Android - notificações][21]

## <a name="next-steps"></a><span data-ttu-id="b5266-229">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b5266-229">Next steps</span></span>
<span data-ttu-id="b5266-230">Recomendamos Olá [utilizar Notification Hubs toopush notificações toousers] tutorial como passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="b5266-230">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="b5266-231">Irá mostrar como toosend notificações de um back-end ASP.NET utilizando etiquetas tootarget de utilizadores específicos.</span><span class="sxs-lookup"><span data-stu-id="b5266-231">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="b5266-232">Se quiser toosegment os seus utilizadores por grupos de interesses, consulte Olá [toosend utilizar Notification Hubs notícias de última hora] tutorial.</span><span class="sxs-lookup"><span data-stu-id="b5266-232">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="b5266-233">toolearn informações mais gerais sobre Notification Hubs, consulte a nossa [documentação de orientação dos Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="b5266-233">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

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
