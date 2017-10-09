---
title: "aaaCreate uma VM com um endereço IP público estático - CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como toocreate uma VM com um estático público endereço IP com Olá interface de linha de comandos do Azure (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3ee906b65735830757b455df00f9f8d4373be3dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-10"></a><span data-ttu-id="d8ac7-103">Criar uma VM com um endereço IP público estático utilizando Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d8ac7-103">Create a VM with a static public IP address using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8ac7-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d8ac7-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="d8ac7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8ac7-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="d8ac7-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="d8ac7-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="d8ac7-107">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d8ac7-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="d8ac7-108">Modelo</span><span class="sxs-lookup"><span data-stu-id="d8ac7-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="d8ac7-109">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="d8ac7-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d8ac7-110">O Azure tem dois modelos de implementação para criar e trabalhar com recursos: [Resource Manager e Clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d8ac7-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d8ac7-111">Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez do modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

<span data-ttu-id="d8ac7-112">Pode concluir esta tarefa utilizando Olá 1.0 CLI do Azure (Este artigo) ou Olá [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d8ac7-112">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> 

## <span data-ttu-id="d8ac7-113"><a name = "create"></a>Passo 1 – iniciar o script</span><span class="sxs-lookup"><span data-stu-id="d8ac7-113"><a name = "create"></a>Step 1 - Start your script</span></span>
<span data-ttu-id="d8ac7-114">Pode transferir o script de deteção completa Olá utilizado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="d8ac7-114">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-cli.sh).</span></span> <span data-ttu-id="d8ac7-115">Olá concluir os seguintes passos toochange Olá script toowork no seu ambiente:</span><span class="sxs-lookup"><span data-stu-id="d8ac7-115">Complete hello following steps toochange hello script toowork in your environment:</span></span>

<span data-ttu-id="d8ac7-116">Alterar Olá valores das variáveis de Olá abaixo com base nos valores de Olá pretende toouse para a sua implementação.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-116">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="d8ac7-117">Olá seguir o cenário de toohello de mapa de valores utilizado neste artigo:</span><span class="sxs-lookup"><span data-stu-id="d8ac7-117">hello following values map toohello scenario used in this article:</span></span>

```azurecli
# Set variables for hello new resource group
rgName="IaaSStory"
location="westus"

# Set variables for VNet
vnetName="TestVNet"
vnetPrefix="192.168.0.0/16"
subnetName="FrontEnd"
subnetPrefix="192.168.1.0/24"

# Set variables for storage
stdStorageAccountName="iaasstorystorage"

# Set variables for VM
vmSize="Standard_A1"
diskSize=127
publisher="Canonical"
offer="UbuntuServer"
sku="14.04.2-LTS"
version="latest"
vmName="WEB1"
osDiskName="osdisk"
nicName="NICWEB1"
privateIPAddress="192.168.1.101"
username='adminuser'
password='adminP@ssw0rd'
pipName="PIPWEB1"
dnsName="iaasstoryws1"
```

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="d8ac7-118">Passo 2 - Criar Olá recursos necessários para a VM</span><span class="sxs-lookup"><span data-stu-id="d8ac7-118">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="d8ac7-119">Antes de criar uma VM, precisa de um grupo de recursos, VNet, pública IP e NIC toobe utilizado pelo Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-119">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="d8ac7-120">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-120">Create a new resource group.</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="d8ac7-121">Criar Olá VNet e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-121">Create hello VNet and subnet.</span></span>

    ```azurecli
    azure network vnet create --resource-group $rgName \
        --name $vnetName \
        --address-prefixes $vnetPrefix \
        --location $location
    azure network vnet subnet create --resource-group $rgName \
        --vnet-name $vnetName \
        --name $subnetName \
        --address-prefix $subnetPrefix
    ```

3. <span data-ttu-id="d8ac7-122">Crie o recurso de IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-122">Create hello public IP resource.</span></span>

    ```azurecli
    azure network public-ip create --resource-group $rgName \
        --name $pipName \
        --location $location \
        --allocation-method Static \
        --domain-name-label $dnsName
    ```

4. <span data-ttu-id="d8ac7-123">Crie a interface de rede (NIC) do Olá para Olá VM na sub-rede Olá criado acima, com o IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-123">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="d8ac7-124">Tenha em atenção Olá primeiro conjunto de comandos são utilizados tooretrieve Olá **Id** da sub-rede Olá criado acima.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-124">Notice hello first set of commands are used tooretrieve hello **Id** of hello subnet created above.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $rgName \
        --vnet-name $vnetName \
        --name $subnetName|grep Id)"

    subnetId=${subnetId#*/}

    azure network nic create --name $nicName \
        --resource-group $rgName \
        --location $location \
        --private-ip-address $privateIPAddress \
        --subnet-id $subnetId \
        --public-ip-name $pipName
    ```

   > [!TIP]
   > <span data-ttu-id="d8ac7-125">Olá primeiro comando acima utiliza [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) e [manipulação de cadeia](http://tldp.org/LDP/abs/html/string-manipulation.html) (mais especificamente, a remoção de subcadeia).</span><span class="sxs-lookup"><span data-stu-id="d8ac7-125">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

5. <span data-ttu-id="d8ac7-126">Crie um Olá de toohost de conta de armazenamento disco de SO de VM.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-126">Create a storage account toohost hello VM OS drive.</span></span>

    ```azurecli
    azure storage account create $stdStorageAccountName \
        --resource-group $rgName \
        --location $location --type LRS
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="d8ac7-127">Passo 3 – criar Olá VM</span><span class="sxs-lookup"><span data-stu-id="d8ac7-127">Step 3 - Create hello VM</span></span>
<span data-ttu-id="d8ac7-128">Agora que todos os recursos necessários estão em vigor, pode criar uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-128">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="d8ac7-129">Crie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-129">Create hello VM.</span></span>

    ```azurecli
    azure vm create --resource-group $rgName \
        --name $vmName \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --nic-names $nicName \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $stdStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName.vhd \
        --admin-username $username \
        --admin-password $password
    ```
2. <span data-ttu-id="d8ac7-130">Guarde o ficheiro de script de Olá.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-130">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="d8ac7-131">Passo 4 - executar Olá script</span><span class="sxs-lookup"><span data-stu-id="d8ac7-131">Step 4 - Run hello script</span></span>
<span data-ttu-id="d8ac7-132">Depois de efetuar as alterações necessárias e compreender o script de Olá Mostrar acima, execute o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-132">After making any necessary changes, and understanding hello script show above, run hello script.</span></span>

1. <span data-ttu-id="d8ac7-133">A partir de uma consola de bash, execute o script de Olá acima.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-133">From a bash console, run hello script above.</span></span>

    ```azurecli
    sh myscript.sh
    ```

2. <span data-ttu-id="d8ac7-134">saída de Olá abaixo deve ser apresentada após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d8ac7-134">hello output below should be displayed after a few minutes.</span></span>

        info:    Executing command group create
        info:    Getting resource group IaaSStory
        info:    Creating resource group IaaSStory
        info:    Created resource group IaaSStory
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
        data:    Name:                IaaSStory
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command network vnet create
        info:    Looking up virtual network "TestVNet"
        info:    Creating virtual network "TestVNet"
        info:    Loading virtual network state
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/TestVNet
        data:    Name                            : TestVNet
        data:    Type                            : Microsoft.Network/virtualNetworks
        data:    Location                        : westus
        data:    ProvisioningState               : Succeeded
        data:    Address prefixes:
        data:      192.168.0.0/16
        info:    network vnet create command OK
        info:    Executing command network vnet subnet create
        info:    Looking up hello subnet "FrontEnd"
        info:    Creating subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:
        info:    network vnet subnet create command OK
        info:    Executing command network public-ip create
        info:    Looking up hello public ip "PIPWEB1"
        info:    Creating public ip address "PIPWEB1"
        info:    Looking up hello public ip "PIPWEB1"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/publicIPAddresses/PIPWEB1
        data:    Name                            : PIPWEB1
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Static
        data:    Idle timeout                    : 4
        data:    IP Address                      : 40.78.63.253
        data:    Domain name label               : iaasstoryws1
        data:    FQDN                            : iaasstoryws1.westus.cloudapp.azure.com
        info:    network public-ip create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICWEB1"
        info:    Looking up hello public ip "PIPWEB1"
        info:    Creating network interface "NICWEB1"
        info:    Looking up hello network interface "NICWEB1"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkInterfaces/NICWEB1
        data:    Name                            : NICWEB1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/publicIPAddresses/PIPWEB1
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory2/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "WEB1"
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account iaasstorystorage
        info:    Looking up hello NIC "NICWEB1"
        info:    Creating VM "WEB1"
        info:    vm create command OK
