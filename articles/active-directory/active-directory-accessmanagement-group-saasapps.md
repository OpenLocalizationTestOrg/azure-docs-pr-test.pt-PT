---
title: "aaaUsing tooSaaS de acesso toomanage um grupo aplicações | Microsoft Docs"
description: "Como toouse grupos no Azure Active Directory Premium ou Basic tooassign acedam a aplicações de tooSaaS que estão integradas no Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>Utilizar um grupo toomanage acesso tooSaaS aplicações
Utilizar o Azure Active Directory (Azure AD) com uma licença do Azure AD Premium ou Basic do Azure AD, pode utilizar grupos tooassign acesso tooa aplicação SaaS que está integrada com o Azure AD. Por exemplo, se pretender que o acesso de tooassign para Olá marketing departamento toouse cinco diferentes aplicações SaaS, pode criar um grupo que contenha Olá os utilizadores do departamento de marketing Olá e, em seguida, atribuir esse grupo toothese cinco aplicações SaaS que são necessária pelo departamento de marketing Olá. Desta forma pode poupar tempo ao gerir associação Olá Olá marketing departamento num único local. Os utilizadores, em seguida, são atribuídos toohello aplicação quando estes são adicionados como membros do grupo de marketing Olá, e as respetivas atribuições removidas da aplicação Olá quando estes são removidos de Olá grupo de marketing.

> [!IMPORTANT]
> A Microsoft recomenda que gere o Azure AD através de Olá [Centro de administração do Azure AD](https://aad.portal.azure.com) no Olá portal do Azure em vez de utilizar Olá portal clássico do Azure referenciado neste artigo. 

Esta capacidade pode ser utilizada com centenas de aplicações que pode adicionar a partir de dentro de Olá Galeria de aplicações do Azure AD.

**acesso de tooassign para uma aplicação SaaS de tooa de grupo**

1. No Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory** na barra de navegação de Olá no Olá lado esquerdo.
2. Selecione Olá **diretório** separador e diretório Olá, em seguida, abra em que pretende acesso tooassign para um grupo de tooa aplicação SaaS.
3. Selecione Olá **aplicações** separador. Selecione uma aplicação que adicionou de Olá Galeria de aplicações e, em seguida, clique em Olá **utilizadores e grupos** separador.
4. No Olá **utilizadores e grupos** separador, Olá **começadas** campo, introduza o nome de Olá de Olá toowhich de grupo que pretende que o acesso de tooassign e, em seguida, selecione Olá marca de verificação no canto superior direito da Olá. Basta tootype Olá primeiro faz parte do nome do grupo.
5. Selecione o grupo de Olá, em seguida, em seguida, selecione Olá **atribuir acesso** botão. Selecione **Sim** quando for apresentada a mensagem de confirmação de saudação. Filiações aninhadas não são suportadas para a atribuição baseada em grupo tooapplications neste momento.
6. Também pode ver que utilizadores são atribuídos a aplicação toohello, diretamente ou através da associação num grupo. toodo Olá, alteração **Mostrar a lista pendente de 'Grupos'** demasiado**'Todos os utilizadores'**. lista de Olá mostra os utilizadores no diretório de Olá e se deve ou não cada utilizador atribuído toohello aplicação. lista de Olá também mostra se os utilizadores de Olá atribuído são atribuídos diretamente aplicação toohello (tipo de atribuição apresentada como 'Direta') ou em virtude da associação de grupo (apresentada como 'Herdado'. tipo de atribuição)

> [!NOTE]
> Pode ver Olá utilizadores e separador grupos apenas depois de ter ativado o Azure AD Premium ou Basic do Azure AD.
>
>

### <a name="next-steps"></a>Passos seguintes
Estes artigos fornecem informações adicionais acerca do Azure Active Directory.

* [Gerir o acesso tooresources com grupos do Azure Active Directory](active-directory-manage-groups.md)
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)
* [Cmdlets do Azure Active Directory para configurar definições de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [O que é o Azure Active Directory?](active-directory-whatis.md)
* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)
