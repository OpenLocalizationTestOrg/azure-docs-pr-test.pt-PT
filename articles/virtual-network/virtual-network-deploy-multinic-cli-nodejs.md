---
title: "aaaCreate uma VM com vários NICs - CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como toocreate uma VM com vários NICs com Olá CLI do Azure 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 07c660b632bcdc004365a6f910ecf8a5c13cbc6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="7c48b-103">Criar uma VM com vários NICs com Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="7c48b-103">Create a VM with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7c48b-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7c48b-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7c48b-105">Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez de Olá [modelo de implementação clássica](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7c48b-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="7c48b-106">Olá passos seguintes utilizam um grupo de recursos com o nome *IaaSStory* para servidores WEB de Olá e um grupo de recursos denominado *IaaSStory-back-end* para servidores de Olá DB.</span><span class="sxs-lookup"><span data-stu-id="7c48b-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span> <span data-ttu-id="7c48b-107">Pode concluir esta tarefa utilizando Olá 1.0 CLI do Azure (Este artigo) ou Olá [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7c48b-107">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="7c48b-108">Olá valores "" para recursos de criação de variáveis de Olá nos passos de Olá que se seguem com as definições do cenário de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c48b-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="7c48b-109">Alterar valores Olá, conforme adequado, para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="7c48b-109">Change hello values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c48b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c48b-110">Prerequisites</span></span>
<span data-ttu-id="7c48b-111">Antes de poder criar Olá servidores de base de dados, terá de toocreate Olá *IaaSStory* grupo de recursos com todos os recursos necessários Olá para este cenário.</span><span class="sxs-lookup"><span data-stu-id="7c48b-111">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="7c48b-112">concluir a estes recursos, toocreate Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7c48b-112">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="7c48b-113">Navegue demasiado[página do modelo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="7c48b-113">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="7c48b-114">Na página de modelo de Olá, toohello à direita dos **grupo de recursos de principal**, clique em **implementar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="7c48b-114">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="7c48b-115">Se for necessário, altere os valores de parâmetros de Olá, em seguida, siga os passos de Olá no grupo de recursos de Olá de portal toodeploy de pré-visualização do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c48b-115">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c48b-116">Certifique-se de que os nomes de conta de armazenamento são exclusivos.</span><span class="sxs-lookup"><span data-stu-id="7c48b-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="7c48b-117">Não podem ter nomes de conta de armazenamento duplicado no Azure.</span><span class="sxs-lookup"><span data-stu-id="7c48b-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="7c48b-118">Criar Olá VMs do back-end</span><span class="sxs-lookup"><span data-stu-id="7c48b-118">Create hello back-end VMs</span></span>
<span data-ttu-id="7c48b-119">Olá que VMS do back-end dependem de criação de Olá de Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="7c48b-119">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="7c48b-120">**Conta de armazenamento para discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="7c48b-120">**Storage account for data disks**.</span></span> <span data-ttu-id="7c48b-121">Para um melhor desempenho, os discos de dados de Olá nos servidores de base de dados de Olá utilizará a tecnologia de unidade (SSD) de estado sólido, que requer uma conta de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="7c48b-121">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="7c48b-122">Certifique-se Olá implementar o armazenamento de premium toosupport de localização do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c48b-122">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="7c48b-123">**NICs**.</span><span class="sxs-lookup"><span data-stu-id="7c48b-123">**NICs**.</span></span> <span data-ttu-id="7c48b-124">Cada VM terá dois NICs, um para acesso de base de dados e outro para gestão.</span><span class="sxs-lookup"><span data-stu-id="7c48b-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="7c48b-125">**Conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="7c48b-125">**Availability set**.</span></span> <span data-ttu-id="7c48b-126">Todos os servidores de base de dados serão adicionados o conjunto de disponibilidade única de tooa, tooensure pelo menos uma das VMs Olá se encontra em execução durante a manutenção.</span><span class="sxs-lookup"><span data-stu-id="7c48b-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="7c48b-127">Passo 1 – iniciar o script</span><span class="sxs-lookup"><span data-stu-id="7c48b-127">Step 1 - Start your script</span></span>
<span data-ttu-id="7c48b-128">Pode transferir o script de deteção completa Olá utilizado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="7c48b-128">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="7c48b-129">Siga os passos de Olá abaixo toochange Olá script toowork no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="7c48b-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="7c48b-130">Alterar Olá valores das variáveis de Olá abaixo com base no seu grupo de recursos existente implementado acima no [pré-requisitos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="7c48b-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="7c48b-131">Alterar Olá valores das variáveis de Olá abaixo com base nos valores de Olá pretende toouse para a implementação de back-end.</span><span class="sxs-lookup"><span data-stu-id="7c48b-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. <span data-ttu-id="7c48b-132">Obter o ID de Olá para Olá `BackEnd` sub-rede onde será criada Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="7c48b-132">Retrieve hello ID for hello `BackEnd` subnet where hello VMs will be created.</span></span> <span data-ttu-id="7c48b-133">É necessário toodo isto, uma vez que Olá NICs toobe associado toothis sub-rede estão num grupo de recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="7c48b-133">You need toodo this since hello NICs toobe associated toothis subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="7c48b-134">Olá primeiro comando acima utiliza [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) e [manipulação de cadeia](http://tldp.org/LDP/abs/html/string-manipulation.html) (mais especificamente, a remoção de subcadeia).</span><span class="sxs-lookup"><span data-stu-id="7c48b-134">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="7c48b-135">Obter o ID de Olá para Olá `NSG-RemoteAccess` NSG.</span><span class="sxs-lookup"><span data-stu-id="7c48b-135">Retrieve hello ID for hello `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="7c48b-136">É necessário toodo isto, uma vez que Olá NICs toobe associados toothis NSG estão num grupo de recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="7c48b-136">You need toodo this since hello NICs toobe associated toothis NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="7c48b-137">Passo 2 – criar recursos necessários para as suas VMs</span><span class="sxs-lookup"><span data-stu-id="7c48b-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="7c48b-138">Crie um novo grupo de recursos para todos os recursos de back-end.</span><span class="sxs-lookup"><span data-stu-id="7c48b-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="7c48b-139">Utilização de Olá de aviso de Olá `$backendRGName` variável para o nome do grupo de recursos de Olá, e `$location` para Olá região do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c48b-139">Notice hello use of hello `$backendRGName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="7c48b-140">Crie uma conta de armazenamento premium para Olá SO e toobe de discos de dados utilizado pelo seu VMs.</span><span class="sxs-lookup"><span data-stu-id="7c48b-140">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="7c48b-141">Crie um conjunto de disponibilidade para Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="7c48b-141">Create an availability set for hello VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="7c48b-142">Passo 3 – criar NICs Olá e VMs do back-end</span><span class="sxs-lookup"><span data-stu-id="7c48b-142">Step 3 - Create hello NICs and back-end VMs</span></span>

1. <span data-ttu-id="7c48b-143">Iniciar um ciclo toocreate várias VMs, com base no Olá `numberOfVMs` variáveis.</span><span class="sxs-lookup"><span data-stu-id="7c48b-143">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="7c48b-144">Para cada VM, crie um NIC de acesso de base de dados.</span><span class="sxs-lookup"><span data-stu-id="7c48b-144">For each VM, create a NIC for database access.</span></span>

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. <span data-ttu-id="7c48b-145">Para cada VM, crie um NIC de acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="7c48b-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="7c48b-146">Olá aviso `--network-security-group` parâmetro, tooassociate utilizados Olá NIC tooan NSG.</span><span class="sxs-lookup"><span data-stu-id="7c48b-146">Notice hello `--network-security-group` parameter, used tooassociate hello NIC tooan NSG.</span></span>

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. <span data-ttu-id="7c48b-147">Crie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="7c48b-147">Create hello VM.</span></span>

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. <span data-ttu-id="7c48b-148">Para cada VM, criar discos de dados de dois e o ciclo de Olá fim com Olá `done` comando.</span><span class="sxs-lookup"><span data-stu-id="7c48b-148">For each VM, create two data disks, and end hello loop with hello `done` command.</span></span>

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="7c48b-149">Passo 4 - executar Olá script</span><span class="sxs-lookup"><span data-stu-id="7c48b-149">Step 4 - Run hello script</span></span>
<span data-ttu-id="7c48b-150">Agora que transferiu e alterados com base nas suas necessidades, executadas novamente Olá de toocreate Olá script de script de Olá termine VMs de base de dados com vários NICs.</span><span class="sxs-lookup"><span data-stu-id="7c48b-150">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="7c48b-151">Guarde o script e execute-à partir do **Bash** terminal.</span><span class="sxs-lookup"><span data-stu-id="7c48b-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="7c48b-152">Irá ver o resultado de inicial Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7c48b-152">You will see hello initial output, as shown below.</span></span>
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up hello availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up hello network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up hello network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB1"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB1-DA"
        info:    Looking up hello NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="7c48b-153">Após alguns minutos, vai terminar execução de Olá e irá ver o resto Olá saída Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7c48b-153">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up hello network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up hello network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB2"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB2-DA"
        info:    Looking up hello NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

