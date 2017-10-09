---
title: "verificação de dois passos aaaTroubleshoot | Microsoft Docs"
description: "Este documento irá fornecer informações aos utilizadores nos qual toodo se executam para um problema com o Azure multi-factor Authentication."
services: multi-factor-authentication
keywords: "cliente de autenticação multifator, problema de autenticação, ID de correlação"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: end-user
ms.openlocfilehash: f5c980d104de684b052c0f7a13394f00e9828abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-help-with-two-step-verification"></a>Obter ajuda com verificação de dois passos
Este artigo responde a perguntas mais comuns de Olá que pessoas colocar sobre verificação de dois passos. 

## <a name="why-do-i-have-tooperform-two-step-verification-can-i-turn-it-off"></a>Por que motivo tenho de verificação de dois passos tooperform? Pode posso desativá-la?

Verificação de dois passos é uma funcionalidade de segurança que sua organização escolheu toouse tooprotect as suas contas. É mais segura do que apenas uma palavra-passe, porque depende de duas formas de autenticação: algo conhece e algo tem consigo. Olá algo que saiba é a palavra-passe. Olá algo com é um telefone ou dispositivo que normalmente tem consigo. Quando a sua conta está protegida com verificação de dois passos, que significa que um hacker malicioso não é possível iniciar sessão como se a palavra-passe preso de algum modo porque não têm telefone de tooyour de acesso, demasiado. 

A Microsoft disponibiliza a verificação de dois passos, mas a sua organização escolhe a funcionalidade de Olá toouse. Não é possível ativamente se o seu departamento de TI requê-lo de que, tal como o não é possível ativamente por não utilizar uma palavra-passe tooprotect sua conta. 

Se tiver ativada para a sua conta Microsoft pessoal de verificação de dois passos e quiser toochange as suas definições, leia [sobre a verificação de dois passos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) em vez disso. 

## <a name="i-dont-have-my-phone-with-me-today"></a>Não tenho meu telefone com-me hoje

Alguns dias a manter o telemóvel em casa, mas ainda tem toosign no trabalho. Olá primeira coisa que deve tentar é iniciar sessão com um método de verificação diferente. Quando se registou para verificação de dois passos, configurar mais do que um número de telefone? tootry iniciar sessão com um método diferente, siga estes passos:

1. Inicie sessão como faria normalmente.
2. Quando abre a página de verificação de dois passos Olá, escolha **utilizar outra opção de verificação**.

   ![Verificação diferente](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. Selecione a opção de verificação de Olá pretende toouse.
4. Continue com a verificação de dois passos.

Se não vir Olá **utilizar outra opção de verificação** ligar, em seguida, o que significa que não foi configurado a métodos alternativos quando se registou primeiro para a verificação de dois passos. Contacte a ajuda do IT departamento tooget tooyour conta de início de sessão. Assim que tem sessão iniciada, certifique-se demasiado[gerir as suas definições](multi-factor-authentication-end-user-manage-settings.md) tooadd métodos de verificação adicional para a próxima vez. 

Se vir Olá **utilizar outra opção de verificação** ligação, mas não tem métodos alternativos de tooyour de acesso a, contacte sua IT departamento tooget ajudá-lo a iniciar sessão tooyour conta. 

## <a name="i-lost-my-phone-or-got-a-new-number"></a>Posso perder o meu telefone ou recebeu um novo número de erro
Existem duas formas tooget novamente tooyour conta. Olá é primeiro toosign utilizando o número de telefone de autenticação alternativo, se configurou um. Olá segundo é tooask sua tooclear do departamento de IT as suas definições.

Se o seu telefone foi perdido ou roubado, recomendamos também que informe o seu departamento de TI, de modo a poderem repor as palavras-passe de aplicação e desmarque qualquer memorizadas dispositivos. 

### <a name="use-an-alternate-phone-number"></a>Utilizar um número de telefone alternativo
Se configurou várias opções de verificação, incluindo um número de telefone secundário ou uma aplicação de autenticação num dispositivo diferente, pode utilizar um deles toosign no.

toosign utilizando o número de telefone alternativo Olá, siga estes passos:

1. Inicie sessão como faria normalmente.
2. Quando o pedido toofurther verificar a sua conta, escolha **utilizar outra opção de verificação**.
   
   ![Verificação diferente](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. Selecione o número de telefone Olá ou dispositivo que tem acesso a.
4. Depois de estiver novamente na sua conta, [gerir as suas definições](multi-factor-authentication-end-user-manage-settings.md) toochange número de telefone a autenticação.

### <a name="clear-your-settings"></a>Limpar as definições
Se não tiver configurado um número de telefone de autenticação secundária, terá toocontact o departamento de TI para obter ajuda. Tem-los limpar as definições, por isso, Olá junto tempo iniciar sessão, será solicitado demasiado[registar para a verificação de dois passos](multi-factor-authentication-end-user-first-time.md) novamente.

## <a name="i-am-not-receiving-a-text-or-call-on-my-phone"></a>Posso não estou a receber um texto ou chamada no meu telefone
Existem vários motivos por que razão poderá tente toosign no, mas não receber Olá texto ou de chamada telefónica. Se tiver recebeu com êxito textos ou chamadas telefónicas tooyour telefone no Olá anterior, em seguida, este é provavelmente um problema com o fornecedor de telefone Olá, não a sua conta. Certifique-se de que possui sinal de célula boa e, se estiver a tentar tooreceive uma mensagem de texto certifique-se de que são toorecieve capaz de mensagens de texto. Peça um friend toocall texto ou utilizador, como um teste. 

Se tiver aguardaram alguns minutos até um texto ou chamada, Olá tooget de forma mais rápida à sua conta é tootry uma opção diferente.

1. Selecione **utilizar outra opção de verificação** na página Olá que está a aguardar a verificação.
   
    ![Verificação diferente](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)
2. Selecione Olá phone número ou entrega método pretende toouse.
   
    Se recebeu vários códigos de verificação, utilize Olá uma mais recente.

Se não tiver outro método configurado, contacte o departamento de TI e peça-lhes tooclear as suas definições. Olá vez seguinte que iniciar sessão, será solicitado demasiado[configurar a autenticação multifator](multi-factor-authentication-end-user-first-time.md) novamente.

Se tiver, muitas vezes, os atrasos devido sinal de célula toobad, recomendamos que utilize Olá [aplicação Microsoft Authenticator](microsoft-authenticator-app-how-to.md) no smartphone. aplicação Olá pode gerar códigos de segurança aleatório que utilizar toosign no e estes códigos não requerem qualquer ligação de sinal ou de internet de célula.

## <a name="app-passwords-are-not-working"></a>As palavras-passe de aplicação não estão a funcionar
Em primeiro lugar, certifique-se de que introduziu palavra-passe de aplicação de Olá corretamente. palavra-passe de aplicação de Olá gerado substitui o normal palavra-passe, mas apenas aplicações de ambiente de trabalho mais antigas que não suportam a verificação em dois passos. Se esta ainda não está a funcionar, experimente iniciar sessão e [criar uma nova palavra-passe de aplicação](multi-factor-authentication-end-user-app-passwords.md).  Se ainda não funciona, contacte o seu departamento de TI e os [eliminar as palavras-passe de aplicação existentes](../multi-factor-authentication-manage-users-and-devices.md) e, em seguida, pode criar um novo.

## <a name="i-didnt-find-an-answer-toomy-problem"></a>Posso não foi encontrado um problema de toomy de resposta.
Se tiver já tentou estes passos de resolução de problemas, mas é continuam a executar para problemas, contacte o seu departamento de TI. Devem ser capaz de tooassist.

## <a name="related-topics"></a>Tópicos relacionados
* [Gerir as definições de verificação em dois passos](multi-factor-authentication-end-user-manage-settings.md)  
* [FAQ acerca da aplicação Microsoft Authenticator](microsoft-authenticator-app-faq.md)

