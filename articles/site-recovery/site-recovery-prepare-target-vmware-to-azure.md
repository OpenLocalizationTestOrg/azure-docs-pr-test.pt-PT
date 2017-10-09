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
# <a name="prepare-target-vmware-tooazure"></a>Preparar o destino (VMware tooAzure)
> [!div class="op_single_selector"]
> * [TooAzure de VMware](./site-recovery-prepare-target-vmware-to-azure.md)
> * [TooAzure físico](./site-recovery-prepare-target-physical-to-azure.md)

Este artigo descreve como tooprepare toostart o ambiente do Azure replicar tooAzure de máquinas virtuais VMware.

## <a name="prerequisites"></a>Pré-requisitos

artigo de Olá assume seguinte Olá:
- Criou um cofre dos serviços de recuperação tooprotect máquinas virtuais VMware. Pode criar um cofre dos serviços de recuperação a partir Olá [portal do Azure](http://portal.azure.com "portal do Azure").
- Tiver [configuração do ambiente no local](./site-recovery-set-up-vmware-to-azure.md) tooAzure de máquinas virtuais de VMware tooreplicate.

## <a name="prepare-target"></a>Preparar o destino

Depois de concluir Olá **objetivo de proteção do passo 1:Select** e **passo 2: preparar a origem**, é direcionado demasiado**passo 3: destino**

![Preparar o destino](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. **Subscrição:** de Olá menu pendente, selecione Olá subscrição que pretende que o tooreplicate as máquinas virtuais.
2. **Modelo de implementação:** modelo de implementação de Olá selecione (clássico ou do Resource Manager)

Com base na Olá escolhido o modelo de implementação, uma validação é executada tooensure tiver pelo menos uma conta de armazenamento compatíveis e de rede virtual no tooreplicate de subscrição de destino Olá e ativação pós-falha da máquina virtual.

Depois de validações Olá concluir com êxito, clique em OK toogo toohello próximo passo.

Se não tiver uma conta de armazenamento do Resource Manager compatível ou de rede virtual, ou se gostaria de tooadd mais, pode fazê-clicando Olá **+ contas de armazenamento** ou **+ rede** botões na parte superior de Olá de Olá painel.

## <a name="next-steps"></a>Passos seguintes
[Configurar as definições de replicação](./site-recovery-setup-replication-settings-vmware.md).
