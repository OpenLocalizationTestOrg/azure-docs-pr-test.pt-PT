---
title: "Tutorial: Integração do Azure Active Directory com Freshservice | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a>Tutorial: Integração do Azure Active Directory com Freshservice

Neste tutorial, saiba como toointegrate Freshservice com o Azure Active Directory (Azure AD).

Integrar Freshservice com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooFreshservice
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooFreshservice (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Freshservice tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Freshservice início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Freshservice da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-freshservice-from-hello-gallery"></a>Adicionar Freshservice da Galeria de Olá
tooconfigure Olá integração de Freshservice com o Azure AD, é necessário tooadd Freshservice Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Freshservice da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Freshservice**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. No painel de resultados de Olá, selecione **Freshservice**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Freshservice com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Freshservice é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Freshservice tem toobe estabelecida.

No Freshservice, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Freshservice, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Freshservice](#creating-a-freshservice-test-user)**  -toohave um homólogo de Britta Simon no Freshservice é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Freshservice.

**tooconfigure do Azure AD-início de sessão único com Freshservice, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Freshservice** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. No Olá **Freshservice domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<democompany>.freshservice.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<democompany>.freshservice.com`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente Freshservice](https://support.freshservice.com/) tooget estes valores. 
 
4. No Olá **certificado de assinatura de SAML** secção, copie **THUMBPRINT** valor do certificado.

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. No Olá **Freshservice configuração** secção, clique em **configurar Freshservice** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da empresa tooyour Freshservice como administrador.

8. No menu de Olá na parte superior do Olá, clique em **Admin**.
   
    ![Administração](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")

9. No Olá **Portal cliente**, clique em **segurança**.
   
    ![Segurança](./media/active-directory-saas-freshservice-tutorial/ic790815.png "segurança")

10. No Olá **segurança** secção, execute Olá os seguintes passos:
   
    ![Início de sessão único](./media/active-directory-saas-freshservice-tutorial/ic790816.png "início de sessão único")
   
    a. Comutador **início de sessão único**.

    b. Selecione **SAML SSO**.

    c. No Olá **URL de início de sessão SAML** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.

    d. No Olá **URL de fim de sessão** caixa de texto, colar Olá valor **Sign-Out URL** que copiou do portal do Azure.

    e. No **impressão digital do certificado de segurança** caixa de texto, colar Olá **THUMBPRINT** valor do certificado que copiou do portal do Azure.

    f. Clique em **guardar**
   
> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-freshservice-test-user"></a>Criar um utilizador de teste Freshservice

tooenable do Azure AD os utilizadores toolog no tooFreshService, estes têm de ser aprovisionados para FreshService. No caso de Olá da FreshService, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **FreshService** site da empresa como administrador.

2. No menu de Olá na parte superior do Olá, clique em **Admin**.
   
    ![Administração](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")

3. No Olá **gestão de utilizadores** secção, clique em **autores de pedido**.
   
    ![Autores de pedido](./media/active-directory-saas-freshservice-tutorial/ic790818.png "autores de pedido")

4. Clique em **novo solicitador**.
   
    ![Autores de pedido de nova](./media/active-directory-saas-freshservice-tutorial/ic790819.png "autores de pedido de novo")

5. No Olá **novo solicitador** secção, execute Olá os seguintes passos:
   
    ![Novo solicitador](./media/active-directory-saas-freshservice-tutorial/ic790820.png "novo solicitador")   

    a. Introduza Olá **nome próprio** e **E-Mail** atributos de uma conta válida do Azure Active Directory que pretende tooprovision Olá relacionadas com caixas de texto.

    b. Clique em **Guardar**.
   
    >[!NOTE]
    >titular de conta do Azure Active Directory Olá obtém uma mensagem de e-mail, incluindo uma conta de Olá tooconfirm ligação antes de ficar ativo
    >  

>[!NOTE]
>Pode utilizar quaisquer outras FreshService utilizador conta criação ferramentas ou APIs fornecidas pelo FreshService tooprovision contas de utilizador do AAD.
>  

![Atribua o utilizador][200] 

**tooassign Britta Simon tooFreshservice, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Freshservice**.

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.

Ao clicar em mosaico de Freshservice Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Freshservice aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

