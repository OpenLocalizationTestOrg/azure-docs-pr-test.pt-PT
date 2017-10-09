---
title: "chassis de aaaReplace no dispositivo de série 8000 do StorSimple | Microsoft Docs"
description: "Descreve como tooremove e substitua Olá chassis para o seu inclusão principal do StorSimple ou a inclusão EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>Substitua o chassis Olá no dispositivo StorSimple
## <a name="overview"></a>Descrição geral
Este tutorial explica como tooremove e substituir um chassis de um dispositivo de série 8000 do StorSimple. modelo de Olá StorSimple 8100 é um dispositivo de inclusão único (chassis), enquanto Olá 8600 é um dispositivo de inclusão dupla (dois chassis). Para um modelo de 8600, existem dois chassis potencialmente poderá falhar num dispositivo Olá: Olá chassis para inclusão principal Olá ou chassis Olá para Olá bastidor EBOD.

Em ambos os casos, o chassis de substituição de Olá que é enviada pela Microsoft está vazio. Sem energia e arrefecimento módulos do (PCMs), módulos de controlador, unidades de disco de estado sólido (SSDs), unidades de disco rígido (HDDs) ou EBOD módulos será incluídos.

> [!IMPORTANT]
> Antes de remover e de substituir chassis Olá, reveja as informações de segurança de Olá na [substituição de componente de hardware do StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-chassis"></a>Remover chassis Olá
Efetue Olá chassis de Olá tooremove de passos a seguir no dispositivo StorSimple.

#### <a name="tooremove-a-chassis"></a>tooremove um chassis
1. Certifique-se de que o dispositivo StorSimple Olá é encerrado e desligado de todas as fontes de alimentação Olá.
2. Remova todos os rede Olá e cabos SAS, se aplicável.
3. Remova unidade de Olá bastidor Olá.
4. Remova a cada uma das unidades de Olá e tenha em atenção as ranhuras Olá partir da qual são removidos. Para obter mais informações, consulte [remover a unidade de disco Olá](storsimple-disk-drive-replacement.md#remove-the-disk-drive).
5. Remova Olá bastidor EBOD (se se tratar de chassis Olá que falharam), módulos de controlador Olá EBOD. Para obter mais informações, consulte [remover um controlador EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller). 
   
    Olá inclusão principal (se se tratar de chassis Olá que falharam), remover controladores de Olá e tenha em atenção as ranhuras Olá partir da qual são removidos. Para obter mais informações, consulte [remover um controlador](storsimple-controller-replacement.md#remove-a-controller).

## <a name="install-hello-chassis"></a>Instalar o chassis Olá
Efetue Olá chassis de Olá tooinstall de passos a seguir no dispositivo StorSimple.

#### <a name="tooinstall-a-chassis"></a>tooinstall um chassis
1. Chassis de Olá num bastidor Olá de montagem. Para obter mais informações, consulte [montar em Bastidor os cabos do 8100 StorSimple dispositivo](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) ou [montar em Bastidor os cabos do 8600 StorSimple dispositivo](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. Depois de chassis Olá está montado num bastidor Olá, instale módulos de controlador Olá Olá posições mesmo tenham sido anteriormente instalados no.
3. Instalação Olá unidades no Olá mesmo posições e ranhuras que anteriormente foram instalados no.
   
   > [!NOTE]
   > Recomendamos que instale Olá SSDs no ranhuras Olá primeiro e, em seguida, instale Olá HDDs.
   > 
   > 
4. Com Olá dispositivo montado num bastidor Olá e componentes de Olá instalados, ligar as fontes de alimentação adequada de toohello do dispositivo e ativar Olá de dispositivos. Para obter mais informações, consulte [instalar os cabos do dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [instalar os cabos do dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre [substituição de componente de hardware do StorSimple](storsimple-hardware-component-replacement.md).

