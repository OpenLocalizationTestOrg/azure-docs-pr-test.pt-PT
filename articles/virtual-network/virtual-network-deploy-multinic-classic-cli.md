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
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a>Criar uma VM (clássica) com vários NICs com Olá CLI do Azure 1.0

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Pode criar máquinas virtuais (VMs) no Azure e anexar rede várias interfaces (NICs) tooeach, das suas VMs. Vários NICs ativar a separação de tipos de tráfego em NICs. Por exemplo, um que NIC poderá comunicar com Olá Internet, enquanto outro comunica apenas com recursos internos não ligado toohello Internet. Olá capacidade tooseparate o tráfego de rede em vários NICs é necessário para muitas virtual os dispositivos de rede, tais como a entrega de aplicações e soluções de otimização de WAN.

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Saiba como tooperform estes passos através de Olá [modelo de implementação do Resource Manager](virtual-network-deploy-multinic-arm-cli.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Olá passos seguintes utilizam um grupo de recursos com o nome *IaaSStory* para servidores WEB de Olá e um grupo de recursos denominado *IaaSStory-back-end* para servidores de Olá DB.

## <a name="prerequisites"></a>Pré-requisitos
Antes de poder criar Olá servidores de base de dados, terá de toocreate Olá *IaaSStory* grupo de recursos com todos os recursos necessários Olá para este cenário. toocreate Olá, estes recursos, concluir os passos que se seguem. Criar uma rede virtual, seguindo os passos de Olá Olá [criar uma rede virtual](virtual-networks-create-vnet-classic-cli.md) artigo.

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a>Implementar Olá back-end VMs
Olá que VMS do back-end dependem de criação de Olá de Olá os seguintes recursos:

* **Conta de armazenamento para discos de dados**. Para um melhor desempenho, os discos de dados de Olá nos servidores de base de dados de Olá utilizará a tecnologia de unidade (SSD) de estado sólido, que requer uma conta de armazenamento premium. Certifique-se Olá implementar o armazenamento de premium toosupport de localização do Azure.
* **NICs**. Cada VM terá dois NICs, um para acesso de base de dados e outro para gestão.
* **Conjunto de disponibilidade**. Todos os servidores de base de dados serão adicionados o conjunto de disponibilidade única de tooa, tooensure pelo menos uma das VMs Olá se encontra em execução durante a manutenção.

### <a name="step-1---start-your-script"></a>Passo 1 – iniciar o script
Pode transferir o script de deteção completa Olá utilizado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh). Olá concluir os seguintes passos toochange Olá script toowork no seu ambiente:

1. Alterar Olá valores das variáveis de Olá abaixo com base no seu grupo de recursos existente implementado acima no [pré-requisitos](#Prerequisites).

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. Alterar Olá valores das variáveis de Olá abaixo com base nos valores de Olá pretende toouse para a implementação de back-end.

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Passo 2 – criar recursos necessários para as suas VMs
1. Crie um novo serviço em nuvem para todas as VMs do back-end. Utilização de Olá de aviso de Olá `$backendCSName` variável para o nome do grupo de recursos de Olá, e `$location` para Olá região do Azure.

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. Crie uma conta de armazenamento premium para Olá SO e toobe de discos de dados utilizado pelo seu VMs.

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a>Passo 3 – criar VMs com vários NICs
1. Iniciar um ciclo toocreate várias VMs, com base no Olá `numberOfVMs` variáveis.

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. Para cada VM, especifique o nome de Olá e endereço IP de cada uma das Olá dois NICs.

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. Crie Olá VM. Tenha em atenção a utilização de Olá de Olá `--nic-config` parâmetro, que contém uma lista de todos os NICs com nome, uma sub-rede e endereço IP.

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

4. Para cada VM, crie dois discos de dados.

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a>Passo 4 - executar Olá script
Agora que transferiu e alterados com base nas suas necessidades, executadas novamente Olá de toocreate Olá script de script de Olá termine VMs de base de dados com vários NICs.

1. Guarde o script e execute-à partir do **Bash** terminal. Irá ver o resultado de inicial Olá, conforme mostrado abaixo.

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

2. Após alguns minutos, vai terminar execução de Olá e irá ver o resto Olá saída Olá, conforme mostrado abaixo.

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
