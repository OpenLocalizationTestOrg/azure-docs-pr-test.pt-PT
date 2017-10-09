---
title: "Tutorial: Integração do Azure Active Directory com Netsuite | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>Tutorial: Integração do Azure Active Directory com Netsuite

Neste tutorial, saiba como toointegrate Netsuite com o Azure Active Directory (Azure AD).

Integrar Netsuite com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooNetsuite
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooNetsuite (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Netsuite tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Netsuite início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Netsuite da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-netsuite-from-hello-gallery"></a>Adicionar Netsuite da Galeria de Olá
tooconfigure Olá integração de Netsuite com o Azure AD, é necessário tooadd Netsuite Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Netsuite da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. Clique em **nova aplicação** botão na parte superior de Olá da caixa de diálogo Olá.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Netsuite**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. No painel de resultados de Olá, selecione **Netsuite**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Netsuite com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Netsuite é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Netsuite tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Netsuite.

tooconfigure e teste do Azure AD-início de sessão único com Netsuite, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Netsuite](#creating-a-netsuite-test-user)**  -toohave um homólogo de Britta Simon no Netsuite é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Netsuite.

**tooconfigure do Azure AD-início de sessão único com Netsuite, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Netsuite** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. No Olá **Netsuite domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > Este valor não é o valor real. Atualização Olá valor com Olá real de resposta de URL. Contacte [equipa de suporte de Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget este valor.
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. No Olá **Netsuite configuração** secção, clique em **configurar Netsuite** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. Abra um novo separador no seu browser e inicie sessão no site da sua empresa Netsuite como administrador.

8. Na barra de ferramentas Olá em Olá parte superior da página Olá, clique em **configuração**, em seguida, clique em **Gestor de configuração**.

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. De Olá **tarefas de configuração** lista, selecione **integração**.

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. No Olá **Gerir autenticação** secção, clique em **SAML-início de sessão único**.

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. No Olá **configuração SAML** página, execute Olá os seguintes passos:
   
    a. Olá cópia **único início de sessão no URL do serviço SAML** valor a partir da **referência rápida** secção **configurar início de sessão** e cole-Olá **fornecedor de identidade Página de início de sessão** campo no Netsuite.

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b. No Netsuite, selecione **método de autenticação principal**.

    c. Para o campo de Olá etiquetado **os metadados do fornecedor de identidade SAMLV2**, selecione **carregar ficheiro de metadados do IDP**. Em seguida, clique em **procurar** ficheiro de metadados de Olá tooupload que transferiu a partir do portal do Azure.

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    d. Clique em **submeter**.

12. No Azure AD, clique em **ver e editar todos os outros atributos de utilizador** caixa de verificação e adicione o atributo.

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Para Olá **nome de atributo** campo, digite na `account`. Para Olá **valor do atributo** campo, escreva o ID de conta Netsuite. Este valor é constante e altere com a conta. Instruções sobre como toofind são incluída abaixo, o ID da conta:

      ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    a. No Netsuite, clique em **configuração** a partir do menu de navegação superior Olá.

    b. Em seguida, clique em Olá **tarefas de configuração** secção do menu de navegação esquerdo Olá, selecione de Olá **integração** secção e clique em **preferências de serviços Web**.

    c. Copie o seu ID de conta Netsuite e cole-o Olá **valor do atributo** campo no Azure AD.

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. Antes dos utilizadores podem efetuar o início de sessão único para Netsuite, estes tem primeiro de atribuir as permissões adequadas Olá no Netsuite. Siga as instruções de Olá abaixo tooassign estas permissões.

    a. No menu de navegação superior Olá, clique em **configuração**, em seguida, clique em **Gestor de configuração**.
      
      ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. No menu de navegação esquerdo Olá, selecione **utilizadores/funções**, em seguida, clique em **gerir funções**.
      
      ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. Clique em **nova função**.

    d. Escreva um **nome** para a sua nova função e selecione Olá **único início de sessão só** caixa de verificação.
      
      ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    e. Clique em **Guardar**.

    f. No menu de Olá na parte superior do Olá, clique em **permissões**. Em seguida, clique em **configuração**.
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. Selecione **definir segurança SAM Single Sign-on**e, em seguida, clique em **adicionar**.

    h. Clique em **Guardar**.

    posso. No menu de navegação superior Olá, clique em **configuração**, em seguida, clique em **Gestor de configuração**.
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. No menu de navegação esquerdo Olá, selecione **utilizadores/funções**, em seguida, clique em **gerir utilizadores**.
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. Selecione um utilizador de teste. Em seguida, clique em **editar**.
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. Na caixa de diálogo de funções Olá, selecione a função de Olá que criou e clique em **adicionar**.
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. Clique em **Guardar**.
    
> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. Na parte superior de Olá da caixa de diálogo Olá, clique em **adicionar** tooopen Olá **utilizador** caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**. 

### <a name="creating-a-netsuite-test-user"></a>Criar um utilizador de teste Netsuite

Nesta secção, é criado um utilizador chamado Britta Simon Netsuite. Netsuite suporta o aprovisionamento de just-in-time, que está ativada por predefinição.
Não há nenhum item de ação para si nesta secção. Se um utilizador já não existe na Netsuite, uma nova é criada quando tenta tooaccess Netsuite.


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooNetsuite.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooNetsuite, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Netsuite**.

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

tootest Olá, as único início de sessão definições, abra o painel de acesso em [https://myapps.microsoft.com](https://myapps.microsoft.com/), iniciar sessão na conta de teste de Olá e, em **Netsuite**.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar o aprovisionamento de utilizadores](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

