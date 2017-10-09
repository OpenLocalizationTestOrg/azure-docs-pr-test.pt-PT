---
title: "aplicação de autenticador aaaMicrosoft para telemóveis | Microsoft Docs"
description: "Saiba como tooupgrade toohello versão mais recente do Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Introdução à aplicação do Microsoft Authenticator Olá
Olá aplicação Authenticator da Microsoft fornece um nível adicional de segurança na sua conta escolar ou profissional (por exemplo, bsimon@contoso.com) ou a sua conta Microsoft (por exemplo, bsimon@outlook.com).

Olá aplicação funciona de uma das seguintes formas:

* **Notificação**. aplicação Olá pode ajudar a impedir o acesso não autorizado tooaccounts e parar as transações fraudulentas ao enviar uma notificação tooyour smartphone ou tablet. Basta ver notificação Olá e se esta for legítima, selecionar **verifique**. Caso contrário, pode selecionar **negar**. 
* **Código de verificação**. aplicação Olá pode ser utilizada como um software token toogenerate um código de verificação de OAuth. Depois de introduzir o nome de utilizador e palavra-passe, introduza código Olá fornecido pela aplicação Olá no ecrã de início de sessão Olá. código de verificação Olá fornece uma segunda forma de autenticação.

aplicação do Microsoft Authenticator Olá substitui Olá do Azure Authenticator. Olá do Azure Authenticator ainda funciona, mas se decidir toomove toohello Microsoft Authenticator nova aplicação, este artigo pode ajudá-lo.  

## <a name="opt-in-for-two-step-verification"></a>Optar por verificação de dois passos

aplicação do Microsoft Authenticator Olá não funciona por si só. Configure cada um dos seus tooprompt de contas para um segundo método de verificação depois de iniciar sessão com o nome de utilizador e palavra-passe. 

Para uma conta escolar ou profissional, não normalmente obtiver toochoose esta funcionalidade para si próprio. Em vez disso, um administrador de segurança de optar por participar ativamente em seu nome e, em seguida, notifica-o tooregister métodos de verificação para a sua conta. Se este cenário aplica-se tooyou, saiba mais em [que Azure multi-factor Authentication significa para me permitir](multi-factor-authentication-end-user.md).

Para uma conta pessoal, terá de tooset se a verificação de dois passos para si próprio. Se tiver uma conta Microsoft, estão disponíveis nesses passos [sobre a verificação de dois passos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification). 

Também pode utilizar Olá Microsoft Authenticator com contas de terceiros. Pode chamar funcionalidade Olá de algo diferente de verificação em dois passos, mas deve ser capaz de toofind-lo com as definições de segurança ou início de sessão. 

## <a name="install-hello-app"></a>Instalar aplicação Olá
aplicação do Microsoft Authenticator Olá está disponível para [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="add-accounts-toohello-app"></a>Adicionar contas toohello aplicação
Para cada conta que pretende que a aplicação de Microsoft Authenticator tooadd toohello, utilize um dos Olá os seguintes procedimentos:

### <a name="add-a-personal-microsoft-account-toohello-app"></a>Adicionar uma aplicação toohello da conta Microsoft pessoal

Para uma conta Microsoft pessoal (um que utilize toosign no tooOutlook.com, Xbox, Skype, etc.), tudo tiver toodo é inicie sessão na conta tooyour na aplicação do Microsoft Authenticator Olá.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>Adicionar um trabalho ou escola utilizando scanner de código Olá QR toohello aplicação da conta
1. Visite o ecrã de definições de verificação de segurança toohello.  Para obter informações sobre como tooget toothis ecrã, consulte [alterar as definições de segurança](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).
2. Olá caixa de verificação-demasiado junto**aplicação de autenticação** , em seguida, selecione **configurar**.

    ![botão de configurar Olá no ecrã de definições de verificação de segurança de Olá](./media/authenticator-app-how-to/azureauthe.png)

    Isto apresenta um ecrã com um código QR no mesmo.

    ![Ecrã fornece código Olá QR](./media/authenticator-app-how-to/barcode2.png)
3. Aplicação do Microsoft Authenticator Olá aberta. No Olá **contas** ecrã, selecione  **+** e, em seguida, especifique que pretende que o tooadd uma conta escolar ou profissional.
4. Utilizar Olá câmara tooscan Olá QR código e, em seguida, selecione **feito** ecrã de código tooclose Olá QR.

    Se a câmara não está a funcionar corretamente, pode [introduzir manualmente o código de Olá QR e o URL](#add-an-account-to-the-app-manually).

5. Quando a aplicação Olá mostra o nome da sua conta com um código de seis dígitos por baixo, terminar. 

    ![Ecrã de contas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>Adicionar uma aplicação da conta toohello manualmente
1. Visite o ecrã de definições de verificação de segurança toohello.  Para obter informações sobre como tooget toothis ecrã, consulte [alterar as definições de segurança](multi-factor-authentication-end-user-manage-settings.md).
2. Selecione **configurar**.

    ![botão de configurar Olá no ecrã de definições de verificação de segurança de Olá](./media/authenticator-app-how-to/azureauthe.png)

    Isto apresenta um ecrã com um código QR no mesmo.  Tenha em atenção Olá código e o URL.

    ![Ecrã fornece código Olá QR e o URL](./media/authenticator-app-how-to/barcode2.png)
3. Aplicação do Microsoft Authenticator Olá aberta. No Olá **contas** ecrã, selecione  **+** e, em seguida, especifique que pretende que o tooadd uma conta escolar ou profissional.

4. Em detetor de Olá, selecione **introduzir manualmente o código**.

    ![Ecrã de análise de um código QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Introduza o código de Olá e o URL de Olá nas caixas adequadas do Olá na aplicação Olá, em seguida, selecione **concluir**.

    ![Ecrã para introduzir o código e o URL](./media/authenticator-app-how-to/manual.png)

6. Quando a aplicação Olá mostra o nome da sua conta com um código de seis dígitos por baixo, terminar.

    ![Ecrã de contas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Adicionar uma aplicação da conta toohello utilizar o Touch ID
aplicação do Microsoft Authenticator Olá no iOS suporta Touch ID.  Multi-factor Authentication do Azure permite que as organizações toorequire um PIN para dispositivos. Com o Touch ID, utilizadores do iOS não precisam de tooenter um PIN. Em vez disso, pode analisar a respetiva impressão digital e selecione **aprovar**.

Configurar o Touch ID com o Microsoft Authenticator é simple. Conclua um desafio de verificação normal com um PIN. Se o dispositivo suporta Touch ID, Microsoft Authenticator define-automaticamente para essa conta.

![Verificação da configuração de Touch ID](./media/authenticator-app-how-to/touchid1.png)

A partir do que ponto reencaminhar, quando estiver necessário tooverify o início de sessão, selecione a notificação push de Olá recebido e analisar a sua impressão digital em vez de introduzir o PIN.

![Notificação Push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>Utilizar a aplicação Olá quando iniciar sessão

Assim que a conta é adicionada toohello aplicação, poderá ser pedido toodo um toomake de verificação de teste se de que tudo foi corretamente configurado. Depois disso, está concluído! Não precisa de toodo há mais alguma coisa até hello próxima vez que iniciar sessão.

Se tiver escolhido toouse códigos de verificação na aplicação Olá, iniciar toosee-las na Olá home page. Se alterar a cada 30 segundos para que tenham sempre um novo código quando precisa de uma. Mas não precisa de toodo nada com as mesmas até a iniciar sessão e são tooenter pedido um código de verificação.  
