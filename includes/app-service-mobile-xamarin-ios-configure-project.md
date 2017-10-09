#### <a name="configure-hello-ios-project-in-xamarin-studio"></a><span data-ttu-id="e2039-101">Configurar o projeto do iOS Olá no Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="e2039-101">Configure hello iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="e2039-102">No Xamarin.Studio, abra **Info. plist**e atualização Olá **identificador de pacote** com Olá agrupar ID que criou anteriormente com o ID de aplicação nova.</span><span class="sxs-lookup"><span data-stu-id="e2039-102">In Xamarin.Studio, open **Info.plist**, and update hello **Bundle Identifier** with hello bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="e2039-103">Desloque para baixo demasiado**modos em segundo plano**.</span><span class="sxs-lookup"><span data-stu-id="e2039-103">Scroll down too**Background Modes**.</span></span> <span data-ttu-id="e2039-104">Selecione Olá **ativar modos de em segundo plano** caixa e Olá **notificações remotas** caixa.</span><span class="sxs-lookup"><span data-stu-id="e2039-104">Select hello **Enable Background Modes** box and hello **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="e2039-105">Faça duplo clique em projeto no Olá solução painel tooopen **opções do projeto**.</span><span class="sxs-lookup"><span data-stu-id="e2039-105">Double-click your project in hello Solution Panel tooopen **Project Options**.</span></span>
4. <span data-ttu-id="e2039-106">Em **criar**, escolha **iOS assinatura do pacote**e selecione Olá identidade correspondente e perfil de aprovisionamento acabou de configurar para este projeto.</span><span class="sxs-lookup"><span data-stu-id="e2039-106">Under **Build**, choose **iOS Bundle Signing**, and select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="e2039-107">Isto garante que projeto Olá utiliza o novo perfil de Olá para assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="e2039-107">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="e2039-108">Para Olá oficial Xamarin aprovisionamento de dispositivos documentação, consulte [aprovisionamento de dispositivos de Xamarin].</span><span class="sxs-lookup"><span data-stu-id="e2039-108">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-hello-ios-project-in-visual-studio"></a><span data-ttu-id="e2039-109">Configurar o projeto do iOS Olá no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e2039-109">Configure hello iOS project in Visual Studio</span></span>
1. <span data-ttu-id="e2039-110">No Visual Studio, clique no projeto Olá e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e2039-110">In Visual Studio, right-click hello project, and then click **Properties**.</span></span>
2. <span data-ttu-id="e2039-111">Nas páginas de propriedades de Olá, clique em Olá **iOS aplicação** separador e atualização Olá **identificador** com o ID de Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e2039-111">In hello properties pages, click hello **iOS Application** tab, and update hello **Identifier** with hello ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="e2039-112">No Olá **iOS assinatura do pacote** separador identidade correspondente Olá selecione e aprovisionamento de conjunto de perfis apenas cópias de segurança para este projeto.</span><span class="sxs-lookup"><span data-stu-id="e2039-112">In hello **iOS Bundle Signing** tab, select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="e2039-113">Isto garante que projeto Olá utiliza o novo perfil de Olá para assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="e2039-113">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="e2039-114">Para Olá oficial Xamarin aprovisionamento de dispositivos documentação, consulte [aprovisionamento de dispositivos de Xamarin].</span><span class="sxs-lookup"><span data-stu-id="e2039-114">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="e2039-115">Faça duplo clique em ficheiro info. plist tooopen-lo e, em seguida, ativar **RemoteNotifications** em **modos em segundo plano**.</span><span class="sxs-lookup"><span data-stu-id="e2039-115">Double-click Info.plist tooopen it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[aprovisionamento de dispositivos de Xamarin]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
