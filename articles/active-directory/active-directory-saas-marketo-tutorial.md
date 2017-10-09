---
title: "Tutorial: Integração do Azure Active Directory com Marketo | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e do Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>Tutorial: Integração do Azure Active Directory com Marketo

Neste tutorial, saiba como toointegrate Marketo no Azure Active Directory (Azure AD).

Integração do Marketo com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooMarketo
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooMarketo (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Marketo tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Marketo início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição do Marketo da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-marketo-from-hello-gallery"></a>A adição do Marketo da Galeria de Olá
tooconfigure Olá integração do Marketo com o Azure AD, é necessário tooadd Marketo Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Marketo da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Marketo**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. No painel de resultados de Olá, selecione **Marketo**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Marketo com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Marketo é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Marketo tem toobe estabelecida.

No Marketo, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Marketo, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste do Marketo](#creating-a-marketo-test-user)**  -toohave um homólogo de Britta Simon no Marketo é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação do Marketo.

**tooconfigure do Azure AD-início de sessão único com Marketo, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Marketo** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. No Olá **URLs e de domínio do Marketo** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://saml.marketo.com/sp`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o URL de identificador e resposta real no Olá. Contacte [equipa de suporte do Marketo](http://investors.marketo.com/contactus.cfm) tooget estes valores.
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. No Olá **Marketo configuração** secção, clique em **configurar Marketo** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. tooget Munchkin Id da aplicação, inicie sessão no tooMarketo utilizando credenciais de administrador e execute os seguintes ações:
   
    a. Inicie sessão na aplicação tooMarketo com credenciais do administrador.
   
    b. Clique em Olá **Admin** botão no painel de navegação superior Olá.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegue toohello menu de integração e clique em Olá **ligação Munchkin**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    d. Copie Olá Id Munchkin mostrado no ecrã de Olá e concluir o seu URL de resposta no Assistente de configuração de Olá do Azure AD.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. tooconfigure Olá SSO na aplicação Olá, siga Olá passos abaixo:
   
    a. Inicie sessão na aplicação tooMarketo com credenciais do administrador.
   
    b. Clique em Olá **Admin** botão no painel de navegação superior Olá.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegue toohello menu de integração e clique em **início de sessão único**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    d. Olá tooenable SAML definições, clique em **editar** botão.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    e. **Ativado** Single Sign-On definições.
   
    f. Olá colar **ID de entidade de SAML**, no Olá **emissor ID** caixa de texto.
   
    g. No Olá **ID de entidade** caixa de texto, introduza o URL de Olá como `http://saml.marketo.com/sp`.
   
    h. Selecione Olá localização do ID de utilizador como **elemento identificador de nome**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > Se o identificador de utilizador não é o valor UPN e altera o valor de Olá no separador de atributo Olá.
   
    posso. Carregue o certificado Olá, que transferiu a partir do Assistente de configuração do Azure AD. **Guardar** Olá definições.
   
    j. Edite definições de páginas de redirecionamento de Olá.
   
    k. Olá colar **único início de sessão no URL do serviço SAML** no Olá **URL de início de sessão** caixa de texto.
   
    l. Olá colar **Sign-Out URL** no Olá **URL de fim de sessão** caixa de texto.
   
    m. No Olá **erro URL**, copiar o **URL de instância do Marketo** e clique em **guardar** botão toosave definições.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. tooenable Olá SSO para os utilizadores, Olá concluída seguintes ações:
   
    a. Inicie sessão na aplicação tooMarketo com credenciais do administrador.
   
    b. Clique em Olá **Admin** botão no painel de navegação superior Olá.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegue toohello **segurança** menu e **definições de início de sessão**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    d. Verifique Olá **requerem SSO** opção e **guardar** Olá definições.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-marketo-test-user"></a>Criar um utilizador de teste do Marketo

Nesta secção, vai criar um utilizador chamado Britta Simon Marketo. Siga estes passos toocreate um utilizador na plataforma do Marketo.

1. Inicie sessão na aplicação tooMarketo com credenciais do administrador.

2. Clique em Olá **Admin** botão no painel de navegação superior Olá.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. Navegue toohello **segurança** menu e **utilizadores e funções**
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. Clique em Olá **convidar novo utilizador** ligação no separador de utilizadores Olá
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. No Olá preenchimento Olá convidar novo utilizador assistente informações a seguir
   
    a. Introduza o utilizador Olá **E-Mail** endereço na caixa de texto Olá
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    b. Introduza Olá **nome próprio** na caixa de texto Olá
   
    c. Introduza Olá **Apelido** na caixa de texto Olá
   
    d. Clique em **Seguinte**

6. No Olá **permissões** separador, selecione de Olá **userRoles** e clique em **seguinte**
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. Clique em Olá **enviar** botão convite de utilizador de Olá toosend
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. Utilizador recebe uma notificação de correio eletrónico Olá e tem tooclick Olá e alterar Olá palavra-passe tooactivate Olá conta da ligação. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooMarketo.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooMarketo, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Marketo**.

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico do Marketo Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Marketo aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

