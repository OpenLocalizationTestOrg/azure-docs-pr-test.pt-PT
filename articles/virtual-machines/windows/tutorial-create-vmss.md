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
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>Criar um conjunto de dimensionamento de Máquina Virtual e implementar uma aplicação altamente disponível no Windows
Um conjunto de dimensionamento de máquina virtual permite-lhe toodeploy e gerir um conjunto de máquinas virtuais idênticas de dimensionamento automático. Pode dimensionar o número de Olá de VMs no conjunto de dimensionamento de Olá manualmente ou definir tooautoscale regras com base na utilização de CPU, a pedido de memória ou tráfego de rede. Neste tutorial, implementa um conjunto no Azure de dimensionamento de máquina virtual. Saiba como:

> [!div class="checklist"]
> * Utilizar Olá extensão de Script personalizado toodefine um tooscale de site do IIS
> * Criar um balanceador de carga para o conjunto de dimensionamento
> * Criar um conjunto de dimensionamento de máquina virtual
> * Aumentar ou diminuir o número de Olá de instâncias de um conjunto de dimensionamento
> * Criar regras de dimensionamento automático

Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior. Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind. Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).


## <a name="scale-set-overview"></a>Descrição geral do conjunto de dimensionamento
Conjuntos de dimensionamento utilizar conceitos semelhantes, aprendeu sobre tutorial anterior Olá demasiado[criar VMs de elevada](tutorial-availability-sets.md). VMs num conjunto de dimensionamento estão distribuídas por domínios de falhas e a atualização tal como VMs num conjunto de disponibilidade.

As VMs são criadas conforme necessário de um conjunto de dimensionamento. Definir dimensionamento automático regras toocontrol como e quando VMs são adicionadas ou removidas do conjunto de dimensionamento de Olá. Estas regras podem acionar com base nas métricas, tais como a carga de CPU, utilização de memória ou tráfego de rede.

Os conjuntos de dimensionamento suporte cópias de segurança too1, 000 VMs ao utilizar uma imagem de plataforma do Azure. Para cargas de trabalho com requisitos de personalização de VM ou instalação significativa, pode ser útil demasiado[criar uma imagem VM personalizada](tutorial-custom-images.md). Pode criar cópias de segurança too100 VMs na escala definido quando utilizar uma imagem personalizada.


## <a name="create-an-app-tooscale"></a>Criar uma aplicação tooscale
Antes de poder criar um conjunto de dimensionamento, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupAutomate* no Olá *EastUS* localização:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

Um tutorial anterior, aprendeu como demasiado[configuração de VM automatizar](tutorial-automate-vm-deployment.md) utilizando Olá a extensão de Script personalizado. Criar uma configuração de conjunto de dimensionamento, em seguida, aplicar um tooinstall de extensão de Script personalizado e configurar o IIS:

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

## <a name="create-scale-load-balancer"></a>Criar Balanceador de carga de escala
Um balanceador de carga do Azure é um balanceador de carga de camada 4 (TCP, UDP) que fornece elevada disponibilidade, distribuição de tráfego de entrada entre VMs em bom estado. Uma sonda de estado de funcionamento do Balanceador de carga monitoriza uma porta especificada em cada VM e distribui apenas tráfego tooan VM operacional. Para obter mais informações, consulte o próximo tutorial de Olá no [como tooload equilibrar as máquinas virtuais do Windows](tutorial-load-balancer.md).

Crie um balanceador de carga que tenha um endereço IP público e distribui o tráfego da web na porta 80:

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

## <a name="create-a-scale-set"></a>Criar um conjunto de dimensionamento
Agora criar um conjunto com de dimensionamento de máquina virtual [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm). Olá exemplo seguinte cria um conjunto nomeado de dimensionamento *myScaleSet*:

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

Este demora alguns minutos toocreate e configurar todos os recursos de conjunto de dimensionamento de Olá e VMs.


## <a name="test-your-app"></a>Testar a aplicação
toosee o seu Web site do IIS em ação, obter o endereço IP público de Olá do seu Balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Olá exemplo seguinte obtém o endereço IP Olá *myPublicIP* criada como parte do conjunto de dimensionamento de Olá:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Introduza o endereço IP público Olá no tooa browser. aplicação de Olá é apresentada, incluindo o nome de anfitrião de Olá do Olá VM que Olá de carga do tráfego do Balanceador distribuída para:

![Site do IIS em execução](./media/tutorial-create-vmss/running-iis-site.png)

toosee Olá conjunto de dimensionamento em ação, pode forçar atualização a carga do web browser toosee Olá balanceador distribuir o tráfego entre todas as VMs de Olá executar a sua aplicação.


## <a name="management-tasks"></a>Tarefas de gestão
Ao longo do ciclo de vida de Olá de conjunto de dimensionamento de Olá, poderá ser necessário toorun uma ou mais tarefas de gestão. Além disso, poderá ser útil toocreate scripts que automatizem várias tarefas de ciclo de vida. O Azure PowerShell fornece uma forma rápida toodo essas tarefas. Seguem-se algumas tarefas comuns.

### <a name="view-vms-in-a-scale-set"></a>Vista VMs num conjunto de dimensionamento
definir uma lista de VMs em execução no seu dimensionamento de tooview, utilize [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) da seguinte forma:

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


### <a name="increase-or-decrease-vm-instances"></a>Aumentar ou diminuir instâncias de VM
toosee Olá diversas instâncias atualmente tem num conjunto de dimensionamento, utilize [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) e consultar no *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

Pode, em seguida, manualmente aumentar ou diminuir o número de Olá das máquinas virtuais em conjunto com de dimensionamento de Olá [atualização AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss). Olá exemplo a seguir define Olá número de VMs no seu dimensionamento definido demasiado*5*:

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

Se demora alguns Olá de tooupdate de minutos especificado o número de instâncias no seu conjunto de dimensionamento.


### <a name="configure-autoscale-rules"></a>Configurar regras de dimensionamento automático
Em vez de conjunto de dimensionamento manualmente o número de instâncias Olá no seu dimensionamento, pode definir regras de dimensionamento automático. Estas regras monitorizar Olá instâncias no seu dimensionamento definido e respondem em conformidade com base nas métricas e os limiares que define. Olá seguinte o exemplo aumenta horizontalmente de forma o número de instâncias Olá por um quando a carga de CPU média Olá é maior do que 60% durante um período de 5 minutos. Se a carga média da CPU de Olá, em seguida, descerem abaixo de 30% durante um período de 5 minutos, instâncias de Olá são ampliadas por uma instância:

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


## <a name="next-steps"></a>Passos seguintes
Neste tutorial, vai criar um conjunto de dimensionamento de máquina virtual. Aprendeu a:

> [!div class="checklist"]
> * Utilizar Olá extensão de Script personalizado toodefine um tooscale de site do IIS
> * Criar um balanceador de carga para o conjunto de dimensionamento
> * Criar um conjunto de dimensionamento de máquina virtual
> * Aumentar ou diminuir o número de Olá de instâncias de um conjunto de dimensionamento
> * Criar regras de dimensionamento automático

Produzir toolearn tutorial seguinte de toohello mais informações sobre conceitos para máquinas virtuais de balanceamento de carga.

> [!div class="nextstepaction"]
> [Máquinas virtuais de balanceamento de carga](tutorial-load-balancer.md)
