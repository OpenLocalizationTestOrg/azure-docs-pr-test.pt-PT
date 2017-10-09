---
title: "Tutorial: Integração do Azure Active Directory com Panorama9 | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a>Tutorial: Integração do Azure Active Directory com Panorama9

Neste tutorial, saiba como toointegrate Panorama9 com o Azure Active Directory (Azure AD).

Integrar Panorama9 com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooPanorama9
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPanorama9 (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Panorama9 tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Panorama9-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Panorama9 da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-panorama9-from-hello-gallery"></a>Adicionar Panorama9 da Galeria de Olá
tooconfigure Olá integração de Panorama9 com o Azure AD, é necessário tooadd Panorama9 Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Panorama9 da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Panorama9**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. No painel de resultados de Olá, selecione **Panorama9**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-

Nesta secção, configure e teste do Azure AD-início de sessão único com Panorama9 com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Panorama9 é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Panorama9 tem toobe estabelecida.

No Panorama9, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Panorama9, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Panorama9](#creating-a-panorama9-test-user)**  -toohave um homólogo de Britta Simon no Panorama9 é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Panorama9.

**tooconfigure do Azure AD-início de sessão único com Panorama9, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Panorama9** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. No Olá **Panorama9 domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL como:`https://dashboard.panorama9.com/saml/access/3262`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`http://www.panorama9.com/saml20/<tenant-name>`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente Panorama9](https://support.panorama9.com) tooget estes valores. 
 
4. No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado.

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. No Olá **Panorama9 configuração** secção, clique em **configurar Panorama9** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. Numa janela do browser web diferente, inicie sessão no site da sua empresa Panorama9 como administrador.

6. Na barra de ferramentas Olá na parte superior do Olá, clique em **gerir**e, em seguida, clique em **extensões**.
   
   ![Extensões](./media/active-directory-saas-panorama9-tutorial/ic790023.png "extensões")
7. No Olá **extensões** caixa de diálogo, clique em **Single Sign-On**.
   
   ![De sessão único-](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")
8. No Olá **definições** secção, execute Olá os seguintes passos:
   
   ![Definições](./media/active-directory-saas-panorama9-tutorial/ic790025.png "definições")
   
    a. No **URL do fornecedor de identidade** caixa de texto, colar Olá valor **URL Single Sign-On serviço**, que copiou do portal do Azure.
   
    b. No **impressão digital do certificado** caixa de texto, colar Olá **Thumbprint** valor do certificado, o qual copiou a partir do portal do Azure.    
         
9. Clique em **Guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-panorama9-test-user"></a>Criar um utilizador de teste Panorama9

Na ordem tooenable do Azure AD os utilizadores toolog para Panorama9, têm de ser aprovisionados para Panorama9.  

No caso de Olá da Panorama9, o aprovisionamento é uma tarefa manual.

**tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **Panorama9** site da empresa como administrador.

2. No menu de Olá na parte superior do Olá, clique em **gerir**e, em seguida, clique em **utilizadores**.
   
  ![Os utilizadores](./media/active-directory-saas-panorama9-tutorial/ic790027.png "utilizadores")

3. Na secção utilizadores Olá, clique em  **+**  tooadd novo utilizador.

 ![Os utilizadores](./media/active-directory-saas-panorama9-tutorial/ic790028.png "utilizadores")

4. Aceda toohello secção de dados de utilizador, Olá tipo endereço de e-mail de um utilizador válido do Azure Active Directory que pretende tooprovision para Olá **E-Mail** caixa de texto.

5. São fornecidos toohello seção de utilizadores, clique em **guardar**.
   
> [!NOTE]
    > titular de conta do Azure Active Directory Olá recebe uma mensagem de e-mail e de que respeita a tooconfirm uma ligação a respetiva conta para ficar ativa.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPanorama9.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooPanorama9, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Panorama9**.

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de Olá Panorama9 no painel de acesso de Olá, deve colocar a aplicação de tooPanorama9 automaticamente com sessão iniciada.
Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

