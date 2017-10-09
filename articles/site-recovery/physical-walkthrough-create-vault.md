---
title: "aaaSet configurar um cofre para tooAzure de replicação do servidor físico utilizando o Azure Site Recovery | Microsoft Docs"
description: "Resume os passos de Olá terá tooset segurança um tooAzure servidores físicos do cofre tooreplicate utilizando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="30157-103">Passo 6: Configurar um cofre para tooAzure de replicação do servidor físico</span><span class="sxs-lookup"><span data-stu-id="30157-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="30157-104">Este artigo descreve como tooset um cofre de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="30157-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="30157-105">Pode criar cofre Olá e especifique pretende tooreplicate da sua tooAzure de localização no local, utilizar Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="30157-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="30157-106">Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="30157-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="30157-107">Criar um cofre dos Serviços de Recuperação </span><span class="sxs-lookup"><span data-stu-id="30157-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="30157-108">Selecione um objetivo de proteção</span><span class="sxs-lookup"><span data-stu-id="30157-108">Select a protection goal</span></span>

<span data-ttu-id="30157-109">Selecione o que pretende tooreplicate, e onde pretende tooreplicate para.</span><span class="sxs-lookup"><span data-stu-id="30157-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="30157-110">Clique em **cofres dos serviços de recuperação** > cofre.</span><span class="sxs-lookup"><span data-stu-id="30157-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="30157-111">No Menu de recurso Olá, clique em **recuperação de Site** > **preparar infraestrutura** > **objetivo de proteção**.</span><span class="sxs-lookup"><span data-stu-id="30157-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="30157-112">No **objetivo de proteção**, selecione **tooAzure** > **não virtualizados/outras**.</span><span class="sxs-lookup"><span data-stu-id="30157-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="30157-113">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="30157-113">Next steps</span></span>

<span data-ttu-id="30157-114">Aceda demasiado[passo 7: configurar a origem e destino](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="30157-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
