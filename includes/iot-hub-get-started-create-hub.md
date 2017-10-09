## <a name="create-an-iot-hub"></a><span data-ttu-id="84237-101">Criar um hub IoT</span><span class="sxs-lookup"><span data-stu-id="84237-101">Create an IoT hub</span></span>
<span data-ttu-id="84237-102">Crie um IoT hub para sua tooconnect de aplicação do dispositivo simulado para.</span><span class="sxs-lookup"><span data-stu-id="84237-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="84237-103">Olá passos seguintes mostram como toocomplete esta tarefa pelo utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="84237-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="84237-104">Inicie sessão no toohello [portal do Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="84237-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="84237-105">No Jumpbar Olá, clique em **novo** > **Internet das coisas** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="84237-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Barra de atalhos do portal do Azure][1]
1. <span data-ttu-id="84237-107">No Olá **IoT hub** painel, escolha Olá configuração para o seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="84237-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![Painel do hub IoT][2]
   
   1. <span data-ttu-id="84237-109">No Olá **nome** box, introduza um nome para o seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="84237-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="84237-110">Se hello **nome** é válido e estiver disponível, irá aparecer uma marca de verificação verde no Olá **nome** caixa.</span><span class="sxs-lookup"><span data-stu-id="84237-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="84237-111">Selecione um [escalão de preços e dimensionamento][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="84237-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="84237-112">Este tutorial não requer um escalão específico.</span><span class="sxs-lookup"><span data-stu-id="84237-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="84237-113">Para este tutorial, utilize o escalão F1 gratuito de Olá.</span><span class="sxs-lookup"><span data-stu-id="84237-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="84237-114">Em **Grupo de recursos**, crie um grupo de recursos ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="84237-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="84237-115">Para obter mais informações, consulte [utilizar recursos grupos toomanage os recursos do Azure][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="84237-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="84237-116">No **localização**, selecione Olá localização toohost seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="84237-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="84237-117">Para este tutorial, escolha a localização mais próxima.</span><span class="sxs-lookup"><span data-stu-id="84237-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="84237-118">Quando tiver escolhido as opções de configuração do hub IoT, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="84237-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="84237-119">Pode demorar alguns minutos para Azure toocreate seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="84237-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="84237-120">Estado de Olá toocheck, pode monitorizar o progresso de Olá Olá Startboard ou no painel de notificações de Olá.</span><span class="sxs-lookup"><span data-stu-id="84237-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![Estado do novo hub IoT][3]
1. <span data-ttu-id="84237-122">Quando o hub IoT de Olá foi criado com êxito, clique no mosaico novo Olá para o seu hub IoT no painel de Olá Olá tooopen portal do Azure para o IoT hub novo Olá.</span><span class="sxs-lookup"><span data-stu-id="84237-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="84237-123">Tome nota do Olá **Hostname**e, em seguida, clique em **políticas de acesso partilhado**.</span><span class="sxs-lookup"><span data-stu-id="84237-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Novo painel do hub IoT][4]
1. <span data-ttu-id="84237-125">No Olá **políticas de acesso partilhado** painel, clique em Olá **iothubowner** política e, em seguida, copie e tome nota da cadeia de ligação do IoT Hub de Olá Olá **iothubowner** painel.</span><span class="sxs-lookup"><span data-stu-id="84237-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="84237-126">Para obter mais informações, consulte [controlo de acesso] [ lnk-access-control] no Olá "Guia para programadores do IoT Hub."</span><span class="sxs-lookup"><span data-stu-id="84237-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
    ![Painel das políticas de acesso partilhado][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
