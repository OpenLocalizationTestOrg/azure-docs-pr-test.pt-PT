---
title: "Primeira impressão: proteger VMs do Azure com o cofre de serviços de recuperação | Microsoft Docs"
description: "Proteger VMs do Azure com um cofre de serviços de recuperação. Utilize cópias de segurança de VMs implementadas no Resource Manager, VMs implementadas clássica e VMs do Premium Storage, VMs encriptados, VMs em discos geridos tooprotect os dados. Crie e registe um cofre dos serviços de recuperação. Registe VMs, crie uma política e proteja VMs no Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>Criar cópias de segurança cofres dos serviços de tooRecovery de máquinas virtuais do Azure
> [!div class="op_single_selector"]
> * [Proteger VMs com um cofre dos serviços de recuperação](backup-azure-vms-first-look-arm.md)
> * [Proteger VMs com um cofre das cópias de segurança](backup-azure-vms-first-look.md)
>
>

Este tutorial guia-o pelos passos Olá para criar um cofre dos serviços de recuperação e cópia de segurança de uma máquina virtual do Azure (VM). Os cofres dos serviços de recuperação protegem:

* VMs implementadas pelo Azure Resource Manager
* VMs clássicas
* VMs de armazenamento standard
* VMs do Premium Storage
* VMs em execução em Managed Disks
* VMs encriptadas através do Azure Disk Encryption, com BEK e KEK
* Cópia de segurança consistente com a aplicação das VMs Windows utilizando VMs VSS e Linux que utilizam scripts de instantâneos anteriores e instantâneos posteriores personalizados

Para obter mais informações sobre a proteção de VMs do Premium storage, consulte o artigo de Olá, [cópia de segurança e restaurar VMs do Premium Storage](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup). Para obter mais informações sobre o suporte para VMs de discos geridos, veja [Criar cópias de segurança e restauro de VMs em discos geridos](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). Para obter mais informações sobre arquitetura de scripts anteriores e posteriores para cópias de segurança de VM Linux veja [Cópia de segurança consistente com a aplicação da VM Linux com o script anterior e o script posterior] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).

toofind mais sobre o que pode cópia de segurança, e que não é possível, consulte [aqui](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> Este tutorial assume que já tem uma VM na sua subscrição do Azure e que tomou medidas tooallow Olá serviço cópia de segurança tooaccess Olá VM.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

Dependendo do número de Olá de máquinas virtuais que pretende tooprotect, pode começar a partir de diferentes pontos de partida. Se quiser tooback várias máquinas virtuais numa operação de cópia de segurança, aceda a cofre dos serviços de recuperação toohello e [tarefa de cópia de segurança de Olá iniciar a partir do dashboard do Cofre de Olá](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault). Se quiser tooback segurança uma única máquina virtual, pode iniciar a tarefa de cópia de segurança de Olá a partir do painel de gestão de VM.

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>Configurar a tarefa de cópia de segurança de Olá a partir do painel de gestão de VM Olá

Utilize Olá seguintes tarefa de cópia de segurança passos tooconfigure Olá de painel de gestão de máquina virtual de Olá no Olá portal do Azure. Estes passos não aplicam toohello máquinas de virtuais no portal clássico Olá.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. No menu do Hub de Olá, clique em **mais serviços** e, na caixa de diálogo de filtro Olá, escreva **máquinas virtuais**. À medida que escreve, Olá lista de filtros de recursos. Quando vir Máquinas Virtuais, selecione-as.

  ![No Hub menu, clique em caixa de diálogo do mais serviços tooopen texto e, escreva as máquinas virtuais](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  é apresentada a lista de Olá das máquinas virtuais (VM) na subscrição Olá.

  ![é apresentada a lista de Olá das VMs na subscrição Olá.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. Na lista de Olá, selecione uma VM tooback cópias de segurança.

  ![é apresentada a lista de Olá das VMs na subscrição Olá.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Quando seleciona Olá VM, lista de Olá de máquinas virtuais desvia toohello esquerda e o painel de gestão de máquina virtual de Olá e o dashboard de máquina virtual de Olá, abrir. </br>
 ![Painel de gestão da VM](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. No painel de gestão de VM de Olá, no Olá **definições** secção, clique em **cópia de segurança**. </br>

  ![Opção Cópia de Segurança no painel de gestão da VM](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  é aberto o painel de cópia de segurança do Olá ativar.

  ![Opção Cópia de Segurança no painel de gestão da VM](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Para o Cofre de serviços de recuperação Olá, clique em **selecionar existente** e escolher Olá cofre Olá na lista pendente.

  ![Assistente para Ativar Cópia de Segurança](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  Se não existem nenhum cofres dos serviços de recuperação ou, se quiser toouse um novo cofre, clique em **criar nova** e forneça o nome de Olá para novo cofre de Olá. Um novo cofre é criado na Olá mesmo grupo de recursos e a mesma localização da máquina virtual de Olá. Se quiser toocreate um cofre dos serviços de recuperação com valores diferentes, consulte a secção de Olá sobre como demasiado[criar um cofre dos serviços de recuperação](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).

6. detalhes de Olá tooview de Olá política de cópia de segurança, clique em **política de cópia de segurança**.

  Olá **política de cópia de segurança** painel abre-se e fornece detalhes de Olá da política de Olá selecionado. Se existirem outras políticas, utilize o menu pendente de Olá toochoose uma política de cópia de segurança diferentes. Se pretender toocreate uma política, selecione **criar novo** no menu de Olá pendente. Para obter instruções sobre como definir uma política de cópia de segurança, consulte o artigo [Definir uma política de cópia de segurança](backup-azure-vms-first-look-arm.md#defining-a-backup-policy). política cópia de segurança do toosave Olá alterações toohello e retorno toohello ativar cópia de segurança painel, clique em **OK**.

  ![Selecionar política de cópia de segurança](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. No painel de cópia de segurança de ativar Olá, clique em **ativar a cópia de segurança** política de Olá toodeploy. Implementar política de Olá, associa-o com o Cofre de Olá e Olá máquinas de virtuais.

  ![Botão Ativar cópia de segurança](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. Pode controlar o progresso de configuração de Olá através de notificações de Olá que são apresentados no portal de Olá. Olá seguinte exemplo mostra que a implementação iniciada.

  ![Notificação de Ativar Cópia de Segurança](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Depois de progresso da configuração de Olá concluída, no painel de gestão de VM Olá, clique em **cópia de segurança** painel de Item de cópia de segurança de Olá tooopen e vista Olá detalhes.

  ![Vista de Item de Cópia de Segurança da VM](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Até que concluiu a cópia de segurança inicial Olá, **última cópia de segurança estado** mostra como **aviso (cópia de segurança inicial pendente)**. ocorre toosee quando Olá agendado o próximo tarefa de cópia de segurança, em **política de cópia de segurança** clique Olá nome da política de Olá. Painel de política de cópia de segurança de Olá abre e apresenta o tempo de Olá de cópia de segurança agendada Olá.

10. toorun uma cópia de segurança da tarefa e criar ponto de recuperação inicial Olá, no Olá cópia de segurança do Cofre Painel clique **cópia de segurança agora**.

  ![Clique em cópia de segurança no agora toorun Olá inicial cópia de segurança](./media/backup-azure-vms-first-look-arm/backup-now.png)

  é aberto o painel cópia de segurança agora Olá.

  ![Mostra o painel cópia de segurança agora Olá](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. Olá cópia de segurança agora painel, clique em ícone de calendário Olá, utilize o Olá de tooselect de controlo do Olá calendário último dia deste ponto de recuperação é mantido e clique em **cópia de segurança**.

  ![Definir Olá último dia Olá agora de cópia de segurança do ponto de recuperação é retido](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Notificações de implementação informá-lo a tarefa de cópia de segurança de Olá foi acionada e que pode monitorizar o progresso de Olá da tarefa de Olá na página de tarefas de cópia de segurança de Olá.

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>Configurar a tarefa de cópia de segurança de Olá de Olá que cofre dos serviços de recuperação
tarefa de cópia de segurança do tooconfigure Olá, concluir Olá os seguintes passos.  

1. Crie um cofre dos Serviços de Recuperação para uma máquina virtual.
2. Olá utilize tooselect portal do Azure num cenário, definir uma política de cópia de segurança e identificar itens tooprotect.
3. Execute cópia de segurança inicial Olá.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Criar um cofre dos Serviços de Recuperação para uma VM
Um cofre dos serviços de recuperação é uma entidade que armazena todas as cópias de segurança de Olá e pontos de recuperação que foram criados ao longo do tempo. Olá cofre dos serviços de recuperação também contém política de cópia de segurança Olá aplicada toohello protegidos VMs.

> [!NOTE]
> A criação de cópias de segurança de VMs é um processo local. Não é possível criar cópias de segurança VMs a partir do Cofre de serviços de recuperação de tooa de uma localização noutra localização. Por isso, para cada localização do Azure que tenha toobe VMs uma cópia de segurança, pelo menos um cofre de serviços de recuperação tem de existir nessa localização.
>
>

toocreate um cofre dos serviços de recuperação:

1. Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com/) através da sua subscrição do Azure.
2. No menu do Hub de Olá, clique em **mais serviços** e no tipo de caixa de diálogo de filtro de Olá **dos serviços de recuperação**. À medida que escreve, Olá lista de filtros de recursos. Quando vir os cofres dos serviços de recuperação na lista de Olá, clique na mesma.

    ![Passo 1 da Criação de um Cofre dos Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Se existirem cofres dos serviços de recuperação na subscrição Olá, cofres Olá são listados.

    ![Passo 2 da Criação do Cofre dos Serviços de Recuperação](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. No Olá **cofres dos serviços de recuperação** menu, clique em **adicionar**.

    ![Passo 2 da Criação do Cofre dos Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    é aberto o painel do cofre dos serviços de recuperação Olá que lhe pede tooprovide um **nome**, **subscrição**, **grupo de recursos**, e **localização**.

    ![Passo 3 da Criação de um Cofre dos Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Para **nome**, introduza um cofre de Olá tooidentify nome amigável. nome de Olá tem toobe exclusivo para Olá subscrição do Azure. Escreva um nome que contenha entre 2 e 50 carateres. Tem de começar com uma letra e pode conter apenas letras, números e hífenes.

5. No Olá **subscrição** secção, utilize Olá de toochoose Olá menu pendente subscrição do Azure. Se utilizar apenas uma subscrição, essa subscrição é apresentado e poderá avançar toohello próximo passo. Se não tiver a certeza de que toouse de subscrição, utilize a predefinição de Olá (ou sugerida) subscrição. Terá várias escolhas apenas se a sua conta organizacional estiver associada a várias subscrições do Azure.

6. No Olá **grupo de recursos** secção:

    * Selecione **criar nova** se quiser toocreate um grupo de recursos.
    Ou
    * Selecione **utilizar existente** e clique em Olá menu pendente toosee Olá disponíveis lista de grupos de recursos.

  Para obter informações completas sobre os grupos de recursos, consulte Olá [descrição geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

7. Clique em **localização** tooselect região geográfica do Olá para o Cofre de Olá. Esta escolha determina a região geográfica olá onde são enviados os dados de cópia de segurança.

  > [!IMPORTANT]
  > Se não souber de localização de Olá na qual existe a VM, feche a caixa de diálogo de criação Olá cofre e aceda toohello lista de máquinas virtuais no portal de Olá. Se tiver máquinas virtuais em várias regiões, crie um cofre dos Serviços de Recuperação em cada região. Crie o Cofre de Olá na localização primeiro Olá antes de avançar toohello de localização seguinte. Não existe que nenhuma conta de armazenamento necessário toospecify Olá utilizado dados de cópia de segurança de Olá toostore – Cofre de serviços de recuperação de Olá e Olá serviço cópia de segurança do Azure processam automaticamente armazenamento Olá.
  >

8. Na Olá parte inferior do painel do Cofre de serviços de recuperação de Olá, clique em **criar**.

    Pode demorar alguns minutos para Olá que toobe criado do cofre dos serviços de recuperação. Monitorizar as notificações de estado de Olá na área superior direita Olá do portal de Olá. Assim que o Cofre for criado, aparece na lista de Olá de cofres dos serviços de recuperação. Se depois de vários minutos não vir o cofre, clique em **Atualizar**.

    ![Clique no botão Atualizar](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Quando vir o Cofre na lista de Olá de cofres dos serviços de recuperação, são redundância de armazenamento de Olá tooset pronto.

Agora que criou o seu Cofre, saiba como tooset Olá replicação de armazenamento.

### <a name="set-storage-replication"></a>Definir Replicação de Armazenamento
opção de replicação de armazenamento Olá permite-lhe toochoose entre o armazenamento georredundante e localmente redundante. Por predefinição, o seu cofre tem um armazenamento georredundante. Se Olá cofre dos serviços de recuperação é a cópia de segurança primária, deixe Olá armazenamento replicação opção set toogeo armazenamento com redundância. Escolha o armazenamento localmente redundante se pretender uma opção mais barata e com menos duração. Leia mais sobre [georredundante](../storage/common/storage-redundancy.md#geo-redundant-storage) e [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opções de armazenamento Olá [descrição geral da replicação de armazenamento do Azure](../storage/common/storage-redundancy.md).

definição de replicação de armazenamento de Olá tooedit:

1. De Olá **cofres dos serviços de recuperação** painel, o novo cofre de Olá selecione.

  ![Selecione o novo cofre de Olá da lista de Olá do Cofre de serviços de recuperação](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Quando seleciona o Cofre de Olá, Olá painel Definições (*que tem o nome do Cofre de Olá na parte superior do Olá*) e o painel de detalhes de cofre Olá aberta.

  ![Configuração de armazenamento de Olá de vista de novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. No painel de definições do cofre Olá novo, utilize Olá gradualmente vertical tooscroll baixo toohello secção Gerir e clique em **infraestrutura de cópia de segurança**.
    é aberto o painel de infraestrutura de cópia de segurança de Olá.
3. No painel de infraestrutura de cópia de segurança de Olá, clique em **configuração de cópia de segurança** tooopen Olá **configuração de cópia de segurança** painel.

    ![Configuração de armazenamento do conjunto de Olá para novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Escolha a opção de replicação de armazenamento adequado Olá para o cofre.

    ![opções de configuração de armazenamento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Por predefinição, o seu cofre tem um armazenamento georredundante. Se utilizar o Azure como um ponto final de armazenamento de cópia de segurança primário, continue a toouse **georredundante**. Se não utilizar o Azure como um ponto final de armazenamento de cópia de segurança primário, em seguida, escolha **localmente redundante**, que reduz os custos de armazenamento do Azure Olá. Leia mais sobre as opções de armazenamento [georredundante](../storage/common/storage-redundancy.md#geo-redundant-storage) e [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) nesta [Descrição geral de redundância de armazenamento](../storage/common/storage-redundancy.md).


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Selecionar um objetivo de cópia de segurança, defina a política e definir tooprotect de itens
Antes de registar uma VM com um cofre, execute tooensure de processo de deteção de Olá que as novas máquinas virtuais que foram adicionadas toohello subscrição são identificadas. Olá processo consulta o Azure para Olá obter lista de máquinas virtuais na subscrição Olá, juntamente com informações adicionais, como o nome do serviço de nuvem de Olá e região Olá. No portal do Azure Olá, cenário refere-se toowhat vai tooput no Cofre de serviços de recuperação Olá. A política é agenda Olá frequência e quando são tirados pontos de recuperação. A política também inclui o período de retenção de Olá Olá pontos de recuperação.

1. Se já tiver dos serviços de recuperação cofre abrir, avance toostep 2. Caso contrário, no menu do Hub de Olá, clique em **mais serviços** e, na lista de Olá de recursos, escreva **dos serviços de recuperação** e clique em **cofres dos serviços de recuperação**.

    ![Passo 1 da Criação de um Cofre dos Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    é apresentada a lista de Olá de cofres dos serviços de recuperação.

    ![Lista de cofres dos vista de Olá dos serviços de recuperação](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Na lista de Olá dos cofres dos serviços de recuperação, selecione um cofre tooopen seu dashboard.

     ![Abrir painel do cofre](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. No menu do dashboard de Olá cofre, clique em **cópia de segurança** painel de cópia de segurança de Olá tooopen.

    ![Abrir o painel Backup](./media/backup-azure-arm-vms-prepare/backup-button.png)

    painéis de cópia de segurança e o objetivo de cópia de segurança de Olá abrir.

    ![Abrir o painel Cenário](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. No painel objetivo de cópia de segurança de Olá, de Olá **onde está a carga de trabalho em execução** menu pendente, selecione Azure. De Olá **que itens pretende toobackup** pendente, selecione a Máquina Virtual, em seguida, clique em **OK**.

    Estas ações registar a extensão da VM Olá Vault Olá. Olá objetivo de cópia de segurança fecha de painel e Olá **política de cópia de segurança** abre o painel.

    ![Abrir o painel Cenário](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. No painel de política de cópia de segurança de Olá, selecione a política de cópia de segurança Olá pretende tooapply toohello cofre.

    ![Selecionar política de cópia de segurança](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    detalhes de Olá da política predefinida do Olá estão listados na menu pendente de Olá. Se pretender toocreate uma política, selecione **criar novo** no menu de Olá pendente. Para obter instruções sobre como definir uma política de cópia de segurança, consulte o artigo [Definir uma política de cópia de segurança](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Clique em **OK** política de cópia de segurança Olá tooassociate Vault Olá.

    Olá fechar de painel de política de cópia de segurança e Olá **selecionar máquinas virtuais** abre o painel.
5. No Olá **selecionar máquinas virtuais** painel, escolha Olá tooassociate de máquinas virtuais com Olá especificado política e clique em **OK**.

    ![Selecionar a carga de trabalho](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    máquina virtual de Olá selecionado está validada. Se não vir Olá virtual máquinas esperado toosee, verifique se existem no Olá mesma localização do Azure como o Cofre dos serviços de recuperação Olá. localização de Olá de Olá que cofre dos serviços de recuperação é apresentada no dashboard do Cofre de Olá.

6. Agora que definiu todas as definições para o Cofre de Olá, no painel de cópia de segurança de Olá, clique em **ativar Backup** toodeploy Olá cofre toohello de política e Olá VMs. Implementar a política de cópia de segurança de Olá não criar um ponto de recuperação inicial Olá para a máquina virtual de Olá.

    ![Ativar Backup](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Depois de ativar a cópia de segurança de Olá com êxito, a política de cópia de segurança será executado numa agenda. No entanto, continuar a tarefa de cópia de segurança tooinitiate Olá primeiro.

## <a name="initial-backup"></a>Cópia de segurança inicial
Assim que foi implementada uma política de cópia de segurança na máquina virtual Olá, que não significa que os dados de Olá tem uma cópia de segurança. Por predefinição, Olá primeira cópia de segurança agendada (conforme definido na política de cópia de segurança de Olá) é Olá cópia de segurança inicial. Até que ocorra a cópia de segurança inicial Olá, Olá último Estado da cópia de segurança no Olá **as tarefas de cópia de segurança** painel mostra como **aviso (cópia de segurança inicial pendente)**.

![Cópia de segurança pendente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

A menos que a cópia de segurança inicial toobegin em breve, é recomendado que execute **criar cópias de segurança agora**.

toorun Olá inicial tarefa de cópia:

1. No dashboard do Cofre de Olá, clique em número Olá em **itens de cópia de segurança**, ou clique em Olá **itens de cópia de segurança** mosaico. <br/>
  Ícone Definições![](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Olá **itens de cópia de segurança** abre o painel.

  ![Itens de cópia de segurança](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. No Olá **itens de cópia de segurança** painel, item de Olá selecione.

  ![Ícone Definições](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Olá **itens de cópia de segurança** lista é aberto. <br/>

  ![Tarefa de cópia de segurança acionada](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. No Olá **itens de cópia de segurança** lista, clique nas reticências de Olá **...**  menu de contexto de Olá tooopen.

  ![Menu Contexto](./media/backup-azure-vms-first-look-arm/context-menu.png)

  é apresentado o menu de contexto de Olá.

  ![Menu Contexto](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. No menu de contexto de Olá, clique em **cópia de segurança agora**.

  ![Menu Contexto](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  é aberto o painel cópia de segurança agora Olá.

  ![Mostra o painel cópia de segurança agora Olá](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Olá cópia de segurança agora painel, clique em ícone de calendário Olá, utilize o Olá de tooselect de controlo do Olá calendário último dia deste ponto de recuperação é mantido e clique em **cópia de segurança**.

  ![Definir Olá último dia Olá agora de cópia de segurança do ponto de recuperação é retido](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Notificações de implementação informá-lo a tarefa de cópia de segurança de Olá foi acionada e que pode monitorizar o progresso de Olá da tarefa de Olá na página de tarefas de cópia de segurança de Olá. Dependendo do tamanho de Olá da sua VM, criar cópia de segurança inicial Olá poderá demorar algum tempo.

6. o estado de Olá tooview ou controlar de Olá cópia de segurança inicial, no dashboard do cofre Olá, no Olá **as tarefas de cópia de segurança** mosaico clique **em curso**.

  ![Mosaico Tarefas de cópia de segurança](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  é aberto o painel de tarefas de cópia de segurança de Olá.

  ![Mosaico Tarefas de cópia de segurança](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  No Olá **tarefas de cópia de segurança** painel, pode ver o estado de Olá de todas as tarefas. Verifique se a tarefa de cópia de segurança de Olá para a VM ainda está em curso ou se foi concluída. Quando uma tarefa de cópia de segurança estiver concluída, o estado de Olá é *concluído*.

  > [!NOTE]
  > Como parte da operação de cópia de segurança de Olá, Olá serviço cópia de segurança do Azure emite uma extensão de cópia de segurança de toohello comando em cada tooflush VM todas as escritas e tirar um instantâneo consistente.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Instalar Olá agente da VM na máquina virtual de Olá
Estas informações são fornecidas no caso de serem necessárias. Olá agente da VM do Azure tem de estar instalado na máquina virtual do Azure para toowork de extensão de cópia de segurança de Olá de Olá. No entanto, se a VM foi criada a partir de Olá galeria do Azure, em seguida, Olá agente da VM já se encontra presente na máquina virtual de Olá. VMs que são migradas dos centros de dados no local seria não tiver Olá agente da VM instalado. Neste caso, Olá agente da VM tem toobe instalado. Se tiver problemas a cópia de segurança Olá VM do Azure, verifique se Olá agente da VM do Azure está corretamente instalado na máquina virtual de Olá (consulte Olá a tabela seguinte). Se criar uma VM personalizada, [Certifique-se Olá **Olá instalar agente da VM** caixa de verificação está selecionada](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) antes de máquina virtual de Olá está aprovisionada.

Saiba mais sobre Olá [agente da VM](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) e [como tooinstall-](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Olá, a tabela seguinte fornece informações adicionais sobre o agente de VM Olá para Windows e VMs com Linux.

| **Operação** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalar Olá agente da VM |<li>Transfira e instale Olá [MSI do agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Terá de instalação de Olá de toocomplete de privilégios de administrador. <li>[Atualizar a propriedade da VM Olá](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate Olá agente está instalado. |<li> Instale os mais recentes Olá [agente Linux](https://github.com/Azure/WALinuxAgent) a partir do GitHub. Terá de instalação de Olá de toocomplete de privilégios de administrador. <li> [Atualizar a propriedade da VM Olá](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate Olá agente está instalado. |
| Atualizar Olá agente da VM |Olá atualizar agente da VM é tão simple como reinstalar Olá [binários do agente da VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Certifique-se de que nenhuma operação de cópia de segurança está em execução enquanto o agente da VM Olá está a ser atualizado. |Siga as instruções de Olá no [atualizar Olá agente da VM com Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br>Certifique-se de que nenhuma operação de cópia de segurança está em execução ao hello que agente VM está a ser atualizado. |
| A validar a instalação do agente de VM de Olá |<li>Navegue toohello *C:\WindowsAzure\Packages* pasta Olá VM do Azure. <li>Deverá considerar o ficheiro do Olá WaAppAgent.exe presente.<li> Clique no ficheiro de Olá, visite demasiado**propriedades**e, em seguida, selecione Olá **detalhes** campo de versão de produto do separador. Olá deve ser 2.6.1198.718 ou superior. |N/D |

### <a name="backup-extension"></a>Extensão da cópia de segurança
Uma vez Olá que agente VM está instalado na máquina virtual de Olá, Olá serviço cópia de segurança do Azure instala a extensão de cópia de segurança de Olá toohello agente da VM. Olá serviço cópia de segurança do Azure perfeitamente atualiza e extensão de cópia de segurança de Olá sem intervenção do utilizador adicional de patches.

serviço de cópia de segurança de Olá instala a extensão de cópia de segurança Olá, mesmo se Olá VM não está em execução. Uma VM em execução fornece a maior possibilidade de Olá de obter um ponto de recuperação consistentes com aplicações. No entanto, Olá serviço de cópia de segurança do Azure continua tooback segurança Olá VM mesmo se está a ser desativada e não foi possível instalar a extensão de Olá. Este tipo de cópia de segurança é conhecido como Offline VM e o ponto de recuperação Olá *consistente com a falha*.

## <a name="troubleshooting-information"></a>Informações sobre a resolução de problemas
Se tiver problemas ao realizar algumas das tarefas de Olá neste artigo, consulte o [orientações de resolução de problemas](backup-azure-vms-troubleshoot.md).

## <a name="pricing"></a>Preços
custo de Olá de cópia de segurança de VMs do Azure é com base no número de Olá de instâncias protegidas. Para uma definição de instância protegida, veja [o que é uma instância protegida](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Para obter um exemplo de calcular o custo de Olá de cópia de segurança de uma máquina virtual, consulte [como são instâncias protegidas calculadas](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances). Consulte Olá preços da cópia de segurança do Azure página para obter informações sobre [preços da cópia de segurança](https://azure.microsoft.com/pricing/details/backup/).

## <a name="questions"></a>Tem dúvidas?
Se tiver dúvidas ou se não houver qualquer funcionalidade que gostaria de toosee incluído, [envie-nos comentários](http://aka.ms/azurebackup_feedback).
