---
title: "aaaCreate e gerir VMs do Windows no Azure que utilizar vários NICs | Microsoft Docs"
description: "Saiba como toocreate e gerir uma VM do Windows que tenha vários NICs tooit de anexado utilizando os modelos do Azure PowerShell ou Gestor de recursos."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Criar e gerir a máquina virtual do Windows que tenha vários NICs
Máquinas virtuais (VMs) no Azure pode ter vários toothem de placas (NICs) ligadas de interface de rede virtual. Um cenário comum é toohave diferentes sub-redes para a conectividade de front-end e back-end, ou uma rede dedicada tooa monitorização ou a solução de cópia de segurança. Este artigo descreve em detalhe como toocreate uma VM que tenha vários NICs ligado tooit. Também saber como NICs tooadd ou remova a partir de uma VM existente. Diferentes [tamanhos de VM](sizes.md) suportar um número de NICs variando, por isso, tamanho da VM em conformidade.

Para obter informações detalhadas, incluindo como toocreate vários NICs os seus próprios scripts do PowerShell, consulte [implementar VMs de vários NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que tem Olá [a versão mais recente do Azure PowerShell instalada e configurada](/powershell/azure/overview).

No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myVnet*, e *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Criar uma VM com vários NICs
Em primeiro lugar, crie um grupo de recursos. Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *EastUs* localização:

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Criar rede virtual e sub-redes
Um cenário comum é para uma rede virtual toohave dois ou mais sub-redes. Pode ser uma sub-rede para o tráfego de front-end, Olá para o tráfego de back-end. tooconnect tooboth sub-redes, em seguida, utilizar vários NICs na VM.

1. Definir duas sub-redes da rede virtual com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Olá exemplo a seguir define sub-redes Olá para *mySubnetFrontEnd* e *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Criar a rede virtual e a sub-redes com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Olá exemplo seguinte cria uma rede virtual denominada *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Criar vários NICs
Criar dois NICs com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Anexe um toohello NIC da sub-rede do front-end e uma sub-rede de back-end de toohello NIC. Olá exemplo seguinte cria NICs com o nome *myNic1* e *myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

Normalmente, também cria um [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) ou [Balanceador de carga](../../load-balancer/load-balancer-overview.md) toohelp gerir e distribuir o tráfego entre as suas VMs. Olá [mais detalhadas VM de vários NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artigo irá orientá-lo a criar um grupo de segurança de rede e atribuir NICs.

### <a name="create-hello-virtual-machine"></a>Criar máquina virtual de Olá
Agora inicie toobuild a configuração de VM. Cada tamanho da VM tem um limite para o número total de Olá de NICs que pode adicionar tooa VM. Para obter mais informações, consulte [tamanhos de Windows VM](sizes.md).

1. Definir o toohello de credenciais VM `$cred` variável da seguinte forma:

    ```powershell
    $cred = Get-Credential
    ```

2. Definir a VM com [novo AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig). Olá exemplo seguinte define uma VM chamada *myVM* e utiliza um tamanho VM que suporte a mais do que dois NICs (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. Criar rest Olá da sua configuração de VM com [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) e [conjunto AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage). Olá seguinte exemplo cria uma VM do Windows Server 2016:

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. Anexar Olá dois NICs que criou anteriormente com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Por fim, crie a VM com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>Adicionar tooan uma NIC existente a VM
Adicionar tooadd um tooan NIC virtual existente a VM, que desalocar Olá VM, Olá virtual NIC, em seguida, iniciar Olá VM.

1. Desalocar Olá VM com [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Olá exemplo seguinte deallocates Olá VM com o nome *myVM* no *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Obter a configuração existente de Olá do Olá VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Olá exemplo seguinte obtém as informações de Olá VM com o nome *myVM* no *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Olá exemplo seguinte cria uma NIC virtual com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) denominado *myNic3* que está ligado demasiado*mySubnetBackEnd*. Olá virtual NIC, em seguida, é anexado toohello VM com o nome *myVM* no *myResourceGroup* com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>NICs virtuais principais
    Um dos Olá NICs numa VM vários NICs precisa toobe principal. Se um dos Olá NICs virtuais existentes no Olá VM já está definida como principal, pode ignorar este passo. Olá seguinte exemplo assume que estão agora presentes numa VM dois NICs virtuais e pretende tooadd Olá NIC primeiro (`[0]`) como Olá primário:
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Iniciar Olá VM com [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Remover um NIC de VM existente
tooremove uma NIC virtual de VM existente, desalocar Olá VM, remova Olá virtual NIC, em seguida, iniciar Olá VM.

1. Desalocar Olá VM com [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Olá exemplo seguinte deallocates Olá VM com o nome *myVM* no *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Obter a configuração existente de Olá do Olá VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Olá exemplo seguinte obtém as informações de Olá VM com o nome *myVM* no *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Obter informações sobre Olá NIC remover com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface). Olá exemplo seguinte obtém as informações *myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Remover Olá NIC com [remover AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) e, em seguida, atualize Olá VM com [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm). Olá exemplo a seguir remove *myNic3* tal como obtidas pelo `$nicId` no Olá precedente passo:

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Iniciar Olá VM com [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Criar vários NICs com modelos
Modelos Azure Resource Manager fornecem uma forma toocreate várias instâncias de um recurso durante a implementação, tais como criar vários NICs. Modelos do Resource Manager utilizam declarativa toodefine de ficheiros JSON seu ambiente. Para obter mais informações, consulte [descrição geral do Gestor de recursos do Azure](../../azure-resource-manager/resource-group-overview.md). Pode utilizar *cópia* toospecify Olá diversas toocreate de instâncias:

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Para obter mais informações, consulte [criar várias instâncias utilizando *cópia*](../../resource-group-create-multiple.md). 

Também pode utilizar `copyIndex()` tooappend um nome de recurso tooa número. Em seguida, pode criar *myNic1*, *MyNic2* e assim sucessivamente. Olá código seguinte mostra um exemplo de acrescentar um valor de índice Olá:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Pode ler um exemplo completo de [criar vários NICs utilizando modelos do Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Passos seguintes
Reveja [tamanhos de Windows VM](sizes.md) quando está a tentar toocreate uma VM que tenha vários NICs. Preste atenção toohello número máximo NICs que suporte a cada tamanho da VM. 


