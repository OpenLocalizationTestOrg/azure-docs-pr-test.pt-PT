---
title: "aaaUse moderna de cópia de segurança de armazenamento com o servidor de cópia de segurança do Azure v2 | Microsoft Docs"
description: "Saiba mais sobre as novas funcionalidades Olá no servidor de cópia de segurança do Azure v2. Este artigo descreve como tooupgrade a instalação do servidor de cópia de segurança."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="13d1d-104">Adicionar armazenamento tooAzure v2 do servidor de cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="13d1d-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="13d1d-105">V2 de servidor do Backup do Azure é fornecido com o System Center 2016 proteção Manager moderna cópia de segurança do armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="13d1d-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="13d1d-106">Armazenamento de cópia de segurança moderna oferece poupança de armazenamento de 50 por cento, cópias de segurança que são armazenamento três vezes, mais rápido e eficiente.</span><span class="sxs-lookup"><span data-stu-id="13d1d-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="13d1d-107">Também proporciona armazenamento com suporte para a carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="13d1d-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="13d1d-108">toouse moderna armazenamento de cópia de segurança, tem de executar v2 do servidor de cópia de segurança no Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="13d1d-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="13d1d-109">Se executar o servidor de cópia de segurança v2 numa versão anterior do Windows Server, servidor de cópia de segurança do Azure não é possível tirar partido do armazenamento de cópia de segurança moderna.</span><span class="sxs-lookup"><span data-stu-id="13d1d-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="13d1d-110">Em vez disso, o que protege cargas de trabalho como acontece com o servidor de cópia de segurança v1.</span><span class="sxs-lookup"><span data-stu-id="13d1d-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="13d1d-111">Para obter mais informações, consulte a versão do servidor de cópia de segurança Olá [matriz proteção](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="13d1d-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="13d1d-112">Volumes no servidor de cópia de segurança v2</span><span class="sxs-lookup"><span data-stu-id="13d1d-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="13d1d-113">Cópia de segurança servidor v2 aceita volumes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="13d1d-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="13d1d-114">Quando adiciona um volume, o servidor de cópia de segurança formata Olá volume tooResilient sistema de ficheiros (ReFS), que necessita de armazenamento de cópia de segurança moderna.</span><span class="sxs-lookup"><span data-stu-id="13d1d-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="13d1d-115">tooadd um volume e tooexpand-lo mais tarde se for necessário, sugerimos que utilize este fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="13d1d-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="13d1d-116">Configure o servidor de cópia de segurança v2 numa VM.</span><span class="sxs-lookup"><span data-stu-id="13d1d-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="13d1d-117">Crie um volume num disco virtual num agrupamento de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="13d1d-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="13d1d-118">Adicione um agrupamento de armazenamento do disco tooa e criar um disco virtual com o esquema simples.</span><span class="sxs-lookup"><span data-stu-id="13d1d-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="13d1d-119">Adicione quaisquer discos adicionais e expandir disco virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="13d1d-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="13d1d-120">Crie volumes no disco virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="13d1d-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="13d1d-121">Adicione Olá volumes tooBackup servidor.</span><span class="sxs-lookup"><span data-stu-id="13d1d-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="13d1d-122">Configure o armazenamento com suporte para a carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="13d1d-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="13d1d-123">Criar um volume de armazenamento de cópia de segurança moderna</span><span class="sxs-lookup"><span data-stu-id="13d1d-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="13d1d-124">Com o servidor de cópia de segurança v2 volumes como armazenamento de disco pode ajudar a manter o controlo sobre o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="13d1d-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="13d1d-125">Um volume pode ser um único disco.</span><span class="sxs-lookup"><span data-stu-id="13d1d-125">A volume can be a single disk.</span></span> <span data-ttu-id="13d1d-126">No entanto, se quiser armazenamento tooextend Olá futuras, crie um volume fora de um disco que criou, utilizando os espaços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="13d1d-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="13d1d-127">Isto pode ajudar a se pretender o volume de Olá tooexpand para armazenamento de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="13d1d-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="13d1d-128">Esta secção oferece melhores práticas para criar um volume com esta configuração.</span><span class="sxs-lookup"><span data-stu-id="13d1d-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="13d1d-129">No Gestor de servidor, selecione **File and Storage Services** > **Volumes** > **agrupamentos de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="13d1d-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="13d1d-130">Em **discos físicos**, selecione **novo agrupamento de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="13d1d-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Criar um novo agrupamento de armazenamento](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="13d1d-132">No Olá **tarefas** caixa pendente, selecione **novo disco Virtual**.</span><span class="sxs-lookup"><span data-stu-id="13d1d-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Adicionar um disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="13d1d-134">Selecione o agrupamento de armazenamento Olá e, em seguida, selecione **adicionar disco físico**.</span><span class="sxs-lookup"><span data-stu-id="13d1d-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![Adicionar um disco físico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="13d1d-136">Selecione o disco físico Olá e, em seguida, selecione **expandir disco Virtual**.</span><span class="sxs-lookup"><span data-stu-id="13d1d-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Expandir disco virtual Olá](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="13d1d-138">Selecione o disco virtual Olá e, em seguida, selecione **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="13d1d-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![Crie um novo volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="13d1d-140">No Olá **selecione Olá servidor e disco** caixa de diálogo, o servidor de Olá selecione e o disco novo Olá.</span><span class="sxs-lookup"><span data-stu-id="13d1d-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="13d1d-141">Em seguida, selecione **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="13d1d-141">Then, select **Next**.</span></span>

    ![Selecione o servidor de Olá e o disco](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="13d1d-143">Adicione armazenamento em disco volumes tooBackup servidor</span><span class="sxs-lookup"><span data-stu-id="13d1d-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="13d1d-144">tooadd um tooBackup de volume de servidor, no Olá **gestão** painel, reanalisar armazenamento Olá e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="13d1d-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="13d1d-145">É apresentada uma lista de todos os Olá volumes disponíveis toobe adicionado para armazenamento de servidor de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="13d1d-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="13d1d-146">Depois de volumes disponíveis são adicionadas toohello lista de volumes selecionados, pode conceder-lhes toohelp um nome amigável geri-los.</span><span class="sxs-lookup"><span data-stu-id="13d1d-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="13d1d-147">Estes volumes tooReFS pelo servidor de cópia de segurança pode utilizar os benefícios de Olá de armazenamento de cópia de segurança moderna, selecione de tooformat **OK**.</span><span class="sxs-lookup"><span data-stu-id="13d1d-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![Adicionar a Volumes disponíveis](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="13d1d-149">Configurar o armazenamento com suporte para a carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="13d1d-149">Set up workload-aware storage</span></span>

<span data-ttu-id="13d1d-150">Com o armazenamento com suporte para a carga de trabalho, pode selecionar os volumes de Olá preferentially armazenam determinados tipos de cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="13d1d-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="13d1d-151">Por exemplo, pode definir volumes dispendiosas que suportam um número elevado de operações de entrada/saída por segundo (IOPS) toostore apenas Olá cargas de trabalho que necessitam de cópias de segurança frequentes, elevado volume.</span><span class="sxs-lookup"><span data-stu-id="13d1d-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="13d1d-152">Um exemplo é o SQL Server com registos de transações.</span><span class="sxs-lookup"><span data-stu-id="13d1d-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="13d1d-153">Outras cargas de trabalho que são uma cópia de segurança com menos frequência, como VMs, podem ser feitas toolow custo volumes.</span><span class="sxs-lookup"><span data-stu-id="13d1d-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="13d1d-154">Atualização DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="13d1d-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="13d1d-155">Pode configurar o armazenamento com suporte para a carga de trabalho utilizando o cmdlet do PowerShell Olá Update-DPMDiskStorage, que atualiza as propriedades de Olá de um volume no agrupamento de armazenamento Olá num servidor do Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="13d1d-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="13d1d-156">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="13d1d-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="13d1d-157">Olá seguinte captura de ecrã mostra Olá atualização DPMDiskStorage cmdlet na janela do PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="13d1d-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![Olá DPMDiskStorage de atualização de comando na janela do PowerShell Olá](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="13d1d-159">alterações de Olá efetuadas através do PowerShell são refletidas no Olá consola do administrador do servidor de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="13d1d-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![Discos e volumes de Olá consola do administrador](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="13d1d-161">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="13d1d-161">Next steps</span></span>
<span data-ttu-id="13d1d-162">Depois de instalar o servidor de cópia de segurança, saiba como tooprepare seu servidor, ou começar a proteger uma carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="13d1d-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="13d1d-163">Preparar as cargas de trabalho do servidor de cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="13d1d-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="13d1d-164">Utilizar o servidor de cópia de segurança tooback configurar um servidor VMware</span><span class="sxs-lookup"><span data-stu-id="13d1d-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="13d1d-165">Utilizar o servidor de cópia de segurança tooback cópias de segurança do SQL Server</span><span class="sxs-lookup"><span data-stu-id="13d1d-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

