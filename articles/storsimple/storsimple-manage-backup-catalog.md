---
title: "aaaManage seu catálogo de cópias de segurança do StorSimple | Microsoft Docs"
description: "Explica como toouse Olá StorSimple Manager serviço catálogo de cópias de segurança página toolist, selecione e eliminar conjuntos de cópias de segurança para um volume."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>Utilizar toomanage de serviço do StorSimple Manager Olá seu catálogo de cópias de segurança
## <a name="overview"></a>Descrição geral
Olá serviço StorSimple Manager **catálogo de cópias de segurança** página apresenta todos os conjuntos de cópias de segurança Olá que são criados quando são efetuadas cópias de segurança de manuais ou agendadas. Pode utilizar este toolist página todas as cópias de segurança Olá para uma política de cópia de segurança ou um volume, selecione ou eliminar as cópias de segurança, ou utilizar uma cópia de segurança toorestore ou clonar um volume.

Este tutorial explica como toolist, selecione e eliminar uma cópia de segurança definido. toolearn como toorestore o dispositivo de cópia de segurança, aceda demasiado[restaurar o seu dispositivo a partir de um conjunto de cópia de segurança](storsimple-restore-from-backup-set.md). toolearn como tooclone um volume demasiado aceda[clonar um volume StorSimple](storsimple-clone-volume.md).

![Catálogo de cópias de segurança](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

Olá **catálogo de cópias de segurança** página fornece uma consulta toonarrow a seleção de conjunto de cópia de segurança. Pode filtrar os conjuntos de cópias de segurança de Olá que são obtidos, com base no Olá os seguintes parâmetros:

* **Dispositivo** – dispositivo Olá no qual Olá o conjunto de cópia de segurança foi criado.
* **Volume ou a política de cópia de segurança** – Olá volume associados a este conjunto de cópia de segurança ou de política de cópia de segurança.
* **A partir de e para** – Olá intervalo de data e hora quando o conjunto de cópias de segurança de Olá foi criado.

Olá filtrados conjuntos de cópias de segurança são, em seguida, apresentados com base no Olá seguintes atributos:

* **Nome** – hello nome da política de cópia de segurança de Olá ou volume associado o conjunto de cópias de segurança de Olá.
* **Tamanho** – Olá tamanho real do conjunto de cópias de segurança de Olá.
* **Criado no** – a data de Olá e a hora quando cópias de segurança de Olá foram criadas. 
* **Tipo** – conjuntos de cópia de segurança podem ser instantâneos locais ou instantâneos de nuvem. Um instantâneo local é uma cópia de segurança de todos os seus dados de volume armazenados localmente no dispositivo Olá, enquanto que um instantâneo na nuvem refere-se toohello cópia de segurança de dados do volume que residem na nuvem de Olá. Instantâneos locais fornecem um acesso mais rápido, enquanto que os instantâneos de nuvem são escolhidos para resiliência de dados.
* **Iniciado pelo** – cópias de segurança de Olá podem ser iniciadas automaticamente por um agendamento ou manualmente por um utilizador. Pode utilizar cópias de segurança de tooschedule uma política de cópia de segurança. Em alternativa, pode utilizar Olá **efetuar cópia de segurança** opção tootake uma cópia de segurança manual.

## <a name="list-backup-sets-for-a-volume"></a>Define a cópia de segurança da lista para um volume
Conclua todas as Olá cópias de segurança para um volume de Olá toolist passos a seguir.

#### <a name="toolist-backup-sets"></a>conjuntos de cópias de segurança toolist
1. Na página do serviço de Olá StorSimple Manager, clique em Olá **catálogo de cópia de segurança** separador.
2. Filtre seleções Olá da seguinte forma:
   
   1. Selecione Olá de dispositivo adequados.
   2. No Olá na lista pendente, escolha um volume tooview Olá correspondente Olá as cópias de segurança.
   3. Especifique o intervalo de tempo de Olá.
   4. Clique Olá ícone de verificação ![Ícone de verificação](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute esta consulta.
      
      cópias de segurança de Olá associadas volume Olá selecionado devem aparecer na lista de Olá de conjuntos de cópia de segurança.

## <a name="select-a-backup-set"></a>Selecione um conjunto de cópia de segurança
Olá concluir os seguintes passos tooselect uma cópia de segurança definido para uma política de cópia de segurança ou volume.

#### <a name="tooselect-a-backup-set"></a>tooselect um conjunto de cópia de segurança
1. Na página do serviço de Olá StorSimple Manager, clique em Olá **catálogo de cópia de segurança** separador.
2. Filtre seleções Olá da seguinte forma:
   
   1. Selecione Olá de dispositivo adequados.
   2. Na Olá na lista pendente, escolha política de cópia de segurança ou volume de Olá para cópia de segurança de Olá pretende tooselect.
   3. Especifique o intervalo de tempo de Olá.
   4. Clique Olá ícone de verificação ![Ícone de verificação](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute esta consulta.
      
      Olá cópias de segurança associadas a política de cópia de segurança ou volume Olá selecionado devem aparecer na lista de Olá de conjuntos de cópia de segurança.
3. Selecione e expanda um conjunto de cópia de segurança. Olá **restaurar** e **eliminar** opções são apresentadas num Olá parte inferior da página Olá. Pode efetuar qualquer uma destas ações no conjunto de cópias de segurança de Olá que selecionou.

## <a name="delete-a-backup-set"></a>Eliminar um conjunto de cópia de segurança
Elimine uma cópia de segurança quando que já não pretenda dados de Olá tooretain associados à mesma. Execute os seguintes passos toodelete um conjunto de cópia de segurança de Olá.

#### <a name="toodelete-a-backup-set"></a>toodelete um conjunto de cópia de segurança
1. Na página do serviço de Olá StorSimple Manager, clique em Olá **separador do catálogo de cópia de segurança**.
2. Filtre seleções Olá da seguinte forma:
   
   1. Selecione Olá de dispositivo adequados.
   2. Na Olá na lista pendente, escolha política de cópia de segurança ou volume de Olá para cópia de segurança de Olá pretende tooselect.
   3. Especifique o intervalo de tempo de Olá.
   4. Clique Olá ícone de verificação ![Ícone de verificação](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute esta consulta.
      
      Olá cópias de segurança associadas a política de cópia de segurança ou volume Olá selecionado devem aparecer na lista de Olá de conjuntos de cópia de segurança.
3. Selecione e expanda um conjunto de cópia de segurança. Olá **restaurar** e **eliminar** opções são apresentadas num Olá parte inferior da página Olá. Clique em **Eliminar**.
4. Será notificado quando a eliminação de Olá está em curso e quando tiver concluído com êxito. Depois da conclusão da eliminação de Olá, atualize a consulta de Olá nesta página. conjunto de cópias de segurança de Olá eliminado deixarão de aparecer na lista de Olá de conjuntos de cópia de segurança.

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[utilize Olá toorestore do catálogo de cópias de segurança de dispositivo a partir de um conjunto de cópia de segurança](storsimple-restore-from-backup-set.md).
* Saiba como demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

