---
title: "Tutorial: Integração do Azure Active Directory com Rightscale | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre Rightscale e o Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 62c95d798e851ddf6030714a052afb32b977b7e3
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a>Tutorial: Integração do Azure Active Directory com Rightscale

Neste tutorial, irá aprender a integrar Rightscale com o Azure Active Directory (Azure AD).

Integrar Rightscale com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso ao Rightscale
- Pode permitir que os utilizadores automaticamente obter com sessão iniciada para Rightscale (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal do Azure

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com Rightscale, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Um Rightscale-início de sessão único ativada subscrição

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Rightscale a partir da Galeria
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-rightscale-from-the-gallery"></a>Adicionar Rightscale a partir da Galeria
Para configurar a integração de Rightscale com o Azure AD, terá de adicionar Rightscale a partir da Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar Rightscale a partir da galeria, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![Aplicações][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa, escreva **Rightscale**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. No painel de resultados, selecione **Rightscale**e, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Rightscale com base num utilizador de teste chamado "Britta Simon".

Para início de sessão trabalhar, do Azure AD tem de saber o que o utilizador homólogo no Rightscale é um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no Rightscale tem de ser estabelecida.

No Rightscale, atribua o valor do **nome de utilizador** no Azure AD como o valor a **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com Rightscale, tem de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Rightscale](#creating-a-rightscale-test-user)**  - para ter um homólogo de Britta Simon Rightscale que está ligada a representação do Azure AD do utilizador.
4. **[Atribuir o utilizador de teste do Azure AD](#assigning-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal do Azure e configurar o início de sessão único na sua aplicação Rightscale.

**Para configurar o Azure AD-início de sessão único com Rightscale, execute os seguintes passos:**

1. No portal do Azure, no **Rightscale** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. No **domínio Rightscale e URLs** secção, se pretender configurar a aplicação no **IDP iniciada modo** não terá de efetuar quaisquer passos, tal como a aplicação já está previamente integrada com o Azure.

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. No **domínio Rightscale e URLs** secção, se pretender configurar a aplicação no **SP iniciada modo**, execute os seguintes passos:
    
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    a. Clique em de **Mostrar avançadas definições de URL**.

    b. No **URL de início de sessão** caixa de texto, escreva o URL:`https://login.rightscale.com/`

5. No **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. No **Rightscale configuração** secção, clique em **configurar Rightscale** para abrir **configurar início de sessão** janela. Copiar o **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** do **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS>
8. Para obter SSO configurado para a sua aplicação, terá de iniciar sessão no seu inquilino RightScale como administrador.

    a. No menu na parte superior, clique em de **definições** separador e selecione **Single Sign-On**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    b. Clique em de "**novo**" botão Adicionar **fornecedores de identidade do seu SAML**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    c. Na caixa de texto de **nome a apresentar**, introduza o nome da sua empresa.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    d. Selecione **SSO iniciado por permitir RightScale utilizando uma sugestão de deteção** e entrada sua **nome de domínio** na abaixo da caixa de texto.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    e. Colar o valor de **único início de sessão no URL do serviço SAML** que copiou do portal do Azure para **SAML SSO Endpoint** no RightScale.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    f. Colar o valor de **ID de entidade de SAML** que copiou do portal do Azure para **SAML EntityID** no RightScale.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    g. Clique em **Browser** botão para carregar o certificado que transferiu a partir do portal do Azure.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    h. Clique em **Guardar**.
<CE>
> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No **portal do Azure**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior da caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. No **utilizador** diálogo página, execute os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    a. No **nome** caixa de texto, tipo **BrittaSimon**.

    b. No **nome de utilizador** caixa de texto, tipo de **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor da **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-rightscale-test-user"></a>Criar um utilizador de teste Rightscale

Nesta secção, vai criar um utilizador chamado Britta Simon RightScale. Trabalhar com [equipa de suporte de cliente Rightscale](mailto:support@rightscale.com) para adicionar os utilizadores na plataforma RightScale.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuir o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso para Rightscale.

![Atribua o utilizador][200] 

**Para atribuir Britta Simon a Rightscale, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **Rightscale**.

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

O objetivo desta secção consiste em testar a configuração de SSO do Azure AD através do painel de acesso.  

Quando clica no mosaico RightScale no painel de acesso, deve obter automaticamente com sessão iniciada para a aplicação de RightScale.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

