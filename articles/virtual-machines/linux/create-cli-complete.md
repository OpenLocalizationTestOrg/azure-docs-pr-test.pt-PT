---
title: "aaaCreate um ambiente de Linux com Olá Azure CLI 2.0 | Microsoft Docs"
description: "Crie armazenamento, uma VM com Linux, uma rede virtual e sub-rede, um balanceador de carga, uma NIC, um IP público e um grupo de segurança de rede, tudo a partir de Olá fundo cópias de segurança utilizando Olá Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a>Criar uma máquina virtual do Linux completa com Olá CLI do Azure
tooquickly criar uma máquina virtual (VM) no Azure, pode utilizar um único comando da CLI do Azure que utiliza a predefinição valores toocreate qualquer necessário a recursos de suporte. Recursos como uma rede virtual, o endereço IP público e regras de grupo de segurança de rede são criados automaticamente. Para obter mais controlo do ambiente de produção utilizar, pode criar estes recursos antecedência e, em seguida, adicionar o toothem VMs. Este artigo orienta-o como toocreate uma VM e cada um dos recursos de suporte um de cada Olá.

Certifique-se de que tem instalado Olá mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) e a conta com sessão iniciada tooan do Azure com [início de sessão az](/cli/azure/#login).

No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myVnet*, e *myVM*.

## <a name="create-resource-group"></a>Criar grupo de recursos
Um grupo de recursos do Azure é um contentor lógico no qual os recursos do Azure são implementados e geridos. Um grupo de recursos tem de ser criado antes de uma máquina virtual e suporte recursos de rede virtual. Criar grupo de recursos de Olá com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:

```azurecli
az group create --name myResourceGroup --location eastus
```

Por predefinição, o resultado de Olá dos comandos da CLI do Azure é no JSON (JavaScript Object Notation). lista de tooa de saída do toochange Olá predefinidos ou tabela, por exemplo, utilizar [az configurar - saída](/cli/azure/#configure). Também pode adicionar `--output` tooany comando por um período de tempo de uma alteração no formato de saída. Olá exemplo seguinte mostra Olá JSON uma saída da Olá `az group create` comando:

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a>Criar uma rede virtual e sub-rede
Em seguida, criar uma rede virtual no Azure e uma sub-rede toowhich pode criar as suas VMs. Utilize [az rede vnet criar](/cli/azure/network/vnet#create) toocreate uma rede virtual denominada *myVnet* com Olá *192.168.0.0/16* prefixo de endereço. Adicionar uma sub-rede com o nome também *mySubnet* com o prefixo de endereço Olá de *192.168.1.0/24*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

saída de Olá mostra sub-rede Olá como logicamente criado no interior da rede virtual Olá:

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a>Crie um endereço IP público
Agora vamos criar um endereço IP público com [az público-ip da rede criar](/cli/azure/network/public-ip#create). Este endereço IP público permite-lhe tooconnect tooyour VMs de Olá Internet. Porque o endereço predefinido de Olá for dinâmico, iremos também criar uma entrada DNS nomeada com Olá `--domain-name-label` opção. Olá exemplo seguinte cria um IP público com o nome *myPublicIP* com o nome DNS Olá *mypublicdns*. Porque o nome DNS Olá têm de ser exclusivo, forneça o seu próprio nome DNS exclusivo:

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

Saída:

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a>Criar um grupo de segurança de rede
fluxo de Olá toocontrol de tráfego que entra e sai as suas VMs, criar um grupo de segurança de rede. Um grupo de segurança de rede pode ser aplicado tooa NIC ou uma sub-rede. Olá exemplo seguinte utiliza [az rede nsg criar](/cli/azure/network/nsg#create) toocreate com o nome de um grupo de segurança de rede *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

Pode definir regras que permitem ou negam o tráfego específico Olá. tooallow ligações de entrada na porta 22 (toosupport SSH), crie uma regra de entrada para o grupo de segurança de rede Olá com [criar regras de nsg de rede az](/cli/azure/network/nsg/rule#create). Olá exemplo seguinte cria uma regra com o nome *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

tooallow ligações de entrada na porta 80 (tráfego de web de toosupport), adicione outra regra de grupo de segurança de rede. Olá exemplo seguinte cria uma regra com o nome *myNetworkSecurityGroupRuleHTTP*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

Examine o grupo de segurança de rede de Olá e as regras com [mostrar de nsg de rede az](/cli/azure/network/nsg#show):

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

Saída:

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a>Criar uma NIC virtual
Placas de interface de rede virtual (NICs) estão disponíveis através de programação porque pode aplicar regras tootheir utilização. Também pode ter mais do que um. No seguinte Olá [nic da rede az criar](/cli/azure/network/nic#create) comando, crie um NIC com o nome *myNic* e associá-lo com o grupo de segurança de rede Olá. Olá, endereço IP público *myPublicIP* está também associado a NIC Olá virtual.

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

Saída:

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a>Criar um conjunto de disponibilidade
Conjuntos de disponibilidade propagação de ajuda as suas VMs em domínios de falhas e domínios de atualização. Embora apenas cria uma VM neste momento, é melhor prática toouse disponibilidade conjuntos toomake-lo mais fácil tooexpand no Olá futura. 

Domínios de falhas de definir um agrupamento de máquinas virtuais que partilham um comutador de rede de origem e de energia comum. Por predefinição, Olá as máquinas virtuais que estão configuradas no seu conjunto de disponibilidade estão separadas em toothree domínios de falhas de cópia de segurança. Um problema de hardware num destes domínios de falhas não afeta cada VM que está a executar a aplicação.

Domínios de atualização indicam grupos de máquinas virtuais e o hardware físico subjacente que pode ser reiniciado no Olá mesmo tempo. Durante a manutenção planeada, ordem de Olá na qual atualização domínios são reiniciados poderá não ser sequencial, mas apenas uma atualização de domínio é reiniciado cada vez.

Azure distribui automaticamente VMs entre domínios de falhas e de atualização de Olá quando colocá-las num conjunto de disponibilidade. Para obter mais informações, consulte [gerir a disponibilidade de Olá de VMs](manage-availability.md).

Criar um conjunto de disponibilidade para a VM com [az vm conjunto de disponibilidade criar](/cli/azure/vm/availability-set#create). Olá exemplo seguinte cria um conjunto nomeado de disponibilidade *myAvailabilitySet*:

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

Olá domínios de falhas de notas de saída e domínios de atualização:

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a>Criar as VMs Linux do Olá
Criou toosupport de recursos de rede Olá VMs acessível através da Internet. Agora, crie uma VM e proteja-a com uma chave SSH. Neste caso, vamos toocreate uma VM com Ubuntu com base no Olá LTS mais recente. Pode encontrar imagens adicionais com [lista de imagens de vm az](/cli/azure/vm/image#list), conforme descrito nas [localizar as imagens de VM do Azure](cli-ps-findimage.md).

Podemos também especificar um toouse de chave SSH para a autenticação. Se não tiver um par de chaves públicas SSH, pode [criá-los](mac-create-ssh-keys.md) ou utilize Olá `--generate-ssh-keys` parâmetro toocreate-las por si. Se tiver já um par de chaves, este parâmetro utiliza chaves existentes no `~/.ssh`.

Criar Olá VM ao colocar todos os nossos recursos e informações juntamente com Olá [az vm criar](/cli/azure/vm#create) comando. Olá exemplo seguinte cria uma VM chamada *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM com Olá entrada DNS que forneceu quando criou o endereço IP público Olá. Isto `fqdn` é apresentado na saída de Olá para criar a VM:

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Saída:

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

Pode instalar NGINX e ver toohello de fluxo de tráfego de Olá VM. Instale NGINX da seguinte forma:

```bash
sudo apt-get install -y nginx
```

site NGINX toosee Olá predefinido em ação, abra o browser e introduza o FQDN:

![Site NGINX predefinido na VM](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a>Exportar como um modelo
E se pretende agora toocreate um ambiente de desenvolvimento adicionais com Olá mesmos parâmetros ou um ambiente de produção que corresponda ao-lo? Gestor de recursos utiliza os modelos JSON que definem a todos os parâmetros de Olá para o seu ambiente. Criar os ambientes completos consultar este modelo JSON. Pode [criar manualmente os modelos JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exportar um modelo JSON do Olá de toocreate ambiente existente para si. Utilize [exportação de grupo az](/cli/azure/group#export) tooexport o recurso do grupo da seguinte forma:

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

Este comando cria Olá `myResourceGroup.json` ficheiros no seu diretório de trabalho atual. Quando criar um ambiente a partir deste modelo, lhe for pedido para todos os nomes de recursos de Olá. Pode preencher estes nomes no seu ficheiro de modelo adicionando Olá `--include-parameter-default-value` parâmetro toohello `az group export` comando. Editar os nomes de recursos do JSON modelo toospecify hello, ou [criar um ficheiro Parameters. JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifica os nomes de recursos de Olá.

toocreate um ambiente do seu modelo, utilize [criar a implementação do grupo az](/cli/azure/group/deployment#create) da seguinte forma:

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

É aconselhável tooread [mais informações sobre como toodeploy a partir de modelos](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Saiba mais sobre como utilizar o ficheiro de parâmetros de Olá tooincrementally ambientes de atualização e aceder modelos a partir de uma única localização de armazenamento.

## <a name="next-steps"></a>Passos seguintes
Agora está pronto toobegin trabalhar com vários componentes de rede e as VMs. Pode utilizar este toobuild de ambiente de exemplo horizontalmente a aplicação através da utilização de componentes do núcleo Olá introduzidos aqui.
