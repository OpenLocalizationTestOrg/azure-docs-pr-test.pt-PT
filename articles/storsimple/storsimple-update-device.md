---
title: aaaUpdate o dispositivo StorSimple | Microsoft Docs
description: "Explica como toouse Olá StorSimple atualizar funcionalidade tooinstall regular e atualizações de modo de manutenção e as correções."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>Atualizar o seu dispositivo de série de 8000 do StorSimple
## <a name="overview"></a>Descrição geral
Olá StorSimple atualizações funcionalidades permitem-lhe tooeasily par o dispositivo StorSimple. Dependendo do tipo de atualização de Olá, pode aplicar o dispositivo de toohello atualizações através de Olá portal clássico do Azure ou através da interface do Windows PowerShell Olá. Este tutorial descreve os tipos de atualização de Olá e como tooinstall, cada um deles.

Pode aplicar dois tipos de atualizações de dispositivo: 

* Regular (ou modo Normal) atualizações
* Atualizações de modo de manutenção

Pode instalar atualizações regulares através de Olá portal clássico do Azure ou o Windows PowerShell; No entanto, tem de utilizar atualizações de modo de manutenção do Windows PowerShell tooinstall. 

Cada tipo de atualização é descrito em separado, abaixo.

### <a name="regular-updates"></a>Atualizações regulares
Atualizações regulares são não acontece atualizações que podem ser instaladas quando o dispositivo de Olá está no modo Normal. Estas atualizações são aplicadas através do controlador de dispositivo de tooeach de Web site Microsoft Update Olá. 

> [!IMPORTANT]
> Um controlador ativação pós-falha pode ocorrer durante o processo de atualização de Olá. No entanto, isto não irá afetar a disponibilidade de sistema ou a operação.
> 
> 

* Para obter detalhes sobre como tooinstall regular atualizações através de Olá portal clássico do Azure, consulte [instalar atualizações regulares através do portal clássico do Azure de Olá](#install-regular-updates-via-the-azure-classic-portal).
* Também pode instalar atualizações regulares através do Windows PowerShell para StorSimple. Para obter mais informações, consulte [instalar atualizações regulares através do Windows PowerShell para StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).

### <a name="maintenance-mode-updates"></a>Atualizações de modo de manutenção
As atualizações de modo de manutenção são atualizações acontece, tais como atualizações de firmware do disco. Estas atualizações requerem Olá dispositivo toobe colocado em modo de manutenção. Para obter mais informações, consulte [passo 2: modo de manutenção introduza](#step2). Não é possível utilizar atualizações de modo de manutenção do Olá tooinstall de portal clássico do Azure. Em vez disso, deve utilizar o Windows PowerShell para StorSimple. 

Para obter detalhes sobre como o modo de manutenção tooinstall atualizações, consulte [atualizações de modo de manutenção instalar através do Windows PowerShell para StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Modo de manutenção atualizações tem de ser aplicadas em separado tooeach controlador. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Instalar atualizações regulares através de Olá portal clássico do Azure
Pode utilizar o dispositivo do StorSimple tooyour Olá tooapply de portal clássico do Azure atualizações.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Instalar atualizações regulares através do Windows PowerShell para StorSimple
Em alternativa, pode utilizar o Windows PowerShell para as atualizações do StorSimple tooapply regular (modo Normal).

> [!IMPORTANT]
> Apesar de poder instalar atualizações regulares através do Windows PowerShell para StorSimple, recomendamos vivamente que instala atualizações regulares através de Olá portal clássico do Azure. A partir do Update 1, verificações prévias será efetuada tooinstalling anterior atualizações do portal de Olá. Estas verificações prévias serão alta impedem mais falhas e certifique-se de uma experiência smoother. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Instalar atualizações de modo de manutenção através do Windows PowerShell para StorSimple
Utilizar o Windows PowerShell para StorSimple tooapply manutenção modo atualizações tooyour o dispositivo StorSimple. Todos os pedidos de e/s são colocadas em pausa neste modo. Serviços, tais como a memória de acesso aleatório não volátil (NVRAM) ou o serviço de cluster de Olá também estão parados. Tanto os controladores são reiniciados, quando introduzir ou sair neste modo. Quando sair deste modo, todos os serviços de Olá retomará e devem estar em bom estado. (Isto pode demorar alguns minutos.)

Se precisar de atualizações de modo de manutenção tooapply, receberá um alerta através de Olá portal clássico do Azure que tem atualizações que devem ser instaladas. Este alerta inclui instruções para utilizar o Windows PowerShell para as atualizações do StorSimple tooinstall Olá. Depois de atualizar o seu dispositivo, utilize Olá mesmo modo de tooRegular do procedimento toochange Olá dispositivo. Para obter instruções passo a passo, consulte [passo 4: modo de manutenção de saída](#step4).

> [!IMPORTANT]
> * Antes de introduzir o modo de manutenção, certifique-se de que ambos os controladores de dispositivo estão em bom Estados, verificando Olá **estado do Hardware** no Olá **manutenção** página Olá portal clássico do Azure. Se o controlador de Olá não está em bom estado, contacte Support da Microsoft para passos Olá. Para obter mais informações, visite tooContact Support da Microsoft. 
> * Quando estiver no modo de manutenção, terá de tooapply Olá atualização pela primeira vez num controlador e, em seguida, no Olá outro controlador.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>Passo 1: Ligar a consola de série toohello<a name="step1">
Em primeiro lugar, utilize uma aplicação, tais como o PuTTY tooaccess Olá consola de série. Olá procedimento seguinte explica como consola de série do toohello toouse PuTTY tooconnect.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Passo 2: Introduza o modo de manutenção<a name="step2">
Depois de ligar a consola de toohello, determine se existem atualizações tooinstall e introduza tooinstall de modo de manutenção-los.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>Passo 3: Instalar as atualizações<a name="step3">
Em seguida, instale as atualizações.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>Passo 4: Modo de manutenção de saída<a name="step4">
Por fim, saia do modo de manutenção.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>Instalar correções através do Windows PowerShell para StorSimple
Ao contrário das atualizações do Microsoft Azure StorSimple, correções estão instaladas a partir de uma pasta partilhada. Tal como acontece com as atualizações, existem dois tipos de correções: 

* Correções regulares 
* Correções de modo de manutenção  

Olá procedimentos seguintes explicam como toouse do Windows PowerShell para StorSimple tooinstall regular e correções do modo de manutenção.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>O que acontece tooupdates se efetuar uma fábrica de reposição do dispositivo Olá?
Se um dispositivo reposição toofactory definições, todas as atualizações de Olá serão perdidas. Depois do dispositivo de reposição de fábrica Olá registado e configurado, terá de atualizações de instalação de toomanually através de Olá portal clássico do Azure e/ou do Windows PowerShell para StorSimple. Para obter mais informações sobre a reposição de fábrica, consulte [repor as predefinições do Olá dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [através do Windows PowerShell para StorSimple tooadminister o dispositivo StorSimple](storsimple-windows-powershell-administration.md).
* Saiba mais sobre [utilizando Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

