---
title: "Cópia de segurança de VMs com Linux do Azure | Microsoft Docs"
description: "Proteger as VMs com Linux através de cópias de segurança utilizando a cópia de segurança do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="5ad37-103">Cópia de segurança de computadores virtuais Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="5ad37-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="5ad37-104">Pode criar cópias de segurança em intervalos regulares para manter os seus dados protegidos.</span><span class="sxs-lookup"><span data-stu-id="5ad37-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="5ad37-105">Cópia de segurança do Azure cria pontos de recuperação que estão armazenados no cofres de recuperação com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="5ad37-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="5ad37-106">Quando restaurar a partir de um ponto de recuperação, pode restaurar Olá VM todo ou ficheiros apenas específicos.</span><span class="sxs-lookup"><span data-stu-id="5ad37-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="5ad37-107">Este artigo explica como toorestore um único ficheiro tooa nginx em execução de VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="5ad37-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="5ad37-108">Se ainda não tiver um toouse VM, pode criar um utilizando Olá [início rápido do Linux](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5ad37-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="5ad37-109">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="5ad37-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5ad37-110">Criar uma cópia de segurança de uma VM</span><span class="sxs-lookup"><span data-stu-id="5ad37-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="5ad37-111">Agendar uma cópia de segurança diária</span><span class="sxs-lookup"><span data-stu-id="5ad37-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="5ad37-112">Restaurar um ficheiro a partir de uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="5ad37-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="5ad37-113">Descrição geral da Cópia de Segurança</span><span class="sxs-lookup"><span data-stu-id="5ad37-113">Backup overview</span></span>

<span data-ttu-id="5ad37-114">Quando Olá serviço cópia de segurança do Azure inicia uma cópia de segurança, aciona tootake de extensão de cópia de segurança de Olá um instantâneo de ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="5ad37-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="5ad37-115">Olá serviço de cópia de segurança do Azure utiliza Olá _VMSnapshotLinux_ extensão no Linux.</span><span class="sxs-lookup"><span data-stu-id="5ad37-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="5ad37-116">extensão de Olá é instalado durante a cópia de segurança Olá primeira VM se Olá VM está em execução.</span><span class="sxs-lookup"><span data-stu-id="5ad37-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="5ad37-117">Se hello VM não está em execução, Olá serviço de cópia de segurança tira um instantâneo de Olá subjacente armazenamento (uma vez que não existem escritas de aplicação ocorrerem ao hello que VM está parada).</span><span class="sxs-lookup"><span data-stu-id="5ad37-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="5ad37-118">Por predefinição, cópia de segurança do Azure assume uma sistema consistente cópia de segurança para a VM com Linux, mas pode ser configurado tootake [aplicação cópia de segurança consistente utilizando o pré- script de e script pós-implementação framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="5ad37-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="5ad37-119">Depois de Olá serviço de cópia de segurança do Azure tira instantâneos Olá, dados de Olá são transferidos toohello cofre.</span><span class="sxs-lookup"><span data-stu-id="5ad37-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="5ad37-120">eficiência toomaximize, o serviço de Olá identifica e transfere apenas os blocos de Olá dos dados que foram alterados desde a cópia de segurança anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="5ad37-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="5ad37-121">Quando a transferência de dados de Olá estiver concluída, o instantâneo de Olá é removido e é criado um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="5ad37-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="5ad37-122">Criar uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="5ad37-122">Create a backup</span></span>
<span data-ttu-id="5ad37-123">Crie uma simple agendada diária cópia de segurança tooa cofre dos serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="5ad37-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="5ad37-124">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5ad37-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5ad37-125">No menu de Olá Olá esquerda, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="5ad37-126">Na lista de Olá, selecione uma VM tooback cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="5ad37-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="5ad37-127">No painel VM Olá, no Olá **definições** secção, clique em **cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="5ad37-128">Olá **ativar cópia de segurança** abre o painel.</span><span class="sxs-lookup"><span data-stu-id="5ad37-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="5ad37-129">No **cofre dos serviços de recuperação**, clique em **criar nova** e forneça o nome de Olá para novo cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ad37-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="5ad37-130">Um novo cofre é criado na Olá mesmo grupo de recursos e localização da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ad37-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="5ad37-131">Clique em **política de cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-131">Click **Backup policy**.</span></span> <span data-ttu-id="5ad37-132">Neste exemplo, mantenha as predefinições de Olá e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="5ad37-133">No Olá **ativar cópia de segurança** painel, clique em **ativar a cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="5ad37-134">Esta ação cria uma cópia de segurança diária, com base numa agenda predefinida de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ad37-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="5ad37-135">toocreate um ponto de recuperação inicial, no Olá **cópia de segurança** painel clique **cópia de segurança agora**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="5ad37-136">No Olá **cópia de segurança agora** painel, clique em ícone de calendário Olá, utilize Olá de tooselect de controlo do Olá calendário último dia deste ponto de recuperação é mantido e clique em **cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="5ad37-137">No Olá **cópia de segurança** painel para a VM, irá ver o número de Olá de pontos de recuperação que estão concluídos.</span><span class="sxs-lookup"><span data-stu-id="5ad37-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Pontos de recuperação](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="5ad37-139">primeira cópia de segurança Olá demora cerca de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="5ad37-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="5ad37-140">Continuar a parte seguinte do toohello deste tutorial depois de concluída a cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="5ad37-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="5ad37-141">Restaurar um ficheiro</span><span class="sxs-lookup"><span data-stu-id="5ad37-141">Restore a file</span></span>

<span data-ttu-id="5ad37-142">Se acidentalmente eliminar ou se o ficheiro de tooa de alterações, pode utilizar o ficheiro de Olá toorecover de recuperação de ficheiros do seu Cofre de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="5ad37-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="5ad37-143">Recuperação de ficheiros utiliza um script que é executado no Olá VM, ponto de recuperação de Olá toomount como unidade local.</span><span class="sxs-lookup"><span data-stu-id="5ad37-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="5ad37-144">Estas unidades permanecerá montadas para 12 horas para que possa copiar os ficheiros do ponto de recuperação Olá e restaurá-las toohello VM.</span><span class="sxs-lookup"><span data-stu-id="5ad37-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="5ad37-145">Neste exemplo, mostramos como toorecover Olá predefinido nginx página web /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="5ad37-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="5ad37-146">endereço IP público de Olá do nosso VM neste exemplo é *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="5ad37-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="5ad37-147">Pode encontrar o endereço IP Olá da sua utilização de vm:</span><span class="sxs-lookup"><span data-stu-id="5ad37-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="5ad37-148">No computador local, abra um browser e o tipo de endereço IP público Olá da VM toosee Olá predefinido nginx página web.</span><span class="sxs-lookup"><span data-stu-id="5ad37-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![Nginx predefinido de página web](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="5ad37-150">SSH para a VM.</span><span class="sxs-lookup"><span data-stu-id="5ad37-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="5ad37-151">Elimine /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="5ad37-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="5ad37-152">No computador local, atualize o browser de Olá por atingir CTRL + F5 toosee que nginx página predefinida é removido.</span><span class="sxs-lookup"><span data-stu-id="5ad37-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![Nginx predefinido de página web](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="5ad37-154">No seu computador local, inicie sessão toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5ad37-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="5ad37-155">No menu de Olá Olá esquerda, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="5ad37-156">Na lista de Olá, selecione Olá VM.</span><span class="sxs-lookup"><span data-stu-id="5ad37-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="5ad37-157">No painel VM Olá, no Olá **definições** secção, clique em **cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="5ad37-158">Olá **cópia de segurança** abre o painel.</span><span class="sxs-lookup"><span data-stu-id="5ad37-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="5ad37-159">No menu de Olá, Olá parte superior do painel de Olá, selecione **recuperação de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="5ad37-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="5ad37-160">Olá **recuperação de ficheiros** abre o painel.</span><span class="sxs-lookup"><span data-stu-id="5ad37-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="5ad37-161">No **passo 1: selecione o ponto de recuperação**, selecione um ponto de recuperação da Olá lista pendente.</span><span class="sxs-lookup"><span data-stu-id="5ad37-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="5ad37-162">No **passo 2: Transferir o script toobrowse e recuperar ficheiros**, clique em Olá **transferir executável** botão.</span><span class="sxs-lookup"><span data-stu-id="5ad37-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="5ad37-163">Guarde o computador local do Olá ficheiro transferido tooyour.</span><span class="sxs-lookup"><span data-stu-id="5ad37-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="5ad37-164">Clique em **transferir o script** toodownload Olá ficheiro de script do localmente.</span><span class="sxs-lookup"><span data-stu-id="5ad37-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="5ad37-165">Abra um Bash linha de comandos e escreva Olá a seguir, substituindo *Linux_myVM_05-05-2017.sh* com Olá corrija o caminho e nome de ficheiro de script de Olá que transferiu, *azureuser* com o nome de utilizador de Olá para Olá VM e *13.69.75.209* com endereço IP público Olá para a VM.</span><span class="sxs-lookup"><span data-stu-id="5ad37-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="5ad37-166">No seu computador local, abra uma toohello de ligação SSH VM.</span><span class="sxs-lookup"><span data-stu-id="5ad37-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="5ad37-167">Na sua VM, adicione executar o ficheiro de script de toohello de permissões.</span><span class="sxs-lookup"><span data-stu-id="5ad37-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="5ad37-168">Na VM a executar o ponto de recuperação do Olá script toomount Olá como um sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="5ad37-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="5ad37-169">Olá o resultado da Olá script fornecem que Olá caminho para o ponto de montagem Olá.</span><span class="sxs-lookup"><span data-stu-id="5ad37-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="5ad37-170">saída de Olá procura toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="5ad37-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="5ad37-171">Na sua VM, copie Olá nginx predefinido de página web do Olá ponto de montagem toowhere back-lhe eliminar ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="5ad37-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="5ad37-172">No computador local, abra o separador do browser Olá qual estão ligados toohello o endereço IP do Olá VM que mostra Olá nginx predefinido de página.</span><span class="sxs-lookup"><span data-stu-id="5ad37-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="5ad37-173">Prima CTRL + F5 página de browser de Olá toorefresh.</span><span class="sxs-lookup"><span data-stu-id="5ad37-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="5ad37-174">Deverá ver que Olá página predefinida está a funcionar novamente.</span><span class="sxs-lookup"><span data-stu-id="5ad37-174">You should now see that hello default page is working again.</span></span>

    ![Nginx predefinido de página web](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="5ad37-176">No computador local, volte atrás toohello separador do browser para Olá portal do Azure e no **passo 3: desmonte discos Olá após a recuperação** clique Olá **desmonte discos** botão.</span><span class="sxs-lookup"><span data-stu-id="5ad37-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="5ad37-177">Caso se esqueça toodo neste passo, Olá ligação toohello pontodemontagem é fechar automaticamente após 12 horas.</span><span class="sxs-lookup"><span data-stu-id="5ad37-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="5ad37-178">Depois dessas 12 horas, terá de toodownload um toocreate script novo pontodemontagem uma novo.</span><span class="sxs-lookup"><span data-stu-id="5ad37-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5ad37-179">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5ad37-179">Next steps</span></span>

<span data-ttu-id="5ad37-180">Neste tutorial, ficou a saber como:</span><span class="sxs-lookup"><span data-stu-id="5ad37-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5ad37-181">Criar uma cópia de segurança de uma VM</span><span class="sxs-lookup"><span data-stu-id="5ad37-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="5ad37-182">Agendar uma cópia de segurança diária</span><span class="sxs-lookup"><span data-stu-id="5ad37-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="5ad37-183">Restaurar um ficheiro a partir de uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="5ad37-183">Restore a file from a backup</span></span>

<span data-ttu-id="5ad37-184">Produzir toohello seguinte toolearn tutorial sobre a monitorização de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5ad37-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5ad37-185">Monitorizar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5ad37-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

