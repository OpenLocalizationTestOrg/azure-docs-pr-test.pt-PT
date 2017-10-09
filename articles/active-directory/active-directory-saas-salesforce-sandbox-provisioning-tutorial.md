---
title: "Tutorial: Integração do Azure Active Directory com o Salesforce Sandbox | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e a Salesforce Sandbox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>Tutorial: Configurar o Salesforce Sandbox para o aprovisionamento de utilizador automáticas

o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform no Salesforce Sandbox e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooSalesforce Sandbox.

## <a name="prerequisites"></a>Pré-requisitos

cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:

*   Um inquilino do Azure Active directory.
*   Tem de ter um inquilino válido para o Salesforce Sandbox para o trabalho ou Salesforce Sandbox para Education. É possível utilizar uma conta de avaliação gratuita para o serviço.
*   Uma conta de utilizador no Salesforce Sandbox com as permissões de administrador de equipa.

## <a name="assigning-users-toosalesforce-sandbox"></a>Atribuir utilizadores tooSalesforce Sandbox

Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações. No contexto de Olá de aprovisionamento da conta de utilizador automático, são sincronizados apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD.

Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos no Azure AD representam Olá utilizadores precisam de aceder tooyour aplicação Salesforce Sandbox. Depois de decidir, pode atribuir tooyour estes utilizadores aplicação Salesforce Sandbox ao seguir as instruções de Olá aqui:

[Atribuir um utilizador ou grupo tooan de aplicações](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>Sugestões importantes para atribuir utilizadores tooSalesforce Sandbox

* Recomenda-se que um único utilizador do Azure AD é atribuído Olá tootest Sandbox de tooSalesforce aprovisionamento de configuração. Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.

* Ao atribuir um Sandbox de tooSalesforce do utilizador, tem de selecionar uma função de utilizador válido. função de "Acesso predefinida" Olá não funciona para o aprovisionamento.

> [!NOTE]
> Esta aplicação importa funções personalizadas a partir de Salesforce Sandbox como parte do processo, o cliente de Olá poderá pretender tooselect ao atribuir os utilizadores de aprovisionamento de Olá.

## <a name="enable-automated-user-provisioning"></a>Ativar o aprovisionamento automatizado do utilizador

Esta secção orienta-o ligar a conta de utilizador do seu Azure AD tooSalesforce Sandbox aprovisionamento API e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar o utilizador atribuído contas no Salesforce Sandbox com base no utilizador e grupo atribuição no Azure AD.

>[!Tip]
>Pode também optar por tooenabled baseados em SAML Single Sign-On do Salesforce Sandbox, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com). O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure aprovisionamento da conta utilizador automáticas:

o objetivo desta secção Olá é toooutline como tooenable aprovisionamento de utilizadores do utilizador do Active Directory contas tooSalesforce Sandbox.

1. No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.

2. Se já tiver configurado o Salesforce Sandbox para o início de sessão único, procure a instância do Salesforce Sandbox utilizando o campo de procura Olá. Caso contrário, selecione **adicionar** e procure **Salesforce Sandbox** na Galeria de aplicações de Olá. Selecione o Salesforce Sandbox de resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.

3. Selecione a sua instância do Salesforce Sandbox, em seguida, selecione Olá **aprovisionamento** separador.

4. Conjunto Olá **modo de aprovisionamento** demasiado**automática**. 
    ![Aprovisionamento](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** secção, forneça Olá seguintes definições de configuração:
   
    a. No Olá **nome de utilizador de Admin** caixa de texto, tipo de nome que tem Olá de conta de uma Salesforce Sandbox **administrador de sistema** perfil no site Salesforce.com atribuído.
   
    b. No Olá **palavra-passe de administrador** caixa de texto, tipo Olá palavra-passe desta conta.

6. tooget seu token de segurança do Salesforce Sandbox, abra um novo separador e inicie sessão no Olá mesma conta de administrador do Salesforce Sandbox. No Olá canto superior direito da página Olá, clique no seu nome e, em seguida, clique em **as minhas definições**.

     ![Ativar o aprovisionamento de utilizador automáticas](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "ativar o aprovisionamento de utilizador automáticas")
7. No painel de navegação esquerdo Olá, clique em **pessoais** tooexpand Olá secção relacionada e, em seguida, clique em **repor o meu Token de segurança**.
  
    ![Ativar o aprovisionamento de utilizador automáticas](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "ativar o aprovisionamento de utilizador automáticas")
8. No Olá **repor o meu Token de segurança** página, clique em Olá **repor o Token de segurança** botão.

    ![Ativar o aprovisionamento de utilizador automáticas](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "ativar o aprovisionamento de utilizador automáticas")
9. Verifique a receber de correio eletrónico de Olá associada a esta conta de administrador. Procure uma mensagem de e-mail do Salesforce Sandbox.com que contém o token de segurança nova Olá.
10. Copiar Olá token, aceda tooyour janela do Azure AD e cole-o Olá **Socket Token** campo.

11. No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar tooyour aplicação Salesforce Sandbox.

12. No Olá **correio eletrónico de notificação** campo, introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro de aprovisionamento e marque Olá caixa de verificação.

13. Clique em **guardar.**  
    
14.  Na secção de mapeamentos Olá, selecione **sincronizar utilizadores do Azure Active Directory tooSalesforce Sandbox.**

15. No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooSalesforce Sandbox. Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá as contas de utilizador no Salesforce Sandbox para operações de atualização. Selecione Olá guardar botão toocommit quaisquer alterações.

16. tooenable Olá serviço aprovisionamento do Azure AD para Salesforce Sandbox, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá secção de definições

17. Clique em **guardar.**


Inicia a sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooSalesforce Sandbox na secção de utilizadores e grupos de Olá. a sincronização inicial Olá demora mais tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução. Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento do serviço na aplicação Salesforce Sandbox.

Agora, pode criar uma conta de teste. Aguarde pela cópia de segurança minutos too20 tooverify Olá conta foi sincronizada toosalesforce.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerir o aprovisionamento da conta de utilizador para aplicações da empresa](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar o início de sessão único](active-directory-saas-salesforcesandbox-tutorial.md)