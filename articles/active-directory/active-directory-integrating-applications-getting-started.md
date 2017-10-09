---
title: "aaaGet iniciar a integração do Azure AD com aplicações | Microsoft Docs"
description: "Este artigo é um guia de introdução para integrar o Azure Active Directory (AD) com aplicações no local e aplicações em nuvem."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>Guia de introdução de integrar o Azure Active Directory com aplicações de introdução
## <a name="overview"></a>Descrição geral
Este tópico é toogive que se destinam a um plano para integrar aplicações com o Azure Active Directory (AD). Cada uma das secções Olá abaixo contém um breve resumo de um tópico mais detalhado para que possa identificar as partes deste guia de introdução são tooyou relevante.  Siga as ligações de Olá para uma descrição mais aprofundada sobre cada assunto.

## <a name="before-you-begin-take-inventory"></a>Antes de começar, fazer o inventário
Antes de avançar toointegrating aplicações com o Azure AD, é importante tooknow onde é e em que pretende toogo.  Olá questões que se seguem são toohelp pretendido tem em consideração o projeto de integração de aplicações do Azure AD.

### <a name="application-inventory"></a>Inventário de aplicações
* Onde estão todas as aplicações? Quem é o proprietário-las?
* Que tipo de autenticação precisam as suas aplicações?
* Quem tem acesso toowhich aplicações?
* Pretende toodeploy uma nova aplicação?
  * Irá criar internas e implementá-la numa instância de computação do Azure?
  * Irá utilizar uma que esteja disponível no Olá Galeria de aplicações do Azure?

### <a name="user-and-group-inventory"></a>Inventário de utilizador e grupo
* Onde residir as contas de utilizador?
  * Active Directory no local
  * Azure AD
  * Dentro de uma base de dados de aplicação separado que é proprietário
  * Nas aplicações não aprovadas
  * Todos os Olá acima
* As atribuições de funções e permissões a utilizadores individuais atualmente dispõe? Precisa de tooreview o acesso ou tem a certeza de que as atribuições de acesso e a função de utilizador são adequadas agora?
* São grupos já existentes no Active Directory no local?
  * Como os seus grupos estão organizados?
  * Quem são membros do grupo Olá?
  * As atribuições de permissões/função alguns grupos Olá atualmente têm?
* Vai precisar tooclean segurança de bases de dados de utilizador/grupo antes da integração?  (Esta é uma pergunta pretty importante. Libertação da memória no lixo out.)

### <a name="access-management-inventory"></a>Inventário de gestão de acesso
* Como atualmente gerir tooapplications de acesso do utilizador? A que precisa de toochange?  Ter é considerado outras formas toomanage acesso, tal como com [RBAC](role-based-access-control-configure.md) por exemplo?
* Quem tem acesso toowhat?

Talvez não tiver tooall de respostas hello destas perguntas adiantado mas que okay.  Este guia possa ajudá-lo a responder a algumas dessas perguntas e tomar algumas decisões informadas.

## <a name="prerequisites"></a>Pré-requisitos
* Uma subscrição do Azure e um diretório do Azure Active Directory.  Se ainda não tiver uma subscrição do Azure, pode experimentar o Azure gratuitamente durante 30 dias. [Experimente!](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Integração de aplicações com o Azure AD
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>Localizar não sancionadas aplicações em nuvem com o Cloud App Discovery
Tal como mencionado acima, poderão existir aplicações que ainda não foram geridas pela sua organização até agora.  Como parte do processo de inventário de Olá, é possível toofind não sancionada aplicações de nuvem. Consulte [localizar aplicações na nuvem não sancionadas com o Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

### <a name="authentication-types"></a>Tipos de autenticação
Cada uma das suas aplicações pode ter requisitos de autenticação diferente. Com o Azure AD, podem ser utilizados certificados de assinatura com as aplicações que utilizam SAML 2.0, WS-Federation, ou OpenID Connect protocolos, bem como palavra-passe de início de sessão único. Para obter mais informações sobre a aplicação veja os tipos de autenticação para utilização com o Azure AD [gestão de certificados para federado Single Sign-On no Azure Active Directory](active-directory-sso-certs.md) e [palavra-passe de início de sessão único com base no](active-directory-appssoaccess-whatis.md).

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Ativar a SSO com o Proxy de aplicações do Azure AD
Com o Proxy de aplicações do Microsoft Azure AD, pode fornecer tooapplications acesso localizado no interior da rede privada em segurança, em qualquer lugar e em qualquer dispositivo. Depois de instalar um conector do proxy da aplicação no seu ambiente, pode ser configurado de facilmente com o Azure AD.

### <a name="integrating-applications-with-azure-ad"></a>Integrar aplicações com o Azure AD
Olá seguintes artigos abordam formas diferentes de Olá aplicações integram com o Azure AD e fornecem algumas orientações.

* [Determinar qual toouse do Active Directory](active-directory-administer.md)
* [Utilizar as aplicações na Galeria de aplicações do Azure de Olá](active-directory-appssoaccess-whatis.md)
* [Integrar a lista de tutoriais de aplicações SaaS](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>Gerir o acesso tooapplications
Olá artigos que se seguem descrevem formas pode gerir o acesso tooapplications depois de ter sido integrados com o Azure AD através do Azure AD conectores e o Azure AD.

* [Gestão de acesso tooapps, utilizar o Azure AD](active-directory-managing-access-to-apps.md)
* [Automatizar com conectores do Azure AD](active-directory-saas-app-provisioning.md)
* [Atribuir utilizadores tooan aplicação](active-directory-applications-guiding-developers-assigning-users.md)
* [Atribuição de grupos de aplicações de tooan](active-directory-applications-guiding-developers-assigning-groups.md)
* [Partilha de contas](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>Integrar aplicações personalizadas
Se estiver a escrever uma nova aplicação e pretende que os programadores de tooassist no tirar partido da energia Olá do Azure AD, consulte [Guiding programadores](active-directory-applications-guiding-developers-for-lob-applications.md).

Se pretender tooadd toohello sua aplicação personalizada Galeria de aplicações do Azure, veja ["Traga a sua própria aplicação" com a configuração SAML do Self-Service do Azure AD](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

## <a name="see-also"></a>Consultar também
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)

