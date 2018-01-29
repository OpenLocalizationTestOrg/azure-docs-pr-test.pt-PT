---
title: "Tutorial: Integração do Azure Active Directory com Egnyte | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre o Azure Active Directory e Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 94c71859aff01b60cee1b49664ad62257f9f9f2a
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a>Tutorial: Integração do Azure Active Directory com Egnyte

Neste tutorial, irá aprender a integrar Egnyte com o Azure Active Directory (Azure AD).

Integrar Egnyte com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso ao Egnyte
- Pode permitir que os utilizadores automaticamente obter com sessão iniciada para Egnyte (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal do Azure

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com Egnyte, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Um Egnyte-início de sessão único ativada subscrição

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Egnyte a partir da Galeria
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-egnyte-from-the-gallery"></a>Adicionar Egnyte a partir da Galeria
Para configurar a integração de Egnyte com o Azure AD, terá de adicionar Egnyte a partir da Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar Egnyte a partir da galeria, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![Aplicações][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa, escreva **Egnyte**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. No painel de resultados, selecione **Egnyte**e, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Egnyte com base num utilizador de teste chamado "Britta Simon."

Para início de sessão trabalhar, do Azure AD tem de saber o que o utilizador homólogo no Egnyte é um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no Egnyte tem de ser estabelecida.

No Egnyte, atribua o valor do **nome de utilizador** no Azure AD como o valor a **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com Egnyte, tem de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Egnyte](#creating-an-egnyte-test-user)**  - para ter um homólogo de Britta Simon Egnyte que está ligada a representação do Azure AD do utilizador.
4. **[Atribuir o utilizador de teste do Azure AD](#assigning-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal do Azure e configurar o início de sessão único na sua aplicação Egnyte.

**Para configurar o Azure AD-início de sessão único com Egnyte, execute os seguintes passos:**

1. No portal do Azure, no **Egnyte** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. No **Egnyte domínio e os URLs** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    No **URL de início de sessão** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<companyname>.egnyte.com`

    > [!NOTE] 
    > Este valor não é real. Atualize este valor com o URL de início de sessão real. Contacte [equipa de suporte de cliente Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) para obter este valor. 
 
4. No **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. No **Egnyte configuração** secção, clique em **configurar Egnyte** para abrir **configurar início de sessão** janela. Copiar o **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** do **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa Egnyte como administrador.

8. Clique em **definições**.
   
   ![Definições](./media/active-directory-saas-egnyte-tutorial/ic787819.png "definições")

9. No menu, clique em **definições**.

   ![Definições](./media/active-directory-saas-egnyte-tutorial/ic787820.png "definições")

10. Clique em de **configuração** separador e, em seguida, clique em **segurança**.

    ![Segurança](./media/active-directory-saas-egnyte-tutorial/ic787821.png "segurança")

11. No **autenticação de início de sessão único** secção, execute os seguintes passos:

    ![Autenticação de início de sessão único](./media/active-directory-saas-egnyte-tutorial/ic787822.png "na autenticação de início de sessão único")   
    
    a. Como **autenticação de início de sessão único**, selecione **SAML 2.0**.
   
    b. Como **fornecedor de identidade**, selecione **AzureAD**.
   
    c. Colar **único início de sessão no URL do serviço SAML** copiados a partir do portal do Azure para o **URL de início de sessão do fornecedor de identidade** caixa de texto.
   
    d. Colar **ID de entidade de SAML** que copiou do portal do Azure para o **ID de entidade do fornecedor de identidade** caixa de texto.
      
    e. Abra o certificado codificado base-64 no bloco de notas transferido a partir do portal do Azure, copie o conteúdo do mesmo para a sua área de transferência e, em seguida, cole-os para o **certificado do fornecedor de identidade** caixa de texto.
   
    f. Como **predefinido mapeamento de utilizador**, selecione **endereço de correio eletrónico**.
   
    g. Como **utilizar valor específicas do domínio emissor**, selecione **desativada**.
   
    h. Clique em **Guardar**.

> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No **portal do Azure**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior da caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. No **utilizador** diálogo página, execute os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    a. No **nome** caixa de texto, tipo **BrittaSimon**.

    b. No **nome de utilizador** caixa de texto, tipo de **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor da **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-egnyte-test-user"></a>Criar um utilizador de teste Egnyte

Para permitir que os utilizadores do Azure AD iniciem sessão nos Egnyte, têm de ser aprovisionados para Egnyte. No caso de Egnyte, o aprovisionamento é uma tarefa manual.

**Aprovisionar contas de utilizador, execute os seguintes passos:**

1. Inicie sessão no seu **Egnyte** site da empresa como administrador.

2. Aceda a **definições \> utilizadores e grupos**.

3. Clique em **adicionar novo utilizador**e, em seguida, selecione o tipo de utilizador que pretende adicionar.
   
   ![Os utilizadores](./media/active-directory-saas-egnyte-tutorial/ic787824.png "utilizadores")

4. No **novo utilizador padrão** secção, execute os seguintes passos:
   
   ![Novo utilizador padrão](./media/active-directory-saas-egnyte-tutorial/ic787825.png "novo utilizador padrão")   

   a. Tipo de **E-Mail**, **Username**e outros detalhes de uma conta válida do Azure Active Directory que pretende aprovisionar.
   
   b. Clique em **Guardar**.
    
    >[!NOTE]
    >O marcador de posição de conta do Azure Active Directory irá receber um e-mail de notificação.
    >

>[!NOTE]
>Pode utilizar quaisquer outras Egnyte utilizador conta criação ferramentas ou APIs fornecidas pelo Egnyte para aprovisionar contas de utilizador do AAD.
> 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuir o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso para Egnyte.

![Atribua o utilizador][200] 

**Para atribuir Britta Simon a Egnyte, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **Egnyte**.

    ![Configurar o início de sessão único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão através do painel de acesso.

Quando clica no mosaico Egnyte no painel de acesso, deve obter automaticamente com sessão iniciada para a aplicação de Egnyte.
Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

