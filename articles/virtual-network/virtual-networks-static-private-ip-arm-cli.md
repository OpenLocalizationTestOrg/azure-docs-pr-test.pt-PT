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
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="d4e59-103">Configurar endereços IP privados para uma máquina virtual utilizando Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4e59-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="d4e59-104">Tarefas do CLI versões toocomplete Olá</span><span class="sxs-lookup"><span data-stu-id="d4e59-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="d4e59-105">Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:</span><span class="sxs-lookup"><span data-stu-id="d4e59-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="d4e59-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – nosso CLI para Olá clássica e resource Gestão modelos de implementação</span><span class="sxs-lookup"><span data-stu-id="d4e59-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="d4e59-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -nossa próxima geração CLI para o modelo de implementação da gestão de recursos de Olá (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="d4e59-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d4e59-108">Este artigo abrange o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="d4e59-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="d4e59-109">Também pode [gerir o endereço IP privado estático no modelo de implementação clássica Olá](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d4e59-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="d4e59-110">comandos de Azure CLI 2.0 de exemplo de Olá abaixo esperam num ambiente simple que já criado.</span><span class="sxs-lookup"><span data-stu-id="d4e59-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="d4e59-111">Se pretender que os comandos de Olá toorun como são apresentados neste documento, primeiro criar ambiente de teste de Olá descrito [criar uma vnet](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d4e59-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="d4e59-112">Especifique um endereço IP privado estático quando criar uma VM</span><span class="sxs-lookup"><span data-stu-id="d4e59-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="d4e59-113">toocreate uma VM chamada *DNS01* no Olá *front-end* sub-rede de uma VNet com o nome *TestVNet* com um IP privado estático de *192.168.1.101*, Siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="d4e59-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="d4e59-114">Se ainda não ainda, instalar e configurar mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) e inicie sessão com a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d4e59-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="d4e59-115">Criar um IP público para Olá VM com Olá [az público-ip da rede criar](/cli/azure/network/public-ip#create) comando.</span><span class="sxs-lookup"><span data-stu-id="d4e59-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="d4e59-116">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="d4e59-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d4e59-117">Pode pretende ou precisa toouse valores diferentes para os argumentos deste e os passos subsequentes, consoante o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="d4e59-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="d4e59-118">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="d4e59-118">Expected output:</span></span>
   
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

   * <span data-ttu-id="d4e59-119">`--resource-group`: Nome do grupo de recursos de Olá no qual toocreate Olá um IP público.</span><span class="sxs-lookup"><span data-stu-id="d4e59-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="d4e59-120">`--name`: Nome do IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="d4e59-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="d4e59-121">`--location`: Azure região na qual toocreate Olá um IP público.</span><span class="sxs-lookup"><span data-stu-id="d4e59-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="d4e59-122">Executar Olá [nic da rede az criar](/cli/azure/network/nic#create) comando toocreate um NIC com um IP privado estático.</span><span class="sxs-lookup"><span data-stu-id="d4e59-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="d4e59-123">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="d4e59-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="d4e59-124">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="d4e59-124">Expected output:</span></span>
   
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
    
    <span data-ttu-id="d4e59-125">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="d4e59-125">Parameters:</span></span>

    * <span data-ttu-id="d4e59-126">`--private-ip-address`: Endereço IP privado estático para Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="d4e59-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="d4e59-127">`--vnet-name`: O nome da VNet Olá no qual toocreate Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="d4e59-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="d4e59-128">`--subnet`: O nome da sub-rede Olá que Olá toocreate NIC.</span><span class="sxs-lookup"><span data-stu-id="d4e59-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="d4e59-129">Executar Olá [vm do azure crie](/cli/azure/vm/nic#create) Olá do comando toocreate VM com o IP público Olá e NIC criado acima.</span><span class="sxs-lookup"><span data-stu-id="d4e59-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="d4e59-130">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="d4e59-130">hello list shown after hello output explains hello parameters used.</span></span>
   
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

    <span data-ttu-id="d4e59-131">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="d4e59-131">Expected output:</span></span>
   
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
   
   <span data-ttu-id="d4e59-132">Os parâmetros que não sejam básico Olá [az vm criar](/cli/azure/vm#create) parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d4e59-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="d4e59-133">`--nics`: O nome do Olá de toowhich Olá NIC VM está ligado.</span><span class="sxs-lookup"><span data-stu-id="d4e59-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="d4e59-134">Obter privadas informações endereços IP estáticos para uma VM</span><span class="sxs-lookup"><span data-stu-id="d4e59-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="d4e59-135">tooview Olá endereço IP privado estático que criou, execute os seguintes comandos da CLI do Azure de Olá e observe valores Olá para *método de alocação de IP privado* e *endereço IP privado*:</span><span class="sxs-lookup"><span data-stu-id="d4e59-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="d4e59-136">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="d4e59-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="d4e59-137">toodisplay Olá informações específicas do IP de Olá NIC para essa VM, Olá consulta NIC especificamente:</span><span class="sxs-lookup"><span data-stu-id="d4e59-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="d4e59-138">o resultado da Olá é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="d4e59-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="d4e59-139">Remover um endereço IP privado estático de uma VM</span><span class="sxs-lookup"><span data-stu-id="d4e59-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="d4e59-140">Não é possível remover um endereço IP privado estático a partir de um NIC na CLI do Azure para implementações do resource manager.</span><span class="sxs-lookup"><span data-stu-id="d4e59-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="d4e59-141">Tem de:</span><span class="sxs-lookup"><span data-stu-id="d4e59-141">You must:</span></span>
- <span data-ttu-id="d4e59-142">Crie um novo NIC que utiliza um IP dinâmico</span><span class="sxs-lookup"><span data-stu-id="d4e59-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="d4e59-143">Definir Olá NIC Olá VM Olá recém-criado NIC.</span><span class="sxs-lookup"><span data-stu-id="d4e59-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="d4e59-144">toochange Olá NIC para Olá VM utilizada nos comandos Olá acima, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="d4e59-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="d4e59-145">Executar Olá **nic da rede do azure crie** comando toocreate um NIC de novo utilizando a atribuição de IP dinâmico com um novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="d4e59-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="d4e59-146">Tenha em atenção que, porque não foi especificado nenhum endereço IP, o método de alocação de Olá é **dinâmica**.</span><span class="sxs-lookup"><span data-stu-id="d4e59-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="d4e59-147">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="d4e59-147">Expected output:</span></span>

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

2. <span data-ttu-id="d4e59-148">Executar Olá **conjunto da vm do azure** Olá toochange do comando NIC utilizada pelo Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d4e59-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="d4e59-149">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="d4e59-149">Expected output:</span></span>
   
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
    > <span data-ttu-id="d4e59-150">Se Olá VM é suficientemente grande toohave mais do que um NIC, execute Olá **nic da rede do azure eliminar** comando NIC. antigo toodelete Olá</span><span class="sxs-lookup"><span data-stu-id="d4e59-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="d4e59-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d4e59-151">Next steps</span></span>
* <span data-ttu-id="d4e59-152">Saiba mais sobre [reservado de IP público](virtual-networks-reserved-public-ip.md) endereços.</span><span class="sxs-lookup"><span data-stu-id="d4e59-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d4e59-153">Saiba mais sobre [instância ao nível do IP público (ILPIP)](virtual-networks-instance-level-public-ip.md) endereços.</span><span class="sxs-lookup"><span data-stu-id="d4e59-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d4e59-154">Consulte Olá [as APIs REST do IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4e59-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

