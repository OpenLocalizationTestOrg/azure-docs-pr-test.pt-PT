---
title: "aaaHow tooload equilibrar máquinas virtuais do Windows no Azure | Microsoft Docs"
description: "Saiba como toouse Olá Azure carregar balanceador toocreate uma aplicação de elevada disponibilidade e segura entre três VMs do Windows"
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
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Como tooload equilibrar virtual machines Windows no Azure toocreate uma aplicação altamente disponível
Balanceamento de carga fornece um nível mais elevado de disponibilidade propagando-se os pedidos recebidos em várias máquinas virtuais. Neste tutorial, pode saber mais sobre Olá diferentes componentes do Balanceador de carga do Azure de Olá que distribui o tráfego de e para fornecem elevada disponibilidade. Saiba como:

> [!div class="checklist"]
> * Criar um balanceador de carga do Azure
> * Criar uma sonda de estado de funcionamento do Balanceador de carga
> * Criar regras de tráfego de Balanceador de carga
> * Utilizar Olá extensão de Script personalizado toocreate um site do IIS básico
> * Criar máquinas virtuais e anexe tooa Balanceador de carga
> * Ver um balanceador de carga em ação
> * Adicionar e remover as VMs a partir de um balanceador de carga

Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior. Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind. Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Descrição geral do Balanceador de carga do Azure
Um balanceador de carga do Azure é um balanceador de carga de camada 4 (TCP, UDP) que fornece elevada disponibilidade, distribuição de tráfego de entrada entre VMs em bom estado. Uma sonda de estado de funcionamento do Balanceador de carga monitoriza uma porta especificada em cada VM e distribui apenas tráfego tooan VM operacional.

É possível definir uma configuração de IP Front-end que contém um ou mais endereços IP públicos. Esta configuração de IP Front-end permite a sua toobe de aplicações e de Balanceador de carga acessível através de Olá Internet. 

As máquinas virtuais ligar tooa Balanceador de carga com o seu cartão de interface de rede virtual (NIC). toodistribute tráfego toohello VMs, um conjunto de endereços de back-end contém endereços IP Olá Olá virtual (NICs) ligado toohello de Balanceador de carga.

fluxo de Olá toocontrol de tráfego, é possível definir as regras de Balanceador de carga para portas específicas e protocolos que mapeiam tooyour VMs.


## <a name="create-azure-load-balancer"></a>Criar Balanceador de carga do Azure
Esta secção descreve em detalhe como pode criar e configurar cada componente Olá de Balanceador de carga. Antes de poder criar seu Balanceador de carga, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupLoadBalancer* no Olá *EastUS* localização:

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Crie um endereço IP público
tooaccess Olá, a aplicação na Internet, tem um endereço IP público Olá Balanceador de carga. Criar um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Olá exemplo seguinte cria um endereço IP público com o nome *myPublicIP* no Olá *myResourceGroupLoadBalancer* grupo de recursos:

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Criar um balanceador de carga
Criar um endereço IP de front-end com [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Olá exemplo seguinte cria um endereço IP de front-end com o nome *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Criar um conjunto de endereços de back-end com [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Olá exemplo seguinte cria um conjunto de endereços de back-end com o nome *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Agora, crie o Balanceador de carga Olá com [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). Olá exemplo seguinte cria um balanceador de carga com o nome *myLoadBalancer* utilizando Olá *myPublicIP* endereço:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Criar uma sonda do Estado de funcionamento
tooallow Olá balanceador toomonitor Olá estado da carga da sua aplicação, utilize uma sonda do Estado de funcionamento. sonda de estado de funcionamento de Olá dinamicamente adiciona ou remove as VMs da rotação de Balanceador de carga de Olá com base na respetiva verificações de toohealth de resposta. Por predefinição, uma VM é removida da distribuição de Balanceador de carga Olá após duas falhas consecutivas em intervalos de 15 segundo. Criar uma sonda do Estado de funcionamento com base num protocolo ou uma página de verificação do Estado de funcionamento específico para a sua aplicação. 

Olá seguinte exemplo cria uma sonda TCP. Também pode criar das sondas personalizadas do HTTP para obter mais detalhada do Estado de funcionamento verificações. Quando utilizar uma pesquisa HTTP personalizada, tem de criar página de verificação do Estado de funcionamento de Olá, tais como *healthcheck.aspx*. sonda de Olá tem de devolver um **HTTP 200 OK** resposta para o anfitrião Olá tookeep de Balanceador de carga de Olá no rotação.

toocreate uma sonda do Estado de funcionamento TCP, utilize [adicionar AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Olá exemplo seguinte cria uma sonda do Estado de funcionamento com o nome *myHealthProbe* que monitoriza a cada VM:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Atualizar o Balanceador de carga Olá com [conjunto AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Criar uma regra de Balanceador de carga
Uma regra de Balanceador de carga é toodefine utilizado como o tráfego é distribuído toohello VMs. Definir a configuração IP de front-end do Olá para tráfego de entrada Olá e Olá back-end conjunto tooreceive Olá tráfego IP, juntamente com a origem necessários Olá e porta de destino. toomake se de que apenas as VMs bom receberem tráfego, também define toouse de sonda de estado de funcionamento de Olá.

Criar uma regra de Balanceador de carga com [adicionar AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Olá exemplo seguinte cria uma regra de Balanceador de carga com o nome *myLoadBalancerRule* e equilibrar o tráfego na porta *80*:

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

Atualizar o Balanceador de carga Olá com [conjunto AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Configurar uma rede virtual
Antes de implementar algumas VMs e pode testar o seu balanceador, crie Olá suporte recursos de rede virtual. Para obter mais informações sobre as redes virtuais, consulte Olá [gerir redes virtuais do Azure](tutorial-virtual-network.md) tutorial.

### <a name="create-network-resources"></a>Criar recursos de rede
Criar uma rede virtual com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Olá exemplo seguinte cria uma rede virtual denominada *myVnet* com *mySubnet*:

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

Criar uma regra de grupo de segurança de rede com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), em seguida, crie um grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Adicionar sub-rede toohello grupo de segurança de rede de Olá com [conjunto AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) e, em seguida, atualize a rede virtual do Olá com [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

Olá exemplo seguinte cria uma regra de grupo de segurança de rede com o nome *myNetworkSecurityGroup* e aplica-demasiado*mySubnet*:

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

NICs virtuais são criados com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Olá exemplo seguinte cria três NICs virtuais. (Uma NIC virtual para cada VM criar para a aplicação no Olá seguindo os passos). Pode criar o NICs virtuais adicionais e VMs em qualquer altura e adicioná-los toohello Balanceador de carga:

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a>Criar máquinas virtuais
elevada disponibilidade da tooimprove Olá da sua aplicação, coloque as suas VMs num conjunto de disponibilidade.

Criar um conjunto de disponibilidade com [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Olá exemplo seguinte cria um conjunto nomeado de disponibilidade *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Definir um administrador do nome de utilizador e palavra-passe para as VMs de Olá com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Agora pode criar VMs Olá com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Olá seguinte exemplo cria três VMs:

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

Este demora alguns minutos toocreate e configurar todos os três VMs.

### <a name="install-iis-with-custom-script-extension"></a>Instalar o IIS com a extensão de Script personalizado
Um tutorial anterior em [como toocustomize máquina virtual do Windows](tutorial-automate-vm-deployment.md), aprendeu como tooautomate personalização de VM com Olá extensão de Script personalizado para Windows. Pode utilizar Olá mesmo abordar tooinstall e configurar o IIS nas suas VMs.

Utilize [conjunto AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Olá extensão de Script personalizado. Olá execuções de extensão `powershell Add-WindowsFeature Web-Server` tooinstall Olá servidor Web do IIS e, em seguida, Olá atualizações *Default.htm* página tooshow Olá nome do anfitrião do Olá VM:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a>Balanceador de carga de teste
Obter o endereço IP público de Olá do seu Balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Olá exemplo seguinte obtém o endereço IP Olá *myPublicIP* criado anteriormente:

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

Em seguida, pode introduzir o endereço IP público Olá no tooa browser. é apresentado o Web site de Olá, incluindo o nome de anfitrião de Olá do Olá VM Balanceador de carga que Olá distribuídas tooas de tráfego no seguinte exemplo de Olá:

![Web site do IIS em execução](./media/tutorial-load-balancer/running-iis-website.png)

Balanceador de carga de Olá toosee distribuir o tráfego entre todas as três VMs executar a sua aplicação, pode forçar atualizar o browser.


## <a name="add-and-remove-vms"></a>Adicionar e remover VMs
Poderá ser necessário tooperform manutenção no Olá as VMs com a sua aplicação, como a instalação de atualizações do SO. toodeal com maior tráfego tooyour aplicação, poderá ser necessário tooadd VMs adicionais. Esta secção mostra-lhe como tooremove ou adicionar uma VM do Balanceador de carga Olá.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Remover uma VM do Balanceador de carga Olá
Obter Olá placa de interface com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), em seguida, conjunto Olá *LoadBalancerBackendAddressPools* Olá de propriedade de virtual NIC demasiado*$null*. Por fim, atualize o NIC virtual. Olá:

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Balanceador de carga de Olá toosee distribuir o tráfego entre Olá restantes duas VMs executar a sua aplicação, pode forçar atualizar o browser. Pode agora efetuar manutenção num Olá VM, tais como instalar atualizações do SO ou efetuar um reinício VM.

### <a name="add-a-vm-toohello-load-balancer"></a>Adicionar um balanceador de carga de toohello VM
Após efetuar a manutenção VM, ou se precisar de capacidade de tooexpand, defina Olá *LoadBalancerBackendAddressPools* propriedade toohello NIC virtual Olá *BackendAddressPool* de [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Obter o Balanceador de carga Olá:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, criou um balanceador de carga e anexado VMs tooit. Aprendeu a:

> [!div class="checklist"]
> * Criar um balanceador de carga do Azure
> * Criar uma sonda de estado de funcionamento do Balanceador de carga
> * Criar regras de tráfego de Balanceador de carga
> * Utilizar Olá extensão de Script personalizado toocreate um site do IIS básico
> * Criar máquinas virtuais e anexe tooa Balanceador de carga
> * Ver um balanceador de carga em ação
> * Adicionar e remover as VMs a partir de um balanceador de carga

Avançar toohello toolearn de tutorial seguinte como toomanage redes de VM.

> [!div class="nextstepaction"]
> [Gerir VMs e redes virtuais](./tutorial-virtual-network.md)
