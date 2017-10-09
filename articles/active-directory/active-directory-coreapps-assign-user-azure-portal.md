---
title: "aaaAssign um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory | Microsoft Docs"
description: "Como tooselect um tooassign de aplicação empresarial um tooit de utilizador ou grupo no Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a>Atribuir um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory
É fácil tooassign um utilizador ou um aplicações da empresa tooyour grupo no Azure Active Directory (Azure AD). Tem de ter Olá as permissões adequadas toomanage Olá de aplicações e tem de ser um administrador global para o diretório de Olá.

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a>Como atribuir acesso de utilizador tooan aplicações de empresa?
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de Olá.
2. Selecione **mais serviços**, introduza Azure Active Directory na caixa de texto Olá e, em seguida, selecione **Enter**.
3. No Olá **Azure Active Directory - *directoryname***  painel (ou seja, Olá do Azure AD painel diretório Olá estiver a gerir), selecione **aplicações empresariais**.

    ![Aplicações da empresa ao abrir](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. No Olá **aplicações empresariais** painel, selecione **todas as aplicações**. Verá uma lista de aplicações de Olá que pode gerir.
5. No Olá **aplicações da empresa - todas as aplicações** painel, selecione uma aplicação.
6. No Olá ***appname*** painel (ou seja, Olá painel com o nome Olá Olá aplicação selecionada no título de Olá), selecione **utilizadores e grupos**.

    ![Selecionar Olá todos os comandos de aplicações](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. No Olá ***appname*** **-atribuição de grupos de & utilizador** painel, selecione de Olá **adicionar** comando.
8. No Olá **adicionar atribuição** painel, selecione **utilizadores e grupos**.

    ![Atribuir um utilizador ou grupo toohello uma aplicação](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. No Olá **utilizadores e grupos** painel, selecione um ou mais utilizadores ou grupos de Olá lista e, em seguida, selecione Olá **selecione** botão na Olá parte inferior do painel de Olá.
10. No Olá **adicionar atribuição** painel, selecione **função**. Em seguida, no Olá **selecionar função** painel, selecione um toohello de tooapply função selecionado de utilizadores ou grupos e, em seguida, selecione Olá **OK** botão na Olá parte inferior do painel de Olá.
11. No Olá **adicionar atribuição** painel, selecione de Olá **atribuir** botão na Olá parte inferior do painel de Olá. Olá atribuídos a utilizadores ou grupos serão tem permissões de Olá definidas pela função selecionada de Olá para esta aplicação empresarial.

## <a name="next-steps"></a>Passos seguintes
* [Ver todos os meus grupos](active-directory-groups-view-azure-portal.md)
* [Remover uma atribuição de utilizador ou grupo a partir de uma aplicação empresarial](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Desativar o utilizador inícios de sessão para uma aplicação empresarial](active-directory-coreapps-disable-app-azure-portal.md)
* [Alterar o nome de Olá ou logótipo de uma aplicação empresarial](active-directory-coreapps-change-app-logo-user-azure-portal.md)
