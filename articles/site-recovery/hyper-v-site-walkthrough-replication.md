---
title: "aaaSet configurar uma política de replicação de VM de Hyper-V tooAzure de replicação (sem VMM do System Center) com o Azure Site Recovery | Microsoft Docs"
description: "Resume os passos de Olá terá tooset configurar uma política de replicação quando replicar VMs Hyper-V tooAzure armazenamento"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="20560-103">Passo 9: Configurar uma política de replicação para tooAzure de replicação de VM de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="20560-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="20560-104">Este artigo descreve como tooset configurar uma política de replicação quando está a replicar VMs Hyper-V tooAzure (sem VMM do System Center) utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="20560-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="20560-105">Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="20560-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="20560-106">Sobre instantâneos</span><span class="sxs-lookup"><span data-stu-id="20560-106">About snapshots</span></span>

<span data-ttu-id="20560-107">Hyper-V utiliza dois tipos de instantâneos – um instantâneo padrão que fornece um instantâneo incremental de toda a máquina virtual Olá e um instantâneo consistente com aplicações, que tira um instantâneo de ponto no tempo dos dados de aplicação Olá no interior da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="20560-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="20560-108">Instantâneos consistentes com aplicações utilizam tooensure do serviço de cópia de sombra de Volume (VSS) que aplicações estão num estado consistente quando se obtém o instantâneo de Olá.</span><span class="sxs-lookup"><span data-stu-id="20560-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="20560-109">Se ativar instantâneos consistentes com aplicações, afetará o desempenho de Olá das aplicações em execução em máquinas virtuais de origem.</span><span class="sxs-lookup"><span data-stu-id="20560-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="20560-110">Certifique-se de que valor Olá definido é inferior ao número de Olá de pontos de recuperação adicionais que configura.</span><span class="sxs-lookup"><span data-stu-id="20560-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="20560-111">Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="20560-111">Set up a replication policy</span></span>

1. <span data-ttu-id="20560-112">toocreate uma nova política de replicação, clique em **preparar a infraestrutura** > **as definições de replicação** > **+ criar e associar**.</span><span class="sxs-lookup"><span data-stu-id="20560-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Rede](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="20560-114">Em **Criar e associar política**, especifique um nome de política.</span><span class="sxs-lookup"><span data-stu-id="20560-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="20560-115">No **copiar frequência**, especifique a frequência pretende que os tooreplicate delta dados após a replicação inicial de Olá (cada 30 segundos, 5 ou 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="20560-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="20560-116">Uma frequência de segundo 30 não é suportada quando replicar toopremium armazenamento.</span><span class="sxs-lookup"><span data-stu-id="20560-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="20560-117">limitação de Olá é determinada pelo número do Olá de instantâneos por blob (100) suportado pelo armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="20560-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="20560-118">[Saiba mais](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="20560-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="20560-119">No **retenção do ponto de recuperação**, especifique, em horas quanto tempo é de janela de retenção de Olá para cada ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="20560-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="20560-120">As VMs podem ser recuperados tooany ponto nessa janela.</span><span class="sxs-lookup"><span data-stu-id="20560-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="20560-121">No **frequência de instantâneos consistentes com aplicação**, especifique a frequência (1-12 horas) pontos de recuperação que contêm instantâneos consistentes com aplicações são criados.</span><span class="sxs-lookup"><span data-stu-id="20560-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="20560-122">No **hora de início da replicação inicial**, especifique quando toostart Olá a replicação inicial.</span><span class="sxs-lookup"><span data-stu-id="20560-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="20560-123">replicação de Olá ocorre através da sua largura de banda de internet, pelo que poderá ser útil tooschedule-lo fora do horário de trabalho.</span><span class="sxs-lookup"><span data-stu-id="20560-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="20560-124">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="20560-124">Then click **OK**.</span></span>

    ![Política de replicação](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="20560-126">Quando cria uma nova política,-la automaticamente associado ao site de Hyper-V Olá.</span><span class="sxs-lookup"><span data-stu-id="20560-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="20560-127">Pode associar um site Hyper-V (e Olá VMs na mesma) várias políticas de replicação no **replicação** > nome da política > **associar o Site de Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="20560-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="20560-128">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="20560-128">Next steps</span></span>

<span data-ttu-id="20560-129">Aceda demasiado[passo 10: Ativar a replicação](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="20560-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
