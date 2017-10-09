---
title: "aaaStorSimple a ativação pós-falha, recuperação após desastre para os dispositivos de 8000 série | Microsoft Docs"
description: Saiba como toofail ao longo do seu toohello do dispositivo StorSimple mesmo dispositivo.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>Efetuar a ativação pós-falha do dispositivo toosame dispositivo físico StorSimple

## <a name="overview"></a>Descrição geral

Este tutorial descreve Olá passos necessários toofail através de um tooitself de dispositivo físico de série 8000 do StorSimple se ocorrer um desastre. StorSimple utiliza Olá os dados de toomigrate da funcionalidade de ativação pós-falha de dispositivo de um dispositivo físico de origem no dispositivo físico do Olá datacenter tooanother. orientações de Olá neste tutorial aplica-se tooStorSimple 8000 físico dispositivos das séries com versões do software Update 3 e posterior.

toolearn mais informações sobre a ativação pós-falha do dispositivo e como é utilizado toorecover de desastres, aceda demasiado[ativação pós-falha e recuperação após desastre para os dispositivos de série 8000 do StorSimple](storsimple-8000-device-failover-disaster-recovery.md).

toofail através de um dispositivo físico tooanother dispositivo físico, aceda demasiado[falhar toohello mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-physical-device.md). toofail através de um tooa do dispositivo físico StorSimple dispositivo de nuvem do StorSimple, aceda demasiado[falhar tooa dispositivo de nuvem do StorSimple](storsimple-8000-device-failover-cloud-appliance.md).


## <a name="prerequisites"></a>Pré-requisitos

- Certifique-se de que reviu Olá as considerações para ativação pós-falha do dispositivo. Para mais informações, visite demasiado[considerações comuns para ativação pós-falha do dispositivo](storsimple-8000-device-failover-disaster-recovery.md).


## <a name="steps-toofail-over-toohello-same-device"></a>Passos toofail através de toohello mesmo dispositivo

Efetuar Olá os passos seguintes se precisar de toofail sobre toohello mesmo dispositivo.

1. Criar instantâneos de nuvem de todos os volumes de Olá no seu dispositivo. Para mais informações, visite demasiado[cópias de segurança do Gestor de dispositivos do StorSimple utilize serviço toocreate](storsimple-8000-manage-backup-policies-u2.md).
2. Repor as predefinições de toofactory de dispositivo. Siga instruções de detalhado Olá [como predefinições tooreset um toofactory do dispositivo StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Aceda toohello do serviço StorSimple Manager de dispositivo e, em seguida, selecione **dispositivos**. No Olá **dispositivos** painel, o dispositivo antigo Olá deve mostrar como **Offline**.

    ![Dispositivo de origem offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. Configurar o dispositivo e registá-lo com o serviço do Gestor de dispositivos do StorSimple. Olá dispositivo recentemente registado deve mostrar como **pronto tooset segurança**. nome de dispositivo Olá para novo dispositivo de Olá é Olá igual ao dispositivo antigo Olá, mas tem anexado um tooindicate numeral desse dispositivo Olá foi reposição toofactory predefinido e registado novamente.

    ![Dispositivo recentemente registado tooset pronto cópias de segurança](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Para o novo dispositivo Olá, conclua a configuração de dispositivo Olá. Para mais informações, visite demasiado[passo 4: concluir a configuração mínima do dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup). No Olá **dispositivos** painel, Olá estado do dispositivo Olá é alterado demasiado**Online**.

   > [!IMPORTANT]
   > **Concluir a configuração mínima Olá pela primeira vez, ou a DR poderão falhar.**

    ![Dispositivo recentemente registado online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Selecione o dispositivo de antigo Olá (estado offline) e a partir da barra de comando Olá, clique em **falhar**. No Olá **falhar** painel, selecione o dispositivo antigo como origem de Olá e especifique o dispositivo de destino Olá como Olá recentemente registado o dispositivo.

    ![Resumo de ativação pós-falha](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    Para obter instruções detalhadas, consulte demasiado[efetuar a ativação pós-falha do dispositivo físico tooanother](#fail-over-to-another-physical-device).

7. É criada uma tarefa de restauro do dispositivo, que pode monitorizar a partir da Olá **tarefas** painel.

8. Depois da tarefa de Olá foi concluída com êxito, aceder ao dispositivo novo Olá e navegue toohello **contentores de Volume** painel. Certifique-se de que todos os contentores de volume de Olá de dispositivo antigo Olá foram migradas toohello novo dispositivo.

   ![Os contentores de volume migrado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Após a conclusão da ativação pós-falha de Olá, pode desativar e eliminar dispositivo antigo Olá a partir do portal de Olá. Selecione Olá antigo dispositivo (offline), botão direito e, em seguida, selecione **desativar**. Depois do dispositivo de Olá está desativado, o estado de Olá do dispositivo Olá é atualizado.

     ![Dispositivo de origem desativado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. Selecione Olá desativou o dispositivo, rato e, em seguida, selecione **eliminar**. Isto elimina dispositivo Olá da lista de Olá de dispositivos.

    ![Dispositivo de origem eliminado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>Passos seguintes

* Depois de ter de efetuar uma ativação pós-falha, poderá ser necessário demasiado[desative ou elimine o dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Para obter informações sobre como toouse Olá StorSimple Manager de dispositivo de serviço, visite demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

