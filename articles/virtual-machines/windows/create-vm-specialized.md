---
title: aaaCreate uma VM do Windows a partir de um VHD especializado no Azure | Microsoft Docs
description: "Crie uma nova VM do Windows ao anexar um disco gerido especializado como disco do SO Olá utilizar no modelo de implementação do Resource Manager Olá."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="b1fcc-103">Criar uma VM do Windows a partir de um disco especializado</span><span class="sxs-lookup"><span data-stu-id="b1fcc-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="b1fcc-104">Crie uma nova VM ao anexar um disco gerido especializado como disco do SO Olá através do Powershell.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="b1fcc-105">Um disco especializado é uma cópia de disco rígido virtual (VHD) de uma VM existente que mantém as contas de utilizador Olá, aplicações e outros dados de estado de original VM.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="b1fcc-106">Quando utiliza um toocreate VHD especializada uma nova VM, Olá nova VM mantém o nome do computador Olá do Olá original VM.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="b1fcc-107">Também é possível mantida outras informações específicas do computador e, em alguns casos, estas informações de duplicados pode causar problemas.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="b1fcc-108">Lembre-se de que tipos de informações específicas do computador as suas aplicações dependem quando copiar uma VM.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="b1fcc-109">Tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="b1fcc-109">You have two options:</span></span>
* [<span data-ttu-id="b1fcc-110">Carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="b1fcc-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="b1fcc-111">Copiar uma VM do Azure existente</span><span class="sxs-lookup"><span data-stu-id="b1fcc-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="b1fcc-112">Este tópico mostra como toouse geridos discos.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="b1fcc-113">Se tiver uma implementação de legado que necessita de utilizar uma conta do storage, consulte [criar uma VM a partir de um VHD numa conta de armazenamento especializado](sa-create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="b1fcc-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b1fcc-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="b1fcc-114">Before you begin</span></span>
<span data-ttu-id="b1fcc-115">Se utilizar o PowerShell, certifique-se de que tem a versão mais recente do Olá de Olá módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="b1fcc-116">Para obter mais informações, consulte [controlo de versões do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b1fcc-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="b1fcc-117">Opção 1: Carregar um VHD especializado</span><span class="sxs-lookup"><span data-stu-id="b1fcc-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="b1fcc-118">Pode carregar Olá que VHD de uma VM especializada criado com uma ferramenta de virtualização no local, como o Hyper-V ou numa VM exportada de outra nuvem.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="b1fcc-119">Preparar Olá VM</span><span class="sxs-lookup"><span data-stu-id="b1fcc-119">Prepare hello VM</span></span>
<span data-ttu-id="b1fcc-120">Se tenciona toouse Olá VHD-é toocreate uma nova VM, certifique-se de que Olá os passos seguintes é concluída.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="b1fcc-121">[Preparar uma tooAzure tooupload do VHD do Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1fcc-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b1fcc-122">**Não** generalizar Olá VM com o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="b1fcc-123">Remova quaisquer agentes que estão instalados no Olá VM (como as ferramentas do VMware) e ferramentas de Virtualização do convidado.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="b1fcc-124">Certifique-se Olá VM é toopull configurado o endereço IP e as definições de DNS através do DHCP.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="b1fcc-125">Isto garante que o servidor Olá obtém um endereço IP no Olá VNet durante o arranque.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="b1fcc-126">Obter a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="b1fcc-126">Get hello storage account</span></span>
<span data-ttu-id="b1fcc-127">Necessita de um armazenamento conta no Azure toostore Olá carregado VHD.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="b1fcc-128">Pode utilizar uma conta de armazenamento existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="b1fcc-129">as contas de armazenamento disponíveis do tooshow Olá, escreva:</span><span class="sxs-lookup"><span data-stu-id="b1fcc-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="b1fcc-130">Se quiser toouse uma conta de armazenamento existente, continuar toohello [carregamento Olá VHD](#upload-the-vhd-to-your-storage-account) secção.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="b1fcc-131">Se precisar de toocreate uma conta do storage, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="b1fcc-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="b1fcc-132">É necessário o nome Olá Olá do grupo de recursos onde a conta de armazenamento Olá deve ser criada.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="b1fcc-133">toofind enviados todos os grupos de recursos de Olá que estão na sua subscrição, o tipo:</span><span class="sxs-lookup"><span data-stu-id="b1fcc-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="b1fcc-134">com o nome de um grupo de recursos de toocreate *myResourceGroup* no Olá *EUA oeste* região, escreva:</span><span class="sxs-lookup"><span data-stu-id="b1fcc-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="b1fcc-135">Criar uma conta de armazenamento com o nome *mystorageaccount* neste grupo de recursos utilizando Olá [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b1fcc-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="b1fcc-136">Carregar a conta de armazenamento do Olá VHD tooyour</span><span class="sxs-lookup"><span data-stu-id="b1fcc-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="b1fcc-137">Olá utilize [adicionar AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload Olá VHD tooa num contentor na sua conta do storage.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="b1fcc-138">Neste exemplo Olá de carregamentos de ficheiros *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` com o nome de conta do storage tooa *mystorageaccount* no Olá *myResourceGroup* grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="b1fcc-139">ficheiro de Olá é armazenado num contentor de Olá com o nome *mycontainer* e vai ser o novo nome de ficheiro Olá *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="b1fcc-140">Se tiver êxito, receberá uma resposta que procura toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="b1fcc-140">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="b1fcc-141">Dependendo da ligação de rede e o tamanho do ficheiro VHD Olá, este comando pode demorar algum tempo toocomplete</span><span class="sxs-lookup"><span data-stu-id="b1fcc-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="b1fcc-142">Criar um disco gerido a partir de Olá VHD</span><span class="sxs-lookup"><span data-stu-id="b1fcc-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="b1fcc-143">Criar um disco gerido a partir de Olá especializada VHD na sua conta de armazenamento utilizar [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="b1fcc-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="b1fcc-144">Este exemplo utiliza **myOSDisk1** para o nome do disco Olá, PUT Olá disco *StandardLRS* armazenamento e utiliza *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* como Olá URI para a origem de Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="b1fcc-145">Criar um novo grupo de recursos para Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="b1fcc-146">Criar Olá disco de SO novo de Olá carregado VHD.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="b1fcc-147">Opção 2: Copiar uma VM do Azure existente</span><span class="sxs-lookup"><span data-stu-id="b1fcc-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="b1fcc-148">Pode criar uma cópia de uma VM que utiliza discos geridos por um instantâneo de Olá VM, em seguida, utilizar essa toocreate instantâneo um novo geridos disco e uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="b1fcc-149">Tirar um instantâneo do disco do SO Olá</span><span class="sxs-lookup"><span data-stu-id="b1fcc-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="b1fcc-150">Pode demorar uma VM de instantâneo do e completa (incluindo todos os discos) ou de apenas um único disco.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="b1fcc-151">Olá passos seguintes mostram como tootake um instantâneo do disco de SO de Olá apenas da sua utilização de VM Olá [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="b1fcc-152">Defina alguns parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="b1fcc-153">Obter o objeto da VM Olá.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="b1fcc-154">Obter nome do disco Olá SO.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="b1fcc-155">Crie a configuração de Olá de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="b1fcc-156">Tire o instantâneo de Olá.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="b1fcc-157">Se planear toouse Olá instantâneo toocreate uma VM que necessita de toobe elevado desempenho, utilize o parâmetro de Olá `-AccountType Premium_LRS` com comando Olá AzureRmSnapshot de novo.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="b1fcc-158">parâmetro de Olá cria instantâneos Olá, de modo a que seja armazenada como um disco de gerido para Premium.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="b1fcc-159">Os discos Premium geridos são mais dispendiosos do que padrão.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="b1fcc-160">Por isso, não se esqueça de que precisar realmente Premium antes de utilizar o parâmetro de Olá.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="b1fcc-161">Criar um novo disco a partir do instantâneo Olá</span><span class="sxs-lookup"><span data-stu-id="b1fcc-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="b1fcc-162">Criar um disco gerido a partir de Olá através de instantâneos [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="b1fcc-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="b1fcc-163">Este exemplo utiliza *myOSDisk* para o nome do disco Olá.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="b1fcc-164">Criar um novo grupo de recursos para Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="b1fcc-165">Definir o nome do disco Olá SO.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="b1fcc-166">Crie disco Olá de gerido.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="b1fcc-167">Criar Olá nova VM</span><span class="sxs-lookup"><span data-stu-id="b1fcc-167">Create hello new VM</span></span> 

<span data-ttu-id="b1fcc-168">Criar redes e outro toobe de recursos VM utilizados pelo Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="b1fcc-169">Criar a sub-rede de Olá e a vNet</span><span class="sxs-lookup"><span data-stu-id="b1fcc-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="b1fcc-170">Criar vNet Olá e sub-rede de Olá [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1fcc-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="b1fcc-171">Crie Olá sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-171">Create hello subNet.</span></span> <span data-ttu-id="b1fcc-172">Este exemplo cria uma sub-rede designada **mySubNet**, no grupo de recursos de Olá **myDestinationResourceGroup**, e conjuntos Olá prefixo de endereço de sub-rede demasiado**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="b1fcc-173">Crie vNet Olá.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-173">Create hello vNet.</span></span> <span data-ttu-id="b1fcc-174">Neste exemplo conjuntos Olá toobe de nome de rede virtual **myVnetName**, Olá localização demasiado**EUA oeste**, e Olá prefixo do endereço de rede virtual Olá demasiado**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="b1fcc-175">Criar grupo de segurança de rede Olá e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="b1fcc-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="b1fcc-176">toobe toolog consegue no tooyour VM através de RDP, terá de toohave uma regra de segurança que permite o acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="b1fcc-177">Porque hello VHD para Olá nova VM foi criada a partir de uma VM especializada existente, pode utilizar uma conta da máquina de virtual de origem Olá para RDP.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="b1fcc-178">Neste exemplo Olá de conjuntos de nome NSG demasiado**myNsg** e Olá RDP nome da regra demasiado**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="b1fcc-179">Para obter mais informações sobre os pontos finais e as regras do NSG, consulte [abrir portas tooa VM no Azure utilizando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1fcc-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="b1fcc-180">Criar um endereço IP público e NIC</span><span class="sxs-lookup"><span data-stu-id="b1fcc-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="b1fcc-181">tooenable comunicação com a máquina virtual de Olá na rede virtual Olá, precisa de um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="b1fcc-182">Crie Olá um IP público.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-182">Create hello public IP.</span></span> <span data-ttu-id="b1fcc-183">Neste exemplo, nome do endereço IP público Olá é definido demasiado**myIP**.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="b1fcc-184">Criar Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-184">Create hello NIC.</span></span> <span data-ttu-id="b1fcc-185">Neste exemplo, o nome NIC de Olá está definido demasiado**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="b1fcc-186">Definir o nome da VM Olá e o tamanho</span><span class="sxs-lookup"><span data-stu-id="b1fcc-186">Set hello VM name and size</span></span>

<span data-ttu-id="b1fcc-187">Neste exemplo Olá de conjuntos de nome VM demasiado*myVM* e Olá VM tamanho demasiado*Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="b1fcc-188">Adicionar Olá NIC</span><span class="sxs-lookup"><span data-stu-id="b1fcc-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="b1fcc-189">Adicionar disco de SO de Olá</span><span class="sxs-lookup"><span data-stu-id="b1fcc-189">Add hello OS disk</span></span> 

<span data-ttu-id="b1fcc-190">Adicionar Olá SO disco toohello configuração utilizando [conjunto AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="b1fcc-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="b1fcc-191">Neste exemplo define Olá tamanho de disco Olá demasiado*128 GB* e anexa Olá disco gerido como um *Windows* disco do SO.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="b1fcc-192">Concluir Olá VM</span><span class="sxs-lookup"><span data-stu-id="b1fcc-192">Complete hello VM</span></span> 

<span data-ttu-id="b1fcc-193">Criar Olá VM utilizando [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)Olá configurações que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="b1fcc-194">Se este comando foi concluída com êxito, verá o resultado como esta:</span><span class="sxs-lookup"><span data-stu-id="b1fcc-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="b1fcc-195">Certifique-se de que Olá que VM foi criada</span><span class="sxs-lookup"><span data-stu-id="b1fcc-195">Verify that hello VM was created</span></span>
<span data-ttu-id="b1fcc-196">Deverá ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com), em **procurar** > **máquinas virtuais**, ou utilizando Olá seguir PowerShell comandos:</span><span class="sxs-lookup"><span data-stu-id="b1fcc-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="b1fcc-197">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b1fcc-197">Next steps</span></span>
<span data-ttu-id="b1fcc-198">toosign no tooyour nova máquina virtual, procurar toohello VM na Olá [portal](https://portal.azure.com), clique em **Connect**e o ficheiro de RDP Remote Desktop Protocol Olá aberta.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="b1fcc-199">Utilize as credenciais da conta de Olá do seu original toosign de máquina virtual na máquina de virtual novo tooyour.</span><span class="sxs-lookup"><span data-stu-id="b1fcc-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="b1fcc-200">Para obter mais informações, consulte [como tooconnect e início de sessão tooan virtual do Azure máquina com o Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="b1fcc-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

