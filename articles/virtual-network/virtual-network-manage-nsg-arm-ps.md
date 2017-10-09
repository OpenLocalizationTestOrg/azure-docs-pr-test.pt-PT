---
title: "aaaManage de rede de grupos de segurança - Azure PowerShell | Microsoft Docs"
description: "Saiba como toomanage rede grupos de segurança através do PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a>Gerir grupos de segurança de rede com o PowerShell

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez do modelo de implementação clássica Olá.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a>Obter as informações
Pode ver os seus NSGs existentes, obter as regras para um NSG existente e descobrir os recursos que um NSG é associado a.

### <a name="view-existing-nsgs"></a>Ver os NSGs existentes
tooview todos os NSGs existentes numa subscrição, execute Olá `Get-AzureRmNetworkSecurityGroup` cmdlet.

Resultado esperado:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


lista de Olá tooview de NSGs num grupo de recursos específico, execute Olá `Get-AzureRmNetworkSecurityGroup` cmdlet.

Resultado esperado:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a>Listar todas as regras para um NSG
regras de Olá tooview de um NSG denominado **NSG-front-end**, introduza Olá os seguintes comandos:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

Resultado esperado:

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> Também pode utilizar `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` regras de predefinidas Olá toolist de Olá **NSG-front-end** NSG.
> 

### <a name="view-nsgs-associations"></a>Ver as associações de NSGs
tooview que Olá recursos **NSG-front-end** NSG é associado ao, hello executar seguinte comando:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

Procure Olá **nomes de NetworkInterfaces** e **sub-redes** propriedades conforme mostrado abaixo:

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

No exemplo anterior Olá, Olá NSG não está associado tooany interfaces de rede (NICs); é associado tooa sub-rede designada **front-end**.

## <a name="manage-rules"></a>Gerir as regras
Pode adicionar tooan regras existentes NSG, editar regras existentes e remova regras.

### <a name="add-a-rule"></a>Adicionar uma regra
tooadd uma regra que permite **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, Olá concluir os seguintes passos:

1. Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Execute Olá tooadd de comando a seguir um NSG de toohello de regra:

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. as alterações de Olá toosave efetuadas toohello NSG, execute Olá os seguintes comandos:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    Resultado esperado Mostrar apenas Olá regras de segurança:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a>Alterar uma regra
regra de Olá toochange criada acima tooallow de entrada do tráfego de Olá **Internet** apenas, siga os passos de Olá abaixo.

1. Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Execute Olá comando com as definições da regra nova Olá os seguintes:

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. as alterações de Olá toosave efetuadas toohello NSG, execute Olá os seguintes comandos:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Resultado esperado Mostrar apenas Olá regras de segurança:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a>Eliminar uma regra
1. Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Execute Olá seguintes regra do comando tooremove Olá de Olá NSG:

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. Guarde as alterações efetuadas de Olá toohello NSG, executando Olá os seguintes comandos:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    O resultado esperado Mostrar apenas Olá regras de segurança, tenha em atenção Olá **regra https** já não está listado:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a>Gerir as associações
Pode associar um NSG toosubnets e NICs. Também pode desassociar um NSG a partir de qualquer recurso que está associado.

### <a name="associate-an-nsg-tooa-nic"></a>Associar um NSG tooa NIC
Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, Olá concluir os seguintes passos:

1. Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Executar Olá seguir Olá do comando tooretrieve existente NIC e armazená-las numa variável:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. Conjunto Olá **NetworkSecurityGroup** propriedade Olá **NIC** valor variável toohello Olá **NSG** variável, introduzindo Olá os seguintes comandos:

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. as alterações de Olá toosave efetuadas toohello NIC, execute Olá os seguintes comandos:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Olá apenas do que mostra o resultado esperado **NetworkSecurityGroup** propriedade:
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a>Desassociar um NSG a partir de uma NIC
Olá toodissociate **NSG-front-end** NSG de Olá **TestNICWeb1** NIC, Olá concluir os seguintes passos:

1. Executar Olá seguir Olá do comando tooretrieve existente NIC e armazená-las numa variável:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. Conjunto Olá **NetworkSecurityGroup** propriedade Olá **NIC** variável demasiado**$null** executando Olá os seguintes comandos:

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. as alterações de Olá toosave efetuadas toohello NIC, execute Olá os seguintes comandos:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Olá apenas do que mostra o resultado esperado **NetworkSecurityGroup** propriedade:
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a>Desassociar um NSG de sub-rede
Olá toodissociate **NSG-front-end** NSG de Olá **front-end** sub-rede, Olá concluir os seguintes passos:

1. Executar Olá seguir Olá do comando tooretrieve existente VNet e armazená-las numa variável:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Execute hello os seguintes comandos tooretrieve Olá **front-end** sub-rede e armazená-las numa variável:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Conjunto Olá **NetworkSecurityGroup** propriedade Olá **sub-rede** variável demasiado**$null** introduzindo Olá os seguintes comandos:

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. as alterações de Olá toosave efetuadas toohello sub-rede, execute Olá os seguintes comandos:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    O resultado esperado que apresenta apenas as propriedades de Olá de Olá **front-end** sub-rede. Observe que não é uma propriedade para **NetworkSecurityGroup**:
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a>Associar uma sub-rede de tooa NSG
Olá tooassociate **NSG-front-end** NSG toohello **FronEnd** sub-rede novamente, Olá concluir os seguintes passos:

1. Executar Olá seguir Olá do comando tooretrieve existente VNet e armazená-las numa variável:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Execute hello os seguintes comandos tooretrieve Olá **front-end** sub-rede e armazená-las numa variável:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. Conjunto Olá **NetworkSecurityGroup** propriedade Olá **sub-rede** variável demasiado**$null** executando Olá os seguintes comandos:

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. as alterações de Olá toosave efetuadas toohello sub-rede, execute Olá os seguintes comandos:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Olá apenas do que mostra o resultado esperado **NetworkSecurityGroup** propriedade Olá **front-end** sub-rede:
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a>Eliminar um NSG
Só é possível eliminar um NSG se tooany recurso não está associado. toodelete um NSG, siga os passos de Olá abaixo.

1. recursos de Olá toocheck associados tooan NSG, execute Olá `azure network nsg show` conforme mostrado no [vista NSGs associações](#View-NSGs-associations).
2. Se Olá NSG é associado tooany NICs, execute Olá `azure network nic set` conforme mostrado no [desassociar um NSG a partir de uma NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC. 
3. Se Olá NSG é associado tooany sub-rede, execute Olá `azure network vnet subnet set` conforme mostrado no [desassociar um NSG de sub-rede](#Dissociate-an-NSG-from-a-subnet) para cada sub-rede.
4. toodelete Olá NSG, execute Olá os seguintes comandos:

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > Olá `-Force` parâmetro garante que não precisa de eliminação de Olá tooconfirm.
   > 

## <a name="next-steps"></a>Passos seguintes
* [Ativar o registo](virtual-network-nsg-manage-log.md) para NSGs.

