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
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="a9db0-103">Criar uma imagem personalizada da VM do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9db0-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="a9db0-104">São imagens personalizadas, como imagens do marketplace, mas que são criados por si.</span><span class="sxs-lookup"><span data-stu-id="a9db0-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="a9db0-105">Imagens personalizadas podem ser utilizados toobootstrap configurações, tais como o pré-carregamento de aplicações, configurações de aplicação e outras configurações de SO.</span><span class="sxs-lookup"><span data-stu-id="a9db0-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="a9db0-106">Neste tutorial, vai criar sua imagem personalizada de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9db0-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="a9db0-107">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="a9db0-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a9db0-108">Sysprep e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="a9db0-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="a9db0-109">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="a9db0-109">Create a custom image</span></span>
> * <span data-ttu-id="a9db0-110">Criar uma VM a partir de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="a9db0-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="a9db0-111">Lista todas as imagens de Olá na sua subscrição</span><span class="sxs-lookup"><span data-stu-id="a9db0-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="a9db0-112">Eliminar uma imagem</span><span class="sxs-lookup"><span data-stu-id="a9db0-112">Delete an image</span></span>

<span data-ttu-id="a9db0-113">Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a9db0-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="a9db0-114">Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="a9db0-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="a9db0-115">Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a9db0-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a9db0-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a9db0-116">Before you begin</span></span>

<span data-ttu-id="a9db0-117">passos de Olá abaixo de detalhe como tootake uma VM existente e ative a imagem para um reutilizável personalizado que podem utilizar toocreate novas instâncias de VM.</span><span class="sxs-lookup"><span data-stu-id="a9db0-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="a9db0-118">exemplo de Olá toocomplete neste tutorial, tem de ter uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="a9db0-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="a9db0-119">Se for necessário, isto [script de exemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) pode criar uma por si.</span><span class="sxs-lookup"><span data-stu-id="a9db0-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="a9db0-120">Quando trabalhar com tutorial de Olá, substitua o grupo de recursos de Olá e VM nomes sempre que necessário.</span><span class="sxs-lookup"><span data-stu-id="a9db0-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="a9db0-121">Preparar a VM</span><span class="sxs-lookup"><span data-stu-id="a9db0-121">Prepare VM</span></span>

<span data-ttu-id="a9db0-122">toocreate uma imagem de uma máquina virtual, terá de tooprepare Olá VM por generalizar Olá VM, Desalocação e, em seguida, marcar Olá de VM de origem como generalizado no Azure.</span><span class="sxs-lookup"><span data-stu-id="a9db0-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="a9db0-123">Generalizar Olá VM do Windows com o Sysprep</span><span class="sxs-lookup"><span data-stu-id="a9db0-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="a9db0-124">Sysprep remove todas as informações pessoais da conta, entre outras coisas e prepara Olá máquina toobe utilizado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="a9db0-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="a9db0-125">Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9db0-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="a9db0-126">Ligar a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="a9db0-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="a9db0-127">Abra a janela de linha de comandos de Olá como administrador.</span><span class="sxs-lookup"><span data-stu-id="a9db0-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="a9db0-128">Altere o diretório de Olá demasiado*%windir%\system32\sysprep*e, em seguida, execute *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="a9db0-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="a9db0-129">No Olá **ferramenta de preparação de sistema** caixa de diálogo, selecione *introduza sistema Out-of-Box experiência (OOBE)*e certifique-se de que Olá *Generalize* caixa de verificação está selecionada.</span><span class="sxs-lookup"><span data-stu-id="a9db0-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="a9db0-130">No **as opções de encerramento**, selecione *encerramento* e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9db0-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="a9db0-131">Quando tiver concluído o Sysprep, encerra Olá máquina.</span><span class="sxs-lookup"><span data-stu-id="a9db0-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="a9db0-132">**Não reiniciar Olá VM**.</span><span class="sxs-lookup"><span data-stu-id="a9db0-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="a9db0-133">Desalocar e marcar Olá VM como generalizado</span><span class="sxs-lookup"><span data-stu-id="a9db0-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="a9db0-134">toocreate uma imagem, tem de Olá VM toobe desalocada e marcada como generalizado no Azure.</span><span class="sxs-lookup"><span data-stu-id="a9db0-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="a9db0-135">Olá desalocada VM utilizando [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="a9db0-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="a9db0-136">Definir o estado de Olá da máquina virtual de Olá demasiado`-Generalized` utilizando [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="a9db0-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="a9db0-137">Criar imagem Olá</span><span class="sxs-lookup"><span data-stu-id="a9db0-137">Create hello image</span></span>

<span data-ttu-id="a9db0-138">Agora pode criar uma imagem de VM de Olá utilizando [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) e [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="a9db0-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="a9db0-139">Olá exemplo seguinte cria uma imagem com o nome *myImage* de uma VM chamada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="a9db0-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="a9db0-140">Obter a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="a9db0-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="a9db0-141">Crie a configuração de imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="a9db0-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="a9db0-142">Crie imagem Olá.</span><span class="sxs-lookup"><span data-stu-id="a9db0-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="a9db0-143">Criar as VMs da imagem de Olá</span><span class="sxs-lookup"><span data-stu-id="a9db0-143">Create VMs from hello image</span></span>

<span data-ttu-id="a9db0-144">Agora que tem uma imagem, pode criar uma ou mais VMs novas da imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="a9db0-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="a9db0-145">Criar uma VM a partir de uma imagem personalizada é muito semelhante toocreating uma VM utilizando uma imagem do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a9db0-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="a9db0-146">Quando utilizar uma imagem do Marketplace, tem tooinformation sobre a imagem de Olá, o fornecedor de imagem, oferta, SKU e versão.</span><span class="sxs-lookup"><span data-stu-id="a9db0-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="a9db0-147">Com uma imagem personalizada, basta tooprovide Olá ID de recurso de imagem personalizada Olá.</span><span class="sxs-lookup"><span data-stu-id="a9db0-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="a9db0-148">Olá script a seguir, iremos criar uma variável *$image* toostore informações sobre a utilização de imagem personalizada Olá [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) e, em seguida, utilizamos [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)e especifique o ID de Olá utilizando Olá *$image* variável acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="a9db0-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="a9db0-149">script de Olá cria uma VM chamada *myVMfromImage* do nosso imagem personalizada num novo grupo de recursos denominado *myResourceGroupFromImage* no Olá *EUA oeste* localização.</span><span class="sxs-lookup"><span data-stu-id="a9db0-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


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

## <a name="image-management"></a><span data-ttu-id="a9db0-150">Gestão de imagens</span><span class="sxs-lookup"><span data-stu-id="a9db0-150">Image management</span></span> 

<span data-ttu-id="a9db0-151">Seguem-se alguns exemplos comuns imagem das tarefas de gestão e como toocomplete-las através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9db0-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="a9db0-152">Liste todas as imagens de por nome.</span><span class="sxs-lookup"><span data-stu-id="a9db0-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="a9db0-153">Elimine uma imagem.</span><span class="sxs-lookup"><span data-stu-id="a9db0-153">Delete an image.</span></span> <span data-ttu-id="a9db0-154">Neste exemplo eliminações Olá imagem com o nome *myOldImage* de Olá *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="a9db0-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a9db0-155">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a9db0-155">Next steps</span></span>

<span data-ttu-id="a9db0-156">Neste tutorial, vai criar uma imagem VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="a9db0-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="a9db0-157">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="a9db0-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a9db0-158">Sysprep e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="a9db0-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="a9db0-159">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="a9db0-159">Create a custom image</span></span>
> * <span data-ttu-id="a9db0-160">Criar uma VM a partir de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="a9db0-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="a9db0-161">Lista todas as imagens de Olá na sua subscrição</span><span class="sxs-lookup"><span data-stu-id="a9db0-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="a9db0-162">Eliminar uma imagem</span><span class="sxs-lookup"><span data-stu-id="a9db0-162">Delete an image</span></span>

<span data-ttu-id="a9db0-163">Produzir toohello seguinte toolearn tutorial sobre máquinas virtuais como elevada.</span><span class="sxs-lookup"><span data-stu-id="a9db0-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a9db0-164">Criar VMs de elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="a9db0-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



