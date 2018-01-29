---
title: "Tutorial: Azure Active Directory a integração com SAML SSO para Jira pela resolução GmbH | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre o Azure Active Directory e SAML SSO para Jira pela resolução GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 3a3224acd2376efca19a29576980b6a3ca6a9e99
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a>Tutorial: Azure Active Directory a integração com SAML SSO para Jira pela resolução GmbH

Neste tutorial, irá aprender a integrar SAML SSO para Jira pela resolução GmbH com o Azure Active Directory (Azure AD).

Integrar SAML SSO para Jira pela resolução GmbH com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso ao SAML SSO para Jira pela resolução GmbH
- Pode permitir que os utilizadores automaticamente obter assinado no SAML SSO para Jira pela resolução GmbH (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal do Azure

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o SAML SSO para Jira resolução GmbH, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Um SAML SSO para Jira pela resolução GmbH início de sessão único subscrição ativado

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar SAML SSO para Jira resolução GmbH na galeria do
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a>Adicionar SAML SSO para Jira resolução GmbH na galeria do
Para configurar a integração de SAML SSO para Jira pela resolução GmbH com o Azure AD, tem de adicionar SAML SSO para Jira pela resolução GmbH na Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar SAML SSO para Jira pela resolução GmbH na galeria do, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![Aplicações][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa, escreva **SAML SSO para Jira pela resolução GmbH**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. No painel de resultados, selecione **SAML SSO para Jira pela resolução GmbH**e, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configurar e testar o Azure AD-início de sessão único com o SAML SSO para Jira pela resolução que GmbH com base num utilizador de teste chamado "Britta Simon."

Para início de sessão trabalhar, do Azure AD tem de saber que homólogo utilizador no SAML SSO para Jira pela resolução GmbH for para um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no SAML SSO para Jira por resolução GmbH tem de ser estabelecida.

No SAML SSO para Jira pela resolução GmbH, atribua o valor do **nome de utilizador** no Azure AD como o valor de **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com o SAML SSO para Jira pela resolução GmbH, tem de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um SAML SSO para Jira pelo utilizador de teste de GmbH resolução](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  - para ter um homólogo de Britta Simon no SAML SSO para Jira pela resolução GmbH que está ligada a representação do Azure AD do utilizador.
4. **[Atribuir o utilizador de teste do Azure AD](#assigning-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, ativar o Azure AD início de sessão no portal do Azure e configurar o início de sessão único na sua SAML SSO para Jira resolução GmbH aplicação.

**Para configurar do Azure AD-início de sessão único com o SAML SSO para Jira resolução GmbH, execute os seguintes passos:**

1. No portal do Azure, no **SAML SSO para Jira pela resolução GmbH** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. No **SAML SSO para Jira pela resolução GmbH domínio e os URLs** secção, se pretender configurar a aplicação no **IDP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    a. No **identificador** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<server-base-url>/plugins/servlet/samlsso`

    b. No **URL de resposta** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<server-base-url>/plugins/servlet/samlsso`

4. Verifique **Mostrar avançadas definições de URL**. Se pretender configurar a aplicação no **SP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    No **URL de início de sessão** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o identificador de real, a URL de resposta e o URL de início de sessão. Contacte [SAML SSO para Jira pela resolução GmbH cliente suportar equipa](https://www.resolution.de/go/support) para obter estes valores. 

5. No **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. Numa janela do browser web diferente, inicie sessão no seu **SAML SSO para Jira pelo portal de administração de GmbH resolução** como administrador.

8. Paire o rato sobre o ícone e clique em de **suplementos**.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. São redirecionados para a página de acesso de administrador. Introduza o **palavra-passe** e clique em **confirmar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. Na secção do separador Suplementos, clique em **localizar novos suplementos**. Pesquisa **SAML único início de sessão (SSO) para JIRA** e clique em **instalar** botão para instalar o novo plug-in SAML.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. A instalação de plug-in será iniciado. Clique em **Fechar**.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. Clique em **Gerir**.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. Clique em **configurar** para configurar o plug-in de novo.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. No **SAML SingleSignOn Plug-in configuração** página, clique em **Adicionar nova IdP** botão para configurar as definições do fornecedor de identidade.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. No **escolha o fornecedor de identidade** página, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon5a.png)
 
    a. Definir **do Azure AD** como o tipo de IdP.
    
    b. Adicionar **nome** do fornecedor de identidade (por exemplo, do Azure AD).
    
    c. Adicionar **Descrição** do fornecedor de identidade (por exemplo, do Azure AD).
    
    d. Clique em **Seguinte**.
    
16. No **configuração do fornecedor de identidade** página, clique em **seguinte** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon5b.png)

17. No **importação SAML IdP metadados** página, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon5c.png)

    a. Clique em **carga ficheiro** botão e escolha o ficheiro XML de metadados que transferiu no passo 5.

    b. Clique em **importação** botão.
    
    c. Aguarde por breves instantes até que a importação for bem sucedida.
    
    d. Clique em **seguinte** botão.
    
18. No **atributo de ID de utilizador e a transformação** página, clique em **seguinte** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon5d.png)
    
19. No **criação de utilizador e a atualização** página, clique em **Guardar & seguinte** ao guardar as definições.   
    
    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon6a.png)
    
20. No **testar as suas definições** página, clique em **ignorar teste & configurar manualmente** para ignorar o teste de utilizador por agora. Isto irá ser efetuado na secção seguinte e necessita de algumas definições no portal do Azure. 
    
    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon6b.png)
    
21. A ler a caixa de diálogo apprearing **ignorar os meios de teste...** , clique em **OK**.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/addon6c.png)

> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No **portal do Azure**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior da caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. No **utilizador** diálogo página, execute os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    a. No **nome** caixa de texto, tipo **BrittaSimon**.

    b. No **nome de utilizador** caixa de texto, tipo de **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor da **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a>Criar um SAML SSO para Jira pelo utilizador de teste de GmbH de resolução

Para permitir que os utilizadores do Azure AD inicie sessão SAML SSO para Jira resolução GmbH, estes têm de ser aprovisionados no SAML SSO para Jira pela resolução GmbH.  
No SAML SSO para Jira pela resolução GmbH, o aprovisionamento é uma tarefa manual.

**Para Aprovisionar uma conta de utilizador, execute os seguintes passos:**

1. Inicie sessão no seu SAML SSO para Jira pelo site de empresa resolução GmbH como administrador.

2. Paire o rato sobre o ícone e clique em de **gestão de utilizadores**.

    ![Adicionar empregado](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. São redirecionados para a página de acesso de administrador para introduzir **palavra-passe** e clique em **confirmar** botão.

    ![Adicionar empregado](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. Em **gestão de utilizadores** separador de secção, clique em **criar utilizador**.

    ![Adicionar empregado](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. No **"Criar novo utilizador"** diálogo página, execute os seguintes passos:

    ![Adicionar empregado](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    a. No **endereço de correio eletrónico** caixa de texto, como o tipo de endereço de correio eletrónico do utilizador Brittasimon@contoso.com.

    b. No **nome completo** caixa de texto, nome completo do tipo de utilizador como Britta Simon.

    c. No **Username** caixa de texto, como o tipo de mensagem de correio eletrónico do utilizador Brittasimon@contoso.com.

    d. No **palavra-passe** caixa de texto, escreva a palavra-passe do utilizador.

    e. Clique em **criar utilizador**.   

### <a name="assigning-the-azure-ad-test-user"></a>Atribuir o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso para SAML SSO para Jira pela resolução GmbH.

![Atribua o utilizador][200] 

**Para atribuir Britta Simon a SAML SSO para Jira pela resolução GmbH, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **SAML SSO para Jira pela resolução GmbH**.

    ![Configurar o início de sessão único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão através do painel de acesso.

Ao clicar o SAML SSO para Jira pelo mosaico de GmbH resolução no painel de acesso, deve obter automaticamente com sessão iniciada para o SAML SSO para Jira pela resolução GmbH aplicação.
Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

