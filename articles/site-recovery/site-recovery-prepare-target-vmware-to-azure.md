---
title: Preparar o destino (VMware tooAzure) | Microsoft Docs
description: "Este artigo descreve como tooprepare toostart o ambiente do Azure replicar tooAzure de máquinas virtuais VMware."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="06c65-103">Preparar o destino (VMware tooAzure)</span><span class="sxs-lookup"><span data-stu-id="06c65-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06c65-104">TooAzure de VMware</span><span class="sxs-lookup"><span data-stu-id="06c65-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="06c65-105">TooAzure físico</span><span class="sxs-lookup"><span data-stu-id="06c65-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="06c65-106">Este artigo descreve como tooprepare toostart o ambiente do Azure replicar tooAzure de máquinas virtuais VMware.</span><span class="sxs-lookup"><span data-stu-id="06c65-106">This article describes how tooprepare your Azure environment toostart replicating VMware virtual machines tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06c65-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="06c65-107">Prerequisites</span></span>

<span data-ttu-id="06c65-108">artigo de Olá assume seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="06c65-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="06c65-109">Criou um cofre dos serviços de recuperação tooprotect máquinas virtuais VMware.</span><span class="sxs-lookup"><span data-stu-id="06c65-109">You have created a Recovery Services Vault tooprotect your VMware virtual machines.</span></span> <span data-ttu-id="06c65-110">Pode criar um cofre dos serviços de recuperação a partir Olá [portal do Azure](http://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="06c65-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="06c65-111">Tiver [configuração do ambiente no local](./site-recovery-set-up-vmware-to-azure.md) tooAzure de máquinas virtuais de VMware tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="06c65-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware virtual machines tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="06c65-112">Preparar o destino</span><span class="sxs-lookup"><span data-stu-id="06c65-112">Prepare target</span></span>

<span data-ttu-id="06c65-113">Depois de concluir Olá **objetivo de proteção do passo 1:Select** e **passo 2: preparar a origem**, é direcionado demasiado**passo 3: destino**</span><span class="sxs-lookup"><span data-stu-id="06c65-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![Preparar o destino](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="06c65-115">**Subscrição:** de Olá menu pendente, selecione Olá subscrição que pretende que o tooreplicate as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="06c65-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your virtual machines to.</span></span>
2. <span data-ttu-id="06c65-116">**Modelo de implementação:** modelo de implementação de Olá selecione (clássico ou do Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="06c65-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="06c65-117">Com base na Olá escolhido o modelo de implementação, uma validação é executada tooensure tiver pelo menos uma conta de armazenamento compatíveis e de rede virtual no tooreplicate de subscrição de destino Olá e ativação pós-falha da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06c65-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your virtual machine to.</span></span>

<span data-ttu-id="06c65-118">Depois de validações Olá concluir com êxito, clique em OK toogo toohello próximo passo.</span><span class="sxs-lookup"><span data-stu-id="06c65-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="06c65-119">Se não tiver uma conta de armazenamento do Resource Manager compatível ou de rede virtual, ou se gostaria de tooadd mais, pode fazê-clicando Olá **+ contas de armazenamento** ou **+ rede** botões na parte superior de Olá de Olá painel.</span><span class="sxs-lookup"><span data-stu-id="06c65-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06c65-120">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="06c65-120">Next steps</span></span>
<span data-ttu-id="06c65-121">[Configurar as definições de replicação](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="06c65-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
