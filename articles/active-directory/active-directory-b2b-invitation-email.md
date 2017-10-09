---
title: "elementos de aaaThe do e-mail de convite de colaboração Olá do Azure Active Directory B2B | Microsoft Docs"
description: "Modelo do e-mail de convite de colaboração do Azure Active Directory B2B"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>elementos de Olá de Olá e-mail de convite de colaboração B2B

Mensagens de e-mail de convite são parceiros de toobring um componente crítico em board como utilizadores de colaboração do B2B no Azure AD. Pode utilizá-los confiança do destinatário Olá tooincrease. Pode adicionar legitimidade e e-mail toohello prova sociais, destinatário de Olá se toomake semelhante confortável com a seleção de Olá **começar** botão convite de Olá tooaccept. Esta confiança é que uma chave significa tooreduce friction de partilha. E também pretende toomake Olá e-mail aspeto excelente!

![E-mail de convite do Azure AD B2b](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Explicar e-mail Olá
Vamos ver alguns elementos de e-mail Olá para saber como melhor toouse as respetivas capacidades.

### <a name="subject"></a>Assunto
Olá assunto do e-mail Olá segue Olá seguir o padrão: está convidado toohello &lt;tenantname&gt; organização

### <a name="from-address"></a>Endereço de
Utilizamos um padrão como o LinkedIn de Olá de endereço.  Deve ser claro que é inviter Olá e de que da empresa e também clarificar que e-mail Olá for proveniente de um endereço de e-mail do Microsoft. formato de Olá é: &lt;nome a apresentar do inviter&gt; de &lt;tenantname&gt; (através do Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Responda a
Olá resposta-tooemail está definido e-mail do toohello inviter se estiver disponível, para que a resposta toohello e-mail envia um inviter de back-toohello de correio eletrónico.

### <a name="branding"></a>Imagem corporativa
convite Olá e-mails a partir do seu inquilino utilizam Olá corporativa que pode configurar para o seu inquilino. Se quiser tootake partido desta capacidade, [aqui](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) Olá detalhes sobre como tooconfigure-lo. logótipo de faixa Olá aparece no e-mail de Olá. Siga o tamanho da imagem Olá e instruções de qualidade [aqui](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) para obter os melhores resultados. Além disso, o nome de empresa Olá também aparece no Olá chamada tooaction.

### <a name="call-tooaction"></a>Chamada tooaction
Olá chamada tooaction consiste em duas partes: explicar por que motivo o destinatário de Olá recebeu correio Olá e o destinatário de Olá está a ser pedido toodo acerca do mesmo.
- Olá "por que motivo" secção pode ser resolvida utilizando Olá seguir o padrão: tiver sido aplicações tooaccess convidados Olá &lt;tenantname&gt; organização

- E Olá "o está a ser pedido toodo" secção é indicada pelo presença Olá Olá **começar** botão. Quando foi adicionado destinatário Olá sem necessidade de Olá de convites, este botão não aparecer.

### <a name="inviters-information"></a>Informações do inviter
nome a apresentar do inviter Olá está incluído no e-mail de Olá. E, além disso, se tiver configurado a uma imagem de perfil para a sua conta do Azure AD, Olá inviting e-mail irá incluir essa imagem bem. Ambas é tooincrease pretendido confiança do destinatário no e-mail de Olá.

Se ainda não configurou a imagem do perfil, é apresentado um ícone com iniciais do inviter Olá em vez de imagem de Olá:

  ![Iniciais de apresentação inviter de Olá](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Corpo
corpo de Olá contém mensagem de saudação esse inviter Olá composes ou é transmitido através do convite Olá API. É uma área de texto, pelo que não processa tags de HTML por motivos de segurança.

### <a name="footer-section"></a>Secção de rodapé
rodapé Olá contém marca de empresa do Microsoft Olá e permite que o destinatário de Olá saber se o e-mail Olá foi enviada a partir de um alias de não monitorizado. Casos especiais:

- inviter Olá não tiver um endereço de e-mail no Olá inviting inquilinos

  ![imagem da inviter não tiver um endereço de e-mail no Olá inviting inquilinos](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- o destinatário de Olá não necessita de convite de Olá tooredeem

  ![Quando o destinatário não necessita tooredeem convite](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Passos seguintes

Consulte os nossos outros artigos sobre a colaboração B2B do Azure AD:

* [O que é a colaboração B2B do Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como é que os administradores de Azure Active Directory adicionar utilizadores de colaboração do B2B?](active-directory-b2b-admin-add-users.md)
* [Como é que os infotrabalhadores adicionar utilizadores de colaboração do B2B?](active-directory-b2b-iw-add-users.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento e colaboração do Azure AD B2B](active-directory-b2b-licensing.md)
* [Resolução de problemas de colaboração B2B do Azure Active Directory do](active-directory-b2b-troubleshooting.md)
* [Colaboração do Azure Active Directory B2B perguntas mais frequentes (FAQ)](active-directory-b2b-faq.md)
* [Colaboração B2B do Active Directory Azure API e personalização](active-directory-b2b-api.md)
* [Autenticação multifator para os utilizadores da colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar utilizadores de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)
