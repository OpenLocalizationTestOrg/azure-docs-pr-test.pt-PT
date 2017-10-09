## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="63e0b-101">Dashboard da solução Olá vista</span><span class="sxs-lookup"><span data-stu-id="63e0b-101">View hello solution dashboard</span></span>

<span data-ttu-id="63e0b-102">dashboard de solução Olá permite-lhe toomanage solução de Olá implementado.</span><span class="sxs-lookup"><span data-stu-id="63e0b-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="63e0b-103">Por exemplo, pode ver a telemetria, adicionar dispositivos e invocar métodos.</span><span class="sxs-lookup"><span data-stu-id="63e0b-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="63e0b-104">Quando Olá aprovisionamento estiver concluído e Olá mosaico da sua solução pré-configuradas indicar **pronto**, escolha **iniciar** tooopen seu portal de solução de monitorização remota num novo separador.</span><span class="sxs-lookup"><span data-stu-id="63e0b-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Iniciar a solução pré-configurada de Olá][img-launch-solution]

1. <span data-ttu-id="63e0b-106">Por predefinição, o portal de solução Olá mostra Olá *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="63e0b-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="63e0b-107">Navegue tooother áreas do portal de solução Olá utilizando o menu de Olá no lado esquerdo do Olá da página Olá.</span><span class="sxs-lookup"><span data-stu-id="63e0b-107">Navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Dashboard da solução pré-configurada de monitorização remota][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="63e0b-109">Adicionar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="63e0b-109">Add a device</span></span>

<span data-ttu-id="63e0b-110">Para uma solução de toohello pré-configurada tooconnect do dispositivo, tem de identificar próprio tooIoT Hub utilizando as credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="63e0b-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="63e0b-111">Pode obter credenciais de dispositivo Olá a partir do dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="63e0b-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="63e0b-112">Incluir as credenciais de dispositivo Olá na sua aplicação de cliente mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="63e0b-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="63e0b-113">uma solução de monitorização remota do dispositivo tooyour tooadd, Olá concluir os seguintes passos no dashboard de solução Olá:</span><span class="sxs-lookup"><span data-stu-id="63e0b-113">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="63e0b-114">No Olá esquerda canto inferior do dashboard de Olá, clique em **adicionar um dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="63e0b-114">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![Adicionar um dispositivo][1]

1. <span data-ttu-id="63e0b-116">No Olá **dispositivo personalizado** painel, clique em **adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="63e0b-116">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![Adicionar um dispositivo personalizado][2]

1. <span data-ttu-id="63e0b-118">Escolha **Definir o meu próprio ID do Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="63e0b-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="63e0b-119">Introduza um ID de dispositivo como **device01**, clique em **verifique ID** tooverify já não tiver usado nome Olá na sua solução e, em seguida, clique em **criar** dispositivo de Olá tooprovision.</span><span class="sxs-lookup"><span data-stu-id="63e0b-119">Enter a Device ID such as **device01**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![Adicionar ID do dispositivo][3]

1. <span data-ttu-id="63e0b-121">Se um dispositivo de Olá nota credenciais (**ID de dispositivo**, **o nome de anfitrião do IoT Hub**, e **chave do dispositivo**).</span><span class="sxs-lookup"><span data-stu-id="63e0b-121">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="63e0b-122">A aplicação de cliente no Olá Intel NUC tem toohello de tooconnect estes valores de solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="63e0b-122">Your client application on hello Intel NUC needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="63e0b-123">Em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="63e0b-123">Then click **Done**.</span></span>

    ![Ver as credenciais do dispositivo][4]

1. <span data-ttu-id="63e0b-125">Selecione o seu dispositivo na lista de dispositivos de Olá no dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="63e0b-125">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="63e0b-126">Em seguida, no Olá **detalhes do dispositivo** painel, clique em **ativar dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="63e0b-126">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="63e0b-127">Estado de Olá do seu dispositivo está agora **executar**.</span><span class="sxs-lookup"><span data-stu-id="63e0b-127">hello status of your device is now **Running**.</span></span> <span data-ttu-id="63e0b-128">solução de monitorização remota Olá pode agora receber telemetria a partir do dispositivo e invocar métodos num dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="63e0b-128">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png