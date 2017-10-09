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
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="10177-103">Como toocreate uma VM não gerida imagem de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="10177-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="10177-104">Este artigo abrange a utilização de contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="10177-104">This article covers using storage accounts.</span></span> <span data-ttu-id="10177-105">Recomendamos que utilize discos geridos e imagens geridas em vez de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="10177-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="10177-106">Para obter mais informações, consulte [capturar uma imagem gerida de uma VM no Azure generalizada](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="10177-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="10177-107">Este artigo mostra como toouse Azure PowerShell toocreate uma imagem de uma VM do Azure generalizado através de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="10177-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="10177-108">Em seguida, pode utilizar Olá imagem toocreate outra VM.</span><span class="sxs-lookup"><span data-stu-id="10177-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="10177-109">imagem de Olá inclui o disco do SO Olá e discos de dados de Olá destinadas a máquina virtual de toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="10177-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="10177-110">imagem de Olá não inclui recursos de rede virtual Olá, por isso terá de tooset esses recursos quando criar Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="10177-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="10177-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="10177-111">Prerequisites</span></span>
<span data-ttu-id="10177-112">Terá de toohave Azure PowerShell versão 1.0.x ou mais recente instalada.</span><span class="sxs-lookup"><span data-stu-id="10177-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="10177-113">Se já não tiver instalado o PowerShell, leia [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter os passos de instalação.</span><span class="sxs-lookup"><span data-stu-id="10177-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="10177-114">Generalizar Olá VM</span><span class="sxs-lookup"><span data-stu-id="10177-114">Generalize hello VM</span></span> 
<span data-ttu-id="10177-115">Esta secção mostra-lhe como toogeneralize a máquina virtual do Windows para utilização como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="10177-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="10177-116">Generalizar uma VM remove todas as informações pessoais da conta, entre outras coisas e prepara Olá máquina toobe utilizado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="10177-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="10177-117">Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="10177-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="10177-118">Certifique-se em execução na máquina de Olá funções de servidor de Olá são suportadas pelo Sysprep.</span><span class="sxs-lookup"><span data-stu-id="10177-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="10177-119">Para obter mais informações, consulte [suporte de Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="10177-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10177-120">Se estiver a carregar o tooAzure VHD para Olá pela primeira vez, certifique-se de que tem [preparado VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="10177-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="10177-121">Também pode generalizar uma VM com Linux utilizando `sudo waagent -deprovision+user` e, em seguida, utilizar o PowerShell toocapture Olá VM.</span><span class="sxs-lookup"><span data-stu-id="10177-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="10177-122">Para obter informações sobre como utilizar a CLI de Olá toocapture uma VM, consulte [como toogeneralize e capturar uma máquina virtual do Linux utilizando Olá CLI do Azure ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="10177-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="10177-123">Inicie sessão no toohello máquina virtual do Windows.</span><span class="sxs-lookup"><span data-stu-id="10177-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="10177-124">Abra a janela de linha de comandos de Olá como administrador.</span><span class="sxs-lookup"><span data-stu-id="10177-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="10177-125">Altere o diretório de Olá demasiado**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="10177-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="10177-126">No Olá **ferramenta de preparação de sistema** caixa de diálogo, selecione **introduza sistema Out-of-Box experiência (OOBE)**e certifique-se de que Olá **Generalize** caixa de verificação está selecionada.</span><span class="sxs-lookup"><span data-stu-id="10177-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="10177-127">No **as opções de encerramento**, selecione **encerramento**.</span><span class="sxs-lookup"><span data-stu-id="10177-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="10177-128">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="10177-128">Click **OK**.</span></span>
   
    ![Iniciar o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="10177-130">Quando tiver concluído o Sysprep, encerra Olá máquina.</span><span class="sxs-lookup"><span data-stu-id="10177-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="10177-131">Não reinicie Olá VM até que sejam efectuada tooAzure VHD Olá carregar ou criar uma imagem de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="10177-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="10177-132">Se, acidentalmente, Olá VM obtém reiniciada, execute o Sysprep toogeneralize-a novamente.</span><span class="sxs-lookup"><span data-stu-id="10177-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="10177-133">Inicie sessão no tooAzure PowerShell</span><span class="sxs-lookup"><span data-stu-id="10177-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="10177-134">Abra o Azure PowerShell e inicie sessão tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="10177-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="10177-135">Abre uma janela de pop-up para tooenter as credenciais da conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="10177-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="10177-136">Obter IDs de subscrição de Olá para as subscrições disponíveis.</span><span class="sxs-lookup"><span data-stu-id="10177-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="10177-137">Definir a subscrição correta Olá com o ID de subscrição. Olá</span><span class="sxs-lookup"><span data-stu-id="10177-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="10177-138">Desalocar Olá VM e defina Olá Estado toogeneralized</span><span class="sxs-lookup"><span data-stu-id="10177-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="10177-139">Anular a atribuição de recursos da VM Olá.</span><span class="sxs-lookup"><span data-stu-id="10177-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="10177-140">Olá *estado* para Olá VM na Olá Azure portal é alterado de **parado** demasiado**parado (desalocado)**.</span><span class="sxs-lookup"><span data-stu-id="10177-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="10177-141">Definir o estado de Olá da máquina virtual de Olá demasiado**generalizado**.</span><span class="sxs-lookup"><span data-stu-id="10177-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="10177-142">Verifique o estado de Olá de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="10177-142">Check hello status of hello VM.</span></span> <span data-ttu-id="10177-143">Olá **OSState/generalizado** secção para Olá VM deve ter Olá **DisplayStatus** definido demasiado**VM generalizado**.</span><span class="sxs-lookup"><span data-stu-id="10177-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="10177-144">Criar imagem Olá</span><span class="sxs-lookup"><span data-stu-id="10177-144">Create hello image</span></span>

<span data-ttu-id="10177-145">Crie uma imagem de máquinas de virtuais não geridos no contentor de armazenamento de destino de Olá utilizando este comando.</span><span class="sxs-lookup"><span data-stu-id="10177-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="10177-146">Olá imagem é criada na Olá mesma conta de armazenamento como Olá máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="10177-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="10177-147">Olá `-Path` parâmetro guarda uma cópia do modelo JSON Olá Olá origem VM tooyour do computador local.</span><span class="sxs-lookup"><span data-stu-id="10177-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="10177-148">Olá `-DestinationContainerName` parâmetro é o nome de Olá do contentor de Olá que pretende toohold as imagens.</span><span class="sxs-lookup"><span data-stu-id="10177-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="10177-149">Se não existir contentor Olá, é criado para si.</span><span class="sxs-lookup"><span data-stu-id="10177-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="10177-150">Pode obter Olá URL da imagem de modelo de ficheiro Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="10177-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="10177-151">Aceda toohello **recursos** > **storageProfile** > **osDisk** > **imagem**  >  **uri** secção para o caminho completo do Olá da imagem.</span><span class="sxs-lookup"><span data-stu-id="10177-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="10177-152">aspeto Olá URL da imagem de Olá: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="10177-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="10177-153">Também pode verificar Olá URI no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="10177-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="10177-154">imagem de Olá é copiado tooa contentor com o nome **sistema** na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="10177-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="10177-155">Criar uma VM a partir da imagem de Olá</span><span class="sxs-lookup"><span data-stu-id="10177-155">Create a VM from hello image</span></span>

<span data-ttu-id="10177-156">Agora, pode criar uma ou mais VMs da imagem não gerido Olá.</span><span class="sxs-lookup"><span data-stu-id="10177-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="10177-157">Definir Olá URI de Olá VHD</span><span class="sxs-lookup"><span data-stu-id="10177-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="10177-158">Olá URI para Olá VHD toouse está num formato de Olá: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**. vhd.</span><span class="sxs-lookup"><span data-stu-id="10177-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="10177-159">Neste exemplo Olá VHD denominado **myVHD** na conta de armazenamento Olá **mystorageaccount** no contentor de Olá **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="10177-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="10177-160">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="10177-160">Create a virtual network</span></span>
<span data-ttu-id="10177-161">Criar vNet Olá e sub-rede de Olá [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10177-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="10177-162">Crie Olá sub-rede.</span><span class="sxs-lookup"><span data-stu-id="10177-162">Create hello subnet.</span></span> <span data-ttu-id="10177-163">Olá exemplo seguinte cria uma sub-rede designada **mySubnet** no grupo de recursos de Olá **myResourceGroup** com o prefixo de endereço Olá de **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="10177-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="10177-164">Crie rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="10177-164">Create hello virtual network.</span></span> <span data-ttu-id="10177-165">Olá exemplo seguinte cria uma rede virtual denominada **myVnet** no Olá **EUA oeste** localização com o prefixo de endereço Olá de **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="10177-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="10177-166">Criar uma interface de rede e o endereço IP pública</span><span class="sxs-lookup"><span data-stu-id="10177-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="10177-167">tooenable comunicação com a máquina virtual de Olá na rede virtual Olá, precisa de um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="10177-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="10177-168">Crie um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="10177-168">Create a public IP address.</span></span> <span data-ttu-id="10177-169">Este exemplo cria um endereço IP público com o nome **myPip**.</span><span class="sxs-lookup"><span data-stu-id="10177-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="10177-170">Criar Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="10177-170">Create hello NIC.</span></span> <span data-ttu-id="10177-171">Este exemplo cria um NIC com o nome **myNic**.</span><span class="sxs-lookup"><span data-stu-id="10177-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="10177-172">Criar grupo de segurança de rede Olá e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="10177-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="10177-173">toobe toolog consegue no tooyour VM através de RDP, terá de toohave uma regra de segurança que permite o acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="10177-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="10177-174">Este exemplo cria um NSG denominado **myNsg** que contenha uma regra denominada **myRdpRule** que permite tráfego RDP de através da porta 3389.</span><span class="sxs-lookup"><span data-stu-id="10177-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="10177-175">Para obter mais informações sobre NSGs, consulte [abrir portas tooa VM no Azure utilizando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10177-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="10177-176">Criar uma variável para a rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="10177-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="10177-177">Crie uma variável para a rede virtual Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="10177-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="10177-178">Criar Olá VM</span><span class="sxs-lookup"><span data-stu-id="10177-178">Create hello VM</span></span>
<span data-ttu-id="10177-179">Olá PowerShell seguintes realiza configurações de máquina virtual de Olá e utiliza a imagem não gerida como origem de Olá para a instalação do novo Olá.</span><span class="sxs-lookup"><span data-stu-id="10177-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

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

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="10177-180">Certifique-se de que Olá que VM foi criada</span><span class="sxs-lookup"><span data-stu-id="10177-180">Verify that hello VM was created</span></span>
<span data-ttu-id="10177-181">Quando terminar, deverá ver Olá recém-criado VM na Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou utilizando o seguinte Olá Comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="10177-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="10177-182">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="10177-182">Next steps</span></span>
<span data-ttu-id="10177-183">toomanage a nova máquina virtual com o Azure PowerShell, consulte [gerir máquinas virtuais utilizando o Azure Resource Manager e o PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10177-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


