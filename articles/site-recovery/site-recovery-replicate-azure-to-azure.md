---
title: "aplicações de aaaReplicate (tooAzure do Azure) | Microsoft Docs"
description: "Este artigo descreve como tooset a replicação de virtual máquinas em execução na região do Azure um demasiado noutra região no Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="bd18d-103">Replicar máquinas virtuais do Azure tooanother região do Azure</span><span class="sxs-lookup"><span data-stu-id="bd18d-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="bd18d-104">Replicação de recuperação de site para máquinas virtuais do Azure está atualmente em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="bd18d-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="bd18d-105">Este artigo descreve como tooset a replicação de virtual máquinas em execução numa região do Azure tooanother região do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd18d-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd18d-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bd18d-106">Prerequisites</span></span>

* <span data-ttu-id="bd18d-107">artigo de Olá pressupõe que já sabe sobre recuperação de Site e o Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="bd18d-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="bd18d-108">É necessário toohave um pre 'Cofre dos serviços de recuperação' criado.</span><span class="sxs-lookup"><span data-stu-id="bd18d-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="bd18d-109">Recomenda-se que crie Olá "Cofre dos serviços de recuperação" na localização de olá onde pretende que o seu tooreplicate VMs.</span><span class="sxs-lookup"><span data-stu-id="bd18d-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="bd18d-110">Por exemplo, se a localização de destino "E.U.A. Central", crie o Cofre "E.U.A. Central".</span><span class="sxs-lookup"><span data-stu-id="bd18d-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="bd18d-111">Se estiver a utilizar as regras de grupos de segurança de rede (NSG) ou firewall proxy toocontrol acesso toooutbound a conectividade à internet no Olá VMs do Azure, certifique-se de que Olá de lista branca necessários URLs ou IPs.</span><span class="sxs-lookup"><span data-stu-id="bd18d-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="bd18d-112">Consulte demasiado[documento de orientação do funcionamento em rede](./site-recovery-azure-to-azure-networking-guidance.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="bd18d-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="bd18d-113">Se tiver o ExpressRoute ou de uma ligação VPN entre no local e Olá da origem de localização no Azure, siga [considerações de recuperação de Site para o local tooon Azure ExpressRoute / configuração de VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) documento.</span><span class="sxs-lookup"><span data-stu-id="bd18d-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="bd18d-114">A conta de utilizador do Azure tem toohave determinadas [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable a replicação da máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd18d-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="bd18d-115">A subscrição do Azure deve estar ativada toocreate VMs na localização de destino Olá pretende toouse como região DR.</span><span class="sxs-lookup"><span data-stu-id="bd18d-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="bd18d-116">Pode contactar o suporte tooenable Olá necessário quota.</span><span class="sxs-lookup"><span data-stu-id="bd18d-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="bd18d-117">Ative a replicação do cofre do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="bd18d-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="bd18d-118">Nesta ilustração, iremos irá replicar as VMs em execução no toohello de localização do Azure Olá 'Oriental' Localização ' Sudeste Asiático '.</span><span class="sxs-lookup"><span data-stu-id="bd18d-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="bd18d-119">passos de Olá são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="bd18d-119">hello steps are as follows:</span></span>

 <span data-ttu-id="bd18d-120">Clique em **+ replicar** na replicação de tooenable Olá cofre para máquinas de virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="bd18d-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="bd18d-121">**Origem:** refere-se toohello ponto de origem das máquinas de Olá que neste caso é **Azure**.</span><span class="sxs-lookup"><span data-stu-id="bd18d-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="bd18d-122">**Localização de origem:** é Olá região do Azure a partir de onde pretende tooprotect as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="bd18d-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="bd18d-123">Nesta ilustração, a localização de origem Olá será 'Oriental'</span><span class="sxs-lookup"><span data-stu-id="bd18d-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="bd18d-124">**Modelo de implementação:** refere-se modelo de implementação do Azure toohello das máquinas de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="bd18d-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="bd18d-125">Pode selecionar qualquer uma das clássico ou do resource manager e as máquinas que pertençam modelo específico toohello serão apresentadas para proteção no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="bd18d-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="bd18d-126">Apenas pode replicar uma máquina virtual clássica e recuperá-la como uma máquina virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="bd18d-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="bd18d-127">Não é possível recuperá-la como uma máquina virtual do Gestor de recursos.</span><span class="sxs-lookup"><span data-stu-id="bd18d-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="bd18d-128">**Grupo de recursos:** -lo do toowhich de grupo de recursos de Olá as máquinas virtuais de origem pertence.</span><span class="sxs-lookup"><span data-stu-id="bd18d-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="bd18d-129">Olá todas as VMs no grupo de recursos selecionado Olá serão apresentados para proteção no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="bd18d-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![Ativar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="bd18d-131">No **máquinas virtuais > Selecione as máquinas virtuais**, clique e selecione cada máquina que quiser tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="bd18d-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="bd18d-132">Só pode selecionar máquinas para as quais a replicação pode ser ativada.</span><span class="sxs-lookup"><span data-stu-id="bd18d-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="bd18d-133">Em seguida, clique em OK.</span><span class="sxs-lookup"><span data-stu-id="bd18d-133">Then click OK.</span></span>
    <span data-ttu-id="bd18d-134">![Ativar replicação](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="bd18d-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="bd18d-135">Na secção de definições pode configurar as propriedades do site de destino</span><span class="sxs-lookup"><span data-stu-id="bd18d-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="bd18d-136">**Localização de destino:** esta é a localização de olá onde os dados de máquina virtual de origem serão replicados.</span><span class="sxs-lookup"><span data-stu-id="bd18d-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="bd18d-137">Consoante a sua localização máquinas selecionadas, a recuperação de sites irá fornecer que Olá lista de regiões de destino adequado.</span><span class="sxs-lookup"><span data-stu-id="bd18d-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="bd18d-138">Recomenda-se localização de destino tookeep mesmo a partir da recuperação do seu Cofre de serviços.</span><span class="sxs-lookup"><span data-stu-id="bd18d-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="bd18d-139">**Grupo de recursos de destino:** é toowhich de grupo de recursos de Olá irão pertencer todas as suas máquinas virtuais replicadas. Por predefinição a ASR irá criar um novo grupo de recursos na região de destino Olá com um nome que o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="bd18d-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="bd18d-140">No caso de grupo de recursos criado pelo ASR já existir, será reutilizada. Também pode escolher toocustomize-lo tal como mostrado na secção de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="bd18d-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="bd18d-141">**Rede Virtual de destino:** por predefinição, a ASR irá criar uma nova rede virtual numa região de destino Olá com um nome que o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="bd18d-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="bd18d-142">Isto será mapeada tooyour rede de origem e será utilizado para qualquer proteção futura.</span><span class="sxs-lookup"><span data-stu-id="bd18d-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd18d-143">[Verifique os detalhes de rede](site-recovery-network-mapping-azure-to-azure.md) tooknow mais sobre o mapeamento da rede.</span><span class="sxs-lookup"><span data-stu-id="bd18d-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="bd18d-144">**As contas de armazenamento de destino:** por predefinição, a ASR irá criar Olá novo destino conta de armazenamento mimicking a configuração de armazenamento VM de origem.</span><span class="sxs-lookup"><span data-stu-id="bd18d-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="bd18d-145">No caso de conta de armazenamento criada por ASR já existir, será reutilizada.</span><span class="sxs-lookup"><span data-stu-id="bd18d-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="bd18d-146">**As contas de armazenamento em cache:** ASR tem chamou o armazenamento de cache na região de origem Olá de conta de armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="bd18d-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="bd18d-147">Olá todas as alterações a acontecer no Olá VMs de origem são controladas e enviadas toocache conta de armazenamento antes de localização de destino esses toohello a replicar.</span><span class="sxs-lookup"><span data-stu-id="bd18d-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="bd18d-148">**Conjunto de disponibilidade:** por predefinição, a ASR irá criar uma novo conjunto de disponibilidade na região de destino Olá com um nome que o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="bd18d-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="bd18d-149">No caso de conjunto de disponibilidade criado pelo ASR já existir, será reutilizada.</span><span class="sxs-lookup"><span data-stu-id="bd18d-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="bd18d-150">**Política de replicação:** define Olá as definições de recuperação ponto retenção histórico e aplicação consistente frequência de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="bd18d-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="bd18d-151">Por predefinição, a ASR irá criar uma nova política de replicação com as predefinições dos ' 24 horas para retenção do ponto de recuperação e ' 60 minutos para a frequência de instantâneos consistentes da aplicação.</span><span class="sxs-lookup"><span data-stu-id="bd18d-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Ativar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="bd18d-153">Personalizar a recursos de destino</span><span class="sxs-lookup"><span data-stu-id="bd18d-153">Customize target resources</span></span>

<span data-ttu-id="bd18d-154">No caso de pretender que as predefinições de Olá toochange utilizadas pelo ASR, pode alterar as definições de Olá com base nas suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="bd18d-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="bd18d-155">**Personalizar:** clique nele toochange Olá as predefinições utilizadas por ASR.</span><span class="sxs-lookup"><span data-stu-id="bd18d-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="bd18d-156">**Grupo de recursos de destino:** pode selecionar o grupo de recursos de Olá na lista de todos os grupos de recursos de Olá existente na localização de destino Olá numa subscrição Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="bd18d-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="bd18d-157">**Rede Virtual de destino:** pode encontrar a lista de Olá de rede virtual de Olá todos os na localização de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="bd18d-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="bd18d-158">**Conjunto de disponibilidade:** só é possível adicionar a disponibilidade conjuntos definições toohello máquinas virtuais que fazem parte de disponibilidade na região de origem.</span><span class="sxs-lookup"><span data-stu-id="bd18d-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="bd18d-159">**Contas de armazenamento de destino:**</span><span class="sxs-lookup"><span data-stu-id="bd18d-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="bd18d-160">![Ativar a replicação](./media/site-recovery-replicate-azure-to-azure/customize.PNG) clique em **criar o recurso de destino** e ativar a replicação</span><span class="sxs-lookup"><span data-stu-id="bd18d-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="bd18d-161">Depois de máquinas virtuais estão protegidas pode verificar o estado de Olá do Estado de funcionamento de VMs em **replicado itens**</span><span class="sxs-lookup"><span data-stu-id="bd18d-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="bd18d-162">Durante a Olá o momento da replicação inicial existe foi uma possibilidade que estado demora tempo toorefresh e não consegue ver o progresso durante algum tempo.</span><span class="sxs-lookup"><span data-stu-id="bd18d-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="bd18d-163">Pode clicar no botão Atualizar Olá na parte superior de Olá de estado mais recente do Olá painel tooget Olá.</span><span class="sxs-lookup"><span data-stu-id="bd18d-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![Ativar a replicação](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="bd18d-165">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bd18d-165">Next steps</span></span>
- <span data-ttu-id="bd18d-166">[Saiba mais](site-recovery-test-failover-to-azure.md) sobre como executar uma ativação pós-falha de teste.</span><span class="sxs-lookup"><span data-stu-id="bd18d-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="bd18d-167">[Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de ativações pós-falha e como toorun-los.</span><span class="sxs-lookup"><span data-stu-id="bd18d-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="bd18d-168">Saiba mais sobre [planos de recuperação a utilizar](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="bd18d-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="bd18d-169">Saiba mais sobre [trocar as VMs do Azure](site-recovery-how-to-reprotect.md) após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="bd18d-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
