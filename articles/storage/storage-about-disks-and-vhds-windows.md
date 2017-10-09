---
title: aaaAbout discos e VHD para as VMs do Microsoft Azure Windows | Microsoft Docs
description: "Saiba mais sobre Olá Noções básicas sobre discos e as máquinas virtuais de VHDs para Windows no Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="607e7-103">Sobre discos e VHDs para VMs do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="607e7-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="607e7-104">Tal como qualquer outro computador, as máquinas virtuais no Azure utilizar discos como um toostore implementado um sistema operativo, aplicações e dados.</span><span class="sxs-lookup"><span data-stu-id="607e7-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="607e7-105">Todas as máquinas virtuais do Azure de ter, pelo menos, dois discos – um disco de sistema operativo Windows e um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="607e7-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="607e7-106">disco do sistema operativo Olá é criado a partir de uma imagem e o disco do sistema operativo Olá e imagem Olá são discos rígidos virtuais (VHDs) armazenados numa conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="607e7-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="607e7-107">Máquinas virtuais podem ter também um ou mais discos de dados, que também são armazenados como VHDs.</span><span class="sxs-lookup"><span data-stu-id="607e7-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="607e7-108">Neste artigo, iremos falar sobre utiliza diferentes de Olá para discos de Olá e, em seguida, aborda os diferentes tipos Olá de discos, pode criar e utilizar.</span><span class="sxs-lookup"><span data-stu-id="607e7-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="607e7-109">Este artigo também está disponível para [máquinas virtuais do Linux](storage-about-disks-and-vhds-linux.md).</span><span class="sxs-lookup"><span data-stu-id="607e7-109">This article is also available for [Linux virtual machines](storage-about-disks-and-vhds-linux.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="607e7-110">Discos utilizados por VMs</span><span class="sxs-lookup"><span data-stu-id="607e7-110">Disks used by VMs</span></span>

<span data-ttu-id="607e7-111">Vamos ver como discos de hello são utilizadas por Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="607e7-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="607e7-112">Disco do sistema operativo</span><span class="sxs-lookup"><span data-stu-id="607e7-112">Operating system disk</span></span>
<span data-ttu-id="607e7-113">Cada máquina virtual possui um disco de sistema de operativo anexado.</span><span class="sxs-lookup"><span data-stu-id="607e7-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="607e7-114">Tem registado como uma unidade SATA e identificados como unidade de c: Olá por predefinição.</span><span class="sxs-lookup"><span data-stu-id="607e7-114">It's registered as a SATA drive and labeled as hello C: drive by default.</span></span> <span data-ttu-id="607e7-115">Este disco tem uma capacidade máxima de 2048 gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="607e7-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="607e7-116">Disco temporário</span><span class="sxs-lookup"><span data-stu-id="607e7-116">Temporary disk</span></span>
<span data-ttu-id="607e7-117">Cada VM contém um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="607e7-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="607e7-118">disco temporário Olá fornece armazenamento de curta duração para aplicações e processos e tooonly pretendido arquivo de dados, tais como ficheiros de página ou a troca.</span><span class="sxs-lookup"><span data-stu-id="607e7-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="607e7-119">Dados em disco temporário Olá podem ser perdidos durante uma [evento de manutenção](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou quando a [voltar a implementar uma VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="607e7-119">Data on hello temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="607e7-120">Durante um reinício padrão do Olá VM, devem manter dados Olá na unidade temporária Olá.</span><span class="sxs-lookup"><span data-stu-id="607e7-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="607e7-121">disco temporário Olá assinalada como como Olá unidade d: por predefinição e utilizado para armazenar pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="607e7-121">hello temporary disk is labeled as hello D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="607e7-122">tooremap esta letra de unidade diferente do disco tooa, consulte [alteração Olá letra da unidade de disco temporário do Windows hello](../virtual-machines/windows/change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="607e7-122">tooremap this disk tooa different drive letter, see [Change hello drive letter of hello Windows temporary disk](../virtual-machines/windows/change-drive-letter.md).</span></span> <span data-ttu-id="607e7-123">o tamanho do disco temporário Olá Olá varia, com base no tamanho Olá da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="607e7-123">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="607e7-124">Para obter mais informações, consulte [máquinas virtuais de tamanhos para Windows](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="607e7-124">For more information, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>

<span data-ttu-id="607e7-125">Para obter mais informações sobre como o Azure utiliza disco temporário Olá, consulte [compreender unidade temporária de Olá em do Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="607e7-125">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="607e7-126">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="607e7-126">Data disk</span></span>
<span data-ttu-id="607e7-127">Um disco de dados é uma imagem VHD que dados de aplicação de toostore de máquina virtual anexado tooa ou outros dados terá tookeep.</span><span class="sxs-lookup"><span data-stu-id="607e7-127">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="607e7-128">Os discos de dados estão registados como unidades de SCSI e são etiquetados com uma letra que escolher.</span><span class="sxs-lookup"><span data-stu-id="607e7-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="607e7-129">Cada disco de dados tem uma capacidade máxima de 4095 GB.</span><span class="sxs-lookup"><span data-stu-id="607e7-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="607e7-130">Olá tamanho da máquina virtual de Olá determina quantos discos de dados, pode anexar tooit e Olá tipo de armazenamento pode utilizar discos de Olá toohost.</span><span class="sxs-lookup"><span data-stu-id="607e7-130">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="607e7-131">Para obter mais informações sobre as capacidades de máquinas virtuais, consulte [máquinas virtuais de tamanhos para Windows](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="607e7-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>
> 

<span data-ttu-id="607e7-132">Quando criar uma máquina virtual a partir de uma imagem, o Azure cria um disco de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="607e7-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="607e7-133">Se utilizar uma imagem que inclui os discos de dados, o Azure também cria Olá discos de dados quando cria a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="607e7-133">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="607e7-134">Caso contrário, adicione discos de dados depois de criar a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="607e7-134">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="607e7-135">Pode adicionar máquinas de virtuais de tooa de discos de dados em qualquer altura, pelo **anexar** Olá disco toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="607e7-135">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="607e7-136">Pode utilizar uma imagem VHD que tiver carregado ou copiados tooyour conta de armazenamento ou um que Azure cria por si.</span><span class="sxs-lookup"><span data-stu-id="607e7-136">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="607e7-137">Anexar um disco de dados associa ficheiro VHD Olá Olá VM colocando uma concessão no Olá VHD, pelo que não pode ser eliminada do armazenamento enquanto ainda está ligado.</span><span class="sxs-lookup"><span data-stu-id="607e7-137">Attaching a data disk associates hello VHD file with hello VM by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="607e7-138">Uma recomendação última: Utilize cortar com discos padrão não geridos</span><span class="sxs-lookup"><span data-stu-id="607e7-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="607e7-139">Se utilizar discos padrão não geridos (HDD), deverá ativar a limitação.</span><span class="sxs-lookup"><span data-stu-id="607e7-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="607e7-140">Operações de COMPACTAÇÃO elimina os blocos no disco Olá, é-lhe faturado apenas para o armazenamento que está a utilizar, na verdade, de modo.</span><span class="sxs-lookup"><span data-stu-id="607e7-140">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="607e7-141">Isto permite poupar nos custos se criar ficheiros grandes e, em seguida, elimine-os.</span><span class="sxs-lookup"><span data-stu-id="607e7-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="607e7-142">Pode executar esta definição COMPACTAÇÃO do comando toocheck Olá.</span><span class="sxs-lookup"><span data-stu-id="607e7-142">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="607e7-143">Abra uma linha de comandos na sua VM do Windows e o tipo:</span><span class="sxs-lookup"><span data-stu-id="607e7-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="607e7-144">Se o comando de Olá devolve 0, cortar está ativada corretamente.</span><span class="sxs-lookup"><span data-stu-id="607e7-144">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="607e7-145">Se devolver-1, execute Olá comando tooenable cortar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="607e7-145">If it returns 1, run hello following command tooenable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="607e7-146">Nota: O suporte começa com o Windows Server 2012 / Windows 8 e superior, consulte ver [nova API permite que aplicações toosend "Compactar e Unmap" sugestões toostorage suporte de dados](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span><span class="sxs-lookup"><span data-stu-id="607e7-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps toosend "TRIM and Unmap" hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="607e7-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="607e7-147">Next steps</span></span>
* <span data-ttu-id="607e7-148">[Anexar um disco](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd armazenamento adicional para a VM.</span><span class="sxs-lookup"><span data-stu-id="607e7-148">[Attach a disk](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="607e7-149">[Alteração Olá letra da unidade de disco temporário do Windows hello](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para a aplicação pode utilizar a unidade de d: Olá de dados.</span><span class="sxs-lookup"><span data-stu-id="607e7-149">[Change hello drive letter of hello Windows temporary disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use hello D: drive for data.</span></span>

