---
title: "aaaCreate uma VM (clássica) com vários NICs com o PowerShell | Microsoft Docs"
description: "Saiba como toocreate e configurar as VMs com vários NICs com o PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>Criar uma VM (clássica) com vários NICs
Pode criar máquinas virtuais (VMs) no Azure e anexar rede várias interfaces (NICs) tooeach, das suas VMs. Vários NICs são um requisito para muitos virtual os dispositivos de rede, tais como a entrega de aplicações e soluções de otimização de WAN. Vários NICs também fornecem o isolamento do tráfego entre NICs.

![Várias NIC para VM](./media/virtual-networks-multiple-nics/IC757773.png)

Mostra a figura de Olá uma VM com três NICs, cada um ligado tooa outra sub-rede.

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que implementações mais novas utilizem o Gestor de recursos.

* VIP de acesso à Internet (implementações clássicas) só é suportada numa NIC de "predefinido" Olá em Não há apenas um VIP toohello IP NIC de predefinição Olá.
* Neste momento, os endereços IP de público ao nível do instância (LPIP) (implementações clássicas) não são suportados para várias VMs de NIC.
* Olá ordem de Olá NICs de dentro de Olá VM será aleatórias e também pode alterar através de atualizações de infraestrutura do Azure. No entanto, Olá endereços IP e Olá ethernet correspondente MAC endereços permanecerá Olá mesmo. Por exemplo, suponha **Eth1** tem o endereço IP 10.1.0.100 e um endereço MAC 00-0D-3A-B0-39-0D; após uma atualização da infraestrutura do Azure e a reinicialização, pode ser alterado demasiado**Eth2**, mas Olá IP e MAC emparelhamento será permanecem Olá mesmo. Quando for iniciada pelo cliente, Olá ordem NIC permanecerá Olá mesmo.
* Olá endereço para cada NIC em cada VM tem de estar localizado numa sub-rede, vários NICs num único VM pode cada ser atribuída Olá de endereços que estão na mesma sub-rede.
* Olá tamanho da VM determina o número de Olá de NICS que pode criar para uma VM. Olá referência [do Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM tamanhos toodetermine de artigos de quantas NICS suporta cada tamanho da VM. 

## <a name="network-security-groups-nsgs"></a>Grupos de segurança de rede (NSGs)
Numa implementação do Resource Manager, qualquer NIC numa VM pode ser associado com uma segurança grupo rede (NSG), incluindo quaisquer NICs numa VM que tenha vários NICs ativados. Se um NIC é atribuído um endereço de uma sub-rede de onde se encontra associado um NSG sub-rede Olá, em seguida, hello regras NSG da sub-rede Olá também se aplicam toothat NIC. Adição tooassociating sub-redes com NSGs, também pode associar um NIC com um NSG.

Se uma sub-rede é associada a um NSG e um NIC dentro dessa sub-rede individualmente associada um NSG, Olá associado regras do NSG são aplicadas em **fluxo ordem** toohello direção do tráfego de Olá que está a ser transmitido para ou de acordo com Olá NIC:

* **Tráfego de entrada** cujo destino é Olá NIC no pergunta flui primeiro através de sub-rede Olá, acionar as regras do NSG da sub-rede Olá, antes de passar para Olá NIC, em seguida, acionar as regras do NSG do Olá NIC.
* **Tráfego de saída** cuja origem é Olá NIC em questão flui primeiro fora do Olá NIC, acionar as regras do NSG da NIC Olá, antes de passar pela sub-rede Olá, em seguida, acionar as regras do NSG da sub-rede Olá.

Saiba mais sobre [grupos de segurança de rede](virtual-networks-nsg.md) e como são aplicadas com base nas associações toosubnets, VMs e NICs...

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a>Como tooConfigure um várias VMS NIC numa implementação clássica
instruções de Olá abaixo irão ajudá-lo a criar um várias VMS NIC que contém 3 NICs: uma predefinição NIC e dois NICs adicionais. passos de configuração de Olá irão criar uma VM que será configurada de acordo com toohello serviço Configuração ficheiro fragmento abaixo:

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


Terá de Olá os seguintes pré-requisitos antes de tentar comandos do PowerShell Olá toorun no exemplo de Olá.

* Uma subscrição do Azure.
* Uma rede virtual configurada. Consulte [descrição geral de rede Virtual](virtual-networks-overview.md) para obter mais informações sobre as VNets.
* versão mais recente do Olá do Azure PowerShell transferido e instalado. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

toocreate uma VM com vários NICs, Olá concluir os passos seguintes, introduzindo cada comando dentro de uma única sessão do PowerShell:

1. Selecione uma imagem VM a partir da Galeria de imagem de VM do Azure. Tenha em atenção que as imagens alterado frequentemente e estão disponíveis através da região. Olá imagem especificada no exemplo Olá abaixo poderá alterar ou poderá não estar na sua região, por isso, não se esqueça de imagem de Olá toospecify precisa.

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. Crie uma configuração de VM.

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. Crie o início de sessão do Olá predefinido administrador.

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. Adicione configuração de VM de toohello NICs adicionais.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. Especifique uma sub-rede de Olá e endereço IP para a NIC de predefinição Olá.

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. Crie Olá VM na sua rede virtual.

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > Olá VNet que especificar aqui tem de existir (tal como mencionado na pré-requisitos de Olá). exemplo de Olá abaixo Especifica uma rede virtual denominada **MultiNIC VNet**.
    >

## <a name="limitations"></a>Limitações
Olá seguintes limitações é aplicável ao utilizar vários NICs:

* As VMs com vários NICs tem de ser criadas no Azure redes virtuais (VNets). Não é possível configurar a VNet não VMs com vários NICs.
* Todas as VMs na disponibilidade de um conjunto necessidade toouse vários NICs ou uma NIC único. Não pode ser uma mistura de várias VMs de NIC e único de NIC de VMs dentro de um conjunto de disponibilidade. Mesmas regras aplicam-se para VMs num serviço em nuvem. Para várias VMs de NIC, não são necessários toohave Olá o mesmo número de NICs, desde que cada têm, pelo menos, dois.
* Não é possível configurar uma VM com um único NIC com vários NICs (e vice-versa) depois de ser implementado, sem eliminar e voltar a criar.

## <a name="secondary-nics-access-tooother-subnets"></a>Secundárias sub-redes de tooother de acesso de NICs
Por predefinição NICs secundárias não serão configurados com um gateway predefinido, devido a toowhich Olá fluxo de tráfego em Olá NICs secundários será limitado toobe dentro Olá mesma sub-rede. Se pretenderem que os utilizadores de Olá tooenable secundário NICs tootalk fora da sua própria sub-rede, terá tooadd uma entrada no Olá tabela tooconfigure Olá gateway de encaminhamento como descrita abaixo.

> [!NOTE]
> VMs criados antes de Julho de 2015, pode ter um gateway predefinido configurado para todos os NICs. gateway predefinido de Olá para NICs secundárias não será removido até que estas VMs são reiniciados. Em sistemas operativos que utilizam o modelo, da encaminhamento de anfitrião fracos de Olá, tais como o Linux, pode interromper a conectividade à Internet se hello tráfego de entrada e de saída utilizar diferentes NICs.
> 

### <a name="configure-windows-vms"></a>Configurar VMs do Windows
Suponha que tem uma VM do Windows com dois NICs da seguinte forma:

* Endereço IP da NIC principal: 192.168.1.4
* Endereço de IP de NIC secundário: 192.168.2.5

tabela de rota IPv4 Olá para esta VM seria ter este aspeto:

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

Repare a que rota predefinida (0.0.0.0) Olá é NIC. principal de apenas toohello disponíveis Não será tooaccess capaz de recursos fora da sub-rede Olá Olá secundário NIC, como mostrado abaixo:

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

Olá, tooadd uma predefinição de rotas no NIC secundário, siga Olá passos abaixo:

1. Numa linha de comandos, execute o comando de Olá abaixo o número de índice de Olá tooidentify para Olá NIC secundário:
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. Tenha em atenção a entrada de segundo Olá na tabela de Olá, com um índice de 27 (neste exemplo).
3. A partir da linha de comandos Olá, execute Olá **rota adicionar** comando conforme mostrado abaixo. Neste exemplo, estiver a especificar 192.168.2.1 como gateway predefinido de Olá para Olá NIC secundário:
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. conectividade tootest, volte atrás toohello linha de comandos e tente tooping sub-rede diferente de Olá NIC secundário como int mostrado eh exemplo abaixo:
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. Também pode verificar o Olá de toocheck de tabela de rota recém-adicionada rota, como mostrado abaixo:
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a>Configurar VMs com Linux
Para VMs com Linux, uma vez que utiliza o comportamento predefinido de Olá anfitrião fraca encaminhamento, recomendamos que Olá NICs secundários são fluxos de tootraffic restrito apenas dentro do Olá mesma sub-rede. No entanto se determinados cenários exigem conectividade fora sub-rede Olá, utilizadores devem ativar tooensure de encaminhamento baseado na política que Olá entrada e saída tráfego utiliza Olá mesmo NIC.

## <a name="next-steps"></a>Passos seguintes
* Implementar [MultiNIC VMs num cenário de aplicação de camada 2 numa implementação do Resource Manager](virtual-network-deploy-multinic-arm-template.md).
* Implementar [MultiNIC VMs num cenário de aplicação de camada 2 numa implementação clássica](virtual-network-deploy-multinic-classic-ps.md).

