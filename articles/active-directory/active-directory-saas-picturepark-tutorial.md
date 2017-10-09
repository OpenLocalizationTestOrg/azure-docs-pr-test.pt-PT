---
title: "Tutorial: Integração do Azure Active Directory com Picturepark | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Tutorial: Integração do Azure Active Directory com Picturepark

Neste tutorial, saiba como toointegrate Picturepark com o Azure Active Directory (Azure AD).

Integrar Picturepark com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooPicturepark
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPicturepark (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Picturepark tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Picturepark-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Picturepark da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-picturepark-from-hello-gallery"></a>Adicionar Picturepark da Galeria de Olá
tooconfigure Olá integração de Picturepark com o Azure AD, é necessário tooadd Picturepark Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Picturepark da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Picturepark**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. No painel de resultados de Olá, selecione **Picturepark**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Picturepark com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Picturepark é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Picturepark tem toobe estabelecida.

No Picturepark, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Picturepark, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Picturepark](#creating-a-picturepark-test-user)**  -toohave um homólogo de Britta Simon no Picturepark é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Picturepark.

**tooconfigure do Azure AD-início de sessão único com Picturepark, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Picturepark** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. No Olá **Picturepark domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.picturepark.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização: 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente Picturepark](https://picturepark.com/about/contact/) tooget estes valores. 
 
4. No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado.

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. No Olá **Picturepark configuração** secção, clique em **configurar Picturepark** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa Picturepark como administrador.

8. Na barra de ferramentas Olá na parte superior do Olá, clique em **ferramentas administrativas**e, em seguida, clique em **consola de gestão**.
   
    ![Consola de gestão](./media/active-directory-saas-picturepark-tutorial/ic795062.png "consola de gestão")

9. Clique em **autenticação**e, em seguida, clique em **fornecedores de identidade**.
   
    ![Autenticação](./media/active-directory-saas-picturepark-tutorial/ic795063.png "autenticação")

10. No Olá **configuração do fornecedor de identidade** secção, execute Olá os seguintes passos:
   
    ![Configuração do fornecedor de identidade](./media/active-directory-saas-picturepark-tutorial/ic795064.png "configuração do fornecedor de identidade")
   
    a. Clique em **Adicionar**.
  
    b. Escreva um nome para a sua configuração.
   
    c. Selecione **configurado como predefinido**.
   
    d. No **URI de Issuer** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.
   
    e. No **impressão de botão de emissor fidedigno** caixa de texto, colar Olá valor **Thumbprint** que copiou do **certificado de assinatura de SAML** secção. 

11. Clique em **JoinDefaultUsersGroup**.

12. Olá tooset **Emailaddress** atributo na Olá **afirmação** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` e clique em **guardar**.

      ![Configuração](./media/active-directory-saas-picturepark-tutorial/ic795065.png "configuração")

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-picturepark-test-user"></a>Criar um utilizador de teste Picturepark

Na ordem tooenable do Azure AD os utilizadores toolog para Picturepark, têm de ser aprovisionados para Picturepark. No caso de Olá da Picturepark, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **Picturepark** inquilino.

2. Na barra de ferramentas Olá na parte superior do Olá, clique em **ferramentas administrativas**e, em seguida, clique em **utilizadores**.
   
    ![Os utilizadores](./media/active-directory-saas-picturepark-tutorial/ic795067.png "utilizadores")

3. No Olá **descrição geral de utilizadores** separador, clique em **novo**.
   
    ![Gestão de utilizadores](./media/active-directory-saas-picturepark-tutorial/ic795068.png "gestão de utilizadores")

4. No Olá **criar utilizador** caixa de diálogo, Olá de efetuar os seguintes passos para um utilizador válido para o Azure Active Directory que pretende tooprovision:
   
    ![Criar utilizador](./media/active-directory-saas-picturepark-tutorial/ic795069.png "criar utilizador")
   
    a. No Olá **endereço de correio eletrónico** caixa de texto, Olá tipo **endereço de correio eletrónico** do utilizador Olá  **BrittaSimon@contoso.com** .  
   
    b. No Olá **palavra-passe** e **Confirmar palavra-passe** caixas de texto, Olá tipo **palavra-passe** de BrittaSimon. 
   
    c. No Olá **nome próprio** caixa de texto, Olá tipo **nome próprio** do utilizador Olá **Britta**. 
   
    d. No Olá **Apelido** caixa de texto, Olá tipo **Apelido** do utilizador Olá **Simon**.
   
    e. No Olá **empresa** caixa de texto, Olá tipo **nome da empresa** do utilizador Olá. 
   
    f. No Olá **país** caixa de texto, selecione de Olá **país** do utilizador Olá.
  
    g. No Olá **ZIP** caixa de texto, Olá tipo **código postal** da cidade de Olá.
   
    h. No Olá **Cidade** caixa de texto, Olá tipo **nome Cidade** do utilizador Olá.

    posso. Selecione um **idioma**.
   
    j. Clique em **Criar**.

>[!NOTE]
>Pode utilizar quaisquer outras Picturepark utilizador conta criação ferramentas ou APIs fornecidas pelo Picturepark tooprovision contas de utilizador do Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPicturepark.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooPicturepark, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Picturepark**.

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de Picturepark Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Picturepark aplicação. Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

