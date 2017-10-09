---
title: "aaaStorSimple a ativação pós-falha, dispositivo físico de série 8000 do StorSimple de tooa de recuperação após desastre | Microsoft Docs"
description: "Saiba como toofail através de 8000 do StorSimple série dispositivo físico tooanother dispositivo físico."
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>Efetuar a ativação pós-falha do dispositivo físico de série tooa 8000 do StorSimple

## <a name="overview"></a>Descrição geral

Este tutorial descreve Olá passos necessários toofail através de um 8000 do StorSimple série dispositivo físico tooanother dispositivo físico StorSimple se ocorrer um desastre. StorSimple utiliza Olá os dados de toomigrate da funcionalidade de ativação pós-falha de dispositivo de um dispositivo físico de origem no dispositivo físico do Olá datacenter tooanother. orientações de Olá neste tutorial aplica-se tooStorSimple 8000 físico dispositivos das séries com versões do software Update 3 e posterior.

toolearn mais informações sobre a ativação pós-falha do dispositivo e como é utilizado toorecover de desastres, aceda demasiado[ativação pós-falha e recuperação após desastre para os dispositivos de série 8000 do StorSimple](storsimple-8000-device-failover-disaster-recovery.md).

toofail através de um tooa do dispositivo físico StorSimple dispositivo de nuvem do StorSimple, aceda demasiado[falhar tooa dispositivo de nuvem do StorSimple](storsimple-8000-device-failover-cloud-appliance.md). toofail através de um dispositivo físico tooitself, aceda demasiado[falhar toohello mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-same-device.md).


## <a name="prerequisites"></a>Pré-requisitos

- Certifique-se de que reviu Olá as considerações para ativação pós-falha do dispositivo. Para mais informações, visite demasiado[considerações comuns para ativação pós-falha do dispositivo](storsimple-8000-device-failover-disaster-recovery.md).

- Tem de ter um dispositivo físico de 8000 do StorSimple série implementado no Centro de dados de Olá. dispositivo de Olá tem de executar atualização 3 ou versão posterior do software. Para mais informações, visite demasiado[implementar o dispositivo StorSimple no local](storsimple-8000-deployment-walkthrough-u2.md).


## <a name="steps-toofail-over-tooa-physical-device"></a>Passos toofail ao longo do dispositivo físico tooa

Efetue Olá os seguintes passos toorestore dispositivo tooa destino dispositivo físico.

1. Certifique-se de que esse contentor de volume Olá que pretende toofail através de associou instantâneos de nuvem. Para mais informações, visite demasiado[cópias de segurança do Gestor de dispositivos do StorSimple utilize serviço toocreate](storsimple-8000-manage-backup-policies-u2.md).
2. Aceda tooyour Gestor de dispositivos do StorSimple e, em seguida, clique em **dispositivos**. No Olá **dispositivos** painel, aceda toohello lista de dispositivos ligados com o serviço.
    ![Selecione o dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. Selecione e clique o dispositivo de origem. dispositivo de origem Olá tem contentores de volume Olá que pretende que sejam toofail ao longo. Aceda demasiado**definições > contentores de Volume**.
4. Selecione um contentor de volume que pretende toofail através de tooanother dispositivo. Clique Olá volume contentor toodisplay Olá lista de volumes dentro deste contentor. Selecione um volume, rato e clique em **Colocar Offline** tootake volume de Olá offline. Repita este processo para todos os volumes de Olá no contentor de volume Olá.
5. Passo anterior Olá repetida para Olá todos os contentores de volume que gostaria de toofail através de tooanother dispositivo.
6. Voltar atrás toohello **dispositivos** painel. A partir da barra de comando Olá, clique em **falhar**.
    ![Clique em ativação pós-falha](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. No Olá **falhar** painel, efetuar Olá os seguintes passos:
   
   1. Clique em **origem**. são apresentados os contentores de volume Olá com volumes associados instantâneos de nuvem. Apenas os contentores de Olá apresentados são elegíveis para ativação pós-falha. Na lista de Olá de contentores de volume, selecione os contentores de volume Olá que gostaria toofail ao longo. **Apenas Olá contentores de volume com instantâneos de nuvem associados e offline volumes são apresentados.**

       ![Selecione a origem](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. Clique em **destino**. Para contentores de volume Olá selecionadas no passo anterior Olá, selecione um dispositivo de destino Olá na lista pendente de dispositivos disponíveis. Apenas os dispositivos Olá que tenham suficientes contentores de volume de origem do capacidade tooaccommodate são apresentados na lista de Olá.

        ![Selecione o destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. Por fim, consultar todas as definições de ativação pós-falha de Olá em **resumo**. Depois de rever as definições de Olá, selecione a caixa de verificação de Olá que indica que os volumes de Olá nos contentores de volume selecionado estão offline. Clique em **OK**.

       ![Reveja as definições de ativação pós-falha](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple cria uma tarefa de ativação pós-falha. Clique em Olá tarefa notificação toomonitor Olá trabalho de ativação pós-falha através de Olá **tarefas** painel.

    Se o contentor de volume de Olá que efetuar a ativação pós-falha tem volumes locais, em seguida, pode ver as tarefas de restauro individuais para cada volume local (e não para volumes em camadas) no contentor de Olá. Estas tarefas de restauro poderá demorar bastante algumas toocomplete de tempo. É provável que essa tarefa de ativação pós-falha Olá poderá concluir anteriormente. Estes volumes terão garantias locais apenas depois de concluídas as tarefas de restauro Olá.

    ![Tarefa de ativação pós-falha de monitorização](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Depois de concluir a ativação pós-falha de Olá, aceda toohello **dispositivos** painel.
   
   1. Selecione o dispositivo de Olá que foi utilizado como dispositivo de destino Olá para o processo de ativação pós-falha de Olá.

       ![Selecione o dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Aceda toohello **contentores de Volume** painel. Todos os contentores de volume Olá, juntamente com volumes Olá do dispositivo de antigo Olá, deverá estar listados.

       ![Contentores de volume de destino de vista](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>Passos seguintes

* Depois de ter de efetuar uma ativação pós-falha, poderá ser necessário demasiado[desative ou elimine o dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Para obter informações sobre como toouse Olá StorSimple Manager de dispositivo de serviço, visite demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

