1. Olá abra o Gestor do Android SDK clicando Olá ícone na barra de ferramentas de Olá do Android Studio ou ao clicar em **ferramentas** -> **Android** -> **SDK Manager**no menu de Olá. Localizar a versão de destino Olá do Olá Android SDK utilizada no seu projeto, abra-o ao clicar em **Mostrar detalhes do pacote**e escolha **Google APIs**, se não estiver já instalado.
2. Clique em Olá **ferramentas do SDK** separador. Se ainda não instalou o Serviço do Google Play, clique em **Serviços do Google Play**, como mostrado abaixo. Em seguida, clique em **aplicar** tooinstall. 
   
    Tenha em atenção o caminho do SDK Olá, para utilização num passo posterior. 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. Abra Olá **gradle** ficheiro no diretório de aplicação Olá.
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. Adicione esta linha sob *dependências*: 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. Clique em Olá **sincronizar projeto com os ficheiros Gradle** ícone na barra de ferramentas de Olá.
6. Abra **AndroidManifest.xml** e adicione esta etiqueta toohello *aplicação* etiquetas.
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

