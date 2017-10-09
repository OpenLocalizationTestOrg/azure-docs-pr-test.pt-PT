---
title: "Tutorial: Integração do Azure Active Directory com Rightscale | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre Rightscale e o Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a>Tutorial: Integração do Azure Active Directory com Rightscale

Neste tutorial, saiba como toointegrate Rightscale com o Azure Active Directory (Azure AD).

Integrar Rightscale com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooRightscale
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooRightscale (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Rightscale tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Rightscale-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Rightscale da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-rightscale-from-hello-gallery"></a>Adicionar Rightscale da Galeria de Olá
tooconfigure Olá integração de Rightscale com o Azure AD, é necessário tooadd Rightscale Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Rightscale da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Rightscale**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. No painel de resultados de Olá, selecione **Rightscale**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Rightscale com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Rightscale é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Rightscale tem toobe estabelecida.

No Rightscale, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Rightscale, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Rightscale](#creating-a-rightscale-test-user)**  -toohave um homólogo de Britta Simon no Rightscale é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Rightscale.

**tooconfigure do Azure AD-início de sessão único com Rightscale, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Rightscale** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. No Olá **domínio Rightscale e URLs** secção, se desejar aplicação Olá tooconfigure **IDP iniciada modo** não dispõe de tooperform quaisquer passos conforme Olá aplicação já está pré-integrada com o Azure.

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. No Olá **domínio Rightscale e URLs** secção, se desejar aplicação Olá tooconfigure **SP iniciada modo**, efetuar Olá os seguintes passos:
    
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    a. Clique em Olá **Mostrar avançadas definições de URL**.

    b. No Olá **URL de início de sessão** caixa de texto, tipo Olá URL:`https://login.rightscale.com/`

5. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. No Olá **Rightscale configuração** secção, clique em **configurar Rightscale** tooopen **configurar início de sessão** janela. Olá cópia **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS>
8. tooget SSO configurado para a sua aplicação, terá de toosign no tooyour RightScale inquilino como administrador.

    a. No menu de Olá na parte superior do Olá, clique em Olá **definições** separador e selecione **Single Sign-On**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    b. Clique em Olá "**novo**" botão tooadd **fornecedores de identidade do seu SAML**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    c. Na caixa de texto Olá de **nome a apresentar**, introduza o nome da sua empresa.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    d. Selecione **SSO iniciado por permitir RightScale utilizando uma sugestão de deteção** e entrada sua **nome de domínio** no Olá abaixo caixa de texto.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    e. Colar o valor Olá **único início de sessão no URL do serviço SAML** que copiou do portal do Azure para **SAML SSO Endpoint** no RightScale.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    f. Colar o valor Olá **ID de entidade de SAML** que copiou do portal do Azure para **SAML EntityID** no RightScale.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    g. Clique em **Browser** botão tooupload Olá certificado que transferiu a partir do portal do Azure.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    h. Clique em **Guardar**.
<CE>
> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-rightscale-test-user"></a>Criar um utilizador de teste Rightscale

Nesta secção, vai criar um utilizador chamado Britta Simon RightScale. Trabalhar com [equipa de suporte de cliente Rightscale](mailto:support@rightscale.com) utilizadores de Olá tooadd na plataforma de RightScale Olá.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooRightscale.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooRightscale, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Rightscale**.

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.  

Ao clicar em mosaico de RightScale Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour RightScale aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

