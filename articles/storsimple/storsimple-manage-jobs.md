---
title: aaaView e gerir tarefas do StorSimple | Microsoft Docs
description: "Descreve a página de tarefas de serviço do Olá StorSimple Manager e como toouse, tarefas de cópia de segurança mais recente, atual e agendada tootrack."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b7341270e37a9f2530a8da1fb7c54f6b699c699c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs"></a>Utilizar tooview de serviço do StorSimple Manager Olá e gerir tarefas do StorSimple
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Descrição geral
Olá **tarefas** página fornece um único portal central para visualização e gestão de tarefas que foram iniciadas em dispositivos ligados tooyour do serviço StorSimple Manager. Pode ver tarefas agendadas, em execução, concluídas e com falhas para vários dispositivos. Os resultados são apresentados em formato tabular. 

![Página das tarefas](./media/storsimple-manage-jobs/HCS_JobsPage.png)

Pode encontrar rapidamente tarefas Olá que estão interessadas nas filtrando campos, tais como:

* **Estado** – tarefas podem estar em execução agendada, falhada, concluída, cancelamento ou cancelada.
* **Tipo** – tarefas podem ser criadas devido a um agendada ou uma cópia de segurança a pedido (**efetuar cópia de segurança**), a clonagem, um restauro de dispositivo ou uma operação de atualização.
* **Dispositivos** – tarefas são iniciadas num serviço determinadas tooyour dispositivo ligado.
* **A partir de e para** – tarefas podem ser o intervalo de filtrado Olá com base na data e hora.

Olá tarefas são, em seguida, apresentadas numa base de Olá de Olá seguintes atributos:

* **Tipo** – cópia de segurança, clone, restauro, ativação pós-falha ou atualização.
* **Estado** – em execução, agendada, falha, concluída, cancelamento ou cancelada.
* **Entidade** – tarefas Olá podem ser associadas um volume, uma política de cópia de segurança ou um dispositivo. Uma tarefa de clone está associada um volume, enquanto uma tarefa de cópia de segurança agendada é associada a uma política de cópia de segurança. Como resultado de uma recuperação após desastre (DR) ou uma operação de restauro, é criada uma tarefa de dispositivo.
* **Dispositivo** – hello nome de dispositivo Olá no qual Olá a tarefa foi iniciada.
* **Foi iniciada no** – tempo Olá quando a tarefa de Olá foi iniciada.
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

## <a name="cancel-a-job"></a>Cancelar uma tarefa
Efetue Olá os seguintes passos toocancel uma tarefa em execução.

### <a name="toocancel-a-job"></a>toocancel uma tarefa
1. No Olá **tarefas** página, apresentar Olá de tarefas em execução que pretende que toocancel ao executar uma consulta com filtros adequados.
2. Selecione a tarefa de Olá.
3. Na Olá parte inferior da página Olá, clique em **Cancelar**.
4. Quando lhe for pedida a confirmação, clique em **Sim**.

Esta tarefa agora, será cancelada.

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[gerir as políticas de cópia de segurança do StorSimple](storsimple-manage-backup-policies.md).
* Saiba como demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

