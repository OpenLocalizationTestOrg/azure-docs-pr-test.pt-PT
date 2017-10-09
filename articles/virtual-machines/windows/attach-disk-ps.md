---
title: aaaAttach um tooa de disco de dados VM do Windows no Azure utilizando o PowerShell | Microsoft Docs
description: "Como os dados de novo ou existente tooattach disco tooa VM do Windows com o PowerShell com o modelo de implementação do Resource Manager Olá."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a>Anexar um tooa de disco de dados VM do Windows com o PowerShell

Este artigo mostra como tooattach nova e existente discos tooa Windows máquina com o PowerShell. Se a VM utiliza discos geridos, pode anexar discos de dados gerida adicionais. Também pode anexar tooa de discos de dados não geridos VM que utiliza discos não geridos numa conta do storage.

Antes de fazer isto, consulte estas sugestões:
* o tamanho da máquina virtual de Olá Olá controla quantos discos de dados, pode anexar. Para obter mais informações, consulte [tamanhos das virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* armazenamento Premium toouse, terá de armazenamento Premium ativado o tamanho da VM como Olá a máquina virtual-série DS ou série GS. Pode utilizar os discos das contas do storage Standard e Premium com estas máquinas virtuais. Armazenamento Premium está disponível em determinados regiões. Para obter mais informações, consulte [Premium Storage: armazenamento de elevado desempenho para cargas de trabalho de Máquina Virtual de Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="before-you-begin"></a>Antes de começar
Se utilizar o PowerShell, certifique-se de que tem a versão mais recente do Olá de Olá módulo AzureRM.Compute PowerShell. Executar Olá seguintes tooinstall de comando.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para obter mais informações, consulte [controlo de versões do Azure PowerShell](/powershell/azure/overview).


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a>Adicionar uma máquina de virtual de tooa de disco de dados vazio

Este exemplo mostra como tooadd um dados vazio disco tooan máquina virtual.

### <a name="using-managed-disks"></a>Utilizar discos geridos

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a>Utilizar discos não geridos numa conta do storage

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a>Inicialize o disco de Olá

Depois de adicionar um disco vazio, é necessário tooinitialize-lo. tooinitialize Olá disco, o que pode iniciar sessão na gestão de discos VM e a utilização de tooa. Se ativar o WinRM e um certificado no Olá VM quando o criou, pode utilizar o disco de Olá de tooinitialize de PowerShell remoto. Também pode utilizar uma extensão de script personalizado: 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
ficheiro de script de Olá pode conter algo semelhante a discos de Olá de tooinitialize este código:

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-tooa-vm"></a>Anexar um tooa de disco de dados VM existente

Também pode anexar um VHD existente como uma máquina virtual de tooa de disco de dados geridos. 

### <a name="using-managed-disks"></a>Utilizar discos geridos

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a>Passos seguintes

Criar um [instantâneo](snapshot-copy-managed-disk.md).
