---
title: "aaaDeactivate e eliminar um dispositivo de série 8000 do StorSimple | Microsoft Docs"
description: "Descreve como o dispositivo StorSimple tooremove do serviço ao desativar-o primeiro e, em seguida, eliminá-lo."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>Desativar e eliminar um dispositivo StorSimple

## <a name="overview"></a>Descrição geral

Este artigo descreve como toodeactivate e eliminar um dispositivo StorSimple que é ligado tooa serviço StorSimple Manager do dispositivo. orientações de Olá neste artigo aplica-se apenas tooStorSimple série 8000 os dispositivos, incluindo aplicações de nuvem Olá StorSimple. Se estiver a utilizar uma matriz de Virtual StorSimple, em seguida, aceda demasiado[desativar e eliminar uma matriz de Virtual StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

A desativação de servidores de ligação de Olá entre dispositivos de Olá e Olá correspondente o serviço do Gestor de dispositivos do StorSimple. Pode ser útil tootake um dispositivo StorSimple fora de serviço (por exemplo, se estiver a substituir ou atualizar o seu dispositivo ou se já não estiver a utilizar StorSimple). Se Sim, terá de dispositivo de Olá toodeactivate antes de poder eliminá-la.

Quando desativar um dispositivo, todos os dados que foram armazenados localmente no dispositivo Olá já não estão acessíveis. Apenas os dados de Olá associados ao dispositivo Olá que foram armazenado na nuvem de Olá podem ser recuperados.

> [!WARNING]
> A desativação de uma operação permanente e não pode ser anulada. Não é possível registar um dispositivo desativado com Olá serviço StorSimple Manager de dispositivo, a menos que seja repor as predefinições de toofactory.
>
> Olá reposição de fábrica do processo elimina todos os dados de Olá que foram armazenados localmente no seu dispositivo. Por conseguinte, tem de colocar um instantâneo de nuvem de todos os seus dados antes de desativar um dispositivo. Este instantâneo na nuvem permite-lhe toorecover Olá todos os dados, uma fase posterior.

Depois de ler este tutorial, será capaz de:

* Desativar um dispositivo e eliminação de dados de Olá.
* Desativar um dispositivo e manter os dados de Olá.

> [!NOTE]
> Antes de desativar um dispositivo físico StorSimple ou um dispositivo de nuvem, pare ou elimine a clientes e anfitriões que dependem desse dispositivo.


## <a name="deactivate-and-delete-data"></a>Desativar e eliminação de dados

Se estiver interessado em eliminar completamente o dispositivo de Olá e não pretender que dados de Olá tooretain no dispositivo Olá, em seguida, conclua Olá os seguintes passos.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate Olá dispositivo e delete Olá dados

1. Antes de desativar um dispositivo, tem de eliminar todos os Olá volume contentores (e volumes de Olá) associados Olá dispositivo. Pode eliminar contentores de volume apenas depois de ter eliminado as cópias de segurança Olá associado.

    > [!NOTE]
    > Antes de desativar um dispositivo físico StorSimple ou um dispositivo de nuvem, certifique-se de que realmente forem eliminados dados de Olá do contentor de volume Olá eliminado do dispositivo Olá. Pode monitorizar os gráficos de consumo de nuvem Olá e quando for apresentada a utilização de nuvem Olá drop devido às cópias de segurança de Olá que tiver eliminado, em seguida, pode avançar dispositivo de Olá toodeactivate. Se desativar o dispositivo de Olá antes deste largar ocorre, Olá dados é stranded na conta do storage Olá e accrues encargos.

2. Desative o dispositivo de Olá da seguinte forma:
   
   1. Aceda tooyour do serviço StorSimple Manager de dispositivo e clique em **dispositivos**. No Olá **dispositivos** painel, o dispositivo de Olá Selecione se pretende toodeactivate, rato e, em seguida, clique em **desativar**.

        ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. No Olá **desativar** painel, escreva tooconfirm de nome de dispositivo Olá e, em seguida, clique em **desativar**. Olá desativar processo inicia e demora alguns minutos toocomplete.

        ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. Após a desativação, pode eliminar dispositivo Olá completamente. Eliminar um dispositivo remove-o da lista de Olá de serviço ligado toohello de dispositivos. serviço de Olá, em seguida, pode deixará de gerir dispositivos Olá eliminado. Utilize Olá dispositivo de Olá toodelete de passos a seguir:
   
   1. Aceda tooyour do serviço StorSimple Manager de dispositivo e clique em **dispositivos**. No Olá **dispositivos** painel, o dispositivo de Olá selecione desativado que pretende toodelete, rato e, em seguida, clique em **eliminar**.

        ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. No Olá **eliminar** painel, escreva tooconfirm de nome de dispositivo Olá e, em seguida, clique em **eliminar**. eliminação de Olá demora alguns minutos toocomplete.

        ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Após a conclusão com êxito da eliminação de Olá, será notificado. lista de dispositivos de Olá também atualiza a eliminação de Olá tooreflect.

## <a name="deactivate-and-retain-data"></a>Desativar e manter os dados

Se tiver está interessadas nas eliminar dispositivo Olá, mas pretende tooretain Olá dados, em seguida, conclua Olá os seguintes passos:

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate um dispositivo e manter os dados de Olá
1. Desative o dispositivo de Olá. Olá todos os contentores de volume e Olá os instantâneos de dispositivo Olá permanecem.
   
   1. Aceda tooyour do serviço StorSimple Manager de dispositivo e clique em **dispositivos**. No Olá **dispositivos** painel, o dispositivo de Olá Selecione se pretende toodeactivate, rato e, em seguida, clique em **desativar**.

         ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. No Olá **desativar** painel, escreva tooconfirm de nome de dispositivo Olá e, em seguida, clique em **desativar**. Olá desativar processo inicia e demora alguns minutos toocomplete.

         ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. Agora pode efetuar a ativação pós-falha de contentores de volume Olá e instantâneos de Olá associado. Para obter os procedimentos, vá demasiado[ativação pós-falha e recuperação após desastre para o dispositivo StorSimple](storsimple-8000-device-failover-disaster-recovery.md).
3. Após a desativação e a ativação pós-falha, pode eliminar dispositivo Olá completamente. Eliminar um dispositivo remove-o da lista de Olá de serviço ligado toohello de dispositivos. serviço de Olá, em seguida, pode deixará de gerir dispositivos Olá eliminado. dispositivo de Olá toodelete, Olá concluir os seguintes passos:
   
   1. Aceda tooyour do serviço StorSimple Manager de dispositivo e clique em **dispositivos**. No Olá **dispositivos** painel, o dispositivo de Olá selecione desativado que pretende toodelete, rato e, em seguida, clique em **eliminar**.

       ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. No Olá **eliminar** painel, escreva tooconfirm de nome de dispositivo Olá e, em seguida, clique em **eliminar**. eliminação de Olá demora alguns minutos toocomplete.

       ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Após a conclusão com êxito da eliminação de Olá, será notificado. lista de dispositivos de Olá também atualiza a eliminação de Olá tooreflect.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>Desativar e eliminar uma aplicação de nuvem

Para uma aplicação de nuvem do StorSimple, a desativação do portal de Olá deallocates e elimina a máquina de virtual Olá e recursos Olá criados no aprovisionamento. Depois do dispositivo de nuvem Olá ter sido desativado, não é possível restaurar o estado anterior tooits.

![Desativar o dispositivo StorSimple nuvem](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

Resultados de Desativação na Olá seguintes ações:

* Olá dispositivo de nuvem do StorSimple é removido do serviço de Olá.
* máquina virtual de Olá para Olá StorSimple nuvem dispositivo é eliminada.
* disco do SO Olá e discos de dados criados para Olá StorSimple nuvem aplicação são removidos.
* serviço de Olá alojado e a rede Virtual que foram criados durante o aprovisionamento são retidos. Se não estiver a utilizar estas entidades, deverá eliminá-los manualmente.
* Instantâneos de nuvem criados por Olá dispositivo do StorSimple nuvem são retidos.

Depois do dispositivo de nuvem Olá está desativado, pode eliminá-lo da lista de Olá dos dispositivos. Selecione Olá desativou o dispositivo, rato e, em seguida, clique em **eliminar**. StorSimple notifica-o assim que o dispositivo Olá é eliminado e Olá a lista de atualizações de dispositivos.

## <a name="next-steps"></a>Passos seguintes

* toorestore Olá as predefinições do dispositivo desativado toofactory, visite demasiado[repor as predefinições do Olá dispositivo toofactory](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Para obter assistência técnica, [contacte a Microsoft Support](storsimple-8000-contact-microsoft-support.md).
* mais informações sobre como toolearn como toouse Olá serviço Gestor de dispositivos do StorSimple, aceda demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

