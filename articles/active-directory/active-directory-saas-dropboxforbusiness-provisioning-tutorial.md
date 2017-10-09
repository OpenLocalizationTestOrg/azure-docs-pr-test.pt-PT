---
title: "Tutorial: Integração do Azure Active Directory com o Dropbox para empresas | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o Dropbox para empresas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a>Tutorial: Configurar o Dropbox para empresas para aprovisionamento de utilizadores automática

o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform no Dropbox para empresas e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooDropbox para empresas.

## <a name="prerequisites"></a>Pré-requisitos

cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:

*   Um inquilino do Azure Active directory.
*   Um Dropbox para empresas início de sessão único subscrição ativado.
*   Uma conta de utilizador no Dropbox para empresas com permissões de administrador de equipa.

## <a name="assigning-users-toodropbox-for-business"></a>Atribuir utilizadores tooDropbox para empresas

Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações. No contexto de Olá de aprovisionamento da conta de utilizador automáticas, apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD é sincronizado.

Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos no Azure AD representam Olá utilizadores precisam de aceder tooyour Dropbox para a aplicação de negócio. Depois de decidir, pode atribuir estes tooyour utilizadores Dropbox para a aplicação de negócio, seguindo as instruções de Olá aqui:

[Atribuir um utilizador ou grupo tooan de aplicações](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a>Sugestões importantes para atribuir utilizadores tooDropbox para empresas

*   Recomenda-se que um único utilizador do Azure AD é atribuído tooDropbox para Olá do negócio tootest aprovisionamento de configuração. Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um tooDropbox de utilizador para empresas, tem de selecionar uma função de utilizador válido. função de "Acesso predefinida" Olá não funciona para o aprovisionamento...

## <a name="enable-automated-user-provisioning"></a>Ativar o aprovisionamento automatizado do utilizador

Esta secção orienta-o ligar a sua tooDropbox do Azure AD para a conta de utilizador de negócio API de aprovisionamento e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar as contas de utilizador atribuído no Dropbox para empresas com base no utilizador e grupo atribuição no Azure AD.

>[!Tip]
>Pode também optar por tooenabled baseados em SAML Single Sign-On para Dropbox para empresas, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com). O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure aprovisionamento da conta utilizador automáticas:

1. No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.

2. Se já tiver configurado o Dropbox para empresas para o início de sessão único, procure a instância da Dropbox para empresas com o campo de procura Olá. Caso contrário, selecione **adicionar** e procure **Dropbox para empresas** na Galeria de aplicações de Olá. Selecione o Dropbox para empresas dos resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.

3. Selecione a instância da Dropbox para empresas, em seguida, selecione Olá **aprovisionamento** separador.

4. Conjunto Olá **modo de aprovisionamento** demasiado**automática**. 

    ![Aprovisionamento](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** secção, clique em **autorizar**. É aberta uma Dropbox para a caixa de diálogo de início de sessão de negócio numa nova janela do browser.

6. No Olá **início de sessão tooDropbox toolink com o Azure AD** caixa de diálogo, início de sessão tooyour Dropbox para o inquilino de negócio.

     ![Aprovisionamento de utilizadores](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "aprovisionamento de utilizadores")

7. Certifique-se de que pretende toogive do Azure Active Directory permissão toomake alterações tooyour Dropbox para o inquilino de negócio. Clique em **permitir**.
    
      ![Aprovisionamento de utilizadores](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "aprovisionamento de utilizadores")

8. No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar tooyour Dropbox para a aplicação de negócio. Se falhar a ligação de Olá, certifique-se a Dropbox para a conta tem permissões de administração de equipa e tente Olá **"Autorizar"** passo novamente.

9. Introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro aprovisionamento no Olá **correio eletrónico de notificação** campo e marque Olá caixa de verificação.

10. Clique em **guardar.**

11. Na secção de mapeamentos Olá, selecione **tooDropbox sincronizar utilizadores do Azure Active Directory para empresas.**

12. No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooDropbox para empresas. Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá contas de utilizador Dropbox para empresas para operações de atualização. Selecione Olá guardar botão toocommit quaisquer alterações.

13. tooenable Olá serviço aprovisionamento do Azure AD para Dropbox para empresas, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá secção de definições

14. Clique em **guardar.**

Iniciar sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooDropbox para empresas no Olá utilizadores e a secção de grupos. a sincronização inicial Olá demora mais tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução. Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento para a aplicação de negócio do serviço no seu Dropbox.

Agora, pode criar uma conta de teste. Aguarde pela cópia de segurança minutos too20 tooverify Olá conta foi sincronizada tooDropbox para empresas.

Um ciclo de aprovisionamento de utilizadores concluída com êxito é indicada pelo Estado relacionado.

![Atribuir utilizadores](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "atribuir utilizadores")


## <a name="additional-resources"></a>Recursos adicionais

* [Gerir o aprovisionamento da conta de utilizador para aplicações da empresa](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar o início de sessão único](active-directory-saas-dropboxforbusiness-tutorial.md)