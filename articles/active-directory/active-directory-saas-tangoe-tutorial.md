---
title: "Tutorial: Integração do Azure Active Directory com Tangoe comando Premium Mobile | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Tangoe comando Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a>Tutorial: Integração do Azure Active Directory com Tangoe comando Premium Mobile

Neste tutorial, saiba como toointegrate Tangoe comando Premium Mobile com o Azure Active Directory (Azure AD).

Integrar Tangoe comando Premium Mobile com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooTangoe comando Premium Mobile
- Pode ativar a utilizadores tooautomatically get com sessão iniciada tooTangoe comando Premium Mobile (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Tangoe comando Premium Mobile tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Tangoe comando Premium Mobile-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Tangoe comando Premium móveis a partir da Galeria de Olá
2. Configurar e testar o Azure AD-início de sessão único

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a>Adicionar Tangoe comando Premium móveis a partir da Galeria de Olá
tooconfigure Olá integração de Tangoe comando Premium Mobile com o Azure AD, é necessário tooadd Tangoe comando Premium Mobile Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Tangoe comando Premium Mobile da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Tangoe comando Premium Mobile**, selecione **Tangoe comando Premium Mobile** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Adicionar Tangoe comando Premium móveis a partir da Galeria ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único
Nesta secção, configure e teste do Azure AD-início de sessão único com Tangoe comando Premium móvel com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Tangoe comando Premium Mobile é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Tangoe comando Premium Mobile tem toobe estabelecida.

No Tangoe comando Premium Mobile, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Tangoe comando Premium móveis, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Tangoe comando Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave um homólogo de Britta Simon no Tangoe comando Premium móvel que é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação móvel do Tangoe comando Premium.

**tooconfigure do Azure AD-início de sessão único com Tangoe comando Premium Mobile, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Tangoe comando Premium Mobile** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Baseados em SAML início de sessão](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. No Olá **Tangoe comando Premium Mobile domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Comando Tangoe Premium móveis domínio e os URLs](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://sso.tangoe.com/sp/ACS.saml2`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o URL de resposta real Olá e o URL de início de sessão. Contacte [equipa de suporte de cliente de Mobile Tangoe comando Premium](https://www.tangoe.com/contact-2/) tooget estes valores. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![Secção de certificado de assinatura de SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. Clique em **guardar** botão.

    ![botão Guardar](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. No Olá **Tangoe comando Premium Mobile configuração** secção, clique em **configurar Tangoe comando Premium Mobile** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Secção de configuração de móvel Tangoe comando Premium](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. tooget SSO configurado para a sua aplicação, contacte o seu [equipa de suporte de cliente de Mobile Tangoe comando Premium](https://www.tangoe.com/contact-2/) e fornece Olá seguinte:

   - ficheiro de metadados transferido Olá
   - Olá **ID de entidade de SAML**
   - Olá **único início de sessão no URL do serviço SAML**
   - Olá **Sign-Out URL**

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Utilizadores e grupos -> todos os utilizadores](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Adicionar utilizador](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Página de caixa de diálogo de utilizador](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a>Criar um utilizador de teste Tangoe comando Premium Mobile

Nesta secção, vai criar um utilizador chamado Britta Simon Tangoe comando Premium Mobile. 

Aplicação Tangoe comando Premium Mobile tem todos os Olá utilizadores toobe aprovisionados na aplicação Olá antes de efetuar início de sessão único. Por isso, consulte o trabalho com Olá [equipa de suporte de cliente de Mobile Tangoe comando Premium](https://www.tangoe.com/contact-2/) tooprovision todos os estes utilizadores numa aplicação Olá. 

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooTangoe comando Premium Mobile.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooTangoe comando Premium Mobile, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Tangoe comando Premium Mobile**.

    ![Tangoe comando Premium Mobile na lista de aplicações](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração de SSO do Azure AD utilizando Olá painel de acesso.

Ao clicar em mosaico de Tangoe comando Premium Mobile Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour aplicação Tangoe comando Premium Mobile. Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

