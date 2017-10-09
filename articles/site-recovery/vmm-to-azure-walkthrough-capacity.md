---
title: "aaaPlan capacidade e dimensionamento de VM de Hyper-V tooAzure de replicação (com o VMM) com o Azure Site Recovery | Microsoft Docs"
description: Utilizar esta capacidade de tooplan artigo e escala quando replicar VMs de Hyper-V no VMM nuvens tooAzure, com o Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a><span data-ttu-id="f3dcf-103">Passo 3: Planear a capacidade e dimensionamento para replicação de tooAzure do Hyper-V (com o VMM)</span><span class="sxs-lookup"><span data-stu-id="f3dcf-103">Step 3: Plan capacity and scaling for Hyper-V (with VMM) tooAzure replication</span></span>

<span data-ttu-id="f3dcf-104">Depois de ter revisto Olá [os pré-requisitos de implementação](vmm-to-azure-walkthrough-prerequisites.md), utilize este toofigure artigo saída planeamento de capacidade e dimensionamento, quando replicar no local VMs de Hyper-V no tooAzure de nuvens do System Center Virtual Machine Manager (VMM), com [do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f3dcf-104">After you've reviewed hello [deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md), use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="f3dcf-105">Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou coloque questões técnicas no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f3dcf-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="f3dcf-106">Como começar a planear a capacidade?</span><span class="sxs-lookup"><span data-stu-id="f3dcf-106">How do I start capacity planning?</span></span>


<span data-ttu-id="f3dcf-107">Recolher informações sobre o seu ambiente de replicação e, em seguida, capacidade de plano utilizando dados Olá, juntamente com considerações de Olá realçados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-107">You gather information about your replication environment, and then plan capacity using hello data, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="f3dcf-108">Reunir informações</span><span class="sxs-lookup"><span data-stu-id="f3dcf-108">Gather information</span></span>

1. <span data-ttu-id="f3dcf-109">Recolher informações sobre o ambiente de replicação, incluindo VMs, discos por VMs e armazenamento por disco.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="f3dcf-110">Identifica a taxa de alteração (renovação) diária para os dados replicados.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="f3dcf-111">Transferir Olá [ferramenta o planeamento de capacidade do Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) taxa de alteração de Olá tooget.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="f3dcf-112">Recomendamos que execute esta ferramenta através de uma semana toocapture médias.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="f3dcf-113">Descobrir a capacidade</span><span class="sxs-lookup"><span data-stu-id="f3dcf-113">Figure out capacity</span></span>

<span data-ttu-id="f3dcf-114">Com base nas informações de Olá tiver recolha, executar Olá [ferramenta de Planeador de capacidade de recuperação de sites](http://aka.ms/asr-capacity-planner-excel) tooanalyze o ambiente de origem e cargas de trabalho, estimar necessidades de largura de banda e de recursos do servidor de localização de origem Olá e Olá recursos (máquinas virtuais e armazenamento, etc.), que necessita na localização de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="f3dcf-115">Pode executar a ferramenta de Olá em alguns dos modos de:</span><span class="sxs-lookup"><span data-stu-id="f3dcf-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="f3dcf-116">Planear rápido: execute a ferramenta de Olá neste modo projeções de rede e o servidor de tooget com base num número médio de VMs, discos, armazenamento e a taxa de alteração.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="f3dcf-117">Detalhadas de planeamento: execute a ferramenta de Olá neste modo e forneça detalhes de cada carga de trabalho ao nível da VM.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="f3dcf-118">Analisar a compatibilidade da VM e obter projeções de rede e servidor.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="f3dcf-119">Agora, execute a ferramenta de Olá:</span><span class="sxs-lookup"><span data-stu-id="f3dcf-119">Now run hello tool:</span></span>

1. <span data-ttu-id="f3dcf-120">Transferir Olá [ferramenta](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="f3dcf-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="f3dcf-121">Planeador de rápida Olá toorun, siga [estas instruções](site-recovery-capacity-planner.md#run-the-quick-planner)e o cenário de Olá selecione **tooAzure de Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="f3dcf-122">toorun Olá Planeador de detalhado, siga [estas instruções](site-recovery-capacity-planner.md#run-the-detailed-planner)e o cenário de Olá selecione **Hyper-V tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="f3dcf-123">Largura de banda de rede de controlo</span><span class="sxs-lookup"><span data-stu-id="f3dcf-123">Control network bandwidth</span></span>

<span data-ttu-id="f3dcf-124">Depois de ter largura de banda Olá calculada que precisa, tem duas opções para controlar Olá quantidade de largura de banda utilizada na replicação:</span><span class="sxs-lookup"><span data-stu-id="f3dcf-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="f3dcf-125">**Limitar largura de banda**: tráfego do Hyper-V que replica tooAzure passa através de um anfitrião Hyper-V específico.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="f3dcf-126">Pode limitar a largura de banda no servidor de anfitrião Olá.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="f3dcf-127">**Influenciar a largura de banda**: pode influenciar a largura de banda Olá utilizada na replicação através de um par de chaves de registo.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="f3dcf-128">Limitar largura de banda</span><span class="sxs-lookup"><span data-stu-id="f3dcf-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="f3dcf-129">Abra Olá MMC da cópia de segurança do Microsoft Azure snap-in no servidor de anfitrião do Hyper-V Olá.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="f3dcf-130">Por predefinição, um atalho para cópia de segurança do Microsoft Azure está disponível no ambiente de trabalho Olá ou em c:\Programas\Microsoft c:\Programas\Microsoft Azure Recovery Services agent\bin\wabadmin..</span><span class="sxs-lookup"><span data-stu-id="f3dcf-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="f3dcf-131">No snap-in Olá clique **alterar propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="f3dcf-132">No Olá **limitação** separador selecione **ativar a limitação para operações de cópia de segurança de utilização de largura de banda de internet**e definir limites de Olá para o trabalho e de descanso horas.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="f3dcf-133">Intervalos válidos são de Kbps 512 too102 Mbps, por segundo.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![Limitar largura de banda](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

<span data-ttu-id="f3dcf-135">Também pode utilizar Olá [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="f3dcf-136">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="f3dcf-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="f3dcf-137">**Set-OBMachineSetting -NoThrottle** indica que não é necessária nenhuma limitação.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="f3dcf-138">Influência da largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="f3dcf-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="f3dcf-139">No registo de Olá navegue demasiado**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="f3dcf-140">tráfego de largura de banda de Olá tooinfluence num disco replicação, modificar Olá de valor de Olá **UploadThreadsPerVM**, ou crie a chave de Olá, se não existir.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="f3dcf-141">largura de banda do tooinfluence Olá para tráfego de reativação pós-falha a partir do Azure, modifique o valor de Olá **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="f3dcf-142">valor predefinido de Olá é 4.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-142">hello default value is 4.</span></span> <span data-ttu-id="f3dcf-143">Numa rede "sobreaprovisionada", estas chaves do registo devem ser Olá valores predefinidos alteradas.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="f3dcf-144">Olá máximo é 32.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-144">hello maximum is 32.</span></span> <span data-ttu-id="f3dcf-145">Monitorizar o valor de Olá toooptimize de tráfego.</span><span class="sxs-lookup"><span data-stu-id="f3dcf-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3dcf-146">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f3dcf-146">Next steps</span></span>

<span data-ttu-id="f3dcf-147">Aceda demasiado[passo 4: planear o funcionamento em rede](vmm-to-azure-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="f3dcf-147">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md).</span></span>
