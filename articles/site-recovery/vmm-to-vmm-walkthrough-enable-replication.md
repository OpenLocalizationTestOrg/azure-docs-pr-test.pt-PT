---
title: "site secundário do tooa de replicação de aaaEnable Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como replicação tooenable para VMs de Hyper-V replicar tooa secundário para o System Center VMM do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>Passo 9: Ativar o site secundário do replicação tooa para VMs de Hyper-V


Depois de configurar uma política de replicação, utilize este site de System Center Virtual Machine Manager (VMM) secundária de tooa do artigo tooenable replicação para máquinas no local Hyper-V virtual (VM), utilizando [do Azure Site Recovery](site-recovery-overview.md).

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="select-vms-tooreplicate"></a>Selecione tooreplicate de VMs

1. Clique em **Passo 2: Replicar aplicação** > **Origem**. 

    ![Ativar a replicação](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. No **origem**, selecione o servidor do VMM Olá e Olá nuvem em que Olá estão localizados os anfitriões de Hyper-V que pretende tooreplicate. Em seguida, clique em **OK**.

    ![Ativar a replicação](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. No **destino**, certifique-se de que servidor VMM secundário Olá e na nuvem.
4. No **máquinas virtuais**, selecione de VMs de Olá pretende tooprotect da lista de Olá.

    ![Ativar a proteção da máquina virtual](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

Pode controlar o progresso de Olá **ativar proteção** ação no **tarefas** > **as tarefas de recuperação de Site**. Depois de Olá **finalizar proteção** tarefa é concluída, Olá a replicação inicial está concluída e Olá máquina está preparada para ativação pós-falha.

Tenha em atenção que:

- Também pode ativar a proteção para máquinas virtuais na consola do VMM Olá. Clique em **ativar proteção** na barra de ferramentas de Olá nas propriedades da máquina virtual de Olá > **do Azure Site Recovery** separador.
- Depois de ativar a replicação, pode ver as propriedades de Olá VM na **itens replicados**. No Olá **Essentials** dashboard, pode ver informações sobre a política de replicação de Olá para Olá VM e o respetivo estado. Clique em **propriedades** para obter mais detalhes.

## <a name="onboard-existing-vms"></a>Carregar VMs existentes

Se tiver máquinas virtuais existentes no VMM que estiver a replicar com a réplica do Hyper-V, pode carregá-las para replicação de recuperação de sites do Azure da seguinte forma:

1. Certifique-se de que o servidor Olá Hyper-V que aloja Olá que VM existente está localizado na nuvem principal Olá e esse servidor de Hyper-V Olá Olá máquina virtual de réplica de alojamento está localizado na nuvem secundário Olá.
2. Certifique-se de que uma política de replicação está configurada para a nuvem VMM principal Olá.
3. Ative a replicação para a máquina virtual primária de Olá. Do Azure Site Recovery e o VMM Certifique-se de que hello mesmo anfitrião de réplica e a máquina virtual é detetada e irá reutilizar o Azure Site Recovery e restabelecer a replicação utilizando Olá especificadas as definições.


## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 10: executar uma ativação pós-falha de teste](vmm-to-vmm-walkthrough-test-failover.md).
