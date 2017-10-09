---
title: "Tutorial: Integração do Azure Active Directory com Wikispaces | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Wikispaces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: eb5b72e60b415cb657b70ba530df731ae14b0425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a>Tutorial: Integração do Azure Active Directory com Wikispaces

Neste tutorial, saiba como toointegrate Wikispaces com o Azure Active Directory (Azure AD).

Integrar Wikispaces com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooWikispaces
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooWikispaces (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Wikispaces tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Wikispaces-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Wikispaces da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-wikispaces-from-hello-gallery"></a>Adicionar Wikispaces da Galeria de Olá
tooconfigure Olá integração de Wikispaces com o Azure AD, é necessário tooadd Wikispaces Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Wikispaces da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Wikispaces**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. No painel de resultados de Olá, selecione **Wikispaces**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Wikispaces com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Wikispaces é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Wikispaces tem toobe estabelecida.

No Wikispaces, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Wikispaces, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Wikispaces](#creating-a-wikispaces-test-user)**  -toohave um homólogo de Britta Simon no Wikispaces é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Wikispaces.

**tooconfigure do Azure AD-início de sessão único com Wikispaces, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Wikispaces** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. No Olá **Wikispaces domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.wikispaces.net`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://session.wikispaces.net/<instancename>`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente Wikispaces](https://www.wikispaces.com/site/help) tooget estes valores. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. tooconfigure-início de sessão único em **Wikispaces** lado, terá de Olá toosend transferido **XML de metadados** demasiado[Wikispaces suporta equipa](https://www.wikispaces.com/site/help). Irá receber uma notificação assim que a configuração de Olá foi concluída.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-wikispaces-test-user"></a>Criar um utilizador de teste Wikispaces

Na ordem tooenable do Azure AD os utilizadores toolog no tooWikispaces, têm de ser aprovisionados para Wikispaces. No caso de Olá da Wikispaces, o aprovisionamento é uma tarefa manual.

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a>executar de contas de utilizador, tooprovision Olá os seguintes passos:
1. Inicie sessão no tooyour **Wikispaces** site da empresa como administrador.

2. Aceda demasiado**membros**.
   
    ![Os membros](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "membros")

3. Clique em Olá **convidar pessoas**.
   
    ![Convidar pessoas](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "convidar pessoas")

4. No Olá **convidar pessoas** secção, execute Olá os seguintes passos:
   
    ![Convidar pessoas](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "convidar pessoas")
   
    a. Olá tipo **nomes de utilizador ou endereço de correio eletrónico** de uma conta válida do AAD que pretende tooprovision Olá relacionadas com caixas de texto.
   
    b. Clique em **enviar**.  
      
    > [!NOTE]
    > titular de conta do Azure Active Directory Olá recebe uma mensagem de e-mail, incluindo uma conta de Olá ligação tooconfirm para ficar ativa.
    
> [!NOTE]
> Pode utilizar quaisquer outras Wikispaces utilizador conta criação ferramentas ou APIs fornecidas pelo Wikispaces tooprovision contas de utilizador do AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooWikispaces.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooWikispaces, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Wikispaces**.

    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá Wikispaces na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour Wikispaces aplicação.
Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

