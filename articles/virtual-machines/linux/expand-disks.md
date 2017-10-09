---
title: "discos rígidos virtuais aaaExpand numa VM com Linux no Azure | Microsoft Docs"
description: "Saiba como discos rígidos virtuais tooexpand numa VM com Linux Olá Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="c303b-103">Como discos rígidos virtuais tooexpand numa VM com Linux Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c303b-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="c303b-104">tamanho de disco rígido virtual Olá predefinido para o sistema de operativo Olá (SO) é, geralmente, 30 GB numa máquina virtual (VM) do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="c303b-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="c303b-105">Pode [adicionar discos de dados](add-disk.md) tooprovide para espaço de armazenamento adicional, mas também pode desejar tooexpand um disco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="c303b-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="c303b-106">Este artigo descreve em detalhe como tooexpand geridos discos para uma VM com Linux com Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c303b-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="c303b-107">Também pode expandir o disco do SO Olá não gerido com Olá [CLI do Azure 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c303b-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="c303b-108">Certificar-se sempre de que a cópia de segurança os dados antes de executar disco redimensiona operações.</span><span class="sxs-lookup"><span data-stu-id="c303b-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="c303b-109">Para obter mais informações, consulte [cópia de segurança VMs com Linux no Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="c303b-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="c303b-110">Expanda o disco</span><span class="sxs-lookup"><span data-stu-id="c303b-110">Expand disk</span></span>
<span data-ttu-id="c303b-111">Certifique-se de que tem mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c303b-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c303b-112">Este artigo requer uma VM existente no Azure pelo menos um disco de dados ligada e está preparado.</span><span class="sxs-lookup"><span data-stu-id="c303b-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="c303b-113">Se ainda não tiver uma VM que pode utilizar, consulte [criar e preparar uma VM com discos de dados](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="c303b-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="c303b-114">No Olá amostras seguintes, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="c303b-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c303b-115">Os nomes dos parâmetros de exemplo incluem *myResourceGroup* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c303b-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="c303b-116">Não não possível efetuar operações em discos rígidos virtuais com Olá VM em execução.</span><span class="sxs-lookup"><span data-stu-id="c303b-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="c303b-117">Desalocar a VM com [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="c303b-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="c303b-118">Olá exemplo seguinte deallocates Olá VM com o nome *myVM* no grupo de recursos de Olá designado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c303b-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="c303b-119">`az vm stop`não disponibilizar recursos de computação Olá.</span><span class="sxs-lookup"><span data-stu-id="c303b-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="c303b-120">toorelease recursos de computação, utilize `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="c303b-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="c303b-121">Olá VM tem de ser desalocada tooexpand Olá disco de rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="c303b-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="c303b-122">Ver uma lista de discos geridos num grupo de recursos com [lista de discos az](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="c303b-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="c303b-123">Olá exemplo seguinte mostra uma lista de discos geridos no grupo de recursos de Olá designado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c303b-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="c303b-124">Expanda o disco de necessário Olá com [atualização de disco az](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="c303b-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="c303b-125">Olá exemplo seguinte expande disco geridos Olá chamado *myDataDisk* toobe *200*tamanho Gb:</span><span class="sxs-lookup"><span data-stu-id="c303b-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="c303b-126">Ao expandir um disco gerido, o tamanho de Olá atualizado é mapeada toohello mais próximo do tamanho de disco gerido.</span><span class="sxs-lookup"><span data-stu-id="c303b-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="c303b-127">Para uma tabela de camadas e tamanhos de disco gerido disponível Olá, consulte [geridos discos descrição geral do Azure - preços e faturação](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="c303b-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="c303b-128">Iniciar a VM com [início de vm az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="c303b-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="c303b-129">Olá seguir iniciado o exemplo Olá VM com o nome *myVM* no grupo de recursos de Olá designado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c303b-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="c303b-130">SSH tooyour VM com as credenciais adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="c303b-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="c303b-131">Pode obter o endereço IP público Olá da sua VM com [mostrar de vm az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="c303b-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="c303b-132">Olá toouse expandir disco, tem de partição subjacente do tooexpand Olá e sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="c303b-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="c303b-133">a.</span><span class="sxs-lookup"><span data-stu-id="c303b-133">a.</span></span> <span data-ttu-id="c303b-134">Se já montado, desmonte disco Olá:</span><span class="sxs-lookup"><span data-stu-id="c303b-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="c303b-135">b.</span><span class="sxs-lookup"><span data-stu-id="c303b-135">b.</span></span> <span data-ttu-id="c303b-136">Utilize `parted` tooview do disco e redimensione partição Olá:</span><span class="sxs-lookup"><span data-stu-id="c303b-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="c303b-137">Ver informações sobre o esquema de existente partição Olá com `print`.</span><span class="sxs-lookup"><span data-stu-id="c303b-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="c303b-138">Olá de saída é semelhante toohello seguinte o exemplo, que mostra o disco subjacente Olá é 215Gb de tamanho:</span><span class="sxs-lookup"><span data-stu-id="c303b-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="c303b-139">c.</span><span class="sxs-lookup"><span data-stu-id="c303b-139">c.</span></span> <span data-ttu-id="c303b-140">Expanda a partição com o Olá `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="c303b-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="c303b-141">Introduza o número de partição Olá, *1*e um tamanho de partição nova Olá:</span><span class="sxs-lookup"><span data-stu-id="c303b-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="c303b-142">d.</span><span class="sxs-lookup"><span data-stu-id="c303b-142">d.</span></span> <span data-ttu-id="c303b-143">tooexit, introduza`quit`</span><span class="sxs-lookup"><span data-stu-id="c303b-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="c303b-144">Com partição de Olá redimensionada, verificar a consistência de partição de Olá com `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="c303b-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="c303b-145">Redimensionar agora Olá filesystem com `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="c303b-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="c303b-146">Montagem Olá partição toohello pretendido localização, tais como `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="c303b-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="c303b-147">foi redimensionado tooverify disco de SO de Olá, utilize `df -h`.</span><span class="sxs-lookup"><span data-stu-id="c303b-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="c303b-148">Olá saídas de exemplo a seguir mostra a unidade de dados de Olá, */dev/sdc1*, está agora 200 GB:</span><span class="sxs-lookup"><span data-stu-id="c303b-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="c303b-149">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c303b-149">Next steps</span></span>
<span data-ttu-id="c303b-150">Se precisar de armazenamento adicional, também [adicionar discos de dados tooa VM com Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="c303b-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="c303b-151">Para obter mais informações sobre a encriptação de disco, consulte [discos encriptar uma VM com Linux utilizando Olá CLI do Azure](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="c303b-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
