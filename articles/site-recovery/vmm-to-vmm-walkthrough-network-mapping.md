---
title: "aaaMap redes para o site secundário do tooa de replicação de VM de Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toomap redes quando replicar VMs Hyper-V tooa site secundário do VMM com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="a413a-103">Passo 7: Mapear redes para o site secundário de tooa do replicação de VM de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="a413a-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="a413a-104">Depois de configurar [as definições de origem e destino](vmm-to-vmm-walkthrough-source-target.md) para replicar o site de System Center Virtual Machine Manager (VMM) Hyper-V máquinas virtuais (VMs) tooa secundário, utilize o mapeamento da rede tooconfigure este artigo para virtual do Hyper-V tooa de replicação de máquina (VM) secundário do site, utilizando [do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a413a-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="a413a-105">Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a413a-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="a413a-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a413a-106">Before you start</span></span>

- <span data-ttu-id="a413a-107">Saiba mais sobre [mapeamento da rede](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="a413a-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="a413a-108">Certifique-se de que as máquinas virtuais nos servidores VMM estão ligados tooa rede VM.</span><span class="sxs-lookup"><span data-stu-id="a413a-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="a413a-109">Configurar o mapeamento da rede</span><span class="sxs-lookup"><span data-stu-id="a413a-109">Configure network mapping</span></span>

1. <span data-ttu-id="a413a-110">No **mapeamento da rede** > **mapeamentos da rede**, clique em **+ mapeamento da rede**.</span><span class="sxs-lookup"><span data-stu-id="a413a-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="a413a-111">No **adicionar mapeamento da rede** separador, selecione a origem de Olá e servidores do VMM de destino.</span><span class="sxs-lookup"><span data-stu-id="a413a-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="a413a-112">redes VM de Olá associadas a servidores de Olá do VMM são obtidos.</span><span class="sxs-lookup"><span data-stu-id="a413a-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="a413a-113">No **rede de origem**, selecione rede Olá pretende toouse na lista de redes VM associadas com o servidor VMM principal do Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="a413a-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="a413a-114">No **rede de destino**, selecione rede Olá pretende toouse do servidor VMM Olá secundário.</span><span class="sxs-lookup"><span data-stu-id="a413a-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="a413a-115">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a413a-115">Then click **OK**.</span></span>

    ![Mapeamento da rede](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="a413a-117">Veja a seguir o que acontece quando começa o mapeamento da rede:</span><span class="sxs-lookup"><span data-stu-id="a413a-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="a413a-118">Quaisquer máquinas de virtuais de réplica existente que correspondem a rede VM de origem toohello será toohello ligado a rede VM de destino.</span><span class="sxs-lookup"><span data-stu-id="a413a-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="a413a-119">Novas máquinas virtuais que estão ligados toohello rede VM de origem serão ligados toohello destino mapeadas rede após a replicação.</span><span class="sxs-lookup"><span data-stu-id="a413a-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="a413a-120">Se modificar um mapeamento existente com uma nova rede, as máquinas virtuais de réplica serão ligadas utilizando as novas definições Olá.</span><span class="sxs-lookup"><span data-stu-id="a413a-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="a413a-121">Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome de sub-rede na máquina virtual de origem que Olá está localizado, em seguida, Olá máquina virtual de réplica será ligada toothat sub-rede de destino após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="a413a-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="a413a-122">Se não existir nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será ligado toohello primeira sub-rede Olá rede.</span><span class="sxs-lookup"><span data-stu-id="a413a-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a413a-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a413a-123">Next steps</span></span>

<span data-ttu-id="a413a-124">Aceda demasiado[passo 8: configurar uma política de replicação](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="a413a-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
