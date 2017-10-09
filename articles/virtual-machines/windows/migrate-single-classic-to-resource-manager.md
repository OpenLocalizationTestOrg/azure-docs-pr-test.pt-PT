---
title: "aaaMigrate um tooan VMS clássicas VM de disco gerido ARM | Microsoft Docs"
description: "Migrar uma única VM do Azure de implementação clássica Olá tooManaged discos no modelo de implementação do Resource Manager Olá de modelo."
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
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>Migrar manualmente um tooa VMS clássicas novo ARM geridos disco VM a partir do Olá VHD 


Esta secção ajuda-toomigrate as suas VMs do Azure existente do modelo de implementação clássica Olá demasiado[discos geridos](managed-disks-overview.md) no modelo de implementação do Resource Manager Olá.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planear a migração de Olá tooManaged discos

Esta secção ajuda-o a decisão de melhor Olá toomake em tipos de disco e de VM.


### <a name="location"></a>Localização

Escolha uma localização onde discos gerida do Azure estão disponíveis. Se estiver a migrar discos geridos de tooPremium, certifique-se também que armazenamento Premium está disponível na região de olá onde estiver a planear toomigrate para. Consulte [byRegion de serviços do Azure](https://azure.microsoft.com/regions/#services) para obter informações atualizadas em localizações disponíveis.

### <a name="vm-sizes"></a>Tamanhos de VM

Se estiver a migrar discos geridos de tooPremium, tem de tamanho de Olá tooupdate de Olá VM tooPremium tamanho com capacidade de armazenamento disponível na região de olá onde está localizada a VM. Reveja os tamanhos de VM Olá que são compatíveis com o Premium Storage. as especificações de tamanho de VM do Azure Olá constam [tamanhos das virtual machines](sizes.md).
Reveja as características de desempenho de Olá de máquinas virtuais que funcionam com o Premium Storage e escolha Olá mais adequado tamanho da VM que melhor se adapta às sua carga de trabalho. Certifique-se de que existe largura de banda suficiente disponível no seu tráfego de disco do VM toodrive Olá.

### <a name="disk-sizes"></a>Tamanhos de disco

**Premium discos geridos**

Existem sete tipos de discos de gerido premium que podem ser utilizados com a VM e cada um tem IOPs específicos e débito limites. Quando escolher Olá tipo de disco Premium para VM com base nas necessidades de Olá da sua aplicação em termos de capacidade, desempenho, escalabilidade e carrega das horas de ponta, considere estes limites.

| Tipo de discos Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamanho do disco           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPs por disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Débito por disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo | 

**Discos geridos padrão**

Existem sete tipos de discos padrão gerido que podem ser utilizados com a VM. Cada um deles tem capacidade de diferentes, mas tem o mesmo IOPS e limites de débito. Escolha o tipo de Olá de gerido padrão discos com base nas necessidades de capacidade de Olá da sua aplicação.

| Tipo de Disco Standard  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Tamanho do disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| IOPs por disco       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Débito por disco | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 


### <a name="disk-caching-policy"></a>Política de colocação em cache em disco 

**Premium discos geridos**

Por predefinição, o disco de política de colocação em cache é *só de leitura* para Olá todos os discos de dados Premium, e *leitura e escrita* para disco do sistema operativo Olá Premium ligados toohello VM. Esta definição de configuração é recomendada tooachieve Olá um desempenho ideal para IOs a aplicação. Pesado de escrita ou só de escrita para discos de dados (por exemplo, ficheiros de registo do SQL Server), desative a colocação em cache no disco, de modo a que pode alcançar um melhor desempenho de aplicações.

### <a name="pricing"></a>Preços

Olá revisão [preços para discos geridos](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Preços dos discos de geridos Premium é a mesmo Olá os discos Premium não gerido. Mas preços para os discos padrão geridos são diferente de discos padrão de não gerido.


## <a name="checklist"></a>Lista de verificação

1.  Se estiver a migrar discos geridos de tooPremium, certifique-se de que está disponível na região de Olá que estiver a migrar para.

2.  Decida Olá novo série de VM que irá utilizar. Deve ser um com capacidade de armazenamento Premium se estiver a migrar discos geridos de tooPremium.

3.  Decida Olá exato tamanho da VM que irá utilizar que estão disponíveis na região de Olá que estiver a migrar. Tamanho da VM tem de número de Olá toobe toosupport grandes o suficiente de discos de dados que tiver. Por exemplo, se tiver quatro discos de dados, Olá VM tem de ter dois ou mais núcleos. Além disso, considere o processamento de energia, memória e as necessidades de largura de banda de rede.

4.  Ter Olá VM detalhes atuais à mão, incluindo Olá lista de discos e blobs VHD correspondentes.

Prepare a sua aplicação para o período de indisponibilidade. uma migração limpa toodo, tiver toostop todo o processamento Olá no sistema atual Olá. Só então, pode obtê-lo tooconsistent Estado, o que pode migrar toohello nova plataforma. Duração do período de indisponibilidade depende da quantidade de Olá de dados no Olá toomigrate de discos.


## <a name="migrate-hello-vm"></a>Migrar Olá VM

Prepare a sua aplicação para o período de indisponibilidade. uma migração limpa toodo, tiver toostop todo o processamento Olá no sistema atual Olá. Só então, pode obtê-lo tooconsistent Estado, o que pode migrar toohello nova plataforma. Duração do período de indisponibilidade depende da quantidade de Olá de dados no Olá toomigrate de discos.


1.  Em primeiro lugar, defina os parâmetros comuns de Olá:

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Criar um disco de SO gerido com Olá VHD de Olá VMS clássicas.

    Certifique-se de que lhe forneceu Olá concluir URI de Olá parâmetro toohello $osVhdUri de VHD de SO. Além disso, introduza **- AccountType** como **PremiumLRS** ou **StandardLRS** com base no tipo de discos (Premium ou Standard) estiver a migrar para.

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Anexar Olá SO disco toohello nova VM.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Criar um disco de dados geridos a partir do ficheiro VHD de dados de Olá e adicioná-la toohello nova VM.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  Criar Olá nova VM ao definir o IP público, rede Virtual e a NIC.

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>Poderão existir toosupport necessários passos adicionais a aplicação que não é ser abrangida neste guia.
>
>

## <a name="next-steps"></a>Passos seguintes

- Ligar a máquina virtual de toohello. Para obter instruções, consulte [como tooconnect e início de sessão tooan virtual do Azure máquina com o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

