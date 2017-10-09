### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="fea7f-101">Conceda acesso tooyour certificado Push tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fea7f-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="fea7f-102">tooallow Mobile Engagement toosend notificações Push em seu nome, terá de toogrant aceder a tooyour certificado.</span><span class="sxs-lookup"><span data-stu-id="fea7f-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="fea7f-103">Isto é feito ao configurar e introduzir o certificado no portal de Mobile Engagement Olá.</span><span class="sxs-lookup"><span data-stu-id="fea7f-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="fea7f-104">Não se esqueça de obter o certificado .p12 conforme explicado na [Documentação da Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6).</span><span class="sxs-lookup"><span data-stu-id="fea7f-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="fea7f-105">Navegue tooyour portal de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fea7f-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="fea7f-106">Certifique-se de que está na Olá correto e, em seguida, clique em Olá **iniciar** botão na parte inferior de Olá:</span><span class="sxs-lookup"><span data-stu-id="fea7f-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="fea7f-107">Clique em Olá **definições** página no Portal do Engagement.</span><span class="sxs-lookup"><span data-stu-id="fea7f-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="fea7f-108">Clique na Olá **Push nativo** secção tooupload o certificado p12:</span><span class="sxs-lookup"><span data-stu-id="fea7f-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="fea7f-109">Selecione o p12, carregue-o e escreva a palavra-passe:</span><span class="sxs-lookup"><span data-stu-id="fea7f-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="fea7f-110"><a id="send"></a>Enviar uma aplicação de tooyour de notificação</span><span class="sxs-lookup"><span data-stu-id="fea7f-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="fea7f-111">Iremos agora criar uma campanha de notificação Push simples que vai enviar uma aplicação de tooour push:</span><span class="sxs-lookup"><span data-stu-id="fea7f-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="fea7f-112">Navegue toohello **alcançar** separador no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fea7f-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="fea7f-113">Clique em **novo anúncio** toocreate a campanha push.</span><span class="sxs-lookup"><span data-stu-id="fea7f-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="fea7f-114">Configurar os campos de primeiro Olá da sua campanha:</span><span class="sxs-lookup"><span data-stu-id="fea7f-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="fea7f-115">Forneça um **Nome** para a campanha.</span><span class="sxs-lookup"><span data-stu-id="fea7f-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="fea7f-116">Selecione Olá **hora de entrega** como **apenas fora da aplicação**: Este é Olá Apple push notification tipo simples que inclui algum texto.</span><span class="sxs-lookup"><span data-stu-id="fea7f-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="fea7f-117">Texto da notificação Olá, escreva primeiro Olá **título** que será a primeira linha de Olá no push Olá.</span><span class="sxs-lookup"><span data-stu-id="fea7f-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="fea7f-118">Em seguida, escreva o **mensagem** que será a segunda linha de Olá</span><span class="sxs-lookup"><span data-stu-id="fea7f-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="fea7f-119">Desloque para baixo e, no Olá secção de conteúdo selecione **apenas notificação**</span><span class="sxs-lookup"><span data-stu-id="fea7f-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="fea7f-120">Terminar a campanha mais básica do Olá definição.</span><span class="sxs-lookup"><span data-stu-id="fea7f-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="fea7f-121">Agora, desloque para baixo e clique em **criar** botão toosave sua campanha de notificações push.</span><span class="sxs-lookup"><span data-stu-id="fea7f-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="fea7f-122">Por fim, clique em **ativar** toosend notificações de push.</span><span class="sxs-lookup"><span data-stu-id="fea7f-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="fea7f-123">Poderá receber a notificação de Olá no seu dispositivo iOS no Centro de notificações de Olá semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="fea7f-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="fea7f-124">Se tiver um Apple Watch emparelhado com este dispositivo iOS, em seguida, verá Olá notificação no seu Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="fea7f-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

