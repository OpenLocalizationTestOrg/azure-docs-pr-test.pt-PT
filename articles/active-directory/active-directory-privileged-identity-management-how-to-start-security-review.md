---
title: "aaaHow toostart uma revisão do acesso | Microsoft Docs"
description: "Saiba como toocreate acesso rever de identidades privilegiadas com Olá aplicação Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>Como toostart acesso consultar no Azure AD Privileged Identity Management
Atribuições de função ficam "obsoletas" quando os utilizadores com acesso privilegiado que não precisam de já. Na ordem de risco Olá tooreduce associado estas atribuições de funções obsoletos, os administradores de com função privilegiada regularmente devem rever funções Olá que atribuiu utilizadores. Este documento aborda os passos de Olá para iniciar uma revisão do acesso no Azure AD Privileged Identity Management (PIM).

## <a name="start-an-access-review"></a>Iniciar uma revisão do acesso
> [!NOTE]
> Se ainda não adicionou o dashboard de tooyour de aplicações Olá PIM em Olá portal do Azure, consulte passos Olá [introdução ao Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Do PIM aplicação principal página Olá, existem três formas toostart uma revisão do acesso:

* **Aceder revisões** > **adicionar**
* **Funções** > **revisão** botão
* Selecione Olá função específica toobe revistos na lista de funções de Olá > **revisão** botão

Quando clica em Olá **rever** botão, hello **iniciar uma revisão do acesso** é apresentado o painel. Neste painel, está curso tooconfigure Olá Reveja com um nome e tempo limite, escolha um tooreview de função e decidir que executará a revisão Olá.

![Iniciar uma revisão do acesso - captura de ecrã][1]

### <a name="configure-hello-review"></a>Configurar revisão Olá
Reveja do toocreate acesso, tem de tooname e defina uma data de início e de fim.

![Configurar revisão - captura de ecrã][2]

Certifique-Olá comprimento Olá rever suficientemente longo para os utilizadores toocomplete. Se concluir antes da data de fim de Olá, pode sempre parar a revisão Olá antecipadamente.

### <a name="choose-a-role-tooreview"></a>Escolha um tooreview de função
Cada revisão centra-se apenas uma função. Exceto se tiver iniciado o Olá revisão do acesso a partir do painel de uma função específica, terá agora toochoose uma função.

1. Navegue demasiado**rever membro da função**
   
    ![Reveja o membro da função - captura de ecrã][3]
2. Escolha uma função Olá lista.

### <a name="decide-who-will-perform-hello-review"></a>Decidir que executará a revisão Olá
Existem três opções para executar uma revisão. Pode atribuir Olá revisão toosomeone toocomplete pessoa, pode fazê-lo por si ou pode fazer com que cada utilizador, reveja os suas próprias acesso.

1. Navegue demasiado**selecione revisores**
   
    ![Selecione os revisores - captura de ecrã][4]
2. Escolha uma das opções de Olá:
   
   * **Selecione revisor**: Utilize esta opção se não souber quem tem acesso. Com esta opção, pode atribuir proprietário do recurso Olá revisão tooa ou toocomplete do Gestor de grupo.
   * **Enviar-me**: útil se pretender que toopreview como acesso revê o trabalho ou se quiser tooreview em nome de pessoas que não é possível.
   * **Membros reveja próprios**: Utilize esta opção toohave Olá utilizadores rever as suas próprias atribuições de funções.

### <a name="start-hello-review"></a>Iniciar Olá revisão
Por fim, terá de Olá opção toorequire que os utilizadores forneçam um motivo se estes aprovar o acesso. Adicionar uma descrição da revisão de Olá se assim o desejar e selecione **iniciar**.

Certifique-se de que permite aos utilizadores saber que existe uma revisão do acesso a aguardar para os mesmos e apresentar [como tooperform rever um acesso](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-hello-access-review"></a>Gerir a revisão do acesso Olá
Pode controlar o progresso de Olá como revisores Olá concluir as revisões em Olá dashboard do Azure AD PIM, no Olá acesso revê secção. Sem direitos de acesso serão alterados no diretório de Olá até [concluir a revisão Olá](active-directory-privileged-identity-management-how-to-complete-review.md).

Até que o período de avaliação de Olá está acima, pode notificar utilizadores toocomplete respetiva revisão ou parar Olá revisão numa fase inicial do acesso Olá revê secção.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>Tabela PIM de conteúdo
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
