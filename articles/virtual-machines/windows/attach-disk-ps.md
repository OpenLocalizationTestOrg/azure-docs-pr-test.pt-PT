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
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a><span data-ttu-id="80e0e-103">Anexar um tooa de disco de dados VM do Windows com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="80e0e-103">Attach a data disk tooa Windows VM using PowerShell</span></span>

<span data-ttu-id="80e0e-104">Este artigo mostra como tooattach nova e existente discos tooa Windows máquina com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80e0e-104">This article shows you how tooattach both new and existing disks tooa Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="80e0e-105">Se a VM utiliza discos geridos, pode anexar discos de dados gerida adicionais.</span><span class="sxs-lookup"><span data-stu-id="80e0e-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="80e0e-106">Também pode anexar tooa de discos de dados não geridos VM que utiliza discos não geridos numa conta do storage.</span><span class="sxs-lookup"><span data-stu-id="80e0e-106">You can also attach unmanaged data disks tooa VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="80e0e-107">Antes de fazer isto, consulte estas sugestões:</span><span class="sxs-lookup"><span data-stu-id="80e0e-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="80e0e-108">o tamanho da máquina virtual de Olá Olá controla quantos discos de dados, pode anexar.</span><span class="sxs-lookup"><span data-stu-id="80e0e-108">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="80e0e-109">Para obter mais informações, consulte [tamanhos das virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80e0e-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="80e0e-110">armazenamento Premium toouse, terá de armazenamento Premium ativado o tamanho da VM como Olá a máquina virtual-série DS ou série GS.</span><span class="sxs-lookup"><span data-stu-id="80e0e-110">toouse Premium storage, you'll need a Premium Storage enabled VM size like hello DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="80e0e-111">Pode utilizar os discos das contas do storage Standard e Premium com estas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="80e0e-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="80e0e-112">Armazenamento Premium está disponível em determinados regiões.</span><span class="sxs-lookup"><span data-stu-id="80e0e-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="80e0e-113">Para obter mais informações, consulte [Premium Storage: armazenamento de elevado desempenho para cargas de trabalho de Máquina Virtual de Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80e0e-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="80e0e-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="80e0e-114">Before you begin</span></span>
<span data-ttu-id="80e0e-115">Se utilizar o PowerShell, certifique-se de que tem a versão mais recente do Olá de Olá módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80e0e-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="80e0e-116">Executar Olá seguintes tooinstall de comando.</span><span class="sxs-lookup"><span data-stu-id="80e0e-116">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="80e0e-117">Para obter mais informações, consulte [controlo de versões do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80e0e-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a><span data-ttu-id="80e0e-118">Adicionar uma máquina de virtual de tooa de disco de dados vazio</span><span class="sxs-lookup"><span data-stu-id="80e0e-118">Add an empty data disk tooa virtual machine</span></span>

<span data-ttu-id="80e0e-119">Este exemplo mostra como tooadd um dados vazio disco tooan máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80e0e-119">This example shows how tooadd an empty data disk tooan existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="80e0e-120">Utilizar discos geridos</span><span class="sxs-lookup"><span data-stu-id="80e0e-120">Using managed disks</span></span>

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="80e0e-121">Utilizar discos não geridos numa conta do storage</span><span class="sxs-lookup"><span data-stu-id="80e0e-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a><span data-ttu-id="80e0e-122">Inicialize o disco de Olá</span><span class="sxs-lookup"><span data-stu-id="80e0e-122">Initialize hello disk</span></span>

<span data-ttu-id="80e0e-123">Depois de adicionar um disco vazio, é necessário tooinitialize-lo.</span><span class="sxs-lookup"><span data-stu-id="80e0e-123">After you add an empty disk, you need tooinitialize it.</span></span> <span data-ttu-id="80e0e-124">tooinitialize Olá disco, o que pode iniciar sessão na gestão de discos VM e a utilização de tooa.</span><span class="sxs-lookup"><span data-stu-id="80e0e-124">tooinitialize hello disk, you can log in tooa VM and use disk management.</span></span> <span data-ttu-id="80e0e-125">Se ativar o WinRM e um certificado no Olá VM quando o criou, pode utilizar o disco de Olá de tooinitialize de PowerShell remoto.</span><span class="sxs-lookup"><span data-stu-id="80e0e-125">If you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="80e0e-126">Também pode utilizar uma extensão de script personalizado:</span><span class="sxs-lookup"><span data-stu-id="80e0e-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="80e0e-127">ficheiro de script de Olá pode conter algo semelhante a discos de Olá de tooinitialize este código:</span><span class="sxs-lookup"><span data-stu-id="80e0e-127">hello script file can contain something like this code tooinitialize hello disks:</span></span>

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


## <a name="attach-an-existing-data-disk-tooa-vm"></a><span data-ttu-id="80e0e-128">Anexar um tooa de disco de dados VM existente</span><span class="sxs-lookup"><span data-stu-id="80e0e-128">Attach an existing data disk tooa VM</span></span>

<span data-ttu-id="80e0e-129">Também pode anexar um VHD existente como uma máquina virtual de tooa de disco de dados geridos.</span><span class="sxs-lookup"><span data-stu-id="80e0e-129">You can also attach an existing VHD as a managed data disk tooa virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="80e0e-130">Utilizar discos geridos</span><span class="sxs-lookup"><span data-stu-id="80e0e-130">Using managed disks</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="80e0e-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="80e0e-131">Next steps</span></span>

<span data-ttu-id="80e0e-132">Criar um [instantâneo](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="80e0e-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
