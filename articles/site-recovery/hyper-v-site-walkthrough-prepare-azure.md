---
title: aaaPrepare recursos do Azure tooreplicate VMs de Hyper-V (sem VMM do System Center) tooAzure utilizando o Azure Site Recovery | Microsoft Docs
description: "Descreve o que precisa no local no Azure antes de iniciar a replicação tooAzure de VMs de Hyper-V (sem VMM) utilizando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a><span data-ttu-id="726d3-103">Passo 5: Preparar os recursos do Azure para tooAzure de replicação de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="726d3-103">Step 5: Prepare Azure resources for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="726d3-104">Utilize as instruções de Olá no tooprepare artigo Azure recursos, de modo a que pode replicar no local VMs de Hyper-V (sem VMM do System Center) tooAzure utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="726d3-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="726d3-105">Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou coloque questões técnicas no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="726d3-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="726d3-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="726d3-106">Before you start</span></span>

<span data-ttu-id="726d3-107">Certifique-se de que leu Olá [pré-requisitos](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="726d3-107">Make sure you've read hello [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="726d3-108">Configurar uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="726d3-108">Set up an Azure account</span></span>

- <span data-ttu-id="726d3-109">Obter um [conta do Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="726d3-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="726d3-110">Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="726d3-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="726d3-111">Verificar as regiões Olá suportado para a recuperação de Site, sob disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="726d3-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="726d3-112">Saiba mais sobre [preços da recuperação de Site](site-recovery-faq.md#pricing)e obter Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="726d3-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="726d3-113">Configurar uma rede do Azure</span><span class="sxs-lookup"><span data-stu-id="726d3-113">Set up an Azure network</span></span>

- <span data-ttu-id="726d3-114">Configure uma rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="726d3-114">Set up an Azure network.</span></span> <span data-ttu-id="726d3-115">As VMs do Azure são colocadas nesta rede quando são criados após a ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="726d3-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="726d3-116">rede de Olá deve estar no Olá mesma região que Olá do cofre dos serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="726d3-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="726d3-117">Recuperação de sites no portal do Azure de Olá pode utilizar redes configuradas no [Resource Manager](../resource-manager-deployment-model.md), ou no modo clássico.</span><span class="sxs-lookup"><span data-stu-id="726d3-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="726d3-118">Recomendamos que configure uma rede antes de começar.</span><span class="sxs-lookup"><span data-stu-id="726d3-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="726d3-119">Se não o fizer, terá de toodo-lo durante a implementação da recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="726d3-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="726d3-120">Saiba mais sobre [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="726d3-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="726d3-121">Configurar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="726d3-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="726d3-122">Recuperação de site são replicados armazenamento de tooAzure de máquinas no local.</span><span class="sxs-lookup"><span data-stu-id="726d3-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="726d3-123">As VMs do Azure são criadas a partir do armazenamento de Olá após a ocorrência da ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="726d3-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="726d3-124">Configurar um padrão/premium [conta do storage do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold dados replicados tooAzure.</span><span class="sxs-lookup"><span data-stu-id="726d3-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="726d3-125">[Armazenamento Premium](../storage/common/storage-premium-storage.md) é normalmente utilizado para máquinas virtuais que necessitam de um forma consistente de elevado desempenho de e/s e baixa latência toohost e/s intensivas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="726d3-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="726d3-126">Se quiser toouse um toostore de conta de premium dados replicados, terá também de um armazenamento standard conta toostore os registos de replicação que captura em curso alterações dados tooon local.</span><span class="sxs-lookup"><span data-stu-id="726d3-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="726d3-127">Consoante o modelo de recursos de Olá pretende toouse para efetuar a ativação pós-falha de VMs do Azure, configure uma conta no [modo Resource Manager](../storage/common/storage-create-storage-account.md), ou [modo clássico](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="726d3-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="726d3-128">Recomendamos que configure uma conta de armazenamento antes de começar.</span><span class="sxs-lookup"><span data-stu-id="726d3-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="726d3-129">Se não o fizer necessário toodo-lo durante a implementação da recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="726d3-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="726d3-130">contas de Olá tem de constar Olá mesma região que Olá do cofre dos serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="726d3-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="726d3-131">Não é possível mover a contas de armazenamento utilizado pela recuperação de sites através de grupos de recursos dentro de Olá mesmo subscrição, ou em subscrições diferentes.</span><span class="sxs-lookup"><span data-stu-id="726d3-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="726d3-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="726d3-132">Next steps</span></span>

<span data-ttu-id="726d3-133">Aceda demasiado[passo 6: recursos preparar Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="726d3-133">Go too[Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
