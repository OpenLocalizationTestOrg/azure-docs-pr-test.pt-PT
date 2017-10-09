---
title: aaaStorSimple Snapshot Manager e os volumes | Microsoft Docs
description: "Descreve como toouse Olá Snapshot Manager do StorSimple MMC snap-in tooview e gerir volumes e tooconfigure cópias de segurança."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>Utilize o Snapshot Manager do StorSimple tooview e gira volumes
## <a name="overview"></a>Descrição geral
Pode utilizar Olá Snapshot Manager do StorSimple **Volumes** nó (no Olá **âmbito** painel) tooselect volumes e ver informações sobre os mesmos. volumes de Olá são apresentados como unidades que correspondem volumes toohello montados pelo anfitrião Olá. Olá **Volumes** nós mostra volumes locais e tipos de volume que são suportados pelo StorSimple, incluindo volumes detetados através da utilização de Olá de iSCSI e um dispositivo. 

Para mais informações sobre volumes suportados, visite demasiado[suporte para vários tipos de volume](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).

![Lista de volume no painel de resultados](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

Olá **Volumes** nós também permite-lhe reanalise ou elimine volumes depois Snapshot Manager do StorSimple Deteta-os. 

Este tutorial explica como montar, inicializar e formatar volumes e, em seguida, utilizar o Snapshot Manager do StorSimple para:

* Ver informações sobre volumes 
* Elimine volumes
* Reanalisar volumes 
* Configurar um volume básico e faça uma cópia de
* Configurar um volume espelhado dinâmico e faça uma cópia de

> [!NOTE]
> Todos os Olá **Volume** ações de nó também estão disponíveis no Olá **ações** painel.
> 
> 

## <a name="mount-volumes"></a>Montar os volumes
Olá de utilização seguintes procedimento toomount, inicializar e formatar volumes do StorSimple. Este procedimento utiliza a gestão de discos, um utilitário de sistema para a gestão de discos rígidos e volumes correspondentes Olá ou partições. Para mais informações sobre a gestão de discos, visite demasiado[gestão de discos](https://technet.microsoft.com/library/cc770943.aspx) no Web site do Microsoft TechNet Olá.

#### <a name="toomount-volumes"></a>toomount volumes
1. No computador anfitrião, inicie o Iniciador do iSCSI Olá Microsoft.
2. Forneça um dos endereços IP de interface de Olá como o portal de destino Olá ou endereço IP de deteção e ligar o dispositivo toohello. Depois do dispositivo de Olá está ligado, volumes Olá será sistema do Windows tooyour acessível. Para obter mais informações sobre como utilizar o Iniciador do iSCSI Olá Microsoft, aceda toohello secção "Ligar tooan iSCSI dispositivo-alvo" [iniciador iSCSI instalar e configurar o Microsoft][1].
3. Utilize qualquer uma das seguintes opções toostart gestão de discos de Olá:
   
   * Escreva Diskmgmt.msc Olá **executar** caixa.
   * Inicie o Gestor de servidor, expanda Olá **armazenamento** nó e, em seguida, selecione **gestão de discos**.
   * Iniciar **ferramentas administrativas**, expanda Olá **gestão de computadores** nó e, em seguida, selecione **gestão de discos**. 
     
     > [!NOTE]
     > Tem de utilizar toorun de privilégios de administrador gestão de discos.
     > 
     > 
4. Efetue Olá volumes online:
   
   1. Na gestão de discos, clique com botão direito qualquer volume marcado **Offline**.
   2. Clique em **reativar disco**. disco Olá deverá ser marcado **Online** depois do disco de Olá é reativado.
5. Inicializar Olá volumes:
   
   1. Clique com botão direito volumes Olá detetado.
   2. No menu de Olá, selecione **Inicializar disco**.
   3. No Olá **Inicializar disco** caixa de diálogo, discos Olá Selecione se pretende tooinitialize e, em seguida, clique em **OK**.
6. Formatar volumes simples:
   
   1. Faça duplo clique num volume que pretende que o tooformat.
   2. No menu de Olá, selecione **Novo Volume simples**.
   3. Utilize o volume do Olá Novo Volume simples assistente tooformat Olá:
      
      * Especifique o tamanho do volume Olá.
      * Forneça uma letra de unidade.
      * Selecione o sistema de ficheiros NTFS Olá.
      * Especifique um tamanho de unidade de alocação de 64 KB.
      * Efetue uma formatação rápida.
7. Formatar partição vários volumes. Para obter instruções, aceda toohello secção, "Partições e Volumes" [implementar a gestão de discos](https://msdn.microsoft.com/library/dd163556.aspx).

## <a name="view-information-about-your-volumes"></a>Ver informações sobre os volumes
Utilize Olá seguir o procedimento tooview sobre local e os volumes de Azure StorSimple.

#### <a name="tooview-volume-information"></a>informações de volume tooview
1. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple. 
2. No Olá **âmbito** painel, clique em Olá **Volumes** nós. É apresentada uma lista de volumes locais e montados, incluindo todos os volumes de Azure StorSimple, no Olá **resultados** painel. Olá colunas na Olá **resultados** painel são configuráveis. (Contexto Olá **Volumes** nó, selecione **vista**e, em seguida, selecione **Adicionar/remover colunas**.)
   
    ![Configurar Olá colunas](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | Coluna de resultados | Descrição |
   |:--- |:--- |
   |  Nome |Olá **nome** coluna contém Olá unidade letra atribuída tooeach detetado volume. |
   |  Dispositivo |Olá **dispositivo** coluna contém o endereço IP Olá do computador anfitrião do Olá dispositivo toohello ligado. |
   |  Nome de Volume do dispositivo |Olá **nome de Volume do dispositivo** coluna contém o nome de Olá do Olá dispositivo volume toowhich Olá selecionado volume pertence. Este é o nome do volume Olá definido no portal do Azure para esse volume específica do Olá. |
   |  Caminhos de acesso |Olá **acesso caminhos** coluna apresenta o volume de toohello Olá acesso caminho. Este é Olá unidade letra ou um montagem ponto no qual Olá volume está acessível no computador do anfitrião de Olá. |

## <a name="delete-a-volume"></a>Eliminar um volume
Utilize Olá seguir o procedimento toodelete um volume do Snapshot Manager do StorSimple.

> [!NOTE]
> Não é possível eliminar um volume se faz parte de qualquer grupo de volume. (opção de eliminação de Olá não está disponível para volumes que são membros de um grupo de volume). Tem de eliminar o volume do Olá volume completo grupo toodelete Olá.

#### <a name="toodelete-a-volume"></a>toodelete um volume
1. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple.
2. No Olá **âmbito** painel, clique em Olá **Volumes** nós. 
3. No Olá **resultados** painel, volume de Olá contexto que pretende que o toodelete.
4. Olá menu, clique em **eliminar**. 
   
    ![Eliminar um volume](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. Olá **Eliminar Volume** é apresentada a caixa de diálogo. Tipo **confirmar** no Olá caixa de texto e, em seguida, clique em **OK**.
6. Por predefinição, Snapshot Manager do StorSimple efetua cópias de segurança num volume antes de eliminá-lo. Esta precaução pode protegê-lo contra perda de dados se a eliminação de Olá tiver sido planeada. Snapshot Manager do StorSimple apresenta um **instantâneo automática** mensagens de progresso, enquanto que efetua cópias de segurança volume Olá. 
   
    ![Mensagem de instantâneo automática](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>Reanalisar volumes
Utilize Olá seguir o procedimento toorescan Olá volumes ligado tooStorSimple Snapshot Manager.

#### <a name="toorescan-hello-volumes"></a>volumes de Olá toorescan
1. Clique em Olá ícone de ambiente de trabalho toostart Snapshot Manager do StorSimple.
2. No Olá **âmbito** painel, faça duplo clique **Volumes**e, em seguida, clique em **reanalisar volumes**.
   
    ![Reanalisar volumes](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    Este procedimento sincroniza a lista de volume Olá com Snapshot Manager do StorSimple. Quaisquer alterações, tais como a novos volumes ou volumes eliminados, serão apresentadas nos resultados de Olá.

## <a name="configure-and-back-up-a-basic-volume"></a>Configurar e efetuar cópias de segurança de um volume básico
Utilizar Olá seguir o procedimento tooconfigure uma cópia de segurança de um volume básico e, em seguida, iniciar de imediato uma cópia de segurança ou criar uma política de cópias de segurança agendadas.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar:

* Certifique-se de que Olá dispositivo StorSimple e o computador anfitrião estão configurados corretamente. Para mais informações, visite demasiado[implementar o dispositivo StorSimple no local](storsimple-deployment-walkthrough-u2.md).
* Instalar e configurar o Snapshot Manager do StorSimple. Para mais informações, visite demasiado[implementar Snapshot Manager do StorSimple](storsimple-snapshot-manager-deployment.md).

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>tooconfigure cópia de segurança de um volume básico
1. Crie um volume básico no dispositivo do StorSimple Olá.
2. Montar, inicializar e formatar o volume de Olá conforme descrito em [montar os volumes](#mount-volumes). 
3. Clique em Olá Snapshot Manager do StorSimple no ícone no seu ambiente de trabalho. é apresentada a janela do Olá Snapshot Manager do StorSimple. 
4. No Olá **âmbito** painel, contexto Olá **Volumes** nó e, em seguida, selecione **reanalisar volumes**. Quando a análise de Olá estiver concluída, uma lista de volumes deve aparecer na Olá **resultados** painel. 
5. No Olá **resultados** painel, faça duplo clique volume Olá e, em seguida, selecione **criar grupo de Volume**. 
   
    ![Criar grupo de volume](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. No Olá **criar grupo de Volume** caixa de diálogo, escreva um nome para o grupo de volume Olá, atribuir volumes tooit e, em seguida, clique em **OK**.
7. No Olá **âmbito** painel, expanda Olá **Volume grupos** nós. novo grupo de volume Olá deve aparecer em Olá **Volume grupos** nós. 
8. Clique no nome do grupo de Olá volume.
   
   * Clique em toostart uma tarefa de cópia de segurança (a pedido) interativa, **efetuar cópia de segurança**. 
   * tooschedule uma cópia de segurança automática, clique em **criar política de cópia de segurança**. No Olá **geral** página, selecione um grupo de volume na lista de Olá. No Olá **agenda** página, introduza os detalhes de agenda Olá. Quando tiver terminado, clique em **OK**. 
9. tooconfirm Olá a tarefa de cópia de segurança foi iniciada, expanda Olá **tarefas** nó Olá **âmbito** painel e, em seguida, clique em Olá **executar** nós. lista de Olá de tarefas atualmente em execução aparece no Olá **resultados** painel. 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>Configurar e efetuar cópias de segurança de um volume espelhado dinâmico
Olá concluir os seguintes passos tooconfigure de cópia de segurança num volume espelhado dinâmico:

* Passo 1: Gestão de discos de utilização toocreate um volume espelhado dinâmico. 
* Passo 2: Cópia de segurança tooconfigure Snapshot Manager do StorSimple utilização.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar:

* Certifique-se de que Olá dispositivo StorSimple e o computador anfitrião estão configurados corretamente. Para mais informações, visite demasiado[implementar o dispositivo StorSimple no local](storsimple-8000-deployment-walkthrough-u2.md).
* Instalar e configurar o Snapshot Manager do StorSimple. Para mais informações, visite demasiado[implementar Snapshot Manager do StorSimple](storsimple-snapshot-manager-deployment.md).
* Configure dois volumes no dispositivo do StorSimple Olá. (Nos exemplos de Olá, são volumes disponíveis Olá **disco 1** e **disco 2**.) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>Passo 1: Gestão de discos de utilização toocreate um volume espelhado dinâmico
Gestão de discos é um utilitário de sistema para a gestão de discos rígidos e volumes de Olá ou as partições que contêm. Para mais informações sobre a gestão de discos, visite demasiado[gestão de discos](https://technet.microsoft.com/library/cc770943.aspx) no Web site do Microsoft TechNet Olá.

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate um volume espelhado dinâmico
1. Utilize qualquer uma das seguintes opções toostart gestão de discos de Olá: 
   
   * Abra Olá **executar** caixa, escreva **Diskmgmt.msc**, e prima Enter.
   * Inicie o Gestor de servidor, expanda Olá **armazenamento** nó e, em seguida, selecione **gestão de discos**. 
   * Iniciar **ferramentas administrativas**, expanda Olá **gestão de computadores** nó e, em seguida, selecione **gestão de discos**. 
2. Certifique-se de que tem dois volumes disponíveis no dispositivo do StorSimple Olá. (No exemplo de Olá, são volumes disponíveis Olá **disco 1** e **disco 2**.) 
3. Na janela de gestão de discos de Olá, na coluna da direita Olá Olá inferior do painel de, clique com botão direito **disco 1** e selecione **Novo Volume espelhada**. 
   
    ![Novo Volume espelhado](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. No Olá **Novo Volume espelhada** página do assistente, clique em **seguinte**.
5. No Olá **selecionar discos** página, selecione **disco 2** no Olá **selecionados** painel, clique em **adicionar**e, em seguida, clique em **seguinte**. 
6. No Olá **atribuir letra da unidade ou caminho** página, aceite as predefinições de Olá e, em seguida, clique em **seguinte**. 
7. No Olá **formatação do Volume** página, numa Olá **tamanho da unidade de alocação** caixa, selecione **64K**. Selecione Olá **Efetue uma formatação rápida** caixa de verificação e, em seguida, clique em **seguinte**. 
8. No Olá **concluir Olá Novo Volume espelhada** página, reveja as definições e, em seguida, clique em **concluir**. 
9. É apresentada uma mensagem tooindicate Olá disco básico será convertida tooa disco dinâmico. Clique em **Sim**.
   
    ![Mensagem de conversão do disco dinâmico](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. Na gestão de discos, certifique-se de que o disco 1 e 2 do disco são apresentadas como volumes espelhados dinâmicos. (**Dinâmica** deve aparecer na coluna de estado de Olá e cor de barras de capacidade de Olá deve ser alterado toored, que indica que um volume espelhado.) 
    
    ![Discos dinâmicos de gestão espelhado de disco](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>Passo 2: Cópia de segurança tooconfigure de utilização do Snapshot Manager do StorSimple
Utilizar Olá seguir o procedimento tooconfigure um volume espelhado dinâmico e, em seguida, iniciar de imediato uma cópia de segurança ou criar uma política de cópias de segurança agendadas.

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>tooconfigure cópia de segurança de um volume espelhada dinâmica
1. Clique em Olá Snapshot Manager do StorSimple no ícone no seu ambiente de trabalho. é apresentada a janela do Olá Snapshot Manager do StorSimple. 
2. No Olá **âmbito** painel, contexto Olá **Volumes** nó e selecione **reanalisar volumes**. Quando a análise de Olá estiver concluída, uma lista de volumes deve aparecer na Olá **resultados** painel. volume de espelhadas dinâmica Olá está listado como um único volume. 
3. No Olá **resultados** painel, clique no volume de espelhadas dinâmica Olá e, em seguida, clique em **criar grupo de Volume**. 
4. No Olá **criar grupo de Volume** caixa de diálogo, escreva um nome para o grupo de volume Olá, atribua Olá dinâmica volume espelhadas toothis grupo e, em seguida, clique em **OK**. 
5. No Olá **âmbito** painel, expanda Olá **Volume grupos** nós. novo grupo de volume Olá deve aparecer em Olá **Volume grupos** nós. 
6. Clique no nome do grupo de Olá volume. 
   
   * Clique em toostart uma tarefa de cópia de segurança (a pedido) interativa, **efetuar cópia de segurança**. 
   * tooschedule uma cópia de segurança automática, clique em **criar política de cópia de segurança**. No Olá **geral** página, o grupo de volume Olá selecione na lista de Olá. No Olá **agenda** página, introduza os detalhes de agenda Olá. Quando tiver terminado, clique em **OK**. 
7. Pode monitorizar a tarefa de cópia de segurança de Olá enquanto é executada. No Olá **âmbito** painel, expanda Olá **tarefas** nó e, em seguida, clique **executar**, os detalhes da tarefa Olá aparecem no Olá **resultados** painel. Quando a tarefa de cópia de segurança de Olá estiver concluída, detalhes de Olá são transferido toohello **últimas 24** horas lista da tarefa. 

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[utilizar Snapshot Manager do StorSimple tooadminister solução StorSimple](storsimple-snapshot-manager-admin.md).
* Saiba como demasiado[utilizar toocreate Snapshot Manager do StorSimple e gerir grupos de volume](storsimple-snapshot-manager-manage-volume-groups.md).

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
