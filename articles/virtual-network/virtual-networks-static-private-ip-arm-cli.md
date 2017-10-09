---
title: "endereços IP privados aaaConfigure para VMs - Azure CLI 2.0 | Microsoft Docs"
description: "Saiba como endereços IP privados tooconfigure para máquinas virtuais utilizando Olá interface de linha de comandos do Azure (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a>Configurar endereços IP privados para uma máquina virtual utilizando Olá Azure CLI 2.0

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá 

Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá: 

- [Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – nosso CLI para Olá clássica e resource Gestão modelos de implementação 
- [Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -nossa próxima geração CLI para o modelo de implementação da gestão de recursos de Olá (Este artigo)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo abrange o modelo de implementação do Resource Manager Olá. Também pode [gerir o endereço IP privado estático no modelo de implementação clássica Olá](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> comandos de Azure CLI 2.0 de exemplo de Olá abaixo esperam num ambiente simple que já criado. Se pretender que os comandos de Olá toorun como são apresentados neste documento, primeiro criar ambiente de teste de Olá descrito [criar uma vnet](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Especifique um endereço IP privado estático quando criar uma VM

toocreate uma VM chamada *DNS01* no Olá *front-end* sub-rede de uma VNet com o nome *TestVNet* com um IP privado estático de *192.168.1.101*, Siga os passos de Olá abaixo:

1. Se ainda não ainda, instalar e configurar mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) e inicie sessão com a conta do Azure tooan [início de sessão az](/cli/azure/#login). 

2. Criar um IP público para Olá VM com Olá [az público-ip da rede criar](/cli/azure/network/public-ip#create) comando. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.

    > [!NOTE]
    > Pode pretende ou precisa toouse valores diferentes para os argumentos deste e os passos subsequentes, consoante o seu ambiente.
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    Resultado esperado:
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * `--resource-group`: Nome do grupo de recursos de Olá no qual toocreate Olá um IP público.
   * `--name`: Nome do IP público Olá.
   * `--location`: Azure região na qual toocreate Olá um IP público.

3. Executar Olá [nic da rede az criar](/cli/azure/network/nic#create) comando toocreate um NIC com um IP privado estático. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados. 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    Resultado esperado:
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    Parâmetros:

    * `--private-ip-address`: Endereço IP privado estático para Olá NIC.
    * `--vnet-name`: O nome da VNet Olá no qual toocreate Olá NIC.
    * `--subnet`: O nome da sub-rede Olá que Olá toocreate NIC.

4. Executar Olá [vm do azure crie](/cli/azure/vm/nic#create) Olá do comando toocreate VM com o IP público Olá e NIC criado acima. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    Resultado esperado:
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   Os parâmetros que não sejam básico Olá [az vm criar](/cli/azure/vm#create) parâmetros.

   * `--nics`: O nome do Olá de toowhich Olá NIC VM está ligado.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Obter privadas informações endereços IP estáticos para uma VM

tooview Olá endereço IP privado estático que criou, execute os seguintes comandos da CLI do Azure de Olá e observe valores Olá para *método de alocação de IP privado* e *endereço IP privado*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Resultado esperado:

```json
"192.168.1.101"
```

toodisplay Olá informações específicas do IP de Olá NIC para essa VM, Olá consulta NIC especificamente:

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

o resultado da Olá é semelhante ao seguinte:

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a>Remover um endereço IP privado estático de uma VM

Não é possível remover um endereço IP privado estático a partir de um NIC na CLI do Azure para implementações do resource manager. Tem de:
- Crie um novo NIC que utiliza um IP dinâmico
- Definir Olá NIC Olá VM Olá recém-criado NIC. 

toochange Olá NIC para Olá VM utilizada nos comandos Olá acima, siga os passos de Olá abaixo.

1. Executar Olá **nic da rede do azure crie** comando toocreate um NIC de novo utilizando a atribuição de IP dinâmico com um novo endereço IP. Tenha em atenção que, porque não foi especificado nenhum endereço IP, o método de alocação de Olá é **dinâmica**.

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    Resultado esperado:

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. Executar Olá **conjunto da vm do azure** Olá toochange do comando NIC utilizada pelo Olá VM.
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    Resultado esperado:
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > Se Olá VM é suficientemente grande toohave mais do que um NIC, execute Olá **nic da rede do azure eliminar** comando NIC. antigo toodelete Olá
   
## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [reservado de IP público](virtual-networks-reserved-public-ip.md) endereços.
* Saiba mais sobre [instância ao nível do IP público (ILPIP)](virtual-networks-instance-level-public-ip.md) endereços.
* Consulte Olá [as APIs REST do IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).

