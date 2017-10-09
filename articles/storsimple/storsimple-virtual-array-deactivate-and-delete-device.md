---
title: aaaDeactivate e eliminar uma matriz Virtual do Microsoft Azure StorSimple | Microsoft Docs
description: "Descreve como o dispositivo StorSimple tooremove do serviço ao desativar-o primeiro e, em seguida, eliminá-lo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>Desativar e eliminar uma matriz de Virtual StorSimple

## <a name="overview"></a>Descrição geral

Ao desativar uma matriz de Virtual StorSimple, interromper a ligação de Olá entre dispositivos de Olá e Olá correspondente o serviço do Gestor de dispositivos do StorSimple. Este tutorial explica como:

* Desativar um dispositivo 
* Eliminar um dispositivo desativado

informações de Olá neste artigo aplicam-se apenas tooStorSimple matrizes Virtual. Para informações sobre 8000 série, visite toohow demasiado[desativar ou eliminar um dispositivo](storsimple-deactivate-and-delete-device.md).

## <a name="when-toodeactivate"></a>Quando toodeactivate?

A desativação de uma operação permanente e não pode ser anulada. Não é possível registar um dispositivo desativado com Olá serviço StorSimple Manager de dispositivo novamente. Poderá ter toodeactivate e eliminar uma matriz de Virtual StorSimple no Olá os seguintes cenários:

* **A ativação pós-falha planeada** : O dispositivo está online e se planear toofail ao longo do seu dispositivo. Se estiver a planear tooupgrade tooa maior dispositivo, poderá ser necessário toofail ao longo do seu dispositivo. Depois de propriedade de dados de Olá é transferida e Olá ativação estiver concluída, o dispositivo de origem Olá é eliminado automaticamente.
* **Ativação pós-falha não planeada** : O dispositivo estiver offline e precisar de toofail sobre dispositivos Olá. Este cenário poderá ocorrer durante um desastre quando houver uma falha no datacenter de Olá e o dispositivo primário está inativo. Planear toofail através de dispositivo do Olá dispositivo tooa secundário. Depois de propriedade de dados de Olá é transferida e Olá ativação estiver concluída, o dispositivo de origem Olá é eliminado automaticamente.
* **Desativar** : pretende que o dispositivo de Olá toodecommission. Isto requer toofirst desativar Olá dispositivo e, em seguida, eliminá-lo. Quando desativar um dispositivo, já não pode aceder a todos os dados que esteja armazenados localmente. Pode apenas acesso e recuperar Olá os dados armazenados na nuvem de Olá. Se planear os dados de dispositivos de Olá tookeep após a desativação, deve ter um instantâneo de nuvem de todos os seus dados antes de desativar um dispositivo. Este instantâneo na nuvem permite-lhe toorecover Olá todos os dados, uma fase posterior.

## <a name="deactivate-a-device"></a>Desativar um dispositivo

toodeactivate seu dispositivo, efetuar Olá os seguintes passos.

#### <a name="toodeactivate-hello-device"></a>dispositivo de Olá toodeactivate

1. No seu serviço, visite demasiado**gestão > dispositivos**. No Olá **dispositivos** painel, clique e dispositivo Olá Selecione se pretende toodeactivate.
   
    ![Selecione o dispositivo toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. No seu **dashboard dispositivo** painel, clique em **... Mais** e na lista de Olá, selecione **desativar**.
   
    ![Clique em Desativar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. No Olá **desativar** painel, nome de dispositivo do tipo Olá e, em seguida, clique em **desativar**. 
   
    ![Confirmar a desativar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    Olá desativar processo inicia e demora alguns minutos toocomplete.
   
    ![Desativar em curso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. Após a desativação, atualiza a lista de Olá dos dispositivos.
   
    ![Desativar concluída](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    Pode agora eliminar este dispositivo.

## <a name="delete-hello-device"></a>Eliminar Olá dispositivo

Um dispositivo tem toodelete de desativado primeiro toobe-lo. Eliminar um dispositivo remove-o da lista de Olá de serviço ligado toohello de dispositivos. serviço de Olá, em seguida, pode deixará de gerir dispositivos Olá eliminado. No entanto permanecem dados Olá associados ao dispositivo Olá na nuvem de Olá. Estes dados accrues, em seguida, os encargos.

dispositivo de Olá toodelete, efetuar Olá os seguintes passos.

#### <a name="toodelete-hello-device"></a>dispositivo de Olá toodelete

1. No Gestor de dispositivos do StorSimple, aceda demasiado**gestão > dispositivos**. No Olá **dispositivos** painel, selecione um dispositivo desativado que pretende toodelete.
2. No Olá **dashboard dispositivo** painel, clique em **... Mais** e, em seguida, clique em **eliminar**.
   
   ![Selecione o dispositivo toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. No Olá **eliminar** painel, o nome do tipo Olá da sua eliminação do dispositivo tooconfirm Olá e, em seguida, clique em **eliminar**. Eliminar dispositivos de Olá não elimina dados de nuvem Olá associados Olá dispositivo. 
   
   ![Confirmar eliminação](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. eliminação de Olá é iniciado e demora alguns minutos toocomplete.
   
   ![Eliminar em curso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    Depois do dispositivo Olá é eliminado, pode ver lista Olá atualizado de dispositivos.

## <a name="next-steps"></a>Passos seguintes

* Para obter informações sobre como toofail, aceda demasiado[ativação pós-falha e recuperação após desastre da sua matriz de Virtual StorSimple](storsimple-virtual-array-failover-dr.md).

* mais informações sobre como toolearn como toouse Olá serviço Gestor de dispositivos do StorSimple, aceda demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple a matriz de Virtual StorSimple](storsimple-virtual-array-manager-service-administration.md). 

