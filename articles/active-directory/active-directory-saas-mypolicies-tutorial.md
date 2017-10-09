---
title: "Tutorial: Integração do Azure Active Directory com myPolicies | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a>Tutorial: Integração do Azure Active Directory com myPolicies

Neste tutorial, saiba como toointegrate myPolicies com o Azure Active Directory (Azure AD).

Integrar myPolicies com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso toomyPolicies
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada toomyPolicies (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com myPolicies tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um myPolicies-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar myPolicies da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-mypolicies-from-hello-gallery"></a>Adicionar myPolicies da Galeria de Olá
tooconfigure Olá integração de myPolicies com o Azure AD, é necessário tooadd myPolicies Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd myPolicies da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **myPolicies**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. No painel de resultados de Olá, selecione **myPolicies**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com myPolicies com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá myPolicies é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá myPolicies tem toobe estabelecida.

No myPolicies, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com myPolicies, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste myPolicies](#creating-a-mypolicies-test-user)**  -toohave um homólogo de Britta Simon no myPolicies é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação myPolicies.

**tooconfigure do Azure AD-início de sessão único com myPolicies, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **myPolicies** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. No Olá **myPolicies domínios e URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.mypolicies.com/`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o URL de identificador e resposta real no Olá. Contacte [myPolicies suporta equipa](mailto:support@mypolicies.com) tooget estes valores.

4. aplicação de myPolicies Olá espera asserções de SAML Olá num formato específico, que requer tooadd atributo personalizado mapeamentos tooyour configuração SAML do token de atributos. Configure Olá seguintes afirmações para esta aplicação. Pode gerir os valores de Olá destes atributos a partir de Olá "**atributos de utilizador**" secção na página de integração de aplicações. Olá seguinte captura de ecrã mostra um exemplo para este. 

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. Clique em **ver e editar todos os outros atributos de utilizador** caixa de verificação no Olá **atributos de utilizador** secção atributos de Olá tooexpand. Efetuar Olá os seguintes passos em cada um dos atributos de Olá apresentado-

    | Nome do atributo | Valor do atributo |
    | ------------------- | ---------- |
    | givenName | User.givenName |
    | Apelido | User.Surname |
    | endereço de correio eletrónico | User.Mail |
    | nome | User.userPrincipalName |
    
    a. Clique em Olá do Olá atributo tooopen **Editar atributo** caixa de diálogo.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    b. Eliminar o valor do URL de Olá da Olá **espaço de nomes**.
    
    c. Clique em **Ok** definição de Olá toosave.
    
6. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. No Olá **myPolicies configuração** secção, clique em **configurar myPolicies** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. tooconfigure-início de sessão único em **myPolicies** lado, terá de Olá toosend transferido **Certificate(Base64)** e **único início de sessão no URL do serviço SAML** demasiado[myPolicies suporta equipa](mailto:support@mypolicies.com). 

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-mypolicies-test-user"></a>Criar um utilizador de teste myPolicies

Nesta secção, vai criar um utilizador chamado Britta Simon myPolicies. Trabalhar com [myPolicies suporta equipa](mailto:support@mypolicies.com) para adicionar utilizadores de Olá na plataforma de myPolicies Olá. Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso toomyPolicies.

![Atribua o utilizador][200] 

**tooassign Britta Simon toomyPolicies, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **myPolicies**.

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá myPolicies na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour myPolicies aplicação.
Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

