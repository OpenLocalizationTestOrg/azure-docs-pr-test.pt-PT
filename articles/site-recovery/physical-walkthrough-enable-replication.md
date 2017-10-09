---
title: "replicação de aaaEnable para servidores físicos a replicar tooAzure com o Azure Site Recovery | Microsoft Docs"
description: "Resume os passos de Olá precisa tooenable replicação tooAzure para servidores físicos, utilizando o serviço do Azure Site Recovery Olá"
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
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a>Passo 10: Ativar a replicação para servidores físicos tooAzure


Este artigo descreve como tooenable replicação no local Windows/Linux tooAzure servidores físicos, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.

Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

- Servidores têm de ter Olá [componente de serviço de mobilidade instalado](physical-walkthrough-install-mobility.md).
- Se uma VM está preparada para a instalação de push, o servidor de processos de Olá instala automaticamente o serviço de mobilidade Olá ao ativar a replicação.
- Quando ativa uma máquina para a replicação, a sua conta de utilizador do Azure tem específico [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure que está a toouse capaz de armazenamento do Azure e criar as VMs do Azure.
- Quando adiciona ou modifica os endereços IP para servidores, pode demorar até too15 minutos ou já está em vigor tootake de alterações e para os mesmos tooappear no portal de Olá.


## <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por predefinição, todos os discos numa máquina são replicados. Pode excluir discos de replicação. Por exemplo, poderá pretender que os discos de tooreplicate com dados temporários ou dados que foi atualizada sempre que uma máquina ou aplicação reinicia (por exemplo pagefile.sys ou tempdb do SQL Server). [Saiba mais](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a>Replicar servidores

1. Clique em **Passo 2: Replicar aplicação** > **Origem**.
2. No **origem**, selecione o servidor de configuração de Olá.
3. No **máquina tipo**, selecione **máquinas físicas**.
4. Selecione o servidor de processos de Olá. Se ainda não criou quaisquer servidores de processos adicionais este será o servidor de configuração de Olá. Em seguida, clique em **OK**.
5. No **destino**, selecione a subscrição de Olá e Olá o grupo de recursos em que pretende Olá toocreate pós-falha nas VMs. Escolha o modelo de implementação de Olá que pretende toouse no Azure (clássica ou recurso management), para Olá pós-falha nas VMs.
6. Selecione a conta de armazenamento do Azure de Olá que pretende toouse para replicar os dados. Se não quiser toouse uma conta que já configurou, pode criar um novo.
7. Selecione Olá **rede Azure** e **sub-rede** ligar toowhich VMs do Azure após a ativação pós-falha. Selecione **configurar agora para as máquinas selecionadas** tooapply Olá rede definição tooall máquinas selecionadas para proteção. Selecione **configurar mais tarde** tooselect Olá rede do Azure por máquina. Se não quiser toouse uma rede existente, pode criar uma.

    ![Ativar a replicação](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. No **máquinas físicas**, clique em **+ máquina física** e introduza Olá **nome** e **endereço IP**. Escolha o sistema de operativo Olá da máquina de Olá pretende tooreplicate. Demora alguns minutos até que as máquinas são detetadas e apresentadas na lista de Olá.
9. No **propriedades** > **configurar propriedades**, selecione conta Olá que será utilizada pelo tooautomatically de servidor de processo Olá instalar o serviço de mobilidade Olá na máquina de Olá.
10. Por predefinição, todos os discos são replicados. Clique em **todos os discos** e desmarque todos os discos que não pretende tooreplicate. Em seguida, clique em **OK**. Pode definir propriedades VM adicionais mais tarde.

    ![Ativar a replicação](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. No **as definições de replicação** > **configurar as definições de replicação**, certifique-se de que Olá correta está selecionada a política de replicação. Se modificar uma política, as alterações serão aplicadas tooreplicating máquina e toonew máquinas.
12. Ativar **a consistência Multi VM** se pretender toogather máquinas para um grupo de replicação e especificar um nome para o grupo de Olá. Em seguida, clique em **OK**. Tenha em atenção que:

    * Computadores em grupos de replicação replicar em conjunto e tem partilhado pontos de recuperação consistentes com falhas e consistentes da aplicação quando efetuar a ativação pós-falha.
    * Recomendamos que pode reunir servidores físicos, para que estes espelhar as cargas de trabalho. Ativar a consistência de várias VMS pode afetar o desempenho da carga de trabalho e só deve ser utilizada se máquinas estiverem a executar Olá mesma carga de trabalho e necessitar de consistência.

13. Clique em **ativar a replicação**. Pode controlar o progresso de Olá **ativar proteção** da tarefa no **definições** > **tarefas** > **tarefas de recuperação de Site**. Depois de Olá **finalizar proteção** tarefa executa máquina Olá está preparada para ativação pós-falha.

## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 11: executar uma ativação pós-falha de teste](physical-walkthrough-test-failover.md)
