---
title: aaaCreate um grupo de utilizadores no Azure Active Directory | Microsoft Docs
description: Como toocreate um grupo no Azure Active Directory e adicionar membros toohello grupo
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Crie um grupo e adicionar membros no Azure Active Directory
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-groups-create-azure-portal.md)
> * [Portal Clássico do Azure](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Este artigo explica como toocreate e preencher um novo grupo no Azure Active Directory. Utilize tarefas de gestão de tooperform um grupo, tais como atribuir licenças ou permissões tooa número de utilizadores ou dispositivos em simultâneo.

## <a name="how-do-i-create-a-group"></a>Como crio um grupo?
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de Olá.
2. Selecione **mais serviços**, introduza **grupos de utilizadores e** no Olá caixa de texto e, em seguida, selecione **Enter**.

   ![Gestão de utilizadores de abertura](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. No Olá **utilizadores e grupos** painel, selecione **todos os grupos**.

   ![Painel de grupos de Olá de abertura](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. No Olá **utilizadores e grupos - todos os grupos** painel, selecione de Olá **adicionar** comando.

   ![Selecionar o comando de adicionar Olá](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. No Olá **grupo** painel, adicionar um nome e descrição para o grupo de Olá.
6. tooselect membros tooadd toohello grupo, selecione **atribuído** no Olá **tipo de associação** caixa e, em seguida, selecione **membros**. Para obter mais informações sobre como toomanage Olá associação de um grupo de forma dinâmica, consulte [utilizar toocreate de atributos avançadas de regras de associação ao grupo](active-directory-groups-dynamic-membership-azure-portal.md).

   ![Selecionar Membros tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. No Olá **membros** painel, selecione uma ou mais utilizadores ou dispositivos grupo de toohello tooadd e Olá selecione **selecione** botão na parte inferior de Olá de Olá painel tooadd-los toohello grupo. Olá **utilizador** filtros caixa Olá apresentação com base na correspondência sua entrada tooany parte um nome de utilizador ou dispositivo. Não existem carateres universais são aceites na caixa de.
8. Quando acabar de adicionar membros toohello grupo, selecione **criar** no Olá **grupo** painel.    

   ![Criar a confirmação de grupo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>Passos seguintes
Estes artigos fornecem informações adicionais acerca do Azure Active Directory.

* [Consulte os grupos existentes](active-directory-groups-view-azure-portal.md)
* [Gerir as definições de um grupo](active-directory-groups-settings-azure-portal.md)
* [Gerir os membros de um grupo](active-directory-groups-members-azure-portal.md)
* [Gerir membros de um grupo](active-directory-groups-membership-azure-portal.md)
* [Gerir regras dinâmicas para os utilizadores de um grupo](active-directory-groups-dynamic-membership-azure-portal.md)
