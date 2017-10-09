---
title: "aaaManage as políticas de cópia de segurança do StorSimple | Microsoft Docs"
description: "Explica como pode utilizar toocreate de serviço do StorSimple Manager Olá e gerir cópias de segurança manuais, as agendas de cópia de segurança e retenção de cópias de segurança."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a>Utilizar políticas de toomanage de serviço StorSimple Manager do Olá cópia de segurança
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Descrição geral
Este tutorial explica como toouse Olá serviço StorSimple Manager **políticas de cópia de segurança** página toocontrol processos de cópia de segurança e retenção de cópias de segurança para os volumes do StorSimple. Descreve também como toocomplete uma cópia de segurança manual.

Olá **políticas de cópia de segurança** página permite-lhe políticas de cópia de segurança toomanage e agenda locais e instantâneos de nuvem. (As políticas de cópia de segurança estão tooconfigure utilizados agendas de cópia de segurança e retenção de cópias de segurança para uma coleção de volumes). Políticas de cópia de segurança permitem-lhe tootake um instantâneo de vários volumes em simultâneo. Isto significa que as cópias de segurança de Olá criadas por uma política de cópia de segurança serão cópias consistentes com falhas. Esta página apresenta uma lista de políticas de cópia de segurança de Olá, os respetivos tipos, volumes Olá associado, número Olá de retenção de cópias de segurança e Olá opção tooenable estas políticas.

Olá **políticas de cópia de segurança** página também permite-lhe toofilter Olá cópia de segurança políticas existentes por uma ou mais Olá seguintes campos:

* **Nome da política** – hello nome associado Olá política. Olá os diferentes tipos de políticas incluem:
  
  * Políticas agendadas, explicitamente são criadas pelo utilizador Olá.
  * Políticas automáticas, que são criadas quando o momento de Olá de criação de volumes de cópia de segurança do Olá predefinida para esta opção de volume foi ativada. Estas políticas são designadas como VolumeName_Default onde o nome do Volume refere-se nome toohello Olá volume StorSimple configurada pelo utilizador Olá Olá portal clássico do Azure. políticas automática Olá resultam em diária instantâneos de nuvem a partir do momento de dispositivo de 22:30.
  * Importar políticas, que foram criadas originalmente no Olá Snapshot Manager do StorSimple. Estes tem uma etiqueta que descreve o anfitrião do Olá Snapshot Manager do StorSimple que políticas Olá foram importadas a partir.
* **Volumes** – Olá volumes associados Olá política. Todos os volumes de Olá associados uma política de cópia de segurança são agrupados quando forem criadas cópias de segurança.
* **Última cópia de segurança com êxito** – Olá data e hora do Olá última cópia de segurança que foi feita com esta política.
* **Cópia de segurança seguinte** – Olá data e hora do Olá próxima cópia de segurança agendada que será iniciada por esta política.
* **As agendas** – Olá diversas agendas associados a política de cópia de segurança de Olá.

operações de Olá utilizada frequentemente que pode efetuar nesta página são:

* Adicionar uma política de cópias de segurança 
* Adicionar ou modificar uma agenda 
* Eliminar uma política de cópia de segurança 
* Efetuar uma cópia de segurança manual 
* Criar uma política de cópia de segurança personalizada com vários volumes e agendas 

## <a name="add-a-backup-policy"></a>Adicionar uma política de cópias de segurança
Adicione uma agenda de tooautomatically de política de cópia de segurança as cópias de segurança. Efetue Olá os seguintes passos no Olá tooadd portal clássico do Azure uma política de cópia de segurança para o dispositivo StorSimple. Depois de adicionar política Olá, pode definir uma agenda (consulte [adicionar ou modificar uma agenda](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

![Vídeo disponível](./media/storsimple-manage-backup-policies/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como toocreate local ou na nuvem de cópia de segurança política, clique em [aqui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).

## <a name="add-or-modify-a-schedule"></a>Adicionar ou modificar uma agenda
Pode adicionar ou modificar uma agenda de cópia de segurança de política existente anexado tooan no dispositivo StorSimple. Execute Olá os seguintes passos no Olá tooadd de portal clássico do Azure ou modificar uma agenda.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a>Eliminar uma política de cópia de segurança
Efetue Olá os seguintes passos no Olá toodelete portal clássico do Azure uma política de cópia de segurança no dispositivo StorSimple.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Efetuar uma cópia de segurança manual
Efetue Olá os seguintes passos no Olá toocreate portal clássico do Azure uma pedido () cópia de segurança manual de um único volume.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Criar uma política de cópia de segurança personalizada com vários volumes e agendas
Execute os seguintes passos no Olá toocreate portal clássico do Azure uma política de cópia de segurança personalizada que tenha vários volumes e agendas de Olá.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre [utilizando Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

