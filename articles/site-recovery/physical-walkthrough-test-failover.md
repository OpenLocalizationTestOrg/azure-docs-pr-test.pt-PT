---
title: "aaaRun uma ativação pós-falha de teste para tooAzure de replicação do servidor físico com o Azure Site Recovery | Microsoft Docs"
description: "Resume os passos de Olá que precisa para executar uma ativação pós-falha de teste para [servidores físicos a replicar tooAzure utilizando o serviço do Azure Site Recovery Olá."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f8ed5ce585c5574be3018ce15339c4fd3b527eaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-of-physical-servers-tooazure"></a>Passo 11: Executar uma ativação pós-falha de teste de servidores físicos tooAzure

Este artigo descreve como toorun uma ativação pós-falha de teste do local tooAzure servidores físicos, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.

Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

Antes de executar uma ativação pós-falha de teste, recomendamos que verifique se as propriedades do servidor Olá e efetue as alterações tem. Pode aceder às propriedades VM Olá no **replicado itens**. Olá **Essentials** painel mostra informações sobre as definições da máquina e de estado.

## <a name="managed-disk-considerations"></a>Considerações de disco gerido

[Discos geridos pelo](../virtual-machines/windows/managed-disks-overview.md) simplificar a gestão de discos para VMs do Azure, através da gestão de contas do storage Olá associadas aos discos VM Olá. 

- Quando ativar a proteção para um servidor, os dados VM replicam tooa conta de armazenamento. Discos geridos são criados e ligados toohello VM apenas quando ocorre a ativação pós-falha.
- Discos geridos podem ser criados apenas para as VMs do Azure implementadas utilizando o modelo do Resource Manager Olá.  
- Com esta definição ativada, conjuntos de disponibilidade só na grupos de recursos que tenham **utilize discos geridos pelo** ativada podem ser selecionadas. As VMs com discos geridos têm de ser em conjuntos de disponibilidade com **utilize discos geridos pelo** definido demasiado**Sim**. Se a definição de Olá não está ativada para as VMs, podem ser selecionados apenas conjuntos de disponibilidade em grupos de recursos sem discos geridos ativados.
- [Saiba mais](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) sobre discos geridos e disponibilidade define.
- Se a conta de armazenamento de Olá que utiliza para replicação foi encriptada com a encriptação do serviço de armazenamento, discos geridos não não possível criar durante a ativação pós-falha. Neste caso: não permitir a utilização de discos geridos, ou desative a proteção de VM de Olá e voltar a ativar toouse uma conta de armazenamento que não tem a encriptação ativada. [Saiba mais](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="network-considerations"></a>Considerações de rede

Pode definir o endereço IP de destino Olá para uma VM do Azure criadas após ativação pós-falha.

- Se não fornecer um endereço, Olá máquina a ativação pós-falha utilizará o DHCP.
- Se definir um endereço que não está disponível na ativação pós-falha, a ativação pós-falha não funcionará.
- Olá mesmo endereço IP de destino pode ser utilizado para ativação pós-falha de teste, se o endereço de Olá está disponível na rede de ativação pós-falha de teste de Olá.
- número de Olá dos adaptadores de rede é ditado pelo tamanho de Olá especificado para a máquina virtual de destino Olá:

     - Se Olá o número de adaptadores de rede na máquina de origem Olá é Olá igual ou inferior ao número de Olá de adaptadores permitido para o tamanho da máquina de destino Olá, em seguida, terá de destino Olá Olá o mesmo número de adaptadores que origem Olá.
     - Se número de Olá de adaptadores Olá máquina virtual de origem exceder o número de Olá permitido para o tamanho de destino Olá, será utilizado o tamanho máximo de Olá destino.
     - Por exemplo, se uma máquina de origem tiver dois adaptadores de rede e tamanho da máquina Olá destino suporta quatro, a máquina de destino Olá terá dois adaptadores. Se Olá máquina de origem tiver dois adaptadores, mas hello tamanho de destino só suporta um computador de destino Olá terá apenas um adaptador.     
   - Se a máquina virtual de Olá tem vários adaptadores de rede, todos serão ligados toohello mesma rede.
   - Se a máquina virtual de Olá tem vários adaptadores de rede, em seguida, Olá primeiro mostrado na lista de Olá torna-se Olá *predefinido* adaptador de rede no Olá máquina virtual do Azure.
 - [Saiba mais](vmware-walkthrough-network.md) sobre endereçamento IP.



## <a name="view-and-modify-vm-settings"></a>Ver e modificar as definições da VM

Recomendamos que verifique as propriedades de Olá hello do servidor de origem antes de executar uma ativação pós-falha.

1. No **itens protegidos**, clique em **itens replicados**e clique Olá máquina.
2. No Olá **replicados item** painel, pode ver um resumo das informações da máquina, o estado de funcionamento e pontos de recuperação disponível mais recentes do Olá. Clique em **propriedades** tooview mais detalhes.
3. No **computação e rede**, pode:
    - Modificar o nome da VM do Azure de Olá. nome de Olá têm de cumprir [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Especifique uma pós-falha [grupo de recursos].
    - Especifique um tamanho de destino para Olá VM do Azure
    - Selecione um [conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md).
    - Especifique se toouse [discos geridos pelo](#managed-disk-considerations). Selecione **Sim**, se pretender que tooattach discos geridos tooyour máquina no tooAzure de migração.
    - Ver ou modificar as definições de rede, incluindo Olá/sub-rede da rede na qual Olá VM do Azure estarão localizada após a ativação pós-falha e o endereço IP de Olá que será atribuído tooit.
4. No **discos**, pode ver informações sobre o sistema de operativo Olá e discos de dados no Olá VM.

## <a name="run-a-test-failover"></a>Executar uma ativação pós-falha de teste

Depois de que configurou tudo, execute um toomake de ativação pós-falha de teste se que tudo está a funcionar conforme esperado.

- Se quiser tooconnect tooAzure VMs com RDP após a ativação pós-falha, [preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - teste de toofully necessita toocopy do Active Directory e DNS no seu ambiente de teste. [Saiba mais](site-recovery-active-directory.md#test-failover-considerations).
 - Para obter informações completas sobre a ativação pós-falha de teste, leia o artigo [neste artigo](site-recovery-test-failover-to-azure.md) artigo.
- Obter uma descrição geral do vídeo rápida antes de começar:

     
     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]

Agora, execute uma ativação pós-falha:

1. toofail através de uma única máquina no **definições** > **itens replicados**, clique Olá máquina > **+ ativação pós-falha de teste** ícone.

    ![Ativação pós-falha de teste](./media/physical-walkthrough-test-failover/test-failover.png)

2. Planear toofail através de uma recuperação, na **definições** > **planos de recuperação**, plano do contexto Olá > **ativação pós-falha de teste**. toocreate um plano de recuperação, [siga estas instruções](site-recovery-create-recovery-plans.md).  

3. No **ativação pós-falha de teste**, selecione Olá rede Azure toowhich VMs do Azure será ligada após a ocorrência da ativação pós-falha.

4. Clique em **OK** toobegin ativação pós-falha de Olá. Pode controlar o progresso clicando na Olá máquina tooopen as respetivas propriedades ou na Olá **ativação pós-falha de teste** tarefa no nome do cofre > **definições** > **tarefas**  >  **As tarefas de recuperação de site**.

5. Após a conclusão da ativação pós-falha de Olá, também deve ser capaz de toosee réplica de Olá VM do Azure são apresentados no portal do Azure de Olá > **máquinas virtuais**. Deve Certifique-se de que Olá VM é Olá um tamanho adequado, que tenha ligado toohello adequada de rede, e que está em execução.

6. Se preparou para as ligações após a ativação pós-falha, deve ser capaz de tooconnect toohello VM do Azure.

### <a name="delete-test-failover-vms"></a>Eliminar a ativação pós-falha de teste VMs

1. Depois de concluir, clique em **ativação pós-falha de teste de limpeza** no plano de recuperação Olá ou numa máquina.
2. No **notas**, registar e guardar todas as observações associadas à ativação pós-falha de teste de Olá.
3. ação de limpeza de Olá elimina as VMs do Azure que foram criadas durante a ativação pós-falha de teste.

## <a name="summary"></a>Resumo

Se concluir com êxito a ativação pós-falha de teste de Olá, os servidores físicos estiver a replicar e tiver verificado que pode efetuar a ativação pós-falha tooAzure. Agora, pode executar as ativações pós-falha de acordo com os requisitos da sua organização. 

Lembre-se de que atualmente não pode falhar novamente a partir do servidor físico tooa do Azure. Ter toofail fazer uma cópia tooa VM de VMware. Isto significa que terá de uma infraestrutura do VMware no local em back toofail de ordem. [Saiba mais](site-recovery-failback-azure-to-vmware.md) sobre falhar back tooVMware de VMs do Azure.


## <a name="next-steps"></a>Passos seguintes

- [Executar as ativações pós-falha](site-recovery-failover.md) conforme necessário.
