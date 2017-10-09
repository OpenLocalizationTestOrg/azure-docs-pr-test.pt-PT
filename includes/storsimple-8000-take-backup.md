<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="ad7b7-101">tootake uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="ad7b7-101">tootake a backup</span></span>

1. <span data-ttu-id="ad7b7-102">Aceda tooyour do serviço StorSimple Manager de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="ad7b7-103">Olá tabela lista de dispositivos selecione e clique em seu dispositivo e, em seguida, clique em **todas as definições**.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="ad7b7-104">No Olá **definições** painel, vá demasiado**definições > Gerir > política de cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="ad7b7-106">No Olá **política de cópia de segurança** painel, clique em **+ Adicionar política**.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="ad7b7-108">No Olá **criar política de cópia de segurança** painel, forneça um nome que contenha entre 3 e 150 carateres para a sua política de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="ad7b7-109">Selecione Olá volumes toobe uma cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="ad7b7-110">Se selecionar mais do que um volume, estes volumes se encontram agrupado toocreate em conjunto uma cópia de segurança consistentes com falhas.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="ad7b7-112">No painel **Adicionar primeira agenda**:</span><span class="sxs-lookup"><span data-stu-id="ad7b7-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="ad7b7-113">Selecione o tipo de Olá da cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-113">Select hello type of backup.</span></span> <span data-ttu-id="ad7b7-114">Para restauros mais rápidos, selecione instantâneo **Local**.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="ad7b7-115">Para resiliência de dados, selecione instantâneo da **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="ad7b7-116">Especifique a frequência de cópia de segurança de Olá em minutos, horas, dias ou semanas.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="ad7b7-117">Selecione um tempo de retenção.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-117">Select a retention time.</span></span> <span data-ttu-id="ad7b7-118">Opções de retenção de Olá dependem da frequência de cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="ad7b7-119">Por exemplo, para uma política diária, retenção de Olá pode ser especificada em semanas, enquanto que o período de retenção para uma política mensal é em meses.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="ad7b7-120">Selecione Olá Iniciar hora e data de política de cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="ad7b7-121">Clique em **OK** política de cópia de segurança de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="ad7b7-123">Clique em **criar** toostart a criação da política de cópia de segurança Olá.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="ad7b7-124">Será notificado quando a política de cópia de segurança de Olá é criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="ad7b7-125">lista de Olá das políticas de cópia de segurança também é atualizada.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-125">hello list of backup policies is also updated.</span></span>
      
      ![Adicionar-política-cópia-de-segurança](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="ad7b7-127">Tem agora uma política de cópias de segurança que cria as cópias de segurança agendadas dos dados do seu volume.</span><span class="sxs-lookup"><span data-stu-id="ad7b7-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




