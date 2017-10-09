---
title: "aaaUse uma VM de resolução de problemas no portal do Azure de Olá do Linux | Microsoft Docs"
description: "Saiba como tootroubleshoot problemas da máquina virtual Linux utilizando a ligação Olá SO disco tooa recuperação VM Olá portal do Azure"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="043ce-103">Resolver problemas de uma VM com Linux ao anexar a VM de recuperação Olá SO disco tooa utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="043ce-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="043ce-104">Se a máquina virtual (VM) do Linux encontra um erro de arranque ou de disco, poderá ser necessário tooperform passos no disco rígido virtual Olá próprio de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="043ce-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="043ce-105">Um exemplo comum é uma entrada inválida no `/etc/fstab` Olá VM que impede de ser capaz de tooboot com êxito.</span><span class="sxs-lookup"><span data-stu-id="043ce-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="043ce-106">Detalhes deste artigo como toouse Olá tooconnect portal do Azure a virtual rígido disco tooanother VM com Linux toofix quaisquer erros, em seguida, voltar a criar a VM original.</span><span class="sxs-lookup"><span data-stu-id="043ce-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="043ce-107">Descrição geral do processo de recuperação</span><span class="sxs-lookup"><span data-stu-id="043ce-107">Recovery process overview</span></span>
<span data-ttu-id="043ce-108">Olá, processo de resolução de problemas é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="043ce-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="043ce-109">Elimine Olá VM encontrar problemas, mantendo Olá os discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="043ce-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="043ce-110">Anexe e montar o disco rígido virtual de Olá tooanother VM com Linux para fins de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="043ce-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="043ce-111">Ligar toohello VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="043ce-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="043ce-112">Editar ficheiros ou executar quaisquer ferramentas toofix problemas no Olá original disco virtual.</span><span class="sxs-lookup"><span data-stu-id="043ce-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="043ce-113">Desmonte e desanexar o disco rígido virtual Olá de Olá VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="043ce-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="043ce-114">Crie uma VM utilizando Olá original disco virtual.</span><span class="sxs-lookup"><span data-stu-id="043ce-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="043ce-115">Determinar os problemas de arranque</span><span class="sxs-lookup"><span data-stu-id="043ce-115">Determine boot issues</span></span>
<span data-ttu-id="043ce-116">Examine o diagnóstico de arranque Olá e toodetermine de captura de ecrã VM por que razão a VM não é possível tooboot corretamente.</span><span class="sxs-lookup"><span data-stu-id="043ce-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="043ce-117">Um exemplo comum é uma entrada inválida no `/etc/fstab`, ou um subjacente disco de rígido virtual que está a ser eliminado ou movido.</span><span class="sxs-lookup"><span data-stu-id="043ce-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="043ce-118">Selecione a VM no portal de Olá e, em seguida, desloque para baixo toohello **suporte + resolução de problemas** secção.</span><span class="sxs-lookup"><span data-stu-id="043ce-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="043ce-119">Clique em **diagnóstico de arranque** mensagens de consola tooview hello transmissão em fluxo da VM.</span><span class="sxs-lookup"><span data-stu-id="043ce-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="043ce-120">Consola de Olá revisão regista toosee se pode determinar o motivo pelo qual hello VM verificou um problema.</span><span class="sxs-lookup"><span data-stu-id="043ce-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="043ce-121">Olá exemplo seguinte mostra que uma VM bloqueada no modo de manutenção que necessite de interação manual:</span><span class="sxs-lookup"><span data-stu-id="043ce-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Visualizar VM diagnóstico de arranque consola registos](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="043ce-123">Também pode clicar em **captura de ecrã** em Olá parte superior do Olá arranque diagnóstico registo toodownload uma captura de captura de ecrã do Olá VM.</span><span class="sxs-lookup"><span data-stu-id="043ce-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="043ce-124">Ver detalhes de disco rígido virtual existente</span><span class="sxs-lookup"><span data-stu-id="043ce-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="043ce-125">Antes de pode anexar o disco rígido virtual de tooanother VM, terá de nome de Olá tooidentify de Olá de disco rígido virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="043ce-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="043ce-126">Selecione o grupo de recursos a partir do portal de Olá, em seguida, selecione a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="043ce-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="043ce-127">Clique em **Blobs**, como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="043ce-127">Click **Blobs**, as in hello following example:</span></span>

![Selecione os blobs de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="043ce-129">Normalmente, tem um contentor com o nome **vhds** que armazena os discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="043ce-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="043ce-130">Selecione o contentor de Olá tooview uma lista de discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="043ce-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="043ce-131">Nome de Olá nota do seu VHD (prefixo Olá é normalmente nome Olá da sua VM):</span><span class="sxs-lookup"><span data-stu-id="043ce-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Identificar o VHD no contentor de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="043ce-133">Selecione o disco rígido virtual existente na lista de Olá e copie o URL de Olá para utilização no Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="043ce-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Copie o URL de disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="043ce-135">Eliminar VM existente</span><span class="sxs-lookup"><span data-stu-id="043ce-135">Delete existing VM</span></span>
<span data-ttu-id="043ce-136">Os discos rígidos virtuais e as VMs são dois recursos diferentes do Azure.</span><span class="sxs-lookup"><span data-stu-id="043ce-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="043ce-137">Um disco rígido virtual é onde são armazenadas Olá sistema operativo, as aplicações e configurações.</span><span class="sxs-lookup"><span data-stu-id="043ce-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="043ce-138">Olá própria VM é apenas metadados, que definem o tamanho de Olá ou localização e referencia recursos, tais como um disco rígido virtual ou o cartão de interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="043ce-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="043ce-139">Cada disco rígido virtual tem uma concessão atribuída quando ligado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="043ce-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="043ce-140">Embora os discos de dados podem ser ligados e anular a exposição mesmo enquanto Olá VM está em execução, o disco do SO Olá não pode ser desligado, a menos que Olá recurso VM é eliminado.</span><span class="sxs-lookup"><span data-stu-id="043ce-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="043ce-141">concessão de Olá continua disco de SO de Olá tooassociate com uma VM, mesmo quando se encontra num estado parado e desalocado essa VM.</span><span class="sxs-lookup"><span data-stu-id="043ce-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="043ce-142">Olá primeiro passo toorecover a VM é o recurso VM de Olá toodelete próprio.</span><span class="sxs-lookup"><span data-stu-id="043ce-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="043ce-143">A eliminar Olá VM deixa Olá os discos rígidos virtuais na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="043ce-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="043ce-144">Depois de Olá que VM é eliminada, anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolva os erros de Olá.</span><span class="sxs-lookup"><span data-stu-id="043ce-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="043ce-145">Selecione a VM no portal de Olá, em seguida, clique em **eliminar**:</span><span class="sxs-lookup"><span data-stu-id="043ce-145">Select your VM in hello portal, then click **Delete**:</span></span>

![VM arranque diagnóstico captura de ecrã com erro de arranque](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="043ce-147">Aguarde até que Olá VM terminou a eliminação antes de anexar o disco rígido virtual de Olá tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="043ce-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="043ce-148">tem de concessão de Olá no disco rígido virtual Olá que associa-Olá VM toobe lançada antes de pode anexar o disco rígido virtual de Olá tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="043ce-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="043ce-149">Anexar tooanother de disco rígido virtual existente VM</span><span class="sxs-lookup"><span data-stu-id="043ce-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="043ce-150">Para Olá, em seguida alguns passos, utilizar outra VM para fins de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="043ce-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="043ce-151">Anexar Olá toothis do disco rígido virtual existente VM toobe capaz de toobrowse de resolução de problemas e editar o conteúdo do disco Olá.</span><span class="sxs-lookup"><span data-stu-id="043ce-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="043ce-152">Este processo permite-lhe toocorrect quaisquer erros de configuração ou a aplicação adicional de revisão ou o sistema de ficheiros de registo por exemplo.</span><span class="sxs-lookup"><span data-stu-id="043ce-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="043ce-153">Escolha ou crie outro toouse VM para fins de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="043ce-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="043ce-154">Selecione o grupo de recursos a partir do portal de Olá, em seguida, selecione a VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="043ce-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="043ce-155">Selecione **discos** e, em seguida, clique em **anexar existente**:</span><span class="sxs-lookup"><span data-stu-id="043ce-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Anexar o disco existente no portal de Olá](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="043ce-157">tooselect o disco rígido virtual existente, clique em **ficheiro VHD**:</span><span class="sxs-lookup"><span data-stu-id="043ce-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Procurar o VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="043ce-159">Selecionar a sua conta do storage e um contentor, em seguida, clique o VHD existente.</span><span class="sxs-lookup"><span data-stu-id="043ce-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="043ce-160">Clique em Olá **selecione** botão tooconfirm à sua escolha:</span><span class="sxs-lookup"><span data-stu-id="043ce-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Selecionar o seu VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="043ce-162">Com o VHD selecionado agora, clique em **OK** tooattach Olá disco rígido virtual existente:</span><span class="sxs-lookup"><span data-stu-id="043ce-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Confirme a anexar o disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="043ce-164">Após alguns segundos, Olá **discos** painel para a VM lista o disco rígido virtual ligado como um disco de dados:</span><span class="sxs-lookup"><span data-stu-id="043ce-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Disco rígido virtual já existente anexado como disco de dados](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="043ce-166">Montar o disco de dados anexados Olá</span><span class="sxs-lookup"><span data-stu-id="043ce-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="043ce-167">Olá exemplos seguintes de detalhe os passos de Olá necessários numa VM com Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="043ce-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="043ce-168">Se estiver a utilizar um distro diferente do Linux, como Red Hat Enterprise Linux ou SUSE, Olá localizações de ficheiros de registo e `mount` os comandos podem ser ligeiramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="043ce-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="043ce-169">Consulte a documentação do toohello para sua distro específico para alterações adequadas do Olá nos comandos.</span><span class="sxs-lookup"><span data-stu-id="043ce-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="043ce-170">Resolução de problemas de VM com as credenciais adequadas Olá tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="043ce-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="043ce-171">Se este disco Olá primeiro dados disco ligado tooyour VM de resolução de problemas, provavelmente, está a ligado demasiado`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="043ce-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="043ce-172">Utilize `dmseg` toolist discos ligados:</span><span class="sxs-lookup"><span data-stu-id="043ce-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="043ce-173">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="043ce-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="043ce-174">Olá anterior exemplo, disco de SO de Olá é em `/dev/sda` e disco temporário Olá fornecido para cada VM está em `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="043ce-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="043ce-175">Se tiver vários discos de dados, devem estar no `/dev/sdd`, `/dev/sde`, e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="043ce-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="043ce-176">Crie um diretório toomount o disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="043ce-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="043ce-177">Olá exemplo seguinte cria um diretório com o nome `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="043ce-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="043ce-178">Se tiver várias partições no seu disco rígido virtual existente, monte partição Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="043ce-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="043ce-179">Olá exemplo seguinte monta primeira partição primária Olá em `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="043ce-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="043ce-180">Melhor prática é toomount discos de dados em VMs no Azure com Olá Identificador exclusivo universalmente (UUID) do disco rígido virtual do Olá.</span><span class="sxs-lookup"><span data-stu-id="043ce-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="043ce-181">Para este cenário de resolução de problemas curto, montagem Olá disco rígido virtual utilizando Olá UUID não é necessário.</span><span class="sxs-lookup"><span data-stu-id="043ce-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="043ce-182">No entanto, na utilização normal, editar `/etc/fstab` toomount os discos rígidos virtuais com o nome de dispositivo em vez de pode provocar um UUID Olá VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="043ce-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="043ce-183">Resolva os problemas no disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="043ce-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="043ce-184">Com Olá disco rígido virtual existente montado, agora pode efetuar qualquer manutenção e passos de resolução de problemas, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="043ce-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="043ce-185">Assim que tiver resolvido problemas Olá, continue com Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="043ce-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="043ce-186">Desmonte e desanexar o disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="043ce-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="043ce-187">Depois dos erros serem resolvidos, desligue o disco rígido virtual existente por Olá da sua VM de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="043ce-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="043ce-188">Não é possível utilizar o disco rígido virtual com quaisquer outro VM até que a concessão de Olá anexar toohello de disco rígido virtual Olá VM de resolução de problemas é libertado.</span><span class="sxs-lookup"><span data-stu-id="043ce-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="043ce-189">De Olá tooyour sessão SSH VM de resolução de problemas, desmonte Olá existente disco virtual.</span><span class="sxs-lookup"><span data-stu-id="043ce-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="043ce-190">Altere primeiro fora do diretório de principal de Olá do ponto de montagem:</span><span class="sxs-lookup"><span data-stu-id="043ce-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="043ce-191">Desmonte agora Olá existente disco virtual.</span><span class="sxs-lookup"><span data-stu-id="043ce-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="043ce-192">Olá exemplo seguinte unmounts dispositivo Olá em `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="043ce-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="043ce-193">Agora anular a exposição do disco rígido virtual Olá de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="043ce-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="043ce-194">Selecione a VM no portal de Olá e clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="043ce-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="043ce-195">Selecione o disco rígido virtual existente e, em seguida, clique em **anulação de exposições**:</span><span class="sxs-lookup"><span data-stu-id="043ce-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Exposição do disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="043ce-197">Aguarde até que Olá VM tem exposição anulada com êxito o disco de dados de Olá antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="043ce-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="043ce-198">Criar a VM de disco rígido original</span><span class="sxs-lookup"><span data-stu-id="043ce-198">Create VM from original hard disk</span></span>
<span data-ttu-id="043ce-199">toocreate uma VM a partir do seu disco rígido virtual original, utilize [este modelo Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="043ce-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="043ce-200">modelo de Olá implementa uma VM numa rede virtual existente, utilizando Olá URL de VHD de Olá comando anterior.</span><span class="sxs-lookup"><span data-stu-id="043ce-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="043ce-201">Clique em Olá **implementar tooAzure** botão da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="043ce-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![Implementar a VM a partir do modelo a partir do GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="043ce-203">modelo de Olá está carregado Olá portal do Azure para a implementação.</span><span class="sxs-lookup"><span data-stu-id="043ce-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="043ce-204">Introduza os nomes de Olá para a sua nova VM e os recursos do Azure existentes e cole Olá URL tooyour disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="043ce-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="043ce-205">implementação de Olá toobegin, clique em **Compra**:</span><span class="sxs-lookup"><span data-stu-id="043ce-205">toobegin hello deployment, click **Purchase**:</span></span>

![Implementar a VM a partir do modelo](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="043ce-207">Reativar o diagnóstico de arranque</span><span class="sxs-lookup"><span data-stu-id="043ce-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="043ce-208">Ao criar a VM de Olá existente disco virtual, diagnóstico de arranque pode não ser ativado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="043ce-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="043ce-209">toocheck Olá estado de diagnóstico de arranque e ative se for necessário, selecione a VM no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="043ce-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="043ce-210">Em **monitorização**, clique em **as definições de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="043ce-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="043ce-211">Certifique-se de estado de Olá **no**, e Olá marca de verificação junto demasiado**diagnóstico de arranque** está selecionada.</span><span class="sxs-lookup"><span data-stu-id="043ce-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="043ce-212">Se efetuar alterações, clique em **guardar**:</span><span class="sxs-lookup"><span data-stu-id="043ce-212">If you make any changes, click **Save**:</span></span>

![Atualizar as definições de diagnóstico de arranque](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="043ce-214">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="043ce-214">Next steps</span></span>
<span data-ttu-id="043ce-215">Se estiver a ter problemas em ligar tooyour VM, consulte [resolver problemas de SSH ligações tooan VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="043ce-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="043ce-216">Para problemas com a aceder a aplicações em execução numa VM, consulte [resolver problemas de conectividade de aplicação numa VM com Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="043ce-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="043ce-217">Para obter mais informações sobre como utilizar o Gestor de recursos, consulte [descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="043ce-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
