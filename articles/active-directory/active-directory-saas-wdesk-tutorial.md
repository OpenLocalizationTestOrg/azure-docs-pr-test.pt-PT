---
title: "Tutorial: Integração do Azure Active Directory com Wdesk | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a>Tutorial: Integração do Azure Active Directory com Wdesk

Neste tutorial, saiba como toointegrate Wdesk com o Azure Active Directory (Azure AD).

Integrar Wdesk com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooWdesk
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooWdesk (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender que tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo. [O que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Wdesk tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Wdesk início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Wdesk da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-wdesk-from-hello-gallery"></a>Adicionar Wdesk da Galeria de Olá
tooconfigure Olá integração de Wdesk com o Azure AD, é necessário tooadd Wdesk Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Wdesk da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Wdesk**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. No painel de resultados de Olá, selecione **Wdesk**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Wdesk com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Wdesk é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Wdesk tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Wdesk.

tooconfigure e teste do Azure AD-início de sessão único com Wdesk, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Wdesk](#creating-a-wdesk-test-user)**  -toohave um homólogo de Britta Simon no Wdesk é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Wdesk.

**tooconfigure do Azure AD-início de sessão único com Wdesk, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Wdesk** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. No Olá **Wdesk domínio e os URLs** secção, se desejar aplicação Olá tooconfigure **IDP** modo iniciado efetuar Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`

4. Verifique **Mostrar avançadas definições de URL**. Se desejar aplicação Olá tooconfigure **SP** iniciada modo, efetuar Olá passo a seguir:

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`
     
    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão. Pode obter estes valores do portal de WDesk quando configurar Olá SSO. 
  
5. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. Numa janela do browser web diferente, tooWdesk de início de sessão como um administrador de segurança.

8. No Olá parte inferior esquerda, clique em **Admin** e escolha **administrador da conta**:
 
     ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. No Wdesk administrador, navegue demasiado**segurança**, em seguida, **SAML** > **SAML definições**:

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. Em **definições gerais**, verifique Olá **ativar SAML início de sessão único**:

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. Em **os detalhes do fornecedor de serviço**, efetuar Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      a. Olá cópia **URL de início de sessão** e cole-a no **Url de início de sessão** caixa de texto no portal do Azure.
   
      b. Olá cópia **Url de metadados** e cole-a no **identificador** caixa de texto no portal do Azure.
       
      c. Olá cópia **url de consumidor** e cole-a no **Url de resposta** caixa de texto no portal do Azure.
   
      d. Clique em **guardar** nas alterações de Olá toosave portal do Azure.      

12. Clique em **configurar definições de IdP** tooopen **editar definições de IdP** caixa de diálogo. Clique em **Escolher ficheiro** toolocate Olá **Metadata.xml** ficheiro guardado no portal do Azure, em seguida, carregue-o.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. Clique em **guardar alterações**.

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-wdesk-test-user"></a>Criar um utilizador de teste Wdesk

tooenable do Azure AD os utilizadores toolog no tooWdesk, estes têm de ser aprovisionados para Wdesk. No Wdesk, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooWdesk como um administrador de segurança.
2. Navegue demasiado**Admin** > **administrador da conta**.

     ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. Clique em **membros** em **pessoas**.

4. Agora, clique em **Add Member** tooopen **Add Member** caixa de diálogo. 
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. No **utilizador** texto, introduza o nome de utilizador de Olá do utilizador, como  **brittasimon@contoso.com**  e clique em **continuar** botão.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  Introduza os detalhes de Olá, conforme mostrado abaixo:
  
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    a. No **correio electrónico** texto, introduza o e-mail de Olá do utilizador, como  **brittasimon@contoso.com** .

    b. No **nome próprio** texto, introduza Olá primeiro nome de utilizador como **Britta**.

    c. No **Apelido** texto, introduza o apelido Olá do utilizador, como **Simon**.

7. Clique em **guardar membro** botão.  

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooWdesk.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooWdesk, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Wdesk**.

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de Wdesk Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Wdesk aplicação.
Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

