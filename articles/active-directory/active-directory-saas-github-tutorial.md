---
title: "Tutorial: Integração do Azure Active Directory com o GitHub | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e do GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Tutorial: Integração do Azure Active Directory com o GitHub

Neste tutorial, saiba como toointegrate GitHub com o Azure Active Directory (Azure AD).

Integrar o GitHub com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooGitHub
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooGitHub (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal de gestão do Azure de Olá

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com o GitHub, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um GitHub início de sessão único subscrição ativado


> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.


tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição de GitHub da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-


## <a name="adding-github-from-hello-gallery"></a>A adição de GitHub da Galeria de Olá
tooconfigure Olá integração do GitHub com o Azure AD, é necessário tooadd GitHub Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd GitHub da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **GitHub.com**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. No painel de resultados de Olá, selecione **GitHub**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com o GitHub com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá no GitHub é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no GitHub tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no GitHub.

tooconfigure e teste do Azure AD-início de sessão único com o GitHub, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste do GitHub](#creating-a-GitHub-test-user)**  -toohave um homólogo de Britta Simon no GitHub que é a representação de toohello ligado do Azure AD de forma.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação do GitHub.

**tooconfigure do Azure AD-início de sessão único com o GitHub, efetuar Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, no Olá **GitHub** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. No Olá **domínio GitHub e URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    a. No Olá **URL de início de sessão** caixa de texto, valor de tipo de Olá como:`https://github.com/orgs/<entity-id>/sso`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > Tenha em atenção que estes não são valores reais Olá. Tiver tooupdate estes valores com Olá real iniciar sessão no URL e o identificador. Aqui sugerimos toouse Olá exclusivo valor da cadeia no Olá identificador. Aceda tooGitHub Admin secção tooretrieve estes valores. 

4. No Olá **atributos de utilizador** secção, selecione **identificador de utilizador** como user.mail.

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. No Olá **certificado de assinatura de SAML** secção, clique em **criar novo certificado**.

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. No Olá **criar o novo certificado** caixa de diálogo, clique Olá ícone de calendário e selecione um **data de expiração**. Em seguida, clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. No Olá **certificado de assinatura de SAML** secção, selecione **tornar o novo certificado ativa** e clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. No pop-up de Olá **o certificado de Rollover** janela, clique em **OK**.

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. No Olá **configuração de GitHub** secção, clique em **configurar GitHub** tooopen **configurar início de sessão** janela.

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. Numa janela do browser web diferente, inicie sessão no seu site do GitHub organização como um administrador.

12. Navegue demasiado**definições** e clique em **segurança**

    ![Definições](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. Verifique Olá **autenticação ativar SAML** caixa, revelando Olá Single Sign-on configuração os campos. Em seguida, utilize Olá URL single sign-on URL valor tooupdate Olá único início de sessão na configuração do Azure AD.

    ![Definições](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. Configure Olá seguintes campos:

    a. **Inicie sessão no URL**: introduza **SAML-início de sessão único URL de serviço** de Olá **configurar GitHub** secção sobre o Azure AD

    b. **Emissor**: introduza **ID de entidade de SAML** de Olá **configurar GitHub** secção sobre o Azure AD

    c. **Certificado público**: Abra Olá transferido o certificado do Azure AD num bloco de notas e copie Olá o conteúdo, incluindo "Certificado começar" e "END certificado"

    ![Definições](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. Clique em **configuração SAML do teste** tooconfirm que não existem falhas de validação ou erros durante a SSO.

    ![Definições](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. Clique em **guardar**

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**. 


### <a name="creating-a-github-test-user"></a>Criar um utilizador de teste do GitHub

Na ordem tooenable do Azure AD os utilizadores toolog no GitHub, tem de ser aprovisionados no GitHub.  
No caso de Olá do GitHub, o aprovisionamento é uma tarefa manual.

**executar de contas de utilizador, tooprovision Olá os seguintes passos:**

1. Inicie sessão no tooyour GitHub site da empresa como administrador.

2. Clique em **pessoas**.

    ![As pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "pessoas")

3. Clique em **convite membro**.

    ![Convidar utilizadores](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "convidar utilizadores")

4. No Olá **convite membro** diálogo página, execute Olá os seguintes passos:

    a. No Olá **E-Mail** caixa de texto, endereço de correio eletrónico de Olá de tipo de conta Britta Simon.

    ![Convidar pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "convidar pessoas")
    
    b. Clique em **enviar o convite**.

    ![Convidar pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "convidar pessoas")

    > [!NOTE]
    > titular de conta do Azure Active Directory Olá irá receber um e-mail e siga a tooconfirm uma ligação a respetiva conta para ficar ativa.


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooGitHub de acesso.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooGitHub, execute Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **GitHub.com**.

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    


### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de GitHub Olá no painel de acesso de Olá, deve obter com sessão iniciada tooyour aplicação do GitHub. Irá ser iniciar sessão como uma conta de organização, mas, em seguida, é necessário toolog com a sua conta pessoal.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
