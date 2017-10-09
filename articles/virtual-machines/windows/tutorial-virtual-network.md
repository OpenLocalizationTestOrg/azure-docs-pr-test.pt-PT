---
title: "aaaAzure redes virtuais e máquinas virtuais do Windows | Microsoft Docs"
description: "Tutorial - Gerir redes virtuais do Azure e máquinas virtuais do Windows com o Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="0fc51-103">Gerir redes virtuais do Azure e máquinas virtuais do Windows com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fc51-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="0fc51-104">Máquinas virtuais do Azure utilizar redes do Azure para a comunicação de rede internos e externos.</span><span class="sxs-lookup"><span data-stu-id="0fc51-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="0fc51-105">Neste tutorial, pode criar várias máquinas virtuais (VMs) numa rede virtual e configurar a conectividade de rede entre eles.</span><span class="sxs-lookup"><span data-stu-id="0fc51-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="0fc51-106">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="0fc51-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0fc51-107">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="0fc51-107">Create a virtual network</span></span>
> * <span data-ttu-id="0fc51-108">Criar sub-redes da rede virtual</span><span class="sxs-lookup"><span data-stu-id="0fc51-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="0fc51-109">Controlar o tráfego de rede com grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="0fc51-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="0fc51-110">Ver as regras de tráfego em ação</span><span class="sxs-lookup"><span data-stu-id="0fc51-110">View traffic rules in action</span></span>

<span data-ttu-id="0fc51-111">Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0fc51-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="0fc51-112">Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="0fc51-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="0fc51-113">Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0fc51-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="0fc51-114">Criar VNet</span><span class="sxs-lookup"><span data-stu-id="0fc51-114">Create VNet</span></span>

<span data-ttu-id="0fc51-115">Uma VNet é uma representação da sua própria rede na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fc51-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="0fc51-116">Uma VNet é um isolamento lógico da Olá em nuvem do Azure dedicada tooyour subscrição.</span><span class="sxs-lookup"><span data-stu-id="0fc51-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="0fc51-117">Numa VNet, encontrará sub-redes, as regras para conectividade toothose sub-redes e ligações a partir de sub-redes de toohello Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="0fc51-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="0fc51-118">Antes de poder criar quaisquer outros recursos do Azure, terá de toocreate um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="0fc51-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="0fc51-119">Olá exemplo seguinte cria um grupo de recursos denominado *myRGNetwork* no Olá *EastUS* localização:</span><span class="sxs-lookup"><span data-stu-id="0fc51-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="0fc51-120">Uma sub-rede é um recurso de subordinados de uma VNet e ajuda a definir segmentos dos espaços de endereços dentro de um bloco CIDR utilizar prefixos de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="0fc51-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="0fc51-121">NICs podem ser adicionados toosubnets e tooVMs ligado, fornecer conectividade de várias cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0fc51-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="0fc51-122">Criar uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="0fc51-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="0fc51-123">Criar uma VNET com o nome *myVNet* utilizando *myFrontendSubnet* com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="0fc51-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="0fc51-124">Criar a VM front-end</span><span class="sxs-lookup"><span data-stu-id="0fc51-124">Create front-end VM</span></span>

<span data-ttu-id="0fc51-125">Para um toocommunicate VM numa VNet, necessita de uma interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="0fc51-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="0fc51-126">Olá *myFrontendVM* é acedido a partir de Olá internet, pelo que também necessita de um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="0fc51-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="0fc51-127">Criar um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="0fc51-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="0fc51-128">Crie um NIC com [novo AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="0fc51-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="0fc51-129">Definir Olá nome de utilizador e palavra-passe necessária para a conta de administrador Olá no Olá VM com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="0fc51-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="0fc51-130">Criar Olá VMs com [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [conjunto AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface adicionar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), e [novo-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="0fc51-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="0fc51-131">Instalar o servidor web</span><span class="sxs-lookup"><span data-stu-id="0fc51-131">Install web server</span></span>

<span data-ttu-id="0fc51-132">Pode instalar o IIS no *myFrontendVM* através da utilização de uma sessão de ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="0fc51-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="0fc51-133">Terá de tooget Olá público endereço IP Olá VM tooaccess-lo.</span><span class="sxs-lookup"><span data-stu-id="0fc51-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="0fc51-134">Pode obter o endereço IP público Olá do *myFrontendVM* com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="0fc51-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="0fc51-135">Olá exemplo seguinte obtém o endereço IP Olá *myPublicIPAddress* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="0fc51-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="0fc51-136">Tome nota deste endereço IP, pelo que pode utilizá-lo nos passos futuros.</span><span class="sxs-lookup"><span data-stu-id="0fc51-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="0fc51-137">Seguinte de Olá utilize comando toocreate uma sessão de ambiente de trabalho remoto com *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="0fc51-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="0fc51-138">Substitua  *<publicIPAddress>*  com endereço Olá que registou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0fc51-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="0fc51-139">Quando lhe for pedido, introduza as credenciais de Olá utilizadas quando criou Olá VM.</span><span class="sxs-lookup"><span data-stu-id="0fc51-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="0fc51-140">Agora que iniciou sessão demasiado*myFrontendVM*, pode utilizar uma única linha de PowerShell tooinstall IIS e ativar o tráfego de web de tooallow de regra de local firewall de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fc51-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="0fc51-141">Abra uma linha de comandos do PowerShell e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0fc51-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="0fc51-142">Utilize [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun Olá personalizado a extensão de script que instala o servidor Web do IIS de Olá:</span><span class="sxs-lookup"><span data-stu-id="0fc51-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="0fc51-143">Agora pode utilizar Olá IP endereço toobrowse toohello VM toosee Olá IIS site público.</span><span class="sxs-lookup"><span data-stu-id="0fc51-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![Site predefinido do IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="0fc51-145">Gerir o tráfego interno</span><span class="sxs-lookup"><span data-stu-id="0fc51-145">Manage internal traffic</span></span>

<span data-ttu-id="0fc51-146">Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam rede tráfego tooresources ligado tooa VNet.</span><span class="sxs-lookup"><span data-stu-id="0fc51-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="0fc51-147">Os NSGs podem ser associados toosubnets ou NICs individuais ligados tooVMs.</span><span class="sxs-lookup"><span data-stu-id="0fc51-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="0fc51-148">Abrir ou fechar tooVMs de acesso através de portas é feita através de regras de NSG.</span><span class="sxs-lookup"><span data-stu-id="0fc51-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="0fc51-149">Quando criou *myFrontendVM*, porta de entrada 3389 automaticamente foi aberta para conectividade RDP.</span><span class="sxs-lookup"><span data-stu-id="0fc51-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="0fc51-150">Comunicação interna de VMs pode ser configurada utilizando um NSG.</span><span class="sxs-lookup"><span data-stu-id="0fc51-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="0fc51-151">Nesta secção, saiba como toocreate uma sub-rede adicional no Olá de rede e atribuir uma ligação a partir de um tooallow de tooit NSG *myFrontendVM* demasiado*myBackendVM* na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="0fc51-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="0fc51-152">a sub-rede de Olá, em seguida, é atribuído toohello VM quando é criado.</span><span class="sxs-lookup"><span data-stu-id="0fc51-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="0fc51-153">Pode limitar o tráfego de interno demasiado*myBackendVM* de apenas *myFrontendVM* criando um NSG para sub-rede de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="0fc51-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="0fc51-154">Olá exemplo seguinte cria uma regra NSG designada *myBackendNSGRule* com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="0fc51-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="0fc51-155">Adicionar um grupo de segurança de rede com o nome *myBackendNSG* com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="0fc51-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="0fc51-156">Adicionar a sub-rede de back-end</span><span class="sxs-lookup"><span data-stu-id="0fc51-156">Add back-end subnet</span></span>

<span data-ttu-id="0fc51-157">Adicionar *myBackEndSubnet* demasiado*myVNet* com [adicionar AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="0fc51-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="0fc51-158">Criar a VM de back-end</span><span class="sxs-lookup"><span data-stu-id="0fc51-158">Create back-end VM</span></span>

<span data-ttu-id="0fc51-159">Olá toocreate da forma mais fácil do Olá VM de back-end é utilizar uma imagem do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0fc51-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="0fc51-160">Este tutorial só cria Olá VM com o servidor de base de dados de Olá, mas não fornece informações sobre como aceder à base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fc51-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="0fc51-161">Criar *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="0fc51-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="0fc51-162">Definir Olá nome de utilizador e palavra-passe necessária para a conta de administrador Olá no Olá VM com o Get-Credential:</span><span class="sxs-lookup"><span data-stu-id="0fc51-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="0fc51-163">Criar *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="0fc51-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="0fc51-164">imagem de Olá que é utilizada tem o SQL Server instalada, mas não é utilizada neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="0fc51-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="0fc51-165">É incluída tooshow, como pode configurar um tráfego de web de toohandle VM e um VM toohandle da base de dados de gestão.</span><span class="sxs-lookup"><span data-stu-id="0fc51-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fc51-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0fc51-166">Next steps</span></span>

<span data-ttu-id="0fc51-167">Neste tutorial, criou e redes do Azure como toovirtual relacionados máquinas protegidas.</span><span class="sxs-lookup"><span data-stu-id="0fc51-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="0fc51-168">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="0fc51-168">Create a virtual network</span></span>
> * <span data-ttu-id="0fc51-169">Criar sub-redes da rede virtual</span><span class="sxs-lookup"><span data-stu-id="0fc51-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="0fc51-170">Controlar o tráfego de rede com grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="0fc51-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="0fc51-171">Ver as regras de tráfego em ação</span><span class="sxs-lookup"><span data-stu-id="0fc51-171">View traffic rules in action</span></span>

<span data-ttu-id="0fc51-172">Produzir toohello seguinte toolearn tutorial sobre a monitorização de proteger dados em máquinas virtuais utilizando cópia de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc51-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="0fc51-173">.</span><span class="sxs-lookup"><span data-stu-id="0fc51-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0fc51-174">Cópia de segurança de máquinas virtuais do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="0fc51-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
