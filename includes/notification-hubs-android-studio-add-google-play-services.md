1. <span data-ttu-id="7a232-101">Olá abra o Gestor do Android SDK clicando Olá ícone na barra de ferramentas de Olá do Android Studio ou ao clicar em **ferramentas** -> **Android** -> **SDK Manager**no menu de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a232-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="7a232-102">Localizar a versão de destino Olá do Olá Android SDK utilizada no seu projeto, abra-o ao clicar em **Mostrar detalhes do pacote**e escolha **Google APIs**, se não estiver já instalado.</span><span class="sxs-lookup"><span data-stu-id="7a232-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="7a232-103">Clique em Olá **ferramentas do SDK** separador. Se ainda não instalou o Serviço do Google Play, clique em **Serviços do Google Play**, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7a232-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="7a232-104">Em seguida, clique em **aplicar** tooinstall.</span><span class="sxs-lookup"><span data-stu-id="7a232-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="7a232-105">Tenha em atenção o caminho do SDK Olá, para utilização num passo posterior.</span><span class="sxs-lookup"><span data-stu-id="7a232-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="7a232-106">Abra Olá **gradle** ficheiro no diretório de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="7a232-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="7a232-107">Adicione esta linha sob *dependências*:</span><span class="sxs-lookup"><span data-stu-id="7a232-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="7a232-108">Clique em Olá **sincronizar projeto com os ficheiros Gradle** ícone na barra de ferramentas de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a232-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="7a232-109">Abra **AndroidManifest.xml** e adicione esta etiqueta toohello *aplicação* etiquetas.</span><span class="sxs-lookup"><span data-stu-id="7a232-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

