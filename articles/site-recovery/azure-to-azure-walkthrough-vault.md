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
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>Passo 4: Configurar um cofre para replicação tooAzure do Azure

Depois de [planeamento redes](azure-to-azure-walkthrough-network.md), utilize este tooset artigo configurar um cofre, máquinas virtuais do Azure (VMs) replicar tooanother região do Azure, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.

- Quando acabar de artigo Olá, deve ter um cofre dos serviços de recuperação que configurar.
- Publique quaisquer comentários na parte inferior deste artigo hello, ou colocar questões no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



>[!NOTE]
>
> Replicação de VM do Azure está atualmente em pré-visualização.




## <a name="create-a-vault"></a>Criar um cofre

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Recomendamos que crie o Cofre de serviços de recuperação de Olá na localização de olá onde pretende que o seu tooreplicate VMs. Por exemplo, se a localização de destino é hello centro dos EUA, criar cofre Olá **EUA Central**.


## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 5: Ativar a replicação](azure-to-azure-walkthrough-enable-replication.md)
