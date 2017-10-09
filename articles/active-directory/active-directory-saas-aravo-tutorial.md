---
title: "Tutorial: Integração do Azure Active Directory com Aravo | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Aravo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 224939d8-2c9c-4561-968d-62722f5ab5ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 8f1336fa307fa9e8d625440a573d9f9d79dd820b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aravo"></a>Tutorial: Integração do Azure Active Directory com Aravo

Neste tutorial, saiba como toointegrate Aravo com o Azure Active Directory (Azure AD).

Integrar Aravo com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooAravo
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooAravo (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Aravo tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Aravo início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Aravo da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-aravo-from-hello-gallery"></a>Adicionar Aravo da Galeria de Olá
tooconfigure Olá integração de Aravo com o Azure AD, é necessário tooadd Aravo Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Aravo da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Aravo**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_search.png)

5. No painel de resultados de Olá, selecione **Aravo**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Aravo com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Aravo é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Aravo tem toobe estabelecida.

No Aravo, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Aravo, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Aravo](#creating-an-aravo-test-user)**  -toohave um homólogo de Britta Simon no Aravo é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Aravo.

**tooconfigure do Azure AD-início de sessão único com Aravo, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Aravo** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_samlbase.png)

3. No Olá **Aravo domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_url.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.aravo.com`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.aravo.com/aems/login.do`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o URL de identificador e resposta real no Olá. Contacte [equipa de suporte de Aravo](http://www.aravo.com/about-us/contact/) tooget estes valores.
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-aravo-tutorial/tutorial_general_400.png)

6. No Olá **Aravo configuração** secção, clique em **configurar Aravo** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_configure.png) 

7. tooconfigure-início de sessão único em **Aravo** lado, terá de Olá toosend transferido **certificado (Base64)**, **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML**demasiado[equipa de suporte de Aravo](http://www.aravo.com/about-us/contact/). 


> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-aravo-test-user"></a>Criar um utilizador de teste Aravo

o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon Aravo. Trabalhar com [equipa de suporte de Aravo](http://www.aravo.com/about-us/contact/) tooadd utilizadores Olá Olá Aravo conta.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooAravo.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooAravo, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Aravo**.

    ![Configurar o início de sessão único](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest Olá, o Microsoft Azure AD Single Sign-On configuração utilizando o painel de acesso.

Ao clicar em mosaico de Aravo Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Aravo aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_203.png

