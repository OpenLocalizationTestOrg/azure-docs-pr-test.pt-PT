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
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Converter Azure geridos armazenamento de discos de toopremium padrão e vice versa

Discos geridos oferece duas opções de armazenamento: [Premium](../../storage/storage-premium-storage.md) (baseadas em SSD) e [padrão](../../storage/storage-standard-storage.md) (baseado em HDD). Permite-lhe tooeasily comutador entre opções de Olá dois com período de indisponibilidade mínimo com base nas necessidades de desempenho. Esta capacidade não está disponível para os discos não geridos. Mas pode facilmente [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily comutador entre opções de Olá dois.

Este artigo mostra como tooconvert discos geridos de toopremium padrão e vice versa utilizando o Azure PowerShell. Se precisar de tooinstall ou atualizá-lo, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Antes de começar

* conversão de Olá requer um reinício de Olá VM, por isso, agendar migração Olá do seu armazenamento de discos durante uma janela de manutenção já existente. 
* Se estiver a utilizar discos não geridos, primeiro [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch este artigo entre as opções de armazenamento Olá dois. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Converter todas Olá geridos discos de uma VM a partir da toopremium padrão e vice versa

No seguinte exemplo de Olá, mostramos como tooswitch Olá todos os discos de uma VM a partir do armazenamento de toopremium padrão. discos geridos pelo toouse premium, a VM tem de utilizar um [tamanho da VM](sizes.md) que suporte o premium storage. Este exemplo também comutadores tooa tamanho que suporte o premium storage.

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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Converter um disco gerido standard toopremium e vice versa

Para sua carga de trabalho de programador/teste, poderá ser útil toohave mistura de discos padrão e premium tooreduce o custo. Pode fazê-lo por atualizar armazenamento toopremium, apenas os discos de Olá que requerem um melhor desempenho. No seguinte exemplo de Olá, mostramos como tooswitch num disco individual de uma VM do armazenamento de toopremium padrão e vice-versa. discos geridos pelo toouse premium, a VM tem de utilizar um [tamanho da VM](sizes.md) que suporte o premium storage. Este exemplo também comutadores tooa tamanho que suporte o premium storage.

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

## <a name="next-steps"></a>Passos seguintes

Efetuar uma cópia só de leitura de uma VM utilizando [instantâneos](snapshot-copy-managed-disk.md).

