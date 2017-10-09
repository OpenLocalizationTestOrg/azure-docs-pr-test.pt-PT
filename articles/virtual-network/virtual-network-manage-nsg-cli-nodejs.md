---
title: "aaaManage de rede de grupos de segurança - CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como grupos de segurança de rede de toomanage utilizando Olá interface de linha de comandos do Azure (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a>Gerir grupos de segurança de rede com Olá CLI do Azure 1.0

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá 

Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá: 

- [Azure CLI 1.0](#View-existing-NSGs) – nosso CLI para Olá clássica e resource Gestão modelos de implementação 
- [Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -nossa próxima geração CLI para o modelo de implementação da gestão de recursos de Olá (Este artigo)

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez do modelo de implementação clássica Olá.
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a>Obter as informações
Pode ver os seus NSGs existentes, obter as regras para um NSG existente e descobrir os recursos que um NSG é associado a.

### <a name="view-existing-nsgs"></a>Ver os NSGs existentes
lista de Olá tooview de NSGs num grupo de recursos específico, execute Olá `azure network nsg list` comando conforme mostrado abaixo.

```azurecli
azure network nsg list --resource-group RG-NSG
```

Resultado esperado:

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a>Listar todas as regras para um NSG
regras de Olá tooview de um NSG denominado **NSG-front-end**, hello execute `azure network nsg show` comando conforme mostrado abaixo. 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

Resultado esperado:

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> Também pode utilizar `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` regras de Olá toolist dos Olá **NSG-front-end** NSG.
>

### <a name="view-nsg-associations"></a>Associações de NSG de vista

tooview que Olá recursos **NSG-front-end** NSG é associado ao, execute Olá `azure network nsg show` comando conforme mostrado abaixo. Tenha em atenção que Olá apenas diferença é a utilização de Olá de Olá **– json** parâmetro.

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

Procure Olá **nomes de networkInterfaces** e **sub-redes** propriedades conforme mostrado abaixo:

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

No exemplo de Olá acima, Olá NSG não está associado a tooany interfaces de rede (NICs) e é associado tooa sub-rede designada **front-end**.

## <a name="manage-rules"></a>Gerir as regras
Pode adicionar tooan regras existentes NSG, editar regras existentes e remova regras.

### <a name="add-a-rule"></a>Adicionar uma regra
tooadd uma regra que permite **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, introduza Olá os seguintes comandos:

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

Resultado esperado:

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a>Alterar uma regra
regra de Olá toochange criada acima tooallow de entrada do tráfego de Olá **Internet** apenas, execute hello os seguintes comandos:

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

Resultado esperado:

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a>Eliminar uma regra
regra de Olá toodelete criado acima, executar Olá os seguintes comandos:

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> Olá `--quiet` parâmetro garante que não precisa de eliminação de Olá tooconfirm.
>

Resultado esperado:

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a>Gerir as associações
Pode associar um NSG toosubnets e NICs. Também pode desassociar um NSG a partir de qualquer recurso que está associado.

### <a name="associate-an-nsg-tooa-nic"></a>Associar um NSG tooa NIC
Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, execute Olá os seguintes comandos:

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

Resultado esperado:

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a>Desassociar um NSG a partir de uma NIC

Olá toodissociate **NSG-front-end** NSG de Olá **TestNICWeb1** NIC, execute Olá os seguintes comandos:

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> Olá de aviso "" valor (vazio) para Olá `network-security-group-id` parâmetro. É como remover uma associação tooan NSG. Não é possível efetuar Olá mesmo com Olá `network-security-group-name` parâmetro.
> 

Resultado esperado:

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a>Desassociar um NSG de sub-rede
Olá toodissociate **NSG-front-end** NSG de Olá **front-end** sub-rede, execute Olá os seguintes comandos:

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

Resultado esperado:

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-tooa-subnet"></a>Associar uma sub-rede de tooa NSG
Olá tooassociate **NSG-front-end** NSG toohello **FronEnd** sub-rede novamente, execute Olá os seguintes comandos:

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> Olá comando acima só funciona porque Olá **NSG-front-end** NSG está em Olá mesmo grupo de recursos à rede virtual Olá **TestVNet**. Se Olá NSG está num grupo de recursos diferente, terá de toouse Olá `--network-security-group-id` parâmetro em vez disso e forneça o id completo de Olá para Olá NSG. Pode obter o id de Olá executando `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` e à procura de Olá **id** propriedade. 
> 

Resultado esperado:

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a>Eliminar um NSG
Só é possível eliminar um NSG se tooany recurso não está associado. toodelete um NSG, siga os passos de Olá abaixo.

1. recursos de Olá toocheck associados tooan NSG, execute Olá `azure network nsg show` conforme mostrado no [vista NSGs associações](#View-NSGs-associations).
2. Se Olá NSG é associado tooany NICs, execute Olá `azure network nic set` conforme mostrado no [desassociar um NSG a partir de uma NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC. 
3. Se Olá NSG é associado tooany sub-rede, execute Olá `azure network vnet subnet set` conforme mostrado no [desassociar um NSG de sub-rede](#Dissociate-an-NSG-from-a-subnet) para cada sub-rede.
4. toodelete Olá NSG, execute Olá os seguintes comandos:

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    Resultado esperado:

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a>Passos seguintes
* [Ativar o registo](virtual-network-nsg-manage-log.md) para NSGs.

