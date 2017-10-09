---
title: "Tutorial: Integração do Azure Active Directory com ITRP | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a>Tutorial: Integração do Azure Active Directory com ITRP

Neste tutorial, saiba como toointegrate ITRP com o Azure Active Directory (Azure AD).

Integrar ITRP com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooITRP
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooITRP (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com ITRP tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um ITRP-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar ITRP da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-itrp-from-hello-gallery"></a>Adicionar ITRP da Galeria de Olá
tooconfigure Olá integração de ITRP no tooAzure AD, é necessário tooadd ITRP Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd ITRP da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **ITRP**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. No painel de resultados de Olá, selecione **ITRP**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-

Nesta secção, configure e teste do Azure AD-início de sessão único com ITRP com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá ITRP é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá ITRP tem toobe estabelecida.

No ITRP, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com ITRP, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um ITRP utilizador de teste](#creating-an-itrp-test-user)**  -toohave um homólogo de Britta Simon no ITRP é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação ITRP.

**tooconfigure do Azure AD-início de sessão único com ITRP, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **ITRP** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. No Olá **ITRP domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.itrp.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.itrp.com`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente ITRP](https://www.itrp.com/support) tooget estes valores. 
 
4. No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado.

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. No Olá **ITRP configuração** secção, clique em **configurar ITRP** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML e o URL de Sign-Out** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da empresa tooyour ITRP como administrador.

8. Na barra de ferramentas Olá na parte superior do Olá, clique em **definições**.
   
    ![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")

8. No painel de navegação esquerdo Olá, selecione **Single Sign-On**.
   
    ![De sessão único-](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")

9. Na secção de configuração Single Sign-On Olá, efetue Olá os seguintes passos:
   
    ![De sessão único-](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")
    
    ![De sessão único-](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")   

    a. Clique em **Ativar**.

    b. No **remoto URL terminar sessão** caixa de texto, colar Olá valor **Sign-Out URL**, que copiou do portal do Azure.

    c. No **SAML SSO URL** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML**, que copiou do portal do Azure.

    d.In **impressão digital do certificado** caixa de texto, colar Olá **Thumbprint** valor do certificado, o qual copiou a partir do portal do Azure. 
      
10. Clique em **Guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-itrp-test-user"></a>Criar um utilizador de teste ITRP

tooenable do Azure AD os utilizadores toolog no tooITRP, estes têm de ser aprovisionados na tooITRP.  

No caso de Olá da ITRP, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **ITRP** inquilino.

2. Na barra de ferramentas Olá na parte superior do Olá, clique em **registos**.
   
    ![Administração](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")

3. No menu de pop-up de Olá, selecione **pessoas**.
   
    ![As pessoas](./media/active-directory-saas-itrp-tutorial/ic775587.png "pessoas")

4. Clique em **Adicionar nova pessoa** ("+").
   
    ![Administração](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")

5. Na caixa de diálogo de adicionar nova pessoa Olá, execute Olá os seguintes passos:
   
    ![Utilizador](./media/active-directory-saas-itrp-tutorial/ic775577.png "utilizador") 
      
    a. Olá tipo **nome**, **E-Mail** de uma conta válida do AAD pretende tooprovision.

    b. Clique em **Guardar**.

>[!NOTE]
>Pode utilizar quaisquer outras ITRP utilizador conta criação ferramentas ou APIs fornecidas pelo ITRP tooprovision contas de utilizador do AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooITRP.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooITRP, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **ITRP**.

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá ITRP na peça de mosaico Olá painel de acesso, pode ser obtido a aplicação de ITRP tooyour automaticamente com sessão iniciada.
Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

