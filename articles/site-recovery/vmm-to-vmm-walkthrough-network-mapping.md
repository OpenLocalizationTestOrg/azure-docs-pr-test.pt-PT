---
title: "aaaMap redes para o site secundário do tooa de replicação de VM de Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toomap redes quando replicar VMs Hyper-V tooa site secundário do VMM com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>Passo 7: Mapear redes para o site secundário de tooa do replicação de VM de Hyper-V


Depois de configurar [as definições de origem e destino](vmm-to-vmm-walkthrough-source-target.md) para replicar o site de System Center Virtual Machine Manager (VMM) Hyper-V máquinas virtuais (VMs) tooa secundário, utilize o mapeamento da rede tooconfigure este artigo para virtual do Hyper-V tooa de replicação de máquina (VM) secundário do site, utilizando [do Azure Site Recovery](site-recovery-overview.md).

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

- Saiba mais sobre [mapeamento da rede](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) antes de começar.
- Certifique-se de que as máquinas virtuais nos servidores VMM estão ligados tooa rede VM.

## <a name="configure-network-mapping"></a>Configurar o mapeamento da rede

1. No **mapeamento da rede** > **mapeamentos da rede**, clique em **+ mapeamento da rede**.
2. No **adicionar mapeamento da rede** separador, selecione a origem de Olá e servidores do VMM de destino. redes VM de Olá associadas a servidores de Olá do VMM são obtidos.
3. No **rede de origem**, selecione rede Olá pretende toouse na lista de redes VM associadas com o servidor VMM principal do Olá Olá.
4. No **rede de destino**, selecione rede Olá pretende toouse do servidor VMM Olá secundário. Em seguida, clique em **OK**.

    ![Mapeamento da rede](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

Veja a seguir o que acontece quando começa o mapeamento da rede:

* Quaisquer máquinas de virtuais de réplica existente que correspondem a rede VM de origem toohello será toohello ligado a rede VM de destino.
* Novas máquinas virtuais que estão ligados toohello rede VM de origem serão ligados toohello destino mapeadas rede após a replicação.
* Se modificar um mapeamento existente com uma nova rede, as máquinas virtuais de réplica serão ligadas utilizando as novas definições Olá.
* Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome de sub-rede na máquina virtual de origem que Olá está localizado, em seguida, Olá máquina virtual de réplica será ligada toothat sub-rede de destino após a ativação pós-falha. Se não existir nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será ligado toohello primeira sub-rede Olá rede.



## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 8: configurar uma política de replicação](vmm-to-vmm-walkthrough-replication.md).
