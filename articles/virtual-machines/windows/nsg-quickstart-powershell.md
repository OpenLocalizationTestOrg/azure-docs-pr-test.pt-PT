---
title: aaaOpen portas tooa VM com o Azure PowerShell | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto final tooyour VM do Windows utilizando o modo de implementação do Olá do Azure resource manager e o Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a>Como tooopen portas e os pontos finais tooa VM no Azure utilizando o PowerShell
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Comandos rápidos
Grupo de segurança de rede toocreate e precisa de regras de ACL [versão mais recente do Olá do Azure PowerShell instalada](/powershell/azureps-cmdlets-docs). Também pode [executar estes passos, utilizando o portal do Azure de Olá](nsg-quickstart-portal.md).

Inicie sessão no tooyour conta do Azure:

```powershell
Login-AzureRmAccount
```

No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes de parâmetros de exemplo incluídos *myResourceGroup*, *myNetworkSecurityGroup*, e *myVnet*.

Criar uma regra com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Olá exemplo seguinte cria uma regra com o nome *myNetworkSecurityGroupRule* tooallow *tcp* tráfego na porta *80*:

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

Em seguida, crie o grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) e atribuir Olá HTTP regra que acabou de criar da seguinte forma. Olá exemplo seguinte cria um grupo de segurança de rede com o nome *myNetworkSecurityGroup*:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

Agora vamos atribuir a sub-rede de tooa do grupo de segurança de rede. Olá seguinte exemplo atribui uma rede virtual existente denominada *myVnet* toohello variável *$vnet* com [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

Associar o seu grupo de segurança de rede com a sub-rede com [conjunto AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig). Olá exemplo seguinte associa sub-rede Olá designada *mySubnet* com o grupo de segurança de rede:

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

Por fim, atualize a rede virtual com [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) por ordem para o efeito de tootake alterações:

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a>Obter mais informações sobre grupos de segurança de rede
comandos rápidos Olá aqui permitem-lhe tooget cópias de segurança e em execução com tooyour de fluxo de tráfego VM. Grupos de segurança de rede fornecem várias funcionalidades excelentes e granularidade para controlar aceder a recursos tooyour. Pode ler mais sobre [criar um grupo de segurança de rede e a ACL regras aqui](tutorial-virtual-network.md#manage-internal-traffic).

Para aplicações web de elevada disponibilidade, deve colocar as VMs por trás de um balanceador de carga do Azure. Balanceador de carga Olá distribui o tráfego tooVMs, com um grupo de segurança de rede que fornece a filtragem de tráfego. Para obter mais informações, consulte [como balancear tooload Linux virtual máquinas na toocreate do Azure, uma aplicação altamente disponível](tutorial-load-balancer.md).

## <a name="next-steps"></a>Passos seguintes
Neste exemplo, criou um tráfego de tooallow HTTP regra simples. Pode encontrar informações sobre como criar ambientes mais detalhados no Olá seguintes artigos:

* [Descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [O que é um Grupo de Segurança de Rede (NSG)? (What is a Network Security Group (NSG)?)](../../virtual-network/virtual-networks-nsg.md)
* [Descrição geral do Gestor de recursos do Azure para balanceadores de carga](../../load-balancer/load-balancer-arm.md)

