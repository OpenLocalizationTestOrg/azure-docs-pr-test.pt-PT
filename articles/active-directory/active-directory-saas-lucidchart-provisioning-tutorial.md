---
title: "Tutorial: Configurar LucidChart para aprovisionamento de utilizadores automática no Azure Active Directory | Microsoft Docs"
description: "Saiba como tooconfigure do Azure Active Directory tooautomatically aprovisionar e aprovisionar desativação do utilizador contas tooLucidChart."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a>Tutorial: Configurar LucidChart para aprovisionamento de utilizadores automática


o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform no LucidChart e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooLucidChart. 

## <a name="prerequisites"></a>Pré-requisitos

cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:

*   Um inquilino do Azure Active directory
*   Um inquilino LucidChart com Olá [plano empresarial](https://www.lucidchart.com/user/117598685#/subscriptionLevel) ou melhor ativado 
*   Uma conta de utilizador no LucidChart com permissões de administrador 

## <a name="assigning-users-toolucidchart"></a>Atribuir utilizadores tooLucidChart

Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações. No contexto de Olá de aprovisionamento da conta de utilizador automáticas, apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD é sincronizado. 

Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos do Azure AD representam Olá os utilizadores que precisam de acesso tooyour LucidChart aplicação. Depois de decidir, pode atribuir estas aplicações de LucidChart tooyour utilizadores ao seguir as instruções de Olá aqui:

[Atribuir um utilizador ou grupo tooan de aplicações](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a>Sugestões importantes para atribuir utilizadores tooLucidChart

*   Recomenda-se que um único utilizador do Azure AD é atribuído tooLucidChart tootest Olá aprovisionamento de configuração. Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um tooLucidChart de utilizador, tem de selecionar o Olá **utilizador** função, ou outra válida específicas da aplicação função (se disponível) na caixa de diálogo de atribuição de Olá. Olá **predefinido acesso** função não funciona para o aprovisionamento e estes utilizadores são ignorados.


## <a name="configuring-user-provisioning-toolucidchart"></a>Configurar tooLucidChart de aprovisionamento de utilizadores 

Esta secção orienta-o ligar a API de aprovisionamento da conta de utilizador do seu tooLucidChart do Azure AD e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar as contas de utilizador atribuída LucidChart com base na atribuição de utilizadores e grupos no Azure AD .

> [!TIP]
> Pode também optar por tooenabled baseados em SAML Single Sign-On para LucidChart, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com). O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a>Configurar conta de utilizador automática aprovisionamento tooLucidChart no Azure AD


1. No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.

2. Se já tiver configurado LucidChart para o início de sessão único, procure a instância do LucidChart utilizando o campo de procura Olá. Caso contrário, selecione **adicionar** e procure **LucidChart** na Galeria de aplicações de Olá. Selecione LucidChart os resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.

3. Selecione a sua instância do LucidChart, em seguida, selecione Olá **aprovisionamento** separador.

4. Conjunto Olá **modo de aprovisionamento** demasiado**automática**.

    ![Aprovisionamento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. Em Olá **credenciais de administrador** secção, Olá entrada **segredo Token** gerado pela conta do seu LucidChart (pode encontrar o token de Olá na sua conta: **equipa**  >  **Integração de aplicações** > **SCIM**). 

    ![Aprovisionamento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar-se a aplicação de LucidChart tooyour. Se falhar a ligação de Olá, certifique-se de que a conta de LucidChart possui permissões de administrador e repita o passo 5.

7. Introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro aprovisionamento no Olá **correio eletrónico de notificação** campo e a caixa de verificação de Olá de verificação "enviar uma notificação por e-mail quando ocorre uma falha."

8. Clique em **Guardar**. 

9. Na secção de mapeamentos Olá, selecione **sincronizar utilizadores do Azure Active Directory tooLucidChart**.

10. No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooLucidChart. Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá contas de utilizador LucidChart para operações de atualização. Selecione Olá guardar botão toocommit quaisquer alterações.

11. tooenable Olá serviço aprovisionamento do Azure AD para LucidChart, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá **definições** secção

12. Clique em **Guardar**. 

Esta operação inicia a sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooLucidChart no Olá utilizadores e a secção de grupos. a sincronização inicial Olá demora mais tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução. Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento do serviço.

Para obter mais informações sobre como os registos de aprovisionamento do tooread Olá do Azure AD, consulte [relatórios sobre o aprovisionamento da conta de utilizador automáticas](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Recursos adicionais

* [Gerir o aprovisionamento da conta de utilizador para aplicações da empresa](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Passos seguintes

* [Saiba como tooreview os registos e obter relatórios sobre o aprovisionamento de atividade](active-directory-saas-provisioning-reporting.md)
