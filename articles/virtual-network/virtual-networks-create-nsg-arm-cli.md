---
title: "aaaCreate de rede de grupos de segurança - Azure CLI 2.0 | Microsoft Docs"
description: "Saiba como toocreate e implementar grupos de segurança de rede utilizando Olá Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a>Criar grupos de segurança utilizando Olá Azure CLI 2.0 de rede

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá 

Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá: 

- [Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – nosso CLI para Olá clássica e resource Gestão modelos de implementação 
- [Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -nossa próxima geração CLI para o modelo de implementação da gestão de recursos de Olá (Este artigo)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

exemplo de Olá Azure CLI 2.0 os comandos seguintes esperam num ambiente simple já criado com base no cenário de Olá anterior. 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a>Criar Olá NSG para Olá `FrontEnd` sub-rede

toocreate um NSG denominado *NSG-front-end* com base no cenário de Olá anterior, siga os seguintes passos de Olá.

1. Se ainda não ainda, instalar e configurar mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) e inicie sessão com a conta do Azure tooan [início de sessão az](/cli/azure/#login). 

2. Criar um NSG utilizando Olá [az rede nsg criar](/cli/azure/network/nsg#create) comando. 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    Parâmetros:
   
   * `--resource-group`: Nome do grupo de recursos de olá onde Olá NSG é criado. Para o nosso cenário *TestRG*.
   * `--location`: Região do azure onde hello novo NSG é criado. Para o nosso cenário *westus*.
   * `--name`: Nome para Olá novo NSG. Para o nosso cenário *NSG-front-end*.

    Olá era esperado o resultado é bastante um bit de informações, incluindo uma lista de todas as regras de predefinidas Olá. Olá exemplo seguinte mostra regras de predefinidas Olá com um filtro de consulta JMESPATH Olá `table` formato de saída:

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   Saída:

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. Criar uma regra que permite acesso tooport 3389 (RDP) de Olá Internet com Olá [criar regras de nsg de rede az](/cli/azure/network/nsg/rule#create) comando.

    > [!NOTE]
    > Dependendo da shell de Olá estiver a utilizar, poderá ser necessário toomodify Olá `*` caráter nos argumentos Olá, depois, por isso, não como argumento de Olá tooexpand antes da execução.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    Resultado esperado:
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    Parâmetros:

    * `--resource-group testrg`: Olá toouse do grupo de recursos. Tenha em atenção que é sensível.
    * `--nsg-name NSG-FrontEnd`: Nome do NSG Olá no qual Olá regra é criada.
    * `--name rdp-rule`: O nome da nova regra de Olá.
    * `--access Allow`: Nível de acesso para a regra de Olá (negar ou permitir).
    * `--protocol Tcp`: O protocolo (Tcp, Udp ou *).
    * `--direction Inbound`: Direção da ligação de Olá (entrada ou saída).
    * `--priority 100`: Prioridade da regra de Olá.
    * `--source-address-prefix Internet`: Prefixo de endereço de origem CIDR ou utilizar etiquetas predefinidas.
    * `--source-port-range "*"`: Porta ou intervalo de portas de origem. Porta que abrir a ligação de Olá.
    * `--destination-address-prefix "*"`: Prefixo de endereço de destino CIDR ou utilizar etiquetas predefinidas.
    * `--destination-port-range 3389`: Porta de destino ou intervalo de portas. Porta que recebe o pedido de ligação de Olá.



4. Criar uma regra que permite acesso tooport 80 (HTTP) de Olá Internet **criar regras de nsg de rede az** comando.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    Putput esperado:
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. Vincular Olá NSG toohello **front-end** sub-rede com Olá [atualização de sub-rede da vnet de rede de az](/cli/azure/network/vnet/subnet#update) comando.
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    Resultado esperado:
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a>Criar Olá NSG para Olá `BackEnd` sub-rede
toocreate um NSG denominado *NSG-back-end* com base no cenário de Olá anterior, siga os seguintes passos de Olá.

1. Criar Olá `NSG-BackEnd` NSG com **az rede nsg criar**.
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    Como no passo 2, anterior, Olá era esperado o resultado é bastante grande, incluindo regras predefinidas.
   
2. Criar uma regra que permite acesso tooport 1433 (SQL) de Olá `FrontEnd` sub-rede com Olá **criar regras de nsg de rede az** comando.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    Resultado esperado:

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. Criar uma regra que nega o acesso através de Internet de toohello Olá **criar regras de nsg de rede az** comando.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    Putput esperado:
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. Vincular Olá NSG toohello `BackEnd` sub-rede utilizando Olá **az rede vnet sub-rede conjunto** comando.
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    Resultado esperado:
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
