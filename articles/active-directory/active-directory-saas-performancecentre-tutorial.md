---
title: "Tutorial: Integração do Azure Active Directory com PerformanceCentre | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a>Tutorial: Integração do Azure Active Directory com PerformanceCentre

Neste tutorial, saiba como toointegrate PerformanceCentre com o Azure Active Directory (Azure AD).

Integrar PerformanceCentre com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooPerformanceCentre
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPerformanceCentre (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com PerformanceCentre tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um PerformanceCentre-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar PerformanceCentre da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-performancecentre-from-hello-gallery"></a>Adicionar PerformanceCentre da Galeria de Olá
tooconfigure Olá integração de PerformanceCentre com o Azure AD, é necessário tooadd PerformanceCentre Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd PerformanceCentre da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **PerformanceCentre**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. No painel de resultados de Olá, selecione **PerformanceCentre**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com PerformanceCentre com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá PerformanceCentre é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá PerformanceCentre tem toobe estabelecida.

No PerformanceCentre, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com PerformanceCentre, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste PerformanceCentre](#creating-a-performancecentre-test-user)**  -toohave um homólogo de Britta Simon no PerformanceCentre é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação PerformanceCentre.

**tooconfigure do Azure AD-início de sessão único com PerformanceCentre, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **PerformanceCentre** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. No Olá **PerformanceCentre domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`http://companyname.performancecentre.com/saml/SSO`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`http://companyname.performancecentre.com`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente PerformanceCentre](https://www.performancecentre.com/contact-us/) tooget estes valores. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. No Olá **PerformanceCentre configuração** secção, clique em **configurar PerformanceCentre** tooopen **configurar início de sessão** janela. Olá cópia **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. Início de sessão tooyour **PerformanceCentre** site da empresa como administrador.

8. No separador de Olá no lado esquerdo Olá, clique em **configurar**.
   
    ![Azure AD início de sessão único][10]

9. No separador de Olá no lado esquerdo Olá, clique em **diversos**e, em seguida, clique em **início de sessão único**.
   
    ![Azure AD início de sessão único][11]

10. Como **protocolo**, selecione **SAML**.
   
    ![Azure AD início de sessão único][12]

11. Abra o ficheiro de metadados transferido no bloco de notas, cópia Olá conteúdo, cole-o Olá **metadados do fornecedor de identidade** caixa de texto e, em seguida, clique em **guardar**.
   
    ![Azure AD início de sessão único][13]

12. Certifique-se de que os valores de Olá para Olá **URL de Base de entidade** e **URL de ID de entidade** estão corretos.
    
     ![Azure AD início de sessão único][14]

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-performancecentre-test-user"></a>Criar um utilizador de teste PerformanceCentre

o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon PerformanceCentre.

**toocreate um utilizador chamar Britta Simon PerformanceCentre, execute Olá os seguintes passos:**

1. Início de sessão tooyour PerformanceCentre site da empresa como administrador.

2. No menu de Olá Olá esquerda, clique em **Interrelate**e, em seguida, clique em **criar participante**.
   
    ![Criar utilizador][400]

3. No Olá **Interrelate - criar participante** caixa de diálogo, efetuar Olá os seguintes passos:
   
    ![Criar utilizador][401]
    
    a. Tipo de atributos de Olá necessário para Britta Simon para caixas de texto relacionadas.
    
    >[!IMPORTANT]
    >Nome de utilizador de Britta tem de ser um atributo no PerformanceCentre Olá igual ao hello do nome de utilizador no Azure AD.
    
    b. Selecione **cliente administrador** como **escolha função**.
    
    c. Clique em **Guardar**. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPerformanceCentre.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooPerformanceCentre, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **PerformanceCentre**.

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.  

Ao clicar em mosaico de PerformanceCentre Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour PerformanceCentre aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

