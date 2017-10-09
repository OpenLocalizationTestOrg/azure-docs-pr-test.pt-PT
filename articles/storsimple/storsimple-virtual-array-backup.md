---
title: "tutorial de cópia de segurança de matriz Virtual do Azure StorSimple aaaMicrosoft | Microsoft Docs"
description: "Descreve como partilha tooback segurança matriz Virtual StorSimple e volumes."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a>Criar cópias de segurança partilhas ou volumes na sua matriz de Virtual StorSimple

## <a name="overview"></a>Descrição geral

Olá matriz Virtual StorSimple é um híbridos na nuvem no local virtual dispositivo de armazenamento que podem ser configurados como um servidor de ficheiros ou um servidor de iSCSI. matriz virtual Olá permite cópias de segurança agendadas e manuais de todos os volumes ou partilhas de Olá Olá toocreate de utilizador no dispositivo Olá. Quando configurado como um servidor de ficheiros, também permite a recuperação ao nível do item. Este tutorial descreve como toocreate agendada e cópias de segurança manuais e efetuar a recuperação ao nível do item toorestore um ficheiro na sua matriz virtual eliminado.

Este tutorial aplica-se toohello StorSimple Virtual matrizes só. Para informações sobre 8000 série, visite demasiado[criar uma cópia de segurança para o dispositivo da 8000 série](storsimple-manage-backup-policies-u2.md)

## <a name="back-up-shares-and-volumes"></a>Cópia de segurança de partilhas e os volumes

As cópias de segurança fornecem proteção de ponto no tempo, melhorar a capacidade de recuperação e minimizar os tempos de restauro de volumes e partilhas. Pode efetuar cópias de segurança de uma partilha ou volume no dispositivo StorSimple de duas formas: **agendada** ou **Manual**. Cada um dos métodos de Olá é abordada em Olá secções a seguir.

## <a name="change-hello-backup-start-time"></a>Hora de início de cópia de segurança de Olá de alteração

> [!NOTE]
> Nesta versão, as cópias de segurança agendadas são criadas por uma política predefinida que é executada diariamente a uma determinada hora e efetua cópias de segurança de todos os volumes ou partilhas de Olá no dispositivo Olá. Não é possível toocreate políticas personalizadas para cópias de segurança agendadas neste momento.


A matriz de Virtual StorSimple tem uma política de cópia de segurança predefinida que inicia a uma determinada hora do dia (22:30) e efetua uma cópia de segurança de todos os volumes ou partilhas de Olá no dispositivo Olá uma vez por dia. Pode alterar o tempo de Olá que começa de cópia de segurança Olá, mas frequência Olá e Olá retenção (que especifica o número de Olá de cópias de segurança tooretain) não pode ser alterada. Durante estas cópias de segurança, o dispositivo virtual completo de Olá é uma cópia de segurança. Isto foi potencialmente afetar o desempenho de Olá do dispositivo Olá e afetam as cargas de trabalho de Olá implementadas no dispositivo Olá. Por conseguinte, recomendamos que agende estas cópias de segurança para as horas de ponta.

 a cópia de segurança predefinida de Olá toochange hora de início, execute Olá os seguintes passos no Olá [portal do Azure](https://portal.azure.com/).

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a>Olá toochange hora de início para política de cópia de segurança Olá predefinida

1. Aceda demasiado**dispositivos**. lista de Olá de dispositivos registados com o serviço StorSimple Manager de dispositivo será apresentada. 
   
    ![Navegue toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. Selecione e clique em seu dispositivo. Olá **definições** é apresentado o painel. Aceda demasiado**gerir > políticas de cópia de segurança**.
   
    ![Selecione o seu dispositivo](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. No Olá **políticas de cópia de segurança** painel, hora de início do Olá predefinido é 22:30. Pode especificar Olá novo a hora de início para uma agenda diária Olá no fuso horário do dispositivo.
   
    ![Navegue toobackup políticas](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. Clique em **Guardar**.

### <a name="take-a-manual-backup"></a>Efetuar uma cópia de segurança manual

Além disso tooscheduled cópias de segurança, que pode tomar uma cópia de segurança (a pedido) manual de dados de dispositivo em qualquer altura.

#### <a name="toocreate-a-manual-backup"></a>toocreate uma cópia de segurança manual

1. Aceda demasiado**dispositivos**. Selecione o seu dispositivo e faça duplo clique **...**  na extremidade direita Olá na linha selecionada Olá. No menu de contexto de Olá, selecione **efetuar cópia de segurança**.
   
    ![Navegue tootake cópia de segurança](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. No Olá **efetuar cópia de segurança** painel, clique em **efetuar cópia de segurança**. Isto irá criar cópias de segurança todas as partilhas de Olá no servidor de ficheiros de Olá ou todos os volumes de Olá no seu servidor de iSCSI. 
   
    ![a partir de cópia de segurança](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    Inicia uma cópia de segurança a pedido e verá que uma tarefa de cópia de segurança foi iniciada.
   
    ![a partir de cópia de segurança](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    Assim que a tarefa de Olá foi concluída com êxito, será notificado novamente. em seguida, inicia o processo de cópia de segurança de Olá.
   
    ![tarefa de cópia de segurança criada](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. progresso de Olá tootrack de cópias de segurança de Olá e ver os detalhes da tarefa Olá, clique em notificação Olá. Isto leva-o demasiado **detalhes da tarefa**.
   
     ![Detalhes da tarefa de cópia de segurança](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. Depois de concluída a cópia de segurança de Olá, aceda demasiado**gestão > catálogo de cópia de segurança**. Verá um instantâneo de nuvem de todas as partilhas de Olá (ou volumes) no seu dispositivo.
   
    ![Cópia de segurança concluída](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a>Ver as cópias de segurança existentes
tooview Olá cópias de segurança existentes, efetuar Olá os seguintes passos no Olá portal do Azure.

#### <a name="tooview-existing-backups"></a>tooview cópias de segurança existentes

1. Aceda demasiado**dispositivos** painel. Selecione e clique em seu dispositivo. No Olá **definições** painel, vá demasiado**gestão > catálogo de cópia de segurança**.
   
    ![Navegue toobackup catálogo](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. Especifique Olá toobe critérios utilizado para filtrar os seguintes:
   
    - **Intervalo de tempo** – pode ser **última 1 hora**, **últimas 24 horas**, **nos últimos 7 dias**, **nos últimos 30 dias**, **passado ano**, e **data personalizada**.
    
    - **Dispositivos** – selecione na lista de Olá de servidores de ficheiros ou servidores iSCSI registados com o serviço do Gestor de dispositivos do StorSimple.
   
    - **Iniciou** – pode ser automaticamente **agendada** (por uma política de cópia de segurança) ou **manualmente** iniciada (por si).
   
    ![Filtrar as cópias de segurança](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. Clique em **Aplicar**. Olá lista filtrada de cópias de segurança é apresentada no Olá **catálogo de cópia de segurança** painel. Elementos de cópia de segurança de nota 100 só podem ser apresentados num determinado momento.
   
    ![Catálogo de cópias de segurança atualizado](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a>Passos seguintes

Saiba mais sobre [administrar a matriz de Virtual StorSimple](storsimple-ova-web-ui-admin.md).

