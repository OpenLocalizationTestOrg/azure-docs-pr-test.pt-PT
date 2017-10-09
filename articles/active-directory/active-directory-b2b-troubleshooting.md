---
title: "aaaTroubleshooting colaboração B2B do Azure Active Directory do | Microsoft Docs"
description: "Responsabilidade para problemas comuns com a colaboração B2B do Azure Active Directory do"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Resolução de problemas de colaboração B2B do Azure Active Directory do

Seguem-se algumas responsabilidade para problemas comuns com a colaboração B2B do Azure Active Directory (Azure AD).


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>Posso adicionar um utilizador externo, mas não vê-los no meu livro de endereços Global ou no selecionador de pessoas Olá

Em casos onde os utilizadores externos não são preenchidos na lista de Olá, objeto Olá poderá demorar alguns minutos tooreplicate.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>Um utilizador de convidado B2B não está visível no seleccionador do SharePoint Online/OneDrive pessoas 
 
Olá toosearch de capacidade dos utilizadores convidados existente no selecionador de pessoas do SharePoint Online (SPO) Olá está OFF ao comportamento de legado de toomatch predefinido.

Pode ativar esta funcionalidade utilizando Olá definição 'ShowPeoplePickerSuggestionsForGuestUsers' na coleção de Olá inquilino e o site de nível. Pode definir a funcionalidade de Olá utilizando Olá SPOTenant conjunto e SPOSite do conjunto de cmdlets que permite que os membros toosearch todos os utilizadores convidados existentes no diretório de Olá. As alterações no âmbito de inquilino Olá não afetam os sites SPO já aprovisionadas.

## <a name="invitations-have-been-disabled-for-directory"></a>Foram desativadas convites para o diretório

Se for notificado de que não tiver permissões tooinvite utilizadores, certifique-se de que a sua conta de utilizador é autorizado tooinvite utilizadores externos em definições de utilizador:

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

Se tiver modificado estas definições ou Olá convidado Inviter função tooa utilizador atribuído recentemente, poderão existir um atraso de 15-60 minutos antes de Olá alterações entram em vigor.

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>utilizador Olá que posso convidado está a receber um erro durante a resgate

Erros comuns incluem:

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>Administrador do invitee não permitiu a EmailVerified utilizadores de que está a ser criada no seu inquilino

Quando inviting utilizadores cuja organização está a utilizar o Azure Active Directory, mas olá onde a conta de utilizador específica não existe (por exemplo, Olá utilizador não existe no Azure AD contoso.com). administrador de Olá de contoso.com pode ter uma política no local a impedir que os utilizadores a ser criada. utilizador Olá tem de verificar com os respetivos toodetermine admin se são permitidos a utilizadores externos. Olá admin externo utilizador poderá ter tooallow verificar E-mail aos utilizadores no respetivo domínio (consulte este [artigo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) em permitir aos utilizadores verificar de E-Mail).

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>Utilizador externo não existe já num domínio federado

Se estiver a utilizar a autenticação de Federação e o utilizador Olá ainda não existir no Azure Active Directory, o utilizador Olá não pode ser convidado.

tooresolve este problema, hello admin de utilizador externo tem de sincronizar tooAzure de conta de utilizador Olá do Active Directory.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>Como dos does\#', que não é normalmente um caráter válido, a sincronização com o Azure AD?

"\#" é um caráter reservado UPNs para colaboração B2B do Azure AD ou utilizadores externos, porque a conta de convidado de Olá user@contoso.com fica user_contoso.com#EXT@fabrikam.onmicrosoft.com. Por conseguinte, \# UPNs feitos no local não são permitidas toosign no toohello portal do Azure. 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>Recebo um erro ao adicionar utilizadores externos tooa sincronizados grupo

Os utilizadores externos podem ser adicionados apenas demasiado "atribuído" ou grupos de "Segurança" e não toogroups são controlado no local.

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>Os meus utilizadores externos não recebeu um e-mail tooredeem

invitee Olá deve verificar junto do seu ISP ou é permitido tooensure de filtro de spam Olá seguinte endereço:Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>Reparar que essa mensagem personalizada de saudação não obter incluída com mensagens convite por vezes

toocomply com as leis de privacidade, os APIs não incluir mensagens personalizadas no convite de correio eletrónico Olá quando:

- inviter Olá não tiver um endereço de e-mail no Olá inviting inquilino
- Quando um principal de serviço aplicacional envia convite Olá

Se este cenário é importante tooyou, pode suprimir os nosso e-mail de convite de API e enviá-lo através do mecanismo de correio eletrónico Olá à sua escolha. Consulte toomake counsel legais da sua organização se qualquer e-mail que enviar desta forma também estas estejam em conformidade com as leis de privacidade.

## <a name="next-steps"></a>Passos seguintes

Consulte os nossos outros artigos sobre a colaboração B2B do Azure AD:

* [O que é a colaboração B2B do Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como é que os administradores de Azure Active Directory adicionar utilizadores de colaboração do B2B?](active-directory-b2b-admin-add-users.md)
* [Como é que os infotrabalhadores adicionar utilizadores de colaboração do B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de Olá de Olá e-mail de convite de colaboração B2B](active-directory-b2b-invitation-email.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento e colaboração do Azure AD B2B](active-directory-b2b-licensing.md)
* [Colaboração do Azure Active Directory B2B perguntas mais frequentes (FAQ)](active-directory-b2b-faq.md)
* [Colaboração B2B do Active Directory Azure API e personalização](active-directory-b2b-api.md)
* [Autenticação multifator para os utilizadores da colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar utilizadores de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)
