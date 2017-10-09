---
title: "Tutorial: Integração do Azure Active Directory com InTime | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e InTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 63652f0f098aeac95e89a2500b46a18440e34698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a>Tutorial: Integração do Azure Active Directory com InTime

Neste tutorial, saiba como toointegrate InTime com o Azure Active Directory (Azure AD).

Integrar InTime com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooInTime.
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooInTime (Single Sign-On) com as respetivas contas do Azure AD.
- Pode gerir as contas numa localização central - Olá portal do Azure.

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com InTime tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um InTime-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar InTime da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-intime-from-hello-gallery"></a>Adicionar InTime da Galeria de Olá
tooconfigure Olá integração de InTime com o Azure AD, é necessário tooadd InTime Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd InTime da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![botão de Azure Active Directory Olá][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Painel de aplicações do Olá Enterprise][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![botão de aplicação nova Olá][3]

4. Na caixa de pesquisa de Olá, escreva **InTime**, selecione **InTime** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Na lista de resultados de Olá inTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único

Nesta secção, configure e teste do Azure AD-início de sessão único com InTime com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá InTime é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá InTime tem toobe estabelecida.

No InTime, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com InTime, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste InTime](#create-a-intime-test-user)**  -toohave um homólogo de Britta Simon no InTime é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação InTime.

**tooconfigure do Azure AD-início de sessão único com InTime, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **InTime** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar a ligação de início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. No Olá **domínio InTime e URLs** secção, execute Olá os seguintes passos:

    ![InTime URLs de domínio e única informações de início de sessão](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, tipo Olá URL:`https://intime6.intimesoft.com/mytime/login/login.xhtml`

    b. No Olá **identificador** caixa de texto, tipo Olá URL:`https://auth.intimesoft.com/auth/realms/master`

4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. A aplicação InTime espera asserções de SAML Olá num formato específico, que requer tooadd atributo personalizado mapeamentos tooyour configuração SAML do token de atributos. Olá seguinte captura de ecrã mostra um exemplo para este. Olá valor predefinido de **identificador de utilizador** é **user.userprincipalname** mas InTime espera este toobe mapeado com o endereço de correio eletrónico do utilizador Olá. Para que pode utilizar **user.mail** atributo da lista de Olá ou utilize o valor do atributo adequado Olá com base na configuração da sua organização 

    ![Configurar atributos](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. No Olá **configuração InTime** secção, clique em **configurar InTime** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configuração inTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. tooconfigure-início de sessão único em **InTime** lado, terá de Olá toosend transferido **XML de metadados**, **Sign-Out URL e o único início de sessão no URL do serviço SAML** demasiado[Equipa de suporte inTime](mailto:hdollard@intimesoft.com). Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

   ![Criar um utilizador de teste do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.

    ![botão de adição de Olá](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    a. No Olá **nome** caixa, escreva **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.

    c. Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-intime-test-user"></a>Criar um utilizador de teste InTime

Nesta secção, vai criar um utilizador chamado Britta Simon InTime. Trabalhar com [equipa de suporte InTime](mailto:hdollard@intimesoft.com) tooadd utilizadores Olá plataforma InTime Olá. Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooInTime.

![Atribuir a função de utilizador Olá][200] 

**tooassign Britta Simon tooInTime, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **InTime**.

    ![Olá InTime ligação na lista de aplicações de Olá](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![ligação de "Utilizadores e grupos" Olá][202]

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição de adicionar Olá][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico InTime Olá no painel de acesso de Olá, deve obter a página de início de sessão de Olá da sua aplicação InTime. Clique em Olá **início de sessão** botão, em seguida, uma série de IdPs será apresentada uma lista dos botões. Clique em **nome IDP** fornecido pelo [equipa de suporte InTime](mailto:hdollard@intimesoft.com) toologin na sua aplicação InTime. Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

