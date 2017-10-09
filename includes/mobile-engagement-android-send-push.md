
### <a name="update-manifest-file-tooenable-notifications"></a>Atualizar o ficheiro de manifesto tooenable notificações
Copiar recursos de mensagens na aplicação Olá abaixo no Manifest.xml entre Olá `<application>` e `</application>` etiquetas.

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

### <a name="specify-an-icon-for-notifications"></a>Especificar um ícone para as notificações
Olá colar seguinte fragmento XML no Manifest.xml entre Olá `<application>` e `</application>` etiquetas.

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

Isto define o ícone de Olá que é apresentado no sistema e nas notificações na aplicação. É opcional para as notificações na aplicação, mas é obrigatório para as notificações do sistema. O Android rejeitará as notificações do sistema com ícones inválidos.

Certifique-se de que está a utilizar um ícone que existe dos Olá **drawable** pastas (como ``engagement_close.png``). A pasta **mipmap** não é suportada.

> [!NOTE]
> Não deve utilizar Olá **iniciador** ícone. Tem uma resolução diferente e está normalmente nas pastas mipmap Olá, que não é suportada.
> 
> 

Para aplicações reais, pode utilizar um ícone que seja adequado para as notificações de acordo com as [Diretrizes de conceção do Android](http://developer.android.com/design/patterns/notifications.html).

> [!TIP]
> toobe toouse se correto resoluções de ícones, pode examinar [estes exemplos](https://www.google.com/design/icons).
> Desloque para baixo toohello **notificação** secção, clique num ícone e, em seguida, clique em `PNGS` conjunto de desenho toodownload Olá ícone. Pode ver que pastas drawable e com que toouse de resolução para cada versão do ícone de Olá.
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>Ativar as notificações de push do GCM tooreceive da aplicação
1. Cole o seguinte Olá no Manifest.xml entre Olá `<application>` e `</application>` etiquetas depois de substituir Olá **ID do remetente** obtidos a partir da consola de projeto Firebase. Olá \n é intencional, por isso, certifique-se de que termina Olá número do projeto com-lo.
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Cole o código de Olá abaixo no Manifest.xml entre Olá `<application>` e `</application>` etiquetas. Substitua o nome do pacote Olá <Your package name>.
   
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
3. Adicionar o último conjunto de Olá de permissões que estão realçadas antes Olá `<application>` etiquetas. Substitua `<Your package name>` pelo nome do pacote real Olá da sua aplicação.
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

