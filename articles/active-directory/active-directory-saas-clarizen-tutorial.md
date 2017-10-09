---
title: "Tutorial: Integração do Azure Active Directory com Clarizen | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Clarizen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>Tutorial: Integração do Azure Active Directory com Clarizen

Neste tutorial, saiba como toointegrate do Azure Active Directory (Azure AD) com Clarizen. Este fornecem integração Olá os seguintes benefícios:

- Pode controlar, no Azure AD, que tenha acesso tooClarizen.
- Pode ativar a sua toobe utilizadores iniciada automaticamente no tooClarizen (-início de sessão único) com as respetivas contas do Azure AD.
- Pode gerir as contas numa localização central, Olá portal do Azure.

cenário de Olá deste tutorial consiste em duas tarefas principais:

1. Adicione Clarizen da Galeria de Olá.
2. Configurar e testar o Azure AD-início de sessão único.

Se pretender obter mais detalhes sobre o software como uma integração de aplicação de serviço (SaaS) com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
integração do Azure AD com Clarizen tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Uma subscrição de Clarizen está ativada para o início de sessão único

passos de Olá tootest neste tutorial, siga estas recomendações:

- Teste do Azure AD-início de sessão único num ambiente de teste. Não utilize o seu ambiente de produção, a menos que isto é necessário.
- Se não tiver um ambiente de teste do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="add-clarizen-from-hello-gallery"></a>Adicionar Clarizen da Galeria de Olá
integração de Olá tooconfigure de Clarizen com o Azure AD, adicione Clarizen Olá Galeria tooyour na lista de aplicações SaaS geridas.

1. No Olá [portal do Azure](https://portal.azure.com), no Olá painel esquerdo, clique em Olá **do Azure Active Directory** ícone.

    ![Ícone do Active Directory do Azure][1]

2. Clique em **aplicações empresariais**. Em seguida, clique em **todas as aplicações**.

    ![Ao clicar em "As aplicações empresariais" e "Todas as aplicações"][2]

3. Clique em Olá **adicionar** botão na parte superior de Olá Olá da caixa de diálogo.

    ![botão de "Adicionar" Olá][3]

4. Na caixa de pesquisa de Olá, escreva **Clarizen**.

    ![Escrever "Clarizen" na caixa de pesquisa de Olá](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. No painel de resultados de Olá, selecione **Clarizen**e, em seguida, clique em **adicionar** aplicação de Olá tooadd.

    ![Selecionar Clarizen no painel de resultados de Olá](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único
Olá secções a seguir, configure e teste do Azure AD-início de sessão único com Clarizen com base no utilizador de teste de Olá Britta Simon.

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Clarizen é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Clarizen tem toobe estabelecida. Estabelecer esta relação de ligação ao atribuir o valor Olá **nome de utilizador** no Azure AD como valor Olá **Username** no Clarizen.

tooconfigure e teste do Azure AD-início de sessão único com Clarizen, Olá concluída blocos modulares os seguintes:

1. **[Configurar o Azure AD-início de sessão único](#configure-azure-ad-single-sign-on)**  tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Clarizen](#create-a-clarizen-test-user)**  toohave um homólogo de Britta Simon no Clarizen é-lhe representação toohello ligado do Azure AD.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único
Ativar o Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Clarizen.

1. No Olá portal do Azure, no Olá **Clarizen** página de integração de aplicações, clique em **de sessão único-**.

    ![Ao clicar em "Single sign-on"][4]

2. No Olá **de sessão único-** caixa de diálogo, para **modo**, selecione **baseados em SAML início de sessão** tooenable-início de sessão único.

    ![Selecionar "baseados em SAML início de sessão"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. No Olá **Clarizen domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Caixas de URL de identificador e resposta](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. No Olá **identificador** caixa, valor de tipo de Olá como: **Clarizen**

    b. No Olá **URL de resposta** caixa, escreva um URL utilizando Olá seguir o padrão: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > Estes não são valores reais Olá. Ter toouse Olá real identificador e o URL de resposta. Aqui sugerimos que utilizar Olá valor exclusivo de uma cadeia como Olá identificador. tooget Olá valores reais, Olá contacto [equipa de suporte de Clarizen](https://success.clarizen.com/hc/en-us/requests/new).

4. No Olá **certificado de assinatura de SAML** secção, clique em **criar novo certificado**.

    ![Clicar em "Criar o novo certificado"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. No Olá **criar o novo certificado** diálogo caixa, clique Olá ícone de calendário e selecione uma data de expiração. Em seguida, clique em **Guardar**.

    ![Selecionar e guardar uma data de expiração](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. No Olá **certificado de assinatura de SAML** secção, selecione **tornar o novo certificado ativa**e, em seguida, clique em **guardar**.

    ![Selecionar Olá caixa de verificação para efetuar o novo certificado de Olá Active Directory](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. No Olá **o certificado de Rollover** caixa de diálogo, clique em **OK**.

    ![Ao clicar em "OK" tooconfirm que pretende que o certificado de Olá toomake Active Directory](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Transferência de Olá de toostart do clicando em "Certificate (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. No Olá **Clarizen configuração** secção, clique em **configurar Clarizen** tooopen Olá **configurar início de sessão** janela.

    ![Clicar em "Configurar Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Janela "Configurar o início de sessão", incluindo URLs e ficheiros](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. Numa janela do browser web diferente, inicie sessão no site da empresa tooyour Clarizen como administrador.

11. Clique em seu nome de utilizador e, em seguida, clique em **definições**.

    ![Ao clicar em "Definições" em seu nome de utilizador](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "definições")

12. Clique em Olá **definições globais** separador. Em seguida, seguinte demasiado**autenticação federada**, clique em **editar**.

    ![Separador "Definições globais"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "definições globais")

13. No Olá **autenticação federada** diálogo caixa, execute Olá os seguintes passos:

    ![Caixa de diálogo "Autenticação federada"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "autenticação federada")

    a. Selecione **ativar federado autenticação**.

    b. Clique em **carregar** tooupload o certificado transferido.

    c. No Olá **URL de início de sessão** box, introduza o valor Olá **único início de sessão no URL do serviço SAML** da janela de configuração de aplicação Olá do Azure AD.

    d. No Olá **Sign-out URL** box, introduza o valor Olá **Sign-Out URL** da janela de configuração de aplicação Olá do Azure AD.

    e. Selecione **utilizar POST**.

    f. Clique em **Guardar**.

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
Olá portal do Azure, crie um utilizador de teste chamado Britta Simon.

![Endereço de correio eletrónico e o nome de utilizador de teste de Olá do Azure AD][100]

1. No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** ícone.

    ![Ícone do Active Directory do Azure](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. Clique em **utilizadores e grupos**e, em seguida, clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.

    ![Ao clicar em "Utilizadores e grupos" e "Todos os utilizadores"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. Na parte superior de Olá Olá da caixa de diálogo, clique em **adicionar** tooopen Olá **utilizador** caixa de diálogo.

    ![botão de "Adicionar" Olá](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:

    ![Caixa de diálogo "Utilizador" com o nome, endereço de correio eletrónico e palavra-passe preenchidos](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. No Olá **nome** caixa, escreva **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa, endereço de correio eletrónico do tipo Olá de Olá conta Britta Simon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá **palavra-passe**.

    d. Clique em **Criar**.

### <a name="create-a-clarizen-test-user"></a>Criar um utilizador de teste Clarizen
toosign de utilizadores do Azure AD tooenable no tooClarizen, terá de aprovisionar contas de utilizador. No caso de Olá da Clarizen, o aprovisionamento é uma tarefa manual.

1. Inicie sessão no tooyour Clarizen site da empresa como administrador.

2. Clique em **pessoas**.

    ![Clicar em "As pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "pessoas")

3. Clique em **convidar utilizador**.

    ![Botão "Convidar utilizadores"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "convidar utilizadores")

4. No Olá **convidar pessoas** diálogo caixa, execute Olá os seguintes passos:

    ![Caixa de diálogo "Convidar pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "convidar pessoas")

    a. No Olá **E-Mail** caixa, endereço de correio eletrónico do tipo Olá de Olá conta Britta Simon.

    b. Clique em **convidar**.

    > [!NOTE]
    > titular de conta do Azure Active Directory Olá irá receber um e-mail e siga a tooconfirm uma ligação a respetiva conta para ficar ativa.

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD
Ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooClarizen de acesso.

![Utilizador de teste atribuído][200]

1. No portal do Azure Olá, abra a vista de aplicações de Olá, procurar toohello vista de diretório, clique em **aplicações empresariais**e, em seguida, clique em **todas as aplicações**.

    ![Ao clicar em "As aplicações empresariais" e "Todas as aplicações"][201]

2. Na lista de aplicações de Olá, selecione **Clarizen**.

    ![Selecionar Clarizen na lista de Olá](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. No painel esquerdo Olá, clique em **utilizadores e grupos**.

    ![Ao clicar em "Utilizadores e grupos"][202]

4. Clique em Olá **adicionar** botão. Em seguida, no Olá **adicionar atribuição** caixa de diálogo, selecione **utilizadores e grupos**.

    ![botão de "Adicionar" Olá e a caixa de diálogo de "Adicionar atribuição" Olá][203]

5. No Olá **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de Olá de utilizadores.

6. No Olá **utilizadores e grupos** caixa de diálogo, clique em Olá **selecione** botão.

7. No Olá **adicionar atribuição** caixa de diálogo, clique em Olá **atribuir** botão.

### <a name="test-single-sign-on"></a>Teste o início de sessão único
Teste a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de Clarizen Olá no painel de acesso de Olá, esta deve ser iniciada automaticamente no tooyour Clarizen aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como aplicações de SaaS toointegrate com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
