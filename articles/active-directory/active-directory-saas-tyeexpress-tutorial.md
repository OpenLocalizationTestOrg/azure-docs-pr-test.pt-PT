---
title: "Tutorial: Integração do Azure Active Directory com o T & Express I | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e T & I Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a>Tutorial: Integração do Azure Active Directory com o T & I Express

Neste tutorial, saiba como toointegrate T & I Express com o Azure Active Directory (Azure AD).

Integrar o T & I Express com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha tooT acesso & I Express
- Pode ativar a utilizadores tooautomatically get com sessão iniciada tooT & I Express (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal de gestão do Azure de Olá

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com o T & I Express tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Redireccionamen & I Express início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar e & I Express na Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-te-express-from-hello-gallery"></a>Adicionar e & I Express na Galeria de Olá
tooconfigure Olá integração d & I Express com o Azure AD, terá de tooadd T & I Express Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd T & I Express a partir da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **T & I Express**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. No painel de resultados de Olá, selecione **T & I Express**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com o T & I Express com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que Olá homólogo utilizador T & I Express é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados com o utilizador no T & I Express toobe necessidades estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** T & I Express.

tooconfigure e teste do Azure AD-início de sessão único com o T & I Express, necessitará de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste T & I Express](#creating-a-te-express-test-user)**  -toohave um homólogo de Britta Simon T & I Express que é a representação de toohello ligado do Azure AD de forma.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação T & I Express.

**tooconfigure do Azure AD-início de sessão único com o T & I Express, execute Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, no Olá **T & I Express** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. No Olá **T & I Express domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    a. No Olá **identificador** caixa de texto, valor de tipo de Olá como:`https://<domain>.tyeexpress.com`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`

    > [!NOTE] 
    > Tenha em atenção que estes não são valores reais Olá. Tiver tooupdate estes valores com o URL de identificador e resposta real no Olá. Aqui sugerimos toouse Olá exclusivo valor da cadeia no Olá identificador. Contacte [equipa de suporte de T & I Express](http://www.tyeexpress.com/contacto.aspx) tooget estes valores.

5. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. tooconfigure-início de sessão único em **T & i rápida** lado, início de sessão toohello T & aplicação rápida do i sem SAML único início de sessão com credenciais do administrador.

9. Em Olá **Admin** separador, clique em **domínio SAML** página de definições do tooOpen Olá SAML.

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. Selecione Olá **Activar(Activate)** opção de **não** demasiado**SI(Yes)**. No Olá **metadados do fornecedor de identidade** caixa de texto, colar Olá metadados XML que tiver donwloaded a partir do portal do Azure.

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. Clique em Olá **Guardar(Save)** no botão Definições de Olá toosave. 


### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-te-express-test-user"></a>Criar um utilizador de teste T & I Express

Na ordem tooenable do Azure AD os utilizadores toolog em T & I Express, têm de ser aprovisionados para T & I Express.  
Em caso de T & I Express, o aprovisionamento é uma tarefa manual.

**executar de contas de utilizador, tooprovision Olá os seguintes passos:**

1. Inicie sessão no tooyour T & I Express site da empresa como administrador.

2. Na etiqueta do administrador, clique na página principal do utilizadores tooopen Olá utilizadores.

    ![Adicionar empregado](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. Na página inicial de Olá, clique em  **+**  utilizadores de Olá tooadd.

    ![Adicionar empregado](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. Introduza todos os detalhes de obrigatório Olá, tal como pedido no formulário de Olá e clique em Olá guardar botão toosave Olá detalhes.

    ![Adicionar empregado](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Adicionar empregado](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooT acesso & I Express.

![Atribua o utilizador][200] 

**tooassign tooT Britta Simon & I Express, execute Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **T & I Express**.

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá T & I Express mosaico no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour T & I Express desta aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

