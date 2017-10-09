---
title: "aaaClone uma cópia de segurança de matriz Virtual StorSimple | Microsoft Docs"
description: "Saiba como tooclone uma cópia de segurança e recuperar um ficheiro a matriz de Virtual StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>Clonar a partir de uma cópia de segurança da sua matriz de Virtual StorSimple

## <a name="overview"></a>Descrição geral

Este artigo descreve passo a passo como tooclone uma cópia de segurança definido das suas partilhas ou volumes na sua matriz Virtual do Microsoft Azure StorSimple. cópia de segurança clonado Olá é toorecover utilizado um ficheiro eliminado ou perdido. artigo de Olá também inclui tooperform os passos detalhados que uma recuperação ao nível do item na sua matriz de Virtual StorSimple configurada como um servidor de ficheiros.

## <a name="clone-shares-from-a-backup-set"></a>Partilhas de clone a partir de um conjunto de cópia de segurança

**Antes de tentar tooclone partilhas, certifique-se de que tem espaço suficiente no Olá dispositivo toocomplete esta operação.** tooclone de uma cópia de segurança, no Olá [portal do Azure](https://portal.azure.com/), efetuar Olá os seguintes passos.

#### <a name="tooclone-a-share"></a>tooclone uma partilha

1. Procurar demasiado**dispositivos** painel. Selecione e clique em seu dispositivo e, em seguida, clique em **partilhas**. Selecione a partilha de Olá que pretende que o tooclone, o menu de contexto Olá partilha tooinvoke Olá contexto. Selecione **Clone**.
   
   ![Clonar uma cópia de segurança](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. No Olá **Clone** painel, clique em **cópia de segurança > selecione** e, em seguida, Olá seguintes: 
   
   a.    Filtre uma cópia de segurança neste dispositivo com base no intervalo de tempo de Olá. Pode escolher entre **nos últimos 7 dias**, **nos últimos 30 dias**, e **passado ano**.
   
   b.    Na lista de Olá de cópias de segurança filtradas apresentada, selecione um tooclone da cópia de segurança.
   
   c.    Clique em **OK**.
   
   ![Clonar uma cópia de segurança](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. No Olá **Clone** painel, clique em **as definições de destino** e, em seguida, Olá seguintes:
   
   a.    Forneça um nome de partilha. nome da partilha Olá tem de conter 3 127 carateres.
   
   b.    Opcionalmente, indique uma descrição para a partilha clonado Olá.
   
   c.    Não é possível alterar o tipo de Olá da partilha de Olá que está a restaurar. Foi clonada a uma partilha em camadas como um em camadas e uma partilha afixada localmente afixado como localmente.
   
   d.    capacidade de Olá está definida como toohello igual tamanho da partilha de Olá que são a clonagem do.
   
   e.    Designar administradores de Olá para esta partilha. Será capaz de toomodify propriedades de partilha de Olá através do Explorador de ficheiros após a conclusão da clonagem de Olá.
   
   f.    Clique em **OK**.
   
   ![Clonar uma cópia de segurança](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. Clique em **Clone** toostart uma tarefa de clone. Após a conclusão da tarefa de Olá, operação de clonagem Olá inicia e será notificado. progresso de Olá toomonitor de clone, aceda toohello **tarefas** painel e clique em detalhes da tarefa Olá tarefa tooview.
5. Depois de clone Olá foi criado com êxito, navegue back toohello **partilhas** painel no seu dispositivo.
6. Agora, pode ver a nova partilha de clonado Olá na lista de Olá de partilhas no seu dispositivo. Foi clonada a uma partilha em camadas como em camadas e uma partilha localmente afixada como uma partilha afixada localmente.
   
   ![Clonar uma cópia de segurança](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>Volumes de clone de um conjunto de cópia de segurança

tooclone de uma cópia de segurança, no portal do Azure, de Olá tiver tooperform passos semelhantes toohello aqueles ao clonar uma partilha. operação de clonagem Olá clones Olá tooa cópia de segurança novo volume Olá mesmo dispositivo virtual; Não é possível clonar tooa noutro dispositivo.

#### <a name="tooclone-a-volume"></a>tooclone um volume

1. Procurar demasiado**dispositivos** painel. Selecione e clique em seu dispositivo e, em seguida, clique em **Volumes**. Volume de Olá que tiver que pretende que o tooclone, clique no menu de contexto do Olá volume tooinvoke Olá. Selecione **Clone**.
   
   ![Clonar um volume](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. No Olá **Clone** painel, clique em **cópia de segurança** e, em seguida, Olá seguintes: 
   
   a.    Filtre uma cópia de segurança neste dispositivo com base no intervalo de tempo de Olá. Pode escolher entre **nos últimos 7 dias**, **nos últimos 30 dias**, e **passado ano**. 
   
   b.    Na lista de Olá de cópias de segurança filtradas apresentada, selecione um tooclone da cópia de segurança.
   
   c.    Clique em **OK**.
   
   ![Clonar uma cópia de segurança](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. No Olá **Clone** painel, clique em **definições de volume de destino** e, em seguida, Olá seguintes:
   
   a. nome do dispositivo Olá é preenchido automaticamente.
   
   b. Forneça um nome de volume para Olá **clonado volume**. nome do volume Olá tem de conter 3 too127 carateres.
   
   c. tipo de volume Olá é automaticamente definido toohello volume original. Foi clonado a um volume em camadas como em camadas e um volume localmente afixado como localmente afixado.
   
   d. Para Olá **ligados a anfitriões**, clique em **selecione**.
   
   ![Clonar uma cópia de segurança](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. No Olá **ligados a anfitriões** painel, selecione de um ACR existente ou adicionar um novo ACR. um novo ACR tooadd, terá de tooprovide um nome ACR e anfitrião Olá IQN. Clique em **Selecionar**.
   
   ![Clonar uma cópia de segurança](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. Clique em **Clone** toolaunch uma tarefa de clone.
   
   ![Clonar uma cópia de segurança](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Depois de criar tarefa de clone Olá, a clonagem irá iniciar. Após criar o clone Olá, é apresentada no painel de Volumes de Olá no seu dispositivo. Tenha em atenção que foi clonado a um volume em camadas como em camadas e um volume localmente afixado é clonado como um volume afixado localmente.
   
   ![Clonar uma cópia de segurança](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Assim que o volume de Olá aparece online na lista de Olá de volumes, o volume de Olá está disponível para utilização. No anfitrião de iniciador iSCSI de Olá, atualize a lista de Olá de destinos na janela de propriedades do iniciador iSCSI. Um novo destino que contém o nome de volume clonado Olá deve aparecer como 'inactive' na coluna de estado de Olá.
8. Selecione o destino de Olá e clique em **Connect**. Depois do iniciador de Olá destino toohello ligado, o estado de Olá deve ser alterado demasiado**ligado**.
9. No Olá **gestão de discos** janela, hello volumes montados apresentados como mostrado na seguinte ilustração de Olá. Clique no volume de Olá detetado (clique no nome do disco de Olá) e, em seguida, clique em **Online**.

> [!IMPORTANT]
> Quando tentar tooclone um volume ou uma partilha de um conjunto de cópia de segurança, se a tarefa de clone Olá falhar, um volume de destino ou uma partilha ainda pode ser criada no portal de Olá. É importante se eliminar este volume de destino ou partilhar no toominimize portal Olá quaisquer problemas futuros resultantes deste elemento.
> 
> 

## <a name="item-level-recovery-ilr"></a>Recuperação ao nível do item (ILR)

Esta versão apresenta a recuperação de ao nível do item (ILR) Olá numa matriz Virtual StorSimple configurado como um servidor de ficheiros. funcionalidade de Olá permite-lhe toodo recuperação granular dos ficheiros e pastas a partir de uma cópia de segurança de nuvem de todas as partilhas de Olá no dispositivo do StorSimple Olá. Pode obter ficheiros eliminados de cópias de segurança recentes através de um modelo personalizado.

Cada partilha tem um *.backups* pasta que contém as cópias de segurança mais recentes Olá. Pode navegar pretendido toohello de cópia de segurança, copiar relevantes ficheiros e pastas de cópia de segurança de Olá e restaurá-las. Esta funcionalidade elimina tooadministrators de chamadas para restaurar os ficheiros de cópias de segurança.

1. Quando efetuar Olá ILR, pode ver as cópias de segurança de Olá através do Explorador de ficheiros. Clique em partilha de específico Olá que pretende que sejam toolook em Olá cópia de segurança. Verá um *.backups* pasta criada partilha Olá que armazena todas as cópias de segurança Olá. Expanda Olá *.backups* pasta tooview Olá as cópias de segurança. pasta de Olá mostra Olá exploded vista de hierarquia de cópia de segurança completa Olá. Esta vista é criada a pedido e normalmente demora apenas alguns segundos toocreate.
   
   últimos cinco Olá de cópias de segurança é apresentados desta forma e pode ser utilizados tooperform um nível de item de recuperação. Olá cinco cópias de segurança recentes incluem os Olá agendada predefinida e Olá cópias de segurança manuais.
   
   * **Cópias de segurança agendadas** com o nome como &lt;nome de dispositivo&gt;DailySchedule-AAAAMMDD HHMMSS UTC.
   * **As cópias de segurança manuais** com o nome como Ad-hoc-AAAAMMDD-HHMMSS-UTC.
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. Identifica a cópia de segurança de Olá com a versão mais recente do Olá do ficheiro de Olá eliminado. Embora o nome da pasta Olá contém um carimbo de UTC em cada um dos Olá precedente casos, o tempo de Olá no qual Olá pasta foi criada é Olá dispositivo real início ao hello cópia de segurança. Utilizar Olá pasta timestamp toolocate e identifique as cópias de segurança Olá.

3. Localize a pasta de Olá ou o ficheiro de Olá que pretende toorestore na cópia de segurança de Olá que identificou no passo anterior Olá. Tenha em atenção que só pode ver Olá ficheiros ou pastas que tem permissões para. Se não é possível aceder a determinados ficheiros ou pastas, contacte um administrador de partilha. administrador de Olá pode utilizar permissões de partilha do Explorador de ficheiros tooedit Olá e dão-lhe acesso toohello específico ficheiro ou pasta. É recomendável que Olá partilha administrador é um grupo de utilizadores em vez de um único utilizador.

4. Copie o ficheiro Olá ou Olá pasta toohello adequadas de partilha no seu servidor de ficheiros do StorSimple.

## <a name="next-steps"></a>Passos seguintes

Saiba mais sobre como demasiado[administrar a matriz de Virtual StorSimple, utilizando a IU da web local Olá](storsimple-ova-web-ui-admin.md).

