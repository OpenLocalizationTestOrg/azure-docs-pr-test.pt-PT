---
title: "Tutorial: Integração do Azure Active Directory com UserVoice | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a>Tutorial: Integração do Azure Active Directory com UserVoice

Neste tutorial, saiba como toointegrate UserVoice com o Azure Active Directory (Azure AD).

Integrar o UserVoice com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooUserVoice.
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooUserVoice (Single Sign-On) com as respetivas contas do Azure AD.
- Pode gerir as contas numa localização central - Olá portal do Azure.

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com UserVoice tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um UserVoice-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar UserVoice da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-uservoice-from-hello-gallery"></a>Adicionar UserVoice da Galeria de Olá
tooconfigure Olá integração do UserVoice com o Azure AD, é necessário tooadd UserVoice Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd UserVoice da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![botão de Azure Active Directory Olá][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Painel de aplicações do Olá Enterprise][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![botão de aplicação nova Olá][3]

4. Na caixa de pesquisa de Olá, escreva **UserVoice**, selecione **UserVoice** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Lista de resultados do UserVoice no Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único

Nesta secção, configure e teste do Azure AD-início de sessão único com UserVoice com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá UserVoice é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no UserVoice tem toobe estabelecida.

No UserVoice, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com o UserVoice, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste do UserVoice](#create-a-uservoice-test-user)**  -toohave um homólogo de Britta Simon no UserVoice é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação da UserVoice.

**tooconfigure do Azure AD-início de sessão único com o UserVoice, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **UserVoice** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar a ligação de início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. No Olá **UserVoice domínio e os URLs** secção, execute Olá os seguintes passos:

    ![UserVoice domínio e os URLs únicos de informações de início de sessão](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.UserVoice.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.UserVoice.com`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente do UserVoice](https://www.uservoice.com/) tooget estes valores.

4. No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado.

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. No Olá **UserVoice configuração** secção, clique em **configurar UserVoice** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configuração do UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site de empresa do UserVoice tooyour como administrador.

8. Na barra de ferramentas Olá na parte superior do Olá, clique em **definições**e, em seguida, selecione **Web portal** menu Olá.
   
    ![Secção de definições no lado de aplicação](./media/active-directory-saas-uservoice-tutorial/ic777519.png "definições")

9. No Olá **Web portal** separador, Olá **autenticação de utilizador** secção, clique em **editar** tooopen Olá **editar autenticação de utilizador** caixa de diálogo página.
   
    ![Portal Web do separador](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")

10. No Olá **editar autenticação de utilizador** diálogo página, execute Olá os seguintes passos:
   
    ![Editar autenticação de utilizador](./media/active-directory-saas-uservoice-tutorial/ic777521.png "editar autenticação de utilizador")
   
    a. Clique em **Single Sign-On (SSO)**.
 
    b. Olá colar **único início de sessão no URL do serviço SAML** valor que copiou do Olá portal do Azure para Olá **SSO remoto início de sessão** caixa de texto.

    c. Olá colar **Sign-Out URL** valor que copiou do Olá portal do Azure para Olá **Sign-Out remoto SSO caixa de texto**.
 
    d. Olá colar **Thumbprint** valor que copiou do portal do Azure para o **impressão digital de certificado SHA1 atual** caixa de texto.
    
    e. Clique em **guardar as definições de autenticação**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

   ![Criar um utilizador de teste do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.

    ![botão de adição de Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    a. No Olá **nome** caixa, escreva **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.

    c. Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-uservoice-test-user"></a>Criar um utilizador de teste do UserVoice

tooenable do Azure AD os utilizadores toolog no tooUserVoice, estes têm de ser aprovisionados para UserVoice. No caso de Olá da UserVoice, o aprovisionamento é uma tarefa manual.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision uma conta de utilizador, execute Olá os seguintes passos:
1. Inicie sessão no tooyour **UserVoice** inquilino.

2. Aceda demasiado**definições**.
   
    ![Definições](./media/active-directory-saas-uservoice-tutorial/ic777811.png "definições")

3. Clique em **geral**.

4. Clique em **agentes e permissões**.
   
    ![Os agentes e permissões](./media/active-directory-saas-uservoice-tutorial/ic777812.png "agentes e permissões")

5. Clique em **adicione administradores**.
   
    ![Adicionar administradores](./media/active-directory-saas-uservoice-tutorial/ic777813.png "adicione administradores")

6. No Olá **convidar admins** caixa de diálogo, efetuar Olá os seguintes passos:
   
    ![Convidar admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "convidar admins")
   
    a. Na caixa de texto de mensagens de correio eletrónico Olá, escreva o endereço de correio eletrónico Olá da conta de Olá pretende tooprovision e, em seguida, clique em **adicionar**.
   
    b. Clique em **convidar**.

> [!NOTE]
> Pode utilizar quaisquer outras UserVoice utilizador conta criação ferramentas ou APIs fornecidas pelo UserVoice tooprovision contas de utilizador do AAD.

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooUserVoice.

![Atribuir a função de utilizador Olá][200] 

**tooassign Britta Simon tooUserVoice, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **UserVoice**.

    ![ligação do UserVoice Olá na lista de aplicações de Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![ligação de "Utilizadores e grupos" Olá][202]

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição de adicionar Olá][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de UserVoice Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour UserVoice aplicação.
Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

