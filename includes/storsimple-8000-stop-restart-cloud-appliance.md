#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="cfc58-101">toostop e iniciar uma aplicação de nuvem</span><span class="sxs-lookup"><span data-stu-id="cfc58-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="cfc58-102">toostop uma aplicação de nuvem, visite toohello VM para a sua aplicação de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cfc58-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="cfc58-103">![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="cfc58-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="cfc58-104">A partir da barra de comando Olá, clique em **parar**.</span><span class="sxs-lookup"><span data-stu-id="cfc58-104">From hello command bar, click **Stop**.</span></span>

    ![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="cfc58-106">Quando lhe for pedida a confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="cfc58-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="cfc58-108">Quando parar uma VM, esta é desalocada.</span><span class="sxs-lookup"><span data-stu-id="cfc58-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="cfc58-109">Enquanto o dispositivo de Olá de nuvem está a parar, o respetivo estado é **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="cfc58-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="cfc58-110">Após a paragem do dispositivo de Olá de nuvem, o respetivo estado é **parado (desalocado)**.</span><span class="sxs-lookup"><span data-stu-id="cfc58-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="cfc58-112">Depois de uma VM estiver parada, clique em **iniciar** (botão torna-se disponível) toostart Olá VM.</span><span class="sxs-lookup"><span data-stu-id="cfc58-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="cfc58-113">Depois do dispositivo de nuvem Olá começou a cópia de segurança, o respetivo estado é **iniciado**.</span><span class="sxs-lookup"><span data-stu-id="cfc58-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="cfc58-115">Utilize Olá os seguintes cmdlets toostop e iniciar uma aplicação de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cfc58-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="cfc58-116">toorestart uma aplicação de nuvem</span><span class="sxs-lookup"><span data-stu-id="cfc58-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="cfc58-117">toorestart uma aplicação de nuvem, visite toohello VM para a sua aplicação de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cfc58-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="cfc58-118">A partir da barra de comando Olá, clique em **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="cfc58-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="cfc58-119">Quando solicitado, confirme Olá reinício.</span><span class="sxs-lookup"><span data-stu-id="cfc58-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="cfc58-120">Quando o dispositivo de nuvem Olá está pronto para lhe toouse, o respetivo estado é **executar**.</span><span class="sxs-lookup"><span data-stu-id="cfc58-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![Máquina Virtual do StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="cfc58-122">Utilize Olá seguintes cmdlet toorestart uma aplicação de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cfc58-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

