---
title: "endereços IP privados aaaConfigure para VMs - CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como endereços IP privados tooconfigure para máquinas virtuais utilizando Olá interface de linha de comandos do Azure (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a><span data-ttu-id="fea4b-103">Configurar endereços IP privados para uma máquina virtual utilizando Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="fea4b-103">Configure private IP addresses for a virtual machine using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="fea4b-104">Tarefas do CLI versões toocomplete Olá</span><span class="sxs-lookup"><span data-stu-id="fea4b-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="fea4b-105">Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:</span><span class="sxs-lookup"><span data-stu-id="fea4b-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="fea4b-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="fea4b-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="fea4b-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -nosso CLI de próxima geração para o modelo de implementação da gestão de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="fea4b-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="fea4b-108">Este artigo abrange o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="fea4b-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="fea4b-109">Também pode [gerir o endereço IP privado estático no modelo de implementação clássica Olá](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fea4b-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="fea4b-110">comandos de CLI do Azure de exemplo de Olá abaixo esperam num ambiente simple que já criado.</span><span class="sxs-lookup"><span data-stu-id="fea4b-110">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="fea4b-111">Se pretender que os comandos de Olá toorun como são apresentados neste documento, primeiro criar ambiente de teste de Olá descrito [criar uma vnet](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fea4b-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="fea4b-112">Como toospecify um privada endereços IP estáticos quando criar uma VM</span><span class="sxs-lookup"><span data-stu-id="fea4b-112">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="fea4b-113">toocreate uma VM chamada *DNS01* no Olá *front-end* sub-rede de uma VNet com o nome *TestVNet* com um IP privado estático de *192.168.1.101*, Siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="fea4b-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="fea4b-114">Se nunca tiver utilizado a CLI do Azure, consulte o artigo [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md) e siga as instruções de Olá toohello ponto onde poderá selecionar a sua conta do Azure e a subscrição de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="fea4b-114">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="fea4b-115">Executar Olá **modo de configuração do azure** comando tooswitch tooResource modo Manager, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="fea4b-115">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="fea4b-116">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fea4b-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="fea4b-117">Executar Olá **público-ip da rede do azure crie** toocreate um IP público para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="fea4b-117">Run hello **azure network public-ip create** toocreate a public IP for hello VM.</span></span> <span data-ttu-id="fea4b-118">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="fea4b-118">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="fea4b-119">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fea4b-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="fea4b-120">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="fea4b-121">Nome do IP público de Olá grupo de recursos Olá será criada.</span><span class="sxs-lookup"><span data-stu-id="fea4b-121">Name of hello resource group hello public IP will be created in.</span></span>
   * <span data-ttu-id="fea4b-122">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-122">**-n (or --name)**.</span></span> <span data-ttu-id="fea4b-123">Nome do IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="fea4b-123">Name of hello public IP.</span></span>
   * <span data-ttu-id="fea4b-124">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-124">**-l (or --location)**.</span></span> <span data-ttu-id="fea4b-125">Região do Azure onde será criado Olá um IP público.</span><span class="sxs-lookup"><span data-stu-id="fea4b-125">Azure region where hello public IP will be created.</span></span> <span data-ttu-id="fea4b-126">Para o nosso cenário *centralus*.</span><span class="sxs-lookup"><span data-stu-id="fea4b-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="fea4b-127">Executar Olá **nic da rede do azure crie** comando toocreate um NIC com um IP privado estático.</span><span class="sxs-lookup"><span data-stu-id="fea4b-127">Run hello **azure network nic create** command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="fea4b-128">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="fea4b-128">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="fea4b-129">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fea4b-129">Expected output:</span></span>
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * <span data-ttu-id="fea4b-130">**-a (ou - endereço de ip privado)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="fea4b-131">Endereço IP privado estático para Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="fea4b-131">Static private IP address for hello NIC.</span></span>
   * <span data-ttu-id="fea4b-132">**-m (ou --vnet-nome de sub-rede)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="fea4b-133">Nome do Olá VNet onde será criada Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="fea4b-133">Name of hello VNet where hello NIC will be created.</span></span>
   * <span data-ttu-id="fea4b-134">**-k (ou - nome de sub-rede)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="fea4b-135">Nome da sub-rede olá onde será criada Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="fea4b-135">Name of hello subnet where hello NIC will be created.</span></span>
5. <span data-ttu-id="fea4b-136">Executar Olá **vm do azure crie** Olá do comando toocreate VM com o IP público Olá e NIC criado acima.</span><span class="sxs-lookup"><span data-stu-id="fea4b-136">Run hello **azure vm create** command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="fea4b-137">lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.</span><span class="sxs-lookup"><span data-stu-id="fea4b-137">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="fea4b-138">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fea4b-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="fea4b-139">**-y (ou tipo de SO –)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="fea4b-140">Tipo de operativo ou o sistema para Olá VM, *Windows* ou *Linux*.</span><span class="sxs-lookup"><span data-stu-id="fea4b-140">Type of operating system for hello VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="fea4b-141">**-f (ou - nic-name)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="fea4b-142">Nome do Olá NIC Olá VM irá utilizar.</span><span class="sxs-lookup"><span data-stu-id="fea4b-142">Name of hello NIC hello VM will use.</span></span>
   * <span data-ttu-id="fea4b-143">**-i (ou - nome do ip público)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="fea4b-144">Nome do Olá IP público VM do Olá irá utilizar.</span><span class="sxs-lookup"><span data-stu-id="fea4b-144">Name of hello public IP hello VM will use.</span></span>
   * <span data-ttu-id="fea4b-145">**-F (ou -- vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="fea4b-146">Nome do Olá VNet onde Olá VM será criada.</span><span class="sxs-lookup"><span data-stu-id="fea4b-146">Name of hello VNet where hello VM will be created.</span></span>
   * <span data-ttu-id="fea4b-147">**-j (ou -- vnet-nome de sub-rede)**.</span><span class="sxs-lookup"><span data-stu-id="fea4b-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="fea4b-148">Nome da sub-rede olá onde Olá VM será criada.</span><span class="sxs-lookup"><span data-stu-id="fea4b-148">Name of hello subnet where hello VM will be created.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="fea4b-149">Como as informações de uma VM do endereço IP privado estático de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="fea4b-149">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="fea4b-150">IP privado estático tooview Olá informações para Olá criada a VM com o script de Olá acima, execute os seguintes comandos da CLI do Azure de Olá de endereço e observar os valores de Olá para *método de alocação de IP privado* e *endereço IP privado*:</span><span class="sxs-lookup"><span data-stu-id="fea4b-150">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="fea4b-151">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fea4b-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="fea4b-152">Como tooremove um privada endereços IP estáticos de uma VM</span><span class="sxs-lookup"><span data-stu-id="fea4b-152">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="fea4b-153">É possível remover um endereço IP privado estático um NIC na CLI do Azure para o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fea4b-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="fea4b-154">Tem de criar um novo NIC que utiliza um IP dinâmico, remova Olá NIC anterior de Olá VM e, em seguida, adicionar Olá novo NIC toohello VM.</span><span class="sxs-lookup"><span data-stu-id="fea4b-154">You must create a new NIC that uses a dynamic IP, remove hello previous NIC from hello VM, and then add hello new NIC toohello VM.</span></span> <span data-ttu-id="fea4b-155">toochange Olá NIC para Olá VM utilizado int eh comandos acima, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="fea4b-155">toochange hello NIC for hello VM used int eh commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="fea4b-156">Executar Olá **nic da rede do azure crie** comando toocreate um NIC de novo utilizando a atribuição de IP dinâmico.</span><span class="sxs-lookup"><span data-stu-id="fea4b-156">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="fea4b-157">Observe como não precisa de endereço IP de Olá toospecify neste momento.</span><span class="sxs-lookup"><span data-stu-id="fea4b-157">Notice how you do not need toospecify hello IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="fea4b-158">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fea4b-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. <span data-ttu-id="fea4b-159">Executar Olá **conjunto da vm do azure** Olá toochange do comando NIC utilizada pelo Olá VM.</span><span class="sxs-lookup"><span data-stu-id="fea4b-159">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="fea4b-160">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fea4b-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="fea4b-161">Se quisesse, execute Olá **nic da rede do azure eliminar** comando os NIC de antigo Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="fea4b-161">If wanted, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="fea4b-162">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fea4b-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="fea4b-163">Como tooadd um IP privado estático endereços tooan existente VM</span><span class="sxs-lookup"><span data-stu-id="fea4b-163">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="fea4b-164">tooadd um estático privada IP endereço toohello NIC utilizada pela VM criada utilizando o script de Olá acima, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fea4b-164">tooadd a static private IP address toohello NIC used by teh VM created using hello script above, run hello following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="fea4b-165">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fea4b-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a><span data-ttu-id="fea4b-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fea4b-166">Next steps</span></span>
* <span data-ttu-id="fea4b-167">Saiba mais sobre [reservado de IP público](virtual-networks-reserved-public-ip.md) endereços.</span><span class="sxs-lookup"><span data-stu-id="fea4b-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="fea4b-168">Saiba mais sobre [instância ao nível do IP público (ILPIP)](virtual-networks-instance-level-public-ip.md) endereços.</span><span class="sxs-lookup"><span data-stu-id="fea4b-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="fea4b-169">Consulte Olá [as APIs REST do IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="fea4b-169">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

