---
title: "Tutorial: Integração do Azure Active Directory a área de trabalho por Facebook | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e à área de trabalho por Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Tutorial: Configurar à área de trabalho ao Facebook para aprovisionamento de utilizadores

o objetivo deste tutorial Olá é tooshow Olá passos que precisa de tooperform na área de trabalho por Facebook e o Azure AD tooautomatically aprovisionar e desativação de aprovisionar contas de utilizador do Azure AD tooWorkplace por Facebook.

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD a área de trabalho por Facebook tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Uma área de trabalho por Facebook início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-tooworkplace-by-facebook"></a>Atribuir utilizadores tooWorkplace por Facebook

Azure Active Directory utiliza um conceito chamado toodetermine "atribuições" os utilizadores que devem receber acesso tooselected aplicações. No contexto de Olá de aprovisionamento da conta de utilizador automáticas, apenas Olá utilizadores e grupos que tenham sido "atribuídos" tooan aplicação no Azure AD é sincronizado.

Antes de configurar e ativar o serviço de fornecimento de Olá, terá de toodecide que os utilizadores e/ou grupos no Azure AD representam Olá utilizadores precisam de aceder à área de trabalho de tooyour pela aplicação do Facebook. Depois de decidir, pode atribuir estes tooyour de utilizadores à área de trabalho através da aplicação do Facebook, seguindo as instruções de Olá aqui:

[Atribuir um utilizador ou grupo tooan de aplicações](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>Sugestões importantes para atribuir utilizadores tooWorkplace por Facebook

*   Recomenda-se que um único utilizador do Azure AD é atribuído tooWorkplace pelo Facebook tootest Olá aprovisionamento de configuração. Os utilizadores adicionais e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um tooWorkplace de utilizador, Facebook, tem de selecionar uma função de utilizador válido. função de "Acesso predefinida" Olá não funciona para o aprovisionamento.

## <a name="enable-user-provisioning"></a>Ativar o aprovisionamento de utilizador

Esta secção orienta-o ao ligar o tooWorkplace do Azure AD através da API de aprovisionamento da conta de utilizador do Facebook e configurar Olá aprovisionamento toocreate de serviço, atualizar e desativar as contas de utilizador atribuído na área de trabalho por Facebook com base no utilizador e grupo atribuição no Azure AD.

>[!Tip]
>Pode também optar por tooenabled baseados em SAML Single Sign-On para a área de trabalho, Facebook, seguindo as instruções de Olá fornecidas no [portal do Azure](https://portal.azure.com). O início de sessão único a pode ser configurado independentemente aprovisionamento automático, apesar destas duas funcionalidades complementar dos entre si.

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>conta de utilizador tooconfigure aprovisionamento tooWorkplace por Facebook no Azure AD:

o objetivo desta secção Olá é toooutline como tooenable aprovisionamento de utilizador do Active Directory contas tooWorkplace por Facebook.

Azure suporta de AD Olá capacidade tooautomatically sincronizar detalhes da conta de Olá atribuído tooWorkplace de utilizadores por Facebook. Esta sincronização automática permite à área de trabalho por necessita que os utilizadores tooauthorize de acesso, antes de dados do Facebook tooget Olá-las de tentar toosign para Olá pela primeira vez. É também anular Aprovisiona os utilizadores da área de trabalho por Facebook quando foi revogado acesso no Azure AD.

1. No Olá [portal do Azure](https://portal.azure.com), procurar toohello **do Azure Active Directory** > **aplicações da empresa** > **todas as aplicações** secção.

2. Se já tiver configurado a área de trabalho ao Facebook para o início de sessão único, procure a instância da área de trabalho por Facebook utilizando o campo de procura Olá. Caso contrário, selecione **adicionar** e procure **à área de trabalho por Facebook** na Galeria de aplicações de Olá. Selecione a área de trabalho por Facebook os resultados da pesquisa Olá e adicioná-lo tooyour lista de aplicações.

3. Selecione a instância da área de trabalho, Facebook, em seguida, selecione Olá **aprovisionamento** separador.

4. Conjunto Olá **modo de aprovisionamento** demasiado**automática**. 

    ![Aprovisionamento](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** secção, introduza Olá segredo Token e Olá URL de inquilino da sua área de trabalho pelo administrador do Facebook.

6. No portal do Azure Olá, clique em **Testar ligação** tooensure do Azure AD pode ligar-se à área de trabalho de tooyour pela aplicação do Facebook. Se falhar a ligação de Olá, certifique-se à sua área de trabalho pela conta do Facebook permissões de administração de equipa.

7. Introduza o endereço de correio eletrónico Olá de uma pessoa ou grupo que deve receber notificações de erro aprovisionamento no Olá **correio eletrónico de notificação** campo e marque Olá caixa de verificação.

8. Clique em **guardar.**

9. Na secção de mapeamentos Olá, selecione **tooWorkplace sincronizar utilizadores do Azure Active Directory, Facebook.**

10. No Olá **mapeamentos de atributos** secção, reveja os atributos de utilizador de Olá são sincronizados a partir do Azure AD tooWorkplace por Facebook. Olá atributos selecionados como **correspondência** propriedades são utilizadas toomatch Olá as contas de utilizador na área de trabalho ao Facebook para operações de atualização. Selecione Olá guardar botão toocommit quaisquer alterações.

11. tooenable Olá serviço aprovisionamento do Azure AD para a área de trabalho, Facebook, alteração Olá **estado de aprovisionamento** demasiado**no** no Olá **definições** secção

12. Clique em **guardar.**

Para obter mais informações sobre como tooconfigure automática de aprovisionamento, consulte [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

Agora, pode criar uma conta de teste. Aguarde pela cópia de segurança minutos too20 tooverify Olá conta foi sincronizada tooWorkplace por Facebook.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerir o aprovisionamento da conta de utilizador para aplicações da empresa](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar o início de sessão único](active-directory-saas-workplacebyfacebook-tutorial.md)

