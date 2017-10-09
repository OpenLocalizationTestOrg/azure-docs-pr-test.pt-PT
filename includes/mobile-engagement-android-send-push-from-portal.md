### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="de26d-101">Conceda o Mobile Engagement acesso tooyour chave de API do GCM</span><span class="sxs-lookup"><span data-stu-id="de26d-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="de26d-102">tooallow Mobile Engagement toosend as notificações push em seu nome, terá de toogrant aceder a tooyour chave de API.</span><span class="sxs-lookup"><span data-stu-id="de26d-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="de26d-103">Isto é feito ao configurar e introduzir a chave no portal de Mobile Engagement Olá.</span><span class="sxs-lookup"><span data-stu-id="de26d-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="de26d-104">Do seu Portal clássico do Azure, certifique-se de que está na aplicação de Olá que estamos a utilizar para este projeto e, em seguida, clique em Olá **iniciar** botão na parte inferior de Olá:</span><span class="sxs-lookup"><span data-stu-id="de26d-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="de26d-105">Em seguida, clique em Olá **definições** -> **Push nativo** secção tooenter a chave do GCM:</span><span class="sxs-lookup"><span data-stu-id="de26d-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="de26d-106">Clique em Olá **editar** ícone à frente do **chave de API** no Olá **definições de GCM** secção conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="de26d-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="de26d-107">No pop-up de Olá, cole Olá chave do servidor GCM que obteve anteriormente e, em seguida, clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="de26d-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="de26d-108"><a id="send"></a>Enviar uma aplicação de tooyour de notificação</span><span class="sxs-lookup"><span data-stu-id="de26d-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="de26d-109">Iremos agora criar uma campanha de notificações push simples que envia uma aplicação de tooour de notificação push.</span><span class="sxs-lookup"><span data-stu-id="de26d-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="de26d-110">Navegue toohello **ALCANÇAR** separador no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="de26d-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="de26d-111">Clique em **novo anúncio** toocreate sua campanha de notificações push.</span><span class="sxs-lookup"><span data-stu-id="de26d-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="de26d-112">Configure o primeiro campo de Olá da campanha com Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="de26d-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="de26d-113">a.</span><span class="sxs-lookup"><span data-stu-id="de26d-113">a.</span></span> <span data-ttu-id="de26d-114">Dê um nome à campanha.</span><span class="sxs-lookup"><span data-stu-id="de26d-114">Name your campaign.</span></span>
   
    <span data-ttu-id="de26d-115">b.</span><span class="sxs-lookup"><span data-stu-id="de26d-115">b.</span></span> <span data-ttu-id="de26d-116">Selecione Olá **tipo de entrega** como *notificação do sistema -> simples*: Este é o tipo de notificação push Android simples do Olá que inclui um título e uma pequena linha de texto.</span><span class="sxs-lookup"><span data-stu-id="de26d-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="de26d-117">c.</span><span class="sxs-lookup"><span data-stu-id="de26d-117">c.</span></span> <span data-ttu-id="de26d-118">Selecione **hora de entrega** como *sempre* tooallow Olá aplicação tooreceive uma notificação se a aplicação Olá é iniciada ou não.</span><span class="sxs-lookup"><span data-stu-id="de26d-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="de26d-119">d.</span><span class="sxs-lookup"><span data-stu-id="de26d-119">d.</span></span> <span data-ttu-id="de26d-120">No Olá de tipo de texto de notificação de Olá **título** que será em negrito no push Olá.</span><span class="sxs-lookup"><span data-stu-id="de26d-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="de26d-121">e.</span><span class="sxs-lookup"><span data-stu-id="de26d-121">e.</span></span> <span data-ttu-id="de26d-122">Em seguida, escreva a **Mensagem**</span><span class="sxs-lookup"><span data-stu-id="de26d-122">Then type your **Message**</span></span>
4. <span data-ttu-id="de26d-123">Desloque-se para baixo e, na Olá **conteúdo** secção, selecione **apenas notificação**.</span><span class="sxs-lookup"><span data-stu-id="de26d-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="de26d-124">Terminar possíveis de campanha mais básica Olá definição.</span><span class="sxs-lookup"><span data-stu-id="de26d-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="de26d-125">Agora, desloque para baixo novamente e clique em Olá **criar** botão toosave sua campanha.</span><span class="sxs-lookup"><span data-stu-id="de26d-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="de26d-126">Último passo: clique em **ativar** tooactivate as notificações de push de toosend campanha.</span><span class="sxs-lookup"><span data-stu-id="de26d-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

