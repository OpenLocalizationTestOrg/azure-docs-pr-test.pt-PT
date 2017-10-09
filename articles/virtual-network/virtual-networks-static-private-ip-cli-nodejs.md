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
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a>Configurar endereços IP privados para uma máquina virtual utilizando Olá CLI do Azure 1.0


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá 

Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá: 

- [Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)
- [Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -nosso CLI de próxima geração para o modelo de implementação da gestão de recursos de Olá 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo abrange o modelo de implementação do Resource Manager Olá. Também pode [gerir o endereço IP privado estático no modelo de implementação clássica Olá](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

comandos de CLI do Azure de exemplo de Olá abaixo esperam num ambiente simple que já criado. Se pretender que os comandos de Olá toorun como são apresentados neste documento, primeiro criar ambiente de teste de Olá descrito [criar uma vnet](virtual-networks-create-vnet-arm-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Como toospecify um privada endereços IP estáticos quando criar uma VM
toocreate uma VM chamada *DNS01* no Olá *front-end* sub-rede de uma VNet com o nome *TestVNet* com um IP privado estático de *192.168.1.101*, Siga os passos de Olá abaixo:

1. Se nunca tiver utilizado a CLI do Azure, consulte o artigo [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md) e siga as instruções de Olá toohello ponto onde poderá selecionar a sua conta do Azure e a subscrição de cópia de segurança.
2. Executar Olá **modo de configuração do azure** comando tooswitch tooResource modo Manager, como mostrado abaixo.
   
        azure config mode arm
   
    Resultado esperado:
   
        info:    New mode is arm
3. Executar Olá **público-ip da rede do azure crie** toocreate um IP público para Olá VM. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    Resultado esperado:
   
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
   
   * **-g (ou --resource-group)**. Nome do IP público de Olá grupo de recursos Olá será criada.
   * **-n (ou --name)**. Nome do IP público Olá.
   * **-l (ou --location)**. Região do Azure onde será criado Olá um IP público. Para o nosso cenário *centralus*.
4. Executar Olá **nic da rede do azure crie** comando toocreate um NIC com um IP privado estático. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    Resultado esperado:
   
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
   
   * **-a (ou - endereço de ip privado)**. Endereço IP privado estático para Olá NIC.
   * **-m (ou --vnet-nome de sub-rede)**. Nome do Olá VNet onde será criada Olá NIC.
   * **-k (ou - nome de sub-rede)**. Nome da sub-rede olá onde será criada Olá NIC.
5. Executar Olá **vm do azure crie** Olá do comando toocreate VM com o IP público Olá e NIC criado acima. lista de Olá apresentada depois do resultado de Olá explica os parâmetros de Olá utilizados.
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    Resultado esperado:
   
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
   
   * **-y (ou tipo de SO –)**. Tipo de operativo ou o sistema para Olá VM, *Windows* ou *Linux*.
   * **-f (ou - nic-name)**. Nome do Olá NIC Olá VM irá utilizar.
   * **-i (ou - nome do ip público)**. Nome do Olá IP público VM do Olá irá utilizar.
   * **-F (ou -- vnet-name)**. Nome do Olá VNet onde Olá VM será criada.
   * **-j (ou -- vnet-nome de sub-rede)**. Nome da sub-rede olá onde Olá VM será criada.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Como as informações de uma VM do endereço IP privado estático de tooretrieve
IP privado estático tooview Olá informações para Olá criada a VM com o script de Olá acima, execute os seguintes comandos da CLI do Azure de Olá de endereço e observar os valores de Olá para *método de alocação de IP privado* e *endereço IP privado*:

    azure vm show -g TestRG -n DNS01

Resultado esperado:

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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Como tooremove um privada endereços IP estáticos de uma VM
É possível remover um endereço IP privado estático um NIC na CLI do Azure para o Resource Manager. Tem de criar um novo NIC que utiliza um IP dinâmico, remova Olá NIC anterior de Olá VM e, em seguida, adicionar Olá novo NIC toohello VM. toochange Olá NIC para Olá VM utilizado int eh comandos acima, siga os passos de Olá abaixo.

1. Executar Olá **nic da rede do azure crie** comando toocreate um NIC de novo utilizando a atribuição de IP dinâmico. Observe como não precisa de endereço IP de Olá toospecify neste momento.
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    Resultado esperado:
   
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
2. Executar Olá **conjunto da vm do azure** Olá toochange do comando NIC utilizada pelo Olá VM.
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    Resultado esperado:
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. Se quisesse, execute Olá **nic da rede do azure eliminar** comando os NIC de antigo Olá toodelete.
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    Resultado esperado:
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Como tooadd um IP privado estático endereços tooan existente VM
tooadd um estático privada IP endereço toohello NIC utilizada pela VM criada utilizando o script de Olá acima, execute Olá os seguintes comandos:

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

Resultado esperado:

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

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [reservado de IP público](virtual-networks-reserved-public-ip.md) endereços.
* Saiba mais sobre [instância ao nível do IP público (ILPIP)](virtual-networks-instance-level-public-ip.md) endereços.
* Consulte Olá [as APIs REST do IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).

