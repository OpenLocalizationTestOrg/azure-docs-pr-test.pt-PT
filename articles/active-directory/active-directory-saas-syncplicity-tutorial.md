---
title: "Tutorial: Integração do Azure Active Directory com Syncplicity | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a>Tutorial: Integração do Azure Active Directory com Syncplicity

Neste tutorial, saiba como toointegrate Syncplicity com o Azure Active Directory (Azure AD).

Integrar Syncplicity com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooSyncplicity
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSyncplicity (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Syncplicity tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Syncplicity-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Syncplicity da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-syncplicity-from-hello-gallery"></a>Adicionar Syncplicity da Galeria de Olá
tooconfigure Olá integração de Syncplicity com o Azure AD, é necessário tooadd Syncplicity Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Syncplicity da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Syncplicity**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. No painel de resultados de Olá, selecione **Syncplicity**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Syncplicity com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Syncplicity é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Syncplicity tem toobe estabelecida.

No Syncplicity, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Syncplicity, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Syncplicity](#creating-a-syncplicity-test-user)**  -toohave um homólogo de Britta Simon no Syncplicity é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Syncplicity.

**tooconfigure do Azure AD-início de sessão único com Syncplicity, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Syncplicity** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. No Olá **Syncplicity domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.syncplicity.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.syncplicity.com/sp`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente Syncplicity](https://www.syncplicity.com/contact-us) tooget estes valores. 
 

4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. No Olá **Syncplicity configuração** secção, clique em **configurar Syncplicity** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. Inicie sessão no tooyour **Syncplicity** inquilino.

8. No menu de Olá na parte superior do Olá, clique em **admin**, selecione **definições**e, em seguida, clique em **domínio personalizado e o início de sessão único**.
   
    ![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")

9. No Olá **único Sign-On (SSO)** diálogo página, execute Olá os seguintes passos:
   
    ![De sessão único- \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")   

    a. No Olá **domínio personalizado** caixa de texto, nome do tipo Olá do seu domínio.
  
    b. Selecione **ativada** como **Single Sign-On estado**.

    c. No Olá **Id de entidade** caixa de texto, valor Olá colar **ID de entidade de SAML** que copiou do portal do Azure.

    d. No Olá **URL de página de início de sessão** caixa de texto, Olá colar **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.

    e. No Olá **terminar o URL da página** caixa de texto, Olá colar **Sign-Out URL** que copiou do portal do Azure.

    f. No **certificado do fornecedor de identidade**, clique em **Escolher ficheiro**e, em seguida, carregue o certificado de Olá que transferiu do Olá portal do Azure. 

    g. Clique em **guardar alterações**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-syncplicity-test-user"></a>Criar um utilizador de teste Syncplicity
Para o AAD utilizadores toobe capaz de toosign no, têm de ser aprovisionada tooSyncplicity aplicação. Esta secção descreve como de contas de utilizador AAD toocreate Syncplicity.

**tooprovision um tooSyncplicity de conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **Syncplicity** inquilino (por exemplo: `https://company.Syncplicity.com`).

2. Clique em **admin** e selecione **contas de utilizador**.

3. Clique em **adicionar um utilizador**.
   
    ![Gerir utilizadores](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "gerir utilizadores")

4. Olá tipo **endereços de correio eletrónico** de uma conta do AAD pretende tooprovision, selecione **utilizador** como **função**e, em seguida, clique em **seguinte**.
   
    ![Informações de conta](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "informações de conta")
   
    >[!NOTE]
    >titular da conta do Olá AAD obtém uma mensagem de e-mail, incluindo um tooconfirm de ligação e ativar a conta de Olá. 
    > 

5. Selecione um grupo na sua empresa que o novo utilizador deve ser membro de e, em seguida, clique em **seguinte**.
   
    ![Associação ao grupo](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "associação ao grupo")
   
    >[!NOTE]
    >Se não existem não existem grupos listados, clique em **seguinte**. 
    > 

6. Selecione as pastas de Olá teria como tooplace sob o controlo da Syncplicity no computador do utilizador Olá e, em seguida, clique em **seguinte**.
   
    ![Pastas de Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity pastas")

>[!NOTE]
>Pode utilizar quaisquer outras Syncplicity utilizador conta criação ferramentas ou APIs fornecidas pelo Syncplicity tooprovision contas de utilizador do AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSyncplicity.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooSyncplicity, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Syncplicity**.

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.

Ao clicar em mosaico de Syncplicity Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Syncplicity aplicação.
## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

