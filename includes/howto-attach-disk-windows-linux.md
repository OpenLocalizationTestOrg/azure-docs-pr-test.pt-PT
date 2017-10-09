


## <a name="attach-an-empty-disk"></a><span data-ttu-id="aa24d-101">Anexar um disco vazio</span><span class="sxs-lookup"><span data-stu-id="aa24d-101">Attach an empty disk</span></span>
<span data-ttu-id="aa24d-102">Anexar um disco vazio é tooadd uma forma simples dados de disco, porque o Azure cria o ficheiro. vhd Olá para si e armazena-os na conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="aa24d-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="aa24d-103">Clique em **máquinas virtuais (clássicas)**, e, em seguida, selecione Olá VM adequado.</span><span class="sxs-lookup"><span data-stu-id="aa24d-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="aa24d-104">No menu de definições de Olá, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="aa24d-104">In hello Settings menu, click **Disks**.</span></span>

   ![Anexar um disco novo vazio](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="aa24d-106">Na barra de comando Olá, clique em **anexar novo**.</span><span class="sxs-lookup"><span data-stu-id="aa24d-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="aa24d-107">Olá **anexar novo disco** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa24d-107">hello **Attach new disk** dialog box appears.</span></span>

    ![Anexe um novo disco](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="aa24d-109">Preencha Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="aa24d-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="aa24d-110">No **nome de ficheiro**, aceite o nome predefinido de Olá ou escreva outro para o ficheiro. vhd Olá.</span><span class="sxs-lookup"><span data-stu-id="aa24d-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="aa24d-111">o disco de dados de Olá utiliza um nome gerado automaticamente, mesmo que escreva outro nome para o ficheiro. vhd Olá.</span><span class="sxs-lookup"><span data-stu-id="aa24d-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="aa24d-112">Selecione Olá **tipo** do disco de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="aa24d-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="aa24d-113">Todas as máquinas virtuais suportam discos padrão.</span><span class="sxs-lookup"><span data-stu-id="aa24d-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="aa24d-114">Número de máquinas virtuais também suporta discos premium.</span><span class="sxs-lookup"><span data-stu-id="aa24d-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="aa24d-115">Selecione Olá **tamanho (GB)** do disco de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="aa24d-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="aa24d-116">Para **alojar a colocação em cache**, escolha none ou só de leitura.</span><span class="sxs-lookup"><span data-stu-id="aa24d-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="aa24d-117">Clique em OK toofinish.</span><span class="sxs-lookup"><span data-stu-id="aa24d-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="aa24d-118">Depois de disco de dados de Olá é criado e ligado, este está listado na secção discos Olá Olá VM.</span><span class="sxs-lookup"><span data-stu-id="aa24d-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![Disco de dados nova e vazio anexado com êxito](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="aa24d-120">Depois de adicionar um disco de dados, tem de toolog no toohello VM e inicializar disco Olá, para que possa ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="aa24d-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="aa24d-121">Como: anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="aa24d-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="aa24d-122">Para anexar um disco existente, tem de ter um .vhd disponível numa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="aa24d-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="aa24d-123">Olá utilize [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload Olá. vhd ficheiro toohello conta do storage.</span><span class="sxs-lookup"><span data-stu-id="aa24d-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="aa24d-124">Depois de ter criado e carregado o ficheiro. vhd Olá, poderá anexar-tooa VM.</span><span class="sxs-lookup"><span data-stu-id="aa24d-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="aa24d-125">Clique em **máquinas virtuais (clássicas)**, e, em seguida, selecione Olá máquina virtual adequado.</span><span class="sxs-lookup"><span data-stu-id="aa24d-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="aa24d-126">No menu de definições de Olá, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="aa24d-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="aa24d-127">Na barra de comando Olá, clique em **anexar existente**.</span><span class="sxs-lookup"><span data-stu-id="aa24d-127">On hello command bar, click **Attach existing**.</span></span>

    ![Anexar disco de dados](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="aa24d-129">Clique em **localização**.</span><span class="sxs-lookup"><span data-stu-id="aa24d-129">Click **Location**.</span></span> <span data-ttu-id="aa24d-130">contas de armazenamento disponível Olá apresentam.</span><span class="sxs-lookup"><span data-stu-id="aa24d-130">hello available storage accounts display.</span></span> <span data-ttu-id="aa24d-131">Em seguida, selecione uma conta de armazenamento adequado aos listados.</span><span class="sxs-lookup"><span data-stu-id="aa24d-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Forneça a conta de armazenamento do disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="aa24d-133">A **conta de armazenamento** contém um ou mais contentores que contêm as unidades de disco (vhds).</span><span class="sxs-lookup"><span data-stu-id="aa24d-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="aa24d-134">Selecione o contentor adequado Olá das listados.</span><span class="sxs-lookup"><span data-stu-id="aa24d-134">Select hello appropriate container from those listed.</span></span>

    ![Forneça o contentor do windows de máquinas virtuais](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="aa24d-136">Olá **vhds** painel apresenta uma lista de unidades de disco Olá contidas no contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="aa24d-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="aa24d-137">Clique dos discos de Olá e, em seguida, clique em selecionar.</span><span class="sxs-lookup"><span data-stu-id="aa24d-137">Click one of hello disks, and then click Select.</span></span>

    ![Forneça a imagem de disco para o windows de máquinas virtuais](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="aa24d-139">Olá **anexar o disco existente** painel apresenta novamente, com a localização de Olá que contém a conta de armazenamento Olá, contentor e máquina virtual do disco rígido (vhd) selecionado tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="aa24d-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="aa24d-140">Definir **alojar a colocação em cache** toonone ou leitura apenas, em seguida, clique em OK.</span><span class="sxs-lookup"><span data-stu-id="aa24d-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![Disco de dados foi exposto com êxito](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
