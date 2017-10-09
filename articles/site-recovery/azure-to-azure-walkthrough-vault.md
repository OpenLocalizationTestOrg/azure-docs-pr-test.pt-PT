---
title: "aaaSet configurar um cofre para a VM do Azure repliction entre regiões com o Azure Site Recovery | Microsoft Docs"
description: "Resume os passos de Olá precisa tooset um cofre de cópia de segurança para a replicação do Azure entre regiões do Azure utilizando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="bea13-103">Passo 4: Configurar um cofre para replicação tooAzure do Azure</span><span class="sxs-lookup"><span data-stu-id="bea13-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="bea13-104">Depois de [planeamento redes](azure-to-azure-walkthrough-network.md), utilize este tooset artigo configurar um cofre, máquinas virtuais do Azure (VMs) replicar tooanother região do Azure, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bea13-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="bea13-105">Quando acabar de artigo Olá, deve ter um cofre dos serviços de recuperação que configurar.</span><span class="sxs-lookup"><span data-stu-id="bea13-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="bea13-106">Publique quaisquer comentários na parte inferior deste artigo hello, ou colocar questões no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bea13-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="bea13-107">Replicação de VM do Azure está atualmente em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="bea13-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="bea13-108">Criar um cofre</span><span class="sxs-lookup"><span data-stu-id="bea13-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="bea13-109">Recomendamos que crie o Cofre de serviços de recuperação de Olá na localização de olá onde pretende que o seu tooreplicate VMs.</span><span class="sxs-lookup"><span data-stu-id="bea13-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="bea13-110">Por exemplo, se a localização de destino é hello centro dos EUA, criar cofre Olá **EUA Central**.</span><span class="sxs-lookup"><span data-stu-id="bea13-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bea13-111">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bea13-111">Next steps</span></span>

<span data-ttu-id="bea13-112">Aceda demasiado[passo 5: Ativar a replicação](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="bea13-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
