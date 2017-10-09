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
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="463d2-103">Criar uma VM a partir de uma imagem gerida</span><span class="sxs-lookup"><span data-stu-id="463d2-103">Create a VM from a managed image</span></span>

<span data-ttu-id="463d2-104">Pode criar várias VMs a partir de uma imagem VM gerida no Azure.</span><span class="sxs-lookup"><span data-stu-id="463d2-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="463d2-105">Uma imagem VM gerida contém Olá informações necessárias toocreate uma VM, incluindo Olá SO e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="463d2-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="463d2-106">Olá VHDs que compõem a imagem de Olá, incluindo discos Olá SO e discos de dados, são armazenadas como discos geridos.</span><span class="sxs-lookup"><span data-stu-id="463d2-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="463d2-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="463d2-107">Prerequisites</span></span>

<span data-ttu-id="463d2-108">É necessário toohave já [criada uma imagem VM gerida](capture-image-resource.md) toouse para criar Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="463d2-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="463d2-109">Certifique-se de que têm versões mais recentes do Olá dos módulos de Olá AzureRM.Compute e AzureRM.Network PowerShell.</span><span class="sxs-lookup"><span data-stu-id="463d2-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="463d2-110">Abra uma linha de comandos do PowerShell como administrador e execute Olá os seguintes comandos tooinstall-los.</span><span class="sxs-lookup"><span data-stu-id="463d2-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="463d2-111">Para obter mais informações, consulte [controlo de versões do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="463d2-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="463d2-112">Recolher informações sobre a imagem de Olá</span><span class="sxs-lookup"><span data-stu-id="463d2-112">Collect information about hello image</span></span>

<span data-ttu-id="463d2-113">Primeiro vamos precisar toogather informações básicas sobre a imagem de Olá e criar uma variável para a imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="463d2-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="463d2-114">Este exemplo utiliza uma imagem VM gerida com o nome **myImage** que está em Olá **myResourceGroup** grupo de recursos no Olá **Central EUA oeste** localização.</span><span class="sxs-lookup"><span data-stu-id="463d2-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="463d2-115">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="463d2-115">Create a virtual network</span></span>
<span data-ttu-id="463d2-116">Criar vNet Olá e sub-rede de Olá [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="463d2-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="463d2-117">Crie Olá sub-rede.</span><span class="sxs-lookup"><span data-stu-id="463d2-117">Create hello subnet.</span></span> <span data-ttu-id="463d2-118">Este exemplo cria uma sub-rede designada **mySubnet** com o prefixo de endereço Olá de **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="463d2-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="463d2-119">Crie rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="463d2-119">Create hello virtual network.</span></span> <span data-ttu-id="463d2-120">Este exemplo cria uma rede virtual denominada **myVnet** com o prefixo de endereço Olá de **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="463d2-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="463d2-121">Criar uma interface de rede e o endereço IP pública</span><span class="sxs-lookup"><span data-stu-id="463d2-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="463d2-122">tooenable comunicação com a máquina virtual de Olá na rede virtual Olá, precisa de um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="463d2-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="463d2-123">Crie um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="463d2-123">Create a public IP address.</span></span> <span data-ttu-id="463d2-124">Este exemplo cria um endereço IP público com o nome **myPip**.</span><span class="sxs-lookup"><span data-stu-id="463d2-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="463d2-125">Criar Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="463d2-125">Create hello NIC.</span></span> <span data-ttu-id="463d2-126">Este exemplo cria um NIC com o nome **myNic**.</span><span class="sxs-lookup"><span data-stu-id="463d2-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="463d2-127">Criar grupo de segurança de rede Olá e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="463d2-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="463d2-128">toobe toolog consegue no tooyour VM através de RDP, terá de toohave uma regra de segurança de rede (NSG) que permite o acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="463d2-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="463d2-129">Este exemplo cria um NSG denominado **myNsg** que contenha uma regra denominada **myRdpRule** que permite tráfego RDP de através da porta 3389.</span><span class="sxs-lookup"><span data-stu-id="463d2-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="463d2-130">Para obter mais informações sobre NSGs, consulte [abrir portas tooa VM no Azure utilizando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="463d2-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="463d2-131">Criar uma variável para a rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="463d2-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="463d2-132">Crie uma variável para a rede virtual Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="463d2-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="463d2-133">Obter credenciais Olá para Olá VM</span><span class="sxs-lookup"><span data-stu-id="463d2-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="463d2-134">Olá seguinte cmdlet irá abrir uma janela onde irá introduzir um novo toouse de nome e palavra-passe de utilizador como conta de administrador local Olá para aceder remotamente a Olá VM.</span><span class="sxs-lookup"><span data-stu-id="463d2-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="463d2-135">As variáveis de conjunto para Olá VM nome, nome do computador e Olá tamanho de Olá VM</span><span class="sxs-lookup"><span data-stu-id="463d2-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="463d2-136">Crie variáveis de nome de VM de Olá e nome do computador.</span><span class="sxs-lookup"><span data-stu-id="463d2-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="463d2-137">Neste exemplo define o nome da VM Olá como **myVM** e nome do computador Olá como **myComputer**.</span><span class="sxs-lookup"><span data-stu-id="463d2-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="463d2-138">Definir Olá tamanho de Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="463d2-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="463d2-139">Este exemplo cria **Standard_DS1_v2** tamanho de VM.</span><span class="sxs-lookup"><span data-stu-id="463d2-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="463d2-140">Consulte Olá [tamanhos de VM](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentação para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="463d2-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="463d2-141">Adicione Olá nome da VM e configuração de VM de toohello de tamanho.</span><span class="sxs-lookup"><span data-stu-id="463d2-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="463d2-142">Imagem de VM do conjunto Olá como imagem de origem para Olá nova VM</span><span class="sxs-lookup"><span data-stu-id="463d2-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="463d2-143">Definir a imagem de origem Olá utilizando Olá ID da imagem VM Olá gerido.</span><span class="sxs-lookup"><span data-stu-id="463d2-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="463d2-144">Definir a configuração do SO Olá e adicione a NIC de Olá.</span><span class="sxs-lookup"><span data-stu-id="463d2-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="463d2-145">Introduza o tipo de armazenamento Olá (PremiumLRS ou StandardLRS) e o tamanho do disco do SO Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="463d2-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="463d2-146">Neste exemplo, define o tipo de conta Olá demasiado**PremiumLRS**, Olá o tamanho do disco demasiado**128 GB** e disco a colocação em cache demasiado**ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="463d2-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="463d2-147">Criar Olá VM</span><span class="sxs-lookup"><span data-stu-id="463d2-147">Create hello VM</span></span>

<span data-ttu-id="463d2-148">Criar Olá nova Vm utilizando a configuração de Olá que vamos ter criado e armazenado no Olá **$vm** variável.</span><span class="sxs-lookup"><span data-stu-id="463d2-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="463d2-149">Certifique-se de que Olá que VM foi criada</span><span class="sxs-lookup"><span data-stu-id="463d2-149">Verify that hello VM was created</span></span>
<span data-ttu-id="463d2-150">Quando terminar, deverá ver Olá recém-criado VM na Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou utilizando o seguinte Olá Comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="463d2-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="463d2-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="463d2-151">Next steps</span></span>
<span data-ttu-id="463d2-152">toomanage a nova máquina virtual com o Azure PowerShell, consulte [criar e gerir VMs do Windows com o módulo do Azure PowerShell Olá](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="463d2-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

