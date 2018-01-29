---
title: "Tutorial: Integração do Azure Active Directory com Suite adaptável | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre o Azure Active Directory e adaptável Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 8e128ddf53a93fe30350d8e914657f3539701603
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a>Tutorial: Integração do Azure Active Directory com Suite adaptável

Neste tutorial, irá aprender a integrar Suite adaptável com o Azure Active Directory (Azure AD).

Integrar Suite adaptável com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso ao adaptável Suite
- Pode permitir que os utilizadores automaticamente obter com sessão iniciada para Suite adaptável (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal do Azure

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com Suite adaptável, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Um conjunto adaptável início de sessão único subscrição ativado

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição de Suite adaptável de galeria
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-adaptive-suite-from-the-gallery"></a>A adição de Suite adaptável de galeria
Para configurar a integração do Suite adaptável com o Azure AD, tem de adicionar Suite adaptável na Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar Suite adaptável a partir da galeria, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![Aplicações][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa, escreva **Suite adaptável**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. No painel de resultados, selecione **Suite adaptável**e, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Suite adaptável com base num utilizador de teste chamado "Britta Simon."

Para início de sessão trabalhar, do Azure AD tem de saber o que o utilizador homólogo no Suite adaptável é um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no Suite adaptável tem de ser estabelecida.

No adaptável Suite, atribua o valor do **nome de utilizador** no Azure AD como o valor a **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com Suite adaptável, terá de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Suite adaptável](#creating-an-adaptive-suite-test-user)**  - para ter um homólogo de Britta Simon Suite adaptável que está ligada a representação do Azure AD do utilizador.
4. **[Atribuir o utilizador de teste do Azure AD](#assigning-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal do Azure e configurar o início de sessão único na sua aplicação adaptável Suite.

**Para configurar o Azure AD-início de sessão único com Suite adaptável, execute os seguintes passos:**

1. No portal do Azure, no **Suite adaptável** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. No **adaptável de conjunto de domínios e URLs** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    No **URL de resposta** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`

    >[!NOTE]
    > Pode obter este valor a partir do Suite adaptável **SAML SSO definições** página.
    >  

4. No **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. No **adaptável Suite configuração** secção, clique em **configurar adaptável Suite** para abrir **configurar início de sessão** janela. Copiar o **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** do **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa Suite adaptável como administrador.

8. Aceda a **Admin**.
   
    ![Administração](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")

9. No **utilizadores e funções** secção, clique em **gerir as definições de SAML SSO**.
   
    ![Gerir definições de SAML SSO](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "gerir definições de SAML SSO")

10. No **SAML SSO definições** página, execute os seguintes passos:
   
    ![Definições de SAML SSO](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO definições")

    a. No **nome do fornecedor de identidade** caixa de texto, escreva um nome para a sua configuração.
    
    b. Colar o **ID de entidade de SAML** valor copiados a partir do portal do Azure para o **fornecedor de identidade ID de entidade** caixa de texto.
  
    c. Colar o **único início de sessão no URL do serviço SAML** valor copiados a partir do portal do Azure para o **fornecedor de identidade SSO URL** caixa de texto.
  
    d. Colar o **único início de sessão no URL do serviço SAML** valor copiados a partir do portal do Azure para o **URL de fim de sessão personalizada** caixa de texto.
  
    e. Para carregar o certificado transferido, clique em **Escolher ficheiro**.
  
    f. Selecione o seguinte, para:
    * **Id de utilizador SAML**, selecione **nome de utilizador do utilizador Insights adaptável**.
    * **Localização do id de utilizador SAML**, selecione **id de utilizador no NameID do requerente**.
    * **Formato de SAML NameID**, selecione **endereço de correio eletrónico**.
    * **Ativar SAML**, selecione **permitir SAML SSO e início de sessão direto Insights adaptável**.
    
    g. Clique em **Guardar**.

> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No **portal do Azure**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior da caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. No **utilizador** diálogo página, execute os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    a. No **nome** caixa de texto, tipo **BrittaSimon**.

    b. No **nome de utilizador** caixa de texto, tipo de **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor da **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-adaptive-suite-test-user"></a>Criar um utilizador de teste adaptável Suite

Para permitir que os utilizadores do Azure AD iniciem sessão nos Suite adaptável, têm de ser aprovisionados para adaptável Suite.  

* No caso de Suite adaptável, o aprovisionamento é uma tarefa manual.

**Para configurar o aprovisionamento de utilizadores, execute os seguintes passos:** 

1. Inicie sessão no seu **Suite adaptável** site da empresa como administrador.
2. Aceda a **Admin**.
   
   ![Administração](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")
3. No **utilizadores e funções** secção, clique em **adicionar utilizador**.
   
   ![Adicionar utilizador](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "adicionar utilizador")
4. No **novo utilizador** secção, execute os seguintes passos:
   
   ![Submeter](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "submeter")   

   a. Tipo de **nome**, **início de sessão**, **E-Mail**, **palavra-passe** de um utilizador válido do Azure Active Directory que pretende aprovisionar num relacionados caixas de texto.
  
   b. Selecione um **função**.
  
   c. Clique em **submeter**.

>[!NOTE]
>Pode utilizar quaisquer outras Suite adaptável utilizador conta criação ferramentas ou APIs fornecidas pelo adaptável Suite para aprovisionar contas de utilizador do AAD.
>  

### <a name="assigning-the-azure-ad-test-user"></a>Atribuir o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso para adaptável Suite.

![Atribua o utilizador][200] 

**Para atribuir Britta Simon a Suite adaptável, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **Suite adaptável**.

    ![Configurar o início de sessão único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

O objetivo desta secção consiste em testar a Microsoft Azure AD Single Sign-On configuração utilizando o painel de acesso.

Quando clica no mosaico Suite adaptável no painel de acesso, deve obter automaticamente com sessão iniciada para a aplicação de Suite adaptável.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

