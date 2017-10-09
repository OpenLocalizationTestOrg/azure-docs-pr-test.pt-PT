---
title: aaaChange as palavras-passe do StorSimple | Microsoft Docs
description: "Descreve como toouse Olá toochange de serviço do Gestor de dispositivos do StorSimple os Snapshot Manager do StorSimple e dispositivo administrador palavras-passe."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>Utilizar toochange de serviço do Gestor de dispositivos do StorSimple Olá as palavras-passe do StorSimple

## <a name="overview"></a>Descrição geral
portal do Azure de Olá **definições do dispositivo** opção contém todos os parâmetros de dispositivo Olá pode reconfigurar num dispositivo StorSimple que é gerido por um serviço do Gestor de dispositivos do StorSimple. Este tutorial explica como pode utilizar Olá **segurança** opção em **definições do dispositivo** toochange o administrador do dispositivo ou a palavra-passe do Snapshot Manager do StorSimple.

## <a name="change-hello-device-administrator-password"></a>Palavra-passe de administrador do dispositivo de Olá de alteração
Quando utilizar o dispositivo do Windows PowerShell interface tooaccess Olá StorSimple, são necessário tooenter uma palavra-passe de administrador do dispositivo. Quando o dispositivo StorSimple primeiro Olá é registado com um serviço, a palavra-passe do Olá predefinida para esta interface é *Password1*. Para segurança Olá dos seus dados, é necessário toochange esta palavra-passe no fim de Olá do processo de registo Olá. Não pode sair do processo de registo Olá sem alterar esta palavra-passe. Para obter mais informações, consulte [passo 3: configurar e registar o dispositivo de Olá através do Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

palavra-passe de Olá que primeiro foi definido através da interface do Windows PowerShell Olá durante o registo pode ser alterado posteriormente através de Olá portal do Azure. Efetue Olá os seguintes passos toochange Olá dispositivo palavra-passe.

#### <a name="toochange-hello-device-administrator-password"></a>palavra-passe de administrador de dispositivo de Olá toochange
1. Aceda tooyour do serviço StorSimple Manager de dispositivo e clique em **dispositivos**.

2. Na lista tabela Olá, dos dispositivos, selecione e clique em dispositivo Olá cuja palavras-passe que tenciona toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. No Olá **definições** painel, vá demasiado**definições do dispositivo > segurança**.

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. No Olá **definições de segurança** painel, clique em **palavra-passe** palavra-passe de administrador de dispositivo de Olá toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. No Olá **palavra-passe** painel, forneça uma palavra-passe de administrador que contém 8 too15 carateres. palavra-passe de Olá tem de ser uma combinação de 3 ou mais carateres em maiúsculas, minúsculas, numérico e especiais.

6. Confirme a palavra-passe de Olá.

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. Clique em **guardar** e quando for pedida a confirmação, clique em **Sim**.

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

palavra-passe de administrador de dispositivo Olá agora deve ser atualizado. Pode utilizar esta palavra-passe modificado tooaccess Olá do Windows PowerShell interface.

## <a name="set-hello-storsimple-snapshot-manager-password"></a>Palavra-passe do conjunto Olá Snapshot Manager do StorSimple
Software Snapshot Manager do StorSimple reside no anfitrião do Windows e permite aos administradores toomanage cópias de segurança do dispositivo StorSimple no formulário de Olá de locais e instantâneos de nuvem.

Quando configurar um dispositivo no Snapshot Manager do StorSimple, será solicitado tooprovide Olá tooauthenticate de palavra-passe e endereço IP do dispositivo, o dispositivo de armazenamento.

Pode definir ou alterar a palavra-passe de Olá para Snapshot Manager do StorSimple através de Olá portal do Azure. Efetuar Olá tooset passos a seguir e alterar palavra-passe do Olá Snapshot Manager do StorSimple.

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>palavra-passe do tooset Olá Snapshot Manager do StorSimple
1. Aceda tooyour do serviço StorSimple Manager de dispositivo e clique em **dispositivos**.

2. Na lista tabela Olá, dos dispositivos, selecione e clique em dispositivo Olá cuja palavras-passe do Snapshot Manager do StorSimple que tenciona tooset ou altere.

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. No Olá **definições** painel, vá demasiado**definições do dispositivo > segurança**.

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. No Olá **definições de segurança** painel, clique em **palavra-passe** tooset alteração Olá Snapshot Manager do StorSimple da palavra-passe.

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. No Olá **palavra-passe** painel, introduza uma palavra-passe 14 ou 15 carateres. Certifique-se de que essa palavra-passe de Olá contém uma combinação de 3 ou mais carateres em maiúsculas, minúsculas, numérico e especiais.

6. Confirme a palavra-passe de Olá.

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. Clique em **guardar** e quando for pedida a confirmação, clique em **Sim**.

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

agora deve ser atualizado a palavra-passe do Olá Snapshot Manager do StorSimple.

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [segurança do StorSimple](storsimple-8000-security.md).
* Saiba mais sobre [modificar a configuração do dispositivo](storsimple-8000-modify-device-config.md).
* Saiba mais sobre [utilizando Olá tooadminister de serviço do Gestor de dispositivos do StorSimple com o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

