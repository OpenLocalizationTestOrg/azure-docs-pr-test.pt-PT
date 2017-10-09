---
title: "máquinas virtuais aaaReplicate Hyper-V em nuvens VMM utilizando o Azure Site Recovery e o PowerShell (Resource Manager) | Microsoft Docs"
description: "Replicar máquinas virtuais de Hyper-V em nuvens VMM utilizando o Azure Site Recovery e o PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="a444a-103">Replicar máquinas virtuais de Hyper-V no VMM nuvens tooAzure com o PowerShell e do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a444a-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a444a-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a444a-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="a444a-105">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a444a-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="a444a-106">Portal Clássico</span><span class="sxs-lookup"><span data-stu-id="a444a-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="a444a-107">PowerShell – Clássica</span><span class="sxs-lookup"><span data-stu-id="a444a-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="a444a-108">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="a444a-108">Overview</span></span>
<span data-ttu-id="a444a-109">O Azure Site Recovery contribui tooyour negócio continuidade e desastre (BCDR) estratégia de recuperação através da orquestração da replicação, ativação pós-falha e recuperação de máquinas virtuais num número de cenários de implementação.</span><span class="sxs-lookup"><span data-stu-id="a444a-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="a444a-110">Para obter uma lista completa de implementação cenários Consulte Olá [descrição geral do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a444a-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="a444a-111">Este artigo mostra como tarefas comuns do toouse PowerShell tooautomate precisa tooperform quando configurar máquinas virtuais de Hyper-V de tooreplicate do Azure Site Recovery no armazenamento de tooAzure de nuvens VMM do System Center.</span><span class="sxs-lookup"><span data-stu-id="a444a-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="a444a-112">Olá artigo inclui os pré-requisitos para o cenário de Olá e mostra-lhe</span><span class="sxs-lookup"><span data-stu-id="a444a-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="a444a-113">Como tooset configurar um cofre dos serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="a444a-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="a444a-114">Instalar Olá fornecedor do Azure Site Recovery no servidor do VMM de origem de Olá</span><span class="sxs-lookup"><span data-stu-id="a444a-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="a444a-115">Registar o servidor de Olá no Cofre de Olá, adicione uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a444a-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="a444a-116">Instalar o agente de Azure Recovery Services Olá nos servidores de anfitrião do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="a444a-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="a444a-117">Configurar definições de proteção de nuvens do VMM, que serão aplicados tooall protegida máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="a444a-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="a444a-118">Ative a proteção para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a444a-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="a444a-119">Teste Olá toomake de ativação pós-falha se que tudo está a funcionar conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="a444a-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="a444a-120">Caso se depare com problemas de configuração neste cenário, publique as suas perguntas nos Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a444a-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="a444a-121">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a444a-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a444a-122">Este artigo abrange utilizando o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="a444a-123">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a444a-123">Before you start</span></span>
<span data-ttu-id="a444a-124">Certifique-se de que tem os pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="a444a-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="a444a-125">Pré-requisitos do Azure</span><span class="sxs-lookup"><span data-stu-id="a444a-125">Azure prerequisites</span></span>
* <span data-ttu-id="a444a-126">Precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a444a-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="a444a-127">Se não tiver uma, comece por um [conta gratuita](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="a444a-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="a444a-128">Além disso, pode ler sobre Olá [preços do Microsoft Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="a444a-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="a444a-129">Irá precisar de uma subscrição do CSP se estiver a tentar terminar o cenário de subscrição do Olá replicação tooa CSP.</span><span class="sxs-lookup"><span data-stu-id="a444a-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="a444a-130">Saiba mais sobre o programa CSP Olá no [como tooenroll no programa CSP Olá](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="a444a-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="a444a-131">Irá precisar de um tooAzure de dados replicados toostore de conta de armazenamento (Resource Manager) de v2 do Azure.</span><span class="sxs-lookup"><span data-stu-id="a444a-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="a444a-132">conta de Olá tem georreplicação ativada.</span><span class="sxs-lookup"><span data-stu-id="a444a-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="a444a-133">Deve estar no Olá mesma região que Olá serviço Azure Site Recovery e estar associado a Olá mesma subscrição ou na subscrição do CSP Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="a444a-134">toolearn mais informações sobre como configurar o armazenamento do Azure, consulte Olá [introdução tooMicrosoft Storage do Azure](../storage/common/storage-introduction.md) para referência.</span><span class="sxs-lookup"><span data-stu-id="a444a-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="a444a-135">Terá de certificar-se de que as máquinas virtuais que pretende tooprotect cumprir Olá toomake [pré-requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="a444a-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="a444a-136">Atualmente, apenas operações ao nível de VM são possíveis através do Powershell.</span><span class="sxs-lookup"><span data-stu-id="a444a-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="a444a-137">Suporte para operações de nível de plano de recuperação será feito em breve.</span><span class="sxs-lookup"><span data-stu-id="a444a-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="a444a-138">Por agora, está limitado tooperforming ativações pós-falha de datacenters apenas granularidade 'protected VM' e não um nível plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="a444a-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="a444a-139">Pré-requisitos do VMM</span><span class="sxs-lookup"><span data-stu-id="a444a-139">VMM prerequisites</span></span>
* <span data-ttu-id="a444a-140">Irá precisar de servidor do VMM em execução no System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="a444a-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="a444a-141">Nenhum servidor VMM que contêm máquinas virtuais que pretende tooprotect tem de estar em execução Olá Azure Site Recovery Provider.</span><span class="sxs-lookup"><span data-stu-id="a444a-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="a444a-142">Este é instalado durante Olá implementação do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a444a-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="a444a-143">Irá precisar de pelo menos uma nuvem no Olá pretende tooprotect de servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="a444a-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="a444a-144">Olá nuvem deve conter:</span><span class="sxs-lookup"><span data-stu-id="a444a-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="a444a-145">Um ou mais grupos de anfitriões VMM.</span><span class="sxs-lookup"><span data-stu-id="a444a-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="a444a-146">Um ou mais servidores anfitrião Hyper-V ou clusters em cada grupo anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a444a-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="a444a-147">Um ou mais máquinas virtuais no servidor de Hyper-V de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="a444a-148">Saiba mais sobre como configurar as nuvens do VMM:</span><span class="sxs-lookup"><span data-stu-id="a444a-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="a444a-149">Saiba mais sobre nuvens privadas do VMM no [Novidades na nuvem privada com o System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) e na [nuvens VMM 2012 e Olá](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="a444a-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="a444a-150">Saiba mais sobre [configurar Olá VMM recursos de infraestrutura de nuvem](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="a444a-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="a444a-151">Depois dos elementos de recursos de infraestrutura de nuvem estão assegurados saber sobre a criação de nuvens privadas em [criar uma nuvem privada no VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) e na [instruções: criar nuvens privadas com o VMM do System Center 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="a444a-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="a444a-152">Pré-requisitos do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="a444a-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="a444a-153">Olá servidores anfitrião Hyper-V tem de estar em execução, pelo menos, **Windows Server 2012** com a função Hyper-V ou **Microsoft Hyper-V Server 2012** e ter Olá atualizações mais recentes instaladas.</span><span class="sxs-lookup"><span data-stu-id="a444a-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="a444a-154">Se estiver a executar Hyper-V num cluster, tenha em atenção que o mediador de clusters não é criado automaticamente se tiver um cluster com base no endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="a444a-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="a444a-155">Terá de Mediador de clusters de Olá tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="a444a-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="a444a-156">Para</span><span class="sxs-lookup"><span data-stu-id="a444a-156">For</span></span>
* <span data-ttu-id="a444a-157">Para obter instruções, consulte [como tooConfigure Mediador de réplicas do Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="a444a-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="a444a-158">Qualquer servidor de anfitrião do Hyper-V ou cluster do qual pretende toomanage proteção têm de ser incluído numa nuvem VMM.</span><span class="sxs-lookup"><span data-stu-id="a444a-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="a444a-159">Pré-requisitos de mapeamento da rede</span><span class="sxs-lookup"><span data-stu-id="a444a-159">Network mapping prerequisites</span></span>
<span data-ttu-id="a444a-160">Quando protege máquinas virtuais no Azure, o mapeamento da rede Olá mapeia redes de máquinas virtuais de Olá no servidor do VMM de origem de Olá e seguinte de Olá de tooenable de redes do Azure de destino:</span><span class="sxs-lookup"><span data-stu-id="a444a-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="a444a-161">Todas as máquinas que efetuar a ativação pós-falha no Olá mesma rede pode ligar-se tooeach outro, independentemente do plano de recuperação onde se encontram no.</span><span class="sxs-lookup"><span data-stu-id="a444a-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="a444a-162">Se um gateway de rede está configurado na rede do Azure de destino de Olá, as máquinas virtuais podem ligar tooother máquinas virtuais no local.</span><span class="sxs-lookup"><span data-stu-id="a444a-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="a444a-163">Se não configurar o mapeamento da rede, Olá apenas máquinas virtuais com ativação pós-falha no Olá mesmo plano de recuperação será capaz de tooconnect tooeach outros após tooAzure de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="a444a-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="a444a-164">Se pretender que o mapeamento da rede toodeploy terá seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="a444a-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="a444a-165">máquinas virtuais Olá pretende tooprotect no servidor do VMM de origem de Olá deve ser ligado tooa rede VM.</span><span class="sxs-lookup"><span data-stu-id="a444a-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="a444a-166">Essa rede deve ser ligado tooa rede lógica que esteja associado Olá nuvem.</span><span class="sxs-lookup"><span data-stu-id="a444a-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="a444a-167">Máquinas virtuais toowhich replicado uma rede do Azure podem ligar após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="a444a-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="a444a-168">Selecionará esta rede momento Olá da ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="a444a-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="a444a-169">rede de Olá deve estar no Olá mesma região que a sua subscrição do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a444a-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="a444a-170">Saiba mais sobre o mapeamento da rede no</span><span class="sxs-lookup"><span data-stu-id="a444a-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="a444a-171">Como tooconfigure redes lógicas no VMM</span><span class="sxs-lookup"><span data-stu-id="a444a-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="a444a-172">Como tooconfigure VM redes e gateways no VMM</span><span class="sxs-lookup"><span data-stu-id="a444a-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="a444a-173">Como tooconfigure e monitorizar redes virtuais no Azure</span><span class="sxs-lookup"><span data-stu-id="a444a-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="a444a-174">Pré-requisitos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="a444a-174">PowerShell prerequisites</span></span>
<span data-ttu-id="a444a-175">Certifique-se de que tem toogo pronto do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a444a-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="a444a-176">Se já estiver a utilizar o PowerShell, terá de tooupgrade tooversion 0.8.10 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a444a-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="a444a-177">Para informações sobre como configurar o PowerShell, consulte Olá [orientar tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a444a-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a444a-178">Assim que tiver definido e configurado o PowerShell, pode ver todas Olá cmdlets disponíveis para o serviço de Olá [aqui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a444a-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="a444a-179">toolearn sobre sugestões que podem ajudar a utilizar os cmdlets de Olá, tais como a forma como os valores de parâmetros, entradas e saídas normalmente são processadas no Azure PowerShell, consulte Olá [guia tooget iniciado com Cmdlets do Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="a444a-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="a444a-180">Passo 1: Conjunto Olá subscrição</span><span class="sxs-lookup"><span data-stu-id="a444a-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="a444a-181">A partir do powershell do Azure, o início de sessão tooyour conta do Azure: Olá os seguintes cmdlets a utilizar</span><span class="sxs-lookup"><span data-stu-id="a444a-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="a444a-182">Obter uma lista das suas subscrições.</span><span class="sxs-lookup"><span data-stu-id="a444a-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="a444a-183">Isto também irá listar Olá subscriptionIDs para cada uma das subscrições de Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="a444a-184">Anotar Olá subscriptionID da subscrição Olá no qual pretende o Cofre de serviços de recuperação de Olá toocreate</span><span class="sxs-lookup"><span data-stu-id="a444a-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="a444a-185">Subscrição de Olá conjunto no qual Olá cofre dos serviços de recuperação é toobe criado pelo mentioning Olá ID de subscrição</span><span class="sxs-lookup"><span data-stu-id="a444a-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="a444a-186">Passo 2: crie um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="a444a-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="a444a-187">Criar um grupo de recursos no Gestor de recursos do Azure se ainda não tiver um</span><span class="sxs-lookup"><span data-stu-id="a444a-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="a444a-188">Crie um novo cofre de serviços de recuperação e guarde Olá criada o objeto de Cofre de ASR numa variável (serão utilizados mais tarde).</span><span class="sxs-lookup"><span data-stu-id="a444a-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="a444a-189">Também pode obter Olá ASR cofre após criar o objeto utilizando o cmdlet Get-AzureRMRecoveryServicesVault de Olá:-</span><span class="sxs-lookup"><span data-stu-id="a444a-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="a444a-190">Passo 3: Definir o contexto do Cofre de serviços de recuperação de Olá</span><span class="sxs-lookup"><span data-stu-id="a444a-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="a444a-191">Definir o contexto de cofre Olá executando Olá comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="a444a-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="a444a-192">Passo 4: Instalar Olá Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="a444a-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="a444a-193">Na máquina do VMM de Olá, crie um diretório, executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="a444a-194">Extraia os ficheiros de Olá utilizando o fornecedor de Olá transferido através da execução Olá comando a seguir</span><span class="sxs-lookup"><span data-stu-id="a444a-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="a444a-195">Instale o fornecedor de Olá utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-195">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="a444a-196">Aguarde Olá toofinish de instalação.</span><span class="sxs-lookup"><span data-stu-id="a444a-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="a444a-197">Registe o servidor de Olá no cofre Olá utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="a444a-198">Passo 5: Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a444a-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="a444a-199">Se não tiver uma conta de armazenamento do Azure, criar uma conta de georreplicação ativada na Olá mesma geografia que Olá cofre executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="a444a-200">Tenha em atenção que conta de armazenamento Olá tem de ser no Olá mesma região que o serviço do Azure Site Recovery Olá e associado Olá mesma subscrição.</span><span class="sxs-lookup"><span data-stu-id="a444a-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="a444a-201">Passo 6: Instalar Olá Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="a444a-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="a444a-202">Transferir o agente de serviços de recuperação do Azure Olá em [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) e instale-lo em cada servidor de anfitrião de Hyper-V localizado em Olá VMM nuvens pretende tooprotect.</span><span class="sxs-lookup"><span data-stu-id="a444a-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="a444a-203">Execute os seguintes comandos em todos os anfitriões VMM de Olá:</span><span class="sxs-lookup"><span data-stu-id="a444a-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="a444a-204">Passo 7: Configurar a nuvem as definições de proteção</span><span class="sxs-lookup"><span data-stu-id="a444a-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="a444a-205">Crie um tooAzure de política de replicação através da execução Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="a444a-206">Obtenha um contentor de proteção através da execução Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="a444a-207">Obter a variável de tooa de detalhes do Olá política utilizando a tarefa de Olá que foi criada e mentioning nome amigável de política de Olá:</span><span class="sxs-lookup"><span data-stu-id="a444a-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="a444a-208">Inicie associação Olá do contentor de proteção de Olá com a política de replicação de Olá:</span><span class="sxs-lookup"><span data-stu-id="a444a-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="a444a-209">Depois de concluir a tarefa de Olá, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="a444a-210">Depois da tarefa de Olá terminou o processamento, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="a444a-211">conclusão de Olá toocheck operação Olá, siga os passos Olá [monitorizar a atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a444a-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="a444a-212">Passo 8: Configurar o mapeamento da rede</span><span class="sxs-lookup"><span data-stu-id="a444a-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="a444a-213">Antes de começar mapeamento da rede Verifique se as máquinas virtuais no servidor do VMM de origem de Olá tooa ligado rede VM.</span><span class="sxs-lookup"><span data-stu-id="a444a-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="a444a-214">Além disso, crie um ou mais redes virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="a444a-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="a444a-215">Saiba mais sobre como toocreate a virtual rede utilizando o Azure Resource Manager e o PowerShell, no [criar uma rede virtual com uma ligação de VPN de site para site com o Azure Resource Manager e o PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a444a-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="a444a-216">Tenha em atenção que várias redes de Máquina Virtual podem ser mapeado tooa única rede Azure.</span><span class="sxs-lookup"><span data-stu-id="a444a-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="a444a-217">Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome de sub-rede na máquina virtual de origem que Olá está localizado, em seguida, Olá máquina virtual de réplica será ligada toothat sub-rede de destino após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="a444a-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="a444a-218">Se não existir nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será ligado toohello primeira sub-rede Olá rede.</span><span class="sxs-lookup"><span data-stu-id="a444a-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="a444a-219">Step-by-Olá primeiro comando obtém servidores para o Cofre de recuperação de sites do Azure atual Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="a444a-220">comando de Olá armazena os servidores do Microsoft Azure Site Recovery de Olá na variável de matriz Olá $Servers.</span><span class="sxs-lookup"><span data-stu-id="a444a-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="a444a-221">Step-by-Olá segundo comando obtém a rede de recuperação de site Olá para o servidor primeiro Olá na matriz de Olá $Servers.</span><span class="sxs-lookup"><span data-stu-id="a444a-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="a444a-222">comando Olá armazena redes Olá na variável Olá $Networks.</span><span class="sxs-lookup"><span data-stu-id="a444a-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="a444a-223">comando terceiro Olá obtém redes virtuais do Azure e, em seguida, esse valor variável Olá $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="a444a-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="a444a-224">cmdlet final Olá cria um mapeamento entre a rede principal Olá e rede de máquina virtual do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="a444a-225">Olá cmdlet Especifica uma rede principal Olá como primeiro elemento de Olá de $Networks.</span><span class="sxs-lookup"><span data-stu-id="a444a-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="a444a-226">cmdlet de Olá Especifica uma rede de máquina virtual como primeiro elemento de Olá de $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="a444a-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="a444a-227">Passo 9: Ativar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="a444a-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="a444a-228">Depois de servidores de Olá, nuvens e as redes estão configurados corretamente, pode ativar a proteção para máquinas virtuais na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="a444a-229">Tenha em atenção o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="a444a-229">Note hello following:</span></span>

* <span data-ttu-id="a444a-230">Máquinas virtuais têm de cumprir os requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a444a-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="a444a-231">Verifique estes na [pré-requisitos e suporte](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) no guia de planeamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="a444a-232">proteção de tooenable, sistema de operativo Olá e propriedades de disco do sistema operativo tem de ser definidas para a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="a444a-233">Quando cria uma máquina virtual no VMM utilizando um modelo de máquina virtual pode definir a propriedade de Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="a444a-234">Também pode definir estas propriedades de máquinas virtuais existentes nos Olá **geral** e **configuração de Hardware** separadores de propriedades da máquina virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="a444a-235">Se não definir estas propriedades no VMM será capaz de tooconfigure-las no portal do Azure Site Recovery Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="a444a-236">proteção de tooenable, execute Olá contentor de proteção do comando tooget Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a444a-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="a444a-237">Obter a entidade de proteção Olá (VM) executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="a444a-238">Ative Olá DR para Olá VM executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="a444a-239">Testar a implementação</span><span class="sxs-lookup"><span data-stu-id="a444a-239">Test your deployment</span></span>
<span data-ttu-id="a444a-240">tootest a implementação pode executar um teste de ativação pós-falha para uma única máquina virtual, ou criar um plano de recuperação consiste em várias máquinas virtuais e executar uma teste de ativação pós-falha para o plano de Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="a444a-241">Pós-falha de teste simula o mecanismo de ativação pós-falha e recuperação numa rede isolada.</span><span class="sxs-lookup"><span data-stu-id="a444a-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="a444a-242">Tenha em atenção que:</span><span class="sxs-lookup"><span data-stu-id="a444a-242">Note that:</span></span>

* <span data-ttu-id="a444a-243">Se quiser tooconnect toohello corresponde uma máquina virtual no Azure utilizando o ambiente de trabalho remoto após a ativação pós-falha Olá, ative a ligação ao ambiente de trabalho remoto na máquina virtual de Olá antes de executar a ativação pós-falha de teste de Olá.</span><span class="sxs-lookup"><span data-stu-id="a444a-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="a444a-244">Após a ativação pós-falha, utilizará uma pública IP endereço tooconnect toohello máquina virtual no Azure utilizando o ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="a444a-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="a444a-245">Se quiser toodo isto, certifique-se de que não tem quaisquer políticas de domínio que impedem que a máquina virtual ao ligar tooa, utilizando um endereço público.</span><span class="sxs-lookup"><span data-stu-id="a444a-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="a444a-246">conclusão de Olá toocheck operação Olá, siga os passos Olá [monitorizar a atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a444a-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="a444a-247">Executar uma ativação pós-falha de teste</span><span class="sxs-lookup"><span data-stu-id="a444a-247">Run a test failover</span></span>
- <span data-ttu-id="a444a-248">Inicie ativação pós-falha de teste de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="a444a-249">Executar uma ativação pós-falha planeada</span><span class="sxs-lookup"><span data-stu-id="a444a-249">Run a planned failover</span></span>
- <span data-ttu-id="a444a-250">Olá de iniciar a ativação pós-falha planeada, executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="a444a-251">Executar uma ativação pós-falha não planeada</span><span class="sxs-lookup"><span data-stu-id="a444a-251">Run an unplanned failover</span></span>
- <span data-ttu-id="a444a-252">Iniciar Olá ativação pós-falha não planeada executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a444a-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="a444a-253"><a name=monitor></a>Monitorizar a atividade</span><span class="sxs-lookup"><span data-stu-id="a444a-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="a444a-254">Utilize Olá atividade de Olá toomonitor de comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a444a-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="a444a-255">Tenha em atenção que tem toowait entre tarefas de Olá toofinish de processamento.</span><span class="sxs-lookup"><span data-stu-id="a444a-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="a444a-256">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a444a-256">Next steps</span></span>
<span data-ttu-id="a444a-257">[Leia mais](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a444a-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
