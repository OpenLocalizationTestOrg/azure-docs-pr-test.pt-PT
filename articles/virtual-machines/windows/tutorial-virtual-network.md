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
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Gerir redes virtuais do Azure e máquinas virtuais do Windows com o Azure PowerShell

Máquinas virtuais do Azure utilizar redes do Azure para a comunicação de rede internos e externos. Neste tutorial, pode criar várias máquinas virtuais (VMs) numa rede virtual e configurar a conectividade de rede entre eles. Saiba como:

> [!div class="checklist"]
> * Criar uma rede virtual
> * Criar sub-redes da rede virtual
> * Controlar o tráfego de rede com grupos de segurança de rede
> * Ver as regras de tráfego em ação

Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior. Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind. Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>Criar VNet

Uma VNet é uma representação da sua própria rede na nuvem de Olá. Uma VNet é um isolamento lógico da Olá em nuvem do Azure dedicada tooyour subscrição. Numa VNet, encontrará sub-redes, as regras para conectividade toothose sub-redes e ligações a partir de sub-redes de toohello Olá VMs.

Antes de poder criar quaisquer outros recursos do Azure, terá de toocreate um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá exemplo seguinte cria um grupo de recursos denominado *myRGNetwork* no Olá *EastUS* localização:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Uma sub-rede é um recurso de subordinados de uma VNet e ajuda a definir segmentos dos espaços de endereços dentro de um bloco CIDR utilizar prefixos de endereços IP. NICs podem ser adicionados toosubnets e tooVMs ligado, fornecer conectividade de várias cargas de trabalho.

Criar uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

Criar uma VNET com o nome *myVNet* utilizando *myFrontendSubnet* com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>Criar a VM front-end

Para um toocommunicate VM numa VNet, necessita de uma interface de rede virtual (NIC). Olá *myFrontendVM* é acedido a partir de Olá internet, pelo que também necessita de um endereço IP público. 

Criar um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

Crie um NIC com [novo AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Definir Olá nome de utilizador e palavra-passe necessária para a conta de administrador Olá no Olá VM com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Criar Olá VMs com [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [conjunto AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface adicionar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), e [novo-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). 

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

## <a name="install-web-server"></a>Instalar o servidor web

Pode instalar o IIS no *myFrontendVM* através da utilização de uma sessão de ambiente de trabalho remoto. Terá de tooget Olá público endereço IP Olá VM tooaccess-lo.

Pode obter o endereço IP público Olá do *myFrontendVM* com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Olá exemplo seguinte obtém o endereço IP Olá *myPublicIPAddress* criado anteriormente:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Tome nota deste endereço IP, pelo que pode utilizá-lo nos passos futuros.

Seguinte de Olá utilize comando toocreate uma sessão de ambiente de trabalho remoto com *myFrontendVM*. Substitua  *<publicIPAddress>*  com endereço Olá que registou anteriormente. Quando lhe for pedido, introduza as credenciais de Olá utilizadas quando criou Olá VM.

```
mstsc /v:<publicIpAddress>
``` 

Agora que iniciou sessão demasiado*myFrontendVM*, pode utilizar uma única linha de PowerShell tooinstall IIS e ativar o tráfego de web de tooallow de regra de local firewall de Olá. Abra uma linha de comandos do PowerShell e execute Olá os seguintes comandos:

Utilize [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun Olá personalizado a extensão de script que instala o servidor Web do IIS de Olá:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Agora pode utilizar Olá IP endereço toobrowse toohello VM toosee Olá IIS site público.

![Site predefinido do IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>Gerir o tráfego interno

Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam rede tráfego tooresources ligado tooa VNet. Os NSGs podem ser associados toosubnets ou NICs individuais ligados tooVMs. Abrir ou fechar tooVMs de acesso através de portas é feita através de regras de NSG. Quando criou *myFrontendVM*, porta de entrada 3389 automaticamente foi aberta para conectividade RDP.

Comunicação interna de VMs pode ser configurada utilizando um NSG. Nesta secção, saiba como toocreate uma sub-rede adicional no Olá de rede e atribuir uma ligação a partir de um tooallow de tooit NSG *myFrontendVM* demasiado*myBackendVM* na porta 1433. a sub-rede de Olá, em seguida, é atribuído toohello VM quando é criado.

Pode limitar o tráfego de interno demasiado*myBackendVM* de apenas *myFrontendVM* criando um NSG para sub-rede de back-end Olá. Olá exemplo seguinte cria uma regra NSG designada *myBackendNSGRule* com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

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

Adicionar um grupo de segurança de rede com o nome *myBackendNSG* com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>Adicionar a sub-rede de back-end

Adicionar *myBackEndSubnet* demasiado*myVNet* com [adicionar AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

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

## <a name="create-back-end-vm"></a>Criar a VM de back-end

Olá toocreate da forma mais fácil do Olá VM de back-end é utilizar uma imagem do SQL Server. Este tutorial só cria Olá VM com o servidor de base de dados de Olá, mas não fornece informações sobre como aceder à base de dados de Olá.

Criar *myBackendNic*:

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Definir Olá nome de utilizador e palavra-passe necessária para a conta de administrador Olá no Olá VM com o Get-Credential:

```powershell
$cred = Get-Credential
```

Criar *myBackendVM*:

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

imagem de Olá que é utilizada tem o SQL Server instalada, mas não é utilizada neste tutorial. É incluída tooshow, como pode configurar um tráfego de web de toohandle VM e um VM toohandle da base de dados de gestão.

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, criou e redes do Azure como toovirtual relacionados máquinas protegidas. 

> [!div class="checklist"]
> * Criar uma rede virtual
> * Criar sub-redes da rede virtual
> * Controlar o tráfego de rede com grupos de segurança de rede
> * Ver as regras de tráfego em ação

Produzir toohello seguinte toolearn tutorial sobre a monitorização de proteger dados em máquinas virtuais utilizando cópia de segurança do Azure. .

> [!div class="nextstepaction"]
> [Cópia de segurança de máquinas virtuais do Windows no Azure](./tutorial-backup-vms.md)
