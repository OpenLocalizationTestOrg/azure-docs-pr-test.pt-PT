---
title: "Tutorial: Integração do Azure Active Directory com PlanMyLeave | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a>Tutorial: Integração do Azure Active Directory com PlanMyLeave

Neste tutorial, saiba como toointegrate PlanMyLeave com o Azure Active Directory (Azure AD).

Integrar PlanMyLeave com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooPlanMyLeave
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPlanMyLeave (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal de gestão do Azure de Olá

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com PlanMyLeave tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um PlanMyLeave início de sessão único subscrição ativado


> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.


tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar PlanMyLeave da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-


## <a name="adding-planmyleave-from-hello-gallery"></a>Adicionar PlanMyLeave da Galeria de Olá
tooconfigure Olá integração de PlanMyLeave com o Azure AD, é necessário tooadd PlanMyLeave Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd PlanMyLeave da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **PlanMyLeave**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. No painel de resultados de Olá, selecione **PlanMyLeave**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com PlanMyLeave com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá PlanMyLeave é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá PlanMyLeave tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no PlanMyLeave.

tooconfigure e teste do Azure AD-início de sessão único com PlanMyLeave, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave um homólogo de Britta Simon no PlanMyLeave é-lhe representação toohello ligado do Azure AD.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação PlanMyLeave.

**tooconfigure do Azure AD-início de sessão único com PlanMyLeave, execute Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, no Olá **PlanMyLeave** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** página da caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. No Olá **PlanMyLeave domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company-name>.planmyleave.com/Login.aspx`
    
    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company-name>.planmyleave.com`

    > [!NOTE] 
    > Tenha em atenção que estes não são valores reais Olá. Ter tooupdate estes valores com Olá real, inicie sessão no URL e o identificador. Contacte [equipa de suporte de PlanMyLeave](mailto:support@planmyleave.com) tooget estes valores.

4. No Olá **certificado de assinatura de SAML** secção, clique em **criar novo certificado**.

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. No Olá **criar o novo certificado** caixa de diálogo, clique Olá ícone de calendário e selecione um **data de expiração**. Em seguida, clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. No Olá **certificado de assinatura de SAML** secção, selecione **tornar o novo certificado ativa** e clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. No pop-up de Olá **o certificado de Rollover** janela, clique em **OK**.

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. No Olá **PlanMyLeave configuração** secção, clique em **configurar PlanMyLeave** tooopen **configurar início de sessão** janela.

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. Numa janela do browser web diferente, inicie sessão no seu inquilino PlanMyLeave como administrador.

11. Aceda demasiado**a configuração do sistema**. Em seguida, na Olá **gestão de segurança** secção clique **definições da empresa SAML** .

    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. No Olá **SAML definições** secção, clique em ícone do editor.

    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. No Olá **definições de atualização de SAML** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    a.  No Olá **URL de início de sessão** caixa de texto, coloque o valor Olá **único início de sessão no URL do serviço SAML** da janela de configuração de aplicação do Azure AD.

    b.  Abra o ficheiro de certificado transferido no bloco de notas, copie apenas Olá conteúdo entre Olá---começar certificado--- e ---fim certificado----lo na sua área de transferência e, em seguida, cole-toohello **certificado** caixa de texto.

    c. Definir"**está activada**"demasiado"**Sim**".

    d. Clique em **Guardar**.



### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**. 



### <a name="creating-a-planmyleave-test-user"></a>Criar um utilizador de teste PlanMyLeave

o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon PlanMyLeave. PlanMyLeave suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.

Não há nenhum item de ação para si nesta secção. Será criado um novo utilizador durante uma tentativa tooaccess PlanMyLeave se não existir ainda.

> [!NOTE]
> Se precisar de um utilizador de toocreate manualmente, terá de toocontact [equipa de suporte de PlanMyLeave](mailto:support@planmyleave.com).



### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooPlanMyLeave de acesso.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooPlanMyLeave, execute Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **PlanMyLeave**.

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    


### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de PlanMyLeave Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour PlanMyLeave aplicação.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png