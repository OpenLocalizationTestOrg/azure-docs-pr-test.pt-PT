<span data-ttu-id="9e045-101">Quando já não necessita de um disco de dados que esteja anexado tooa máquina de virtual (VM), pode facilmente desanexá-lo.</span><span class="sxs-lookup"><span data-stu-id="9e045-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="9e045-102">Quando lhe desligar um disco de Olá VM, disco de Olá não é removido do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9e045-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="9e045-103">Se pretende que os toouse Olá existente dados no disco Olá novamente, pode reattach-toohello VM mesmo ou outro.</span><span class="sxs-lookup"><span data-stu-id="9e045-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="9e045-104">Uma VM no Azure utiliza diferentes tipos de discos - um disco de sistema operativo, um disco local temporário e discos de dados opcionais.</span><span class="sxs-lookup"><span data-stu-id="9e045-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="9e045-105">Para obter detalhes, veja [Acerca dos Discos e VHDs para Máquinas Virtuais](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e045-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9e045-106">Não é possível desanexar um disco de sistema operativo, a menos que também eliminar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="9e045-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="9e045-107">Localizar o disco de Olá</span><span class="sxs-lookup"><span data-stu-id="9e045-107">Find hello disk</span></span>
<span data-ttu-id="9e045-108">Antes de pode desanexar um disco de uma VM tem toofind saída Olá número LUN, que é um identificador para Olá disco toobe desligado.</span><span class="sxs-lookup"><span data-stu-id="9e045-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="9e045-109">toodo que, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="9e045-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="9e045-110">Abra a CLI do Azure e [ligar tooyour subscrição do Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="9e045-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="9e045-111">Confirme que está no modo Gestão de Serviço do Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="9e045-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="9e045-112">Determinar que discos estão anexado tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="9e045-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="9e045-113">Olá exemplo seguinte apresenta uma lista de discos para a VM com o nome de Olá `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9e045-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="9e045-114">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9e045-114">hello output is similar toohello following example:</span></span>

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. <span data-ttu-id="9e045-115">Tenha em atenção Olá LUN ou Olá **número de unidade lógica** para disco Olá que pretende que o toodetach.</span><span class="sxs-lookup"><span data-stu-id="9e045-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="9e045-116">Remover disco do sistema operativo referências toohello</span><span class="sxs-lookup"><span data-stu-id="9e045-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="9e045-117">Antes de desanexar o disco de Olá de convidado de Linux Olá, certifique-se de que todas as partições de disco Olá não estão em utilização.</span><span class="sxs-lookup"><span data-stu-id="9e045-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="9e045-118">Certifique-se de que esse sistema de operativo Olá não tenta tooremount-las após um reinício.</span><span class="sxs-lookup"><span data-stu-id="9e045-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="9e045-119">Estes passos de configuração de Olá provavelmente criado quando anular [anexar](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disco Olá.</span><span class="sxs-lookup"><span data-stu-id="9e045-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="9e045-120">Olá utilize `lsscsi` identificador do comando toodiscover Olá disco.</span><span class="sxs-lookup"><span data-stu-id="9e045-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="9e045-121">`lsscsi` pode ser instalado através de `yum install lsscsi` (em distribuições baseadas no Red Hat) ou de `apt-get install lsscsi` (em distribuições baseadas no Debian).</span><span class="sxs-lookup"><span data-stu-id="9e045-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="9e045-122">Pode encontrar o identificador de disco Olá que estiver à procura de utilizando o número LUN Olá.</span><span class="sxs-lookup"><span data-stu-id="9e045-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="9e045-123">número da última Olá na cadeia de identificação de Olá em cada linha é Olá LUN.</span><span class="sxs-lookup"><span data-stu-id="9e045-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="9e045-124">No Olá seguinte o exemplo de `lsscsi`, LUN 0 mapeia demasiado  */dev/sdc*</span><span class="sxs-lookup"><span data-stu-id="9e045-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="9e045-125">Utilize `fdisk -l <disk>` partições de Olá toodiscover associadas Olá disco toobe desligado.</span><span class="sxs-lookup"><span data-stu-id="9e045-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="9e045-126">Olá exemplo seguinte mostra o resultado Olá para `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="9e045-126">hello following example shows hello output for `/dev/sdc`:</span></span>

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. <span data-ttu-id="9e045-127">Desmonte cada partição listada para o disco de Olá.</span><span class="sxs-lookup"><span data-stu-id="9e045-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="9e045-128">Olá exemplo seguinte unmounts `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="9e045-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="9e045-129">Olá utilize `blkid` Olá de toodiscovery UUIDs não comandos para todas as partições.</span><span class="sxs-lookup"><span data-stu-id="9e045-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="9e045-130">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9e045-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="9e045-131">Remova as entradas no Olá **etc/fstab** ficheiro associado caminhos de dispositivo Olá ou UUIDs não para todas as partições de Olá disco toobe desligado.</span><span class="sxs-lookup"><span data-stu-id="9e045-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="9e045-132">As entradas para este exemplo poderão ser:</span><span class="sxs-lookup"><span data-stu-id="9e045-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="9e045-133">ou</span><span class="sxs-lookup"><span data-stu-id="9e045-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="9e045-134">Exposição do disco de Olá</span><span class="sxs-lookup"><span data-stu-id="9e045-134">Detach hello disk</span></span>
<span data-ttu-id="9e045-135">Depois de encontrar o número LUN de Olá de disco Olá e referências de sistema operativo Olá removido, está pronto toodetach-lo:</span><span class="sxs-lookup"><span data-stu-id="9e045-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="9e045-136">Exposição do disco selecionado do Olá da máquina virtual de Olá executando o comando de Olá `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="9e045-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="9e045-137">Olá exemplo seguinte Desanexa LUN `0` da VM com o nome de Olá `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9e045-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="9e045-138">Pode verificar se o disco Olá obteve desligado executando `azure vm disk list` novamente.</span><span class="sxs-lookup"><span data-stu-id="9e045-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="9e045-139">Olá seguintes verificações de exemplo Olá VM com o nome `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9e045-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="9e045-140">Olá de saída é semelhante toohello seguinte o exemplo, que mostra o disco de dados de Olá já não está ligado:</span><span class="sxs-lookup"><span data-stu-id="9e045-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

<span data-ttu-id="9e045-141">disco Olá desligado permanece no armazenamento, mas já não máquina virtual de tooa anexado.</span><span class="sxs-lookup"><span data-stu-id="9e045-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

