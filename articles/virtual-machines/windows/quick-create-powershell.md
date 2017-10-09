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
# <a name="create-a-windows-virtual-machine-with-powershell"></a>Criar máquinas virtuais do Windows com o PowerShell

módulo do Azure PowerShell Olá é toocreate utilizado e gerir recursos do Azure da linha de comandos do PowerShell Olá ou em scripts. Este detalhes guia através do PowerShell toocreate e máquina virtual do Azure a executar o Windows Server 2016. Após a conclusão da implementação, vamos ligar toohello servidor e instale o IIS.  

Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

Este guia de introdução requer Olá Azure PowerShell versão do módulo 3,6 ou posterior. Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).

## <a name="log-in-tooazure"></a>Inicie sessão no tooAzure

Inicie sessão no tooyour subscrição do Azure com Olá `Login-AzureRmAccount` de comandos e siga Olá no ecrã de instruções.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Criar grupo de recursos

Crie um grupo de recursos do Azure com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Um grupo de recursos é um contentor lógico no qual os recursos do Azure são implementados e geridos. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>Criar recursos de rede

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Crie uma rede virtual, uma sub-rede e um endereço IP público. 
Estes recursos são utilizados tooprovide rede conectividade toohello máquina e ligá-lo toohello internet.

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Crie um grupo de segurança de rede e uma regra do grupo de segurança de rede. 
grupo de segurança de rede Olá protege máquinas virtuais de Olá através de regras de entrada e saídas. Neste caso, é criada uma regra de entrada para a porta 3389, que permite ligações de ambiente de trabalho remotas recebidas. Pretendemos também toocreate uma regra de entrada para a porta 80, que permite o tráfego web recebido.

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

### <a name="create-a-network-card-for-hello-virtual-machine"></a>Crie uma placa de rede para a máquina virtual de Olá. 
Criar uma placa de rede com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) para a máquina virtual de Olá. placa de rede Olá liga-se a sub-rede de tooa Olá máquinas virtuais, o grupo de segurança de rede e o endereço IP público.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Criar a máquina virtual

Criar uma configuração da máquina virtual. Esta configuração inclui definições de Olá que são utilizadas quando implementar a máquina virtual de Olá, tais como a configuração de imagem, tamanho e a autenticação de máquina virtual. Ao executar este passo, serão pedidas credenciais. os valores de Olá que introduzir são configurados como nome de utilizador de Olá e a palavra-passe para a máquina virtual de Olá.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Criar máquina virtual de Olá com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Ligue toovirtual máquina

Depois de concluída a implementação de Olá, crie uma ligação de ambiente de trabalho remota com a máquina virtual de Olá.

Olá utilize [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn Olá público endereço IP Olá máquinas de comandos. Tome nota deste endereço IP para que possa ligar tooit com a conectividade de web browser tootest num passo futura.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Toocreate uma sessão de ambiente de trabalho remoto com a máquina virtual de Olá de comando seguinte Olá de utilização. Substitua o endereço IP Olá Olá *publicIPAddress* da sua máquina virtual. Quando lhe for pedido, introduza as credenciais de Olá utilizadas ao criar a máquina virtual de Olá.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>Instalar o IIS através do PowerShell

Agora que iniciou sessão toohello VM do Azure, pode utilizar uma única linha de PowerShell tooinstall IIS e ativar o tráfego de web de tooallow de regra de local firewall de Olá. Abra uma linha de comandos do PowerShell e execute Olá os seguintes comandos:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Olá vista página de boas-vindas do IIS

Com a instalação do IIS e a porta 80 agora abra na VM a partir da Internet de Olá, pode utilizar um browser da sua choice tooview Olá predefinido IIS bem-vindo página. Ser se toouse Olá *publicIpAddress* documentados acima página do toovisit Olá predefinida. 

![Site predefinido do IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Limpar recursos

Quando já não é necessário, pode utilizar Olá [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) comando o grupo de recursos do tooremove Olá, VM e relacionados todos os recursos.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Passos seguintes

Neste guia de introdução, implementou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web. toolearn mais informações sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Windows.

> [!div class="nextstepaction"]
> [Tutoriais de máquinas virtuais do Windows do Azure](./tutorial-manage-vm.md)
