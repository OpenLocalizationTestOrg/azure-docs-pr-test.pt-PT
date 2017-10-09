---
title: aaaGet iniciado com o Azure AD Privileged Identity Management | Microsoft Docs
description: "Saiba como toomanage privilegiado identidades com aplicações do Azure Active Directory Privileged Identity Management Olá no portal do Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Comece a utilizar o Azure AD Privileged Identity Management
Com o Azure Active Directory (AD) Privileged Identity Management, pode gerir, controlar e monitorizar o acesso dentro da sua organização. Este âmbito inclui acesso tooresources no Azure AD e outros serviços online da Microsoft, como o Office 365 ou o Microsoft Intune.

Este artigo mostra como tooadd Olá tooyour de aplicação do Azure AD PIM dashboard do portal do Azure.

## <a name="add-hello-privileged-identity-management-application"></a>Adicionar a aplicação de Privileged Identity Management Olá
Antes de utilizar o Azure AD Privileged Identity Management, terá de tooadd Olá aplicação tooyour dashboard do portal do Azure.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/) como um administrador global do seu diretório.
2. Se a sua organização tiver mais do que um diretório, selecione o seu nome de utilizador no canto direito superior Olá de Olá portal do Azure. Selecione o diretório de olá onde pretende toouse PIM.
3. Selecione **mais serviços** e utilizar Olá toosearch de caixa de texto de filtro para **do Azure AD Privileged Identity Management**.
4. Verifique **Pin toodashboard** e, em seguida, clique em **criar**. é aberto o Olá aplicação Privileged Identity Management.

Se estiver a hello primeira pessoa toouse do Azure AD Privileged Identity Management no seu diretório, são automaticamente atribuídos Olá **administrador de segurança** e **administrador com função privilegiada** funções no diretório de Olá. Apenas os administradores de função com privilégios podem gerir as atribuições de funções de utilizadores. Além disso, pode optar por toorun Olá [Assistente de segurança.](active-directory-privileged-identity-management-security-wizard.md) que o orienta através de experiência de deteção e atribuição inicial no Olá.

## <a name="navigate-tooyour-tasks"></a>Navegue tooyour tarefas
Depois de configurada do Azure AD Privileged Identity Management, consulte painel de navegação de Olá sempre que abrir a aplicação Olá. Utilize este painel tooaccomplish as tarefas de gestão de identidade.

![Tarefas de nível superior para PIM - captura de ecrã](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **As minhas funções** leva-o tooa lista das funções que são atribuídos tooyou. Esta secção é onde ativa as funções que lhe são elegíveis.
* **Aprovar Pedidos (Pré-visualização)** apresenta uma lista de pedidos pendentes de ativação dos utilizadores no seu diretório. [Saiba mais.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **(Pré-visualização) de pedidos pendentes** apresenta qualquer tooactivate de toohave efetuada pedidos atual.
* **Rever o acesso** demora tooany pendentes acesso revê terá toocomplete, se estiver a rever o acesso para si próprio ou outra pessoa.
* **Funções de diretório do Azure AD** localizado Olá "Gerir" secção é dashboard Olá para atribuições de funções de toomanage de administradores de com função privilegiada, alterar definições de ativação de função, revisões de acesso de início e muito mais. Opções de Olá neste dashboard estão desativadas para qualquer pessoa que não é um administrador com função privilegiada.

## <a name="next-steps"></a>Passos seguintes
Olá [descrição geral do Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) inclui mais informações sobre como pode gerir o acesso administrativo na sua organização.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
