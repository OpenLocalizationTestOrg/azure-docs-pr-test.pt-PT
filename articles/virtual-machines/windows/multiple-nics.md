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
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="3aba5-103">Criar e gerir a máquina virtual do Windows que tenha vários NICs</span><span class="sxs-lookup"><span data-stu-id="3aba5-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="3aba5-104">Máquinas virtuais (VMs) no Azure pode ter vários toothem de placas (NICs) ligadas de interface de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3aba5-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="3aba5-105">Um cenário comum é toohave diferentes sub-redes para a conectividade de front-end e back-end, ou uma rede dedicada tooa monitorização ou a solução de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="3aba5-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="3aba5-106">Este artigo descreve em detalhe como toocreate uma VM que tenha vários NICs ligado tooit.</span><span class="sxs-lookup"><span data-stu-id="3aba5-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="3aba5-107">Também saber como NICs tooadd ou remova a partir de uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="3aba5-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="3aba5-108">Diferentes [tamanhos de VM](sizes.md) suportar um número de NICs variando, por isso, tamanho da VM em conformidade.</span><span class="sxs-lookup"><span data-stu-id="3aba5-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="3aba5-109">Para obter informações detalhadas, incluindo como toocreate vários NICs os seus próprios scripts do PowerShell, consulte [implementar VMs de vários NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3aba5-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3aba5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3aba5-110">Prerequisites</span></span>
<span data-ttu-id="3aba5-111">Certifique-se de que tem Olá [a versão mais recente do Azure PowerShell instalada e configurada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3aba5-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="3aba5-112">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="3aba5-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3aba5-113">Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myVnet*, e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="3aba5-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="3aba5-114">Criar uma VM com vários NICs</span><span class="sxs-lookup"><span data-stu-id="3aba5-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="3aba5-115">Em primeiro lugar, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3aba5-115">First, create a resource group.</span></span> <span data-ttu-id="3aba5-116">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *EastUs* localização:</span><span class="sxs-lookup"><span data-stu-id="3aba5-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="3aba5-117">Criar rede virtual e sub-redes</span><span class="sxs-lookup"><span data-stu-id="3aba5-117">Create virtual network and subnets</span></span>
<span data-ttu-id="3aba5-118">Um cenário comum é para uma rede virtual toohave dois ou mais sub-redes.</span><span class="sxs-lookup"><span data-stu-id="3aba5-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="3aba5-119">Pode ser uma sub-rede para o tráfego de front-end, Olá para o tráfego de back-end.</span><span class="sxs-lookup"><span data-stu-id="3aba5-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="3aba5-120">tooconnect tooboth sub-redes, em seguida, utilizar vários NICs na VM.</span><span class="sxs-lookup"><span data-stu-id="3aba5-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="3aba5-121">Definir duas sub-redes da rede virtual com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="3aba5-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="3aba5-122">Olá exemplo a seguir define sub-redes Olá para *mySubnetFrontEnd* e *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="3aba5-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="3aba5-123">Criar a rede virtual e a sub-redes com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="3aba5-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="3aba5-124">Olá exemplo seguinte cria uma rede virtual denominada *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="3aba5-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="3aba5-125">Criar vários NICs</span><span class="sxs-lookup"><span data-stu-id="3aba5-125">Create multiple NICs</span></span>
<span data-ttu-id="3aba5-126">Criar dois NICs com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="3aba5-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="3aba5-127">Anexe um toohello NIC da sub-rede do front-end e uma sub-rede de back-end de toohello NIC.</span><span class="sxs-lookup"><span data-stu-id="3aba5-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="3aba5-128">Olá exemplo seguinte cria NICs com o nome *myNic1* e *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="3aba5-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

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

<span data-ttu-id="3aba5-129">Normalmente, também cria um [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) ou [Balanceador de carga](../../load-balancer/load-balancer-overview.md) toohelp gerir e distribuir o tráfego entre as suas VMs.</span><span class="sxs-lookup"><span data-stu-id="3aba5-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="3aba5-130">Olá [mais detalhadas VM de vários NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artigo irá orientá-lo a criar um grupo de segurança de rede e atribuir NICs.</span><span class="sxs-lookup"><span data-stu-id="3aba5-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="3aba5-131">Criar máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="3aba5-131">Create hello virtual machine</span></span>
<span data-ttu-id="3aba5-132">Agora inicie toobuild a configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="3aba5-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="3aba5-133">Cada tamanho da VM tem um limite para o número total de Olá de NICs que pode adicionar tooa VM.</span><span class="sxs-lookup"><span data-stu-id="3aba5-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="3aba5-134">Para obter mais informações, consulte [tamanhos de Windows VM](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="3aba5-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="3aba5-135">Definir o toohello de credenciais VM `$cred` variável da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="3aba5-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="3aba5-136">Definir a VM com [novo AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="3aba5-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="3aba5-137">Olá exemplo seguinte define uma VM chamada *myVM* e utiliza um tamanho VM que suporte a mais do que dois NICs (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="3aba5-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="3aba5-138">Criar rest Olá da sua configuração de VM com [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) e [conjunto AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="3aba5-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="3aba5-139">Olá seguinte exemplo cria uma VM do Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="3aba5-139">hello following example creates a Windows Server 2016 VM:</span></span>

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

4. <span data-ttu-id="3aba5-140">Anexar Olá dois NICs que criou anteriormente com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="3aba5-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="3aba5-141">Por fim, crie a VM com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="3aba5-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="3aba5-142">Adicionar tooan uma NIC existente a VM</span><span class="sxs-lookup"><span data-stu-id="3aba5-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="3aba5-143">Adicionar tooadd um tooan NIC virtual existente a VM, que desalocar Olá VM, Olá virtual NIC, em seguida, iniciar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="3aba5-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="3aba5-144">Desalocar Olá VM com [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3aba5-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="3aba5-145">Olá exemplo seguinte deallocates Olá VM com o nome *myVM* no *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3aba5-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="3aba5-146">Obter a configuração existente de Olá do Olá VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3aba5-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="3aba5-147">Olá exemplo seguinte obtém as informações de Olá VM com o nome *myVM* no *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3aba5-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="3aba5-148">Olá exemplo seguinte cria uma NIC virtual com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) denominado *myNic3* que está ligado demasiado*mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="3aba5-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="3aba5-149">Olá virtual NIC, em seguida, é anexado toohello VM com o nome *myVM* no *myResourceGroup* com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="3aba5-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

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

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="3aba5-150">NICs virtuais principais</span><span class="sxs-lookup"><span data-stu-id="3aba5-150">Primary virtual NICs</span></span>
    <span data-ttu-id="3aba5-151">Um dos Olá NICs numa VM vários NICs precisa toobe principal.</span><span class="sxs-lookup"><span data-stu-id="3aba5-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="3aba5-152">Se um dos Olá NICs virtuais existentes no Olá VM já está definida como principal, pode ignorar este passo.</span><span class="sxs-lookup"><span data-stu-id="3aba5-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="3aba5-153">Olá seguinte exemplo assume que estão agora presentes numa VM dois NICs virtuais e pretende tooadd Olá NIC primeiro (`[0]`) como Olá primário:</span><span class="sxs-lookup"><span data-stu-id="3aba5-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="3aba5-154">Iniciar Olá VM com [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="3aba5-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="3aba5-155">Remover um NIC de VM existente</span><span class="sxs-lookup"><span data-stu-id="3aba5-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="3aba5-156">tooremove uma NIC virtual de VM existente, desalocar Olá VM, remova Olá virtual NIC, em seguida, iniciar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="3aba5-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="3aba5-157">Desalocar Olá VM com [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3aba5-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="3aba5-158">Olá exemplo seguinte deallocates Olá VM com o nome *myVM* no *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3aba5-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="3aba5-159">Obter a configuração existente de Olá do Olá VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3aba5-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="3aba5-160">Olá exemplo seguinte obtém as informações de Olá VM com o nome *myVM* no *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3aba5-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="3aba5-161">Obter informações sobre Olá NIC remover com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="3aba5-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="3aba5-162">Olá exemplo seguinte obtém as informações *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="3aba5-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="3aba5-163">Remover Olá NIC com [remover AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) e, em seguida, atualize Olá VM com [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3aba5-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="3aba5-164">Olá exemplo a seguir remove *myNic3* tal como obtidas pelo `$nicId` no Olá precedente passo:</span><span class="sxs-lookup"><span data-stu-id="3aba5-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="3aba5-165">Iniciar Olá VM com [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="3aba5-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="3aba5-166">Criar vários NICs com modelos</span><span class="sxs-lookup"><span data-stu-id="3aba5-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="3aba5-167">Modelos Azure Resource Manager fornecem uma forma toocreate várias instâncias de um recurso durante a implementação, tais como criar vários NICs.</span><span class="sxs-lookup"><span data-stu-id="3aba5-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="3aba5-168">Modelos do Resource Manager utilizam declarativa toodefine de ficheiros JSON seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="3aba5-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="3aba5-169">Para obter mais informações, consulte [descrição geral do Gestor de recursos do Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3aba5-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="3aba5-170">Pode utilizar *cópia* toospecify Olá diversas toocreate de instâncias:</span><span class="sxs-lookup"><span data-stu-id="3aba5-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="3aba5-171">Para obter mais informações, consulte [criar várias instâncias utilizando *cópia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3aba5-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="3aba5-172">Também pode utilizar `copyIndex()` tooappend um nome de recurso tooa número.</span><span class="sxs-lookup"><span data-stu-id="3aba5-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="3aba5-173">Em seguida, pode criar *myNic1*, *MyNic2* e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="3aba5-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="3aba5-174">Olá código seguinte mostra um exemplo de acrescentar um valor de índice Olá:</span><span class="sxs-lookup"><span data-stu-id="3aba5-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="3aba5-175">Pode ler um exemplo completo de [criar vários NICs utilizando modelos do Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="3aba5-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3aba5-176">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3aba5-176">Next steps</span></span>
<span data-ttu-id="3aba5-177">Reveja [tamanhos de Windows VM](sizes.md) quando está a tentar toocreate uma VM que tenha vários NICs.</span><span class="sxs-lookup"><span data-stu-id="3aba5-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="3aba5-178">Preste atenção toohello número máximo NICs que suporte a cada tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="3aba5-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


