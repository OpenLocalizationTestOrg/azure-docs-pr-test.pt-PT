<!--author=alkohli last changed: 07/07/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a><span data-ttu-id="6ce58-101">tooinstall uma atualização do Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6ce58-101">tooinstall an update from hello Azure portal</span></span>

1. <span data-ttu-id="6ce58-102">Na página do serviço de Olá StorSimple, selecione o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6ce58-102">On hello StorSimple service page, select your device.</span></span>

    ![Selecione o dispositivo](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. <span data-ttu-id="6ce58-104">Navegue demasiado**definições do dispositivo** > **atualizações ao dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="6ce58-104">Navigate too**Device settings** > **Device updates**.</span></span>

    ![Clique em atualizações ao dispositivo](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. <span data-ttu-id="6ce58-106">É apresentada uma notificação se estiverem disponíveis novas atualizações.</span><span class="sxs-lookup"><span data-stu-id="6ce58-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="6ce58-107">Em alternativa, na Olá **atualizações ao dispositivo** painel, clique em **procurar atualizações**.</span><span class="sxs-lookup"><span data-stu-id="6ce58-107">Alternatively, in hello **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="6ce58-108">É criada uma tarefa tooscan para as atualizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6ce58-108">A job is created tooscan for available updates.</span></span> <span data-ttu-id="6ce58-109">Será notificado quando a tarefa de Olá for concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="6ce58-109">You are notified when hello job completes successfully.</span></span>

    ![Clique em atualizações ao dispositivo](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. <span data-ttu-id="6ce58-111">Recomendamos que consulte as notas de versão Olá antes de aplicar uma atualização no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6ce58-111">We recommend that you review hello release notes before you apply an update on your device.</span></span> <span data-ttu-id="6ce58-112">tooapply atualizações, clique em **instalar atualizações**.</span><span class="sxs-lookup"><span data-stu-id="6ce58-112">tooapply updates, click **Install updates**.</span></span> <span data-ttu-id="6ce58-113">No Olá **confirmar atualizações regulares** painel, reveja Olá pré-requisitos toocomplete antes de aplicar as atualizações.</span><span class="sxs-lookup"><span data-stu-id="6ce58-113">In hello **Confirm regular updates** blade, review hello prerequisites toocomplete before you apply updates.</span></span> <span data-ttu-id="6ce58-114">Selecione Olá tooindicate de caixa de verificação que sejam tooupdate pronto Olá dispositivo e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="6ce58-114">Select hello checkbox tooindicate that you are ready tooupdate hello device and then click **Install**.</span></span>

    ![Clique em atualizações ao dispositivo](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. <span data-ttu-id="6ce58-116">Um conjunto de verificações de pré-requisitos é iniciado.</span><span class="sxs-lookup"><span data-stu-id="6ce58-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="6ce58-117">Estas verificações incluem:</span><span class="sxs-lookup"><span data-stu-id="6ce58-117">These checks include:</span></span>
   
   * <span data-ttu-id="6ce58-118">**As verificações de estado de funcionamento do controlador** tooverify ambos Olá de controladores de dispositivo são bom estado de funcionamento e online.</span><span class="sxs-lookup"><span data-stu-id="6ce58-118">**Controller health checks** tooverify that both hello device controllers are healthy and online.</span></span>
   * <span data-ttu-id="6ce58-119">**Verificações de estado de funcionamento do componente de hardware** tooverify que Olá todos os componentes de hardware no dispositivo StorSimple estão em bom estado.</span><span class="sxs-lookup"><span data-stu-id="6ce58-119">**Hardware component health checks** tooverify that all hello hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="6ce58-120">**DATA 0 verifica** tooverify que dados 0 estão ativados no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6ce58-120">**DATA 0 checks** tooverify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="6ce58-121">Se esta interface não estiver ativada, terá de ativá-la e, em seguida, tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="6ce58-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="6ce58-122">atualização de Olá é transferida e instalada apenas se a todas as verificações de Olá forem concluídas com êxito.</span><span class="sxs-lookup"><span data-stu-id="6ce58-122">hello update is downloaded and installed only if all hello checks are successfully completed.</span></span> <span data-ttu-id="6ce58-123">Será notificado quando as verificações de Olá estão em curso.</span><span class="sxs-lookup"><span data-stu-id="6ce58-123">You are notified when hello checks are in progress.</span></span> <span data-ttu-id="6ce58-124">Se falharem prechecks Olá, em seguida, irá ser fornecido com motivos Olá da falha.</span><span class="sxs-lookup"><span data-stu-id="6ce58-124">If hello prechecks fail, then you will be provided with hello reasons for failure.</span></span> <span data-ttu-id="6ce58-125">Resolva os problemas e, em seguida, repita a operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="6ce58-125">Address those issues and then retry hello operation.</span></span> <span data-ttu-id="6ce58-126">Poderá ser necessário toocontact Support da Microsoft, caso não é possível resolver estes problemas por si.</span><span class="sxs-lookup"><span data-stu-id="6ce58-126">You may need toocontact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="6ce58-127">Depois de Olá prechecks forem concluídos com êxito, é criada uma tarefa de atualização.</span><span class="sxs-lookup"><span data-stu-id="6ce58-127">After hello prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="6ce58-128">Será notificado quando a tarefa de atualização de Olá é criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="6ce58-128">You are notified when hello update job is successfully created.</span></span>
   
    ![Criação de tarefa de atualização](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    <span data-ttu-id="6ce58-130">atualização de Olá, em seguida, é aplicada no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6ce58-130">hello update is then applied on your device.</span></span>

9. <span data-ttu-id="6ce58-131">atualização de Olá demora algumas horas toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6ce58-131">hello update takes a few hours toocomplete.</span></span> <span data-ttu-id="6ce58-132">Selecione a tarefa de atualização de Olá e clique em **detalhes** tooview Olá detalhes sobre a tarefa de Olá em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="6ce58-132">Select hello update job and click **Details** tooview hello details of hello job at any time.</span></span>

    ![Criação de tarefa de atualização](./media/storsimple-8000-install-update4-via-portal/update8.png)

     <span data-ttu-id="6ce58-134">Também pode monitorizar o progresso de Olá da tarefa de atualização de Olá de **definições do dispositivo > tarefas**.</span><span class="sxs-lookup"><span data-stu-id="6ce58-134">You can also monitor hello progress of hello update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="6ce58-135">No Olá **tarefas** painel, pode ver Olá em curso de atualização.</span><span class="sxs-lookup"><span data-stu-id="6ce58-135">On hello **Jobs** blade, you can see hello update progress.</span></span>

     ![Criação de tarefa de atualização](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. <span data-ttu-id="6ce58-137">Após a conclusão da tarefa de Olá, navegue até toohello **definições do dispositivo > atualizações ao dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="6ce58-137">After hello job is complete, navigate toohello **Device settings > Device updates**.</span></span> <span data-ttu-id="6ce58-138">versão do software de Olá agora deve ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="6ce58-138">hello software version should now be updated.</span></span>

    ![Criação de tarefa de atualização](./media/storsimple-8000-install-update4-via-portal/update9.png)

