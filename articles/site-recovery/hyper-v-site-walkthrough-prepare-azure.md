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
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a>Passo 5: Preparar os recursos do Azure para tooAzure de replicação de Hyper-V

Utilize as instruções de Olá no tooprepare artigo Azure recursos, de modo a que pode replicar no local VMs de Hyper-V (sem VMM do System Center) tooAzure utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou coloque questões técnicas no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Antes de começar

Certifique-se de que leu Olá [pré-requisitos](hyper-v-site-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Configurar uma conta do Azure

- Obter um [conta do Microsoft Azure](http://azure.microsoft.com/).
- Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
- Verificar as regiões Olá suportado para a recuperação de Site, sob disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Saiba mais sobre [preços da recuperação de Site](site-recovery-faq.md#pricing)e obter Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).


## <a name="set-up-an-azure-network"></a>Configurar uma rede do Azure

- Configure uma rede do Azure. As VMs do Azure são colocadas nesta rede quando são criados após a ativação pós-falha.
- rede de Olá deve estar no Olá mesma região que Olá do cofre dos serviços de recuperação
- Recuperação de sites no portal do Azure de Olá pode utilizar redes configuradas no [Resource Manager](../resource-manager-deployment-model.md), ou no modo clássico.
- Recomendamos que configure uma rede antes de começar. Se não o fizer, terá de toodo-lo durante a implementação da recuperação de Site.
- Saiba mais sobre [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).


## <a name="set-up-an-azure-storage-account"></a>Configurar uma conta de armazenamento do Azure

- Recuperação de site são replicados armazenamento de tooAzure de máquinas no local. As VMs do Azure são criadas a partir do armazenamento de Olá após a ocorrência da ativação pós-falha.
- Configurar um padrão/premium [conta do storage do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold dados replicados tooAzure.
- [Armazenamento Premium](../storage/common/storage-premium-storage.md) é normalmente utilizado para máquinas virtuais que necessitam de um forma consistente de elevado desempenho de e/s e baixa latência toohost e/s intensivas cargas de trabalho.
- Se quiser toouse um toostore de conta de premium dados replicados, terá também de um armazenamento standard conta toostore os registos de replicação que captura em curso alterações dados tooon local.
- Consoante o modelo de recursos de Olá pretende toouse para efetuar a ativação pós-falha de VMs do Azure, configure uma conta no [modo Resource Manager](../storage/common/storage-create-storage-account.md), ou [modo clássico](../storage/common/storage-create-storage-account.md).
- Recomendamos que configure uma conta de armazenamento antes de começar. Se não o fizer necessário toodo-lo durante a implementação da recuperação de Site. contas de Olá tem de constar Olá mesma região que Olá do cofre dos serviços de recuperação.
- Não é possível mover a contas de armazenamento utilizado pela recuperação de sites através de grupos de recursos dentro de Olá mesmo subscrição, ou em subscrições diferentes.


## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 6: recursos preparar Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)
