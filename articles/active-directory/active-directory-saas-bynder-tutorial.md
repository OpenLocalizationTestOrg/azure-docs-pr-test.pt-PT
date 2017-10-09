---
title: "Tutorial: Integração do Azure Active Directory com Bynder | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Tutorial: Integração do Azure Active Directory com Bynder
o objetivo deste tutorial Olá é tooshow como toointegrate Bynder com o Azure Active Directory (Azure AD).

Integrar Bynder com o Azure AD fornece-lhe Olá seguintes vantagens:

* Pode controlar no Azure AD que tenha acesso tooBynder
* Pode ativar a utilizadores tooautomatically get com sessão iniciada tooBynder-início de sessão único (SSO) com as respetivas contas do Azure AD
* Pode gerir as contas numa localização central - Olá portal clássico do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
integração do Azure AD com Bynder tooconfigure, terá de Olá seguintes itens:

* Uma subscrição do Azure AD
* Um Bynder início de sessão único (SSO) ativada subscrição

>[!NOTE]
>Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção. 
> 

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

* Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
* Se não tiver um ambiente de avaliação do Azure AD, pode obter um [avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
o objetivo deste tutorial Olá é tooenable tootest SSO do Microsoft Azure AD num ambiente de teste.

cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Bynder da Galeria de Olá
2. Configurar e testar o SSO do Microsoft Azure AD

## <a name="add-bynder-from-hello-gallery"></a>Adicionar Bynder da Galeria de Olá
tooconfigure Olá integração de Bynder com o Azure AD, é necessário tooadd Bynder Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Bynder da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá **Portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**. 
   
    ![Active Directory][1]
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Aplicações][2]
4. Clique em **adicionar** em Olá parte inferior da página Olá.
   
    ![Aplicações][3]
5. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.
   
    ![Aplicações][4]
6. Na caixa de pesquisa de Olá, escreva **Bynder**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. No painel de resultados de Olá, selecione **Bynder**e, em seguida, clique em **concluída** aplicação de Olá tooadd.
   
    ![Selecionar aplicação Olá na Galeria de Olá](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Configurar e testar o SSO do Microsoft Azure AD
o objetivo desta secção Olá é tooshow que como tooconfigure e teste do Microsoft Azure AD SSO com Bynder com base num utilizador de teste chamado "Britta Simon".

Para SSO toowork, do Azure AD tem tooknow é o utilizador de homólogo Olá Bynder tooan utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Bynder tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Bynder.

tooconfigure e teste do Microsoft Azure AD SSO com Bynder, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Microsoft Azure AD-início de sessão único](#configuring-azure-ad-single-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On com Britta Simon.
3. **[Criar um utilizador de teste Bynder](#creating-a-bynder-test-user)**  -toohave um homólogo de Britta Simon no Bynder é-lhe representação toohello ligado do Azure AD.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-microsoft-azure-ad-sso"></a>Configurar o SSO do Microsoft Azure AD
Nesta secção, ativar o SSO do Microsoft Azure AD no portal clássico Olá e configurar o SSO na sua aplicação Bynder.

**tooconfigure Microsoft Azure AD SSO com Bynder, execute Olá os seguintes passos:**

1. No portal clássico Olá, no Olá **Bynder** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar Single Sign-On** caixa de diálogo.
   
    ![Configurar o início de sessão único][6] 
2. No Olá **como seria, como os utilizadores toosign no tooBynder** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. No Olá **configurar definições de aplicação** página da caixa de diálogo, se desejar aplicação Olá tooconfigure **IDP iniciada modo**, efetuar Olá os passos seguintes e clique em **seguinte**:
   
    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. Clique em **Seguinte**.
4. Se desejar aplicação Olá tooconfigure **SP iniciada modo** no Olá **configurar definições de aplicação** página da caixa de diálogo, em seguida, clique em Olá **"(opcionais) definições avançada Show"**e, em seguida, introduza Olá **URL de início de sessão** e clique em **seguinte**.

    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.getbynder.com/login/`
  2. Clique em **Seguinte**.
  
   >[!NOTE]
   >valor de Olá para Olá URL de início de sessão neste tutorial é apenas um placeholfer. tooget Olá vlaue real para o seu ambiente, contacte Bynder.
   >

5. No Olá **configurar o início de sessão único em Bynder** página, execute os seguintes passos de Olá e clique em **seguinte**:
   
    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Clique em **transferir metadados**e, em seguida, guarde o ficheiro de Olá no seu computador.
  2. Clique em **Seguinte**.
6. tooget SSO configurado para a sua aplicação, contacte a equipa de suporte de Bynder. Anexar o ficheiro de metadados transferido Olá e partilhá-las com Bynder equipa tooset segurança SSO no seu lado.
7. No portal clássico Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**.
   
    ![Azure AD início de sessão único][10]
8. No Olá **único início de sessão confirmação** página, clique em **concluída**.  
   
    ![Azure AD início de sessão único][11]

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste no portal clássico Olá chamado Britta Simon.

![Criar utilizador do Azure AD][20]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **Portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos:
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. Como tipo de utilizador, selecione o novo utilizador na sua organização.
  2. No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.
  3. Clique em **Seguinte**.
6. No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos:
   
   ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. No Olá **nome próprio** caixa de texto, tipo **Britta**.  
  2. No Olá **Apelido** caixa de texto, tipo, **Simon**. 
  3. No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.
  4. No Olá **função** lista, selecione **utilizador**.
  5. Clique em **Seguinte**.
7. No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Anote o valor Olá Olá **nova palavra-passe**.
   2. Clique em **Concluído**.   

### <a name="create-a-bynder-test-user"></a>Criar um utilizador de teste Bynder
o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon Bynder. Bynder suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.

Não há nenhum item de ação para si nesta secção. Será criado um novo utilizador durante uma tentativa tooaccess Bynder se não existir ainda.

>[!NOTE]
>Se precisar de um utilizador de toocreate manualmente, terá de equipa de suporte do toocontact Olá Bynder. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD
objetivo Olá desta secção é tooenabling Britta Simon toouse SSO do Azure, concedendo utras tooBynder de acesso.

   ![Atribua o utilizador][200]

**tooassign Britta Simon tooBynder, execute Olá os seguintes passos:**

1. No portal clássico Olá, clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Atribua o utilizador][201]
2. Na lista de aplicações de Olá, selecione **Bynder**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. No menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![Atribua o utilizador][203]
4. Na lista de utilizadores Olá, selecione **Britta Simon**.
5. Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.
   
    ![Atribua o utilizador][205]

### <a name="test-single-sign-on"></a>Teste o início de sessão único
o objetivo desta secção Olá é tootest a configuração do Microsoft Azure AD SSO através de Olá painel de acesso.

Ao clicar em mosaico de Bynder Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Bynder aplicação.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
