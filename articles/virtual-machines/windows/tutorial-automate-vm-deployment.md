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
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a>Como toocustomize uma máquina virtual do Windows no Azure
Normalmente, se pretendido tooconfigure as máquinas virtuais (VMs) de uma forma rápida e consistente, alguma forma de automatização. Um toocustomize abordagem comum uma VM do Windows é toouse [extensão de Script personalizado para Windows](extensions-customscript.md). Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Utilizar Olá extensão de Script personalizado tooinstall IIS
> * Criar uma VM que utiliza Olá extensão de Script personalizado
> * Ver um site do IIS em execução depois de aplicada a extensão de Olá

Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior. Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind. Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).


## <a name="custom-script-extension-overview"></a>Descrição geral de extensão de script personalizado
Olá extensão de Script personalizado transfere e executa os scripts em VMs do Azure. Esta extensão é útil para configuração de implementação de post, instalação de software ou qualquer outra configuração / tarefas de gestão. Scripts podem ser transferidos a partir do armazenamento do Azure ou do GitHub, ou fornecidos toohello do portal do Azure em tempo de execução de extensão.

Olá a extensão de Script personalizado se integra com modelos Azure Resource Manager e também pode ser executado utilizando Olá CLI do Azure, o PowerShell, o portal do Azure ou o Olá API de REST de Máquina Virtual do Azure.

Pode utilizar Olá extensão de Script personalizado com o Windows e VMs com Linux.


## <a name="create-virtual-machine"></a>Criar a máquina virtual
Antes de poder criar uma VM, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupAutomate* no Olá *EastUS* localização:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

Definir um administrador do nome de utilizador e palavra-passe para as VMs de Olá com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Agora pode criar Olá VM com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Olá exemplo seguinte cria componentes de rede virtual Olá necessário, configuração de Olá SO e, em seguida, cria uma VM chamada *myVM*:

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

Demora alguns minutos para que os recursos de Olá e toobe VM criada.


## <a name="automate-iis-install"></a>Automatizar a instalação do IIS
Utilize [conjunto AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Olá extensão de Script personalizado. Olá execuções de extensão `powershell Add-WindowsFeature Web-Server` tooinstall Olá servidor Web do IIS e, em seguida, Olá atualizações *Default.htm* página tooshow Olá nome do anfitrião do Olá VM:

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


## <a name="test-web-site"></a>Teste web site
Obter o endereço IP público de Olá do seu Balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Olá exemplo seguinte obtém o endereço IP Olá *myPublicIP* criado anteriormente:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

Em seguida, pode introduzir o endereço IP público Olá no tooa browser. é apresentado o Web site de Olá, incluindo o nome de anfitrião de Olá do Olá VM Balanceador de carga que Olá distribuídas tooas de tráfego no seguinte exemplo de Olá:

![Web site do IIS em execução](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a>Passos seguintes

Neste tutorial, automatizada Olá IIS instalar numa VM. Aprendeu a:

> [!div class="checklist"]
> * Utilizar Olá extensão de Script personalizado tooinstall IIS
> * Criar uma VM que utiliza Olá extensão de Script personalizado
> * Ver um site do IIS em execução depois de aplicada a extensão de Olá

Avançar toohello toolearn de tutorial seguinte como toocreate personalizadas imagens da VM.

> [!div class="nextstepaction"]
> [Criar imagens de VM personalizadas](./tutorial-custom-images.md)
