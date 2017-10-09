---
title: aaaCreate VM a partir de uma imagem VM gerida no Azure | Microsoft Docs
description: "Crie uma máquina virtual do Windows a partir de uma imagem VM gerida generalizada com o Azure PowerShell, no modelo de implementação do Resource Manager Olá."
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Criar uma VM a partir de uma imagem gerida

Pode criar várias VMs a partir de uma imagem VM gerida no Azure. Uma imagem VM gerida contém Olá informações necessárias toocreate uma VM, incluindo Olá SO e discos de dados. Olá VHDs que compõem a imagem de Olá, incluindo discos Olá SO e discos de dados, são armazenadas como discos geridos. 


## <a name="prerequisites"></a>Pré-requisitos

É necessário toohave já [criada uma imagem VM gerida](capture-image-resource.md) toouse para criar Olá nova VM. 

Certifique-se de que têm versões mais recentes do Olá dos módulos de Olá AzureRM.Compute e AzureRM.Network PowerShell. Abra uma linha de comandos do PowerShell como administrador e execute Olá os seguintes comandos tooinstall-los.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Para obter mais informações, consulte [controlo de versões do Azure PowerShell](/powershell/azure/overview).



## <a name="collect-information-about-hello-image"></a>Recolher informações sobre a imagem de Olá

Primeiro vamos precisar toogather informações básicas sobre a imagem de Olá e criar uma variável para a imagem de Olá. Este exemplo utiliza uma imagem VM gerida com o nome **myImage** que está em Olá **myResourceGroup** grupo de recursos no Olá **Central EUA oeste** localização. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Criar uma rede virtual
Criar vNet Olá e sub-rede de Olá [rede virtual](../../virtual-network/virtual-networks-overview.md).

1. Crie Olá sub-rede. Este exemplo cria uma sub-rede designada **mySubnet** com o prefixo de endereço Olá de **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crie rede virtual Olá. Este exemplo cria uma rede virtual denominada **myVnet** com o prefixo de endereço Olá de **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Criar uma interface de rede e o endereço IP pública

tooenable comunicação com a máquina virtual de Olá na rede virtual Olá, precisa de um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.

1. Crie um endereço IP público. Este exemplo cria um endereço IP público com o nome **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Criar Olá NIC. Este exemplo cria um NIC com o nome **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Criar grupo de segurança de rede Olá e uma regra RDP

toobe toolog consegue no tooyour VM através de RDP, terá de toohave uma regra de segurança de rede (NSG) que permite o acesso RDP na porta 3389. 

Este exemplo cria um NSG denominado **myNsg** que contenha uma regra denominada **myRdpRule** que permite tráfego RDP de através da porta 3389. Para obter mais informações sobre NSGs, consulte [abrir portas tooa VM no Azure utilizando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Criar uma variável para a rede virtual Olá

Crie uma variável para a rede virtual Olá foi concluída. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Obter credenciais Olá para Olá VM

Olá seguinte cmdlet irá abrir uma janela onde irá introduzir um novo toouse de nome e palavra-passe de utilizador como conta de administrador local Olá para aceder remotamente a Olá VM. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>As variáveis de conjunto para Olá VM nome, nome do computador e Olá tamanho de Olá VM

1. Crie variáveis de nome de VM de Olá e nome do computador. Neste exemplo define o nome da VM Olá como **myVM** e nome do computador Olá como **myComputer**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Definir Olá tamanho de Olá máquina virtual. Este exemplo cria **Standard_DS1_v2** tamanho de VM. Consulte Olá [tamanhos de VM](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentação para obter mais informações.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Adicione Olá nome da VM e configuração de VM de toohello de tamanho.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Imagem de VM do conjunto Olá como imagem de origem para Olá nova VM

Definir a imagem de origem Olá utilizando Olá ID da imagem VM Olá gerido.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Definir a configuração do SO Olá e adicione a NIC de Olá.

Introduza o tipo de armazenamento Olá (PremiumLRS ou StandardLRS) e o tamanho do disco do SO Olá Olá. Neste exemplo, define o tipo de conta Olá demasiado**PremiumLRS**, Olá o tamanho do disco demasiado**128 GB** e disco a colocação em cache demasiado**ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Criar Olá VM

Criar Olá nova Vm utilizando a configuração de Olá que vamos ter criado e armazenado no Olá **$vm** variável.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Certifique-se de que Olá que VM foi criada
Quando terminar, deverá ver Olá recém-criado VM na Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou utilizando o seguinte Olá Comandos do PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Passos seguintes
toomanage a nova máquina virtual com o Azure PowerShell, consulte [criar e gerir VMs do Windows com o módulo do Azure PowerShell Olá](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

