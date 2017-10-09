---
title: "replicação aaaEnable para VMs de VMware replicar tooAzure com o Azure Site Recovery | Microsoft Docs"
description: "Resume os passos de Olá terá tooenable replicação tooAzure para VMs de VMware com o serviço do Azure Site Recovery Olá"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a><span data-ttu-id="7d5fe-103">Passo 11: Ativar a replicação para tooAzure de máquinas virtuais de VMware</span><span class="sxs-lookup"><span data-stu-id="7d5fe-103">Step 11: Enable replication for VMware virtual machines tooAzure</span></span>


<span data-ttu-id="7d5fe-104">Este artigo descreve como tooenable replicação de VMware no local virtual máquinas tooAzure, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-104">This article describes how tooenable replication for on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="7d5fe-105">Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7d5fe-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="7d5fe-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7d5fe-106">Before you start</span></span>

- <span data-ttu-id="7d5fe-107">VMs de VMware tem de ter Olá [componente de serviço de mobilidade instalado](vmware-walkthrough-install-mobility.md).</span><span class="sxs-lookup"><span data-stu-id="7d5fe-107">VMware VMs must have hello [Mobility service component installed](vmware-walkthrough-install-mobility.md).</span></span> <span data-ttu-id="7d5fe-108">-Se uma VM está preparada para a instalação de push, o servidor de processos de Olá instala automaticamente o serviço de mobilidade Olá ao ativar a replicação.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-108">- If a VM is prepared for push installation, hello process server automatically installs hello Mobility service when you enable replication.</span></span>
- <span data-ttu-id="7d5fe-109">A conta de utilizador do Azure tem específico [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicação de uma VM tooAzure</span><span class="sxs-lookup"><span data-stu-id="7d5fe-109">Your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a VM tooAzure</span></span>
- <span data-ttu-id="7d5fe-110">Quando adiciona ou modifica as VMs, pode demorar até too15 minutos ou já está em vigor tootake de alterações e para os mesmos tooappear no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-110">When you add or modify VMs, it can take up too15 minutes or longer for changes tootake effect, and for them tooappear in hello portal.</span></span>
- <span data-ttu-id="7d5fe-111">Pode verificar o tempo Olá pela última vez detetado para VMs no **servidores de configuração** > **último contacto em**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-111">You can check hello last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="7d5fe-112">tooadd VMs sem aguardar deteção agendada do Olá, servidor de configuração de Olá realce (não clique nele) e clique em **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-112">tooadd VMs without waiting for hello scheduled discovery, highlight hello configuration server (don’t click it), and click **Refresh**.</span></span>



## <a name="exclude-disks-from-replication"></a><span data-ttu-id="7d5fe-113">Excluir discos da replicação</span><span class="sxs-lookup"><span data-stu-id="7d5fe-113">Exclude disks from replication</span></span>

<span data-ttu-id="7d5fe-114">Por predefinição, todos os discos numa máquina são replicados.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-114">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="7d5fe-115">Pode excluir discos de replicação.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-115">You can exclude disks from replication.</span></span> <span data-ttu-id="7d5fe-116">Por exemplo, poderá pretender que os discos de tooreplicate com dados temporários ou dados que foi atualizada sempre que uma máquina ou aplicação reinicia (por exemplo pagefile.sys ou tempdb do SQL Server).</span><span class="sxs-lookup"><span data-stu-id="7d5fe-116">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="7d5fe-117">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="7d5fe-117">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a><span data-ttu-id="7d5fe-118">Replicar VMs</span><span class="sxs-lookup"><span data-stu-id="7d5fe-118">Replicate VMs</span></span>

<span data-ttu-id="7d5fe-119">Antes de começar, veja uma rápida descrição geral do vídeo</span><span class="sxs-lookup"><span data-stu-id="7d5fe-119">Before you start, watch a quick video overview</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. <span data-ttu-id="7d5fe-120">Clique em **Passo 2: Replicar aplicação** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-120">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="7d5fe-121">No **origem**, selecione o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-121">In **Source**, select hello configuration server.</span></span>
3. <span data-ttu-id="7d5fe-122">No **máquina tipo**, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-122">In **Machine type**, select **Virtual Machines**.</span></span>
4. <span data-ttu-id="7d5fe-123">No **vCenter/vSphere hipervisor**, selecione o servidor vCenter Olá que gere anfitriões vSphere de Olá ou selecione Olá anfitrião.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-123">In **vCenter/vSphere Hypervisor**, select hello vCenter server that manages hello vSphere host, or select hello host.</span></span>
5. <span data-ttu-id="7d5fe-124">Selecione o servidor de processos de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-124">Select hello process server.</span></span> <span data-ttu-id="7d5fe-125">Se ainda não criou quaisquer servidores de processos adicionais este será o servidor de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-125">If you haven't created any additional process servers this will be hello configuration server.</span></span> <span data-ttu-id="7d5fe-126">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-126">Then click **OK**.</span></span>

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. <span data-ttu-id="7d5fe-128">No **destino**, selecione a subscrição de Olá e Olá o grupo de recursos em que pretende Olá toocreate pós-falha nas VMs.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-128">In **Target**, select hello subscription and hello resource group in which you want toocreate hello failed over VMs.</span></span> <span data-ttu-id="7d5fe-129">Escolha o modelo de implementação de Olá que pretende toouse no Azure (clássica ou recurso management), para Olá pós-falha nas VMs.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-129">Choose hello deployment model that you want toouse in Azure (classic or resource management), for hello failed over VMs.</span></span>


7. <span data-ttu-id="7d5fe-130">Selecione a conta de armazenamento do Azure de Olá que pretende toouse para replicar os dados.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-130">Select hello Azure storage account you want toouse for replicating data.</span></span> <span data-ttu-id="7d5fe-131">Se não quiser toouse uma conta que já configurou, pode criar um novo.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-131">If you don't want toouse an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="7d5fe-132">Selecione Olá Azure toowhich de rede e sub-rede VMs do Azure irá ligar, quando são criados após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-132">Select hello Azure network and subnet toowhich Azure VMs will connect, when they're created after failover.</span></span> <span data-ttu-id="7d5fe-133">Selecione **configurar agora para as máquinas selecionadas**, tooapply Olá rede definição tooall máquinas selecionadas para proteção.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-133">Select **Configure now for selected machines**, tooapply hello network setting tooall machines you select for protection.</span></span> <span data-ttu-id="7d5fe-134">Selecione **configurar mais tarde** tooselect Olá rede do Azure por máquina.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-134">Select **Configure later** tooselect hello Azure network per machine.</span></span> <span data-ttu-id="7d5fe-135">Se não quiser toouse uma rede existente, pode criar uma.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-135">If you don't want toouse an existing network, you can create one.</span></span>

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. <span data-ttu-id="7d5fe-137">No **máquinas virtuais** > **selecionar máquinas virtuais**, clique e selecione cada máquina que quiser tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-137">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="7d5fe-138">Só pode selecionar máquinas para as quais a replicação pode ser ativada.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-138">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="7d5fe-139">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-139">Then click **OK**.</span></span>

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. <span data-ttu-id="7d5fe-141">No **propriedades** > **configurar propriedades**, selecione conta Olá que será utilizada pelo tooautomatically de servidor de processo Olá instalar o serviço de mobilidade Olá na máquina de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-141">In **Properties** > **Configure properties**, select hello account that will be used by hello process server tooautomatically install hello Mobility service on hello machine.</span></span>
11. <span data-ttu-id="7d5fe-142">Por predefinição, todos os discos são replicados.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-142">By default all disks are replicated.</span></span> <span data-ttu-id="7d5fe-143">Clique em **todos os discos** e desmarque todos os discos que não pretende tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-143">Click **All Disks** and clear any disks you don't want tooreplicate.</span></span> <span data-ttu-id="7d5fe-144">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-144">Then click **OK**.</span></span> <span data-ttu-id="7d5fe-145">Pode definir propriedades VM adicionais mais tarde.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-145">You can set additional VM properties later.</span></span>

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="7d5fe-147">No **as definições de replicação** > **configurar as definições de replicação**, certifique-se de que Olá correta está selecionada a política de replicação.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-147">In **Replication settings** > **Configure replication settings**, verify that hello correct replication policy is selected.</span></span> <span data-ttu-id="7d5fe-148">Se modificar uma política, as alterações serão aplicadas tooreplicating máquina e toonew máquinas.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-148">If you modify a policy, changes will be applied tooreplicating machine, and toonew machines.</span></span>
12. <span data-ttu-id="7d5fe-149">Ativar **a consistência Multi VM** se pretender toogather máquinas para um grupo de replicação e especificar um nome para o grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-149">Enable **Multi-VM consistency** if you want toogather machines into a replication group, and specify a name for hello group.</span></span> <span data-ttu-id="7d5fe-150">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-150">Then click **OK**.</span></span> <span data-ttu-id="7d5fe-151">Tenha em atenção que:</span><span class="sxs-lookup"><span data-stu-id="7d5fe-151">Note that:</span></span>

    * <span data-ttu-id="7d5fe-152">Computadores em grupos de replicação replicar em conjunto e tem partilhado pontos de recuperação consistentes com falhas e consistentes da aplicação quando efetuar a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-152">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="7d5fe-153">Recomendamos que pode reunir VMs e servidores físicos, para que estes espelhar as cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-153">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="7d5fe-154">Ativar a consistência de várias VMS pode afetar o desempenho da carga de trabalho e só deve ser utilizada se máquinas estiverem a executar Olá mesma carga de trabalho e necessitar de consistência.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-154">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running hello same workload and you need consistency.</span></span>

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. <span data-ttu-id="7d5fe-156">Clique em **ativar a replicação**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-156">Click **Enable Replication**.</span></span> <span data-ttu-id="7d5fe-157">Pode controlar o progresso de Olá **ativar proteção** da tarefa no **definições** > **tarefas** > **tarefas de recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-157">You can track progress of hello **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="7d5fe-158">Depois de Olá **finalizar proteção** tarefa executa máquina Olá está preparada para ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="7d5fe-158">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d5fe-159">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7d5fe-159">Next steps</span></span>

<span data-ttu-id="7d5fe-160">Aceda demasiado[passo 12: executar uma ativação pós-falha de teste](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="7d5fe-160">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
