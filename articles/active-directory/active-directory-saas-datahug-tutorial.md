---
title: "Tutorial: Integração do Azure Active Directory com Datahug | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a>Tutorial: Integração do Azure Active Directory com Datahug

Neste tutorial, saiba como toointegrate Datahug com o Azure Active Directory (Azure AD).

Integrar Datahug com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooDatahug
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooDatahug (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender que tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo. [O que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Datahug tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Datahug início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Datahug da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-datahug-from-hello-gallery"></a>Adicionar Datahug da Galeria de Olá
tooconfigure Olá integração de Datahug com o Azure AD, é necessário tooadd Datahug Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Datahug da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Datahug**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. No painel de resultados de Olá, selecione **Datahug**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Datahug com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Datahug é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Datahug tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Datahug.

tooconfigure e teste do Azure AD-início de sessão único com Datahug, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Datahug](#creating-a-datahug-test-user)**  -toohave um homólogo de Britta Simon no Datahug é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Datahug.

**tooconfigure do Azure AD-início de sessão único com Datahug, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Datahug** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. No Olá **Datahug domínio e os URLs** secção, se desejar aplicação Olá tooconfigure **IDP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://apps.datahug.com/identity/<uniqueID>`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://apps.datahug.com/identity/<uniqueID>/acs`

4. Verifique **Mostrar avançadas definições de URL**. Se desejar aplicação Olá tooconfigure **SP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    No Olá **URL de início de sessão** caixa de texto, escreva um URL como:`https://apps.datahug.com/`
     
    > [!NOTE] 
    > Estes valores não estiverem Olá real. Atualize estes valores com o URL de identificador e resposta real no Olá. Aqui sugerimos toouse Olá exclusivo valor da cadeia no Olá identificador e o URL de resposta. Contacte [equipa de suporte de cliente Datahug](http://datahug.com/about/contact-us/) tooget estes valores. 

5. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  Verifique **"Mostrar avançadas definições de assinatura de certificado"** e efetuar Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    a. No **assinatura opção**, selecione **asserção SAML de início de sessão**.
    
    b. No **algoritmo de assinatura**, selecione **SHA1**.
 
7. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. No Olá **Datahug configuração** secção, clique em **configurar Datahug** tooopen **configurar início de sessão** janela. Olá cópia **ID de entidade de SAML** e **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. tooconfigure-início de sessão único em **Datahug** lado, terá de Olá toosend transferido **XML de metadados**, **ID de entidade de SAML** e **SAML único início de sessão no serviço URL** demasiado[Datahug suporte](http://datahug.com/about/contact-us/). Se definir esta aplicação Olá toohave corretamente em ambos os lados de ligação de SAML SSO.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-datahug-test-user"></a>Criar um utilizador de teste Datahug

tooenable do Azure AD os utilizadores toolog no tooDatahug, estes têm de ser aprovisionados para Datahug.  
Quando Datahug, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour Datahug site da empresa como administrador.

2. Coloque o cursor sobre Olá **roda dentada** no canto superior direito Olá e clique em **definições**
   
   ![Adicionar empregado](./media/active-directory-saas-datahug-tutorial/1.png)

3. Escolha **pessoas** e clique em Olá **adicionar utilizadores** separador

    ![Adicionar empregado](./media/active-directory-saas-datahug-tutorial/2.png)

4. Tipo de correio eletrónico de Olá de pessoa Olá gostaria toocreate uma conta para e clique em **adicionar**.

    ![Adicionar empregado](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > Pode enviar o registo correio toouser selecionando **enviar correio eletrónico de boas-vindas** caixa de verificação.  
    > Se estiver a criar uma conta do Salesforce não enviar e-mail de boas-vindas Olá.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooDatahug.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooDatahug, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Datahug**.

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.
Ao clicar em mosaico de Datahug Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Datahug aplicação. Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

