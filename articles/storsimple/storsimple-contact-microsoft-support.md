---
title: "aaaLog pedido de suporte para a série 8000 do StorSimple | Microsoft Docs"
description: "Saiba como toocreate um suporte de pedido e iniciar uma sessão de suporte no dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a>Contacte o suporte da Microsoft para do StorSimple
Se tiver quaisquer problemas com a sua solução do Microsoft Azure StorSimple, pode criar um pedido de serviço para o suporte técnico. Numa sessão com o seu engenheiro de suporte online, também poderá ser necessário toostart uma sessão de suporte no dispositivo StorSimple. Este artigo explica como:

* Como toocreate um suporte de pedidos.
* Como toostart uma sessão de suporte no Olá interface do Windows PowerShell do dispositivo StorSimple.

Olá revisão [SLAs de suporte de série do StorSimple 8000 e informações](https://msdn.microsoft.com/library/mt433077.aspx) antes de criar um pedido de suporte.

## <a name="create-a-support-request"></a>Criar um pedido de suporte
Execute os seguintes passos toocreate um pedido de suporte de Olá:

#### <a name="toocreate-a-support-request"></a>toocreate um pedido de suporte
1. No Olá [portal clássico do Azure](https://manage.windowsazure.com/), no Olá canto superior direito, clique em seu nome de conta e, em seguida, clique em **contactar o suporte da Microsoft**.
   
    ![MS contacte o suporte através do ManagementPortal](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. Será redirecionado toohello novo portal do Azure (portal.azure.com). Clique em Olá **novo pedido de suporte** mosaico.
   
    ![MS contacte o suporte através do novo portal](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    No lado direito de Olá do ecrã de Olá, Olá **novo pedido de suporte** painel aparece. 
   
    ![Novo painel de pedido de suporte](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. No Olá **Noções básicas** caixa de diálogo, Olá concluir os seguintes:                                
   
   1. De Olá **emitir tipo** na lista pendente, selecione **técnica**.
   2. Selecione um **subscrição** de Olá na lista pendente.
   3. De Olá **serviço** na lista pendente, selecione **StorSimple**. 
   4. Selecione um **plano de suporte** de Olá na lista pendente. É necessário um tooenable do plano de suporte pago suporte técnico.
4. Clique em **Seguinte**. Olá **problema** é apresentada a caixa de diálogo.
   
    ![Novo painel de pedido de suporte](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. No Olá **problema** caixa de diálogo, Olá concluir os seguintes:
   
   1. Selecione um **gravidade** ao nível do Olá na lista pendente.
   2. Selecione um **tipo de problema** de Olá na lista pendente.
   3. Selecione um **categoria** de Olá na lista pendente. 
   4. No Olá **detalhes** caixa, descreva resumidamente o seu problema.
   5. No Olá **período de tempo** caixa, indique Olá data, hora e fuso horário que corresponde ao toohello ocorrência mais recente do seu problema.
   6. Em **carregamento de ficheiros**, clique em pacote de suporte de tooyour ícone toobrowse Olá pasta.
   7. Selecione Olá **partilhar informações de diagnóstico** caixa de verificação.
6. Clique em **Seguinte**. Olá **informações de contacto** é apresentada a caixa de diálogo.
   
    ![Novo painel de pedido de suporte](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. Introduza as informações de contacto e selecione um método de contacto (telefone ou e-mail). 
8. Selecione Olá **guardar alterações de contactos para futuros pedidos de suporte** caixa de verificação.
9. Clique em **Criar**.

Depois de ter submetido o pedido, um engenheiro de suporte irá contactá-lo logo que possível tooproceed com o seu pedido.

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a>Iniciar uma sessão de suporte no Windows PowerShell para StorSimple
tootroubleshoot os problemas que pode ocorrer com o dispositivo StorSimple Olá, terá de tooengage com a equipa do Olá Support da Microsoft. Support da Microsoft podem ter toouse um toolog de sessão de suporte no dispositivo tooyour. 

Execute o seguinte Olá passos toostart uma sessão de suporte:

#### <a name="toostart-a-support-session"></a>toostart uma sessão de suporte
1. Acesso Olá o dispositivo diretamente utilizando a consola de série de Olá ou através de uma sessão telnet a partir de um computador remoto. toodo, passos Olá siga [utilizar o PuTTY tooconnect toohello consola de série dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Na sessão de Olá que se abre, prima Olá **Enter** tooget chave numa linha de comandos.
3. No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**.
4. Na linha de Olá, escreva Olá seguinte palavra-passe: 
   
    `Password1`
5. Na linha de Olá, escreva Olá os seguintes comandos:
   
    `Enable-HcsSupportAccess`
6. Será apresentada uma cadeia encriptada tooyou. Copie esta cadeia para um editor de texto como o bloco de notas.
7. Guarde esta cadeia e envie-num tooMicrosoft de mensagem de e-mail suporte. 

> [!IMPORTANT]
> Pode desativar o acesso de suporte executando `Disable-HcsSupportAccess`. o dispositivo StorSimple Olá também tentará toodisable suporte acesso 8 horas após a sessão de Olá foi iniciada. É uma melhor toochange de prática o dispositivo StorSimple credenciais depois de iniciar uma sessão de suporte.
> 
> 

