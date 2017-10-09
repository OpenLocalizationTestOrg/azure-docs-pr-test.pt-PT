> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b960-101">C em Windows</span><span class="sxs-lookup"><span data-stu-id="7b960-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="7b960-102">C em Linux</span><span class="sxs-lookup"><span data-stu-id="7b960-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="7b960-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="7b960-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="7b960-104">Descrição geral do cenário</span><span class="sxs-lookup"><span data-stu-id="7b960-104">Scenario overview</span></span>
<span data-ttu-id="7b960-105">Neste cenário, vai criar um dispositivo que envia Olá seguir monitorização remota do telemetria toohello [solução pré-configurada][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="7b960-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="7b960-106">Temperatura externa</span><span class="sxs-lookup"><span data-stu-id="7b960-106">External temperature</span></span>
* <span data-ttu-id="7b960-107">Temperatura interna</span><span class="sxs-lookup"><span data-stu-id="7b960-107">Internal temperature</span></span>
* <span data-ttu-id="7b960-108">Humidade</span><span class="sxs-lookup"><span data-stu-id="7b960-108">Humidity</span></span>

<span data-ttu-id="7b960-109">Para uma simplicidade código Olá no dispositivo Olá gera valores de exemplo, mas Aconselhamo-tooextend Olá exemplo por ligar sensores real tooyour dispositivo e envia a telemetria real.</span><span class="sxs-lookup"><span data-stu-id="7b960-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="7b960-110">Olá é dispositivo também toomethods toorespond capaz de invocado a partir do dashboard de solução Olá e valores de propriedade definidos no dashboard de solução Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="7b960-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="7b960-111">toocomplete neste tutorial, precisa de uma conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7b960-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="7b960-112">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="7b960-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7b960-113">Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="7b960-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7b960-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7b960-114">Before you start</span></span>
<span data-ttu-id="7b960-115">Antes de escrever qualquer código para o seu dispositivo, terá de aprovisionar a sua solução pré-configurada de monitorização remota e aprovisionar um novo dispositivo personalizado nessa solução.</span><span class="sxs-lookup"><span data-stu-id="7b960-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="7b960-116">Aprovisionar a solução pré-configurada de monitorização remota</span><span class="sxs-lookup"><span data-stu-id="7b960-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="7b960-117">dispositivo de Olá criar neste tutorial envia a instância de tooan de dados do Olá [monitorização remota] [ lnk-remote-monitoring] solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="7b960-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="7b960-118">Se não tiver sido já aprovisionada Olá solução pré-configurada na sua conta do Azure de monitorização remota, utilize Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7b960-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="7b960-119">No Olá <https://www.azureiotsuite.com/> página, clique em  **+**  toocreate uma solução.</span><span class="sxs-lookup"><span data-stu-id="7b960-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="7b960-120">Clique em **selecione** no Olá **monitorização remota** painel toocreate sua solução.</span><span class="sxs-lookup"><span data-stu-id="7b960-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="7b960-121">No Olá **criar solução de monitorização remota** página, introduza um **nome da solução** à sua escolha, selecione Olá **região** pretende toodeploy para e selecione Olá do Azure subscrição toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="7b960-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="7b960-122">Em seguida, clique em **Criar solução**.</span><span class="sxs-lookup"><span data-stu-id="7b960-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="7b960-123">Aguarde pela conclusão do processo de aprovisionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b960-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="7b960-124">soluções de Olá pré-configuradas utilizam facturável serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b960-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="7b960-125">Certifique-se de tooremove Olá solução pré-configurada da sua subscrição quando tiver terminado com o mesmo tooavoid quaisquer custos desnecessários.</span><span class="sxs-lookup"><span data-stu-id="7b960-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="7b960-126">Pode remover por completo uma solução pré-configurada da sua subscrição, visitando Olá <https://www.azureiotsuite.com/> página.</span><span class="sxs-lookup"><span data-stu-id="7b960-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="7b960-127">Quando terminar, Olá processo para Olá solução de monitorização remota de aprovisionamento, clique em **iniciar** dashboard da solução Olá tooopen no seu browser.</span><span class="sxs-lookup"><span data-stu-id="7b960-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Dashboard de soluções][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="7b960-129">Aprovisionar o seu dispositivo no Olá solução de monitorização remota</span><span class="sxs-lookup"><span data-stu-id="7b960-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="7b960-130">Se já tiver aprovisionado um dispositivo na sua solução, pode ignorar este passo.</span><span class="sxs-lookup"><span data-stu-id="7b960-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="7b960-131">Precisa de credenciais de dispositivo tooknow Olá quando cria a aplicação de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="7b960-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="7b960-132">Para uma solução de toohello pré-configurada tooconnect do dispositivo, tem de identificar próprio tooIoT Hub utilizando as credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="7b960-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="7b960-133">Pode obter credenciais de dispositivo Olá a partir do dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="7b960-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="7b960-134">Incluir as credenciais de dispositivo Olá na sua aplicação de cliente mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b960-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="7b960-135">uma solução de monitorização remota do dispositivo tooyour tooadd, Olá concluir os seguintes passos no dashboard de solução Olá:</span><span class="sxs-lookup"><span data-stu-id="7b960-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="7b960-136">No Olá esquerda canto inferior do dashboard de Olá, clique em **adicionar um dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="7b960-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Adicionar um dispositivo][1]
2. <span data-ttu-id="7b960-138">No Olá **dispositivo personalizado** painel, clique em **adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="7b960-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Adicionar um dispositivo personalizado][2]
3. <span data-ttu-id="7b960-140">Escolha **Definir o meu próprio ID do Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="7b960-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="7b960-141">Introduza um ID de dispositivo como **mydevice**, clique em **verifique ID** tooverify esse nome não está já em utilização e, em seguida, clique em **criar** dispositivo de Olá tooprovision.</span><span class="sxs-lookup"><span data-stu-id="7b960-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Adicionar ID do dispositivo][3]
4. <span data-ttu-id="7b960-143">Se um dispositivo de Olá nota credenciais (ID de dispositivo, o nome de anfitrião do IoT Hub e a chave de dispositivo).</span><span class="sxs-lookup"><span data-stu-id="7b960-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="7b960-144">A aplicação cliente tem toohello de tooconnect estes valores de solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="7b960-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="7b960-145">Em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7b960-145">Then click **Done**.</span></span>
   
    ![Ver as credenciais do dispositivo][4]
5. <span data-ttu-id="7b960-147">Selecione o seu dispositivo na lista de dispositivos de Olá no dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="7b960-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="7b960-148">Em seguida, no Olá **detalhes do dispositivo** painel, clique em **ativar dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="7b960-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="7b960-149">Estado de Olá do seu dispositivo está agora **executar**.</span><span class="sxs-lookup"><span data-stu-id="7b960-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="7b960-150">solução de monitorização remota Olá pode agora receber telemetria a partir do dispositivo e invocar métodos num dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="7b960-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/