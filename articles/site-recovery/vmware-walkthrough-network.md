---
title: "aaaPlan de rede para a replicação do VMware tooAzure | Microsoft Docs"
description: "Este artigo aborda de planeamento necessários quando replicar VMs de VMware tooAzure da rede"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5578a0b4-0352-41c3-9cce-56beb17a4d97
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 2b4f385c768cc7f5e98abae0afb8258b00f3724f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-vmware-tooazure-replication"></a><span data-ttu-id="3b97b-103">Passo 4: Planear o funcionamento em rede para a replicação de tooAzure de VMware</span><span class="sxs-lookup"><span data-stu-id="3b97b-103">Step 4: Plan networking for VMware tooAzure replication</span></span>

<span data-ttu-id="3b97b-104">Este artigo resume rede considerações de planeamento quando replicar no local tooAzure de VMs de VMware utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="3b97b-104">This article summarizes network planning considerations when replicating on-premises VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="3b97b-105">Publique quaisquer comentários na parte inferior deste artigo hello, ou colocar questões no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3b97b-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connect-tooreplica-vms"></a><span data-ttu-id="3b97b-106">Ligar as VMs de tooreplica</span><span class="sxs-lookup"><span data-stu-id="3b97b-106">Connect tooreplica VMs</span></span>

<span data-ttu-id="3b97b-107">Ao planear a replicação e a estratégia de ativação pós-falha, uma das perguntas chave Olá é como tooconnect toohello VM do Azure após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="3b97b-108">Existem duas opções ao conceber a estratégia de rede para a réplica de VMs do Azure:</span><span class="sxs-lookup"><span data-stu-id="3b97b-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="3b97b-109">**Utilize o endereço IP diferente**: pode selecionar toouse um intervalo de endereços IP diferentes para Olá replicado a rede VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b97b-109">**Use different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="3b97b-110">Olá este cenário VM obtém um novo endereço IP, após a ativação pós-falha e é necessária uma atualização DNS.</span><span class="sxs-lookup"><span data-stu-id="3b97b-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="3b97b-111">**Manter o mesmo endereço IP**: É aconselhável toouse Olá mesmo intervalo de endereços IP que no seu site no local primário, Olá rede Azure após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-111">**Retain same IP address**: You might want toouse hello same IP address range as that in your primary on-premises site, for hello Azure network after failover.</span></span> <span data-ttu-id="3b97b-112">Olá manter os mesmos endereços IP simplifica a recuperação de Olá, reduzindo relativamente a problemas de rede após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-112">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="3b97b-113">No entanto, quando está a replicar tooAzure, terá de rotas tooupdate com a localização nova Olá endereços IP Olá após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-113">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span> 


## <a name="retain-ip-addresses"></a><span data-ttu-id="3b97b-114">Manter os endereços IP</span><span class="sxs-lookup"><span data-stu-id="3b97b-114">Retain IP addresses</span></span>

<span data-ttu-id="3b97b-115">Recuperação de sites fornece a capacidade de Olá tooretain fixo endereços IP quando efetuar a ativação pós-falha tooAzure, com uma sub-rede de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-115">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="3b97b-116">Com a ativação pós-falha de sub-rede, uma sub-rede específica está presente no Site 1 ou 2 do Site, mas nunca em ambos os sites em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="3b97b-116">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="3b97b-117">Na ordem toomaintain Olá espaço de endereços IP no evento Olá de uma ativação pós-falha, é através de programação dispor Olá router infraestrutura toomove Olá sub-redes de um site tooanother.</span><span class="sxs-lookup"><span data-stu-id="3b97b-117">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="3b97b-118">Durante a ativação pós-falha, Olá sub-redes mover com Olá associados a máquinas virtuais protegidas.</span><span class="sxs-lookup"><span data-stu-id="3b97b-118">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="3b97b-119">desvantagem principal Olá é que o evento de Olá de uma falha, têm toomove Olá todo sub-rede.</span><span class="sxs-lookup"><span data-stu-id="3b97b-119">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="3b97b-120">Exemplo de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="3b97b-120">Failover example</span></span>

<span data-ttu-id="3b97b-121">Vamos ver um exemplo de tooAzure de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-121">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="3b97b-122">Uma empresa de ficticious, o Woodgrove Bank, tem uma infraestrutura no local, as aplicações de empresas de alojamento.</span><span class="sxs-lookup"><span data-stu-id="3b97b-122">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="3b97b-123">As aplicações móveis estão alojadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b97b-123">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="3b97b-124">A conectividade entre VMs do Banco Woodgrove nos servidores do Azure e no local é fornecida por uma ligação de (VPN) de site a site entre a rede de limite Olá no local e Olá rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b97b-124">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="3b97b-125">Isto significa VPN que Olá da rede virtual da empresa no Azure aparece como uma extensão da sua rede no local.</span><span class="sxs-lookup"><span data-stu-id="3b97b-125">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="3b97b-126">Woodgrove pretende tooAzure de cargas de trabalho do toouse recuperação de Site tooreplicate no local.</span><span class="sxs-lookup"><span data-stu-id="3b97b-126">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="3b97b-127">Woodgrove tem toodeal com as aplicações e configurações que dependem hard-coded endereços IP e, por conseguinte, tem de endereços IP tooretain para as aplicações após tooAzure de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-127">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="3b97b-128">Woodgrove tem endereços IP do intervalo 172.16.1.0/24, 172.16.2.0/24 tooits recursos atribuídos em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b97b-128">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="3b97b-129">Para Woodgrove toobe capaz de tooreplicate respetivo tooAzure VMS enquanto mantém Olá IP endereços, é aqui que empresa Olá tem toodo:</span><span class="sxs-lookup"><span data-stu-id="3b97b-129">For Woodgrove toobe able tooreplicate its VMS tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="3b97b-130">Crie uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b97b-130">Create an Azure virtual network.</span></span> <span data-ttu-id="3b97b-131">Deve ser uma extensão de Olá no local rede, para que as aplicações podem efetuar a ativação pós-falha totalmente integrada.</span><span class="sxs-lookup"><span data-stu-id="3b97b-131">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="3b97b-132">O Azure permite-lhe tooadd local para conetividade VPN, além disso redes do toohello de conetividade toopoint para o site virtual criadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b97b-132">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="3b97b-133">Quando configurar a ligação de site a site Olá, no Olá Azure de rede, pode encaminhar localização do tráfego toohello no local (rede local) apenas se o intervalo de endereços IP Olá é diferente do intervalo de endereços IP Olá no local.</span><span class="sxs-lookup"><span data-stu-id="3b97b-133">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="3b97b-134">Isto acontece porque o Azure não suporta sub-redes Stretch.</span><span class="sxs-lookup"><span data-stu-id="3b97b-134">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="3b97b-135">Por isso, se tiver de sub-rede 192.168.1.0/24 no local, não é possível adicionar um 192.168.1.0/24 local da rede no Olá rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b97b-135">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="3b97b-136">Isto é esperado porque o Azure não sabe que existem sem VMs do Active Directory na sub-rede Olá e essa sub-rede Olá está a ser criada para a recuperação de desastre apenas.</span><span class="sxs-lookup"><span data-stu-id="3b97b-136">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="3b97b-137">toobe toocorrectly consegue encaminhar o tráfego de rede fora de uma rede Azure Olá sub-redes rede Olá e Olá da rede local não pode entrar em conflito.</span><span class="sxs-lookup"><span data-stu-id="3b97b-137">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![Antes da ativação pós-falha de sub-rede](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="3b97b-139">Antes da ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="3b97b-139">Before failover</span></span>

1. <span data-ttu-id="3b97b-140">Crie uma rede adicional (por exemplo rede recuperação).</span><span class="sxs-lookup"><span data-stu-id="3b97b-140">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="3b97b-141">Esta é Olá rede em que executar a ativação pós-falha de VMs são criados.</span><span class="sxs-lookup"><span data-stu-id="3b97b-141">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="3b97b-142">tooensure hello endereço IP para uma VM é mantido após uma ativação pós-falha, nas propriedades VM Olá > **configurar**, especifique Olá esse Olá VM tem no local e clique em de endereços IP mesmo **guardar**.</span><span class="sxs-lookup"><span data-stu-id="3b97b-142">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="3b97b-143">Quando Olá VM é efetuada a ativação pós-falha, o Azure Site Recovery atribuirá Olá fornecido tooit de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="3b97b-143">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![Propriedades da rede](./media/site-recovery-network-design/network-design8.png)

4. <span data-ttu-id="3b97b-145">Após a ativação pós-falha acionador é acionado e Olá VMs são criadas no Azure com o endereço IP Olá necessário, pode ligar toohello rede utilizando um [Vnet tooVnet ligação](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3b97b-145">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet connection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="3b97b-146">Esta ação pode ser colocado em script.</span><span class="sxs-lookup"><span data-stu-id="3b97b-146">This action can be scripted.</span></span>
5. <span data-ttu-id="3b97b-147">Tem de rotas toobe adequadamente modificado, tooreflect esse 192.168.1.0/24 foi agora movido tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3b97b-147">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![Após a ativação pós-falha de sub-rede](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="3b97b-149">Após a ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="3b97b-149">After failover</span></span>

<span data-ttu-id="3b97b-150">Se não tiver uma rede do Azure, conforme ilustrado acima, pode criar uma ligação de VPN de site a site entre o site primário e o Azure, após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-150">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failover.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="3b97b-151">Alterar os endereços IP</span><span class="sxs-lookup"><span data-stu-id="3b97b-151">Change IP addresses</span></span>

<span data-ttu-id="3b97b-152">Isto [blogue](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explica como tooset segurança Olá infraestrutura de rede do Azure quando não precisar tooretain IP endereços após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-152">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="3b97b-153">Começa com uma descrição da aplicação, procura como tooset configurar redes no local e no Azure e conclui com informações sobre como executar as ativações pós-falha.</span><span class="sxs-lookup"><span data-stu-id="3b97b-153">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3b97b-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3b97b-154">Next steps</span></span>

<span data-ttu-id="3b97b-155">Aceda demasiado[passo 5: preparar o Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3b97b-155">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>
