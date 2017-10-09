---
title: "Tutorial: Integração do Azure Active Directory com ScreenSteps | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a>Tutorial: Integração do Azure Active Directory com ScreenSteps

Neste tutorial, saiba como toointegrate ScreenSteps com o Azure Active Directory (Azure AD).

Integrar ScreenSteps com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooScreenSteps.
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooScreenSteps (Single Sign-On) com as respetivas contas do Azure AD.
- Pode gerir as contas numa localização central - Olá portal do Azure.

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com ScreenSteps tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um ScreenSteps-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar ScreenSteps da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-screensteps-from-hello-gallery"></a>Adicionar ScreenSteps da Galeria de Olá
tooconfigure Olá integração de ScreenSteps com o Azure AD, é necessário tooadd ScreenSteps Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd ScreenSteps da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![botão de Azure Active Directory Olá][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Painel de aplicações do Olá Enterprise][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![botão de aplicação nova Olá][3]

4. Na caixa de pesquisa de Olá, escreva **ScreenSteps**, selecione **ScreenSteps** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![ScreenSteps na lista de resultados de Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único

Nesta secção, configure e teste do Azure AD-início de sessão único com ScreenSteps com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá ScreenSteps é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá ScreenSteps tem toobe estabelecida.

No ScreenSteps, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com ScreenSteps, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste ScreenSteps](#create-a-screensteps-test-user)**  -toohave um homólogo de Britta Simon no ScreenSteps é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação ScreenSteps.

**tooconfigure do Azure AD-início de sessão único com ScreenSteps, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **ScreenSteps** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar a ligação de início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. No Olá **ScreenSteps domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Domínio ScreenSteps e os URLs únicos de informações de início de sessão](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.ScreenSteps.com`

    > [!NOTE] 
    > Este valor não é real. Atualizar este valor com Olá real início de sessão no URL, que é explicado posteriormente neste tutorial. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. No Olá **ScreenSteps configuração** secção, clique em **configurar ScreenSteps** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configuração de ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa ScreenSteps como administrador.

8. Clique em **definições da conta**.

    ![Gestão de contas](./media/active-directory-saas-screensteps-tutorial/ic778523.png "gestão de contas")

9. Clique em **de sessão único-**.

    ![Autenticação remota](./media/active-directory-saas-screensteps-tutorial/ic778524.png "autenticação remota")

10. Clique em **criar o ponto final de início de sessão único**.

    ![Autenticação remota](./media/active-directory-saas-screensteps-tutorial/ic778525.png "autenticação remota")

11. No Olá **ponto final de início de sessão único criar** secção, execute Olá os seguintes passos:

    ![Criar um ponto final de autenticação](./media/active-directory-saas-screensteps-tutorial/ic778526.png "criar um ponto final de autenticação")
    
    a. No Olá **título** caixa de texto, escreva um título.
    
    b. De Olá **modo** lista, selecione **SAML**.
    
    c. Clique em **Criar**.

12. **Editar** Olá novo ponto final.

    ![Editar endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "editar ponto final")

13. No Olá **ponto final de início de sessão único editar** secção, execute Olá os seguintes passos:

    ![Ponto final de autenticação remota](./media/active-directory-saas-screensteps-tutorial/ic778527.png "ponto final de autenticação remota")

    a. Clique em **carregamento novo ficheiro de certificado de SAML**e, em seguida, carregue Olá certificado, o que transferiu a partir do portal do Azure.
    
    b. Colar **único início de sessão no URL do serviço SAML** valor que copiou do Olá portal do Azure para Olá **URL de início de sessão remoto** caixa de texto.
    
    c. Colar **Sign-Out URL** valor que copiou do Olá portal do Azure para Olá **URL para terminar sessão** caixa de texto.
    
    d. Selecione um **grupo** tooassign utilizadores toowhen terem sido aprovisionados.
    
    e. Clique em **atualização**.

    f. Olá cópia **SAML consumidor URL** toohello área de transferência e cole no toohello **URL de início de sessão** textbox em **ScreenSteps domínio e os URLs** secção.
    
    g. Devolver toohello **ponto final de início de sessão único editar**.
    
    h. Clique em Olá **predefinir para conta** botão toouse este ponto final para todos os utilizadores que inicie sessão no ScreenSteps. Em alternativa, pode clicar em Olá **adicionar tooSite** botão toouse este ponto final para sites específicos de **ScreenSteps**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

   ![Criar um utilizador de teste do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.

    ![botão de adição de Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    a. No Olá **nome** caixa, escreva **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.

    c. Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-screensteps-test-user"></a>Criar um utilizador de teste ScreenSteps

Nesta secção, vai criar um utilizador chamado Britta Simon ScreenSteps. Trabalhar com [equipa de suporte de cliente ScreenSteps](https://www.screensteps.com/contact) para adicionar utilizadores de Olá na plataforma de ScreenSteps Olá. Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único. 

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooScreenSteps.

![Atribuir a função de utilizador Olá][200] 

**tooassign Britta Simon tooScreenSteps, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **ScreenSteps**.

    ![ligação de ScreenSteps Olá na lista de aplicações de Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![ligação de "Utilizadores e grupos" Olá][202]

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição de adicionar Olá][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá ScreenSteps na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour ScreenSteps aplicação.
Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

