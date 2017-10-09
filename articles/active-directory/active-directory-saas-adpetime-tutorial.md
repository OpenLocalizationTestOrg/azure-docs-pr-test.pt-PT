---
title: "Tutorial: Integração do Azure Active Directory com ADP eTime | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a>Tutorial: Integração do Azure Active Directory com ADP eTime

Neste tutorial, saiba como toointegrate ADP eTime com o Azure Active Directory (Azure AD).

Integrar ADP eTime com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooADP eTime
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooADP eTime (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com ADP eTime tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um ADP eTime-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar ADP eTime da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-adp-etime-from-hello-gallery"></a>Adicionar ADP eTime da Galeria de Olá
tooconfigure Olá integração de ADP eTime com o Azure AD, é necessário tooadd ADP eTime Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd ADP eTime da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **ADP eTime**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. No painel de resultados de Olá, selecione **ADP eTime**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com eTime ADP com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá ADP eTime é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá ADP eTime tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no ADP eTime.

tooconfigure e teste do Azure AD-início de sessão único com ADP eTime, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste de eTime ADP](#creating-an-adp-etime-test-user)**  -toohave um homólogo de Britta Simon no eTime ADP que é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de eTime ADP.

**tooconfigure do Azure AD-início de sessão único com ADP eTime, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **ADP eTime** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. No Olá **ADP eTime domínio e os URLs** secção, execute Olá passo a seguir:

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<servername>.adp.com`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer` 
 
    > [!NOTE] 
    > Estes valores não estiverem Olá real. Atualize estes valores com o URL de resposta real Olá e o identificador. Contacte [equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx) tooget estes valores.

4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. Olá aplicação de eTime ADP espera asserções de SAML Olá num formato específico, que requer tooadd atributo personalizado mapeamentos tooyour configuração SAML do token de atributos. Olá seguinte captura de ecrã mostra um exemplo para este. Olá afirmação nome será sempre **"PersonImmutableID"** e valor Olá que podemos ter mapeado os tooExtensionAttribute2 que contém Olá campo IDdeEmpregado do utilizador Olá. 

    Aqui mapeamento de utilizador de Olá do Azure AD tooADP eTime será efetuado em Olá campo IDdeEmpregado, mas pode mapear este valor diferente de tooa também com base nas suas definições de aplicação. Por isso, consulte o trabalho com [equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx) toouse primeiro Olá identificador correto de um utilizador e esse valor com Olá do mapa **"PersonImmutableID"** de afirmação.

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. No Olá **atributos de utilizador** secção em Olá **de sessão único-** caixa de diálogo, configurar atributos token SAML, conforme mostrado na imagem de Olá e efetuar Olá os seguintes passos:
    
    | Nome do atributo | Valor do atributo |
    | ------------------- | -------------------- |    
    | PersonImmutableID | User.extensionattribute2 |
    
    a. Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    b. No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.

    c. De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.
    
    d. Clique em **OK**.

    > [!NOTE] 
    > Antes de poder configurar de asserção SAML Olá, terá de toocontact sua [equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx) e valor de Olá do atributo de identificador exclusivo de Olá de pedido para o seu inquilino. É necessário este valor tooconfigure Olá afirmação personalizada para a sua aplicação. 

7. No Olá **ADP eTime configuração** secção, clique em **configurar ADP eTime** tooopen **configurar início de sessão** janela.

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. tooconfigure-início de sessão único em **ADP eTime** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx). 

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-adp-etime-test-user"></a>Criar um utilizador de teste de eTime ADP

o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon ADP eTime. Trabalhar com [equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx) utilizadores de Olá tooadd na conta de eTime Olá ADP. 
   
### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooADP eTime.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooADP eTime, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **ADP eTime**.

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de eTime ADP Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour ADP eTime aplicação.
Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

