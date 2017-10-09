---
title: "Tutorial: Integração do Azure Active Directory com Bime | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Bime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a>Tutorial: Integração do Azure Active Directory com Bime

Neste tutorial, saiba como toointegrate Bime com o Azure Active Directory (Azure AD).

Integrar Bime com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooBime
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooBime (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Bime tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Bime-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Bime da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-bime-from-hello-gallery"></a>Adicionar Bime da Galeria de Olá
tooconfigure Olá integração de Bime com o Azure AD, é necessário tooadd Bime Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Bime da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Bime**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. No painel de resultados de Olá, selecione **Bime**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Bime com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Bime é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Bime tem toobe estabelecida.

No Bime, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Bime, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Bime](#creating-a-bime-test-user)**  -toohave um homólogo de Britta Simon no Bime é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Bime.

**tooconfigure do Azure AD-início de sessão único com Bime, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Bime** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. No Olá **Bime domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.Bimeapp.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.Bimeapp.com`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget estes valores. 
 
4. No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado de Olá.

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. No Olá **Bime configuração** secção, clique em **configurar Bime** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa Bime como administrador.

8. Na barra de ferramentas Olá, clique em **Admin**e, em seguida, **conta**.
   
    ![Administração](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")

9. Na página de configuração de conta Olá, execute Olá os seguintes passos:
   
    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/ic775559.png "configurar o início de sessão único")
   
    a. Selecione **autenticação ativar SAML**.

    b. No Olá **URL de início de sessão remoto** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML**, que copiou do portal do Azure.

    c.  Olá colar **Thumbprint** valor a partir do portal do Azure para Olá **impressão digital do certificado** caixa de texto.       
   
    d. Clique em **Guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-bime-test-user"></a>Criar um utilizador de teste Bime

Na ordem tooenable do Azure AD os utilizadores toolog no tooBime, têm de ser aprovisionados para Bime. No caso de Olá da Bime, o aprovisionamento é uma tarefa manual.

**tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **Bime** inquilino.

2. Na barra de ferramentas Olá, clique em **Admin**e, em seguida, **utilizadores**.
   
    ![Administração](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")

3. No Olá **lista utilizadores**, clique em **adicionar novo utilizador** ("+").
   
    ![Os utilizadores](./media/active-directory-saas-bime-tutorial/ic775562.png "utilizadores")

4. No Olá **detalhes de utilizador** diálogo página, execute Olá os seguintes passos:
   
    ![Detalhes de utilizador](./media/active-directory-saas-bime-tutorial/ic775563.png "detalhes de utilizador")
   
    a. No Olá **nome próprio** caixa de texto, introduza Olá primeiro nome de utilizador como **Britta**.

    b. No Olá **Apelido** caixa de texto, introduza o apelido Olá do utilizador, como **Simon**.
 
    c. No Olá **E-Mail** caixa de texto, introduza Olá e-mail do utilizador, como  **brittasimon@contoso.com** .

    d. Clique em **Guardar**.

>[!NOTE]
>Pode utilizar quaisquer outras Bime utilizador conta criação ferramentas ou APIs fornecidas pelo Bime tooprovision contas de utilizador do AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooBime.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooBime, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Bime**.

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.

Ao clicar em mosaico de Bime Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Bime aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

