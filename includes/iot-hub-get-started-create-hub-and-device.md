## <a name="create-an-iot-hub"></a><span data-ttu-id="119be-101">Criar um hub IoT</span><span class="sxs-lookup"><span data-stu-id="119be-101">Create an IoT hub</span></span>

1. <span data-ttu-id="119be-102">No Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **Internet das coisas** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="119be-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Criar um hub IoT no Olá portal do Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="119be-104">No Olá **IoT hub** painel, introduza Olá seguintes informações para o seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="119be-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="119be-105">**Nome**: introduza o nome de Olá do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="119be-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="119be-106">Se o nome de Olá introduzido é válido, aparece uma marca de verificação verde.</span><span class="sxs-lookup"><span data-stu-id="119be-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="119be-107">**Escalão de preço e escala**: Olá selecione **F1 - livre** camada.</span><span class="sxs-lookup"><span data-stu-id="119be-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="119be-108">Esta opção é suficiente para esta demonstração.</span><span class="sxs-lookup"><span data-stu-id="119be-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="119be-109">Para obter mais informações, consulte Olá [escalão de preço e escala](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="119be-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="119be-110">**Grupo de recursos**: criar um IoT hub do recurso grupo toohost Olá ou utilize uma já existente.</span><span class="sxs-lookup"><span data-stu-id="119be-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="119be-111">Para obter mais informações, consulte [toomanage de grupos de recursos de utilização, os recursos do Azure](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="119be-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="119be-112">**Localização**: selecione hello mais próximo tooyou de localização onde o hub IoT de Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="119be-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="119be-113">**PIN toodashboard**: selecione esta opção para o IoT hub tooyour facilitar o acesso a partir do dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="119be-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Introduza informações toocreate seu IoT hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="119be-115">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="119be-115">Click **Create**.</span></span> <span data-ttu-id="119be-116">IoT hub poderá demorar alguns minutos toocreate.</span><span class="sxs-lookup"><span data-stu-id="119be-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="119be-117">Pode ver o progresso na Olá **notificações** painel.</span><span class="sxs-lookup"><span data-stu-id="119be-117">You can see progress in hello **Notifications** pane.</span></span>

   ![Ver as notificações de progresso do hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="119be-119">Depois de criado o seu IoT hub, clique na mesma no dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="119be-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="119be-120">Tome nota do Olá **Hostname**e, em seguida, clique em **políticas de acesso partilhado**.</span><span class="sxs-lookup"><span data-stu-id="119be-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![Obter nome do anfitrião Olá do seu IoT hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="119be-122">No Olá **políticas de acesso partilhado** painel, clique em Olá **iothubowner** política e, em seguida, copiar e tome nota do Olá **cadeia de ligação** do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="119be-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="119be-123">Para obter mais informações, consulte [tooIoT de acesso de controlo Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="119be-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="119be-124">Não precisará da cadeia de ligação iothubowner para este tutorial de configuração.</span><span class="sxs-lookup"><span data-stu-id="119be-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="119be-125">No entanto, poderá ser necessário, para algumas das tutoriais Olá sobre os diferentes cenários de IoT depois de concluir esta configuração.</span><span class="sxs-lookup"><span data-stu-id="119be-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Obter a cadeia de ligação do hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="119be-127">Registar um dispositivo no Olá IoT hub para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="119be-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="119be-128">No Olá [portal do Azure](https://portal.azure.com/), abra o seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="119be-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="119be-129">Clique em **Device Explorer**.</span><span class="sxs-lookup"><span data-stu-id="119be-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="119be-130">No painel do Explorador de dispositivo Olá, clique em **adicionar** tooadd um dispositivo tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="119be-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="119be-131">Em seguida, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="119be-131">Then do hello following:</span></span>

   <span data-ttu-id="119be-132">**ID de dispositivo**: introduza o ID de Olá do novo dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="119be-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="119be-133">Os IDs dos dispositivos são sensíveis às maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="119be-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="119be-134">**Tipo de Autenticação**: selecione **Chave Simétrica**.</span><span class="sxs-lookup"><span data-stu-id="119be-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="119be-135">**Gerar Chaves Automaticamente**: selecione esta caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="119be-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="119be-136">**Ligar dispositivo tooIoT Hub**: clique em **ativar**.</span><span class="sxs-lookup"><span data-stu-id="119be-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![Adicionar um dispositivo no Olá Explorador de dispositivo do seu IoT hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="119be-138">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="119be-138">Click **Save**.</span></span>
5. <span data-ttu-id="119be-139">Depois de criar dispositivo Olá, abra o dispositivo de Olá no Olá **Explorador de dispositivo** painel.</span><span class="sxs-lookup"><span data-stu-id="119be-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="119be-140">Tome nota da chave primária de Olá Olá da cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="119be-140">Make a note of hello primary key of hello connection string.</span></span>

   ![Obter a cadeia de ligação do dispositivo Olá](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
