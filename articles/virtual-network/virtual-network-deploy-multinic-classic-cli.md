---
title: "aaaCreate uma VM (clássica) com vários NICs - CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como toocreate uma VM (clássica) com vários NICs com Olá interface de linha de comandos do Azure (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="115a0-103">Criar uma VM (clássica) com vários NICs com Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="115a0-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="115a0-104">Pode criar máquinas virtuais (VMs) no Azure e anexar rede várias interfaces (NICs) tooeach, das suas VMs.</span><span class="sxs-lookup"><span data-stu-id="115a0-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="115a0-105">Vários NICs ativar a separação de tipos de tráfego em NICs.</span><span class="sxs-lookup"><span data-stu-id="115a0-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="115a0-106">Por exemplo, um que NIC poderá comunicar com Olá Internet, enquanto outro comunica apenas com recursos internos não ligado toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="115a0-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="115a0-107">Olá capacidade tooseparate o tráfego de rede em vários NICs é necessário para muitas virtual os dispositivos de rede, tais como a entrega de aplicações e soluções de otimização de WAN.</span><span class="sxs-lookup"><span data-stu-id="115a0-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="115a0-108">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="115a0-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="115a0-109">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="115a0-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="115a0-110">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="115a0-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="115a0-111">Saiba como tooperform estes passos através de Olá [modelo de implementação do Resource Manager](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="115a0-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="115a0-112">Olá passos seguintes utilizam um grupo de recursos com o nome *IaaSStory* para servidores WEB de Olá e um grupo de recursos denominado *IaaSStory-back-end* para servidores de Olá DB.</span><span class="sxs-lookup"><span data-stu-id="115a0-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="115a0-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="115a0-113">Prerequisites</span></span>
<span data-ttu-id="115a0-114">Antes de poder criar Olá servidores de base de dados, terá de toocreate Olá *IaaSStory* grupo de recursos com todos os recursos necessários Olá para este cenário.</span><span class="sxs-lookup"><span data-stu-id="115a0-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="115a0-115">toocreate Olá, estes recursos, concluir os passos que se seguem.</span><span class="sxs-lookup"><span data-stu-id="115a0-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="115a0-116">Criar uma rede virtual, seguindo os passos de Olá Olá [criar uma rede virtual](virtual-networks-create-vnet-classic-cli.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="115a0-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="115a0-117">Implementar Olá back-end VMs</span><span class="sxs-lookup"><span data-stu-id="115a0-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="115a0-118">Olá que VMS do back-end dependem de criação de Olá de Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="115a0-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="115a0-119">**Conta de armazenamento para discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="115a0-119">**Storage account for data disks**.</span></span> <span data-ttu-id="115a0-120">Para um melhor desempenho, os discos de dados de Olá nos servidores de base de dados de Olá utilizará a tecnologia de unidade (SSD) de estado sólido, que requer uma conta de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="115a0-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="115a0-121">Certifique-se Olá implementar o armazenamento de premium toosupport de localização do Azure.</span><span class="sxs-lookup"><span data-stu-id="115a0-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="115a0-122">**NICs**.</span><span class="sxs-lookup"><span data-stu-id="115a0-122">**NICs**.</span></span> <span data-ttu-id="115a0-123">Cada VM terá dois NICs, um para acesso de base de dados e outro para gestão.</span><span class="sxs-lookup"><span data-stu-id="115a0-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="115a0-124">**Conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="115a0-124">**Availability set**.</span></span> <span data-ttu-id="115a0-125">Todos os servidores de base de dados serão adicionados o conjunto de disponibilidade única de tooa, tooensure pelo menos uma das VMs Olá se encontra em execução durante a manutenção.</span><span class="sxs-lookup"><span data-stu-id="115a0-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="115a0-126">Passo 1 – iniciar o script</span><span class="sxs-lookup"><span data-stu-id="115a0-126">Step 1 - Start your script</span></span>
<span data-ttu-id="115a0-127">Pode transferir o script de deteção completa Olá utilizado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="115a0-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="115a0-128">Olá concluir os seguintes passos toochange Olá script toowork no seu ambiente:</span><span class="sxs-lookup"><span data-stu-id="115a0-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="115a0-129">Alterar Olá valores das variáveis de Olá abaixo com base no seu grupo de recursos existente implementado acima no [pré-requisitos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="115a0-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="115a0-130">Alterar Olá valores das variáveis de Olá abaixo com base nos valores de Olá pretende toouse para a implementação de back-end.</span><span class="sxs-lookup"><span data-stu-id="115a0-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="115a0-131">Passo 2 – criar recursos necessários para as suas VMs</span><span class="sxs-lookup"><span data-stu-id="115a0-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="115a0-132">Crie um novo serviço em nuvem para todas as VMs do back-end.</span><span class="sxs-lookup"><span data-stu-id="115a0-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="115a0-133">Utilização de Olá de aviso de Olá `$backendCSName` variável para o nome do grupo de recursos de Olá, e `$location` para Olá região do Azure.</span><span class="sxs-lookup"><span data-stu-id="115a0-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="115a0-134">Crie uma conta de armazenamento premium para Olá SO e toobe de discos de dados utilizado pelo seu VMs.</span><span class="sxs-lookup"><span data-stu-id="115a0-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="115a0-135">Passo 3 – criar VMs com vários NICs</span><span class="sxs-lookup"><span data-stu-id="115a0-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="115a0-136">Iniciar um ciclo toocreate várias VMs, com base no Olá `numberOfVMs` variáveis.</span><span class="sxs-lookup"><span data-stu-id="115a0-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="115a0-137">Para cada VM, especifique o nome de Olá e endereço IP de cada uma das Olá dois NICs.</span><span class="sxs-lookup"><span data-stu-id="115a0-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="115a0-138">Crie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="115a0-138">Create hello VM.</span></span> <span data-ttu-id="115a0-139">Tenha em atenção a utilização de Olá de Olá `--nic-config` parâmetro, que contém uma lista de todos os NICs com nome, uma sub-rede e endereço IP.</span><span class="sxs-lookup"><span data-stu-id="115a0-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="115a0-140">Para cada VM, crie dois discos de dados.</span><span class="sxs-lookup"><span data-stu-id="115a0-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="115a0-141">Passo 4 - executar Olá script</span><span class="sxs-lookup"><span data-stu-id="115a0-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="115a0-142">Agora que transferiu e alterados com base nas suas necessidades, executadas novamente Olá de toocreate Olá script de script de Olá termine VMs de base de dados com vários NICs.</span><span class="sxs-lookup"><span data-stu-id="115a0-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="115a0-143">Guarde o script e execute-à partir do **Bash** terminal.</span><span class="sxs-lookup"><span data-stu-id="115a0-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="115a0-144">Irá ver o resultado de inicial Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="115a0-144">You will see hello initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="115a0-145">Após alguns minutos, vai terminar execução de Olá e irá ver o resto Olá saída Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="115a0-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
