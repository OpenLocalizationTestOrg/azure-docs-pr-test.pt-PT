---
title: "Tutorial: Integração do Azure Active Directory com LockPath Keylight | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a>Tutorial: Integração do Azure Active Directory com LockPath Keylight

Neste tutorial, saiba como toointegrate LockPath Keylight com o Azure Active Directory (Azure AD).

Integrar LockPath Keylight com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooLockPath Keylight
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooLockPath Keylight (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com LockPath Keylight tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um LockPath Keylight início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar LockPath Keylight da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-lockpath-keylight-from-hello-gallery"></a>Adicionar LockPath Keylight da Galeria de Olá
tooconfigure Olá integração de LockPath Keylight com o Azure AD, é necessário tooadd LockPath Keylight Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd LockPath Keylight da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **LockPath Keylight**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. No painel de resultados de Olá, selecione **LockPath Keylight**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com LockPath Keylight com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá LockPath Keylight é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá LockPath Keylight tem toobe estabelecida.

No LockPath Keylight, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com LockPath Keylight, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave um homólogo de Britta Simon no LockPath Keylight que é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação LockPath Keylight.

**tooconfigure do Azure AD-início de sessão único com LockPath Keylight, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **LockPath Keylight** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. No Olá **LockPath Keylight domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.keylightgrc.com/`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.keylightgrc.com`

    c. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.keylightgrc.com/Login.aspx`
    
    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão. Contacte [equipa de suporte de cliente de Keylight LockPath](https://www.lockpath.com/contact/) tooget estes valores. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Raw)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. No Olá **LockPath Keylight configuração** secção, clique em **configurar Keylight de LockPath** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. tooenable SSO no LockPath Keylight, execute Olá os seguintes passos:
   
    a. Início de sessão tooyour LockPath Keylight conta como administrador.
    
    b. No menu de Olá na parte superior do Olá, clique em **pessoa**e selecione **Keylight configuração**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/401.png) 

    c. Olá TreeView Olá esquerda, clique em **SAML**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/402.png) 

    d. No Olá **SAML definições** caixa de diálogo, clique em **editar**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/404.png) 

8. No Olá **editar definições de SAML** diálogo página, execute Olá os seguintes passos:
   
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    a. Definir **autenticação SAML** demasiado**Active Directory**.

    b. Olá colar **único início de sessão no URL do serviço SAML** valor que copiou do Olá portal do Azure para Olá **URL de início de sessão do fornecedor de identidade** caixa de texto.

    c. Olá colar **único URL de serviço Sign-Out** valor que copiou do Olá portal do Azure para Olá **URL de fim de sessão do fornecedor de identidade** caixa de texto.

    d. Clique em **Escolher ficheiro** tooselect sua LockPath Keylight transferido do certificado e, em seguida, clique em **abra** certificado de Olá tooupload.

    e. Definir **localização de Id de utilizador de SAML** demasiado**NameIdentifier elemento da instrução de assunto Olá**.
    
    f. Fornecer Olá **fornecedor de serviços de Keylight** Olá seguir o padrão de utilização: **https://&lt;CompanyName&gt;. keylightgrc.com**.
    
    g. Definir **utilizadores de aprovisionamento automático** demasiado**Active Directory**.

    h. Definir **tipo de conta de aprovisionamento automático** demasiado**utilizador completo**.

    posso. Definir **função de segurança de aprovisionamento automático**, selecione **utilizador padrão com SAML**.
    
    j. Definir **configuração de segurança de aprovisionamento automático**, selecione **configuração de utilizador padrão**.
     
    k. No Olá **atributo de correio eletrónico** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    l. No Olá **nome próprio atributo** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    m. No Olá **atributo de nome do último** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    n. Clique em **Guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-lockpath-keylight-test-user"></a>Criar um utilizador de teste LockPath Keylight

Nesta secção, vai criar um utilizador chamado Britta Simon LockPath Keylight. LockPath Keylight suporta o aprovisionamento de just-in-time, que está ativada por predefinição.

Não há nenhum item de ação para si nesta secção. Um novo utilizador é criado quando aceder ao LockPath Keylight se o utilizador Olá ainda não existe. 

>[!NOTE]
>Se precisar de um utilizador de toocreate manualmente, terá de toocontact Olá [equipa de suporte de cliente de Keylight LockPath](https://www.lockpath.com/contact/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooLockPath Keylight.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooLockPath Keylight, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **LockPath Keylight**.

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá LockPath Keylight na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour LockPath Keylight aplicação. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

