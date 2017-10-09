---
title: aaaDeactivate e eliminar um dispositivo StorSimple | Microsoft Docs
description: "Descreve como o dispositivo StorSimple tooremove do serviço ao desativar-o primeiro e, em seguida, eliminá-lo."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>Desativar e eliminar um dispositivo da série 8000 do StorSimple através do serviço StorSimple Manager
## <a name="overview"></a>Descrição geral
Pode ser útil tootake um dispositivo StorSimple fora de serviço (por exemplo, se estiver a substituir ou atualizar o seu dispositivo ou se já não estiver a utilizar StorSimple). Se for este caso de Olá, precisa de dispositivo de Olá toodeactivate antes de poder eliminá-la. Desativar servidores ligação Olá entre o dispositivo de Olá e do serviço StorSimple Manager Olá correspondente. Este tutorial explica como tooremove um dispositivo StorSimple do serviço ao desativar-o primeiro e, em seguida, eliminá-lo. 

Quando desativar um dispositivo, todos os dados que foram armazenados localmente no dispositivo Olá deixará de estar acessíveis. Apenas os dados de Olá associados ao dispositivo Olá que foram armazenado na nuvem de Olá podem ser recuperados.  

> [!WARNING]
> A desativação de uma operação permanente e não pode ser anulada. Não é possível registar um dispositivo desativado com o serviço do StorSimple Manager Olá, a menos que é primeiro repor toohello predefinições de fábrica. 
> 
> Olá reposição de fábrica do processo elimina todos os dados de Olá que foram armazenados localmente no seu dispositivo. Por conseguinte, é essencial que tirar um instantâneo de nuvem de todos os seus dados antes de desativar um dispositivo. Isto permitirá toorecover Olá todos os dados, uma fase posterior.
> 
> 

Este tutorial explica como:

* Desativar um dispositivo e eliminação de dados de Olá
* Desativar um dispositivo e manter os dados de Olá

Também explica como a desativação e a eliminação funciona num dispositivo virtual StorSimple.

> [!NOTE]
> Antes de desativar um dispositivo StorSimple de físico ou virtual, certifique-se de que toostop ou elimina os clientes e anfitriões que dependem desse dispositivo.
> 
> 

## <a name="deactivate-and-delete-data"></a>Desativar e eliminação de dados
Se estiver interessado em eliminar completamente o dispositivo de Olá e não pretender que dados de Olá tooretain no dispositivo Olá, em seguida, conclua Olá os seguintes passos.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate Olá dispositivo e delete Olá dados
1. Toodeactivating antes de um dispositivo, tem de eliminar todos os Olá volume contentores (e volumes de Olá) associados Olá dispositivo. Pode eliminar contentores de volume apenas depois de ter eliminado as cópias de segurança Olá associado.
2. Desative o dispositivo de Olá da seguinte forma:
   
   1. No Olá serviço StorSimple Manager **dispositivos** página, o dispositivo de Olá selecione desejar toodeactivate e, em Olá parte inferior da página Olá, clique em **desativar**.
   2. Será apresentada uma mensagem de confirmação. Clique em **Sim** toocontinue. Olá desativar processo irá iniciar e demorar alguns minutos toocomplete.
3. Após a desativação, pode eliminar dispositivo Olá completamente. Eliminar um dispositivo remove-o da lista de Olá de serviço ligado toohello de dispositivos. serviço de Olá, em seguida, pode deixará de gerir dispositivos Olá eliminado. Utilize Olá dispositivo de Olá toodelete de passos a seguir:
   
   1. No Olá serviço StorSimple Manager **dispositivos** página, selecione um dispositivo desativado que pretende toodelete.
   2. Na parte inferior de Olá na página Olá, clique em **eliminar**.
   3. Será solicitado para confirmação. Clique em **Sim** toocontinue.
      
      Pode demorar alguns minutos para Olá dispositivo toobe eliminado.

## <a name="deactivate-and-retain-data"></a>Desativar e manter os dados
Se tiver está interessadas nas eliminar dispositivo Olá, mas pretende tooretain Olá dados, em seguida, conclua Olá os seguintes passos.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate um dispositivo e manter os dados de Olá
1. Desative o dispositivo de Olá. Olá todos os contentores de volume e Olá os instantâneos de dispositivo Olá permanecerá.
   
   1. No Olá serviço StorSimple Manager **dispositivos** página, o dispositivo de Olá selecione desejar toodeactivate e, em Olá parte inferior da página Olá, clique em **desativar**.
   2. Será apresentada uma mensagem de confirmação. Clique em **Sim** toocontinue. Olá desativar processo irá iniciar e demorar alguns minutos toocomplete.
2. Agora pode efetuar a ativação pós-falha de contentores de volume Olá e instantâneos de Olá associado. Para obter os procedimentos, vá demasiado[ativação pós-falha e recuperação após desastre para o dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md).
3. Após a desativação e a ativação pós-falha, pode eliminar dispositivo Olá completamente. Eliminar um dispositivo remove-o da lista de Olá de serviço ligado toohello de dispositivos. serviço de Olá, em seguida, pode deixará de gerir dispositivos Olá eliminado. Conclua Olá dispositivo de Olá toodelete de passos a seguir:
   
   1. No Olá serviço StorSimple Manager **dispositivos** página, selecione um dispositivo desativado que pretende toodelete.
   2. Na parte inferior de Olá na página Olá, clique em **eliminar**.
   3. Será solicitado para confirmação. Clique em **Sim** toocontinue.
      
      Pode demorar alguns minutos para Olá dispositivo toobe eliminado.

## <a name="deactivate-and-delete-a-virtual-device"></a>Desativar e eliminar um dispositivo virtual
Para um dispositivo virtual StorSimple, à desativação deallocates Olá máquina. Em seguida, pode eliminar máquina virtual de Olá e recursos de Olá criados quando foi aprovisionado. Depois do dispositivo virtual Olá ter sido desativado, não é possível restaurar o estado anterior tooits. 

Resultados de Desativação na Olá seguintes ações:

* o dispositivo virtual StorSimple Olá é removido.
* Olá OSDisk e discos de dados criada para o dispositivo virtual StorSimple Olá são removidos.
* Olá serviço alojado e a rede Virtual que foram criados durante o aprovisionamento são retidos. Se não estiver a utilizar estas entidades, deverá eliminá-los manualmente.
* Instantâneos de nuvem criados através do dispositivo virtual StorSimple Olá são retidos.

## <a name="next-steps"></a>Passos seguintes
* toorestore Olá as predefinições do dispositivo desativado toofactory, visite demasiado[repor as predefinições do Olá dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Para obter assistência técnica, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md).
* mais informações sobre como toolearn como toouse Olá serviço StorSimple Manager, aceda demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md). 

