---
title: "armazenamento de discos de geridos aaaConvert Azure a partir da toopremium padrão e vice-versa | Microsoft Docs"
description: "Como tooconvert Azure discos geridos de toopremium padrão e vice-versa, utilizando o Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="7efe0-103">Converter Azure geridos armazenamento de discos de toopremium padrão e vice versa</span><span class="sxs-lookup"><span data-stu-id="7efe0-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="7efe0-104">Discos geridos oferece duas opções de armazenamento: [Premium](../../storage/storage-premium-storage.md) (baseadas em SSD) e [padrão](../../storage/storage-standard-storage.md) (baseado em HDD).</span><span class="sxs-lookup"><span data-stu-id="7efe0-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="7efe0-105">Permite-lhe tooeasily comutador entre opções de Olá dois com período de indisponibilidade mínimo com base nas necessidades de desempenho.</span><span class="sxs-lookup"><span data-stu-id="7efe0-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="7efe0-106">Esta capacidade não está disponível para os discos não geridos.</span><span class="sxs-lookup"><span data-stu-id="7efe0-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="7efe0-107">Mas pode facilmente [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily comutador entre opções de Olá dois.</span><span class="sxs-lookup"><span data-stu-id="7efe0-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="7efe0-108">Este artigo mostra como tooconvert discos geridos de toopremium padrão e vice versa utilizando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7efe0-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="7efe0-109">Se precisar de tooinstall ou atualizá-lo, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7efe0-109">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7efe0-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7efe0-110">Before you begin</span></span>

* <span data-ttu-id="7efe0-111">conversão de Olá requer um reinício de Olá VM, por isso, agendar migração Olá do seu armazenamento de discos durante uma janela de manutenção já existente.</span><span class="sxs-lookup"><span data-stu-id="7efe0-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="7efe0-112">Se estiver a utilizar discos não geridos, primeiro [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch este artigo entre as opções de armazenamento Olá dois.</span><span class="sxs-lookup"><span data-stu-id="7efe0-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="7efe0-113">Converter todas Olá geridos discos de uma VM a partir da toopremium padrão e vice versa</span><span class="sxs-lookup"><span data-stu-id="7efe0-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="7efe0-114">No seguinte exemplo de Olá, mostramos como tooswitch Olá todos os discos de uma VM a partir do armazenamento de toopremium padrão.</span><span class="sxs-lookup"><span data-stu-id="7efe0-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="7efe0-115">discos geridos pelo toouse premium, a VM tem de utilizar um [tamanho da VM](sizes.md) que suporte o premium storage.</span><span class="sxs-lookup"><span data-stu-id="7efe0-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="7efe0-116">Este exemplo também comutadores tooa tamanho que suporte o premium storage.</span><span class="sxs-lookup"><span data-stu-id="7efe0-116">This example also switches tooa size that supports premium storage.</span></span>

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="7efe0-117">Converter um disco gerido standard toopremium e vice versa</span><span class="sxs-lookup"><span data-stu-id="7efe0-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="7efe0-118">Para sua carga de trabalho de programador/teste, poderá ser útil toohave mistura de discos padrão e premium tooreduce o custo.</span><span class="sxs-lookup"><span data-stu-id="7efe0-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="7efe0-119">Pode fazê-lo por atualizar armazenamento toopremium, apenas os discos de Olá que requerem um melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="7efe0-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="7efe0-120">No seguinte exemplo de Olá, mostramos como tooswitch num disco individual de uma VM do armazenamento de toopremium padrão e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="7efe0-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="7efe0-121">discos geridos pelo toouse premium, a VM tem de utilizar um [tamanho da VM](sizes.md) que suporte o premium storage.</span><span class="sxs-lookup"><span data-stu-id="7efe0-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="7efe0-122">Este exemplo também comutadores tooa tamanho que suporte o premium storage.</span><span class="sxs-lookup"><span data-stu-id="7efe0-122">This example also switches tooa size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="7efe0-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7efe0-123">Next steps</span></span>

<span data-ttu-id="7efe0-124">Efetuar uma cópia só de leitura de uma VM utilizando [instantâneos](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="7efe0-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

