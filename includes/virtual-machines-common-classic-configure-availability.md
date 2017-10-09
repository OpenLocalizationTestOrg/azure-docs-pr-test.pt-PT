


<span data-ttu-id="dd76e-101">Um conjunto de disponibilidade ajuda a manter as máquinas virtuais disponíveis durante o período de inatividade, tal como durante a manutenção.</span><span class="sxs-lookup"><span data-stu-id="dd76e-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="dd76e-102">Colocar duas ou mais máquinas virtuais da mesma forma configuradas num conjunto de disponibilidade cria Olá redundância necessária toomaintain disponibilidade dos serviços ou aplicações de Olá que executa a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dd76e-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="dd76e-103">Para obter mais informações sobre como isto funciona, consulte [gerir a disponibilidade de Olá das máquinas virtuais][Manage hello availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="dd76e-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="dd76e-104">É uma melhor toouse de prática conjuntos de disponibilidade e balanceamento de carga toohelp de pontos finais Certifique-se de que a aplicação está sempre disponível e em execução com eficiência.</span><span class="sxs-lookup"><span data-stu-id="dd76e-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="dd76e-105">Para obter detalhes sobre os pontos finais com balanceamento de carga, consulte [para serviços de infraestrutura do Azure de balanceamento de carga][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="dd76e-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="dd76e-106">Pode adicionar as máquinas virtuais clássicas para um conjunto, utilizando uma das duas opções de disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="dd76e-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="dd76e-107">[Opção 1: Criar uma máquina virtual e um conjunto de disponibilidade em Olá mesmo tempo][Option 1: Create a virtual machine and an availability set at hello same time].</span><span class="sxs-lookup"><span data-stu-id="dd76e-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="dd76e-108">Em seguida, adicione novas máquinas virtuais toohello, definido ao criar essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="dd76e-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="dd76e-109">[Opção 2: Adicionar um conjunto de disponibilidade de tooan de máquina virtual existente][Option 2: Add an existing virtual machine tooan availability set].</span><span class="sxs-lookup"><span data-stu-id="dd76e-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="dd76e-110">No modelo clássico de Olá Olá máquinas virtuais que pretende tooput no mesmo conjunto de disponibilidade tem de pertencer toohello mesmo serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="dd76e-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="dd76e-111"><a id="createset"></a>Opção 1: criar uma máquina virtual e um conjunto de disponibilidade em Olá mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="dd76e-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="dd76e-112">Pode utilizar qualquer um dos Olá portal do Azure ou do Azure PowerShell comandos toodo isto.</span><span class="sxs-lookup"><span data-stu-id="dd76e-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="dd76e-113">Olá toouse portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="dd76e-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="dd76e-114">Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd76e-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dd76e-115">No menu do hub de Olá, clique em **+ novo**e, em seguida, clique em **Máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="dd76e-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="dd76e-117">Selecione a imagem de máquina virtual de Marketplace Olá desejar toouse.</span><span class="sxs-lookup"><span data-stu-id="dd76e-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="dd76e-118">Pode escolher toocreate uma máquina virtual Linux ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="dd76e-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="dd76e-119">Para Olá selecionado máquina virtual, certifique-se de que modelo de implementação Olá estiver definido demasiado**clássico** e, em seguida, clique em **criar**</span><span class="sxs-lookup"><span data-stu-id="dd76e-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="dd76e-121">Introduza um nome da máquina virtual, o nome de utilizador e a palavra-passe (para máquinas do Windows) ou a chave pública SSH (para computadores Linux).</span><span class="sxs-lookup"><span data-stu-id="dd76e-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="dd76e-122">Escolha o tamanho da VM Olá e, em seguida, clique em **selecione** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="dd76e-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="dd76e-123">Escolha **configuração opcional > do conjunto de disponibilidade**e selecione o conjunto de disponibilidade de Olá desejar tooadd Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dd76e-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="dd76e-125">Reveja as definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="dd76e-125">Review your configuration settings.</span></span> <span data-ttu-id="dd76e-126">Quando tiver terminado, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="dd76e-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="dd76e-127">Enquanto o Azure cria a máquina virtual, pode controlar o progresso de Olá em **máquinas virtuais** no menu do hub de Olá.</span><span class="sxs-lookup"><span data-stu-id="dd76e-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="dd76e-128">toouse Azure PowerShell comandos toocreate uma máquina virtual do Azure e adicione-o conjunto de disponibilidade novo ou existente tooa, consulte [toocreate de utilização do Azure PowerShell e pré-configurar máquinas virtuais baseadas no Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="dd76e-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="dd76e-129"><a id="addmachine"></a>Opção 2: adicionar um conjunto de disponibilidade de tooan de máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="dd76e-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="dd76e-130">No portal do Azure Olá, pode adicionar existente as máquinas virtuais clássicas tooan, conjunto de disponibilidade de existente ou crie um novo para os mesmos.</span><span class="sxs-lookup"><span data-stu-id="dd76e-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="dd76e-131">(Tenha em atenção que as máquinas virtuais Olá Olá mesmo conjunto de disponibilidade tem de pertencer toohello mesmo serviço em nuvem.) passos de Olá são quase Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="dd76e-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="dd76e-132">Com o Azure PowerShell, pode adicionar o conjunto de disponibilidade Olá máquina virtual tooan existente.</span><span class="sxs-lookup"><span data-stu-id="dd76e-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="dd76e-133">Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd76e-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dd76e-134">No menu do Hub de Olá, clique em **máquinas virtuais (clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="dd76e-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="dd76e-136">Na lista de Olá de máquinas virtuais, selecione o nome de Olá da máquina virtual de Olá que pretende que o conjunto de toohello tooadd.</span><span class="sxs-lookup"><span data-stu-id="dd76e-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="dd76e-137">Escolha **do conjunto de disponibilidade** da máquina virtual de Olá **definições**.</span><span class="sxs-lookup"><span data-stu-id="dd76e-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="dd76e-139">Selecione o conjunto de disponibilidade de Olá que desejar tooadd Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dd76e-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="dd76e-140">máquina virtual de Olá têm de pertencer toohello mesmo serviço em nuvem como conjunto de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="dd76e-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="dd76e-142">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="dd76e-142">Click **Save**.</span></span>

<span data-ttu-id="dd76e-143">comandos do Azure PowerShell toouse, abra uma sessão do PowerShell do Azure de nível de administrador e execute Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="dd76e-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="dd76e-144">Para os marcadores de posição de Olá (tais como &lt;VmCloudServiceName&gt;), substituir tudo dentro de aspas Olá, incluindo Olá < e > carateres, com Olá corrigir nomes.</span><span class="sxs-lookup"><span data-stu-id="dd76e-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="dd76e-145">Olá poderá ter toofinish toobe reiniciado adicioná-lo toohello conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="dd76e-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

