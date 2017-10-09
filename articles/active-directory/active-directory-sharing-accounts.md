---
title: contas de aaaSharing utilizar o Azure AD | Microsoft Docs
description: "Descreve como o Azure Active Directory permite às organizações toosecurely partilha contas aplicações no local e serviços de cloud de consumidor."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Partilha de contas com o Azure AD
## <a name="overview"></a>Descrição geral
Por vezes, as organizações precisam de toouse um único nome de utilizador e palavra-passe para várias pessoas. Esta situação ocorre normalmente em dois cenários:

* Ao aceder a aplicações que requerem um início de sessão único e uma palavra-passe para cada utilizador, se aplicações no local ou o consumidor serviços em nuvem (por exemplo, contas de redes sociais empresariais).
* Ao criar ambientes de vários utilizadores. Pode ter uma conta local, única que tem privilégios elevados e podem ser utilizado toodo core configuração, a administração e a recuperação atividades (por exemplo Olá "global" conta de administrador local para a conta de raiz do Office 365 ou Olá no Salesforce).

Tradicionalmente, estas contas teriam de ser partilhadas por distribuir indivíduos à direita do Olá credenciais (nome de utilizador/palavra-passe) toohello ou armazene-os numa localização partilhada onde vários fidedigna agentes podem aceder aos mesmos.

modelo de partilha tradicional Olá tem vários desvantagens:

* Ativar acesso toonew aplicações requer toodistribute credenciais tooeveryone que necessita de acesso.
* Cada aplicação partilhada pode exigir que o seu próprio conjunto exclusivo de credenciais partilhadas, a necessidade dos utilizadores tooremember vários conjuntos de credenciais. Quando os utilizadores têm tooremember várias credenciais, o risco Olá aumenta a que estes irão recorrer toorisky práticas. (por exemplo, escrever para baixo de palavras-passe).
* Não é possível saber quem tem acesso tooan aplicação.
* Não é possível saber quem tem *acedidos* uma aplicação.
* Quando precisar de aplicação de tooan tooremove acesso, ter tooupdate Olá credenciais e distribuir novamente tooeveryone que precisa de aceder à aplicação de toothat.

## <a name="azure-active-directory-account-sharing"></a>Partilha e conta do Azure Active Directory
O Azure AD fornece uma nova abordagem contas toousing partilhado que elimina estes desvantagens.

administrador do Azure AD de Olá configura as aplicações que um utilizador pode aceder através do painel de acesso de Olá e escolher tipo de Olá de início de sessão mais adequada para essa aplicação. Um desses tipos *baseada em palavra-passe de início de sessão único*, permite ao Azure AD atuar como um tipo de "Mediador" durante o início de sessão no processo Olá para essa aplicação.

Os utilizadores iniciar sessão uma vez com a respetiva conta profissional. Este é Olá mesma conta que utilizam regularmente tooaccess respetivo ambiente de trabalho ou e-mail. Podem detetar e aceder apenas as aplicações que estão atribuídos. Com as contas partilhadas, esta lista de aplicações pode incluir qualquer número de credenciais partilhadas. utilizador final de Olá não precisa de tooremember ou anote Olá várias contas que podem estar a utilizar.

Contas partilhadas não só aumentam supervisão e melhoram a facilidade de utilização, também melhoram a segurança. Os utilizadores com permissões toouse Olá credenciais não veem a palavra-passe de partilhado do Olá, mas em vez disso, obter palavra-passe do permissões toouse Olá como parte de um fluxo de autenticação orquestradas. Além disso, com algumas aplicações de SSO de palavra-passe, tem Olá opção toohave do Azure AD periodicamente rollover (atualização) Olá palavra-passe com grande e complexas palavras-passe, aumentar a segurança da conta Olá. administrador de Olá pode facilmente conceder ou revogar o acesso tooan aplicação e também saber quem tem acesso toohello conta e quem acedeu ao mesmo no Olá passado.

AD do Azure suporta a contas partilhadas para qualquer Enterprise Mobility Suite (EMS), Premium ou Basic utilizadores licenciados, em todos os tipos de palavra-passe única, inicie sessão em aplicações. Pode partilhar contas para qualquer uma das milhares de aplicações previamente integradas na Galeria de aplicações de Olá e pode adicionar a sua própria aplicação de autenticação de palavra-passe com [aplicações personalizadas de SSO](active-directory-sso-integrate-saas-apps.md).

Funcionalidades do Azure AD que ativar a partilha de conta incluem:

* [Palavra-passe-início de sessão único](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Palavra-passe único início de sessão no agente
* [Atribuição de grupo](active-directory-accessmanagement-self-service-group-management.md)
* Aplicações de palavra-passe personalizada
* [Dashboard/relatórios de utilização da aplicação](active-directory-passwords-get-insights.md)
* Portais de acesso do utilizador final
* [Proxy de aplicações](active-directory-application-proxy-get-started.md)
* [Do Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>Uma conta de partilha
toouse do Azure AD tooshare uma conta precisa de:

* Adicionar uma aplicação [Galeria de aplicações](https://azure.microsoft.com/marketplace/active-directory/) ou [aplicação personalizada](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* Configurar aplicação Olá palavra-passe único Sign-On (SSO)
* Utilize [atribuição baseada em grupo](active-directory-accessmanagement-group-saasapps.md) e selecione Olá opção tooenter uma credencial partilhada
* Opcional: em algumas aplicações, tais como o Facebook, Twitter ou LinkedIn, pode ativar a opção de Olá para [do Azure AD automatizada palavra-passe roll a ativação pós-falha](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

Pode também efetuar a conta partilhada mais segura com o multi-factor Authentication (MFA) (saber mais sobre [proteger aplicações com o Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) e pode delegar Olá capacidade toomanage quem tem acesso toohello aplicação a utilizar [Do azure AD Self-Service](active-directory-accessmanagement-self-service-group-management.md) gestão de grupo.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)
* [Proteger aplicações com o acesso condicional](active-directory-conditional-access.md)
* [Gestão de grupos self-service/SSAA](active-directory-accessmanagement-self-service-group-management.md)

