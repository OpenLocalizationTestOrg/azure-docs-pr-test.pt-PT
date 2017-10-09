---
title: "aaaSet configurar um cofre para tooAzure de replicação de VMware utilizando o Azure Site Recovery | Microsoft Docs"
description: "Resume os passos de Olá precisa tooset um cofre de cópia de segurança para tooAzure de replicação de VMware utilizando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a><span data-ttu-id="d62e6-103">Passo 7: Configurar um cofre para tooAzure de replicação de VMware</span><span class="sxs-lookup"><span data-stu-id="d62e6-103">Step 7: Set up a vault for VMware replication tooAzure</span></span>


<span data-ttu-id="d62e6-104">Este artigo descreve como configurar um cofre tooset e especifique pretende tooreplicate da sua localização no local, tooAzure utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d62e6-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="d62e6-105">Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="d62e6-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="d62e6-106">Criar um cofre dos Serviços de Recuperação </span><span class="sxs-lookup"><span data-stu-id="d62e6-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="d62e6-107">Selecione um objetivo de proteção</span><span class="sxs-lookup"><span data-stu-id="d62e6-107">Select a protection goal</span></span>

<span data-ttu-id="d62e6-108">Selecione o que pretende tooreplicate, e onde pretende tooreplicate para.</span><span class="sxs-lookup"><span data-stu-id="d62e6-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="d62e6-109">Clique em **cofres dos serviços de recuperação** > cofre.</span><span class="sxs-lookup"><span data-stu-id="d62e6-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="d62e6-110">No Menu de recurso Olá, clique em **recuperação de Site** > **preparar infraestrutura** > **objetivo de proteção**.</span><span class="sxs-lookup"><span data-stu-id="d62e6-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="d62e6-111">No **objetivo de proteção**, selecione **tooAzure** > **Sim, com o VMware vSphere hipervisor**.</span><span class="sxs-lookup"><span data-stu-id="d62e6-111">In **Protection goal**, select **tooAzure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="d62e6-112">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d62e6-112">Next steps</span></span>

<span data-ttu-id="d62e6-113">Aceda demasiado[passo 8: configurar a origem e destino](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="d62e6-113">Go too[Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
