---
title: "aaaAzure MFA inicie sessão com a verificação de dois passos | Microsoft Docs"
description: "Esta página será fornecem orientações sobre onde toogo toosee Olá vários início de sessão métodos disponíveis com a MFA do Azure."
keywords: "autenticação de utilizador, o início de sessão experiência, início de sessão com o telemóvel, início de sessão com o telefone do escritório"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>Olá início de sessão experiência com multi-factor Authentication do Azure
> [!NOTE]
> objetivo Olá este artigo é toowalk através de uma experiência de início de sessão normal. Para obter ajuda com início de sessão, ou tootroubleshoot problemas, consulte [problemas com o Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).

## <a name="what-will-your-sign-in-experience-be"></a>O que será a experiência de início de sessão?
A experiência de início de sessão é diferente consoante aquilo que escolher toouse como o segundo fator: uma chamada telefónica, uma aplicação de autenticação ou textos. Escolha a opção de Olá que melhor descreve o que fazer:

| Como pode iniciar sessão? | 
| --- |
| [Com um telefone de escritório ou mobile da toomy de chamada telefónica](#signing-in-with-a-phone-call) |
| [Com um telemóvel de toomy de texto](#signing-in-with-a-text-message)
| [Notificações da aplicação do Microsoft Authenticator Olá](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [Com códigos de verificação da aplicação do Microsoft Authenticator Olá](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [Com um método alternativo, porque o meu método preferido não é possível utilizar neste momento](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>Iniciar sessão com uma chamada telefónica
Olá informações a seguir descreve a experiência de verificação de dois passos Olá com chamada tooyour móveis ou de telefone do escritório.

1. Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe.  
2. Microsoft chama a.  
3. Responder phone Olá e prima a tecla de # Olá.  

## <a name="signing-in-with-a-text-message"></a>Iniciar sessão com uma mensagem de texto
Olá informações a seguir descreve a experiência de verificação de dois passos Olá com um texto mensagem tooyour telemóvel:

1. Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe. 
2. Microsoft envia uma mensagem de texto que contém um código de número. 
3. Introduza o código de Olá na caixa de Olá fornecida na página de início de sessão Olá. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Iniciar sessão com a aplicação do Microsoft Authenticator Olá 
Olá seguintes informações descrevem Olá experiência de utilização da aplicação do Microsoft Authenticator Olá para verificações de validação em dois passos. Existem duas formas diferentes o toouse Olá aplicação. Pode receber notificações push no seu dispositivo ou pode abrir Olá aplicação tooget um código de verificação.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>toosign com uma notificação da aplicação do Microsoft Authenticator Olá
1. Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe.
2. Microsoft envia uma aplicação de Microsoft Authenticator toohello notificação no seu dispositivo.

  ![Microsoft envia a notificação](./media/multi-factor-authentication-end-user-signin/notify.png)

3. Notificação de Olá aberto no seu telemóvel e selecione Olá **verifique** chave. Se a sua empresa necessita de um PIN, introduza-o aqui.
4. Agora que deve ser iniciou sessão.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>toosign utilizando um código de verificação com a aplicação do Microsoft Authenticator Olá

Se utilizar códigos de verificação de tooget de aplicações Microsoft Authenticator Olá, em seguida, quando abre a aplicação Olá verá um número em nome da sua conta. Este número altera a cada 30 segundos para que não utilize Olá igual número duas vezes. Quando estiver a pedido para um código de verificação, abra a aplicação Olá e utilizar qualquer número atualmente é apresentado. 

1. Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe.
2. Microsoft pede-lhe um código de verificação.

  ![Introduza o código de verificação](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. Abra a aplicação do Microsoft Authenticator Olá no seu telemóvel e introduza o código de Olá na caixa de olá onde está a iniciar sessão.

## <a name="signing-in-with-an-alternate-method"></a>Iniciar sessão com um método alternativo
Por vezes, não tem o telefone Olá ou dispositivos que configurou como método de verificação preferida. Esta situação é a razão pela qual recomendamos que configure métodos de cópia de segurança para a sua conta. Olá secção seguinte mostra como toosign com um método alternativo quando o método principal pode não estar disponível.

1. Inicie sessão no tooan aplicação ou serviço como o Office 365, utilizando o seu nome de utilizador e palavra-passe.
2. Selecione **utilizar outra opção de verificação**. Consulte as opções de verificação diferente com base no número que configurou.
3. Escolha um método alternativo e iniciar sessão.

  ![Utilize o método alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>Passos seguintes

Se tiver problemas em iniciar sessão com a verificação de dois passos, obter mais informações em [problemas com o Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).

Saiba como demasiado[gerir as definições da verificação de dois passos](multi-factor-authentication-end-user-manage-settings.md).

Saiba como demasiado[introdução à aplicação do Microsoft Authenticator Olá](microsoft-authenticator-app-how-to.md) para que possa utilizar notificações toosign, em vez de textos e chamadas telefónicas. 
