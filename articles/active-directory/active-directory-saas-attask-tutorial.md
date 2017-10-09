---
title: "Tutorial: Integração do Azure Active Directory com @Task| Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>Tutorial: Integração do Azure Active Directory com o@Task
o objetivo deste tutorial Olá é tooshow como toointegrate @Task com o Azure Active Directory (Azure AD).  
Integrar @Task com o Azure AD fornece-lhe Olá seguintes vantagens: 

* Pode controlar no Azure AD quem tem acessotoo@Task
* Pode ativar os seus utilizadores tooautomatically obter com sessão iniciada too@Task (Single Sign-On) com as respetivas contas do Azure AD
* Pode gerir as contas numa localização central - Olá Portal clássico do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
integração de tooconfigure do Azure AD com @Task, terá de Olá seguintes itens:

* Uma subscrição do Azure AD
* Um @Task início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.
> 
> 

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

* Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
* Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrição do cenário
o objetivo deste tutorial Olá é tooenable tootest do Azure AD-início de sessão único num ambiente de teste.  
cenário de Olá descrito neste tutorial consiste em três blocos modulares principais:

1. Adicionar @Task da Galeria de Olá 
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-task-from-hello-gallery"></a>Adicionar @Task da Galeria de Olá
integração de Olá tooconfigure de @Task com o Azure AD, terá de tooadd @Task Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd @Task da Galeria de Olá, efetuar Olá os seguintes passos:**

1. No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**. 
   
    ![Active Directory][1] 
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Aplicações][2] 
4. Clique em **adicionar** em Olá parte inferior da página Olá.
   
    ![Aplicações][3] 
5. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.
   
    ![Aplicações][4] 
6. Na caixa de pesquisa de Olá, escreva  **@Task** .
   
    ![Aplicações][5] 
7. No painel de resultados de Olá, selecione  **@Task** e, em seguida, clique em **concluída** aplicação de Olá tooadd.
   
    ![Aplicações][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Olá objetivo desta secção é tooshow tem como único tooconfigure e teste do Azure AD início de sessão com @Task com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá @Task tooan utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados utilizador @Task tem toobe estabelecida.   
Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no @Task.

tooconfigure e teste do Azure AD de sessão único-com @Task, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um @Tasktest utilizador](#creating-a-halogen-software-test-user)**  -toohave uma homólogo de Britta Simon no @Taskthat é-lhe representação toohello ligado do Azure AD.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD início de sessão único
o objetivo desta secção Olá é tooenable do Azure AD início de sessão no portal clássico do Azure de Olá e tooconfigure-início de sessão único na sua @Task aplicação.

**tooconfigure do Azure AD-início de sessão único com @Task, efetuar Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no Olá  **@Task**  página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar Single Sign-On**  caixa de diálogo.
   
    ![Configurar o início de sessão único][6] 
2. No Olá **como faria, como os utilizadores toosign num too@Task**  página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
    ![Azure AD início de sessão único][7] 
3. No Olá **configurar definições de aplicação** diálogo página, execute Olá os seguintes passos:
   
    ![Configurar definições da aplicação][8] 
   
     a. No Olá **URL de início de sessão** caixa de texto, tipo Olá URL utilizado por utilizadores em toosign tooyour @Task aplicação (por ex.:*https://<Tenant name>.attask ondemand.com*).
   
     b. Clique em **Seguinte**.
4. No Olá **configurar início de sessão único em @Task**  página, clique em **transferir metadados**, guarde o ficheiro de metadados de Olá localmente no seu computador e, em seguida, clique em **seguinte**.
   
    ![O que é o Azure AD Connect][9] 
5. Início de sessão tooyour @Task site da empresa como administrador.
6. Aceda demasiado**início de sessão único na configuração**.
7. No Olá **Single Sign-On** caixa de diálogo, efetuar Olá os passos seguintes
   
    ![Configurar o início de sessão único][23]
   
    a. Como **tipo**, selecione **SAML 2.0**.
   
    b. Selecione **ID do fornecedor de serviço**.
   
    c. No portal clássico do Azure Olá, copie Olá **URL de início de sessão remoto**e, em seguida, cole-o Olá **URL do Portal de início de sessão** caixa de texto.
   
    d. No portal clássico do Azure Olá, copie Olá **único URL de serviço Sign-Out**e, em seguida, cole-o Olá **Sign-Out URL** caixa de texto.
   
    e. No portal clássico do Azure Olá, copie Olá **alterar palavra-passe URL**e, em seguida, cole-o Olá **alterar palavra-passe URL** caixa de texto.
   
    f. Clique em **Guardar**.
8. No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**. 
   
    ![O que é o Azure AD Connect][10]
9. No Olá **único início de sessão confirmação** página, clique em **concluída**.  
   
    ![O que é o Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste no portal clássico do Azure chamado Britta Simon de Olá.  

![Criar utilizador do Azure AD][20]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**. 
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos: 
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. Como tipo de utilizador, selecione o novo utilizador na sua organização.
   
    b. No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.
   
    c. Clique em **Seguinte**.
6. No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos: 
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. No Olá **nome próprio** caixa de texto, tipo **Britta**.  
   
    b. No Olá **Apelido** caixa de texto, tipo, **Simon**.
   
    c. No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.
   
    d. No Olá **função** lista, selecione **utilizador**.

    e. Clique em **Seguinte**.

7. No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. Anote o valor Olá Olá **nova palavra-passe**.
   
    b. Clique em **Concluído**.   

### <a name="creating-an-task-test-user"></a>Criar um @Task utilizador de teste
o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon no @Task.

**toocreate um utilizador chamado Britta Simon @Task, efetuar Olá os seguintes passos:**

1. Início de sessão tooyour @Task site da empresa como administrador.
2. No menu de Olá na parte superior do Olá, clique em **pessoas**.
3. Clique em **nova pessoa**. 
4. Na caixa de diálogo de nova pessoa Olá, execute Olá os seguintes passos:
   
    ![Criar um @Task utilizador de teste][21] 
   
    a. No Olá **nome próprio** caixa de texto, escreva "Britta".
   
    b. No Olá **Apelido** caixa de texto, escreva "Simon".
   
    c. No Olá **endereço de correio eletrónico** caixa de texto, escreva o endereço de correio eletrónico de Britta Simon no Azure Active Directory.
   
    d. Clique em **Adicionar pessoa**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD
objetivo Olá desta secção é tooenabling Britta Simon toouse do Azure-início de sessão único, concedendo o respetivo acesso too@Task.

![Atribua o utilizador][200] 

**tooassign Britta Simon too@Task, efetuar Olá os seguintes passos:**

1. Olá, Azure portal clássico, a vista de aplicações Olá tooopen, na vista de diretório Olá, clique em **aplicações** no menu superior Olá.
   
    ![Atribua o utilizador][201] 
2. Na lista de aplicações de Olá, selecione  **@Task** .
   
    ![Atribua o utilizador][202] 
3. No menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![Atribua o utilizador][203] 
4. Na lista de utilizadores Olá, selecione **Britta Simon**.
5. Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.
   
    ![Atribua o utilizador][205]

### <a name="testing-single-sign-on"></a>Teste o início de sessão único
o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.  
Ao clicar em Olá @Task Olá de mosaico no painel de acesso, deve obter automaticamente com sessão iniciada tooyour @Task aplicação.

## <a name="additional-resources"></a>Recursos Adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






