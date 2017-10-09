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
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a>Passo 6: Configurar um cofre para tooAzure de replicação do servidor físico


Este artigo descreve como tooset um cofre de cópia de segurança. Pode criar cofre Olá e especifique pretende tooreplicate da sua tooAzure de localização no local, utilizar Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.


Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação 

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Selecione um objetivo de proteção

Selecione o que pretende tooreplicate, e onde pretende tooreplicate para.

1. Clique em **cofres dos serviços de recuperação** > cofre.
2. No Menu de recurso Olá, clique em **recuperação de Site** > **preparar infraestrutura** > **objetivo de proteção**.
3. No **objetivo de proteção**, selecione **tooAzure** > **não virtualizados/outras**.


## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 7: configurar a origem e destino](physical-walkthrough-source-target.md)
