---
title: "aaaCreate imagens VM personalizadas com Olá Azure PowerShell | Microsoft Docs"
description: "Tutorial - criar uma imagem VM personalizada utilizando Olá Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>Criar uma imagem personalizada da VM do Azure com o PowerShell

São imagens personalizadas, como imagens do marketplace, mas que são criados por si. Imagens personalizadas podem ser utilizados toobootstrap configurações, tais como o pré-carregamento de aplicações, configurações de aplicação e outras configurações de SO. Neste tutorial, vai criar sua imagem personalizada de uma máquina virtual do Azure. Saiba como:

> [!div class="checklist"]
> * Sysprep e generalizar VMs
> * Criar uma imagem personalizada
> * Criar uma VM a partir de uma imagem personalizada
> * Lista todas as imagens de Olá na sua subscrição
> * Eliminar uma imagem

Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior. Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind. Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).

## <a name="before-you-begin"></a>Antes de começar

passos de Olá abaixo de detalhe como tootake uma VM existente e ative a imagem para um reutilizável personalizado que podem utilizar toocreate novas instâncias de VM.

exemplo de Olá toocomplete neste tutorial, tem de ter uma máquina virtual existente. Se for necessário, isto [script de exemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) pode criar uma por si. Quando trabalhar com tutorial de Olá, substitua o grupo de recursos de Olá e VM nomes sempre que necessário.

## <a name="prepare-vm"></a>Preparar a VM

toocreate uma imagem de uma máquina virtual, terá de tooprepare Olá VM por generalizar Olá VM, Desalocação e, em seguida, marcar Olá de VM de origem como generalizado no Azure.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalizar Olá VM do Windows com o Sysprep

Sysprep remove todas as informações pessoais da conta, entre outras coisas e prepara Olá máquina toobe utilizado como uma imagem. Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).


1. Ligar a máquina virtual de toohello.
2. Abra a janela de linha de comandos de Olá como administrador. Altere o diretório de Olá demasiado*%windir%\system32\sysprep*e, em seguida, execute *sysprep.exe*.
3. No Olá **ferramenta de preparação de sistema** caixa de diálogo, selecione *introduza sistema Out-of-Box experiência (OOBE)*e certifique-se de que Olá *Generalize* caixa de verificação está selecionada.
4. No **as opções de encerramento**, selecione *encerramento* e, em seguida, clique em **OK**.
5. Quando tiver concluído o Sysprep, encerra Olá máquina. **Não reiniciar Olá VM**.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Desalocar e marcar Olá VM como generalizado

toocreate uma imagem, tem de Olá VM toobe desalocada e marcada como generalizado no Azure.

Olá desalocada VM utilizando [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Definir o estado de Olá da máquina virtual de Olá demasiado`-Generalized` utilizando [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm). 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Criar imagem Olá

Agora pode criar uma imagem de VM de Olá utilizando [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) e [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage). Olá exemplo seguinte cria uma imagem com o nome *myImage* de uma VM chamada *myVM*.

Obter a máquina virtual de Olá. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Crie a configuração de imagem de Olá.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Crie imagem Olá.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Criar as VMs da imagem de Olá

Agora que tem uma imagem, pode criar uma ou mais VMs novas da imagem de Olá. Criar uma VM a partir de uma imagem personalizada é muito semelhante toocreating uma VM utilizando uma imagem do Marketplace. Quando utilizar uma imagem do Marketplace, tem tooinformation sobre a imagem de Olá, o fornecedor de imagem, oferta, SKU e versão. Com uma imagem personalizada, basta tooprovide Olá ID de recurso de imagem personalizada Olá. 

Olá script a seguir, iremos criar uma variável *$image* toostore informações sobre a utilização de imagem personalizada Olá [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) e, em seguida, utilizamos [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)e especifique o ID de Olá utilizando Olá *$image* variável acabamos de criar. 

script de Olá cria uma VM chamada *myVMfromImage* do nosso imagem personalizada num novo grupo de recursos denominado *myResourceGroupFromImage* no Olá *EUA oeste* localização.


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>Gestão de imagens 

Seguem-se alguns exemplos comuns imagem das tarefas de gestão e como toocomplete-las através do PowerShell.

Liste todas as imagens de por nome.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

Elimine uma imagem. Neste exemplo eliminações Olá imagem com o nome *myOldImage* de Olá *myResourceGroup*.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, vai criar uma imagem VM personalizada. Aprendeu a:

> [!div class="checklist"]
> * Sysprep e generalizar VMs
> * Criar uma imagem personalizada
> * Criar uma VM a partir de uma imagem personalizada
> * Lista todas as imagens de Olá na sua subscrição
> * Eliminar uma imagem

Produzir toohello seguinte toolearn tutorial sobre máquinas virtuais como elevada.

> [!div class="nextstepaction"]
> [Criar VMs de elevada disponibilidade](tutorial-availability-sets.md)



