---
title: aaaView e gerir tarefas do StorSimple | Microsoft Docs
description: "Descreve a página de tarefas de serviço do Olá StorSimple Manager e como toouse, tarefas de cópia de segurança mais recente, atual e agendada tootrack."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a>Utilize tooview de serviço do StorSimple Manager Olá e gerir tarefas do StorSimple (atualização 2)
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Descrição geral
Olá **tarefas** página fornece um único portal central para visualização e gestão de tarefas que foram iniciadas em dispositivos ligados tooyour do serviço StorSimple Manager. Pode ver as tarefas agendadas, em execução, concluídas, canceladas e falhadas para vários dispositivos. Os resultados são apresentados em formato tabular. 

![Página das tarefas](./media/storsimple-manage-jobs-u2/jobs.png)

Pode encontrar rapidamente tarefas Olá que estão interessadas nas filtrando campos, tais como:

* **Estado** – tarefas podem estar em execução, concluída, cancelada, com falha, cancelamento ou foi concluída com erros.
* **A partir de e para** – tarefas podem ser o intervalo de filtrado Olá com base na data e hora.
* **Tipo** – o tipo de tarefa de Olá pode ser a cópia de segurança, restauro, cópia de segurança manual, a ativação pós-falha do dispositivo, e clone volume localmente afixado de criar, modificar o volume, atualizar, suporta pacote ou aprovisionamento do dispositivo virtual.
* **Dispositivos** – tarefas são iniciadas num serviço determinadas tooyour dispositivo ligado.
  Olá tarefas são, em seguida, apresentadas numa base de Olá de Olá seguintes atributos:
  
  * **Tipo** – cópia de segurança, restauro, cópia de segurança manual, a ativação pós-falha do dispositivo, e clone volume localmente afixado de criar, modificar o volume, atualizar, suporta pacote ou aprovisionamento do dispositivo virtual.
  * **Estado** – em execução, concluída, cancelada, com falha, cancelamento ou foi concluída com erros.
  * **Entidade** – tarefas Olá podem ser associadas um volume, uma política de cópia de segurança ou um dispositivo. Por exemplo, uma tarefa de clone está associada um volume, enquanto uma tarefa de cópia de segurança agendada é associada a uma política de cópia de segurança. Como resultado de uma recuperação após desastre (DR) ou uma operação de restauro, é criada uma tarefa de dispositivo.
  * **Dispositivo** – hello nome de dispositivo Olá no qual Olá a tarefa foi iniciada.
  * **Iniciar** – tempo Olá quando a tarefa de Olá foi iniciada.
  * **Progresso** – Olá percentagem de conclusão de uma tarefa em execução. Para uma tarefa concluída, isto deve ser sempre 100%.

lista de Olá de tarefas é atualizada a cada 30 segundos.

Pode efetuar Olá seguintes ações relacionadas com a tarefa nesta página:

* Ver detalhes da tarefa
* Cancelar uma tarefa

## <a name="view-job-details"></a>Ver detalhes da tarefa
Efetue Olá os passos tooview Olá detalhes de qualquer tarefa.

#### <a name="tooview-job-details"></a>Detalhes da tarefa tooview
1. No Olá **tarefas** página, apresentar tarefas Olá estão interessadas ao executar uma consulta com filtros adequados. Pode pesquisar para concluir, em execução ou cancelar tarefas.
2. Selecione uma tarefa.
3. Na Olá parte inferior da página Olá, clique em **detalhes**.
4. No Olá **detalhes da tarefa de cópia de segurança** caixa de diálogo, pode ver o estado de Olá, detalhes, as estatísticas de tempo e estatísticas de dados.
   
    ![Página de detalhes da tarefa](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a>Cancelar uma tarefa
Efetue Olá os seguintes passos toocancel uma tarefa em execução.

> [!NOTE]
> Algumas tarefas, tais como modificar um tipo de volume do volume toochange Olá ou expandir um volume, não podem ser canceladas.
> 
> 

### <a name="toocancel-a-job"></a>toocancel uma tarefa
1. No Olá **tarefas** página, apresentar Olá de tarefas em execução que pretende que toocancel ao executar uma consulta com filtros adequados.
2. Selecione a tarefa de Olá.
3. Na Olá parte inferior da página Olá, clique em **Cancelar**.
4. Quando lhe for pedida a confirmação, clique em **Sim**.

Esta tarefa agora, será cancelada.

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[gerir as políticas de cópia de segurança do StorSimple](storsimple-manage-backup-policies.md).
* Saiba como demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

