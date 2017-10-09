---
title: "Tutorial: Integração do Azure Active Directory com EverBridge | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a>Tutorial: Integração do Azure Active Directory com EverBridge

Neste tutorial, saiba como toointegrate EverBridge com o Azure Active Directory (Azure AD).

Integrar EverBridge com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooEverBridge
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooEverBridge (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com EverBridge tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um EverBridge início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar EverBridge da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-everbridge-from-hello-gallery"></a>Adicionar EverBridge da Galeria de Olá
tooconfigure Olá integração de EverBridge com o Azure AD, é necessário tooadd EverBridge Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd EverBridge da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **EverBridge**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. No painel de resultados de Olá, selecione **EverBridge**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com EverBridge com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá EverBridge é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá EverBridge tem toobe estabelecida.

No EverBridge, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com EverBridge, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste EverBridge](#creating-an-everbridge-test-user)**  -toohave um homólogo de Britta Simon no EverBridge é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação EverBridge.

**tooconfigure do Azure AD-início de sessão único com EverBridge, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **EverBridge** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. No Olá **EverBridge domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://sso.everbridge.net/<companyname>`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o URL de identificador e resposta real no Olá. Contacte [equipa de suporte de EverBridge](mailto:support@everbridge.com) tooget estes valores.
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. No Olá **EverBridge configuração** secção, clique em **configurar EverBridge** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. tooget SSO configurado para a sua aplicação, terá de toosign no tooyour Everbridge inquilino como administrador.

7. No menu de Olá na parte superior do Olá, clique em Olá **definições** separador e selecione **Single Sign-On** em **segurança**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    a. No Olá **nome** caixa de texto, nome de Olá de tipo de identificador do fornecedor (por exemplo: nome da sua empresa).
   
    b. No Olá **nome API** caixa de texto, nome do tipo Olá da API.
   
    c. Clique em **Escolher ficheiro** botão tooupload Olá ficheiro de metadados do que transferiu a partir do portal do Azure.
   
    d. Na localização de identidade de SAML Olá, selecione **é de identidade no elemento de NameIdentifier Olá do Olá instrução requerente**.
   
    e. No Olá **URL de início de sessão do fornecedor de identidade** caixa de texto, colar Olá valor do URL de SSO de SAML do Azure AD.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    f. No Olá fornecedor iniciada pedido vínculo de serviço, selecione **redirecionamento de HTTP**.

    g. Clique em **guardar**

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-everbridge-test-user"></a>Criar um utilizador de teste EverBridge

Nesta secção, vai criar um utilizador chamado Britta Simon Everbridge. Trabalhar com [equipa de suporte de EverBridge](mailto:support@everbridge.com) utilizadores de Olá tooadd na plataforma de Everbridge Olá.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooEverBridge.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooEverBridge, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **EverBridge**.

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.

Ao clicar em mosaico de Everbridge Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Everbridge aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

