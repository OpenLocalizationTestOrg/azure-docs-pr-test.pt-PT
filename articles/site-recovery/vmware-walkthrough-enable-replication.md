---
title: "replicação aaaEnable para VMs de VMware replicar tooAzure com o Azure Site Recovery | Microsoft Docs"
description: "Resume os passos de Olá terá tooenable replicação tooAzure para VMs de VMware com o serviço do Azure Site Recovery Olá"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a>Passo 11: Ativar a replicação para tooAzure de máquinas virtuais de VMware


Este artigo descreve como tooenable replicação de VMware no local virtual máquinas tooAzure, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.

Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

- VMs de VMware tem de ter Olá [componente de serviço de mobilidade instalado](vmware-walkthrough-install-mobility.md). -Se uma VM está preparada para a instalação de push, o servidor de processos de Olá instala automaticamente o serviço de mobilidade Olá ao ativar a replicação.
- A conta de utilizador do Azure tem específico [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicação de uma VM tooAzure
- Quando adiciona ou modifica as VMs, pode demorar até too15 minutos ou já está em vigor tootake de alterações e para os mesmos tooappear no portal de Olá.
- Pode verificar o tempo Olá pela última vez detetado para VMs no **servidores de configuração** > **último contacto em**.
- tooadd VMs sem aguardar deteção agendada do Olá, servidor de configuração de Olá realce (não clique nele) e clique em **atualizar**.



## <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por predefinição, todos os discos numa máquina são replicados. Pode excluir discos de replicação. Por exemplo, poderá pretender que os discos de tooreplicate com dados temporários ou dados que foi atualizada sempre que uma máquina ou aplicação reinicia (por exemplo pagefile.sys ou tempdb do SQL Server). [Saiba mais](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Replicar VMs

Antes de começar, veja uma rápida descrição geral do vídeo

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Clique em **Passo 2: Replicar aplicação** > **Origem**.
2. No **origem**, selecione o servidor de configuração de Olá.
3. No **máquina tipo**, selecione **máquinas virtuais**.
4. No **vCenter/vSphere hipervisor**, selecione o servidor vCenter Olá que gere anfitriões vSphere de Olá ou selecione Olá anfitrião.
5. Selecione o servidor de processos de Olá. Se ainda não criou quaisquer servidores de processos adicionais este será o servidor de configuração de Olá. Em seguida, clique em **OK**.

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. No **destino**, selecione a subscrição de Olá e Olá o grupo de recursos em que pretende Olá toocreate pós-falha nas VMs. Escolha o modelo de implementação de Olá que pretende toouse no Azure (clássica ou recurso management), para Olá pós-falha nas VMs.


7. Selecione a conta de armazenamento do Azure de Olá que pretende toouse para replicar os dados. Se não quiser toouse uma conta que já configurou, pode criar um novo.

8. Selecione Olá Azure toowhich de rede e sub-rede VMs do Azure irá ligar, quando são criados após a ativação pós-falha. Selecione **configurar agora para as máquinas selecionadas**, tooapply Olá rede definição tooall máquinas selecionadas para proteção. Selecione **configurar mais tarde** tooselect Olá rede do Azure por máquina. Se não quiser toouse uma rede existente, pode criar uma.

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. No **máquinas virtuais** > **selecionar máquinas virtuais**, clique e selecione cada máquina que quiser tooreplicate. Só pode selecionar máquinas para as quais a replicação pode ser ativada. Em seguida, clique em **OK**.

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. No **propriedades** > **configurar propriedades**, selecione conta Olá que será utilizada pelo tooautomatically de servidor de processo Olá instalar o serviço de mobilidade Olá na máquina de Olá.
11. Por predefinição, todos os discos são replicados. Clique em **todos os discos** e desmarque todos os discos que não pretende tooreplicate. Em seguida, clique em **OK**. Pode definir propriedades VM adicionais mais tarde.

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. No **as definições de replicação** > **configurar as definições de replicação**, certifique-se de que Olá correta está selecionada a política de replicação. Se modificar uma política, as alterações serão aplicadas tooreplicating máquina e toonew máquinas.
12. Ativar **a consistência Multi VM** se pretender toogather máquinas para um grupo de replicação e especificar um nome para o grupo de Olá. Em seguida, clique em **OK**. Tenha em atenção que:

    * Computadores em grupos de replicação replicar em conjunto e tem partilhado pontos de recuperação consistentes com falhas e consistentes da aplicação quando efetuar a ativação pós-falha.
    * Recomendamos que pode reunir VMs e servidores físicos, para que estes espelhar as cargas de trabalho. Ativar a consistência de várias VMS pode afetar o desempenho da carga de trabalho e só deve ser utilizada se máquinas estiverem a executar Olá mesma carga de trabalho e necessitar de consistência.

    ![Ativar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. Clique em **ativar a replicação**. Pode controlar o progresso de Olá **ativar proteção** da tarefa no **definições** > **tarefas** > **tarefas de recuperação de Site**. Depois de Olá **finalizar proteção** tarefa executa máquina Olá está preparada para ativação pós-falha.

## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 12: executar uma ativação pós-falha de teste](vmware-walkthrough-test-failover.md)
