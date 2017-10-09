---
title: "aaaAzure início rápido - criar Windows VM PowerShell | Microsoft Docs"
description: "Saiba rapidamente toocreate máquinas virtuais do Windows com o PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="5929a-103">Criar máquinas virtuais do Windows com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5929a-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="5929a-104">módulo do Azure PowerShell Olá é toocreate utilizado e gerir recursos do Azure da linha de comandos do PowerShell Olá ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="5929a-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="5929a-105">Este detalhes guia através do PowerShell toocreate e máquina virtual do Azure a executar o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5929a-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="5929a-106">Após a conclusão da implementação, vamos ligar toohello servidor e instale o IIS.</span><span class="sxs-lookup"><span data-stu-id="5929a-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="5929a-107">Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="5929a-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="5929a-108">Este guia de introdução requer Olá Azure PowerShell versão do módulo 3,6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5929a-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="5929a-109">Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="5929a-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="5929a-110">Se precisar de tooinstall ou atualização, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="5929a-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="5929a-111">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="5929a-111">Log in tooAzure</span></span>

<span data-ttu-id="5929a-112">Inicie sessão no tooyour subscrição do Azure com Olá `Login-AzureRmAccount` de comandos e siga Olá no ecrã de instruções.</span><span class="sxs-lookup"><span data-stu-id="5929a-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="5929a-113">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5929a-113">Create resource group</span></span>

<span data-ttu-id="5929a-114">Crie um grupo de recursos do Azure com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="5929a-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="5929a-115">Um grupo de recursos é um contentor lógico no qual os recursos do Azure são implementados e geridos.</span><span class="sxs-lookup"><span data-stu-id="5929a-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="5929a-116">Criar recursos de rede</span><span class="sxs-lookup"><span data-stu-id="5929a-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="5929a-117">Crie uma rede virtual, uma sub-rede e um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="5929a-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="5929a-118">Estes recursos são utilizados tooprovide rede conectividade toohello máquina e ligá-lo toohello internet.</span><span class="sxs-lookup"><span data-stu-id="5929a-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="5929a-119">Crie um grupo de segurança de rede e uma regra do grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5929a-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="5929a-120">grupo de segurança de rede Olá protege máquinas virtuais de Olá através de regras de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="5929a-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="5929a-121">Neste caso, é criada uma regra de entrada para a porta 3389, que permite ligações de ambiente de trabalho remotas recebidas.</span><span class="sxs-lookup"><span data-stu-id="5929a-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="5929a-122">Pretendemos também toocreate uma regra de entrada para a porta 80, que permite o tráfego web recebido.</span><span class="sxs-lookup"><span data-stu-id="5929a-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="5929a-123">Crie uma placa de rede para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5929a-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="5929a-124">Criar uma placa de rede com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5929a-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="5929a-125">placa de rede Olá liga-se a sub-rede de tooa Olá máquinas virtuais, o grupo de segurança de rede e o endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="5929a-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="5929a-126">Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5929a-126">Create virtual machine</span></span>

<span data-ttu-id="5929a-127">Criar uma configuração da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5929a-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="5929a-128">Esta configuração inclui definições de Olá que são utilizadas quando implementar a máquina virtual de Olá, tais como a configuração de imagem, tamanho e a autenticação de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5929a-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="5929a-129">Ao executar este passo, serão pedidas credenciais.</span><span class="sxs-lookup"><span data-stu-id="5929a-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="5929a-130">os valores de Olá que introduzir são configurados como nome de utilizador de Olá e a palavra-passe para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5929a-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="5929a-131">Criar máquina virtual de Olá com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="5929a-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="5929a-132">Ligue toovirtual máquina</span><span class="sxs-lookup"><span data-stu-id="5929a-132">Connect toovirtual machine</span></span>

<span data-ttu-id="5929a-133">Depois de concluída a implementação de Olá, crie uma ligação de ambiente de trabalho remota com a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5929a-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="5929a-134">Olá utilize [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn Olá público endereço IP Olá máquinas de comandos.</span><span class="sxs-lookup"><span data-stu-id="5929a-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="5929a-135">Tome nota deste endereço IP para que possa ligar tooit com a conectividade de web browser tootest num passo futura.</span><span class="sxs-lookup"><span data-stu-id="5929a-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="5929a-136">Toocreate uma sessão de ambiente de trabalho remoto com a máquina virtual de Olá de comando seguinte Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="5929a-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="5929a-137">Substitua o endereço IP Olá Olá *publicIPAddress* da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5929a-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="5929a-138">Quando lhe for pedido, introduza as credenciais de Olá utilizadas ao criar a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="5929a-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="5929a-139">Instalar o IIS através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="5929a-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="5929a-140">Agora que iniciou sessão toohello VM do Azure, pode utilizar uma única linha de PowerShell tooinstall IIS e ativar o tráfego de web de tooallow de regra de local firewall de Olá.</span><span class="sxs-lookup"><span data-stu-id="5929a-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="5929a-141">Abra uma linha de comandos do PowerShell e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5929a-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="5929a-142">Olá vista página de boas-vindas do IIS</span><span class="sxs-lookup"><span data-stu-id="5929a-142">View hello IIS welcome page</span></span>

<span data-ttu-id="5929a-143">Com a instalação do IIS e a porta 80 agora abra na VM a partir da Internet de Olá, pode utilizar um browser da sua choice tooview Olá predefinido IIS bem-vindo página.</span><span class="sxs-lookup"><span data-stu-id="5929a-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="5929a-144">Ser se toouse Olá *publicIpAddress* documentados acima página do toovisit Olá predefinida.</span><span class="sxs-lookup"><span data-stu-id="5929a-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Site predefinido do IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="5929a-146">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="5929a-146">Clean up resources</span></span>

<span data-ttu-id="5929a-147">Quando já não é necessário, pode utilizar Olá [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) comando o grupo de recursos do tooremove Olá, VM e relacionados todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="5929a-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="5929a-148">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5929a-148">Next steps</span></span>

<span data-ttu-id="5929a-149">Neste guia de introdução, implementou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="5929a-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="5929a-150">toolearn mais informações sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="5929a-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5929a-151">Tutoriais de máquinas virtuais do Windows do Azure</span><span class="sxs-lookup"><span data-stu-id="5929a-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
