---
title: "aaaAzure colaboração B2B do Active Directory perguntas mais frequentes | Microsoft Docs"
description: "Obter toofrequently respostas perguntas mais sobre a colaboração B2B do Azure Active Directory do."
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
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Colaboração B2B do Active Directory Azure perguntas mais frequentes

Estas perguntas mais frequentes (FAQ) sobre a colaboração de empresa-empresa (B2B) do Azure Active Directory (Azure AD) são atualizados periodicamente tooinclude novos tópicos.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>Colaboração B2B do Azure AD está disponível no Olá portal clássico do Azure?
Não. Funcionalidades de colaboração do Azure AD B2B só estão disponíveis em Olá [portal do Azure](https://portal.azure.com) e no Olá [painel de acesso](https://myapps.microsoft.com/). 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>Iremos pode personalizar a nossa página de início de sessão para que seja mais intuitiva dos nossos utilizadores de convidados de colaboração B2B?
Absolutamente! Consulte a nossa [blogue sobre esta funcionalidade](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/). Para obter mais informações sobre como toocustomize da sua organização início de sessão página, consulte [adicionar imagem corporativa toosign no e páginas de painel de acesso da empresa](active-directory-add-company-branding.md).

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>Os utilizadores de colaboração do B2B podem aceder SharePoint Online e OneDrive?
Sim. No entanto, é Olá toosearch de capacidade dos utilizadores convidados existente no SharePoint Online utilizando o selecionador de pessoas Olá **desativar** por predefinição. Definir tooturn no Olá opção toosearch dos utilizadores convidados existente, **ShowPeoplePickerSuggestionsForGuestUsers** demasiado**no**. Pode ativar esta definição ao nível do inquilino Olá ou ao nível de coleção de sites Olá. Pode alterar esta definição utilizando Olá SPOTenant conjunto e SPOSite do conjunto de cmdlets. Com estes cmdlets, membros podem procurar todos os utilizadores convidados existentes no diretório de Olá. As alterações no âmbito de inquilino Olá não afetam os sites do SharePoint Online que já foram aprovisionados.

### <a name="is-hello-csv-upload-feature-still-supported"></a>É Olá CSV carregar funcionalidade ainda suportada?
Sim. Para obter mais informações sobre como utilizar a funcionalidade de carregamento de ficheiros. csv Olá, consulte [este exemplo do PowerShell](active-directory-b2b-code-samples.md).

### <a name="how-can-i-customize-my-invitation-emails"></a>Como personalizar o meu mensagens de e-mail de convite?
Pode personalizar quase tudo sobre o processo de inviter Olá utilizando Olá [B2B convite APIs](active-directory-b2b-api.md).

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>Um utilizador externo convidado pode deixar a organização Olá após a ser convidou?
administrador de organização convidando Olá pode eliminar um utilizador de convidado de colaboração B2B do respetivo diretório, mas o utilizador convidado de Olá não pode deixar Olá inviting diretório organização por si mesmos. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>Os utilizadores convidados podem repor o respetivo método de autenticação multifator?
Sim. Os utilizadores convidados podem repor as respetivas Olá de método de autenticação multifator que mesma forma que os utilizadores regulares fazer.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>Que organização é responsável por licenças de autenticação multifator?
organização convidando Olá efetua a autenticação multifator. Olá inviting organização tem de se certificar de que a organização Olá tem licenças suficientes para os respetivos utilizadores B2B que estão a utilizar a autenticação multifator.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>E se uma organização de parceiro já tem de configurar a autenticação multifator? Estamos a autenticação multifator de confiança e utiliza a nossa própria autenticação multifator?
Esta funcionalidade é planeada para uma versão futura, pelo que, em seguida, que pode selecionar tooexclude parceiros específicos de autenticação multifator de (Olá convidando da sua organização).

### <a name="how-can-i-use-delayed-invitations"></a>Como utilizar o convites atrasadas?
Uma organização poderá pretender que os utilizadores de colaboração B2B do tooadd, aprovisioná-los tooapplications conforme necessário e, em seguida, enviar convites para. Pode utilizar Olá B2B colaboração convite API toocustomize Olá integração fluxo de trabalho.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>Eu fizer um utilizador convidado um administrador limitado?
Com certeza. Para obter mais informações, consulte [ao adicionar a função de tooa de utilizadores convidados](active-directory-users-assign-role-azure-portal.md).

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Colaboração B2B do Azure AD permite B2B utilizadores tooaccess Olá portal do Azure?
A menos que um utilizador tem atribuído a função de Olá de administrador global ou limitado, os utilizadores de colaboração do B2B não necessitam de acesso toohello portal do Azure. No entanto, os utilizadores de colaboração do B2B que são atribuídos Olá função de administrador global ou limitado aceder Olá portal. Além disso, se um utilizador de convidados que não está atribuído uma dessas funções de administrador aceder ao portal de Olá, utilizador Olá poderá ser capaz de tooaccess algumas partes do Olá experiência. a função de utilizador convidado Olá tem algumas permissões no diretório de Olá.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>Pode bloquear acesso toohello portal do Azure para os utilizadores convidados?
Sim! Quando configurar esta política, ser tooavoid cuidado acidentalmente bloqueio acesso toomembers e administradores.
do tooblock um utilizador convidado acesso toohello [portal do Azure](https://portal.azure.com), utilizar uma política de acesso condicional no Olá API de modelo de implementação clássica do Windows Azure:
1. Modificar Olá **todos os utilizadores** para que contém apenas os membros de grupo.
  ![modificar a captura de ecrã do Olá grupo](media/active-directory-b2b-faq/modify-all-users-group.png)
2. Crie um grupo dinâmico que contenha os utilizadores convidados.
  ![Criar grupo captura de ecrã](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Configure um acesso condicional política tooblock os utilizadores convidados de aceder ao portal de Olá, conforme mostrado no seguinte Olá vídeo:
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>Colaboração B2B do Azure AD suporta autenticação multifator e contas de correio eletrónico de consumidor?
Sim. Contas de correio eletrónico de multi-factor authentication e de consumidor são suportadas para colaboração B2B do Azure AD.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>Planeia toosupport a palavra-passe repor para os utilizadores de colaboração B2B do Azure AD?
Sim. Seguem-se detalhes importantes do Olá para a reposição de palavra-passe self-service (SSPR) para um utilizador de B2B que está convidado a partir de uma organização de parceiro:
 
* SSPR ocorre apenas no inquilino de identidade de Olá de utilizador de B2B Olá.
* Se o inquilino de identidade Olá é uma conta Microsoft, Olá conta Microsoft mecanismo SSPR é utilizado.
* Se o inquilino de identidade Olá for um just-in-time (JIT) ou de inquilino "viral", é enviado um e-mail de reposição de palavra-passe.
* Para os outros inquilinos, o processo SSPR padrão Olá é seguido para utilizadores B2B. Como membro SSPR para os utilizadores de B2B, no contexto de Olá do recurso de Olá, inquilinos está bloqueado. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>É a palavra-passe reposto utilizadores convidados um just-in-time (JIT) ou "viral" inquilino que aceitaram convites com um trabalho ou endereço de e-mail profissional, mas que não tenham uma conta do Azure AD pré-existente?
Sim. Pode ser enviado um e-mail de reposição de palavra-passe que permite que um utilizador tooreset a palavra-passe na inquilinos JIT Olá.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Microsoft Dynamics CRM fornecem suporte online para colaboração B2B do Azure AD?
Atualmente, a Microsoft Dynamics CRM não fornece suporte online para colaboração B2B do Azure AD. No entanto, planeamos toosupport isto no Olá futura.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>O que é a duração de Olá de uma palavra-passe inicial para um utilizador recentemente criado de colaboração B2B?
Azure AD tem um conjunto fixo de caráter, força de palavra-passe e os requisitos de bloqueio de conta que se aplicam, igualmente, contas de utilizador de nuvem do tooall do Azure AD. Contas de utilizador de nuvem são contas que não federadas com o outro fornecedor de identidade, tais como 
* Conta Microsoft
* Facebook
* Serviços de Federação do Active Directory
* Outro inquilino de nuvem (para colaboração B2B)

Para contas federadas, política de palavra-passe depende da política de Olá que é aplicada nas definições de conta Microsoft Olá no local inquilinos e Olá do utilizador.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Uma organização poderá achar útil toohave diferentes ocorre nas respetivas aplicações para utilizadores de inquilino e os utilizadores convidados. Existe orientações padrão para isto? É presença Olá Olá identidade fornecedor afirmação Olá modelo correto toouse?
 Um utilizador convidado pode utilizar qualquer tooauthenticate do fornecedor de identidade. Para obter mais informações, consulte [propriedades de um utilizador de colaboração B2B](active-directory-b2b-user-properties.md). Olá utilize **UserType** experiência de utilizador de toodetermine de propriedade. Olá **UserType** afirmação não está atualmente incluída no token de Olá. As aplicações devem utilizar o diretório de Olá Olá Graph API tooquery para utilizador Olá e tooget Olá UserType.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>Onde posso encontrar um tooshare de Comunidade de colaboração B2B soluções e ideias toosubmit?
Estamos constantemente está a escutar tooyour comentários, tooimprove colaboração B2B. Convidamo-tooshare o utilizador cenários, as melhores práticas e o que gostou do colaboração B2B do Azure AD. Associar o debate Olá Olá [Microsoft técnico Comunidade](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).
 
Também Convidamo-toosubmit as suas ideias e votar para futuras funcionalidades em [ideias de colaboração do B2B](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>Podemos enviar um convite que é automaticamente resgatadas, pelo que Olá utilizador é apenas "pronto toogo"? Ou utilizador Olá always possui tooclick através do URL de resgate toohello?
Convites para que são enviadas por um utilizador no Olá inviting organização que também seja membro da organização do parceiro Olá não necessitam de resgate por utilizador do Olá B2B.

Recomendamos que convidar um utilizador de Olá toojoin Olá parceiro organização inviting organização. [Adicione esta função de inviter de convidado de toohello de utilizador na organização de recursos de Olá](active-directory-b2b-add-guest-to-role.md). Este utilizador pode convidar os outros utilizadores na organização do parceiro Olá utilizando Olá início de sessão IU, scripts do PowerShell ou APIs. Em seguida, utilizadores de colaboração B2B da organização não é necessária tooredeem os respetivos convites.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>Como funciona colaboração B2B quando parceiro Olá convidado está a utilizar Federação tooadd as seus próprios autenticação no local?
Se o parceiro de Olá tem um inquilino do Azure AD é federado toohello infraestrutura de autenticação no local, no local-início de sessão único (SSO) automaticamente é conseguido. Se o parceiro de Olá não tiver um inquilino do Azure AD, é criada uma conta do Azure AD para os novos utilizadores. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>Posso considerar o Azure AD B2B não aceitou gmail.com e outlook.com endereços de correio eletrónico e que B2C foi utilizado para esses tipos de contas?
Estamos a remover Olá diferenças B2B e colaboração (B2C) de empresa-empresa relativamente a quais identidades são suportadas. identidade Olá utilizada não é um toochoose bom motivo entre utilizando B2B ou B2C. Para obter informações sobre como escolher a opção de colaboração, consulte [colaboração B2B comparar e B2C no Azure Active Directory](active-directory-b2b-compare-b2c.md).

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>As aplicações e serviços suportam os utilizadores convidados de B2B do Azure?
Todas as aplicações do Azure integrada no AD suportam os utilizadores convidados de B2B do Azure. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>Iremos forçar multi-factor authentication para os utilizadores convidados de B2B se nossos parceiros de não tem a autenticação multifator?
Sim. Para obter mais informações, consulte [acesso condicional para os utilizadores de colaboração do B2B](active-directory-b2b-mfa-instructions.md).

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>No SharePoint, pode definir uma lista de "" ou "negadas" para os utilizadores externos. Vamos fazer isto no Azure?
Sim. Suporta a colaboração do Azure AD B2B apresenta uma lista de permissão e negação listas. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>O que fazem licenças precisamos toouse B2B do Azure AD?
Para obter informações sobre o que licenças a sua organização precisam de toouse B2B do Azure AD, consulte [colaboração do Azure Active Directory B2B licenciamento orientações](active-directory-b2b-licensing.md).

### <a name="next-steps"></a>Passos seguintes

Consulte os nossos outros artigos sobre a colaboração B2B do Azure AD:

* [O que é a colaboração B2B do Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como é que os administradores do Azure AD adicionar utilizadores de colaboração do B2B?](active-directory-b2b-admin-add-users.md)
* [Como é que os infotrabalhadores adicionar utilizadores de colaboração do B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de Olá de Olá e-mail de convite de colaboração B2B](active-directory-b2b-invitation-email.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento e colaboração do Azure AD B2B](active-directory-b2b-licensing.md)
* [Resolução de problemas de colaboração B2B do Azure AD](active-directory-b2b-troubleshooting.md)
* [Azure AD B2B colaboração API e personalização](active-directory-b2b-api.md)
* [Autenticação multifator para os utilizadores da colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar utilizadores de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de artigos da gestão de aplicações no Azure AD](active-directory-apps-index.md)
