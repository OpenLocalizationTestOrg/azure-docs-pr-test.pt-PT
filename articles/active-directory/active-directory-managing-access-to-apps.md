---
title: aaaManaging acesso tooapps utilizar o Azure AD | Microsoft Docs
description: "Descreve como o Azure Active Directory permite às organizações toospecify Olá aplicações toowhich cada utilizador tem acesso."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>Gerir o acesso tooapps
Gestão de acesso em curso, avaliação de utilização e relatórios continuam toobe um desafio depois de uma aplicação está integrada no sistema de identidade da sua organização. Em muitos casos, os administradores de TI ou suporte técnico tem tootake uma função ativa em curso na gestão de aplicações de tooyour de acesso. Por vezes, a atribuição é efetuada por uma equipa de TI por divisões ou geral. Muitas vezes, a decisão de atribuição de Olá é toobe pretendido toohello delegado negócio decisor, os respetivos aprovação antes de IT torna Olá atribuição.  Outras organizações investem na integração com um existente automatizada identidades e acessos sistema de gestão, como o controlo de acesso baseado em funções (RBAC) ou o controlo de acesso baseado em atributos (ABAC). Integração de Olá e desenvolvimento de regra tendem toobe especializado e dispendioso. Monitorização ou relatórios sobre a abordagem de gestão são o seu próprio investimento separado, dispendioso e complexo.

## <a name="how-does-azure-active-directory-help"></a>Como ajuda do Azure Active Directory?
 Azure AD de gestão de acesso de um vasto conjunto de suporta para aplicações configuradas, permitindo organizações tooeasily alcançar políticas de acesso à direita de Olá vão de atribuição automática, baseadas em atributos (cenários de ABAC ou RBAC) através da delegação e incluindo gestão de administradores. Com o Azure AD pode facilmente conseguir políticas complexas, combinar vários modelos de gestão para uma única aplicação e podem ainda utilizar novamente as regras de gestão em todas as aplicações com Olá audiências mesmas.

* [Adicionar novos ou existentes de aplicações](active-directory-sso-integrate-saas-apps.md)

 Atribuição de aplicações do Azure AD centra-se em dois modos de atribuição primário:

* **Atribuição de individuais** administrador de TI um com permissões de Administrador Global do diretório pode selecionar as contas de utilizador individuais e conceder-lhes acesso toohello aplicação.
* **Atribuição baseada em grupo (paga do Azure AD apenas)** administrador de TI um com permissões de Administrador Global do diretório pode atribuir uma aplicação de toohello de grupo. Acesso de utilizadores específicos é determinado pelo se forem membros do grupo de Olá momento Olá tentam aplicação de Olá tooaccess. Por outras palavras, um administrador eficazmente pode criar uma regra de atribuição a indicar "qualquer membro de Olá atribuído grupo atual tem acesso toohello aplicação". Utilizar esta opção de atribuição, os administradores podem beneficiar de qualquer uma das opções de gestão de grupo do Azure AD, incluindo [baseadas em atributos de grupos dinâmicos](active-directory-accessmanagement-manage-groups.md), grupos de sistema externo (por exemplo, no local do Active Directory ou Workday), ou grupos gerida pelo administrador ou self-service-geridos. Um único grupo pode ser facilmente atribuído toomultiple aplicações, garantindo que as aplicações com a afinidade de atribuição possam partilhar as regras de atribuição, reduzindo Olá geral complexidade da gestão. Tenha em atenção que o grupo aninhado associações não são suportadas para atribuição baseada em grupo tooapplications neste momento.

Utilizar estes modos de atribuição de dois, os administradores podem alcançar qualquer abordagem de gestão de atribuição desejados.

Com o Azure AD, utilização e relatórios de atribuição é totalmente integrados, ativar administradores tooeasily relatório no estado de atribuição, erros de atribuição e a utilização do mesmo.

## <a name="complex-application-assignment-with-azure-ad"></a>Atribuição de aplicações complexas com o Azure AD
Considere uma aplicação, como o Salesforce. Em muitas organizações, Salesforce é principalmente utilizado por organizações Olá de vendas e marketing. Muitas vezes, os membros da equipa de marketing de Olá tem altamente privilegiados tooSalesforce de acesso, enquanto os membros da equipa de vendas Olá tem acesso limitado. Em muitos casos, uma população abrangente dos técnicos de informação ter restringido a acesso toohello aplicação. Regras de toothese exceções dificultar é importante. É frequentemente prerogative Olá de Olá marketing ou vendas liderança equipas toogrant um acesso de utilizadores ou alterar as respetivas funções independentemente estas regras genéricas.

Com o Azure AD, aplicações, como o Salesforce podem ser pré-configurados para-início de sessão único (SSO) e o aprovisionamento automatizado. Assim que a aplicação de Olá está configurada, um administrador pode demorar Olá ação única toocreate e atribuir grupos adequados Olá. Neste exemplo, um administrador foi possível executar Olá atribuições os seguintes:

* [Grupos dinâmicos](active-directory-accessmanagement-manage-groups.md) pode ser definido tooautomatically representar todos os membros das equipas de marketing e de vendas de Olá utilizar atributos como departamento ou função:
  
  * Todos os membros dos grupos de marketing deverá ser atribuídos a função de "marketing" de toohello no Salesforce
  * Todos os membros de vendas equipa grupos seria ser atribuída a função de "vendas" toohello no Salesforce. Um refinement mais utilizar vários grupos que representam as equipas de vendas regionais atribuídas toodifferent Salesforce funções.
* mecanismo de exceção do tooenable Olá, pode ser criado um grupo de self-service para cada função. Por exemplo, o grupo de "Salesforce exceção de marketing" Olá pode ser criado como um grupo self-service. grupo de Olá pode ser atribuído a função de marketing toohello Salesforce e a equipa de liderança marketing Olá pode ser efetuada proprietários. Os membros da equipa de liderança marketing Olá foi possível adicionar ou remover utilizadores, definir uma política de associação, ou mesmo aprovar ou negar toojoin de pedidos de utilizadores individuais. Esta opção é suportada através de uma trabalho adequada experiência de informações do que não necessite de formação especializada para proprietários ou membros.

Neste caso, todos os utilizadores atribuídos seria tooSalesforce automaticamente aprovisionado, conforme forem grupos toodifferent adicionado que a atribuição de função seria atualizada no Salesforce. Os utilizadores seriam ser capaz de toodiscover e aceder Salesforce através do painel de acesso da aplicação Microsoft Olá, os clientes do Office web, ou mesmo navegando tootheir organizacional página de início de sessão do Salesforce. Os administradores seria tooeasily capaz de ver utilização e atribuição de estado utilizando relatórios do Azure AD.

Os administradores podem utilizar [acesso condicional do Azure AD](active-directory-conditional-access.md) tooset as políticas de acesso para funções específicas. Estas políticas podem incluir se é permitido acesso fora do ambiente empresarial Olá e até mesmo multi-factor Authentication ou acesso tooachieve de requisitos de dispositivos em vários casos.

## <a name="how-can-i-get-started"></a>Como pode começar a utilizar?
Primeiro, se já não estão a utilizar o Azure AD e são o administrador de TI:

* [Experimente!](https://azure.microsoft.com/trial/get-started-active-directory/) -Pode inscrever-se para uma avaliação gratuita de 30 dias hoje e implementar a sua primeira solução em nuvem em 5 minutos, utilizando a seguinte hiperligação

Funcionalidades do Azure AD que ativar a partilha de conta incluem:

* [Atribuição de grupo](active-directory-accessmanagement-self-service-group-management.md)
* Adicionar aplicações tooAzure AD
* Introdução à atribuição
* Atribuição de aplicação FAQ
* [Dashboard/relatórios de utilização da aplicação](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>Onde posso obter mais informações?
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)
* [Proteger aplicações com o acesso condicional](active-directory-conditional-access.md)
* [Gestão de grupos self-service/SSAA](active-directory-accessmanagement-self-service-group-management.md)

