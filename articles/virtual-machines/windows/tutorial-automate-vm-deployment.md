---
title: aaaCustomize uma VM do Windows no Azure | Microsoft Docs
description: "Saiba como toouse Olá Cofre de chaves toocustomize VMs do Windows no Azure e a extensão de script personalizado"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="f1da8-103">Como toocustomize uma máquina virtual do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="f1da8-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="f1da8-104">Normalmente, se pretendido tooconfigure as máquinas virtuais (VMs) de uma forma rápida e consistente, alguma forma de automatização.</span><span class="sxs-lookup"><span data-stu-id="f1da8-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="f1da8-105">Um toocustomize abordagem comum uma VM do Windows é toouse [extensão de Script personalizado para Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="f1da8-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="f1da8-106">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="f1da8-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f1da8-107">Utilizar Olá extensão de Script personalizado tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="f1da8-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="f1da8-108">Criar uma VM que utiliza Olá extensão de Script personalizado</span><span class="sxs-lookup"><span data-stu-id="f1da8-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="f1da8-109">Ver um site do IIS em execução depois de aplicada a extensão de Olá</span><span class="sxs-lookup"><span data-stu-id="f1da8-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="f1da8-110">Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f1da8-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f1da8-111">Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="f1da8-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="f1da8-112">Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f1da8-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="f1da8-113">Descrição geral de extensão de script personalizado</span><span class="sxs-lookup"><span data-stu-id="f1da8-113">Custom script extension overview</span></span>
<span data-ttu-id="f1da8-114">Olá extensão de Script personalizado transfere e executa os scripts em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1da8-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="f1da8-115">Esta extensão é útil para configuração de implementação de post, instalação de software ou qualquer outra configuração / tarefas de gestão.</span><span class="sxs-lookup"><span data-stu-id="f1da8-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="f1da8-116">Scripts podem ser transferidos a partir do armazenamento do Azure ou do GitHub, ou fornecidos toohello do portal do Azure em tempo de execução de extensão.</span><span class="sxs-lookup"><span data-stu-id="f1da8-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="f1da8-117">Olá a extensão de Script personalizado se integra com modelos Azure Resource Manager e também pode ser executado utilizando Olá CLI do Azure, o PowerShell, o portal do Azure ou o Olá API de REST de Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1da8-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="f1da8-118">Pode utilizar Olá extensão de Script personalizado com o Windows e VMs com Linux.</span><span class="sxs-lookup"><span data-stu-id="f1da8-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="f1da8-119">Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f1da8-119">Create virtual machine</span></span>
<span data-ttu-id="f1da8-120">Antes de poder criar uma VM, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f1da8-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f1da8-121">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupAutomate* no Olá *EastUS* localização:</span><span class="sxs-lookup"><span data-stu-id="f1da8-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="f1da8-122">Definir um administrador do nome de utilizador e palavra-passe para as VMs de Olá com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="f1da8-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="f1da8-123">Agora pode criar Olá VM com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f1da8-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="f1da8-124">Olá exemplo seguinte cria componentes de rede virtual Olá necessário, configuração de Olá SO e, em seguida, cria uma VM chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="f1da8-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="f1da8-125">Demora alguns minutos para que os recursos de Olá e toobe VM criada.</span><span class="sxs-lookup"><span data-stu-id="f1da8-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="f1da8-126">Automatizar a instalação do IIS</span><span class="sxs-lookup"><span data-stu-id="f1da8-126">Automate IIS install</span></span>
<span data-ttu-id="f1da8-127">Utilize [conjunto AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Olá extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="f1da8-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="f1da8-128">Olá execuções de extensão `powershell Add-WindowsFeature Web-Server` tooinstall Olá servidor Web do IIS e, em seguida, Olá atualizações *Default.htm* página tooshow Olá nome do anfitrião do Olá VM:</span><span class="sxs-lookup"><span data-stu-id="f1da8-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="f1da8-129">Teste web site</span><span class="sxs-lookup"><span data-stu-id="f1da8-129">Test web site</span></span>
<span data-ttu-id="f1da8-130">Obter o endereço IP público de Olá do seu Balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="f1da8-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="f1da8-131">Olá exemplo seguinte obtém o endereço IP Olá *myPublicIP* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f1da8-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="f1da8-132">Em seguida, pode introduzir o endereço IP público Olá no tooa browser.</span><span class="sxs-lookup"><span data-stu-id="f1da8-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="f1da8-133">é apresentado o Web site de Olá, incluindo o nome de anfitrião de Olá do Olá VM Balanceador de carga que Olá distribuídas tooas de tráfego no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="f1da8-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Web site do IIS em execução](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="f1da8-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f1da8-135">Next steps</span></span>

<span data-ttu-id="f1da8-136">Neste tutorial, automatizada Olá IIS instalar numa VM.</span><span class="sxs-lookup"><span data-stu-id="f1da8-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="f1da8-137">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="f1da8-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f1da8-138">Utilizar Olá extensão de Script personalizado tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="f1da8-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="f1da8-139">Criar uma VM que utiliza Olá extensão de Script personalizado</span><span class="sxs-lookup"><span data-stu-id="f1da8-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="f1da8-140">Ver um site do IIS em execução depois de aplicada a extensão de Olá</span><span class="sxs-lookup"><span data-stu-id="f1da8-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="f1da8-141">Avançar toohello toolearn de tutorial seguinte como toocreate personalizadas imagens da VM.</span><span class="sxs-lookup"><span data-stu-id="f1da8-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1da8-142">Criar imagens de VM personalizadas</span><span class="sxs-lookup"><span data-stu-id="f1da8-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
