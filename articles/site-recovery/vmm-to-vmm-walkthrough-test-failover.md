---
title: "aaaRun uma ativação pós-falha de teste para o site secundário do tooa de replicação de VM de Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toorun uma ativação pós-falha de teste para tooa de replicação de VM de Hyper-V secundário para o System Center VMM do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="7d01e-103">Passo 10: Executar uma ativação pós-falha de teste para o site secundário do tooa de replicação de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="7d01e-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="7d01e-104">Depois de ativar a replicação para máquinas virtuais de Hyper-V (VMs) com [do Azure Site Recovery](site-recovery-overview.md), utilize este artigo de toorun uma ativação pós-falha de teste.</span><span class="sxs-lookup"><span data-stu-id="7d01e-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="7d01e-105">Uma ativação pós-falha de teste verifica que a replicação está a funcionar, sem afetar o seu ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7d01e-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="7d01e-106">Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7d01e-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="7d01e-107">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7d01e-107">Before you start</span></span>

- <span data-ttu-id="7d01e-108">Quando estiver a acionar uma ativação pós-falha de teste, pode especificar as réplica de teste toowhich de rede do Olá Olá que ligarão as VMs.</span><span class="sxs-lookup"><span data-stu-id="7d01e-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="7d01e-109">[Saiba mais](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sobre as opções de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="7d01e-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="7d01e-110">Recomendamos que não escolha uma rede que selecionou durante o mapeamento da rede.</span><span class="sxs-lookup"><span data-stu-id="7d01e-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="7d01e-111">instruções de Olá neste artigo descrevem como toofail através de uma única VM.</span><span class="sxs-lookup"><span data-stu-id="7d01e-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="7d01e-112">Leia sobre [criar planos de recuperação](site-recovery-create-recovery-plans.md) se quiser toofail através de várias VMs em conjunto.</span><span class="sxs-lookup"><span data-stu-id="7d01e-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="7d01e-113">Leia sobre [limitações para as ativações pós-falha de teste](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="7d01e-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="7d01e-114">Olá endereço IP especificado tooa VM durante a ativação pós-falha de teste é Olá mesmo endereço IP que Olá VM receberia para uma ativação de pós-falha planeada ou imprevista (presuming que o endereço IP Olá está disponível na rede de ativação pós-falha de teste de Olá).</span><span class="sxs-lookup"><span data-stu-id="7d01e-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="7d01e-115">Se o endereço IP Olá não está disponível na rede de ativação pós-falha de teste de Olá, Olá VM recebe outro endereço IP que está disponível na rede de ativação pós-falha de teste de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d01e-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="7d01e-116">Se pretender toodo uma ativação pós-falha de teste na sua rede de produção, para validatation completo da máquina de conectividade de rede ponto a ponto, tenha em atenção que:</span><span class="sxs-lookup"><span data-stu-id="7d01e-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="7d01e-117">Olá que VM principal deve ser encerrado quando estiver a efetuar ativação pós-falha de teste de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d01e-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="7d01e-118">Caso contrário, duas VMs com Olá mesma identidade será executado numa Olá mesmo rede em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="7d01e-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="7d01e-119">Se efetuar alterações tootest VMs, essas alterações serão perdidas quando a limpeza Olá ativação pós-falha de teste.</span><span class="sxs-lookup"><span data-stu-id="7d01e-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="7d01e-120">Estas alterações não são replicada toohello back VM principal.</span><span class="sxs-lookup"><span data-stu-id="7d01e-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="7d01e-121">Testar uma rede de produção leva toodowntime para as cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="7d01e-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="7d01e-122">Peça aos utilizadores não toouse aplicação Olá quando exercício de recuperação de desastre Olá está em curso.</span><span class="sxs-lookup"><span data-stu-id="7d01e-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="7d01e-123">Executar uma ativação pós-falha de teste para uma VM</span><span class="sxs-lookup"><span data-stu-id="7d01e-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="7d01e-124">toofail através de uma única VM, na **itens replicados**, clique em Olá VM > **ativação pós-falha de teste**.</span><span class="sxs-lookup"><span data-stu-id="7d01e-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="7d01e-125">No **ativação pós-falha de teste**, especifique como o teste VMs será ligado toonetworks após a ativação pós-falha de teste de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d01e-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="7d01e-126">Clique em **OK** toobegin ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d01e-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="7d01e-127">Controlar o progresso no Olá **tarefas** separador.</span><span class="sxs-lookup"><span data-stu-id="7d01e-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="7d01e-128">Após a conclusão da ativação pós-falha, certifique-se que teste Olá início VMs com êxito.</span><span class="sxs-lookup"><span data-stu-id="7d01e-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="7d01e-129">Quando tiver terminado, clique em **ativação pós-falha de teste de limpeza** no plano de recuperação Olá.</span><span class="sxs-lookup"><span data-stu-id="7d01e-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="7d01e-130">No **notas**, registar e guardar todas as observações associadas à ativação pós-falha de teste de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d01e-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="7d01e-131">Este passo elimina Olá máquinas de virtuais e redes que foram criados durante a ativação pós-falha de teste.</span><span class="sxs-lookup"><span data-stu-id="7d01e-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7d01e-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7d01e-132">Next steps</span></span>

<span data-ttu-id="7d01e-133">Depois de ter testado implementação Olá, saiba mais sobre outros tipos de [ativação pós-falha](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="7d01e-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
