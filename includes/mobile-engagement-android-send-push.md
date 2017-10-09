
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="da9ce-101">Atualizar o ficheiro de manifesto tooenable notificações</span><span class="sxs-lookup"><span data-stu-id="da9ce-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="da9ce-102">Copiar recursos de mensagens na aplicação Olá abaixo no Manifest.xml entre Olá `<application>` e `</application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="da9ce-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="da9ce-103">Especificar um ícone para as notificações</span><span class="sxs-lookup"><span data-stu-id="da9ce-103">Specify an icon for notifications</span></span>
<span data-ttu-id="da9ce-104">Olá colar seguinte fragmento XML no Manifest.xml entre Olá `<application>` e `</application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="da9ce-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="da9ce-105">Isto define o ícone de Olá que é apresentado no sistema e nas notificações na aplicação.</span><span class="sxs-lookup"><span data-stu-id="da9ce-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="da9ce-106">É opcional para as notificações na aplicação, mas é obrigatório para as notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="da9ce-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="da9ce-107">O Android rejeitará as notificações do sistema com ícones inválidos.</span><span class="sxs-lookup"><span data-stu-id="da9ce-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="da9ce-108">Certifique-se de que está a utilizar um ícone que existe dos Olá **drawable** pastas (como ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="da9ce-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="da9ce-109">A pasta **mipmap** não é suportada.</span><span class="sxs-lookup"><span data-stu-id="da9ce-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="da9ce-110">Não deve utilizar Olá **iniciador** ícone.</span><span class="sxs-lookup"><span data-stu-id="da9ce-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="da9ce-111">Tem uma resolução diferente e está normalmente nas pastas mipmap Olá, que não é suportada.</span><span class="sxs-lookup"><span data-stu-id="da9ce-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="da9ce-112">Para aplicações reais, pode utilizar um ícone que seja adequado para as notificações de acordo com as [Diretrizes de conceção do Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="da9ce-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="da9ce-113">toobe toouse se correto resoluções de ícones, pode examinar [estes exemplos](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="da9ce-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="da9ce-114">Desloque para baixo toohello **notificação** secção, clique num ícone e, em seguida, clique em `PNGS` conjunto de desenho toodownload Olá ícone.</span><span class="sxs-lookup"><span data-stu-id="da9ce-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="da9ce-115">Pode ver que pastas drawable e com que toouse de resolução para cada versão do ícone de Olá.</span><span class="sxs-lookup"><span data-stu-id="da9ce-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="da9ce-116">Ativar as notificações de push do GCM tooreceive da aplicação</span><span class="sxs-lookup"><span data-stu-id="da9ce-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="da9ce-117">Cole o seguinte Olá no Manifest.xml entre Olá `<application>` e `</application>` etiquetas depois de substituir Olá **ID do remetente** obtidos a partir da consola de projeto Firebase.</span><span class="sxs-lookup"><span data-stu-id="da9ce-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="da9ce-118">Olá \n é intencional, por isso, certifique-se de que termina Olá número do projeto com-lo.</span><span class="sxs-lookup"><span data-stu-id="da9ce-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="da9ce-119">Cole o código de Olá abaixo no Manifest.xml entre Olá `<application>` e `</application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="da9ce-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="da9ce-120">Substitua o nome do pacote Olá <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="da9ce-120">Replace hello package name <Your package name>.</span></span>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. <span data-ttu-id="da9ce-121">Adicionar o último conjunto de Olá de permissões que estão realçadas antes Olá `<application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="da9ce-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="da9ce-122">Substitua `<Your package name>` pelo nome do pacote real Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="da9ce-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

