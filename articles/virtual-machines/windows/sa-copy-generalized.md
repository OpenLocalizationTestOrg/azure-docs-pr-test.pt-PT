---
title: "aaaCreate uma imagem de uma VM no Azure generalizada não gerida | Microsoft Docs"
description: "Crie uma imagem unmanged um generalizado toouse toocreate da VM do Windows várias cópias de uma VM no Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Como toocreate uma VM não gerida imagem de VM do Azure

Este artigo abrange a utilização de contas de armazenamento. Recomendamos que utilize discos geridos e imagens geridas em vez de uma conta de armazenamento. Para obter mais informações, consulte [capturar uma imagem gerida de uma VM no Azure generalizada](capture-image-resource.md).

Este artigo mostra como toouse Azure PowerShell toocreate uma imagem de uma VM do Azure generalizado através de uma conta de armazenamento. Em seguida, pode utilizar Olá imagem toocreate outra VM. imagem de Olá inclui o disco do SO Olá e discos de dados de Olá destinadas a máquina virtual de toohello anexado. imagem de Olá não inclui recursos de rede virtual Olá, por isso terá de tooset esses recursos quando criar Olá nova VM. 

## <a name="prerequisites"></a>Pré-requisitos
Terá de toohave Azure PowerShell versão 1.0.x ou mais recente instalada. Se já não tiver instalado o PowerShell, leia [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter os passos de instalação.

## <a name="generalize-hello-vm"></a>Generalizar Olá VM 
Esta secção mostra-lhe como toogeneralize a máquina virtual do Windows para utilização como uma imagem. Generalizar uma VM remove todas as informações pessoais da conta, entre outras coisas e prepara Olá máquina toobe utilizado como uma imagem. Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).

Certifique-se em execução na máquina de Olá funções de servidor de Olá são suportadas pelo Sysprep. Para obter mais informações, consulte [suporte de Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Se estiver a carregar o tooAzure VHD para Olá pela primeira vez, certifique-se de que tem [preparado VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep. 
> 
> 

Também pode generalizar uma VM com Linux utilizando `sudo waagent -deprovision+user` e, em seguida, utilizar o PowerShell toocapture Olá VM. Para obter informações sobre como utilizar a CLI de Olá toocapture uma VM, consulte [como toogeneralize e capturar uma máquina virtual do Linux utilizando Olá CLI do Azure ](../linux/capture-image.md).


1. Inicie sessão no toohello máquina virtual do Windows.
2. Abra a janela de linha de comandos de Olá como administrador. Altere o diretório de Olá demasiado**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.
3. No Olá **ferramenta de preparação de sistema** caixa de diálogo, selecione **introduza sistema Out-of-Box experiência (OOBE)**e certifique-se de que Olá **Generalize** caixa de verificação está selecionada.
4. No **as opções de encerramento**, selecione **encerramento**.
5. Clique em **OK**.
   
    ![Iniciar o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Quando tiver concluído o Sysprep, encerra Olá máquina. 

> [!IMPORTANT]
> Não reinicie Olá VM até que sejam efectuada tooAzure VHD Olá carregar ou criar uma imagem de Olá VM. Se, acidentalmente, Olá VM obtém reiniciada, execute o Sysprep toogeneralize-a novamente.
> 
> 

## <a name="log-in-tooazure-powershell"></a>Inicie sessão no tooAzure PowerShell
1. Abra o Azure PowerShell e inicie sessão tooyour conta do Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Abre uma janela de pop-up para tooenter as credenciais da conta do Azure.
2. Obter IDs de subscrição de Olá para as subscrições disponíveis.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Definir a subscrição correta Olá com o ID de subscrição. Olá
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Desalocar Olá VM e defina Olá Estado toogeneralized
1. Anular a atribuição de recursos da VM Olá.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    Olá *estado* para Olá VM na Olá Azure portal é alterado de **parado** demasiado**parado (desalocado)**.
2. Definir o estado de Olá da máquina virtual de Olá demasiado**generalizado**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Verifique o estado de Olá de Olá VM. Olá **OSState/generalizado** secção para Olá VM deve ter Olá **DisplayStatus** definido demasiado**VM generalizado**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Criar imagem Olá

Crie uma imagem de máquinas de virtuais não geridos no contentor de armazenamento de destino de Olá utilizando este comando. Olá imagem é criada na Olá mesma conta de armazenamento como Olá máquina virtual original. Olá `-Path` parâmetro guarda uma cópia do modelo JSON Olá Olá origem VM tooyour do computador local. Olá `-DestinationContainerName` parâmetro é o nome de Olá do contentor de Olá que pretende toohold as imagens. Se não existir contentor Olá, é criado para si.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Pode obter Olá URL da imagem de modelo de ficheiro Olá JSON. Aceda toohello **recursos** > **storageProfile** > **osDisk** > **imagem**  >  **uri** secção para o caminho completo do Olá da imagem. aspeto Olá URL da imagem de Olá: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
Também pode verificar Olá URI no portal de Olá. imagem de Olá é copiado tooa contentor com o nome **sistema** na sua conta de armazenamento. 

## <a name="create-a-vm-from-hello-image"></a>Criar uma VM a partir da imagem de Olá

Agora, pode criar uma ou mais VMs da imagem não gerido Olá.

### <a name="set-hello-uri-of-hello-vhd"></a>Definir Olá URI de Olá VHD

Olá URI para Olá VHD toouse está num formato de Olá: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**. vhd. Neste exemplo Olá VHD denominado **myVHD** na conta de armazenamento Olá **mystorageaccount** no contentor de Olá **mycontainer**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Criar uma rede virtual
Criar vNet Olá e sub-rede de Olá [rede virtual](../../virtual-network/virtual-networks-overview.md).

1. Crie Olá sub-rede. Olá exemplo seguinte cria uma sub-rede designada **mySubnet** no grupo de recursos de Olá **myResourceGroup** com o prefixo de endereço Olá de **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crie rede virtual Olá. Olá exemplo seguinte cria uma rede virtual denominada **myVnet** no Olá **EUA oeste** localização com o prefixo de endereço Olá de **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Criar uma interface de rede e o endereço IP pública
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

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Criar grupo de segurança de rede Olá e uma regra RDP
toobe toolog consegue no tooyour VM através de RDP, terá de toohave uma regra de segurança que permite o acesso RDP na porta 3389. 

Este exemplo cria um NSG denominado **myNsg** que contenha uma regra denominada **myRdpRule** que permite tráfego RDP de através da porta 3389. Para obter mais informações sobre NSGs, consulte [abrir portas tooa VM no Azure utilizando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Criar uma variável para a rede virtual Olá
Crie uma variável para a rede virtual Olá foi concluída. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Criar Olá VM
Olá PowerShell seguintes realiza configurações de máquina virtual de Olá e utiliza a imagem não gerida como origem de Olá para a instalação do novo Olá.

</br>

```powershell
    # Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-hello-vm-was-created"></a>Certifique-se de que Olá que VM foi criada
Quando terminar, deverá ver Olá recém-criado VM na Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou utilizando o seguinte Olá Comandos do PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Passos seguintes
toomanage a nova máquina virtual com o Azure PowerShell, consulte [gerir máquinas virtuais utilizando o Azure Resource Manager e o PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


