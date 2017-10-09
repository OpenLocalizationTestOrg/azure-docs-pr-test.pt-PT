---
title: aaaDedicated grupos no Azure Active Directory | Microsoft Docs
description: "Descrição geral de como dedicado de grupos de trabalho no Azure Active Directory e como são criados."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Grupos dedicados no Azure Active Directory
No Azure Active Directory (Azure AD), funcionalidade de grupos dedicados Olá cria e povoa automaticamente a associação de grupos do Azure AD predefinido. Não não possível adicionar membros dos grupos dedicados ou removida utilizando hello do Azure clássicos portal, cmdlets do Windows PowerShell, ou através de programação.

> [!NOTE]
> Grupos dedicados requerem que está atribuída uma licença do Azure AD Premium
>
> * administrador de Olá que gere a regra de Olá num grupo
> * todos os utilizadores que estão selecionados por Olá regra toobe um membro do grupo de Olá
>
>

**grupos de tooenable dedicado**

1. No Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e, em seguida, abra o diretório da sua organização.
2. Selecione Olá **grupos** separador e grupo, em seguida, abra Olá pretende tooedit.
3. Selecione Olá **configurar** separador e, em seguida, defina **ative os grupos dedicados** demasiado**Sim**.

Depois de Olá ativar grupos dedicados comutador está definido demasiado**Sim**, pode ativar a mais Olá diretório tooautomatically criar grupo dedicado de todos os utilizadores Olá por definição Olá **ativar "Todos os utilizadores" grupo** comutador demasiado**Sim**. Em seguida, também pode editar nome Olá deste grupo dedicado, introduzindo-Olá **nome a apresentar para "Todos os utilizadores" grupo** campo.

pode ser utilizado o grupo de todos os utilizadores Olá tooassign Olá mesmo permissões tooall Olá os utilizadores no seu diretório. Por exemplo, pode conceder todos os utilizadores na sua tooa de acesso de diretório aplicação SaaS através da atribuição de acesso para Olá todos os utilizadores dedicados grupo toothis aplicação.

grupo de todos os utilizadores Olá dedicado inclui todos os utilizadores no diretório de Olá, incluindo utilizadores externos e de convidados. Se precisar de um grupo que exclui os utilizadores externos, em seguida, pode conseguir isto ao criar um grupo com uma regra dinâmica baseadas em atributos como seguinte Olá:

                (user.userPrincipalName -notContains "#EXT#@")

Para um grupo que exclua todos os convidados, utilize uma regra, como o seguinte Olá:

                (user.userType -ne "Guest")

toolearn sobre como toocreate *avançadas* regras (regras que podem conter várias comparações) para filiação dinâmica em grupos, consulte [utilizar toocreate de atributos avançadas regras](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Passos seguintes
Estes artigos fornecem informações adicionais acerca do Azure Active Directory.

* [Gerir o acesso tooresources com grupos do Azure Active Directory](active-directory-manage-groups.md)
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)
* [O que é o Azure Active Directory?](active-directory-whatis.md)
* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)
