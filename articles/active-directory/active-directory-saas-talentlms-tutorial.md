---
title: "Tutorial: Integração do Azure Active Directory com TalentLMS | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre o Azure Active Directory e TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 171457617c23f2c0ff761f7ae1e78dcf152cd0b3
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a>Tutorial: Integração do Azure Active Directory com TalentLMS

Neste tutorial, irá aprender a integrar TalentLMS com o Azure Active Directory (Azure AD).

Integrar TalentLMS com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso ao TalentLMS
- Pode permitir que os utilizadores automaticamente obter com sessão iniciada para TalentLMS (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal do Azure

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com TalentLMS, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Um TalentLMS-início de sessão único ativada subscrição

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar TalentLMS a partir da Galeria
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-talentlms-from-the-gallery"></a>Adicionar TalentLMS a partir da Galeria
Para configurar a integração de TalentLMS com o Azure AD, terá de adicionar TalentLMS a partir da Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar TalentLMS a partir da galeria, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![Aplicações][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa, escreva **TalentLMS**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. No painel de resultados, selecione **TalentLMS**e, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com TalentLMS com base num utilizador de teste chamado "Britta Simon."

Para início de sessão trabalhar, do Azure AD tem de saber o que o utilizador homólogo no TalentLMS é um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no TalentLMS tem de ser estabelecida.

No TalentLMS, atribua o valor do **nome de utilizador** no Azure AD como o valor a **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com TalentLMS, tem de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste TalentLMS](#creating-a-talentlms-test-user)**  - para ter um homólogo de Britta Simon TalentLMS que está ligada a representação do Azure AD do utilizador.
4. **[Atribuir o utilizador de teste do Azure AD](#assigning-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal do Azure e configurar o início de sessão único na sua aplicação TalentLMS.

**Para configurar o Azure AD-início de sessão único com TalentLMS, execute os seguintes passos:**

1. No portal do Azure, no **TalentLMS** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. No **TalentLMS domínio e os URLs** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    a. No **URL de início de sessão** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<tenant-name>.TalentLMSapp.com`

    b. No **identificador** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`http://<tenant-name>.talentlms.com`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o URL de início de sessão e o identificador real. Contacte [equipa de suporte de cliente TalentLMS](https://www.talentlms.com/contact) para obter estes valores. 
 
4. No **certificado de assinatura de SAML** secção, copie o **THUMBPRINT** valor do certificado.

    ![Configurar o início de sessão único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. No **TalentLMS configuração** secção, clique em **configurar TalentLMS** para abrir **configurar início de sessão** janela. Copiar o **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** do **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa TalentLMS como administrador.

8. No **definições de conta de &** secção, clique em de **utilizadores** separador.
   
    ![Definições de conta de &](./media/active-directory-saas-talentlms-tutorial/IC777296.png "definições de conta de &")

9. Clique em **Single Sign-On (SSO)**,

10. Na secção de Single Sign-On, execute os seguintes passos:
   
    ![De sessão único-](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")   

    a. Do **tipo de integração do SSO** lista, selecione **SAML 2.0**.

    b. No **fornecedor de identidade (IDP)** caixa de texto, cole o valor de **ID de entidade de SAML**, que copiou do portal do Azure.
 
    c. Colar o **Thumbprint** valor a partir do portal do Azure para o **impressão digital do certificado** caixa de texto.    

    d.  No **URL de início de sessão remoto** caixa de texto, cole o valor de **único início de sessão no URL do serviço SAML**, que copiou do portal do Azure.
 
    e. No **URL de início de sessão remoto** caixa de texto, cole o valor de **Sign-Out URL**, que copiou do portal do Azure.

    f. Preencha o seguinte: 

    * No **TargetedID** caixa de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`
     
    * No **nome próprio** caixa de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`
    
    * No **Apelido** caixa de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`
    
    * No **E-Mail** caixa de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`
    
11. Clique em **Guardar**.
 
> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No **portal do Azure**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior da caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. No **utilizador** diálogo página, execute os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    a. No **nome** caixa de texto, tipo **BrittaSimon**.

    b. No **nome de utilizador** caixa de texto, tipo de **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor da **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-talentlms-test-user"></a>Criar um utilizador de teste TalentLMS

Para permitir que os utilizadores do Azure AD iniciem sessão nos TalentLMS, têm de ser aprovisionados para TalentLMS. No caso de TalentLMS, o aprovisionamento é uma tarefa manual.

**Para Aprovisionar uma conta de utilizador, execute os seguintes passos:**

1. Inicie sessão no seu **TalentLMS** inquilino.

2. Clique em **utilizadores**e, em seguida, clique em **adicionar utilizador**.

3. No **adicionar utilizador** diálogo página, execute os seguintes passos:
   
    ![Adicionar utilizador](./media/active-directory-saas-talentlms-tutorial/IC777299.png "adicionar utilizador")  

    a. No **nome próprio** caixa de texto, introduza o nome de utilizador como **Britta**.

    b. No **Apelido** caixa de texto, introduza o apelido do utilizador, como **Simon**.
 
    c. No **endereço de correio eletrónico** caixa de texto, introduza o e-mail do utilizador, como  **brittasimon@contoso.com** .

    d. Clique em **adicionar utilizador**.

>[!NOTE]
>Pode utilizar quaisquer outras TalentLMS utilizador conta criação ferramentas ou APIs fornecidas pelo TalentLMS para aprovisionar contas de utilizador do AAD.
 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuir o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso para TalentLMS.

![Atribua o utilizador][200] 

**Para atribuir Britta Simon a TalentLMS, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **TalentLMS**.

    ![Configurar o início de sessão único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

O objetivo desta secção consiste em testar a configuração do Azure AD único início de sessão através do painel de acesso.

Quando clica no mosaico TalentLMS no painel de acesso, deve obter automaticamente com sessão iniciada para a aplicação de TalentLMS

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

