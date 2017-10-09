---
title: "mapeamento de aaaNetwork entre duas regiões do Azure no Azure Site Recovery | Microsoft Docs"
description: "O Azure Site Recovery coordena a replicação de Olá, a ativação pós-falha e a recuperação de máquinas virtuais e servidores físicos. Saiba mais sobre tooAzure de ativação pós-falha ou num datacenter secundário."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="4aebd-104">Mapeamento de rede entre as duas regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="4aebd-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="4aebd-105">Este artigo descreve como toomap Azure redes virtuais das duas regiões do Azure entre si.</span><span class="sxs-lookup"><span data-stu-id="4aebd-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="4aebd-106">Mapeamento de rede assegura que quando a máquina virtual replicada é criada no destino Olá região do Azure, é criada em Olá de rede virtual é mapeado toovirtual rede Olá virtual da máquina de origem.</span><span class="sxs-lookup"><span data-stu-id="4aebd-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="4aebd-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4aebd-107">Prerequisites</span></span>
<span data-ttu-id="4aebd-108">Antes de mapear redes Certifique-se, criou [redes virtuais do Azure](../virtual-network/virtual-networks-overview.md) na origem e destino regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aebd-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="4aebd-109">Mapear redes</span><span class="sxs-lookup"><span data-stu-id="4aebd-109">Map networks</span></span>

<span data-ttu-id="4aebd-110">toomap uma Azure virtual network na rede virtual do tooanother de uma região do Azure noutra região, aceda tooSite infraestrutura de recuperação -> o mapeamento da rede (para máquinas virtuais do Azure) e crie um mapeamento da rede.</span><span class="sxs-lookup"><span data-stu-id="4aebd-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="4aebd-112">No Olá o exemplo abaixo minha máquina virtual está em execução na Ásia Oriental região e está a ser replicadas tooSoutheast Ásia.</span><span class="sxs-lookup"><span data-stu-id="4aebd-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="4aebd-113">Selecione a rede de origem e destino Olá e, em seguida, clique em OK toocreate um mapeamento de rede de Oriental tooSoutheast Ásia.</span><span class="sxs-lookup"><span data-stu-id="4aebd-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="4aebd-115">Olá a mesma coisa toocreate um mapeamento de rede do Sudeste asiático tooEast Ásia.</span><span class="sxs-lookup"><span data-stu-id="4aebd-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="4aebd-117">Mapeamento de rede ao ativar a replicação</span><span class="sxs-lookup"><span data-stu-id="4aebd-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="4aebd-118">Se não é executado o mapeamento da rede quando estiver a replicar uma máquina virtual para Olá primeiro tempo formulário uma região do Azure tooanother, em seguida, pode escolher a rede de destino como parte da Olá mesmo processo.</span><span class="sxs-lookup"><span data-stu-id="4aebd-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="4aebd-119">Recuperação de sites cria os mapeamentos de rede da região de tootarget de região de origem e a região de toosource de região de destino com base nesta seleção.</span><span class="sxs-lookup"><span data-stu-id="4aebd-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="4aebd-121">Por predefinição, a recuperação de sites cria uma rede na região de destino Olá que é a rede de origem toohello idênticas e adicionando '-asr' como um nome de toohello sufixos de rede de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="4aebd-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="4aebd-122">Pode escolher uma rede já criada ao clicar em Personalizar.</span><span class="sxs-lookup"><span data-stu-id="4aebd-122">You can choose an already created network by clicking Customize.</span></span>

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="4aebd-124">Se o mapeamento da rede Olá já é concluído, não é possível alterar a rede virtual de destino Olá durante a ativação da replicação.</span><span class="sxs-lookup"><span data-stu-id="4aebd-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="4aebd-125">toochange, modifique o mapeamento de rede existente.</span><span class="sxs-lookup"><span data-stu-id="4aebd-125">toochange it, modify existing network mapping.</span></span>  

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="4aebd-128">Se modificar um mapeamento de rede de 1 região tooregion-2, certifique-se que modificar o mapeamento da rede Olá de região-2 tooregion-1 também.</span><span class="sxs-lookup"><span data-stu-id="4aebd-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="4aebd-129">Seleção de sub-rede</span><span class="sxs-lookup"><span data-stu-id="4aebd-129">Subnet selection</span></span>
<span data-ttu-id="4aebd-130">Sub-rede Olá virtual da máquina de destino está selecionado com base no nome de Olá da sub-rede Olá Olá virtual da máquina de origem.</span><span class="sxs-lookup"><span data-stu-id="4aebd-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="4aebd-131">Se existir uma sub-rede de Olá mesmo nome que Olá virtual da máquina de origem disponível na rede de destino Olá, em seguida, o que é escolhido para Olá máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="4aebd-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="4aebd-132">Se não existir nenhuma sub-rede com Olá mesmo nome na rede de destino Olá, em seguida, por ordem alfabética primeira sub-rede é escolhido como Olá sub-rede de destino.</span><span class="sxs-lookup"><span data-stu-id="4aebd-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="4aebd-133">Pode modificar esta sub-rede acedendo tooCompute e definições de rede da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="4aebd-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![Modificar a sub-rede](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="4aebd-135">Endereço IP</span><span class="sxs-lookup"><span data-stu-id="4aebd-135">IP address</span></span>

<span data-ttu-id="4aebd-136">Endereço IP para cada interface de rede Olá Olá virtual da máquina de destino é escolhido, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4aebd-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="4aebd-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="4aebd-137">DHCP</span></span>
<span data-ttu-id="4aebd-138">Se a interface de rede Olá Olá virtual da máquina de origem estiver a utilizar DHCP, a interface de rede da máquina de virtual de destino Olá também está definido como DHCP.</span><span class="sxs-lookup"><span data-stu-id="4aebd-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="4aebd-139">IP estático</span><span class="sxs-lookup"><span data-stu-id="4aebd-139">Static IP</span></span>
<span data-ttu-id="4aebd-140">Se a interface de rede Olá Olá virtual da máquina de origem utilizar IP estático, a interface de rede Olá virtual da máquina de destino seja também definido toouse IP estático.</span><span class="sxs-lookup"><span data-stu-id="4aebd-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="4aebd-141">IP estático é escolhido, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4aebd-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="4aebd-142">Mesmo espaço de endereços</span><span class="sxs-lookup"><span data-stu-id="4aebd-142">Same address space</span></span>

<span data-ttu-id="4aebd-143">Se a sub-rede de origem Olá e a sub-rede de destino Olá têm Olá mesmo espaço de endereços, IP de destino é definida igual ao IP Olá Olá da interface de rede Olá virtual da máquina de origem.</span><span class="sxs-lookup"><span data-stu-id="4aebd-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="4aebd-144">Se o mesmo IP não estiver disponível, alguns outro IP disponível está definido como Olá IP de destino.</span><span class="sxs-lookup"><span data-stu-id="4aebd-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="4aebd-145">Espaço de endereços diferente</span><span class="sxs-lookup"><span data-stu-id="4aebd-145">Different address space</span></span>

<span data-ttu-id="4aebd-146">Se a sub-rede de origem Olá e a sub-rede de destino Olá têm espaço de endereços diferente, IP de destino está definido como qualquer IP disponível na sub-rede de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="4aebd-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="4aebd-147">Pode modificar o IP de destino Olá em cada interface de rede acedendo tooCompute e definições de rede da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="4aebd-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aebd-148">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4aebd-148">Next steps</span></span>

- <span data-ttu-id="4aebd-149">Saiba mais sobre [redes orientações para replicar as VMs do Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="4aebd-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
