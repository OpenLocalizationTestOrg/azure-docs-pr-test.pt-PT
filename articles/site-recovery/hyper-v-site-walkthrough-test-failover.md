---
title: "aaaRun uma ativação pós-falha de teste para Hyper-V tooAzure de replicação (sem VMM do System Center) | Microsoft Docs"
description: "Resume os passos de Olá que precisa para executar uma ativação pós-falha de teste para VMs de Hyper-V tooAzure utilizando o serviço do Azure Site Recovery Olá a replicar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c9a4c3ca-84a0-4668-b700-9b0046202299
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: dbcca080a8fa139e2ea0d132323101dd0f7cd265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-tooazure"></a>Passo 11: Executar uma ativação pós-falha de teste para tooAzure de replicação de Hyper-V

Este artigo descreve como toorun uma ativação pós-falha de teste do local máquinas de virtuais de Hyper-V (não geridos pelo System Center VMM) tooAzure, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.

Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Antes de começar

Antes de executar uma ativação pós-falha de teste, recomendamos que verifique Olá propriedades da VM e efetue as alterações tem. Pode aceder às propriedades VM Olá no **replicado itens**. Olá **Essentials** painel mostra informações sobre o estado e as definições de máquinas.

## <a name="managed-disk-considerations"></a>Considerações de disco gerido

[Discos geridos pelo](../virtual-machines/windows/managed-disks-overview.md) simplificar a gestão de discos para VMs do Azure, através da gestão de contas do storage Olá associadas aos discos VM Olá. 

- Discos geridos são criados e ligados toohello VM apenas quando ocorre um tooAzure de ativação pós-falha. Quando ativar a proteção, os dados a partir de VMs no local replicam toostorage contas.
- Discos geridos podem ser criados apenas para as VMs que são implementadas utilizando o modelo de implementação do Olá Resource manager.
- Reativação pós-falha a partir do Azure tooan no local do ambiente de Hyper-V não é atualmente suportada em máquinas com discos geridos. Só deve definir **utilize discos geridos pelo** demasiado**Sim** se estiver a fazer uma migração apenas (ativação pós-falha tooAzure sem reativação pós-falha)
- Com esta definição ativada, conjuntos de disponibilidade só na grupos de recursos que tenham **utilize discos geridos pelo** ativada podem ser selecionadas. As VMs com discos geridos têm de ser em conjuntos de disponibilidade com **utilize discos geridos pelo** definido demasiado**Sim**. Se a definição de Olá não está ativada para as VMs, podem ser selecionados apenas conjuntos de disponibilidade em grupos de recursos sem discos geridos ativados. [Saiba mais](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).
- - Se a conta de armazenamento de Olá que utiliza para replicação foi encriptada com a encriptação do serviço de armazenamento, discos geridos não não possível criar durante a ativação pós-falha. Neste caso: não permitir a utilização de discos geridos, ou desative a proteção de VM de Olá e voltar a ativar toouse uma conta de armazenamento que não tem a encriptação ativada. [Saiba mais](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).

 
## <a name="network-considerations"></a>Considerações de rede
    
- Pode definir Olá destino IP endereço toobe utilizado para Olá VM do Azure após a ativação pós-falha. Se não fornecer um endereço, Olá máquina a ativação pós-falha utilizará o DHCP. Se definir um endereço que não está disponível na ativação pós-falha, a ativação pós-falha de Olá irá falhar. Olá mesmo endereço IP de destino pode ser utilizado para ativação pós-falha de teste se o endereço de Olá está disponível na rede de ativação pós-falha de teste de Olá.
- número de Olá dos adaptadores de rede é ditado pelo tamanho Olá que especificar para a máquina de virtual de destino Olá, da seguinte forma:
    - Se o número de Olá de adaptadores de rede na máquina de origem Olá é menor ou igual toohello número de adaptadores de permitido para o tamanho da máquina de destino Olá, em seguida, terá de destino Olá Olá o mesmo número de adaptadores que origem Olá.
    - Se o número de Olá de adaptadores Olá máquina virtual de origem excede o número de Olá permitido para o tamanho de destino Olá, o tamanho máximo de destino Olá será utilizado.
    - Por exemplo, se uma máquina de origem tiver dois adaptadores de rede e tamanho da máquina Olá destino suporta quatro, a máquina de destino Olá terá dois adaptadores. Se Olá máquina de origem tiver dois adaptadores, mas hello tamanho de destino só suporta um computador de destino Olá terá apenas um adaptador.     
- Se Olá VM tem vários adaptadores de rede, todos serão ligados toohello mesma rede.
- Se a máquina virtual de Olá tem vários adaptadores de rede, em seguida, Olá primeiro mostrado na lista de Olá torna-se Olá *predefinido* adaptador de rede no Olá máquina virtual do Azure.


## <a name="view-and-manage-vm-settings"></a>Ver e gerir as definições da VM

Recomendamos que verifique as propriedades de Olá Olá da máquina de origem antes de executar uma ativação pós-falha.

1. No **itens protegidos**, clique em **itens replicados**e clique em Olá VM.

    ![Ativar a replicação](./media/hyper-v-site-walkthrough-test-failover/test-failover1.png)
2. No Olá **replicados item** painel, pode ver um resumo das informações de VM, o estado de funcionamento e pontos de recuperação disponível mais recentes do Olá. Clique em **propriedades** tooview mais detalhes.

    ![Ativar a replicação](./media/hyper-v-site-walkthrough-test-failover/test-failover2.png)
3. No **computação e rede**, pode:
    - Modificar o nome da VM do Azure de Olá. nome de Olá têm de cumprir [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Especifique uma pós-falha [grupo de recursos].
    - Especifique um tamanho de destino para Olá VM do Azure
    - Selecione um [conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md).
    - Especifique se toouse [discos geridos pelo](#managed-disk-considerations). Selecione **Sim**, se pretender que tooattach discos geridos tooyour máquina no tooAzure de migração.
    - Ver ou modificar as definições de rede, incluindo Olá/sub-rede da rede na qual Olá VM do Azure estarão localizada após a ativação pós-falha e o endereço IP de Olá que será atribuído tooit.

    ![Ativar a replicação](./media/hyper-v-site-walkthrough-test-failover/test-failover4.png)
4. No **discos**, pode ver informações sobre o sistema de operativo Olá e discos de dados no Olá VM.


## <a name="run-a-test-failover"></a>Executar uma ativação pós-falha de teste

Agora, execute um toomake de ativação pós-falha de teste se que tudo está a funcionar conforme esperado.

- Se quiser tooconnect tooAzure VMs com RDP após a ativação pós-falha, [preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - teste de toofully necessita toocopy do Active Directory e DNS no seu ambiente de teste. [Saiba mais](site-recovery-active-directory.md#test-failover-considerations).
 - Para obter informações completas sobre a ativação pós-falha de teste, leia o artigo [neste artigo](site-recovery-test-failover-to-azure.md) artigo.
 
 Agora, execute uma ativação pós-falha:

1. toofail através de uma única máquina no **itens replicados**, clique em Olá VM > **+ ativação pós-falha de teste** ícone.
2. Planear toofail através de uma recuperação, na **planos de recuperação**, plano do contexto Olá > **ativação pós-falha de teste**. toocreate um plano de recuperação, [siga estas instruções](site-recovery-create-recovery-plans.md).
3. No **ativação pós-falha de teste**, selecione Olá rede Azure toowhich VMs do Azure será ligada após a ocorrência da ativação pós-falha.
4. Clique em **OK** toobegin ativação pós-falha de Olá. Pode controlar o progresso clicando na Olá VM tooopen as respetivas propriedades ou na Olá **ativação pós-falha de teste** tarefa no nome do cofre > **tarefas** > **as tarefas de recuperação de Site**.
5. Após a conclusão da ativação pós-falha de Olá, também deve ser capaz de réplica de Olá toosee máquina do Azure são apresentados no Olá portal do Azure > **máquinas virtuais**. Deve Certifique-se de que Olá VM é Olá um tamanho adequado, que tenha ligado toohello adequada de rede, e que está em execução.
6. Se preparou para as ligações após a ativação pós-falha, deve ser capaz de tooconnect toohello VM do Azure.
7. Depois de concluir, clique em **ativação pós-falha de teste de limpeza** no plano de recuperação Olá. No **notas** registar e guardar todas as observações associadas à ativação pós-falha de teste de Olá. Este procedimento eliminará Olá as máquinas virtuais que foram criadas durante a ativação pós-falha de teste.



## <a name="next-steps"></a>Passos seguintes

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de ativações pós-falha e como toorun-los.
- [Leia sobre a reativação pós-falha](site-recovery-failback-from-azure-to-hyper-v.md), toofail back e replicar as VMs do Azure fazer uma cópia de site de Hyper-V no local primário toohello.

