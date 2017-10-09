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
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>Criar uma VM do Windows a partir de um disco especializado

Crie uma nova VM ao anexar um disco gerido especializado como disco do SO Olá através do Powershell. Um disco especializado é uma cópia de disco rígido virtual (VHD) de uma VM existente que mantém as contas de utilizador Olá, aplicações e outros dados de estado de original VM. 

Quando utiliza um toocreate VHD especializada uma nova VM, Olá nova VM mantém o nome do computador Olá do Olá original VM. Também é possível mantida outras informações específicas do computador e, em alguns casos, estas informações de duplicados pode causar problemas. Lembre-se de que tipos de informações específicas do computador as suas aplicações dependem quando copiar uma VM.

Tem duas opções:
* [Carregar um VHD](#option-1-upload-a-specialized-vhd)
* [Copiar uma VM do Azure existente](#option-2-copy-an-existing-azure-vm)

Este tópico mostra como toouse geridos discos. Se tiver uma implementação de legado que necessita de utilizar uma conta do storage, consulte [criar uma VM a partir de um VHD numa conta de armazenamento especializado](sa-create-vm-specialized.md)

## <a name="before-you-begin"></a>Antes de começar
Se utilizar o PowerShell, certifique-se de que tem a versão mais recente do Olá de Olá módulo AzureRM.Compute PowerShell. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para obter mais informações, consulte [controlo de versões do Azure PowerShell](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Opção 1: Carregar um VHD especializado

Pode carregar Olá que VHD de uma VM especializada criado com uma ferramenta de virtualização no local, como o Hyper-V ou numa VM exportada de outra nuvem.

### <a name="prepare-hello-vm"></a>Preparar Olá VM
Se tenciona toouse Olá VHD-é toocreate uma nova VM, certifique-se de que Olá os passos seguintes é concluída. 
  
  * [Preparar uma tooAzure tooupload do VHD do Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Não** generalizar Olá VM com o Sysprep.
  * Remova quaisquer agentes que estão instalados no Olá VM (como as ferramentas do VMware) e ferramentas de Virtualização do convidado.
  * Certifique-se Olá VM é toopull configurado o endereço IP e as definições de DNS através do DHCP. Isto garante que o servidor Olá obtém um endereço IP no Olá VNet durante o arranque. 


### <a name="get-hello-storage-account"></a>Obter a conta de armazenamento Olá
Necessita de um armazenamento conta no Azure toostore Olá carregado VHD. Pode utilizar uma conta de armazenamento existente ou crie um novo. 

as contas de armazenamento disponíveis do tooshow Olá, escreva:

```powershell
Get-AzureRmStorageAccount
```

Se quiser toouse uma conta de armazenamento existente, continuar toohello [carregamento Olá VHD](#upload-the-vhd-to-your-storage-account) secção.

Se precisar de toocreate uma conta do storage, siga estes passos:

1. É necessário o nome Olá Olá do grupo de recursos onde a conta de armazenamento Olá deve ser criada. toofind enviados todos os grupos de recursos de Olá que estão na sua subscrição, o tipo:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    com o nome de um grupo de recursos de toocreate *myResourceGroup* no Olá *EUA oeste* região, escreva:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Criar uma conta de armazenamento com o nome *mystorageaccount* neste grupo de recursos utilizando Olá [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Carregar a conta de armazenamento do Olá VHD tooyour 
Olá utilize [adicionar AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload Olá VHD tooa num contentor na sua conta do storage. Neste exemplo Olá de carregamentos de ficheiros *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` com o nome de conta do storage tooa *mystorageaccount* no Olá *myResourceGroup* grupo de recursos. ficheiro de Olá é armazenado num contentor de Olá com o nome *mycontainer* e vai ser o novo nome de ficheiro Olá *myUploadedVHD.vhd*.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


Se tiver êxito, receberá uma resposta que procura toothis semelhante:

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

Dependendo da ligação de rede e o tamanho do ficheiro VHD Olá, este comando pode demorar algum tempo toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>Criar um disco gerido a partir de Olá VHD

Criar um disco gerido a partir de Olá especializada VHD na sua conta de armazenamento utilizar [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). Este exemplo utiliza **myOSDisk1** para o nome do disco Olá, PUT Olá disco *StandardLRS* armazenamento e utiliza *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* como Olá URI para a origem de Olá VHD.

Criar um novo grupo de recursos para Olá nova VM.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Criar Olá disco de SO novo de Olá carregado VHD. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>Opção 2: Copiar uma VM do Azure existente

Pode criar uma cópia de uma VM que utiliza discos geridos por um instantâneo de Olá VM, em seguida, utilizar essa toocreate instantâneo um novo geridos disco e uma nova VM.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Tirar um instantâneo do disco do SO Olá

Pode demorar uma VM de instantâneo do e completa (incluindo todos os discos) ou de apenas um único disco. Olá passos seguintes mostram como tootake um instantâneo do disco de SO de Olá apenas da sua utilização de VM Olá [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet. 

Defina alguns parâmetros. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Obter o objeto da VM Olá.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
Obter nome do disco Olá SO.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Crie a configuração de Olá de instantâneos. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Tire o instantâneo de Olá.

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Se planear toouse Olá instantâneo toocreate uma VM que necessita de toobe elevado desempenho, utilize o parâmetro de Olá `-AccountType Premium_LRS` com comando Olá AzureRmSnapshot de novo. parâmetro de Olá cria instantâneos Olá, de modo a que seja armazenada como um disco de gerido para Premium. Os discos Premium geridos são mais dispendiosos do que padrão. Por isso, não se esqueça de que precisar realmente Premium antes de utilizar o parâmetro de Olá.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Criar um novo disco a partir do instantâneo Olá

Criar um disco gerido a partir de Olá através de instantâneos [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). Este exemplo utiliza *myOSDisk* para o nome do disco Olá.

Criar um novo grupo de recursos para Olá nova VM.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Definir o nome do disco Olá SO. 

```powershell
$osDiskName = 'myOsDisk'
```

Crie disco Olá de gerido.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>Criar Olá nova VM 

Criar redes e outro toobe de recursos VM utilizados pelo Olá nova VM.

### <a name="create-hello-subnet-and-vnet"></a>Criar a sub-rede de Olá e a vNet

Criar vNet Olá e sub-rede de Olá [rede virtual](../../virtual-network/virtual-networks-overview.md).

Crie Olá sub-rede. Este exemplo cria uma sub-rede designada **mySubNet**, no grupo de recursos de Olá **myDestinationResourceGroup**, e conjuntos Olá prefixo de endereço de sub-rede demasiado**10.0.0.0/24**.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Crie vNet Olá. Neste exemplo conjuntos Olá toobe de nome de rede virtual **myVnetName**, Olá localização demasiado**EUA oeste**, e Olá prefixo do endereço de rede virtual Olá demasiado**10.0.0.0/16**. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Criar grupo de segurança de rede Olá e uma regra RDP
toobe toolog consegue no tooyour VM através de RDP, terá de toohave uma regra de segurança que permite o acesso RDP na porta 3389. Porque hello VHD para Olá nova VM foi criada a partir de uma VM especializada existente, pode utilizar uma conta da máquina de virtual de origem Olá para RDP.

Neste exemplo Olá de conjuntos de nome NSG demasiado**myNsg** e Olá RDP nome da regra demasiado**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Para obter mais informações sobre os pontos finais e as regras do NSG, consulte [abrir portas tooa VM no Azure utilizando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="create-a-public-ip-address-and-nic"></a>Criar um endereço IP público e NIC
tooenable comunicação com a máquina virtual de Olá na rede virtual Olá, precisa de um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.

Crie Olá um IP público. Neste exemplo, nome do endereço IP público Olá é definido demasiado**myIP**.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Criar Olá NIC. Neste exemplo, o nome NIC de Olá está definido demasiado**myNicName**.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Definir o nome da VM Olá e o tamanho

Neste exemplo Olá de conjuntos de nome VM demasiado*myVM* e Olá VM tamanho demasiado*Standard_A2*.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Adicionar Olá NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Adicionar disco de SO de Olá 

Adicionar Olá SO disco toohello configuração utilizando [conjunto AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk). Neste exemplo define Olá tamanho de disco Olá demasiado*128 GB* e anexa Olá disco gerido como um *Windows* disco do SO.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>Concluir Olá VM 

Criar Olá VM utilizando [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)Olá configurações que acabamos de criar.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

Se este comando foi concluída com êxito, verá o resultado como esta:

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Certifique-se de que Olá que VM foi criada
Deverá ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com), em **procurar** > **máquinas virtuais**, ou utilizando Olá seguir PowerShell comandos:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>Passos seguintes
toosign no tooyour nova máquina virtual, procurar toohello VM na Olá [portal](https://portal.azure.com), clique em **Connect**e o ficheiro de RDP Remote Desktop Protocol Olá aberta. Utilize as credenciais da conta de Olá do seu original toosign de máquina virtual na máquina de virtual novo tooyour. Para obter mais informações, consulte [como tooconnect e início de sessão tooan virtual do Azure máquina com o Windows](connect-logon.md).

