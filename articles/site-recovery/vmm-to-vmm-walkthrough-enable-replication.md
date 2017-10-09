---
title: "site secundário do tooa de replicação de aaaEnable Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como replicação tooenable para VMs de Hyper-V replicar tooa secundário para o System Center VMM do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="7d292-103">Passo 9: Ativar o site secundário do replicação tooa para VMs de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="7d292-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="7d292-104">Depois de configurar uma política de replicação, utilize este site de System Center Virtual Machine Manager (VMM) secundária de tooa do artigo tooenable replicação para máquinas no local Hyper-V virtual (VM), utilizando [do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7d292-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="7d292-105">Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7d292-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="7d292-106">Selecione tooreplicate de VMs</span><span class="sxs-lookup"><span data-stu-id="7d292-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="7d292-107">Clique em **Passo 2: Replicar aplicação** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="7d292-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Ativar a replicação](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="7d292-109">No **origem**, selecione o servidor do VMM Olá e Olá nuvem em que Olá estão localizados os anfitriões de Hyper-V que pretende tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="7d292-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="7d292-110">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d292-110">Then click **OK**.</span></span>

    ![Ativar a replicação](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="7d292-112">No **destino**, certifique-se de que servidor VMM secundário Olá e na nuvem.</span><span class="sxs-lookup"><span data-stu-id="7d292-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="7d292-113">No **máquinas virtuais**, selecione de VMs de Olá pretende tooprotect da lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d292-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![Ativar a proteção da máquina virtual](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="7d292-115">Pode controlar o progresso de Olá **ativar proteção** ação no **tarefas** > **as tarefas de recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="7d292-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="7d292-116">Depois de Olá **finalizar proteção** tarefa é concluída, Olá a replicação inicial está concluída e Olá máquina está preparada para ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="7d292-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="7d292-117">Tenha em atenção que:</span><span class="sxs-lookup"><span data-stu-id="7d292-117">Note that:</span></span>

- <span data-ttu-id="7d292-118">Também pode ativar a proteção para máquinas virtuais na consola do VMM Olá.</span><span class="sxs-lookup"><span data-stu-id="7d292-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="7d292-119">Clique em **ativar proteção** na barra de ferramentas de Olá nas propriedades da máquina virtual de Olá > **do Azure Site Recovery** separador.</span><span class="sxs-lookup"><span data-stu-id="7d292-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="7d292-120">Depois de ativar a replicação, pode ver as propriedades de Olá VM na **itens replicados**.</span><span class="sxs-lookup"><span data-stu-id="7d292-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="7d292-121">No Olá **Essentials** dashboard, pode ver informações sobre a política de replicação de Olá para Olá VM e o respetivo estado.</span><span class="sxs-lookup"><span data-stu-id="7d292-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="7d292-122">Clique em **propriedades** para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="7d292-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="7d292-123">Carregar VMs existentes</span><span class="sxs-lookup"><span data-stu-id="7d292-123">Onboard existing VMs</span></span>

<span data-ttu-id="7d292-124">Se tiver máquinas virtuais existentes no VMM que estiver a replicar com a réplica do Hyper-V, pode carregá-las para replicação de recuperação de sites do Azure da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="7d292-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="7d292-125">Certifique-se de que o servidor Olá Hyper-V que aloja Olá que VM existente está localizado na nuvem principal Olá e esse servidor de Hyper-V Olá Olá máquina virtual de réplica de alojamento está localizado na nuvem secundário Olá.</span><span class="sxs-lookup"><span data-stu-id="7d292-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="7d292-126">Certifique-se de que uma política de replicação está configurada para a nuvem VMM principal Olá.</span><span class="sxs-lookup"><span data-stu-id="7d292-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="7d292-127">Ative a replicação para a máquina virtual primária de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d292-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="7d292-128">Do Azure Site Recovery e o VMM Certifique-se de que hello mesmo anfitrião de réplica e a máquina virtual é detetada e irá reutilizar o Azure Site Recovery e restabelecer a replicação utilizando Olá especificadas as definições.</span><span class="sxs-lookup"><span data-stu-id="7d292-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7d292-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7d292-129">Next steps</span></span>

<span data-ttu-id="7d292-130">Aceda demasiado[passo 10: executar uma ativação pós-falha de teste](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="7d292-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
