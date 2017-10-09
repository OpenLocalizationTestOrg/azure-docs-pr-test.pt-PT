---
title: "Tutorial: Integração do Azure Active Directory com Netsuite | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a>Tutorial: Configurar Netsuite para aprovisionamento de utilizadores automática

o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform no Netsuite e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooNetsuite.

## <a name="prerequisites"></a>Pré-requisitos

cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:

*   Um inquilino do Azure Active directory.
*   Um Netsuite início de sessão único subscrição ativado.
*   Uma conta de utilizador no Netsuite com permissões de administrador de equipa.

## <a name="assigning-users-toonetsuite"></a>Atribuir utilizadores tooNetsuite

Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações. No contexto de Olá de aprovisionamento da conta de utilizador automático, são sincronizados apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD.

Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos do Azure AD representam Olá os utilizadores que precisam de acesso tooyour Netsuite aplicação. Depois de decidir, pode atribuir estas aplicações de Netsuite tooyour utilizadores ao seguir as instruções de Olá aqui:

[Atribuir um utilizador ou grupo tooan de aplicações](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a>Sugestões importantes para atribuir utilizadores tooNetsuite

*   Recomenda-se que um único utilizador do Azure AD é atribuído tooNetsuite tootest Olá aprovisionamento de configuração. Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um tooNetsuite de utilizador, tem de selecionar uma função de utilizador válido. função de "Acesso predefinida" Olá não funciona para o aprovisionamento.

## <a name="enable-user-provisioning"></a>Ativar o aprovisionamento de utilizador

Esta secção orienta-o ligar a API de aprovisionamento da conta de utilizador do seu tooNetsuite do Azure AD e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar as contas de utilizador atribuída Netsuite com base na atribuição de utilizadores e grupos no Azure AD.

> [!TIP] 
> Pode também optar por tooenabled baseados em SAML Single Sign-On para Netsuite, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com). O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.

### <a name="tooconfigure-user-account-provisioning"></a>Aprovisionamento de conta do utilizador de tooconfigure:

o objetivo desta secção Olá é toooutline como tooenable aprovisionamento de utilizadores do utilizador do Active Directory tooNetsuite de contas.

1. No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.

2. Se já tiver configurado Netsuite para o início de sessão único, procure a instância do Netsuite utilizando o campo de procura Olá. Caso contrário, selecione **adicionar** e procure **Netsuite** na Galeria de aplicações de Olá. Selecione Netsuite os resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.

3. Selecione a sua instância do Netsuite, em seguida, selecione Olá **aprovisionamento** separador.

4. Conjunto Olá **modo de aprovisionamento** demasiado**automática**. 

    ![Aprovisionamento](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** secção, forneça Olá seguintes definições de configuração:
   
    a. No Olá **nome de utilizador de Admin** caixa de texto, tipo um Netsuite conta nome que tem Olá **administrador de sistema** perfil no Netsuite.com atribuído.
   
    b. No Olá **palavra-passe de administrador** caixa de texto, tipo Olá palavra-passe desta conta.
      
6. No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar-se a aplicação de Netsuite tooyour.

7. No Olá **correio eletrónico de notificação** campo, introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro de aprovisionamento e marque Olá caixa de verificação.

8. Clique em **guardar.**

9. Na secção de mapeamentos Olá, selecione **tooNetsuite sincronizar utilizadores do Azure Active Directory.**

10. No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooNetsuite. Tenha em atenção que Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá contas de utilizador Netsuite para operações de atualização. Selecione Olá guardar botão toocommit quaisquer alterações.

11. tooenable Olá serviço aprovisionamento do Azure AD para Netsuite, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá secção de definições

12. Clique em **guardar.**

Iniciar sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooNetsuite no Olá utilizadores e a secção de grupos. Tenha em atenção que a sincronização inicial Olá demora mais tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução. Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento do serviço na sua aplicação Netsuite.

Agora, pode criar uma conta de teste. Aguarde pela cópia de segurança minutos too20 tooverify Olá conta foi sincronizada tooNetsuite.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerir o aprovisionamento da conta de utilizador para aplicações da empresa](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar o início de sessão único](active-directory-saas-netsuite-tutorial.md)