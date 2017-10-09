---
title: "Replicar VMs do Azure entre regiões do Azure para recuperação após desastre tem: tooAzure do Azure | Microsoft Docs"
description: "Resume os passos de Olá precisa de VMs do Azure tooreplicate entre regiões do Azure (Azure para o Azure) com o serviço do Azure Site Recovery Olá para as necessidades de recuperação após desastre."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="f586d-103">Replicar VMs do Azure entre regiões com o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f586d-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="f586d-104">Azure Site Recovery replicação para máquinas de virtuais (VMs) do Azure está atualmente em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="f586d-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="f586d-105">Este artigo descreve como tooreplicate VMs do Azure entre regiões do Azure utilizando Olá [recuperação de Site](site-recovery-overview.md) serviço no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f586d-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="f586d-106">Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum do Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f586d-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="f586d-107">Recuperação após desastre no Azure</span><span class="sxs-lookup"><span data-stu-id="f586d-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="f586d-108">Funcionalidades e capacidades de infraestrutura do Azure incorporada contribuem tooa estratégia de disponibilidade robusto e resiliente para cargas de trabalho que são executados em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f586d-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="f586d-109">No entanto, existem muitos motivos por que motivo precisa tooplan para recuperação após desastre entre regiões do Azure por si:</span><span class="sxs-lookup"><span data-stu-id="f586d-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="f586d-110">Terá das diretrizes de conformidade toomeet para aplicações específicas e cargas de trabalho que requerem uma continuidade do negócio e a estratégia de recuperação (BCDR) de desastre.</span><span class="sxs-lookup"><span data-stu-id="f586d-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="f586d-111">Pretende Olá capacidade tooprotect e recuperar as VMs do Azure com base nas suas decisões de negócio e não apenas com base na funcionalidade do Azure integrada.</span><span class="sxs-lookup"><span data-stu-id="f586d-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="f586d-112">Terá de tootest de ativação pós-falha e recuperação de acordo com as suas necessidades comerciais e de conformidade, sem afetar a produção.</span><span class="sxs-lookup"><span data-stu-id="f586d-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="f586d-113">Tem de toofail através de região de recuperação toohello no evento Olá de um desastre e falhar back toohello região de origem original de forma totalmente integrada.</span><span class="sxs-lookup"><span data-stu-id="f586d-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="f586d-114">Utilizar a recuperação de Site para a VM do Azure para o Azure replicação toohelp fizer todas estas tarefas.</span><span class="sxs-lookup"><span data-stu-id="f586d-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="f586d-115">Por que utilizar a Recuperação de Sites?</span><span class="sxs-lookup"><span data-stu-id="f586d-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="f586d-116">Recuperação de sites fornece uma forma simples tooreplicate VMs do Azure entre regiões:</span><span class="sxs-lookup"><span data-stu-id="f586d-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="f586d-117">**Implementação automática**.</span><span class="sxs-lookup"><span data-stu-id="f586d-117">**Automatic deployment**.</span></span> <span data-ttu-id="f586d-118">Ao contrário de um modelo de replicação ativo-ativo, não é necessário para uma infraestrutura dispendiosas e complexa na região secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="f586d-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="f586d-119">Ao ativar a replicação, a recuperação de sites cria automaticamente recursos Olá necessária na região de destino Olá, com base nas definições de região de origem.</span><span class="sxs-lookup"><span data-stu-id="f586d-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="f586d-120">**Controlar regiões**.</span><span class="sxs-lookup"><span data-stu-id="f586d-120">**Control regions**.</span></span> <span data-ttu-id="f586d-121">Com a recuperação de Site, pode replicar a partir de qualquer região de tooany região dentro de um continente.</span><span class="sxs-lookup"><span data-stu-id="f586d-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="f586d-122">Compare-as com o armazenamento georredundante de acesso de leitura, o que replica de forma assíncrona entre padrão [emparelhado regiões](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) apenas.</span><span class="sxs-lookup"><span data-stu-id="f586d-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="f586d-123">Armazenamento georredundante com acesso de leitura fornece dados de toohello acesso só de leitura na região de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="f586d-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="f586d-124">**Automatizada replicação**.</span><span class="sxs-lookup"><span data-stu-id="f586d-124">**Automated replication**.</span></span> <span data-ttu-id="f586d-125">Recuperação de sites fornece automatizada replicação contínua.</span><span class="sxs-lookup"><span data-stu-id="f586d-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="f586d-126">Ativação pós-falha e a reativação pós-falha podem ser acionadas com um único clique.</span><span class="sxs-lookup"><span data-stu-id="f586d-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="f586d-127">**RTO e RPO**.</span><span class="sxs-lookup"><span data-stu-id="f586d-127">**RTO and RPO**.</span></span> <span data-ttu-id="f586d-128">Recuperação de site tira partido da infraestrutura de rede do Azure de Olá que liga regiões tookeep RTO e RPO muito baixo.</span><span class="sxs-lookup"><span data-stu-id="f586d-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="f586d-129">**Testar**.</span><span class="sxs-lookup"><span data-stu-id="f586d-129">**Testing**.</span></span> <span data-ttu-id="f586d-130">Pode executar simulações de recuperação após desastre com as ativações pós-falha de teste a pedido, como e quando for necessárias, sem afetar as cargas de trabalho de produção ou a replicação em curso.</span><span class="sxs-lookup"><span data-stu-id="f586d-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="f586d-131">**Planos de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="f586d-131">**Recovery plans**.</span></span> <span data-ttu-id="f586d-132">Pode utilizar a ativação pós-falha de tooorchestrate de planos de recuperação e a reativação pós-falha da aplicação todo Olá em execução em várias VMs.</span><span class="sxs-lookup"><span data-stu-id="f586d-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="f586d-133">funcionalidade de plano de recuperação Olá tem integração de primeira classe avançada com runbooks de automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="f586d-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="f586d-134">Resumo de implementação</span><span class="sxs-lookup"><span data-stu-id="f586d-134">Deployment summary</span></span>

<span data-ttu-id="f586d-135">Eis um resumo de que precisa toodo tooset a replicação de VMs entre regiões do Azure:</span><span class="sxs-lookup"><span data-stu-id="f586d-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="f586d-136">Crie um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="f586d-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="f586d-137">cofre Olá contém definições de configuração e orquestra a replicação.</span><span class="sxs-lookup"><span data-stu-id="f586d-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="f586d-138">Ative a replicação para Olá VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f586d-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="f586d-139">Execute um toomake de ativação pós-falha de teste se tudo está a funcionar conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="f586d-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="f586d-140">Pode verificar Olá [matriz de suporte para a replicação de VM do Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f586d-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="f586d-141">Para obter informações sobre como o tooconfigure Olá necessárias conectividade de saída de rede para as VMs do Azure para replicação de recuperação de sites, consulte Olá [rede documento de orientação](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="f586d-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="f586d-142">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f586d-142">Before you start</span></span>

* <span data-ttu-id="f586d-143">A conta de utilizador do Azure tem toohave determinadas [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable a replicação da máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="f586d-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="f586d-144">A subscrição do Azure deve estar ativada toocreate VMs na localização de destino Olá que pretende que o toouse como região de recuperação de desastre Olá.</span><span class="sxs-lookup"><span data-stu-id="f586d-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="f586d-145">Contacte o suporte tooenable Olá necessário quota.</span><span class="sxs-lookup"><span data-stu-id="f586d-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f586d-146">Criar um cofre dos Serviços de Recuperação </span><span class="sxs-lookup"><span data-stu-id="f586d-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="f586d-147">Recomendamos que crie o Cofre de serviços de recuperação de Olá na localização de olá onde pretende que o seu tooreplicate VMs.</span><span class="sxs-lookup"><span data-stu-id="f586d-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="f586d-148">Por exemplo, se a localização de destino é hello centro dos EUA, criar cofre Olá **EUA Central**.</span><span class="sxs-lookup"><span data-stu-id="f586d-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="f586d-149">Ativar a replicação</span><span class="sxs-lookup"><span data-stu-id="f586d-149">Enable replication</span></span>

<span data-ttu-id="f586d-150">No **cofres dos serviços de recuperação**, clique em nome do cofre Olá.</span><span class="sxs-lookup"><span data-stu-id="f586d-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="f586d-151">No Cofre de Olá, clique em Olá **+ replicar** botão.</span><span class="sxs-lookup"><span data-stu-id="f586d-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="f586d-152">Passo 1.</span><span class="sxs-lookup"><span data-stu-id="f586d-152">Step 1.</span></span> <span data-ttu-id="f586d-153">Configurar a origem de Olá</span><span class="sxs-lookup"><span data-stu-id="f586d-153">Configure hello source</span></span>
1. <span data-ttu-id="f586d-154">No **origem**, selecione **Azure - pré-visualização**.</span><span class="sxs-lookup"><span data-stu-id="f586d-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="f586d-155">No **localização de origem**, selecione a origem de Olá região do Azure onde as VMs estão a ser executados.</span><span class="sxs-lookup"><span data-stu-id="f586d-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="f586d-156">Modelo de implementação de Olá selecione das suas VMs: **Resource Manager** ou **clássico**.</span><span class="sxs-lookup"><span data-stu-id="f586d-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="f586d-157">Selecione Olá **grupo de recursos de origem** para as VMs do Gestor de recursos ou **serviço em nuvem** para VMs clássicas.</span><span class="sxs-lookup"><span data-stu-id="f586d-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Configurar a origem de Olá](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="f586d-159">Passo 2.</span><span class="sxs-lookup"><span data-stu-id="f586d-159">Step 2.</span></span> <span data-ttu-id="f586d-160">Selecione as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f586d-160">Select virtual machines</span></span>

* <span data-ttu-id="f586d-161">Selecione Olá VMs que pretende tooreplicate e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f586d-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![Selecione as VMs](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="f586d-163">Passo 3.</span><span class="sxs-lookup"><span data-stu-id="f586d-163">Step 3.</span></span> <span data-ttu-id="f586d-164">Configurar definições</span><span class="sxs-lookup"><span data-stu-id="f586d-164">Configure settings</span></span>

1. <span data-ttu-id="f586d-165">predefinição de Olá toooverride as definições de destino e especifique as definições de Olá à sua escolha, clique em **personalizar**.</span><span class="sxs-lookup"><span data-stu-id="f586d-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="f586d-166">Para obter mais informações, consulte [Personalizar recursos de destino](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="f586d-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Configurar definições](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="f586d-168">Por predefinição, a recuperação de sites cria uma política de replicação que tem instantâneos consistentes com aplicação todas as 4 horas e mantém pontos de recuperação durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="f586d-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="f586d-169">toocreate uma política com diferentes definições, clique em **personalizar** seguinte demasiado**política de replicação**.</span><span class="sxs-lookup"><span data-stu-id="f586d-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![Personalizar a política](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="f586d-171">toostart aprovisionamento Olá recursos do destino, clique em **criar recursos de destino**.</span><span class="sxs-lookup"><span data-stu-id="f586d-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="f586d-172">Aprovisionamento leva um minuto ou.</span><span class="sxs-lookup"><span data-stu-id="f586d-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="f586d-173">Não feche o painel de Olá durante o aprovisionamento ou precisar de toostart sobre.</span><span class="sxs-lookup"><span data-stu-id="f586d-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="f586d-174">replicação tootrigger de Olá selecionada VM, clique em **ativar a replicação**.</span><span class="sxs-lookup"><span data-stu-id="f586d-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="f586d-175">Pode controlar o progresso de Olá **ativar a proteção** da tarefa no **definições** > **tarefas** > **tarefas de recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="f586d-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="f586d-176">No **definições** > **itens replicados**, pode ver o estado de Olá de VMs e Olá progresso da replicação inicial.</span><span class="sxs-lookup"><span data-stu-id="f586d-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="f586d-177">Clique em Olá VM toodrill para baixo para as respetivas definições.</span><span class="sxs-lookup"><span data-stu-id="f586d-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="f586d-178">Executar uma ativação pós-falha de teste</span><span class="sxs-lookup"><span data-stu-id="f586d-178">Run a test failover</span></span>

<span data-ttu-id="f586d-179">Depois de configurar tudo, execute um toomake de ativação pós-falha de teste se tudo está a funcionar conforme esperado:</span><span class="sxs-lookup"><span data-stu-id="f586d-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="f586d-180">toofail através de uma única máquina no **definições** > **itens replicados**, clique em Olá VM **+ ativação pós-falha de teste** ícone.</span><span class="sxs-lookup"><span data-stu-id="f586d-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="f586d-181">Planear toofail através de uma recuperação, na **definições** > **planos de recuperação**, plano do contexto Olá **ativação pós-falha de teste**.</span><span class="sxs-lookup"><span data-stu-id="f586d-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="f586d-182">toocreate um plano de recuperação, [siga estas instruções](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="f586d-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="f586d-183">No **ativação pós-falha de teste**, selecione toowhich de rede virtual do Azure de destino Olá VMs do Azure estão ligadas após a ocorrência da ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="f586d-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="f586d-184">toostart Olá ativação pós-falha, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f586d-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="f586d-185">tootrack progresso, clique em Olá VM tooopen as respetivas propriedades.</span><span class="sxs-lookup"><span data-stu-id="f586d-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="f586d-186">Ou pode clicar em Olá **ativação pós-falha de teste** tarefa no nome do cofre Olá > **definições** > **tarefas** > **astarefasderecuperaçãodesites**.</span><span class="sxs-lookup"><span data-stu-id="f586d-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="f586d-187">Depois de Olá conclusão ativação pós-falha, réplica Olá máquina do Azure é apresentado no portal do Azure de Olá > **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="f586d-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="f586d-188">Certifique-se que Olá VM Olá um tamanho adequado, que tenha ligado toohello adequada de rede, e que está em execução.</span><span class="sxs-lookup"><span data-stu-id="f586d-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="f586d-189">Olá toodelete VMs que foram criados durante a ativação pós-falha de teste de Olá, clique em **ativação pós-falha de teste de limpeza** em Olá replicadas item ou Olá plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="f586d-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="f586d-190">No **notas**, registar e guardar todas as observações associadas à ativação pós-falha de teste de Olá.</span><span class="sxs-lookup"><span data-stu-id="f586d-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="f586d-191">[Saiba mais](site-recovery-test-failover-to-azure.md) sobre as ativações pós-falha de teste.</span><span class="sxs-lookup"><span data-stu-id="f586d-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f586d-192">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f586d-192">Next steps</span></span>

<span data-ttu-id="f586d-193">Depois de testar a implementação de Olá:</span><span class="sxs-lookup"><span data-stu-id="f586d-193">After you test hello deployment:</span></span>

- <span data-ttu-id="f586d-194">[Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de ativações pós-falha e como toorun-los.</span><span class="sxs-lookup"><span data-stu-id="f586d-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="f586d-195">Saiba mais sobre [planos de recuperação a utilizar](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="f586d-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
