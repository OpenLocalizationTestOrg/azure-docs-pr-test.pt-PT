---
title: "Tutorial: Integração do Azure Active Directory com SuccessFactors | Microsoft Docs"
description: "Saiba como toouse SuccessFactors com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>Tutorial: Integração do Azure Active Directory com SuccessFactors
o objetivo deste tutorial Olá é tooshow como toointegrate SuccessFactors com o Azure Active Directory (Azure AD).

Integrar SuccessFactors com o Azure AD fornece-lhe Olá seguintes vantagens:

* Pode controlar no Azure AD que tenha acesso tooSuccessFactors
* Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSuccessFactors (Single Sign-On) com as respetivas contas do Azure AD
* Pode gerir as contas numa localização central - Olá portal clássico do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
integração do Azure AD com SuccessFactors tooconfigure, terá de Olá seguintes itens:

* Uma subscrição do Azure válida
* Um inquilino na SuccessFactors

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.
> 
> 

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

* Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
* Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
o objetivo deste tutorial Olá é tooenable tootest do Azure AD-início de sessão único num ambiente de teste.

cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar SuccessFactors da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-successfactors-from-hello-gallery"></a>Adicionar SuccessFactors da Galeria de Olá
tooconfigure Olá integração de SuccessFactors com o Azure AD, é necessário tooadd SuccessFactors Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd SuccessFactors da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.
   
    ![Configurar o início de sessão único][1]
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Configurar o início de sessão único][2]
4. Clique em **adicionar** em Olá parte inferior da página Olá.
   
    ![Aplicações][3]
5. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.
   
    ![Configurar o início de sessão único][4]
6. No Olá **caixa pesquisa**, tipo **SuccessFactors**.
   
    ![Configurar o início de sessão único][5]
7. No painel de resultados de Olá, selecione **SuccessFactors**e, em seguida, clique em **concluída** aplicação de Olá tooadd.
   
    ![Configurar o início de sessão único][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
o objetivo desta secção Olá é tooshow que como tooconfigure e teste do Azure AD-início de sessão único com SuccessFactors com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow é o utilizador de homólogo Olá SuccessFactors tooan utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá SuccessFactors tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no SuccessFactors.

tooconfigure e teste do Azure AD-início de sessão único com SuccessFactors, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste SuccessFactors](#creating-a-successfactors-test-user)**  -toohave um homólogo de Britta Simon no SuccessFactors é-lhe representação toohello ligado do Azure AD.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único
Nesta secção, pode ativar do Azure AD início de sessão no portal clássico Olá e configurar o início de sessão único na sua aplicação SuccessFactors.

**tooconfigure do Azure AD-início de sessão único com SuccessFactors, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no Olá **SuccessFactors** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo.
   
    ![Configurar o início de sessão único][7]
2. No Olá **como seria, como os utilizadores toosign no tooSuccessFactors** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
    ![Configurar o início de sessão único][8]
3. No Olá **URL da aplicação configurar** página, execute os seguintes passos de Olá e, em seguida, clique em **seguinte**.
   
    ![Configurar o início de sessão único][9]
   
    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL utilizando um dos seguintes padrões de Olá: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. No Olá **URL de resposta** caixa de texto, escreva um URL utilizando um dos seguintes padrões de Olá: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. Clique em **Seguinte**. 

    > [!NOTE]
    > Tenha em atenção que estes não são valores reais Olá. Tiver tooupdate estes valores com Olá real URL de início de sessão e de resposta do URL. Contacte o tooget estes valores, [SuccessFactors suporta equipa](https://www.successfactors.com/en_us/support.html).

1. No Olá **configurar o início de sessão único em SuccessFactors** página, clique em **Transferir certificado**e, em seguida, guarde o ficheiro de certificado Olá localmente no seu computador.
   
    ![Configurar o início de sessão único][10]

2. Numa janela do browser web diferente, inicie sessão no seu **portal de administração de SuccessFactors** como administrador.

3. Visite **segurança da aplicação** e nativo demasiado**início de sessão único na funcionalidade**. 

4. Colocar qualquer valor Olá **repor Token** e clique em **guardar Token** tooenable SAML SSO.
   
    ![Configurar o início de sessão único no lado de aplicação][11]

    > [!NOTE] 
    > Este valor é utilizado apenas como Olá/desative comutador. Se qualquer valor for guardado, Olá SAML SSO está ON. Se um valor em branco é guardado Olá SAML SSO está OFF.

1. Captura de ecrã toobelow nativo e efetuar Olá ações a seguir.
   
    ![Configurar o início de sessão único no lado de aplicação][12]
   
    a. Selecione Olá **SAML v2 SSO** botão de opção
   
    b. Defina Olá SAML Asserting terceiros Name(e.g. SAml issuer + company name).
   
    c. No Olá **SAML emissor** caixa de texto colocados valor Olá **URL do emissor** do Assistente de configuração de aplicações do Azure AD.
   
    d. Selecione **resposta (cliente gerado/IdP/AP)** como **exigir assinatura obrigatória**.
   
    e. Selecione **ativada** como **ativar SAML sinalizador**.
   
    f. Selecione **não** como **assinatura do pedido de início de sessão (SF gerado/SP/RP)**.
   
    g. Selecione **Browser/Post perfil** como **perfil SAML**.
   
    h. Selecione **não** como **impor período válido de certificado**.
   
    posso. Copie Olá conteúdo do ficheiro de certificado transferido Olá e, em seguida, cole-o Olá **SAML verificar certificado** caixa de texto.

    > [!NOTE] 
    > conteúdo de certificado Olá tem de ter começar etiquetas de certificado do certificado e de fim.

1. Navegue tooSAML V2 e, em seguida, execute Olá os seguintes passos:
   
    ![Configurar o início de sessão único no lado de aplicação][13]
   
    a. Selecione **Sim** como **suporta iniciado por SP Global terminar**.
   
    b. No Olá **Global URL do serviço fim de sessão (LogoutRequest destino)** caixa de texto colocados valor Olá **URL de fim de sessão remoto** do Assistente de configuração de aplicações do Azure AD.
   
    c. Selecione **não** como **requerem sp tem de encriptar todos os NameID elemento**.
   
    d. Selecione **não especificado** como **NameID formato**.
   
    e. Selecione **Sim** como **ativar SP2 iniciada pelo início de sessão (AuthnRequest)**.
   
    f. No Olá **pedido de envio como emissor de toda a empresa** caixa de texto colocados valor Olá **URL de início de sessão remoto** do Assistente de configuração de aplicações do Azure AD.
2. Execute estes passos, se pretender que os nomes de utilizador de início de sessão de Olá de toomake sensível,.
   
    a. Visite **definições da empresa**(perto do fim Olá).
   
    b. Selecione a caixa de verificação junto **ativar o nome de utilizador de caso de não-sensíveis**.
   
    c.Click **guardar**.
   
    ![Configurar o início de sessão único][29]

    > [!NOTE] 
    > Se tentar tooenable isto, o sistema Olá verifica se criará um nome de início de sessão SAML duplicado. Por exemplo, se o cliente de Olá tem nomes de utilizador User1 e user1. Colocar ausente sensibilidade às maiúsculas e minúsculas torna estas duplicados. sistema de Olá irá dar-lhe uma mensagem de erro e não irá ativar a funcionalidade de Olá. Olá cliente terá de toochange um dos nomes de utilizador Olá pelo que, na verdade, está a ser escrito diferentes. 

1. No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída** tooclose Olá **configurar início de sessão único** caixa de diálogo.
   
    ![Aplicações][14]
2. No Olá **único início de sessão confirmação** página, clique em **concluída**.
   
    ![Aplicações][15]

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste no portal clássico Olá chamado Britta Simon.

![Criar utilizador do Azure AD][16]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **Portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.
   
    ![Criar um utilizador de teste do Azure AD][17]
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![Criar um utilizador de teste do Azure AD][18]
4. Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.
   
    ![Criar um utilizador de teste do Azure AD][19]
5. No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos:
   
    ![Criar um utilizador de teste do Azure AD][20]
   
    a. Como tipo de utilizador, selecione o novo utilizador na sua organização.
   
    b. No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.
   
    c. Clique em **Seguinte**.
6. No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos:
   
    ![Criar um utilizador de teste do Azure AD][21]
   
    a. No Olá **nome próprio** caixa de texto, tipo **Britta**.  
   
    b. No Olá **Apelido** caixa de texto, tipo, **Simon**.
   
    c. No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.
   
    d. No Olá **função** lista, selecione **utilizador**.
   
    e. Clique em **Seguinte**.
7. No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criar um utilizador de teste do Azure AD][22]
8. No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:
   
    ![Criar um utilizador de teste do Azure AD][23]
   
    a. Anote o valor Olá Olá **nova palavra-passe**.
   
    b. Clique em **Concluído**.  

### <a name="creating-a-successfactors-test-user"></a>Criar um utilizador de teste SuccessFactors
Na ordem tooenable do Azure AD os utilizadores toolog para SuccessFactors, têm de ser aprovisionados para SuccessFactors.  
No caso de Olá da SuccessFactors, o aprovisionamento é uma tarefa manual.

utilizadores de tooget criados no SuccessFactors, terá de toocontact Olá [SuccessFactors suporta equipa](https://www.successfactors.com/en_us/support.html).

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD
objetivo Olá desta secção é tooenabling Britta Simon toouse do Azure-início de sessão único, concedendo utras tooSuccessFactors de acesso.

![Atribua o utilizador][24]

**tooassign Britta Simon tooSuccessFactors, execute Olá os seguintes passos:**

1. No portal clássico Olá, clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Atribua o utilizador][25]
2. Na lista de aplicações de Olá, selecione **SuccessFactors**.
   
    ![Configurar o início de sessão único][26]
3. No menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![Atribua o utilizador][27]
4. Na lista de utilizadores Olá, selecione **Britta Simon**.
5. Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.
   
    ![Atribua o utilizador][28]

### <a name="testing-single-sign-on"></a>Teste o início de sessão único
o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.

Ao clicar Olá SuccessFactors na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour SuccessFactors aplicação.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
