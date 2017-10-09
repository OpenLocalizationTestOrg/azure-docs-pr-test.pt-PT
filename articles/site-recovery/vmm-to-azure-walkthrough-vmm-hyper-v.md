---
title: "aaaPrepare System Center VMM para tooAzure de replicação de Hyper-V | Microsoft Docs"
description: "Descreve como servidor do System Center VMM tooprepare para tooAzure de replicação de Hyper-V, utilizando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="8a4c1-103">Passo 6: Preparar servidores VMM e anfitriões Hyper-V para tooAzure de replicação de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="8a4c1-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="8a4c1-104">Depois de configurar [componentes do Azure](vmm-to-azure-walkthrough-prepare-azure.md) para implementação de Olá, utilize instruções Olá na toointeract de anfitriões Hyper-V e servidores VMM do artigo tooprepare no local com o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8a4c1-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="8a4c1-105">Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou coloque questões técnicas no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8a4c1-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="8a4c1-106">Preparar servidores VMM</span><span class="sxs-lookup"><span data-stu-id="8a4c1-106">Prepare VMM servers</span></span>

- <span data-ttu-id="8a4c1-107">É necessário pelo menos um servidor VMM que cumpre os requisitos de suporte de Olá para replicação de recuperação de sites (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="8a4c1-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="8a4c1-108">Certifique-se de já preparou servidor do VMM Olá para [mapeamento da rede](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="8a4c1-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="8a4c1-109">Certifique-se de que o servidor VMM Olá pode aceder a estes URLs</span><span class="sxs-lookup"><span data-stu-id="8a4c1-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="8a4c1-110">Se tiver regras de firewall baseadas no endereço IP, certifique-se de que permitem comunicação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8a4c1-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="8a4c1-111">Permitir Olá [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e Olá porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="8a4c1-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="8a4c1-112">Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).</span><span class="sxs-lookup"><span data-stu-id="8a4c1-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="8a4c1-113">Durante a implementação da recuperação de sites, Olá fornecedor da recuperação de Site de transferir e instalá-lo em cada servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="8a4c1-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="8a4c1-114">servidor do VMM Olá é registado no Cofre de serviços de recuperação de Olá.</span><span class="sxs-lookup"><span data-stu-id="8a4c1-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="8a4c1-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8a4c1-115">Next steps</span></span>

<span data-ttu-id="8a4c1-116">Aceda demasiado[passo 7: criar um cofre](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="8a4c1-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

