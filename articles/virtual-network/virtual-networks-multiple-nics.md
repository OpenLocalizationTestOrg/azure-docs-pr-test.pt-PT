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
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="9c21a-103">Criar uma VM (clássica) com vários NICs</span><span class="sxs-lookup"><span data-stu-id="9c21a-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="9c21a-104">Pode criar máquinas virtuais (VMs) no Azure e anexar rede várias interfaces (NICs) tooeach, das suas VMs.</span><span class="sxs-lookup"><span data-stu-id="9c21a-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="9c21a-105">Vários NICs são um requisito para muitos virtual os dispositivos de rede, tais como a entrega de aplicações e soluções de otimização de WAN.</span><span class="sxs-lookup"><span data-stu-id="9c21a-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="9c21a-106">Vários NICs também fornecem o isolamento do tráfego entre NICs.</span><span class="sxs-lookup"><span data-stu-id="9c21a-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Várias NIC para VM](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="9c21a-108">Mostra a figura de Olá uma VM com três NICs, cada um ligado tooa outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9c21a-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c21a-109">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9c21a-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9c21a-110">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="9c21a-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="9c21a-111">A Microsoft recomenda que implementações mais novas utilizem o Gestor de recursos.</span><span class="sxs-lookup"><span data-stu-id="9c21a-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="9c21a-112">VIP de acesso à Internet (implementações clássicas) só é suportada numa NIC de "predefinido" Olá em</span><span class="sxs-lookup"><span data-stu-id="9c21a-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="9c21a-113">Não há apenas um VIP toohello IP NIC de predefinição Olá.</span><span class="sxs-lookup"><span data-stu-id="9c21a-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="9c21a-114">Neste momento, os endereços IP de público ao nível do instância (LPIP) (implementações clássicas) não são suportados para várias VMs de NIC.</span><span class="sxs-lookup"><span data-stu-id="9c21a-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="9c21a-115">Olá ordem de Olá NICs de dentro de Olá VM será aleatórias e também pode alterar através de atualizações de infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c21a-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="9c21a-116">No entanto, Olá endereços IP e Olá ethernet correspondente MAC endereços permanecerá Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="9c21a-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="9c21a-117">Por exemplo, suponha **Eth1** tem o endereço IP 10.1.0.100 e um endereço MAC 00-0D-3A-B0-39-0D; após uma atualização da infraestrutura do Azure e a reinicialização, pode ser alterado demasiado**Eth2**, mas Olá IP e MAC emparelhamento será permanecem Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="9c21a-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="9c21a-118">Quando for iniciada pelo cliente, Olá ordem NIC permanecerá Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="9c21a-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="9c21a-119">Olá endereço para cada NIC em cada VM tem de estar localizado numa sub-rede, vários NICs num único VM pode cada ser atribuída Olá de endereços que estão na mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9c21a-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="9c21a-120">Olá tamanho da VM determina o número de Olá de NICS que pode criar para uma VM.</span><span class="sxs-lookup"><span data-stu-id="9c21a-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="9c21a-121">Olá referência [do Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM tamanhos toodetermine de artigos de quantas NICS suporta cada tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="9c21a-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="9c21a-122">Grupos de segurança de rede (NSGs)</span><span class="sxs-lookup"><span data-stu-id="9c21a-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="9c21a-123">Numa implementação do Resource Manager, qualquer NIC numa VM pode ser associado com uma segurança grupo rede (NSG), incluindo quaisquer NICs numa VM que tenha vários NICs ativados.</span><span class="sxs-lookup"><span data-stu-id="9c21a-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="9c21a-124">Se um NIC é atribuído um endereço de uma sub-rede de onde se encontra associado um NSG sub-rede Olá, em seguida, hello regras NSG da sub-rede Olá também se aplicam toothat NIC.</span><span class="sxs-lookup"><span data-stu-id="9c21a-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="9c21a-125">Adição tooassociating sub-redes com NSGs, também pode associar um NIC com um NSG.</span><span class="sxs-lookup"><span data-stu-id="9c21a-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="9c21a-126">Se uma sub-rede é associada a um NSG e um NIC dentro dessa sub-rede individualmente associada um NSG, Olá associado regras do NSG são aplicadas em **fluxo ordem** toohello direção do tráfego de Olá que está a ser transmitido para ou de acordo com Olá NIC:</span><span class="sxs-lookup"><span data-stu-id="9c21a-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="9c21a-127">**Tráfego de entrada** cujo destino é Olá NIC no pergunta flui primeiro através de sub-rede Olá, acionar as regras do NSG da sub-rede Olá, antes de passar para Olá NIC, em seguida, acionar as regras do NSG do Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="9c21a-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="9c21a-128">**Tráfego de saída** cuja origem é Olá NIC em questão flui primeiro fora do Olá NIC, acionar as regras do NSG da NIC Olá, antes de passar pela sub-rede Olá, em seguida, acionar as regras do NSG da sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="9c21a-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="9c21a-129">Saiba mais sobre [grupos de segurança de rede](virtual-networks-nsg.md) e como são aplicadas com base nas associações toosubnets, VMs e NICs...</span><span class="sxs-lookup"><span data-stu-id="9c21a-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="9c21a-130">Como tooConfigure um várias VMS NIC numa implementação clássica</span><span class="sxs-lookup"><span data-stu-id="9c21a-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="9c21a-131">instruções de Olá abaixo irão ajudá-lo a criar um várias VMS NIC que contém 3 NICs: uma predefinição NIC e dois NICs adicionais.</span><span class="sxs-lookup"><span data-stu-id="9c21a-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="9c21a-132">passos de configuração de Olá irão criar uma VM que será configurada de acordo com toohello serviço Configuração ficheiro fragmento abaixo:</span><span class="sxs-lookup"><span data-stu-id="9c21a-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

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


<span data-ttu-id="9c21a-133">Terá de Olá os seguintes pré-requisitos antes de tentar comandos do PowerShell Olá toorun no exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="9c21a-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="9c21a-134">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c21a-134">An Azure subscription.</span></span>
* <span data-ttu-id="9c21a-135">Uma rede virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="9c21a-135">A configured virtual network.</span></span> <span data-ttu-id="9c21a-136">Consulte [descrição geral de rede Virtual](virtual-networks-overview.md) para obter mais informações sobre as VNets.</span><span class="sxs-lookup"><span data-stu-id="9c21a-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="9c21a-137">versão mais recente do Olá do Azure PowerShell transferido e instalado.</span><span class="sxs-lookup"><span data-stu-id="9c21a-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="9c21a-138">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9c21a-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="9c21a-139">toocreate uma VM com vários NICs, Olá concluir os passos seguintes, introduzindo cada comando dentro de uma única sessão do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9c21a-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="9c21a-140">Selecione uma imagem VM a partir da Galeria de imagem de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c21a-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="9c21a-141">Tenha em atenção que as imagens alterado frequentemente e estão disponíveis através da região.</span><span class="sxs-lookup"><span data-stu-id="9c21a-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="9c21a-142">Olá imagem especificada no exemplo Olá abaixo poderá alterar ou poderá não estar na sua região, por isso, não se esqueça de imagem de Olá toospecify precisa.</span><span class="sxs-lookup"><span data-stu-id="9c21a-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="9c21a-143">Crie uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="9c21a-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="9c21a-144">Crie o início de sessão do Olá predefinido administrador.</span><span class="sxs-lookup"><span data-stu-id="9c21a-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="9c21a-145">Adicione configuração de VM de toohello NICs adicionais.</span><span class="sxs-lookup"><span data-stu-id="9c21a-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="9c21a-146">Especifique uma sub-rede de Olá e endereço IP para a NIC de predefinição Olá.</span><span class="sxs-lookup"><span data-stu-id="9c21a-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="9c21a-147">Crie Olá VM na sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9c21a-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="9c21a-148">Olá VNet que especificar aqui tem de existir (tal como mencionado na pré-requisitos de Olá).</span><span class="sxs-lookup"><span data-stu-id="9c21a-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="9c21a-149">exemplo de Olá abaixo Especifica uma rede virtual denominada **MultiNIC VNet**.</span><span class="sxs-lookup"><span data-stu-id="9c21a-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="9c21a-150">Limitações</span><span class="sxs-lookup"><span data-stu-id="9c21a-150">Limitations</span></span>
<span data-ttu-id="9c21a-151">Olá seguintes limitações é aplicável ao utilizar vários NICs:</span><span class="sxs-lookup"><span data-stu-id="9c21a-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="9c21a-152">As VMs com vários NICs tem de ser criadas no Azure redes virtuais (VNets).</span><span class="sxs-lookup"><span data-stu-id="9c21a-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="9c21a-153">Não é possível configurar a VNet não VMs com vários NICs.</span><span class="sxs-lookup"><span data-stu-id="9c21a-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="9c21a-154">Todas as VMs na disponibilidade de um conjunto necessidade toouse vários NICs ou uma NIC único.</span><span class="sxs-lookup"><span data-stu-id="9c21a-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="9c21a-155">Não pode ser uma mistura de várias VMs de NIC e único de NIC de VMs dentro de um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="9c21a-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="9c21a-156">Mesmas regras aplicam-se para VMs num serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="9c21a-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="9c21a-157">Para várias VMs de NIC, não são necessários toohave Olá o mesmo número de NICs, desde que cada têm, pelo menos, dois.</span><span class="sxs-lookup"><span data-stu-id="9c21a-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="9c21a-158">Não é possível configurar uma VM com um único NIC com vários NICs (e vice-versa) depois de ser implementado, sem eliminar e voltar a criar.</span><span class="sxs-lookup"><span data-stu-id="9c21a-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="9c21a-159">Secundárias sub-redes de tooother de acesso de NICs</span><span class="sxs-lookup"><span data-stu-id="9c21a-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="9c21a-160">Por predefinição NICs secundárias não serão configurados com um gateway predefinido, devido a toowhich Olá fluxo de tráfego em Olá NICs secundários será limitado toobe dentro Olá mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9c21a-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="9c21a-161">Se pretenderem que os utilizadores de Olá tooenable secundário NICs tootalk fora da sua própria sub-rede, terá tooadd uma entrada no Olá tabela tooconfigure Olá gateway de encaminhamento como descrita abaixo.</span><span class="sxs-lookup"><span data-stu-id="9c21a-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="9c21a-162">VMs criados antes de Julho de 2015, pode ter um gateway predefinido configurado para todos os NICs.</span><span class="sxs-lookup"><span data-stu-id="9c21a-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="9c21a-163">gateway predefinido de Olá para NICs secundárias não será removido até que estas VMs são reiniciados.</span><span class="sxs-lookup"><span data-stu-id="9c21a-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="9c21a-164">Em sistemas operativos que utilizam o modelo, da encaminhamento de anfitrião fracos de Olá, tais como o Linux, pode interromper a conectividade à Internet se hello tráfego de entrada e de saída utilizar diferentes NICs.</span><span class="sxs-lookup"><span data-stu-id="9c21a-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="9c21a-165">Configurar VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="9c21a-165">Configure Windows VMs</span></span>
<span data-ttu-id="9c21a-166">Suponha que tem uma VM do Windows com dois NICs da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="9c21a-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="9c21a-167">Endereço IP da NIC principal: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="9c21a-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="9c21a-168">Endereço de IP de NIC secundário: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="9c21a-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="9c21a-169">tabela de rota IPv4 Olá para esta VM seria ter este aspeto:</span><span class="sxs-lookup"><span data-stu-id="9c21a-169">hello IPv4 route table for this VM would look like this:</span></span>

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

<span data-ttu-id="9c21a-170">Repare a que rota predefinida (0.0.0.0) Olá é NIC. principal de apenas toohello disponíveis</span><span class="sxs-lookup"><span data-stu-id="9c21a-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="9c21a-171">Não será tooaccess capaz de recursos fora da sub-rede Olá Olá secundário NIC, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="9c21a-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="9c21a-172">Olá, tooadd uma predefinição de rotas no NIC secundário, siga Olá passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="9c21a-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="9c21a-173">Numa linha de comandos, execute o comando de Olá abaixo o número de índice de Olá tooidentify para Olá NIC secundário:</span><span class="sxs-lookup"><span data-stu-id="9c21a-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="9c21a-174">Tenha em atenção a entrada de segundo Olá na tabela de Olá, com um índice de 27 (neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="9c21a-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="9c21a-175">A partir da linha de comandos Olá, execute Olá **rota adicionar** comando conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9c21a-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="9c21a-176">Neste exemplo, estiver a especificar 192.168.2.1 como gateway predefinido de Olá para Olá NIC secundário:</span><span class="sxs-lookup"><span data-stu-id="9c21a-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="9c21a-177">conectividade tootest, volte atrás toohello linha de comandos e tente tooping sub-rede diferente de Olá NIC secundário como int mostrado eh exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="9c21a-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="9c21a-178">Também pode verificar o Olá de toocheck de tabela de rota recém-adicionada rota, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="9c21a-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="9c21a-179">Configurar VMs com Linux</span><span class="sxs-lookup"><span data-stu-id="9c21a-179">Configure Linux VMs</span></span>
<span data-ttu-id="9c21a-180">Para VMs com Linux, uma vez que utiliza o comportamento predefinido de Olá anfitrião fraca encaminhamento, recomendamos que Olá NICs secundários são fluxos de tootraffic restrito apenas dentro do Olá mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9c21a-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="9c21a-181">No entanto se determinados cenários exigem conectividade fora sub-rede Olá, utilizadores devem ativar tooensure de encaminhamento baseado na política que Olá entrada e saída tráfego utiliza Olá mesmo NIC.</span><span class="sxs-lookup"><span data-stu-id="9c21a-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c21a-182">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9c21a-182">Next steps</span></span>
* <span data-ttu-id="9c21a-183">Implementar [MultiNIC VMs num cenário de aplicação de camada 2 numa implementação do Resource Manager](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="9c21a-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="9c21a-184">Implementar [MultiNIC VMs num cenário de aplicação de camada 2 numa implementação clássica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9c21a-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

