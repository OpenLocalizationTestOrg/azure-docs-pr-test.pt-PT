---
title: "Tutorial: Integração do Azure Active Directory com o SSO Kantega para Bamboo | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Kantega SSO para Bamboo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a>Tutorial: Integração do Azure Active Directory com o SSO Kantega para Bamboo

Neste tutorial, saiba como toointegrate Kantega SSO para Bamboo com o Azure Active Directory (Azure AD).

Integrar Kantega SSO para Bamboo com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooKantega SSO para Bamboo
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooKantega SSO para Bamboo (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com o SSO Kantega para Bamboo tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um SSO Kantega para Bamboo-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Kantega SSO para Bamboo da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a>Adicionar Kantega SSO para Bamboo da Galeria de Olá
tooconfigure Olá integração do SSO Kantega para Bamboo com o Azure AD, terá de tooadd Kantega SSO para Bamboo Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Kantega SSO para Bamboo da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Kantega SSO para Bamboo**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. No painel de resultados de Olá, selecione **Kantega SSO para Bamboo**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com o SSO Kantega para Bamboo com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Kantega SSO para Bamboo é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Kantega SSO para Bamboo tem toobe estabelecida.

Em Kantega SSO para Bamboo, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com o Kantega SSO para Bamboo, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um SSO Kantega para o utilizador de teste de Bamboo](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave um homólogo de Britta Simon em Kantega SSO para Bamboo é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua SSO Kantega para aplicação Bamboo.

**tooconfigure do Azure AD-início de sessão único com o SSO Kantega para Bamboo, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Kantega SSO para Bamboo** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. No **IDP** iniciada modo, Olá **Kantega SSO para o domínio de Bamboo e URLs** secção efetuar Olá passo a seguir:

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. No **SP** modo iniciado, verifique **Mostrar avançadas definições de URL** e efetuar Olá passo a seguir:

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`
     
    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão. Estes valores são recebidos durante a configuração de Olá do plug-in de Bamboo que é explicado mais tarde no tutorial Olá.

5. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. Numa janela do browser web diferente, inicie sessão no tooyour Bamboo no servidor no local como administrador.

8. Paire o rato sobre o ícone e clique em Olá **suplementos**.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. Na secção do separador Suplementos, clique em **localizar novos suplementos**. Pesquisa **Kantega SSO para Bamboo (SAML & Kerberos)** e clique em **instalar** botão tooinstall Olá Plug-in SAML de novo.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. instalação de plug-in de Olá será iniciado.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. Depois de concluída a instalação de Olá. Clique em **Fechar**.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. Clique em **Gerir**.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. Clique em **configurar** tooconfigure Olá novo plug-in.  

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. No Olá **SAML** secção. Selecione **Azure Active Directory (Azure AD)** de Olá **Adicionar fornecedor de identidade** pendente.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. Selecione o nível de subscrição como **básico**.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. No Olá **as propriedades da aplicação** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    a. Olá cópia **URI de ID de aplicação** valor e utilizá-lo como **identificador, o URL de resposta e o URL de início de sessão** no Olá **Kantega SSO para o domínio de Bamboo e URLs** secção no portal do Azure.

    b. Clique em **Seguinte**.

17. No Olá **importar metadados** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    a. Selecione **ficheiro de metadados no meu computador**e o ficheiro de metadados do carregamento, que transferiu a partir do portal do Azure.

    b. Clique em **Seguinte**.

18. No Olá **localização nome e SSO** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    a. Adicione o nome do fornecedor de identidade de Olá no **nome do fornecedor de identidade** caixa de texto (por exemplo, do Azure AD).

    b. Clique em **Seguinte**.

19. Verificar o certificado de assinatura de Olá e clique em **seguinte**.    

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. No Olá **contas de utilizador Bamboo** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    a. Selecione **criar utilizadores no diretório interno do Bamboo se for necessário** e introduza o nome adequado Olá do grupo de Olá para os utilizadores (pode ser não vários. de grupos separados por vírgulas).

    b. Clique em **Seguinte**.

21. Clique em **Concluir**.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. No Olá **conhecido domínios para o Azure AD** secção, execute os seguintes passos:   

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    a. Selecione **conhecido domínios** do painel esquerdo do Olá da página Olá.

    b. Introduza o nome de domínio no Olá **conhecido domínios** caixa de texto.

    c. Clique em **Guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a>Criar um SSO Kantega para o utilizador de teste de Bamboo

tooenable do Azure AD os utilizadores toolog no tooBamboo, estes têm de ser aprovisionados para Bamboo. Em Kantega SSO para Bamboo, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour Bamboo no servidor no local como administrador.

2. Paire o rato sobre o ícone e clique em Olá **gestão de utilizadores**.

    ![Adicionar empregado](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. Clique em **Utilizadores**. Em Olá **adicionar utilizador** secção, execute os passos de follwing:

    ![Adicionar empregado](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    a. No Olá **Username** caixa de texto, como o tipo Olá e-mail do utilizador Brittasimon@contoso.com.
    
    b. No Olá **palavra-passe** caixa de texto, palavra-passe Olá de tipo de utilizador.

    c. No Olá **Confirmar palavra-passe** caixa de texto, reintroduza o Olá palavra-passe do utilizador.
    
    d. No Olá **nome completo** caixa de texto, nome completo do tipo de utilizador de Olá como Britta Simon.
    
    e. No Olá **E-Mail** caixa de texto, como o endereço de correio eletrónico de Olá de tipo de utilizador Brittasimon@contoso.com.
    
    f. Clique em **Guardar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooKantega SSO para Bamboo.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooKantega SSO para Bamboo, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Kantega SSO para Bamboo**.

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá Kantega SSO para mosaico Bamboo no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Kantega SSO para a aplicação de Bamboo.
Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

