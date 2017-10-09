---
title: "Tutorial: Integração do Azure Active Directory com o Tableau Online | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>Tutorial: Integração do Azure Active Directory com o Tableau Online

Neste tutorial, saiba como toointegrate Tableau Online com o Azure Active Directory (Azure AD).

Integrar o Tableau Online com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooTableau Online
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooTableau Online (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com o Tableau Online, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Tableau Online-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Tableau Online a partir da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-tableau-online-from-hello-gallery"></a>Adicionar Tableau Online a partir da Galeria de Olá
tooconfigure Olá integração do Tableau Online com o Azure AD, é necessário tooadd Tableau Online Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Tableau Online da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Tableau Online**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. No painel de resultados de Olá, selecione **Tableau Online**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com o Tableau Online de acordo com um utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que Olá homólogo utilizador Tableau Online é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados utilizador Tableau Online tem toobe estabelecida.

No Tableau Online, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com o Tableau Online, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Tableau Online](#creating-a-tableau-online-test-user)**  -toohave um homólogo de Britta Simon Tableau online que está ligado toohello do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Tableau Online.

**tooconfigure do Azure AD-início de sessão único com o Tableau Online, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Tableau Online** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. No Olá **domínio Online Tableau e URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    a. No Olá **URL de início de sessão** caixa de texto, tipo Olá URL:`https://sso.online.tableau.com`

    b. No Olá **identificador** caixa de texto, tipo Olá URL:`https://sso.online.tableau.com/public/sp/<instancename>`

4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. Na janela do browser diferente, início de sessão tooyour aplicação Tableau Online. Aceda demasiado**definições** e, em seguida, **autenticação**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. tooenable SAML, em **tipos de autenticação** secção. Verifique Olá **-início de sessão único com o SAML** caixa de verificação.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. Desloque para baixo até **ficheiro de metadados de importação para o Tableau Online** secção.  Clique em Procurar e importar o ficheiro de metadados de Olá que transferiu a partir do Azure AD. Em seguida, clique em **aplicar**.
   
   ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. No Olá **corresponder asserções** secção, inserir Olá fornecedor de identidade asserção nome correspondente para **endereço de correio eletrónico**, **nome próprio**, e **Apelido** . tooget estas informações do Azure AD: 
  
    a. No Olá portal do Azure, visite no Olá **Tableau Online** página de integração de aplicações.
    
    b. Na secção de atributos de Olá, selecione Olá **"ver e editar todos os outros atributos de utilizador"** caixa de verificação. 
    
   ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    c. Copie o valor de espaço de nomes de Olá para estes atributos: givenname, ao e-mail e apelido utilizando Olá os seguintes passos:

   ![Azure AD início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    d. Clique em **user.givenname** valor 
    
    e. Copie o valor de Olá de Olá **espaço de nomes** caixa de texto.

   ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    f. toocopy Olá namesapce os valores e-mail Olá e apelido siga Olá precedente passos.

    g. Comutador aplicação Tableau Online toohello, em seguida, definir Olá **atributos Online Tableau** secção da seguinte forma:
     * E-mail: **correio** ou **userprincipalname**
     * Nome próprio: **givenname**
     * Apelido: **Apelido**
   
   ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-tableau-online-test-user"></a>Criar um utilizador de teste Tableau Online

Nesta secção, vai criar um utilizador chamado Britta Simon Tableau online.

1. No **Tableau Online**, clique em **definições** e, em seguida, **autenticação** secção. Desloque para baixo demasiado**selecionar utilizadores** secção. Clique em **adicionar utilizadores** e, em seguida, **introduza os endereços de correio eletrónico**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. Selecione **adicionar utilizadores para a autenticação de início de sessão único (SSO)**. No Olá **Introduza endereços de correio eletrónico** adicionar caixa de textobritta.simon@contoso.com
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. Clique em **Criar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooTableau Online.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooTableau Online, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Tableau Online**.

    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.

Ao clicar em mosaico Tableau Online do Olá no painel de acesso de Olá, deve obter aplicações Tableau Online tooyour automaticamente com sessão iniciada.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

