
<span data-ttu-id="7856c-101">Para obter mais informações sobre discos, veja [About Disks and VHDs for Virtual Machines (Acerca de Discos e VHDs para Máquinas Virtuais)](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7856c-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="7856c-102">Anexar um disco vazio</span><span class="sxs-lookup"><span data-stu-id="7856c-102">Attach an empty disk</span></span>
1. <span data-ttu-id="7856c-103">Abra a CLI do Azure 1.0 e [ligar tooyour subscrição do Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7856c-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="7856c-104">Confirme que está no modo Gestão de Serviço do Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="7856c-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="7856c-105">Introduza `azure vm disk attach-new` toocreate e anexe um novo disco, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="7856c-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="7856c-106">Substitua *myVM* com o nome de Olá da Máquina Virtual com Linux e especifique o tamanho do disco de Olá Olá em GB, o que é *100GB* neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="7856c-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="7856c-107">Depois de disco de dados de Olá é criado e ligado, está listado no resultado Olá `azure vm disk list <virtual-machine-name>` conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="7856c-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="7856c-108">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="7856c-108">hello output is similar toohello following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="7856c-109">Anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="7856c-109">Attach an existing disk</span></span>
<span data-ttu-id="7856c-110">Para anexar um disco existente, tem de ter um .vhd disponível numa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7856c-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="7856c-111">Abra a CLI do Azure 1.0 e [ligar tooyour subscrição do Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7856c-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="7856c-112">Confirme que está no modo Gestão de Serviço do Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="7856c-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="7856c-113">Verifique se Olá VHD que pretende tooattach já está carregado tooyour subscrição do Azure:</span><span class="sxs-lookup"><span data-stu-id="7856c-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="7856c-114">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="7856c-114">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="7856c-115">Se não encontrar o disco de Olá que quiser toouse, pode carregar uma subscrição de tooyour VHD local utilizando `azure vm disk create` ou `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="7856c-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="7856c-116">Um exemplo de `disk create` seria como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="7856c-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="7856c-117">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="7856c-117">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="7856c-118">Também pode utilizar `azure vm disk upload` tooupload uma conta de armazenamento específicas de tooa do VHD.</span><span class="sxs-lookup"><span data-stu-id="7856c-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="7856c-119">Ler mais sobre Olá comandos toomanage os discos de dados de máquina virtual do Azure [através de aqui](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7856c-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="7856c-120">Agora pode anexa Olá pretendido VHD tooyour máquina:</span><span class="sxs-lookup"><span data-stu-id="7856c-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="7856c-121">Certifique-se de que tooreplace *myVM* com o nome de Olá da sua máquina virtual, e *myVHD* com o VHD pretendido.</span><span class="sxs-lookup"><span data-stu-id="7856c-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="7856c-122">Pode verificar o disco de Olá é anexado toohello máquina de virtual com `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="7856c-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="7856c-123">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="7856c-123">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="7856c-124">Depois de adicionar um disco de dados, irá precisar de toolog na máquina virtual de toohello e inicializar disco Olá, para que a máquina virtual de Olá pode utilizar o disco de Olá para armazenamento (veja Olá os seguintes passos para obter mais informações sobre como toodo Inicializar disco Olá).</span><span class="sxs-lookup"><span data-stu-id="7856c-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 

