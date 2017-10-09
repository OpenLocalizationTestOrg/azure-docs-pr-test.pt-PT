---
title: "aaaUse uma VM de resolução de problemas com Olá Azure CLI 2.0 do Linux | Microsoft Docs"
description: "Saiba como tootroubleshoot emite VM com Linux utilizando a ligação Olá SO disco tooa recuperação VM Olá Azure CLI 2.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="98544-103">Resolver problemas de uma VM com Linux ligando Olá SO disco tooa VM de recuperação com Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="98544-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="98544-104">Se a máquina virtual (VM) do Linux encontra um erro de arranque ou de disco, poderá ser necessário tooperform passos no disco rígido virtual Olá próprio de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98544-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="98544-105">Um exemplo comum é uma entrada inválida no `/etc/fstab` Olá VM que impede de ser capaz de tooboot com êxito.</span><span class="sxs-lookup"><span data-stu-id="98544-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="98544-106">Detalhes deste artigo como toouse Olá, Azure CLI 2.0 tooconnect seu virtual rígido disco tooanother VM com Linux toofix quaisquer erros, em seguida, voltar a criar a VM original.</span><span class="sxs-lookup"><span data-stu-id="98544-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="98544-107">Também pode executar estes passos com Olá [CLI do Azure 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98544-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="98544-108">Descrição geral do processo de recuperação</span><span class="sxs-lookup"><span data-stu-id="98544-108">Recovery process overview</span></span>
<span data-ttu-id="98544-109">Olá, processo de resolução de problemas é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="98544-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="98544-110">Elimine Olá VM encontrar problemas, mantendo Olá os discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="98544-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="98544-111">Anexe e montar o disco rígido virtual de Olá tooanother VM com Linux para fins de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98544-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="98544-112">Ligar toohello VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98544-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="98544-113">Editar ficheiros ou executar quaisquer ferramentas toofix problemas no Olá original disco virtual.</span><span class="sxs-lookup"><span data-stu-id="98544-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="98544-114">Desmonte e desanexar o disco rígido virtual Olá de Olá VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98544-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="98544-115">Crie uma VM utilizando Olá original disco virtual.</span><span class="sxs-lookup"><span data-stu-id="98544-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="98544-116">tooperform estes passos, a resolução de problemas precisar de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="98544-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="98544-117">No Olá exemplos a seguir, substitua os nomes de parâmetros com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="98544-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="98544-118">Os nomes dos parâmetros de exemplo incluem `myResourceGroup`, `mystorageaccount`, e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="98544-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="98544-119">Determinar os problemas de arranque</span><span class="sxs-lookup"><span data-stu-id="98544-119">Determine boot issues</span></span>
<span data-ttu-id="98544-120">Examine Olá saída série toodetermine motivo pelo qual a VM não é capaz de tooboot corretamente.</span><span class="sxs-lookup"><span data-stu-id="98544-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="98544-121">Um exemplo comum é uma entrada inválida no `/etc/fstab`, ou Olá subjacente o disco rígido virtual que está a ser eliminado ou movido.</span><span class="sxs-lookup"><span data-stu-id="98544-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="98544-122">Obter registos de arranque Olá com [az vm diagnóstico de arranque get-arranque-registo](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="98544-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="98544-123">Olá exemplo seguinte obtém saída série Olá da VM com o nome de Olá `myVM` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="98544-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="98544-124">Reveja Olá série toodetermine por que motivo está a falhar tooboot Olá VM de saída.</span><span class="sxs-lookup"><span data-stu-id="98544-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="98544-125">Se a saída de série de Olá não está a fornecer qualquer indicação, poderá ser necessário tooreview ficheiros de registo na `/var/log` assim que tiver Olá virtual disco rígido ligado tooa VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98544-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="98544-126">Ver detalhes de disco rígido virtual existente</span><span class="sxs-lookup"><span data-stu-id="98544-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="98544-127">Antes de pode anexar o disco rígido virtual (VHD) de tooanother VM, terá de tooidentify Olá URI de disco de SO Olá.</span><span class="sxs-lookup"><span data-stu-id="98544-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="98544-128">Ver informações sobre a VM com [mostrar de vm az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="98544-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="98544-129">Olá utilize `--query` disco de SO de toohello do sinalizador tooextract Olá URI.</span><span class="sxs-lookup"><span data-stu-id="98544-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="98544-130">Olá exemplo seguinte obtém informações do disco para a VM com o nome de Olá `myVM` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="98544-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="98544-131">Olá URI é demasiado semelhante**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="98544-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="98544-132">Eliminar VM existente</span><span class="sxs-lookup"><span data-stu-id="98544-132">Delete existing VM</span></span>
<span data-ttu-id="98544-133">Os discos rígidos virtuais e as VMs são dois recursos diferentes do Azure.</span><span class="sxs-lookup"><span data-stu-id="98544-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="98544-134">Um disco rígido virtual é onde são armazenadas Olá sistema operativo, as aplicações e configurações.</span><span class="sxs-lookup"><span data-stu-id="98544-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="98544-135">Olá própria VM é apenas metadados, que definem o tamanho de Olá ou localização e referencia recursos, tais como um disco rígido virtual ou o cartão de interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="98544-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="98544-136">Cada disco rígido virtual tem uma concessão atribuída quando ligado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="98544-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="98544-137">Embora os discos de dados podem ser ligados e anular a exposição mesmo enquanto Olá VM está em execução, o disco do SO Olá não pode ser desligado, a menos que Olá recurso VM é eliminado.</span><span class="sxs-lookup"><span data-stu-id="98544-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="98544-138">concessão de Olá continua disco de SO de Olá tooassociate com uma VM, mesmo quando se encontra num estado parado e desalocado essa VM.</span><span class="sxs-lookup"><span data-stu-id="98544-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="98544-139">Olá primeiro passo toorecover a VM é o recurso VM de Olá toodelete próprio.</span><span class="sxs-lookup"><span data-stu-id="98544-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="98544-140">A eliminar Olá VM deixa Olá os discos rígidos virtuais na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="98544-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="98544-141">Depois de Olá que VM é eliminada, anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolva os erros de Olá.</span><span class="sxs-lookup"><span data-stu-id="98544-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="98544-142">Eliminar Olá VM com [az vm eliminar](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="98544-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="98544-143">Olá, seguindo as eliminações de exemplo Olá VM com o nome `myVM` do grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="98544-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="98544-144">Aguarde até que Olá VM terminou a eliminação antes de anexar o disco rígido virtual de Olá tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="98544-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="98544-145">tem de concessão de Olá no disco rígido virtual Olá que associa-Olá VM toobe lançada antes de pode anexar o disco rígido virtual de Olá tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="98544-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="98544-146">Anexar tooanother de disco rígido virtual existente VM</span><span class="sxs-lookup"><span data-stu-id="98544-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="98544-147">Para Olá, em seguida alguns passos, utilizar outra VM para fins de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98544-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="98544-148">Anexar Olá toothis do disco rígido virtual existente toobrowse VM de resolução de problemas e editar o conteúdo do disco Olá.</span><span class="sxs-lookup"><span data-stu-id="98544-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="98544-149">Este processo permite-lhe toocorrect quaisquer erros de configuração ou a aplicação adicional de revisão ou o sistema de ficheiros de registo por exemplo.</span><span class="sxs-lookup"><span data-stu-id="98544-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="98544-150">Escolha ou crie outro toouse VM para fins de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98544-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="98544-151">Anexar o disco rígido virtual existente por Olá com [az unmanaged-disco da vm ligar](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="98544-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="98544-152">Quando anexa Olá existente disco virtual, especifique o disco de toohello URI de Olá obtido no Olá anterior `az vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="98544-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="98544-153">Olá exemplo seguinte anexa um toohello de disco rígido virtual existente VM com o nome de resolução de problemas `myVMRecovery` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="98544-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="98544-154">Montar o disco de dados anexados Olá</span><span class="sxs-lookup"><span data-stu-id="98544-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="98544-155">Olá exemplos seguintes de detalhe os passos de Olá necessários numa VM com Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="98544-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="98544-156">Se estiver a utilizar um distro diferente do Linux, como Red Hat Enterprise Linux ou SUSE, Olá localizações de ficheiros de registo e `mount` os comandos podem ser ligeiramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="98544-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="98544-157">Consulte a documentação do toohello para sua distro específico para alterações adequadas do Olá nos comandos.</span><span class="sxs-lookup"><span data-stu-id="98544-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="98544-158">Resolução de problemas de VM com as credenciais adequadas Olá tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="98544-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="98544-159">Se este disco Olá primeiro dados disco ligado tooyour VM de resolução de problemas, disco de Olá, provavelmente, está ligado demasiado`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="98544-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="98544-160">Utilize `dmseg` tooview discos ligados:</span><span class="sxs-lookup"><span data-stu-id="98544-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="98544-161">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="98544-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="98544-162">Olá anterior exemplo, disco de SO de Olá é em `/dev/sda` e disco temporário Olá fornecido para cada VM está em `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="98544-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="98544-163">Se tiver vários discos de dados, devem estar no `/dev/sdd`, `/dev/sde`, e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="98544-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="98544-164">Crie um diretório toomount o disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="98544-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="98544-165">Olá exemplo seguinte cria um diretório com o nome `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="98544-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="98544-166">Se tiver várias partições no seu disco rígido virtual existente, monte partição Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="98544-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="98544-167">Olá exemplo seguinte monta primeira partição primária Olá em `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="98544-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="98544-168">Melhor prática é toomount discos de dados em VMs no Azure com Olá Identificador exclusivo universalmente (UUID) do disco rígido virtual do Olá.</span><span class="sxs-lookup"><span data-stu-id="98544-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="98544-169">Para este cenário de resolução de problemas curto, montagem Olá disco rígido virtual utilizando Olá UUID não é necessário.</span><span class="sxs-lookup"><span data-stu-id="98544-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="98544-170">No entanto, na utilização normal, editar `/etc/fstab` toomount os discos rígidos virtuais com o nome de dispositivo em vez de pode provocar um UUID Olá VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="98544-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="98544-171">Resolva os problemas no disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="98544-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="98544-172">Com Olá disco rígido virtual existente montado, agora pode efetuar qualquer manutenção e passos de resolução de problemas, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="98544-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="98544-173">Assim que tiver resolvido problemas Olá, continue com Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="98544-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="98544-174">Desmonte e desanexar o disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="98544-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="98544-175">Depois dos erros serem resolvidos, desmonte e desanexar Olá existente disco virtual de VM resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98544-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="98544-176">Não é possível utilizar o disco rígido virtual com quaisquer outro VM até que a concessão de Olá anexar toohello de disco rígido virtual Olá VM de resolução de problemas é libertado.</span><span class="sxs-lookup"><span data-stu-id="98544-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="98544-177">De Olá tooyour sessão SSH VM de resolução de problemas, desmonte Olá existente disco virtual.</span><span class="sxs-lookup"><span data-stu-id="98544-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="98544-178">Altere primeiro fora do diretório de principal de Olá do ponto de montagem:</span><span class="sxs-lookup"><span data-stu-id="98544-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="98544-179">Desmonte agora Olá existente disco virtual.</span><span class="sxs-lookup"><span data-stu-id="98544-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="98544-180">Olá exemplo seguinte unmounts dispositivo Olá em `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="98544-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="98544-181">Agora anular a exposição do disco rígido virtual Olá de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="98544-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="98544-182">Sair Olá SSH sessão tooyour VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="98544-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="98544-183">Olá lista ligado tooyour de discos de dados resolução de problemas de VM com [az vm unmanaged-lista de discos](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="98544-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="98544-184">Olá listas Olá discos de dados de exemplo seguinte ligado toohello VM com o nome `myVMRecovery` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="98544-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="98544-185">Tenha em atenção Olá o nome do seu disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="98544-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="98544-186">Por exemplo, o nome de Olá de um disco com Olá URI de **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** é **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="98544-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="98544-187">Exposição do disco de dados de Olá da sua VM [az unmanaged-disco da vm desanexar](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="98544-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="98544-188">Olá exemplo seguinte Desanexa disco Olá chamado `myVHD` da VM com o nome de Olá `myVMRecovery` no Olá `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="98544-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="98544-189">Criar a VM de disco rígido original</span><span class="sxs-lookup"><span data-stu-id="98544-189">Create VM from original hard disk</span></span>
<span data-ttu-id="98544-190">toocreate uma VM a partir do seu disco rígido virtual original, utilize [este modelo Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="98544-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="98544-191">modelo JSON Olá está em Olá seguinte hiperligação:</span><span class="sxs-lookup"><span data-stu-id="98544-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="98544-192">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-Templates/Master/201-VM-Specialized-VHD/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="98544-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="98544-193">Olá modelo implementa uma VM utilizando Olá URI de VHD de Olá comando anterior.</span><span class="sxs-lookup"><span data-stu-id="98544-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="98544-194">Implementar a modelo Olá com [criar a implementação do grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="98544-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="98544-195">Fornecer Olá URI tooyour original VHD e, em seguida, especifique o tipo de SO de Olá, o tamanho da VM e o nome VM da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="98544-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="98544-196">Reativar o diagnóstico de arranque</span><span class="sxs-lookup"><span data-stu-id="98544-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="98544-197">Ao criar a VM de Olá existente disco virtual, diagnóstico de arranque pode não ser ativado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="98544-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="98544-198">Ativar o diagnóstico de arranque com [ativar o diagnóstico de arranque do vm az](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="98544-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="98544-199">Olá exemplo seguinte ativa a extensão de diagnóstico de Olá na VM com o nome de Olá `myDeployedVM` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="98544-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="98544-200">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="98544-200">Next steps</span></span>
<span data-ttu-id="98544-201">Se estiver a ter problemas em ligar tooyour VM, consulte [resolver problemas de SSH ligações tooan VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98544-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="98544-202">Para problemas com a aceder a aplicações em execução numa VM, consulte [resolver problemas de conectividade de aplicação numa VM com Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98544-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
