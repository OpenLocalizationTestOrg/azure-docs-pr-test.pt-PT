---
title: "aaaCreate uma Máquina Virtual escala conjuntos para Windows no Azure | Microsoft Docs"
description: "Criar e implementar uma aplicação altamente disponível em VMs do Windows utilizando um conjunto de dimensionamento de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="94d6c-103">Criar um conjunto de dimensionamento de Máquina Virtual e implementar uma aplicação altamente disponível no Windows</span><span class="sxs-lookup"><span data-stu-id="94d6c-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="94d6c-104">Um conjunto de dimensionamento de máquina virtual permite-lhe toodeploy e gerir um conjunto de máquinas virtuais idênticas de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="94d6c-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="94d6c-105">Pode dimensionar o número de Olá de VMs no conjunto de dimensionamento de Olá manualmente ou definir tooautoscale regras com base na utilização de CPU, a pedido de memória ou tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="94d6c-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="94d6c-106">Neste tutorial, implementa um conjunto no Azure de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94d6c-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="94d6c-107">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="94d6c-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94d6c-108">Utilizar Olá extensão de Script personalizado toodefine um tooscale de site do IIS</span><span class="sxs-lookup"><span data-stu-id="94d6c-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="94d6c-109">Criar um balanceador de carga para o conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="94d6c-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="94d6c-110">Criar um conjunto de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="94d6c-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="94d6c-111">Aumentar ou diminuir o número de Olá de instâncias de um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="94d6c-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="94d6c-112">Criar regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="94d6c-112">Create autoscale rules</span></span>

<span data-ttu-id="94d6c-113">Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="94d6c-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="94d6c-114">Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="94d6c-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="94d6c-115">Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="94d6c-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="94d6c-116">Descrição geral do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="94d6c-116">Scale Set overview</span></span>
<span data-ttu-id="94d6c-117">Conjuntos de dimensionamento utilizar conceitos semelhantes, aprendeu sobre tutorial anterior Olá demasiado[criar VMs de elevada](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="94d6c-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="94d6c-118">VMs num conjunto de dimensionamento estão distribuídas por domínios de falhas e a atualização tal como VMs num conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="94d6c-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="94d6c-119">As VMs são criadas conforme necessário de um conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="94d6c-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="94d6c-120">Definir dimensionamento automático regras toocontrol como e quando VMs são adicionadas ou removidas do conjunto de dimensionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="94d6c-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="94d6c-121">Estas regras podem acionar com base nas métricas, tais como a carga de CPU, utilização de memória ou tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="94d6c-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="94d6c-122">Os conjuntos de dimensionamento suporte cópias de segurança too1, 000 VMs ao utilizar uma imagem de plataforma do Azure.</span><span class="sxs-lookup"><span data-stu-id="94d6c-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="94d6c-123">Para cargas de trabalho com requisitos de personalização de VM ou instalação significativa, pode ser útil demasiado[criar uma imagem VM personalizada](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="94d6c-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="94d6c-124">Pode criar cópias de segurança too100 VMs na escala definido quando utilizar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="94d6c-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="94d6c-125">Criar uma aplicação tooscale</span><span class="sxs-lookup"><span data-stu-id="94d6c-125">Create an app tooscale</span></span>
<span data-ttu-id="94d6c-126">Antes de poder criar um conjunto de dimensionamento, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="94d6c-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="94d6c-127">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupAutomate* no Olá *EastUS* localização:</span><span class="sxs-lookup"><span data-stu-id="94d6c-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="94d6c-128">Um tutorial anterior, aprendeu como demasiado[configuração de VM automatizar](tutorial-automate-vm-deployment.md) utilizando Olá a extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="94d6c-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="94d6c-129">Criar uma configuração de conjunto de dimensionamento, em seguida, aplicar um tooinstall de extensão de Script personalizado e configurar o IIS:</span><span class="sxs-lookup"><span data-stu-id="94d6c-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="94d6c-130">Criar Balanceador de carga de escala</span><span class="sxs-lookup"><span data-stu-id="94d6c-130">Create scale load balancer</span></span>
<span data-ttu-id="94d6c-131">Um balanceador de carga do Azure é um balanceador de carga de camada 4 (TCP, UDP) que fornece elevada disponibilidade, distribuição de tráfego de entrada entre VMs em bom estado.</span><span class="sxs-lookup"><span data-stu-id="94d6c-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="94d6c-132">Uma sonda de estado de funcionamento do Balanceador de carga monitoriza uma porta especificada em cada VM e distribui apenas tráfego tooan VM operacional.</span><span class="sxs-lookup"><span data-stu-id="94d6c-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="94d6c-133">Para obter mais informações, consulte o próximo tutorial de Olá no [como tooload equilibrar as máquinas virtuais do Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="94d6c-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="94d6c-134">Crie um balanceador de carga que tenha um endereço IP público e distribui o tráfego da web na porta 80:</span><span class="sxs-lookup"><span data-stu-id="94d6c-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="94d6c-135">Criar um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="94d6c-135">Create a scale set</span></span>
<span data-ttu-id="94d6c-136">Agora criar um conjunto com de dimensionamento de máquina virtual [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="94d6c-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="94d6c-137">Olá exemplo seguinte cria um conjunto nomeado de dimensionamento *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="94d6c-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="94d6c-138">Este demora alguns minutos toocreate e configurar todos os recursos de conjunto de dimensionamento de Olá e VMs.</span><span class="sxs-lookup"><span data-stu-id="94d6c-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="94d6c-139">Testar a aplicação</span><span class="sxs-lookup"><span data-stu-id="94d6c-139">Test your app</span></span>
<span data-ttu-id="94d6c-140">toosee o seu Web site do IIS em ação, obter o endereço IP público de Olá do seu Balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="94d6c-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="94d6c-141">Olá exemplo seguinte obtém o endereço IP Olá *myPublicIP* criada como parte do conjunto de dimensionamento de Olá:</span><span class="sxs-lookup"><span data-stu-id="94d6c-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="94d6c-142">Introduza o endereço IP público Olá no tooa browser.</span><span class="sxs-lookup"><span data-stu-id="94d6c-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="94d6c-143">aplicação de Olá é apresentada, incluindo o nome de anfitrião de Olá do Olá VM que Olá de carga do tráfego do Balanceador distribuída para:</span><span class="sxs-lookup"><span data-stu-id="94d6c-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Site do IIS em execução](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="94d6c-145">toosee Olá conjunto de dimensionamento em ação, pode forçar atualização a carga do web browser toosee Olá balanceador distribuir o tráfego entre todas as VMs de Olá executar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="94d6c-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="94d6c-146">Tarefas de gestão</span><span class="sxs-lookup"><span data-stu-id="94d6c-146">Management tasks</span></span>
<span data-ttu-id="94d6c-147">Ao longo do ciclo de vida de Olá de conjunto de dimensionamento de Olá, poderá ser necessário toorun uma ou mais tarefas de gestão.</span><span class="sxs-lookup"><span data-stu-id="94d6c-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="94d6c-148">Além disso, poderá ser útil toocreate scripts que automatizem várias tarefas de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="94d6c-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="94d6c-149">O Azure PowerShell fornece uma forma rápida toodo essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="94d6c-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="94d6c-150">Seguem-se algumas tarefas comuns.</span><span class="sxs-lookup"><span data-stu-id="94d6c-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="94d6c-151">Vista VMs num conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="94d6c-151">View VMs in a scale set</span></span>
<span data-ttu-id="94d6c-152">definir uma lista de VMs em execução no seu dimensionamento de tooview, utilize [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="94d6c-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="94d6c-153">Aumentar ou diminuir instâncias de VM</span><span class="sxs-lookup"><span data-stu-id="94d6c-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="94d6c-154">toosee Olá diversas instâncias atualmente tem num conjunto de dimensionamento, utilize [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) e consultar no *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="94d6c-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="94d6c-155">Pode, em seguida, manualmente aumentar ou diminuir o número de Olá das máquinas virtuais em conjunto com de dimensionamento de Olá [atualização AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="94d6c-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="94d6c-156">Olá exemplo a seguir define Olá número de VMs no seu dimensionamento definido demasiado*5*:</span><span class="sxs-lookup"><span data-stu-id="94d6c-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="94d6c-157">Se demora alguns Olá de tooupdate de minutos especificado o número de instâncias no seu conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="94d6c-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="94d6c-158">Configurar regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="94d6c-158">Configure autoscale rules</span></span>
<span data-ttu-id="94d6c-159">Em vez de conjunto de dimensionamento manualmente o número de instâncias Olá no seu dimensionamento, pode definir regras de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="94d6c-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="94d6c-160">Estas regras monitorizar Olá instâncias no seu dimensionamento definido e respondem em conformidade com base nas métricas e os limiares que define.</span><span class="sxs-lookup"><span data-stu-id="94d6c-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="94d6c-161">Olá seguinte o exemplo aumenta horizontalmente de forma o número de instâncias Olá por um quando a carga de CPU média Olá é maior do que 60% durante um período de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="94d6c-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="94d6c-162">Se a carga média da CPU de Olá, em seguida, descerem abaixo de 30% durante um período de 5 minutos, instâncias de Olá são ampliadas por uma instância:</span><span class="sxs-lookup"><span data-stu-id="94d6c-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="94d6c-163">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="94d6c-163">Next steps</span></span>
<span data-ttu-id="94d6c-164">Neste tutorial, vai criar um conjunto de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94d6c-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="94d6c-165">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="94d6c-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94d6c-166">Utilizar Olá extensão de Script personalizado toodefine um tooscale de site do IIS</span><span class="sxs-lookup"><span data-stu-id="94d6c-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="94d6c-167">Criar um balanceador de carga para o conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="94d6c-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="94d6c-168">Criar um conjunto de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="94d6c-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="94d6c-169">Aumentar ou diminuir o número de Olá de instâncias de um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="94d6c-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="94d6c-170">Criar regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="94d6c-170">Create autoscale rules</span></span>

<span data-ttu-id="94d6c-171">Produzir toolearn tutorial seguinte de toohello mais informações sobre conceitos para máquinas virtuais de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="94d6c-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94d6c-172">Máquinas virtuais de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="94d6c-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
