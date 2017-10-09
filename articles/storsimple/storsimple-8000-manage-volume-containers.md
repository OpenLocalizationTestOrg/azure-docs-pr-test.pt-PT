---
title: "aaaManage os contentores de volume do StorSimple no dispositivo de série de Olá 8000 do StorSimple | Microsoft Docs"
description: "Explica como pode utilizar Olá Gestor de dispositivos do StorSimple contentores de volume do serviço página tooadd, modificarem ou eliminar um contentor de volume."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Utilize contentores de volume de StorSimple serviço toomanage Olá Gestor de dispositivos do StorSimple

## <a name="overview"></a>Descrição geral
Este tutorial explica como toouse Olá toocreate de serviço do Gestor de dispositivos do StorSimple e gerir contentores de volume do StorSimple.

Um contentor de volume no dispositivo Microsoft Azure StorSimple contém um ou mais volumes que partilham a conta de armazenamento, a encriptação e definições de consumo de largura de banda. Um dispositivo pode ter vários contentores de volume para todos os seus volumes. 

Um contentor de volume possui Olá seguintes atributos:

* **Volumes** – Olá camadas ou afixado localmente volumes do StorSimple que estão contidas dentro do contentor de volume Olá. 
* **Encriptação** – uma chave de encriptação pode ser definida para cada contentor de volume. Esta chave é utilizada para encriptar dados Olá que são enviados a partir da nuvem toohello dispositivo StorSimple. Uma chave do nível military AES 256 bits é utilizada com a chave de utilizador introduzido Olá. toosecure os dados, recomendamos que ativar sempre a encriptação de armazenamento de nuvem.
* **Conta de armazenamento** – Olá conta de armazenamento do Azure que seja utilizado toostore Olá dados. Todos os volumes de Olá que residem num contentor de volume partilham esta conta de armazenamento. Pode escolher uma conta de armazenamento a partir de uma lista existente ou crie uma nova conta ao criar o contentor de volume Olá e, em seguida, especifique as credenciais de acesso de Olá para essa conta.
* **Largura de banda da nuvem** – Olá largura de banda consumida pelo dispositivo Olá quando estão a ser enviados dados de Olá de dispositivo Olá toohello nuvem. Pode impor um controlo de largura de banda, especificando um valor entre 1 e 1000 Mbps quando cria este contentor. Se quiser Olá dispositivo tooconsume largura de banda disponível, defina este campo demasiado**ilimitada**. Também pode criar e aplicar uma largura de banda modelo tooallocate da largura de banda com base numa agenda.

Olá procedimentos seguintes explicam como toouse Olá StorSimple **contentores de Volume** Olá do painel toocomplete seguintes operações comuns:

* Adicionar um contentor de volume
* Modificar um contentor de volume
* Eliminar um contentor de volume

## <a name="add-a-volume-container"></a>Adicionar um contentor de volume
Efetue Olá os seguintes passos tooadd um contentor de volume.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modificar um contentor de volume
Efetue Olá os seguintes passos toomodify um contentor de volume.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Eliminar um contentor de volume
Um contentor de volume possui volumes dentro do mesmo. Pode ser eliminado apenas se todos os volumes de Olá nele contidos são eliminados primeiro. Efetue Olá os seguintes passos toodelete um contentor de volume.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [gerir volumes do StorSimple](storsimple-8000-manage-volumes-u2.md). 
* Saiba mais sobre [utilizando Olá tooadminister de serviço do Gestor de dispositivos do StorSimple com o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

