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
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="b5acd-103">Criar uma máquina virtual do Linux completa com Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b5acd-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="b5acd-104">tooquickly criar uma máquina virtual (VM) no Azure, pode utilizar um único comando da CLI do Azure que utiliza a predefinição valores toocreate qualquer necessário a recursos de suporte.</span><span class="sxs-lookup"><span data-stu-id="b5acd-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="b5acd-105">Recursos como uma rede virtual, o endereço IP público e regras de grupo de segurança de rede são criados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b5acd-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="b5acd-106">Para obter mais controlo do ambiente de produção utilizar, pode criar estes recursos antecedência e, em seguida, adicionar o toothem VMs.</span><span class="sxs-lookup"><span data-stu-id="b5acd-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="b5acd-107">Este artigo orienta-o como toocreate uma VM e cada um dos recursos de suporte um de cada Olá.</span><span class="sxs-lookup"><span data-stu-id="b5acd-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="b5acd-108">Certifique-se de que tem instalado Olá mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) e a conta com sessão iniciada tooan do Azure com [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b5acd-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b5acd-109">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="b5acd-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b5acd-110">Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myVnet*, e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="b5acd-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="b5acd-111">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b5acd-111">Create resource group</span></span>
<span data-ttu-id="b5acd-112">Um grupo de recursos do Azure é um contentor lógico no qual os recursos do Azure são implementados e geridos.</span><span class="sxs-lookup"><span data-stu-id="b5acd-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="b5acd-113">Um grupo de recursos tem de ser criado antes de uma máquina virtual e suporte recursos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b5acd-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="b5acd-114">Criar grupo de recursos de Olá com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b5acd-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b5acd-115">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="b5acd-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="b5acd-116">Por predefinição, o resultado de Olá dos comandos da CLI do Azure é no JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="b5acd-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="b5acd-117">lista de tooa de saída do toochange Olá predefinidos ou tabela, por exemplo, utilizar [az configurar - saída](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="b5acd-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="b5acd-118">Também pode adicionar `--output` tooany comando por um período de tempo de uma alteração no formato de saída.</span><span class="sxs-lookup"><span data-stu-id="b5acd-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="b5acd-119">Olá exemplo seguinte mostra Olá JSON uma saída da Olá `az group create` comando:</span><span class="sxs-lookup"><span data-stu-id="b5acd-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

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

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="b5acd-120">Criar uma rede virtual e sub-rede</span><span class="sxs-lookup"><span data-stu-id="b5acd-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="b5acd-121">Em seguida, criar uma rede virtual no Azure e uma sub-rede toowhich pode criar as suas VMs.</span><span class="sxs-lookup"><span data-stu-id="b5acd-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="b5acd-122">Utilize [az rede vnet criar](/cli/azure/network/vnet#create) toocreate uma rede virtual denominada *myVnet* com Olá *192.168.0.0/16* prefixo de endereço.</span><span class="sxs-lookup"><span data-stu-id="b5acd-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="b5acd-123">Adicionar uma sub-rede com o nome também *mySubnet* com o prefixo de endereço Olá de *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="b5acd-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="b5acd-124">saída de Olá mostra sub-rede Olá como logicamente criado no interior da rede virtual Olá:</span><span class="sxs-lookup"><span data-stu-id="b5acd-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

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


## <a name="create-a-public-ip-address"></a><span data-ttu-id="b5acd-125">Crie um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="b5acd-125">Create a public IP address</span></span>
<span data-ttu-id="b5acd-126">Agora vamos criar um endereço IP público com [az público-ip da rede criar](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="b5acd-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="b5acd-127">Este endereço IP público permite-lhe tooconnect tooyour VMs de Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="b5acd-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="b5acd-128">Porque o endereço predefinido de Olá for dinâmico, iremos também criar uma entrada DNS nomeada com Olá `--domain-name-label` opção.</span><span class="sxs-lookup"><span data-stu-id="b5acd-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="b5acd-129">Olá exemplo seguinte cria um IP público com o nome *myPublicIP* com o nome DNS Olá *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="b5acd-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="b5acd-130">Porque o nome DNS Olá têm de ser exclusivo, forneça o seu próprio nome DNS exclusivo:</span><span class="sxs-lookup"><span data-stu-id="b5acd-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="b5acd-131">Saída:</span><span class="sxs-lookup"><span data-stu-id="b5acd-131">Output:</span></span>

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


## <a name="create-a-network-security-group"></a><span data-ttu-id="b5acd-132">Criar um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="b5acd-132">Create a network security group</span></span>
<span data-ttu-id="b5acd-133">fluxo de Olá toocontrol de tráfego que entra e sai as suas VMs, criar um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="b5acd-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="b5acd-134">Um grupo de segurança de rede pode ser aplicado tooa NIC ou uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b5acd-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="b5acd-135">Olá exemplo seguinte utiliza [az rede nsg criar](/cli/azure/network/nsg#create) toocreate com o nome de um grupo de segurança de rede *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="b5acd-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="b5acd-136">Pode definir regras que permitem ou negam o tráfego específico Olá.</span><span class="sxs-lookup"><span data-stu-id="b5acd-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="b5acd-137">tooallow ligações de entrada na porta 22 (toosupport SSH), crie uma regra de entrada para o grupo de segurança de rede Olá com [criar regras de nsg de rede az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="b5acd-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="b5acd-138">Olá exemplo seguinte cria uma regra com o nome *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="b5acd-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

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

<span data-ttu-id="b5acd-139">tooallow ligações de entrada na porta 80 (tráfego de web de toosupport), adicione outra regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="b5acd-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="b5acd-140">Olá exemplo seguinte cria uma regra com o nome *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="b5acd-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

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

<span data-ttu-id="b5acd-141">Examine o grupo de segurança de rede de Olá e as regras com [mostrar de nsg de rede az](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="b5acd-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="b5acd-142">Saída:</span><span class="sxs-lookup"><span data-stu-id="b5acd-142">Output:</span></span>

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

## <a name="create-a-virtual-nic"></a><span data-ttu-id="b5acd-143">Criar uma NIC virtual</span><span class="sxs-lookup"><span data-stu-id="b5acd-143">Create a virtual NIC</span></span>
<span data-ttu-id="b5acd-144">Placas de interface de rede virtual (NICs) estão disponíveis através de programação porque pode aplicar regras tootheir utilização.</span><span class="sxs-lookup"><span data-stu-id="b5acd-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="b5acd-145">Também pode ter mais do que um.</span><span class="sxs-lookup"><span data-stu-id="b5acd-145">You can also have more than one.</span></span> <span data-ttu-id="b5acd-146">No seguinte Olá [nic da rede az criar](/cli/azure/network/nic#create) comando, crie um NIC com o nome *myNic* e associá-lo com o grupo de segurança de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="b5acd-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="b5acd-147">Olá, endereço IP público *myPublicIP* está também associado a NIC Olá virtual.</span><span class="sxs-lookup"><span data-stu-id="b5acd-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="b5acd-148">Saída:</span><span class="sxs-lookup"><span data-stu-id="b5acd-148">Output:</span></span>

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


## <a name="create-an-availability-set"></a><span data-ttu-id="b5acd-149">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b5acd-149">Create an availability set</span></span>
<span data-ttu-id="b5acd-150">Conjuntos de disponibilidade propagação de ajuda as suas VMs em domínios de falhas e domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="b5acd-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="b5acd-151">Embora apenas cria uma VM neste momento, é melhor prática toouse disponibilidade conjuntos toomake-lo mais fácil tooexpand no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="b5acd-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="b5acd-152">Domínios de falhas de definir um agrupamento de máquinas virtuais que partilham um comutador de rede de origem e de energia comum.</span><span class="sxs-lookup"><span data-stu-id="b5acd-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="b5acd-153">Por predefinição, Olá as máquinas virtuais que estão configuradas no seu conjunto de disponibilidade estão separadas em toothree domínios de falhas de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="b5acd-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="b5acd-154">Um problema de hardware num destes domínios de falhas não afeta cada VM que está a executar a aplicação.</span><span class="sxs-lookup"><span data-stu-id="b5acd-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="b5acd-155">Domínios de atualização indicam grupos de máquinas virtuais e o hardware físico subjacente que pode ser reiniciado no Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="b5acd-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="b5acd-156">Durante a manutenção planeada, ordem de Olá na qual atualização domínios são reiniciados poderá não ser sequencial, mas apenas uma atualização de domínio é reiniciado cada vez.</span><span class="sxs-lookup"><span data-stu-id="b5acd-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="b5acd-157">Azure distribui automaticamente VMs entre domínios de falhas e de atualização de Olá quando colocá-las num conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b5acd-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="b5acd-158">Para obter mais informações, consulte [gerir a disponibilidade de Olá de VMs](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="b5acd-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="b5acd-159">Criar um conjunto de disponibilidade para a VM com [az vm conjunto de disponibilidade criar](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="b5acd-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="b5acd-160">Olá exemplo seguinte cria um conjunto nomeado de disponibilidade *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="b5acd-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="b5acd-161">Olá domínios de falhas de notas de saída e domínios de atualização:</span><span class="sxs-lookup"><span data-stu-id="b5acd-161">hello output notes fault domains and update domains:</span></span>

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


## <a name="create-hello-linux-vms"></a><span data-ttu-id="b5acd-162">Criar as VMs Linux do Olá</span><span class="sxs-lookup"><span data-stu-id="b5acd-162">Create hello Linux VMs</span></span>
<span data-ttu-id="b5acd-163">Criou toosupport de recursos de rede Olá VMs acessível através da Internet.</span><span class="sxs-lookup"><span data-stu-id="b5acd-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="b5acd-164">Agora, crie uma VM e proteja-a com uma chave SSH.</span><span class="sxs-lookup"><span data-stu-id="b5acd-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="b5acd-165">Neste caso, vamos toocreate uma VM com Ubuntu com base no Olá LTS mais recente.</span><span class="sxs-lookup"><span data-stu-id="b5acd-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="b5acd-166">Pode encontrar imagens adicionais com [lista de imagens de vm az](/cli/azure/vm/image#list), conforme descrito nas [localizar as imagens de VM do Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="b5acd-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="b5acd-167">Podemos também especificar um toouse de chave SSH para a autenticação.</span><span class="sxs-lookup"><span data-stu-id="b5acd-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="b5acd-168">Se não tiver um par de chaves públicas SSH, pode [criá-los](mac-create-ssh-keys.md) ou utilize Olá `--generate-ssh-keys` parâmetro toocreate-las por si.</span><span class="sxs-lookup"><span data-stu-id="b5acd-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="b5acd-169">Se tiver já um par de chaves, este parâmetro utiliza chaves existentes no `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="b5acd-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="b5acd-170">Criar Olá VM ao colocar todos os nossos recursos e informações juntamente com Olá [az vm criar](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b5acd-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="b5acd-171">Olá exemplo seguinte cria uma VM chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="b5acd-171">hello following example creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="b5acd-172">SSH tooyour VM com Olá entrada DNS que forneceu quando criou o endereço IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="b5acd-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="b5acd-173">Isto `fqdn` é apresentado na saída de Olá para criar a VM:</span><span class="sxs-lookup"><span data-stu-id="b5acd-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

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

<span data-ttu-id="b5acd-174">Saída:</span><span class="sxs-lookup"><span data-stu-id="b5acd-174">Output:</span></span>

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

<span data-ttu-id="b5acd-175">Pode instalar NGINX e ver toohello de fluxo de tráfego de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b5acd-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="b5acd-176">Instale NGINX da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="b5acd-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="b5acd-177">site NGINX toosee Olá predefinido em ação, abra o browser e introduza o FQDN:</span><span class="sxs-lookup"><span data-stu-id="b5acd-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Site NGINX predefinido na VM](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="b5acd-179">Exportar como um modelo</span><span class="sxs-lookup"><span data-stu-id="b5acd-179">Export as a template</span></span>
<span data-ttu-id="b5acd-180">E se pretende agora toocreate um ambiente de desenvolvimento adicionais com Olá mesmos parâmetros ou um ambiente de produção que corresponda ao-lo?</span><span class="sxs-lookup"><span data-stu-id="b5acd-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="b5acd-181">Gestor de recursos utiliza os modelos JSON que definem a todos os parâmetros de Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="b5acd-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="b5acd-182">Criar os ambientes completos consultar este modelo JSON.</span><span class="sxs-lookup"><span data-stu-id="b5acd-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="b5acd-183">Pode [criar manualmente os modelos JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exportar um modelo JSON do Olá de toocreate ambiente existente para si.</span><span class="sxs-lookup"><span data-stu-id="b5acd-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="b5acd-184">Utilize [exportação de grupo az](/cli/azure/group#export) tooexport o recurso do grupo da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="b5acd-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="b5acd-185">Este comando cria Olá `myResourceGroup.json` ficheiros no seu diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="b5acd-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="b5acd-186">Quando criar um ambiente a partir deste modelo, lhe for pedido para todos os nomes de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5acd-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="b5acd-187">Pode preencher estes nomes no seu ficheiro de modelo adicionando Olá `--include-parameter-default-value` parâmetro toohello `az group export` comando.</span><span class="sxs-lookup"><span data-stu-id="b5acd-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="b5acd-188">Editar os nomes de recursos do JSON modelo toospecify hello, ou [criar um ficheiro Parameters. JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifica os nomes de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="b5acd-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="b5acd-189">toocreate um ambiente do seu modelo, utilize [criar a implementação do grupo az](/cli/azure/group/deployment#create) da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="b5acd-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="b5acd-190">É aconselhável tooread [mais informações sobre como toodeploy a partir de modelos](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5acd-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b5acd-191">Saiba mais sobre como utilizar o ficheiro de parâmetros de Olá tooincrementally ambientes de atualização e aceder modelos a partir de uma única localização de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b5acd-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5acd-192">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b5acd-192">Next steps</span></span>
<span data-ttu-id="b5acd-193">Agora está pronto toobegin trabalhar com vários componentes de rede e as VMs.</span><span class="sxs-lookup"><span data-stu-id="b5acd-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="b5acd-194">Pode utilizar este toobuild de ambiente de exemplo horizontalmente a aplicação através da utilização de componentes do núcleo Olá introduzidos aqui.</span><span class="sxs-lookup"><span data-stu-id="b5acd-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
