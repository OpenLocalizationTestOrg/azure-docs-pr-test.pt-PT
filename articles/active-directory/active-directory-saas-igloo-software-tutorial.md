---
title: "Tutorial: Integração do Azure Active Directory com o Igloo Software | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>Tutorial: Integração do Azure Active Directory com Igloo Software

Neste tutorial, saiba como toointegrate Igloo Software com o Azure Active Directory (Azure AD).

Integrar Igloo Software com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooIgloo Software
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooIgloo Software (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com o Software de Igloo tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Igloo Software-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Igloo Software da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-igloo-software-from-hello-gallery"></a>Adicionar Igloo Software da Galeria de Olá
tooconfigure Olá integração Igloo software com o Azure AD, é necessário tooadd Igloo Software Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Software Igloo da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Igloo Software**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. No painel de resultados de Olá, selecione **Igloo Software**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com o Software de Igloo com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Igloo Software é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no Igloo Software tem toobe estabelecida.

No Igloo Software, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com o Software de Igloo, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste de Igloo Software](#creating-an-igloo-software-test-user)**  -toohave um homólogo de Britta Simon no Software Igloo toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Igloo Software.

**tooconfigure do Azure AD-início de sessão único com o Software de Igloo, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Igloo Software** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. No Olá **Igloo Software domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.igloocommmunities.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.igloocommmunities.com/saml.digest`

    c. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão. Contacte [equipa de suporte de cliente de Software Igloo](https://www.igloosoftware.com/services/support) tooget estes valores. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. No Olá **Igloo Software configuração** secção, clique em **configurar Software Igloo** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site de empresa de Igloo Software tooyour como administrador.

8. Aceda toohello **painel de controlo**.
   
     ![Painel de controlo](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "painel de controlo")

9. No Olá **associação** separador, clique em **definições de início de sessão**.
   
    ![Iniciar sessão nas definições](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "iniciar sessão nas definições")

10. Na secção de configuração de SAML Olá, clique em **configurar a autenticação SAML**.
   
    ![Configuração de SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "configuração SAML")
   
11. No Olá **configuração geral** secção, execute Olá os seguintes passos:
   
    ![Configuração geral](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "configuração geral")

    a. No Olá **nome da ligação** caixa de texto, escreva um nome personalizado para a sua configuração.
   
    b. No Olá **URL de início de sessão do IdP** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.
   
    c. No Olá **URL de fim de sessão do IdP** caixa de texto, colar Olá valor **Sign-Out URL** que copiou do portal do Azure.
    
    d. Selecione **resposta de fim de sessão e o tipo de pedido de HTTP** como **POST**.
   
    e. Abra o **base-64** codificado certificado no bloco de notas transferido a partir do portal do Azure, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado público** caixa de texto.
    
12. No Olá **resposta e a configuração de autenticação**, efetuar Olá os seguintes passos:
    
    ![Resposta e a configuração de autenticação](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "resposta e a configuração de autenticação")
  
      a. Como **fornecedor de identidade**, selecione **Microsoft ADFS**.
      
      b. Como **tipo de identificador**, selecione **endereço de correio eletrónico**. 

      c. No Olá **atributo de correio eletrónico** caixa de texto, tipo **emailaddress**.

      d. No Olá **nome próprio atributo** caixa de texto, tipo **givenname**.

      e. No Olá **último nome do atributo** caixa de texto, tipo **Apelido**.

13. Execute Olá configuração de Olá toocomplete de passos a seguir:
    
    ![Criação de utilizador no início de sessão](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "criação de utilizador no início de sessão") 

     a. Como **criação de utilizador no início de sessão**, selecione **criar um novo utilizador do seu site quando iniciam sessão no**.

     b. Como **iniciar sessão nas definições**, selecione **botão SAML de utilização no ecrã de "Iniciar sessão"**.

     c. Clique em **Guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-igloo-software-test-user"></a>Criar um utilizador de teste Igloo Software

Não há nenhum item de ação para tooconfigure aprovisionamento de utilizadores tooIgloo Software.  

Quando um utilizador atribuído tenta toolog no tooIgloo Software utilizando o painel de acesso de Olá, Igloo Software verifica se o utilizador Olá existe.  Se não existe nenhuma conta de utilizador ainda estão disponíveis, é criado automaticamente pelo Software de Igloo.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooIgloo Software.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooIgloo Software, efetuar Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Igloo Software**.

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de Igloo Software Olá no painel de acesso de Olá, deve obter as aplicações de Igloo Software tooyour automaticamente com sessão iniciada.
Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

