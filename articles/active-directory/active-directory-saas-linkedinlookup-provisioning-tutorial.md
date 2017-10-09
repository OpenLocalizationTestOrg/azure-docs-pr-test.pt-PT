---
title: "Tutorial: Configurar LinkedIn pesquisa para o aprovisionamento de utilizadores automática no Azure Active Directory | Microsoft Docs"
description: "Saiba como tooconfigure do Azure Active Directory tooautomatically aprovisionar e aprovisionar desativação do utilizador contas tooLinkedIn pesquisa."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3e41abb8af00715f70e5a14d9d26ff600c10f492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a>Tutorial: Configurar LinkedIn pesquisa para o aprovisionamento de utilizadores automática


o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform na pesquisa do LinkedIn e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooLinkedIn pesquisa. 

## <a name="prerequisites"></a>Pré-requisitos

cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:

*   Um inquilino do Azure Active Directory
*   Um inquilino LinkedIn pesquisa 
*   Uma conta de administrador na pesquisa do LinkedIn com acesso toohello LinkedIn do Centro de contas

> [!NOTE]
> Azure Active Directory se integra com pesquisa de LinkedIn com Olá [SCIM](http://www.simplecloud.info/) protocolo.

## <a name="assigning-users-toolinkedin-lookup"></a>Atribuir utilizadores tooLinkedIn pesquisa

Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações. No contexto de Olá de aprovisionamento da conta de utilizador automáticas, serão sincronizados apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD. 

Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos no Azure AD representam Olá utilizadores precisam de aceder tooLinkedIn pesquisa. Depois de decidir, pode atribuir tooLinkedIn estes utilizadores pesquisa ao seguir as instruções de Olá aqui:

[Atribuir um utilizador ou grupo tooan de aplicações](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-lookup"></a>Sugestões importantes para atribuir utilizadores tooLinkedIn pesquisa

*   Recomenda-se que um único utilizador do Azure AD ser atribuídos Olá tootest pesquisa de tooLinkedIn aprovisionamento de configuração. Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir uma pesquisa de tooLinkedIn do utilizador, tem de selecionar Olá **utilizador** função na caixa de diálogo de atribuição de Olá. função de "Acesso predefinida" Olá não funciona para o aprovisionamento.


## <a name="configuring-user-provisioning-toolinkedin-lookup"></a>Configurar tooLinkedIn pesquisa de aprovisionamento de utilizadores

Esta secção orienta-o ligar a conta de utilizador do seu Azure AD tooLinkedIn pesquisa SCIM aprovisionamento API e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar o utilizador atribuído contas no LinkedIn pesquisa com base no utilizador e grupo atribuição no Azure AD.

> [!TIP]
> Pode também optar por tooenabled baseados em SAML Single Sign-On para a pesquisa de LinkedIn, seguindo as instruções de Olá fornecidas [portal do Azure](https://portal.azure.com). O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementam entre si.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-lookup-in-azure-ad"></a>conta de utilizador automáticas tooconfigure aprovisionamento tooLinkedIn pesquisa no Azure AD:


primeiro passo de Olá é tooretrieve seu token de acesso LinkedIn. Se for um administrador de empresa, pode aprovisionar um token de acesso. No seu centro de contas, aceda demasiado**definições &gt; definições globais** e abra Olá **SCIM configuração** painel.

> [!NOTE]
> Se está a aceder ao centro de contas de Olá diretamente em vez de através de uma ligação, pode chegá-la utilizando Olá os seguintes passos.

1)  Inicie sessão no Centro de tooAccount.

2)  Selecione **Admin &gt; definições de administrador** .

3)  Clique em **avançadas integrações** na barra lateral esquerdo de Olá. São direcionados toohello do Centro de contas.

4)  Clique em **+ Adicionar nova configuração de SCIM** e siga o procedimento de Olá preenchendo em cada campo.

> Quando autoassign licenças não estiver ativada, significa que apenas os dados de utilizador estão sincronizados.

![Pesquisa de LinkedIn aprovisionamento](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> Quando a atribuição de autolicense estiver ativada, terá de toonote a instância da aplicação e tipo de licença. São atribuídas as licenças num provenientes do primeiro, primeiro servir base até que todas as licenças de Olá são executadas.

![Pesquisa de LinkedIn aprovisionamento](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  Clique em **gerar token**. Deverá ver o seu ecrã de token de acesso em Olá **token de acesso** campo.

6)  Guarde a sua área de transferência de token tooyour de acesso ou o computador antes de deixarem a página Olá.

7) Em seguida, inicie sessão no toohello [portal do Azure](https://portal.azure.com)e procure toohello **do Azure Active Directory > aplicações da empresa > todas as aplicações** secção.

8) Se já tiver configurado o LinkedIn pesquisa para o início de sessão único, procure a instância de pesquisa de LinkedIn com o campo de procura Olá. Caso contrário, selecione **adicionar** e procure **LinkedIn pesquisa** na Galeria de aplicações de Olá. Selecione LinkedIn pesquisa de resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.

9)  Selecione a sua instância do LinkedIn pesquisa, em seguida, selecione Olá **aprovisionamento** separador.

10) Conjunto Olá **modo de aprovisionamento** demasiado**automática**.

![Pesquisa de LinkedIn aprovisionamento](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  Preencha Olá seguintes campos em **credenciais de administrador** :

* No Olá **URL de inquilino** campo, introduza https://api.linkedin.com.

* No Olá **segredo Token** campo, introduza o token de acesso de Olá gerados no passo 1 e clique em **Testar ligação** .

* Deverá ver uma notificação de sucesso no lado de upperright Olá do seu portal.

12) Introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro aprovisionamento no Olá **correio eletrónico de notificação** campo e marque Olá caixa de verificação abaixo.

13) Clique em **Guardar**. 

14) No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador e grupo Olá que serão sincronizados a partir do Azure AD tooLinkedIn pesquisa. Tenha em atenção que Olá atributos selecionados como **correspondência** propriedades será toomatch utilizadas contas de utilizador de Olá e grupos na pesquisa do LinkedIn para operações de atualização. Selecione Olá guardar botão toocommit quaisquer alterações.

![Pesquisa de LinkedIn aprovisionamento](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) tooenable Olá serviço aprovisionamento do Azure AD para a pesquisa de LinkedIn, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá **definições** secção

16) Clique em **Guardar**. 

Isto iniciará a sincronização inicial de Olá de todos os utilizadores e/ou grupos atribuídos tooLinkedIn procura na secção de utilizadores e grupos de Olá. Tenha em atenção que a sincronização inicial Olá irá demorar mais longo tooperform que sincronizações subsequentes, o que ocorrer aproximadamente a cada 20 minutos, desde que o serviço de Olá está em execução. Pode utilizar Olá **detalhes de sincronização** secção toomonitor progresso e siga as ligações tooprovisioning atividade relatórios que descrevem a todas as ações efetuadas pelo Olá aprovisionamento do serviço na sua aplicação de pesquisa de LinkedIn.


## <a name="additional-resources"></a>Recursos Adicionais

* [Gerir o aprovisionamento da conta de utilizador para aplicações da empresa](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
