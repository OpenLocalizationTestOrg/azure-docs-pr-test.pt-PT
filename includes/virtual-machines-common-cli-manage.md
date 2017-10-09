<span data-ttu-id="7b4e0-101">Olá, Azure CLI 2.0 permite-lhe toocreate e gerir os recursos do Azure no macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="7b4e0-101">hello Azure CLI 2.0 allows you toocreate and manage your Azure resources on macOS, Linux, and Windows.</span></span> <span data-ttu-id="7b4e0-102">Este artigo fornece detalhes sobre algumas das Olá mais comuns comandos toocreate e gerir máquinas virtuais (VMs).</span><span class="sxs-lookup"><span data-stu-id="7b4e0-102">This article details some of hello most common commands toocreate and manage virtual machines (VMs).</span></span>

<span data-ttu-id="7b4e0-103">Este artigo requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7b4e0-103">This article requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7b4e0-104">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="7b4e0-104">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7b4e0-105">Se precisar de tooupgrade, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7b4e0-105">If you need tooupgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="7b4e0-106">Também pode utilizar [nuvem Shell](/azure/cloud-shell/quickstart) partir do seu browser.</span><span class="sxs-lookup"><span data-stu-id="7b4e0-106">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="7b4e0-107">Comandos básicos do Azure Resource Manager na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7b4e0-107">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="7b4e0-108">Para obter mais ajuda com os parâmetros da linha de comandos específicos e as opções, pode utilizar opções de ajuda do comando online Olá e escrevendo `az <command> <subcommand> --help`.</span><span class="sxs-lookup"><span data-stu-id="7b4e0-108">For more detailed help with specific command line switches and options, you can use hello online command help and options by typing `az <command> <subcommand> --help`.</span></span>

### <a name="create-vms"></a><span data-ttu-id="7b4e0-109">Criar VMs</span><span class="sxs-lookup"><span data-stu-id="7b4e0-109">Create VMs</span></span>
| <span data-ttu-id="7b4e0-110">Tarefa</span><span class="sxs-lookup"><span data-stu-id="7b4e0-110">Task</span></span> | <span data-ttu-id="7b4e0-111">Comandos da CLI Azure</span><span class="sxs-lookup"><span data-stu-id="7b4e0-111">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="7b4e0-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7b4e0-112">Create a resource group</span></span> | `az group create --name myResourceGroup --location eastus` |
| <span data-ttu-id="7b4e0-113">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="7b4e0-113">Create a Linux VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| <span data-ttu-id="7b4e0-114">Criar uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="7b4e0-114">Create a Windows VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a><span data-ttu-id="7b4e0-115">Gerir o estado VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-115">Manage VM state</span></span>
| <span data-ttu-id="7b4e0-116">Tarefa</span><span class="sxs-lookup"><span data-stu-id="7b4e0-116">Task</span></span> | <span data-ttu-id="7b4e0-117">Comandos da CLI Azure</span><span class="sxs-lookup"><span data-stu-id="7b4e0-117">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="7b4e0-118">Iniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-118">Start a VM</span></span> | `az vm start --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="7b4e0-119">Parar uma VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-119">Stop a VM</span></span> | `az vm stop --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="7b4e0-120">Desalocar uma VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-120">Deallocate a VM</span></span> | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="7b4e0-121">Reiniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-121">Restart a VM</span></span> | `az vm restart --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="7b4e0-122">Reimplementar uma VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-122">Redeploy a VM</span></span> | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="7b4e0-123">Eliminar uma VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-123">Delete a VM</span></span> | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a><span data-ttu-id="7b4e0-124">Obter as informações de VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-124">Get VM info</span></span>
| <span data-ttu-id="7b4e0-125">Tarefa</span><span class="sxs-lookup"><span data-stu-id="7b4e0-125">Task</span></span> | <span data-ttu-id="7b4e0-126">Comandos da CLI Azure</span><span class="sxs-lookup"><span data-stu-id="7b4e0-126">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="7b4e0-127">Listar VMs</span><span class="sxs-lookup"><span data-stu-id="7b4e0-127">List VMs</span></span> | `az vm list` |
| <span data-ttu-id="7b4e0-128">Obter informações sobre uma VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-128">Get information about a VM</span></span> | `az vm show --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="7b4e0-129">Obter a utilização de recursos de VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-129">Get usage of VM resources</span></span> | `az vm list-usage --location eastus` |
| <span data-ttu-id="7b4e0-130">Obter todos os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="7b4e0-130">Get all available VM sizes</span></span> | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a><span data-ttu-id="7b4e0-131">Discos e imagens</span><span class="sxs-lookup"><span data-stu-id="7b4e0-131">Disks and images</span></span>
| <span data-ttu-id="7b4e0-132">Tarefa</span><span class="sxs-lookup"><span data-stu-id="7b4e0-132">Task</span></span> | <span data-ttu-id="7b4e0-133">Comandos da CLI Azure</span><span class="sxs-lookup"><span data-stu-id="7b4e0-133">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="7b4e0-134">Adicionar um tooa de disco de dados VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-134">Add a data disk tooa VM</span></span> | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| <span data-ttu-id="7b4e0-135">Remover um disco de dados de uma VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-135">Remove a data disk from a VM</span></span> | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| <span data-ttu-id="7b4e0-136">Redimensionar um disco</span><span class="sxs-lookup"><span data-stu-id="7b4e0-136">Resize a disk</span></span> | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| <span data-ttu-id="7b4e0-137">Tirar um instantâneo de um disco</span><span class="sxs-lookup"><span data-stu-id="7b4e0-137">Snapshot a disk</span></span> | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| <span data-ttu-id="7b4e0-138">Criar a imagem de uma VM</span><span class="sxs-lookup"><span data-stu-id="7b4e0-138">Create image of a VM</span></span> | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| <span data-ttu-id="7b4e0-139">Criar a VM da imagem</span><span class="sxs-lookup"><span data-stu-id="7b4e0-139">Create VM from image</span></span> | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a><span data-ttu-id="7b4e0-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7b4e0-140">Next steps</span></span>
<span data-ttu-id="7b4e0-141">Para obter exemplos adicionais de comandos da CLI Olá, consulte Olá [criar e gerir VMs com Linux com Olá CLI do Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b4e0-141">For additional examples of hello CLI commands, see hello [Create and Manage Linux VMs with hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span></span>

