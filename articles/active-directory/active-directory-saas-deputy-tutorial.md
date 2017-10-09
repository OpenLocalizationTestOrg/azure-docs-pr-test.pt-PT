---
title: "Tutorial: Integração do Azure Active Directory com Deputy | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Deputy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a>Tutorial: Integração do Azure Active Directory com Deputy

Neste tutorial, saiba como toointegrate Deputy com o Azure Active Directory (Azure AD).

Integrar Deputy com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooDeputy
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooDeputy (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Deputy tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Deputy-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Deputy da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-deputy-from-hello-gallery"></a>Adicionar Deputy da Galeria de Olá
tooconfigure Olá integração de Deputy com o Azure AD, é necessário tooadd Deputy Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Deputy da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Deputy**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. No painel de resultados de Olá, selecione **Deputy**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Deputy com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Deputy é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Deputy tem toobe estabelecida.

No Deputy, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Deputy, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Deputy](#creating-a-deputy-test-user)**  -toohave um homólogo de Britta Simon no Deputy é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Deputy.

**tooconfigure do Azure AD-início de sessão único com Deputy, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Deputy** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. No Olá **Deputy domínio e os URLs** secção, se desejar aplicação Olá tooconfigure **IDP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. Verifique **Mostrar avançadas definições de URL**. Se desejar aplicação Olá tooconfigure **SP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<your-subdomain>.<region>.deputy.com`
    
    >[!NOTE]
    > Sufixo de região Deputy é opcional, ou deve utilizar um destes: au | na | eu | como | la | af | um | ente au | ente na | ente eu | ente-como | Ente-la | Ente af | um Ente

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão. Contacte [equipa de suporte de Deputy](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget estes valores. 

5. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. No Olá **Deputy configuração** secção, clique em **configurar Deputy** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. Navegue toohello seguinte URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config). Aceda demasiado**definições de segurança** e clique em **editar**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. Neste **definições de segurança** página, execute passos abaixo.

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    a. Ativar **início de sessão de redes Social**.
   
    b. Abra o certificado codificado em Base64 transferido a partir do portal do Azure no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **OpenSSL certificado** caixa de texto.
   
    c. Na caixa de texto de SAML SSO URL Olá, escreva`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`
    
    d. Na caixa de texto de SAML SSO URL Olá, substitua `<your subdomain>` com o subdomínio.
   
    e. Na caixa de texto de SAML SSO URL Olá, substitua `<saml sso url>` com Olá **único início de sessão no URL do serviço SAML** copiou do Olá portal do Azure.
   
    f. Clique em **guardar definições**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-deputy-test-user"></a>Criar um utilizador de teste Deputy

tooenable do Azure AD os utilizadores toolog no tooDeputy, estes têm de ser aprovisionados para Deputy. Em caso de Deputy, o aprovisionamento é uma tarefa manual.

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision uma conta de utilizador, execute Olá os seguintes passos:
1. Inicie sessão no site da empresa tooyour Deputy como administrador.

2. No painel de navegação superior Olá, clique em **pessoas**.
   
   ![As pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "pessoas")

3. Clique em Olá **adicionar pessoas** botão e clique em **adicionar uma única pessoa**.
   
   ![Adicionar pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "adicionar pessoas")

4. Efetuar Olá os passos seguintes e clique em **Guardar & convidar**.
   
   ![Novo utilizador](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "novo utilizador")

   a. No Olá **nome** caixa de texto, nome do tipo de utilizador de Olá como **BrittaSimon**.
   
   b. No Olá **E-Mail** caixa de texto, endereço de correio eletrónico de Olá de tipo de uma conta do Azure AD que pretende tooprovision.
   
   c. No Olá **funcionam ao** caixa de texto, o nome do tipo Olá empresariais.
   
   d. Clique em **Guardar & convidar** botão.

5. o marcador de posição do Olá AAD conta recebe uma mensagem de e-mail e segue um tooconfirm ligação respetiva conta para ficar ativa. Pode utilizar quaisquer outras Deputy utilizador conta criação ferramentas ou APIs fornecidas pelo Deputy tooprovision AAD contas de utilizador.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooDeputy.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooDeputy, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Deputy**.

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.

Ao clicar Olá Deputy na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour Deputy aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

