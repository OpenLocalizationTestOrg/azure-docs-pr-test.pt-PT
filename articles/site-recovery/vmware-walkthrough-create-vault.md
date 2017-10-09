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
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a>Passo 7: Configurar um cofre para tooAzure de replicação de VMware


Este artigo descreve como configurar um cofre tooset e especifique pretende tooreplicate da sua localização no local, tooAzure utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.


Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação 

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Selecione um objetivo de proteção

Selecione o que pretende tooreplicate, e onde pretende tooreplicate para.

1. Clique em **cofres dos serviços de recuperação** > cofre.
2. No Menu de recurso Olá, clique em **recuperação de Site** > **preparar infraestrutura** > **objetivo de proteção**.
3. No **objetivo de proteção**, selecione **tooAzure** > **Sim, com o VMware vSphere hipervisor**.



## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 8: configurar a origem e destino](vmware-walkthrough-source-target.md)
