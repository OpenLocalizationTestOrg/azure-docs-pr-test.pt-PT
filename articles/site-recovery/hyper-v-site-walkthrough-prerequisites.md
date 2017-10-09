---
title: "Pré-requisitos de Olá de aaaReview para replicação de tooAzure Hyper-V (sem VMM do System Center) utilizando o Azure Site Recovery | Microsoft Docs"
description: "Descreve Olá pré-requisitos para configurar a replicação, ativação pós-falha e recuperação de tooAzure de VMs de Hyper-V no local com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="a828f-103">Passo 2: Consultar Olá pré-requisitos para replicação de tooAzure do Hyper-V (sem VMM)</span><span class="sxs-lookup"><span data-stu-id="a828f-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="a828f-104">Pré-requisitos de Olá estão resumidos na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="a828f-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="a828f-105">**Pré-requisito**</span><span class="sxs-lookup"><span data-stu-id="a828f-105">**Prerequisite**</span></span> | <span data-ttu-id="a828f-106">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="a828f-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="a828f-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="a828f-107">**Azure**</span></span> | <span data-ttu-id="a828f-108">Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="a828f-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="a828f-109">**Servidores no local**</span><span class="sxs-lookup"><span data-stu-id="a828f-109">**On-premises servers**</span></span> | <span data-ttu-id="a828f-110">[Saiba mais](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sobre os requisitos para anfitriões de Hyper-V Olá no local.</span><span class="sxs-lookup"><span data-stu-id="a828f-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="a828f-111">**VMs de Hyper-V no local**</span><span class="sxs-lookup"><span data-stu-id="a828f-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="a828f-112">As VMs que pretende tooreplicate devem estar a executar um [sistema operativo suportado](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="a828f-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="a828f-113">**URLs do Azure**</span><span class="sxs-lookup"><span data-stu-id="a828f-113">**Azure URLs**</span></span> | <span data-ttu-id="a828f-114">Anfitriões Hyper-V tem de aceder toothese URLs:</span><span class="sxs-lookup"><span data-stu-id="a828f-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="a828f-115">Se tiver regras de firewall baseadas no endereço IP, certifique-se de que permitem comunicação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a828f-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="a828f-116">Permitir Olá [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e Olá porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="a828f-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="a828f-117">Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).</span><span class="sxs-lookup"><span data-stu-id="a828f-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="a828f-118">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a828f-118">Next steps</span></span>

- <span data-ttu-id="a828f-119">Se estiver a fazer uma implementação completa, aceda demasiado[passo 3: planear a capacidade](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="a828f-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="a828f-120">Se estiver a fazer uma implementação de teste simples, aceda demasiado[passo 4: planear o funcionamento em rede](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="a828f-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
