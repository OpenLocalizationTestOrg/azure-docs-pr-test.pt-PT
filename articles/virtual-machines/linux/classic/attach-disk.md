---
title: aaaAttach tooa um disco VM com Linux no Azure | Microsoft Docs
description: "Saiba como tooattach dados de um disco tooa VM com Linux utilizando a implementação de clássico Olá modelo e inicializar disco Olá, para que fique pronta para ser utilizado"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="3a78d-103">Como tooAttach tooa um disco de dados Máquina Virtual com Linux</span><span class="sxs-lookup"><span data-stu-id="3a78d-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="3a78d-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3a78d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3a78d-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="3a78d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3a78d-106">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="3a78d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3a78d-107">Veja como demasiado[anexar um disco de dados com o modelo de implementação do Resource Manager Olá](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a78d-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3a78d-108">Pode anexar vazios discos e os discos que contêm dados tooyour VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a78d-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="3a78d-109">Ambos os tipos de discos são ficheiros. vhd que residem numa conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a78d-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="3a78d-110">Como com a adição de qualquer máquina de Linux do disco tooa, depois de ligar o disco de Olá que precisa tooinitialize e formate-o para que fique pronta para ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="3a78d-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="3a78d-111">Este detalhes de artigo anexar discos vazios e discos já que contém, bem como dados tooyour VMs, como a forma como toothen inicializar e formatar um novo disco.</span><span class="sxs-lookup"><span data-stu-id="3a78d-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="3a78d-112">É uma melhor toouse de prática um ou mais discos toostore separam dados de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3a78d-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="3a78d-113">Quando cria uma máquina virtual do Azure, tem um disco de sistema operativo e um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="3a78d-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="3a78d-114">**Não utilize dados persistentes do Olá disco temporário toostore.**</span><span class="sxs-lookup"><span data-stu-id="3a78d-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="3a78d-115">Como Olá nome indica, fornece apenas armazenamento temporário.</span><span class="sxs-lookup"><span data-stu-id="3a78d-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="3a78d-116">Não oferece nenhuma cópia de segurança ou redundância porque esta não reside no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a78d-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="3a78d-117">disco temporário Olá é, normalmente, gerido pelo Olá agente Linux do Azure e automaticamente montado demasiado**/mnt/recursos** (ou **/mnt** nas imagens Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="3a78d-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="3a78d-118">No Olá por outro lado, um disco de dados pode ser denominado pelo kernel de Linux Olá algo semelhante ao seguinte `/dev/sdc`, e terá de toopartition, formatar e monte este recurso.</span><span class="sxs-lookup"><span data-stu-id="3a78d-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="3a78d-119">Consulte Olá [guia de utilizador de agente do Azure Linux] [ Agent] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="3a78d-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="3a78d-120">Inicializar um novo disco de dados no Linux</span><span class="sxs-lookup"><span data-stu-id="3a78d-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="3a78d-121">SSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="3a78d-121">SSH tooyour VM.</span></span> <span data-ttu-id="3a78d-122">Para obter mais informações, consulte [como toolog tooa máquina de virtual com Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="3a78d-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="3a78d-123">Em seguida precisa o identificador do dispositivo Olá toofind para tooinitialize de disco de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="3a78d-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="3a78d-124">Existem duas formas toodo que:</span><span class="sxs-lookup"><span data-stu-id="3a78d-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="3a78d-125">a) registos de Grep para dispositivos SCSI Olá, como Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3a78d-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="3a78d-126">Para as distribuições do Ubuntu recentes, poderá ser necessário toouse `sudo grep SCSI /var/log/syslog` porque o registo demasiado`/var/log/messages` podem estar desativados por predefinição.</span><span class="sxs-lookup"><span data-stu-id="3a78d-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="3a78d-127">Pode encontrar o identificador de Olá de Olá último disco de dados que foi adicionado no mensagens hello que são apresentadas.</span><span class="sxs-lookup"><span data-stu-id="3a78d-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Obter mensagens hello do disco](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="3a78d-129">OU</span><span class="sxs-lookup"><span data-stu-id="3a78d-129">OR</span></span>
   
    <span data-ttu-id="3a78d-130">b) Olá utilize `lsscsi` toofind comando terminar o id de dispositivo Olá. `lsscsi` podem ser instaladas por um `yum install lsscsi` (no Red Hat com base distribuições) ou `apt-get install lsscsi` (no Debian com base distribuições).</span><span class="sxs-lookup"><span data-stu-id="3a78d-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="3a78d-131">Pode encontrar o disco de Olá que está procurando pelo respetivo *lun* ou **número de unidade lógica**.</span><span class="sxs-lookup"><span data-stu-id="3a78d-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="3a78d-132">Por exemplo, Olá *lun* para discos de Olá anexou podem ser facilmente vistos a partir de `azure vm disk list <virtual-machine>` como:</span><span class="sxs-lookup"><span data-stu-id="3a78d-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="3a78d-133">o resultado da Olá é semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="3a78d-133">hello output is similar toohello following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="3a78d-134">Comparar estes dados com o resultado Olá `lsscsi` para Olá mesma máquina virtual de exemplo:</span><span class="sxs-lookup"><span data-stu-id="3a78d-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="3a78d-135">número da última Olá na cadeia de identificação de Olá em cada linha é Olá *lun*.</span><span class="sxs-lookup"><span data-stu-id="3a78d-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="3a78d-136">Consulte `man lsscsi` para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="3a78d-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="3a78d-137">Na linha de Olá, escreva, por exemplo, o dispositivo Olá toocreate de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3a78d-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="3a78d-138">Quando lhe for pedido, escreva  **n**  toocreate uma partição.</span><span class="sxs-lookup"><span data-stu-id="3a78d-138">When prompted, type **n** toocreate a partition.</span></span>

    ![Criar dispositivo](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="3a78d-140">Quando lhe for pedido, escreva **p** partição primária do toomake Olá partição Olá.</span><span class="sxs-lookup"><span data-stu-id="3a78d-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="3a78d-141">Tipo **1** toomake Olá primeira partição e, em seguida, escreva introduza o valor do tooaccept Olá predefinido para cilindro Olá.</span><span class="sxs-lookup"><span data-stu-id="3a78d-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="3a78d-142">Em alguns sistemas, pode mostrar os valores predefinidos de Olá de Olá primeiro e Olá último setores, em vez de cilindro Olá.</span><span class="sxs-lookup"><span data-stu-id="3a78d-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="3a78d-143">Pode escolher tooaccept estas predefinições.</span><span class="sxs-lookup"><span data-stu-id="3a78d-143">You can choose tooaccept these defaults.</span></span>

    ![Criar a partição](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="3a78d-145">Tipo **p** toosee Olá detalhes disco Olá que está a ser particionado.</span><span class="sxs-lookup"><span data-stu-id="3a78d-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![Informações do disco de lista](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="3a78d-147">Tipo **w** definições de Olá toowrite para disco Olá.</span><span class="sxs-lookup"><span data-stu-id="3a78d-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Escrever Olá alterações de disco](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="3a78d-149">Agora pode criar o sistema de ficheiros de Olá na partição Olá de novo.</span><span class="sxs-lookup"><span data-stu-id="3a78d-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="3a78d-150">Acrescentar Olá partição número toohello ID do dispositivo (no seguinte exemplo de Olá `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="3a78d-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="3a78d-151">Olá exemplo seguinte cria uma partição ext4 no /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="3a78d-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Criar o sistema de ficheiros](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="3a78d-153">Sistemas SuSE Linux Enterprise 11 só suportam acesso só de leitura ext4 sistemas de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="3a78d-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="3a78d-154">Para estes sistemas, recomenda-se tooformat Olá novo sistema de ficheiros como ext3 em vez de ext4.</span><span class="sxs-lookup"><span data-stu-id="3a78d-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="3a78d-155">Efetue um diretório toomount Olá novo sistema de ficheiros, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="3a78d-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="3a78d-156">Por fim, pode montar unidade Olá, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="3a78d-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="3a78d-157">disco de dados de Olá está agora pronto toouse como **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="3a78d-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Criar disco de Olá de diretório e montagem Olá](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="3a78d-159">Adicione Olá nova unidade demasiado/etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="3a78d-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="3a78d-160">unidade de Olá tooensure é remontadas da automaticamente depois de reiniciar o computador tem de ser adicionado toohello /etc/fstab ficheiro.</span><span class="sxs-lookup"><span data-stu-id="3a78d-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="3a78d-161">Além disso, recomenda-se vivamente que Olá UUID (universalmente Unique IDentifier) é utilizada na unidade de toohello /etc/fstab toorefer em vez de apenas Olá nome do dispositivo (ou seja, /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="3a78d-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="3a78d-162">Utilizar Olá UUID evita a ser montado tooa fornecido localização se Olá SO Deteta um erro de disco durante o arranque e de quaisquer discos de dados restantes, em seguida, que está a ser atribuído aos IDs de dispositivo de disco incorreta Olá.</span><span class="sxs-lookup"><span data-stu-id="3a78d-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="3a78d-163">toofind Olá UUID da nova unidade de Olá, pode utilizar Olá **blkid** utilitário:</span><span class="sxs-lookup"><span data-stu-id="3a78d-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="3a78d-164">saída de Olá procura toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3a78d-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="3a78d-165">Editar incorretamente Olá **etc/fstab** ficheiros poderia resultar num sistema de arranque.</span><span class="sxs-lookup"><span data-stu-id="3a78d-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="3a78d-166">Se não souber, consulte a documentação da distribuição toohello para obter informações sobre como tooproperly editar este ficheiro.</span><span class="sxs-lookup"><span data-stu-id="3a78d-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="3a78d-167">Também é recomendável que uma cópia de segurança do ficheiro de /etc/fstab Olá foi criada antes de editar.</span><span class="sxs-lookup"><span data-stu-id="3a78d-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="3a78d-168">Em seguida, abra Olá **etc/fstab** ficheiro num editor de texto:</span><span class="sxs-lookup"><span data-stu-id="3a78d-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="3a78d-169">Neste exemplo, vamos utilizar Olá UUID valor para Olá novo **/dev/sdc1** dispositivo que foi criado nos passos anteriores Olá e Olá pontodemontagem **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="3a78d-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="3a78d-170">Adicionar Olá seguir final toohello linha Olá **etc/fstab** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="3a78d-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="3a78d-171">Ou, em sistemas com base no SuSE Linux poderá ser necessário toouse formato ligeiramente diferente:</span><span class="sxs-lookup"><span data-stu-id="3a78d-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="3a78d-172">Olá `nofail` opção garante que Olá VM entrar, mesmo se o sistema de ficheiros de Olá está danificado ou disco Olá não existe no momento do arranque.</span><span class="sxs-lookup"><span data-stu-id="3a78d-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="3a78d-173">Sem esta opção, pode encontrar o comportamento, conforme descrito em [não é possível SSH tooLinux VM devido a erros de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="3a78d-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="3a78d-174">Pode agora testar que o sistema de ficheiros de Olá está montado corretamente pela desmontagem e remontar, em seguida, o sistema de ficheiros hello, ou seja, utilizando o ponto de montagem de exemplo de Olá `/datadrive` criado no Olá anteriormente os passos:</span><span class="sxs-lookup"><span data-stu-id="3a78d-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="3a78d-175">Se hello `mount` comando produz erro, verifique Olá ficheiro etc/fstab para a sintaxe correta.</span><span class="sxs-lookup"><span data-stu-id="3a78d-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="3a78d-176">Se as unidades de dados adicionais ou partições são criadas, introduzi-las em etc/fstab separadamente bem.</span><span class="sxs-lookup"><span data-stu-id="3a78d-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="3a78d-177">Faz com que Olá unidade gravável utilizando este comando:</span><span class="sxs-lookup"><span data-stu-id="3a78d-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="3a78d-178">Posteriormente, remover um disco de dados sem necessitar de editar fstab causam Olá VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="3a78d-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="3a78d-179">Se se tratar de uma ocorrência comum, a maioria das distribuições fornecem o Olá `nofail` e/ou `nobootwait` fstab opções que permitem uma tooboot de sistema, mesmo que o disco de Olá falha toomount no momento do arranque.</span><span class="sxs-lookup"><span data-stu-id="3a78d-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="3a78d-180">Consulte a documentação de sua distribuição para obter mais informações sobre estes parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3a78d-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="3a78d-181">Suporte de cortar/UNMAP para Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="3a78d-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="3a78d-182">Alguns kernels Linux suportam toodiscard de operações de cortar/UNMAP blocos não utilizados no disco Olá.</span><span class="sxs-lookup"><span data-stu-id="3a78d-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="3a78d-183">Estas operações são principalmente útil para armazenamento standard tooinform Azure eliminado páginas já não são válidos e pode ser eliminada.</span><span class="sxs-lookup"><span data-stu-id="3a78d-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="3a78d-184">Rejeitar páginas pode guardar o custo, se criar ficheiros grandes e, em seguida, elimine-os.</span><span class="sxs-lookup"><span data-stu-id="3a78d-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="3a78d-185">Existem duas formas tooenable cortar suportar na sua VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="3a78d-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="3a78d-186">Normalmente, consulte a distribuição para Olá abordagem recomendada:</span><span class="sxs-lookup"><span data-stu-id="3a78d-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="3a78d-187">Olá utilize `discard` montar opção na `/etc/fstab`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3a78d-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="3a78d-188">Em alguns Olá casos `discard` opção pode ter implicações de desempenho.</span><span class="sxs-lookup"><span data-stu-id="3a78d-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="3a78d-189">Em alternativa, pode executar Olá `fstrim` comando manualmente a partir da linha de comandos hello, ou adicione-tooyour crontab toorun regularmente:</span><span class="sxs-lookup"><span data-stu-id="3a78d-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="3a78d-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="3a78d-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="3a78d-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="3a78d-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="3a78d-192">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="3a78d-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="3a78d-193">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="3a78d-193">Next Steps</span></span>
<span data-ttu-id="3a78d-194">Pode ler mais sobre como utilizar a VM com Linux no Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="3a78d-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="3a78d-195">[Como toolog tooa máquina de virtual com Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="3a78d-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="3a78d-196">Como toodetach um disco de uma máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="3a78d-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="3a78d-197">Utilizar Olá CLI do Azure com o modelo de implementação clássica Olá</span><span class="sxs-lookup"><span data-stu-id="3a78d-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="3a78d-198">Configurar o RAID numa VM com Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="3a78d-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="3a78d-199">Configurar LVM numa VM com Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="3a78d-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
