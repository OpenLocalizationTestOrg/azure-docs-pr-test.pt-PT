---
title: "aaaHow toouse palavras-passe de aplicação no Azure MFA? | Microsoft Docs"
description: "Esta página irá ajudar os utilizadores a compreenderem quais são as palavras-passe de aplicação e o que são utilizados para com regard tooAzure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>Quais são palavras-passe de aplicação no Azure multi-factor Authentication?
Determinadas aplicações não baseadas no browser, como o cliente de e-mail nativa de Apple Olá que utiliza o Exchange Active Sync, atualmente não suportam autenticação multifator. Autenticação multifator é ativada por utilizador.  Isto significa que um utilizador não é possível utilizar a autenticação multifator se:

- utilizador Olá foi ativada para autenticação multifator
- utilizador Olá está a tentar toouse uma aplicação não baseadas no browser.

Uma palavra-passe de aplicação permite Olá utilizador toouse Olá aplicação.

Assim que tiver uma palavra-passe de aplicação, utilize-o em vez da palavra-passe original com estas aplicações não baseadas no browser. Ao registar para a verificação de dois passos, está a informar Microsoft não toolet qualquer pessoa iniciar sessão com a sua palavra-passe se estes também não é possível efetuar a verificação de segundo Olá. cliente de e-mail nativo Olá Apple no seu telemóvel não pode iniciar sessão como porque não é possível pedir a verificação. Olá solução toothis problema é toocreate uma mais segura palavra-passe de aplicação não utilizar diárias. As palavras-passe de aplicação são apenas para essas aplicações que não suportem a verificação de dois passos. Utilize Olá palavra-passe para que as aplicações podem ignorar multi-factor authentication e continuar toowork.


> [!NOTE]
> Clientes do Office 2013 (incluindo o Outlook) suportam o novo protocolos de autenticação e pode ser utilizado com verificação de dois passos. As palavras-passe de aplicação não são necessárias para utilização com clientes do Office 2013.  Para obter mais informações, consulte [Office 2013 autenticação moderna pré-visualização pública anunciada](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-toouse-app-passwords"></a>Como toouse palavras-passe de aplicação
Seguem-se algumas tooknow coisas sobre palavras-passe de aplicação:

* Não crie as suas próprias palavras-passe de aplicação. São geradas automaticamente.
* Atualmente não há um limite de 40 palavras-passe por utilizador. 
* Se tentar toocreate uma palavra-passe de aplicação após ter atingido o limite de Olá, terá de toodelete uma das suas palavras-passe de aplicação existentes antes de criar um novo.
* Utilize uma palavra-passe por dispositivo, não por aplicação. Por exemplo, pode criar uma palavra-passe de aplicação para o seu computador portátil e utilizar essa palavra-passe de aplicação para todas as aplicações desse portátil. Em seguida, crie uma segunda toouse de palavra-passe de aplicação para todas as suas aplicações no seu ambiente de trabalho. 
* É-lhe dada uma Olá de palavra-passe de aplicação pela primeira vez a que registar para a verificação de dois passos.  Se precisar de adicionais, pode criá-los.



## <a name="creating-and-deleting-app-passwords"></a>Criar e eliminar as palavras-passe de aplicação
Durante a sua inicial início de sessão, é-lhe dada uma palavra-passe de aplicação que pode utilizar.  Também pode criar e eliminar as palavras-passe de aplicação mais tarde. Como eliminar palavras-passe de aplicação depende de como utilizar a autenticação multifator. Olá resposta seguintes questões de toodetermine onde deve passar toomanage palavras-passe de aplicação: 

1. Utiliza a verificação da sua conta Microsoft pessoal? Se Sim, devem consultar toohello [palavras-passe de aplicação e a verificação de dois passos](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artigo para obter ajuda. Se não, continue tooquestion dois.

2. OK, pelo que utilizar a verificação de dois passos para a sua conta escolar ou profissional. A utilizar toosign tooOffice 365 aplicações? Se Sim, deve consultar demasiado[criar uma palavra-passe de aplicação para o Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) para obter ajuda. Se não, continue tooquestion três. 

3. Utiliza a verificação com o Microsoft Azure? Se Sim, continuar toohello [gerir palavras-passe de aplicação no portal do Azure de Olá](#manage-app-passwords-in-the-Azure-portal) secção deste artigo. Se não, continue tooquestion quatro.

4. Não tem a certeza, quando utiliza a verificação de dois passos? Continuar toohello [gerir palavras-passe de aplicação com o portal de MyApps Olá](#manage-app-passwords-with-the-myapps-portal) secção deste artigo. 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>Gerir palavras-passe de aplicação no Olá portal do Azure
Se utilizar a verificação com o Azure, quer palavras-passe de aplicação de toocreate através de Olá portal do Azure.

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>palavras-passe de aplicação de toocreate no Olá portal do Azure
1. Inicie sessão no toohello portal clássico do Azure.
2. Na parte superior do Olá, o nome de utilizador com o botão direito e selecione a verificação de segurança adicional.
3. Na página de proofup Olá, na parte superior do Olá, selecione as palavras-passe de aplicação
4. Clique em **Criar**.
5. Introduza um nome para a palavra-passe de aplicação de Olá e clique em **seguinte**
6. Copie a área de transferência do Olá aplicação palavra-passe toohello e cole-o sua aplicação.
   
   ![Nuvem](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>palavras-passe de aplicação de toodelete no Olá portal do Azure
1. Inicie sessão no toohello portal clássico do Azure.
2. Na parte superior do Olá, o nome de utilizador com o botão direito e selecione a verificação de segurança adicional.
3. Na parte superior de Olá, verificação de segurança tooadditional seguinte, selecione **palavras-passe de aplicação.**
4. Seguinte toohello palavra-passe que pretende toodelete, selecione **eliminar**.
5. Confirmar eliminação de Olá clicando **Sim**.
6. Assim que a palavra-passe de aplicação de Olá é eliminado, pode clicar em **fechar**.


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>Gerir palavras-passe de aplicação com o portal do Olá MyApps.
Se não tem a certeza de como utilizar a autenticação multifator, em seguida, pode sempre criar e eliminar palavras-passe de aplicação através do portal Olá myapps.

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>uma palavra-passe de aplicação através de toocreate Olá Myapps portal
1. A iniciar sessão demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Clique no seu nome no canto superior Olá direito e selecione **perfil**.
3. Selecione **verificação adicional de segurança**.
   ![Selecione verificação adicional de segurança - captura de ecrã](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selecione **palavras-passe de aplicação**.
   ![Selecione as palavras-passe de aplicação - captura de ecrã](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Clique em **Criar**.
6. Introduza um nome para a palavra-passe de aplicação de Olá e clique em **seguinte**.
7. Copie a área de transferência do Olá aplicação palavra-passe toohello e cole-o sua aplicação.
   ![Criar uma palavra-passe de aplicação](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>uma palavra-passe de aplicação através de toodelete Olá Myapps portal
1. A iniciar sessão demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Na parte superior do Olá, selecione o perfil.
3. Selecione **verificação adicional de segurança**.

   ![Selecione verificação adicional de segurança - captura de ecrã](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selecione **palavras-passe de aplicação**.

   ![Selecione as palavras-passe de aplicação - captura de ecrã](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Clique em seguinte toohello palavra-passe que pretende toodelete, **eliminar**.

   ![Eliminar uma palavra-passe de aplicação](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. Confirmar que pretende que toodelete essa palavra-passe clicando **Sim**.
7. Assim que a palavra-passe de aplicação de Olá é eliminado, pode clicar em **fechar**.

## <a name="next-steps"></a>Passos seguintes

- [Gerir as definições da verificação de dois passos](multi-factor-authentication-end-user-manage-settings.md)

- Experimentar Olá [aplicação Microsoft Authenticator](microsoft-authenticator-app-how-to.md) tooverify os inícios de sessão com as notificações de aplicação, em vez de textos ou chamadas a receber. 
