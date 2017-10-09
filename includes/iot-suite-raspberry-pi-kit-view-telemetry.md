## <a name="view-hello-telemetry"></a><span data-ttu-id="3fc9c-101">Telemetria de visualizações de Olá</span><span class="sxs-lookup"><span data-stu-id="3fc9c-101">View hello telemetry</span></span>

<span data-ttu-id="3fc9c-102">Olá Raspberry Pi agora está a enviar solução de monitorização remota telemetria toohello.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="3fc9c-103">Pode ver a telemetria de Olá no dashboard da solução Olá.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="3fc9c-104">Também pode enviar mensagens tooyour Raspberry Pi a partir do dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="3fc9c-105">Navegue toohello dashboard da solução.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="3fc9c-106">Selecione o seu dispositivo no Olá **dispositivo tooView** pendente.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="3fc9c-107">a telemetria de Olá de Olá Raspberry Pi apresenta no dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Apresentar a telemetria de Olá Raspberry Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a><span data-ttu-id="3fc9c-109">Atuar no dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="3fc9c-109">Act on hello device</span></span>

<span data-ttu-id="3fc9c-110">A partir do dashboard de solução Olá, pode invocar métodos no seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-110">From hello solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="3fc9c-111">Quando Olá Raspberry Pi se liga a solução de monitorização remota toohello, envia informações sobre métodos de Olá suporta.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-111">When hello Raspberry Pi connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span>

- <span data-ttu-id="3fc9c-112">No dashboard de solução Olá, clique em **dispositivos** toovisit Olá **dispositivos** página.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-112">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="3fc9c-113">Selecione o seu Raspberry Pi na Olá **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-113">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="3fc9c-114">Em seguida, escolha **métodos**:</span><span class="sxs-lookup"><span data-stu-id="3fc9c-114">Then choose **Methods**:</span></span>

    ![Lista de dispositivos no dashboard][img-list-devices]

- <span data-ttu-id="3fc9c-116">No Olá **invocar método** página, escolha **LightBlink** no Olá **método** pendente.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-116">On hello **Invoke Method** page, choose **LightBlink** in hello **Method** dropdown.</span></span>

- <span data-ttu-id="3fc9c-117">Escolha **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="3fc9c-118">Olá LED ligado toohello que raspberry Pi está intermitente várias vezes.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-118">hello LED connected toohello Raspberry Pi flashes several times.</span></span> <span data-ttu-id="3fc9c-119">aplicação Olá Olá Raspberry Pi envia um dashboard de solução de back-toohello confirmação:</span><span class="sxs-lookup"><span data-stu-id="3fc9c-119">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard:</span></span>

    ![Mostrar histórico de método][img-method-history]

- <span data-ttu-id="3fc9c-121">Pode mudar Olá LED e desativar a utilização Olá **ChangeLightStatus** método com um **LightStatusValue** definido demasiado**1** no ou **0** para desativado.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-121">You can switch hello LED on and off using hello **ChangeLightStatus** method with a **LightStatusValue** set too**1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="3fc9c-122">Se deixar Olá em execução na sua conta do Azure de solução de monitorização remota, é-lhe faturado por período de tempo de Olá que é executada.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-122">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="3fc9c-123">Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="3fc9c-123">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="3fc9c-124">Elimine a solução pré-configurada de Olá da sua conta do Azure quando tiver concluído a utilizá-la.</span><span class="sxs-lookup"><span data-stu-id="3fc9c-124">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md