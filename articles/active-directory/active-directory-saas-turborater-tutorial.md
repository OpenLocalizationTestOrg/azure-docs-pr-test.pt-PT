---
title: "Tutorial: Integração do Azure Active Directory com TurboRater | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre o Azure Active Directory e TurboRater."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: abb116b8-8024-4cc6-bc81-f32ef490ea17
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2017
ms.author: jeedes
ms.openlocfilehash: 82d9ee4768507bfcc554bbd18a2588f315180e82
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-turborater"></a>Tutorial: Integração do Azure Active Directory com TurboRater

Neste tutorial, irá aprender a integrar TurboRater com o Azure Active Directory (Azure AD).

Integrar TurboRater com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso ao TurboRater.
- Pode permitir que os utilizadores automaticamente obter com sessão iniciada para TurboRater (Single Sign-On) com as respetivas contas do Azure AD.
- Pode gerir as contas numa localização central - portal do Azure.

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com TurboRater, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Um TurboRater-início de sessão único ativada subscrição

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar TurboRater a partir da Galeria
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-turborater-from-the-gallery"></a>Adicionar TurboRater a partir da Galeria
Para configurar a integração de TurboRater com o Azure AD, terá de adicionar TurboRater a partir da Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar TurboRater a partir da galeria, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![O botão do Azure Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![O painel de aplicações da empresa][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![O novo botão de aplicação][3]

4. Na caixa de pesquisa, escreva **TurboRater**, selecione **TurboRater** partir do painel de resultados, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![TurboRater na lista de resultados](./media/active-directory-saas-turborater-tutorial/tutorial_turborater_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único

Nesta secção, configure e teste do Azure AD-início de sessão único com TurboRater com base num utilizador de teste chamado "Britta Simon".

Para início de sessão trabalhar, do Azure AD tem de saber o que o utilizador homólogo no TurboRater é um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no TurboRater tem de ser estabelecida.

No TurboRater, atribua o valor do **nome de utilizador** no Azure AD como o valor a **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com TurboRater, tem de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste TurboRater](#create-a-turborater-test-user)**  - para ter um homólogo de Britta Simon TurboRater que está ligada a representação do Azure AD do utilizador.
4. **[Atribua o utilizador de teste do Azure AD](#assign-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal do Azure e configurar o início de sessão único na sua aplicação TurboRater.

**Para configurar o Azure AD-início de sessão único com TurboRater, execute os seguintes passos:**

1. No portal do Azure, no **TurboRater** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar a ligação de início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-turborater-tutorial/tutorial_turborater_samlbase.png)

3. No **TurboRater domínio e os URLs** secção, execute os seguintes passos:

    ![Domínio TurboRater e os URLs únicos de informações de início de sessão](./media/active-directory-saas-turborater-tutorial/tutorial_turborater_url.png)

    a. No **identificador** caixa de texto, digite o valor como:`https://www.itcdataservices.com`
 
    b. No **URL de resposta** caixa de texto, digite o valor como:
    
    | Ambiente | URL |
    | ---------------| --------------- |    
    | Teste  | `https://ratingqa.itcdataservices.com/webservices/imp/saml/login` |
    | Em direto  | `https://www.itcratingservices.com/webservices/imp/saml/login` |

4. No **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados no seu computador.

    ![A hiperligação de transferência do certificado](./media/active-directory-saas-turborater-tutorial/tutorial_turborater_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-turborater-tutorial/tutorial_general_400.png)

7. Para configurar o início de sessão único em **TurboRater** lado, terá de enviar o transferido **XML de metadados** para [equipa de suporte de TurboRater](https://www.getitc.com/support). Se definir esta definição para que a ligação de SAML SSO corretamente em ambos os lados.

> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

   ![Criar um utilizador de teste do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No portal do Azure, no painel esquerdo, clique em de **do Azure Active Directory** botão.

    ![O botão do Azure Active Directory](./media/active-directory-saas-turborater-tutorial/create_aaduser_01.png)

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.

    !["Os utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-turborater-tutorial/create_aaduser_02.png)

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior do **todos os utilizadores** caixa de diálogo.

    ![O botão de adição](./media/active-directory-saas-turborater-tutorial/create_aaduser_03.png)

4. No **utilizador** diálogo caixa, execute os seguintes passos:

    ![A caixa de diálogo de utilizador](./media/active-directory-saas-turborater-tutorial/create_aaduser_04.png)

    a. No **nome** caixa, escreva **BrittaSimon**.

    b. No **nome de utilizador** caixa, escreva o endereço de e-mail do utilizador Britta Simon.

    c. Selecione o **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor que é apresentado no **palavra-passe** caixa.

    d. Clique em **Criar**.
  
### <a name="create-a-turborater-test-user"></a>Criar um utilizador de teste TurboRater

Para permitir que os utilizadores do Azure AD iniciem sessão nos TurboRater, têm de ser aprovisionados para TurboRater.  
No caso de TurboRater, o aprovisionamento é uma tarefa manual.
Para criar um utilizador,. trabalhar com [equipa de suporte de TurboRater](https://www.getitc.com/support).

### <a name="assign-the-azure-ad-test-user"></a>Atribua o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso para TurboRater.

![Atribuir a função de utilizador][200] 

**Para atribuir Britta Simon a TurboRater, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **TurboRater**.

    ![A ligação de TurboRater na lista de aplicações](./media/active-directory-saas-turborater-tutorial/tutorial_turborater_app.png)  

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![A ligação de "Utilizadores e grupos"][202]

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar atribuição][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão através do painel de acesso.

Quando clica no mosaico TurboRater no painel de acesso, deve obter automaticamente com sessão iniciada para a aplicação de TurboRater.
Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-turborater-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-turborater-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-turborater-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-turborater-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-turborater-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-turborater-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-turborater-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-turborater-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-turborater-tutorial/tutorial_general_203.png

