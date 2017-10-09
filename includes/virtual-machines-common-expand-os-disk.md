## <a name="overview"></a><span data-ttu-id="a89c3-101">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="a89c3-101">Overview</span></span>
<span data-ttu-id="a89c3-102">Quando cria uma nova máquina virtual (VM) num grupo de recursos ao implementar uma imagem de [Azure Marketplace](https://azure.microsoft.com/marketplace/), disco de SO Olá predefinido é de 127 GB.</span><span class="sxs-lookup"><span data-stu-id="a89c3-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="a89c3-103">Mesmo que é possível tooadd dados discos toohello VM (quantos consoante Olá SKU que escolheu) e além é recomendada tooinstall aplicações e cargas de trabalho que consomem muita CPU nestes discos adenda, frequentemente que os clientes precisam tooexpand Olá SO unidade toosupport determinados cenários, como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a89c3-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="a89c3-104">Suportar aplicações antigas que instalam componentes na unidade do SO.</span><span class="sxs-lookup"><span data-stu-id="a89c3-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="a89c3-105">Migrar uma máquina virtual ou PC físicos no local com uma unidade de SO maior.</span><span class="sxs-lookup"><span data-stu-id="a89c3-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a89c3-106">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: Resource Manager e Clássico.</span><span class="sxs-lookup"><span data-stu-id="a89c3-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="a89c3-107">Este artigo abrange utilizando o modelo do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="a89c3-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="a89c3-108">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="a89c3-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="a89c3-109">Redimensionar disco Olá SO</span><span class="sxs-lookup"><span data-stu-id="a89c3-109">Resize hello OS drive</span></span>
<span data-ttu-id="a89c3-110">Neste artigo, irá realizar tarefas Olá de redimensionamento unidade Olá SO utilizar módulos do Gestor de recursos de [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a89c3-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a89c3-111">Abra o ISE do Powershell ou a janela do Powershell no modo administrativo e siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="a89c3-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="a89c3-112">Início de sessão tooyour Microsoft Azure conta no modo de gestão de recursos e selecione a sua subscrição da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="a89c3-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="a89c3-113">Defina o nome do grupo de recursos e o nome VM da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="a89c3-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="a89c3-114">Obter uma referência tooyour VM da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="a89c3-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="a89c3-115">Pare Olá VM antes de o redimensionamento de disco Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="a89c3-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="a89c3-116">E provém aqui momento Olá que tiver sido a aguardar!</span><span class="sxs-lookup"><span data-stu-id="a89c3-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="a89c3-117">Definir o tamanho de Olá de valor de toohello pretendido de disco de SO de Olá e atualizar Olá VM da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="a89c3-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="a89c3-118">tamanho do novo Olá deve ser superior ao tamanho do disco existente Olá.</span><span class="sxs-lookup"><span data-stu-id="a89c3-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="a89c3-119">Olá máximo permitido é de 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="a89c3-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="a89c3-120">Atualização Olá VM pode demorar alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="a89c3-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="a89c3-121">Depois de comando de Olá terminar em execução, reinicie Olá VM da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="a89c3-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="a89c3-122">E já está!</span><span class="sxs-lookup"><span data-stu-id="a89c3-122">And that’s it!</span></span> <span data-ttu-id="a89c3-123">Agora RDP nas Olá VM, abra a gestão de computadores (ou gestão de discos) e expanda a unidade de Olá Olá recentemente atribuído espaço a utilizar.</span><span class="sxs-lookup"><span data-stu-id="a89c3-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="a89c3-124">Resumo</span><span class="sxs-lookup"><span data-stu-id="a89c3-124">Summary</span></span>
<span data-ttu-id="a89c3-125">Neste artigo, utilizámos o Azure Resource Manager módulos do Powershell tooexpand Olá disco do SO da máquina virtual IaaS.</span><span class="sxs-lookup"><span data-stu-id="a89c3-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="a89c3-126">Reproduzido abaixo é o script de conclusão de Olá para sua referência:</span><span class="sxs-lookup"><span data-stu-id="a89c3-126">Reproduced below is hello complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="a89c3-127">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="a89c3-127">Next Steps</span></span>
<span data-ttu-id="a89c3-128">Embora este artigo, vamos concentra-se principalmente em expandir disco Olá SO de VM de Olá, hello programada script também pode ser utilizada para expandir Olá dados discos anexados toohello VM alterando uma única linha de código.</span><span class="sxs-lookup"><span data-stu-id="a89c3-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="a89c3-129">Por exemplo, dados de primeiro tooexpand Olá disco ligado toohello VM, substitua Olá ```OSDisk``` objeto do ```StorageProfile``` com ```DataDisks``` matriz e utilizar tooobtain um índice numérico um disco de dados anexados de toofirst de referência, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="a89c3-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="a89c3-130">Do mesmo modo pode fazer referência a VM, utilizando um índice, conforme mostrado acima outro dados discos anexados toohello ou Olá ```Name``` propriedade dos discos de Olá conforme ilustrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="a89c3-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="a89c3-131">Se quiser toofind enviados como tooattach discos tooan VM do Azure Resource Manager, selecionar esta opção [artigo](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a89c3-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

