---
title: "Tutorial: Integração do Azure Active Directory com DocuSign | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>Tutorial: Integração do Azure Active Directory com DocuSign

Neste tutorial, saiba como toointegrate DocuSign com o Azure Active Directory (Azure AD).

Integrar DocuSign com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooDocuSign
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooDocuSign (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com DocuSign tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um DocuSign-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar DocuSign da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-docusign-from-hello-gallery"></a>Adicionar DocuSign da Galeria de Olá
tooconfigure Olá integração de DocuSign com o Azure AD, é necessário tooadd DocuSign Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd DocuSign da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. Clique em **nova aplicação** botão na parte superior de Olá da caixa de diálogo Olá.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **DocuSign**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. No painel de resultados de Olá, selecione **DocuSign**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com DocuSign com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá DocuSign é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá DocuSign tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no DocuSign.

tooconfigure e teste do Azure AD-início de sessão único com DocuSign, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste DocuSign](#creating-a-docusign-test-user)**  -toohave um homólogo de Britta Simon no DocuSign é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação DocuSign.

**tooconfigure do Azure AD-início de sessão único com DocuSign, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **DocuSign** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base 64)** e, em seguida, guarde o ficheiro de certificado no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. No Olá **DocuSign configuração** secção do portal do Azure, clique em **configurar DocuSign** janela tooopen configurar início de sessão. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**
    
    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. Numa janela do browser web diferente, início de sessão tooyour **portal de administração de DocuSign** como administrador.

6. No menu de navegação de Olá Olá esquerda, clique em **domínios**.
   
    ![Configurar o início de sessão único][51]

7. No painel direito Olá, clique em **afirmação domínio**.
   
    ![Configurar o início de sessão único][52]

8. No Olá **de afirmações de um domínio** caixa de diálogo, no Olá **nome de domínio** caixa de texto, escreva o domínio da sua empresa e, em seguida, clique em **afirmação**. Certifique-se que verifique o domínio de Olá e estado de Olá está ativo.
   
    ![Configurar o início de sessão único][53]

9. No menu no lado esquerdo Olá, clique em **fornecedores de identidade**  
   
    ![Configurar o início de sessão único][54]
10. No painel direito Olá, clique em **Adicionar fornecedor de identidade**. 
   
    ![Configurar o início de sessão único][55]

11. No Olá **as definições do fornecedor de identidade** página, execute Olá os seguintes passos:
   
    ![Configurar o início de sessão único][56]

    a. No Olá **nome** caixa de texto, escreva um nome exclusivo para a sua configuração. Não utilize espaços.

    b. Colar **ID de entidade de SAML** para Olá **emissor do fornecedor de identidade** caixa de texto.

    c. Colar **único início de sessão no URL do serviço SAML** para Olá **URL de início de sessão do fornecedor de identidade** caixa de texto.

    d. Colar **Sign-Out URL** para Olá **URL de fim de sessão do fornecedor de identidade** caixa de texto.

    e. Selecione **assinar pedido AuthN**.

    f. Como **AuthN enviar pedido pelo**, selecione **POST**.

    g. Como **envio fim de sessão pedido pelo**, selecione **obter**.

12. No Olá **mapeamento de atributos personalizado** secção, escolha o campo de Olá pretende toomap com afirmações do Azure AD. Neste exemplo, Olá **emailaddress** afirmação está mapeada com o valor Olá **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**. Este é o nome de afirmação de predefinido de Olá do Azure AD para afirmações de e-mail. 
   
    > [!NOTE]
    > Olá de utilização adequado **identificador de utilizador** utilizador de Olá toomap do mapeamento de utilizador de tooDocuSign do Azure AD. Selecione Olá campo adequado e introduza o valor adequado Olá com base nas definições da sua organização.
          
    ![Configurar o início de sessão único][57]

13. No Olá **certificado do fornecedor de identidade** secção, clique em **adicionar certificado**e, em seguida, carregue o certificado de Olá transferiu a partir do portal do Azure AD.   
   
    ![Configurar o início de sessão único][58]

14. Clique em **Guardar**.

15. No Olá **fornecedores de identidade** secção, clique em **ações**e, em seguida, clique em **pontos finais**.   
   
    ![Configurar o início de sessão único][59]
 
16. No Olá **ver SAML 2.0 pontos finais** secção no **portal de administração de DocuSign**, efetuar Olá os seguintes passos:
   
    ![Configurar o início de sessão único][60]
   
    a. Olá cópia **URL do emissor de fornecedor de serviço**e, em seguida, cole Olá **identificador** caixa de texto no **DocuSign domínio e os URLs** secção Olá Olá seguinte de portal do Azure padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.
   
    b. Olá cópia **URL de início de sessão do fornecedor de serviço**e, em seguida, cole Olá **URL de início de sessão** caixa de texto no **DocuSign domínio e os URLs** secção Olá Olá seguinte de portal do Azure padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.

    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  Clique em **fechar**
    
17. No portal do Azure Olá, clique em **guardar**.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. Na parte superior de Olá da caixa de diálogo Olá, clique em **adicionar** tooopen Olá **utilizador** caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-docusign-test-user"></a>Criar um utilizador de teste DocuSign

Aplicação suporta **apenas no tempo de aprovisionamento de utilizador** e depois dos utilizadores de autenticação são criados na aplicação Olá automaticamente.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooDocuSign de acesso.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooDocuSign, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **DocuSign**.

    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de DocuSign Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour DocuSign aplicação.
Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar o aprovisionamento de utilizadores](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

