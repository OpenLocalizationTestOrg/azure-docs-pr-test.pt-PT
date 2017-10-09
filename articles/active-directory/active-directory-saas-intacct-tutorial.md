---
title: "Tutorial: Integração do Azure Active Directory com Intacct | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a>Tutorial: Integração do Azure Active Directory com Intacct

Neste tutorial, saiba como toointegrate Intacct com o Azure Active Directory (Azure AD).

Integrar Intacct com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooIntacct
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooIntacct (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Intacct tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Intacct-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Intacct da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-intacct-from-hello-gallery"></a>Adicionar Intacct da Galeria de Olá
tooconfigure Olá integração de Intacct com o Azure AD, é necessário tooadd Intacct Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Intacct da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Intacct**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. No painel de resultados de Olá, selecione **Intacct**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Intacct com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Intacct é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Intacct tem toobe estabelecida.

No Intacct, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Intacct, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Intacct](#creating-an-intacct-test-user)**  -toohave um homólogo de Britta Simon no Intacct é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Intacct.

**tooconfigure do Azure AD-início de sessão único com Intacct, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Intacct** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. No Olá **Intacct domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > Este valor não é real. Atualize este valor com o URL de resposta real Olá. Contacte [equipa de suporte de Intacct](https://us.intacct.com/support) tooget este valor.

4. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. No Olá **Intacct configuração** secção, clique em **configurar Intacct** tooopen **configurar início de sessão** janela. Olá cópia **ID de entidade de SAML e único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da empresa tooyour Intacct como administrador.

8. Clique em Olá **empresa** separador e, em seguida, clique em **informações da empresa**.

    ![Empresa](./media/active-directory-saas-intacct-tutorial/ic790037.png "empresa")

9. Clique em Olá **segurança** separador e, em seguida, clique em **editar**.

    ![Segurança](./media/active-directory-saas-intacct-tutorial/ic790038.png "segurança")

10. No Olá **início de sessão (SSO) único** secção, execute Olá os seguintes passos:

    ![Início de sessão único](./media/active-directory-saas-intacct-tutorial/ic790039.png "início de sessão único")

    a. Selecione **ativar o início de sessão único em**.

    b. Como **tipo de fornecedor de identidade**, selecione **SAML 2.0**.

    c. No **URL do emissor** caixa de texto, colar Olá valor **ID de entidade de SAML** que copiou do portal do Azure.
   
    d. No **URL de início de sessão** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.

    e. Abra o **base-64** codificado certificado no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado** caixa.
   
    f. Clique em **Guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-intacct-test-user"></a>Criar um utilizador de teste Intacct

tooset cópias de segurança utilizadores do Azure AD, para poderem iniciar sessão tooIntacct, estes têm de ser aprovisionados para Intacct. Intacct, o aprovisionamento é uma tarefa manual.

**contas de utilizador tooprovision, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **Intacct** inquilino.

2. Clique em Olá **empresa** separador e, em seguida, clique em **utilizadores**.

    ![Os utilizadores](./media/active-directory-saas-intacct-tutorial/ic790041.png "utilizadores")
3. Clique em Olá **adicionar** separador.

    ![Adicionar](./media/active-directory-saas-intacct-tutorial/ic790042.png "adicionar")
4. No Olá **informações do utilizador** secção, execute Olá os seguintes passos:

    ![Informações do utilizador](./media/active-directory-saas-intacct-tutorial/ic790043.png "informações do utilizador")

    a. Introduza Olá **ID de utilizador**, Olá **Apelido**, **nome próprio**, Olá **endereço de correio eletrónico**, Olá **título**, e Olá **Phone** de uma conta do Azure AD que pretenda tooprovision incorporar Olá **informações do utilizador** secção.

    b. Selecione Olá **privilégios de administrador** de uma conta do Azure AD que pretende que o tooprovision.
   
    c. Clique em **Guardar**. titular da conta do Olá do Azure AD recebe uma mensagem de e-mail e segue um tooconfirm ligação respetiva conta para ficar ativa.

>[!NOTE]
>tooprovision contas de utilizador do Azure AD, pode utilizar outras ferramentas de criação de conta de utilizador Intacct ou APIs fornecidas pelo Intacct.
        
### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooIntacct.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooIntacct, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Intacct**.

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, teste configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de Intacct Olá no painel de acesso de Olá, esta deve ser iniciada automaticamente no tooyour Intacct aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

