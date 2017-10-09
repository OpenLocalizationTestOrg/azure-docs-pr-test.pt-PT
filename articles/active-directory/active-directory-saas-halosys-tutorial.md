---
title: "Tutorial: Integração do Azure Active Directory com Halosys | Microsoft Docs"
description: "Saiba como toouse Halosys com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Tutorial: Integração do Azure Active Directory com Halosys

Neste tutorial, saiba como toointegrate Halosys com o Azure Active Directory (Azure AD).

Integrar Halosys com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooHalosys
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooHalosys (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal clássico do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Halosys tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Halosys início de sessão único subscrição ativado


> [!NOTE] 
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.


tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.

cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Halosys da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-


## <a name="adding-halosys-from-hello-gallery"></a>Adicionar Halosys da Galeria de Olá
tooconfigure Olá integração de Halosys com o Azure AD, é necessário tooadd Halosys Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Halosys da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.

    ![Active Directory][1]
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.

3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.

    ![Aplicações][2]

4. Clique em **adicionar** em Olá parte inferior da página Olá.

    ![Aplicações][3]

5. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.

    ![Aplicações][4]

6. Na caixa de pesquisa de Olá, escreva **Halosys**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. No painel de resultados de Olá, selecione **Halosys**e, em seguida, clique em **concluída** aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Halosys com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Halosys é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Halosys tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Halosys.

tooconfigure e teste do Azure AD-início de sessão único com Halosys, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Halosys](#creating-a-halosys-test-user)**  -toohave um homólogo de Britta Simon no Halosys é-lhe representação toohello ligado do Azure AD.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal clássico Olá e configurar o início de sessão único na sua aplicação Halosys.


**tooconfigure do Azure AD-início de sessão único com Halosys, execute Olá os seguintes passos:**

1. No portal clássico Olá, no Olá **Halosys** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar Single Sign-On** caixa de diálogo.
     
    ![Configurar o início de sessão único][6] 

2. No Olá **como seria, como os utilizadores toosign no tooHalosys** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.

    ![Configurar o início de sessão único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. No Olá **configurar definições de aplicação** diálogo página, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. No Olá **URL de início de sessão** caixa de texto, tipo Olá URL utilizado por utilizadores em toosign tooyour Halosys aplicação Olá seguir o padrão de utilização: `https://<company-name>.Halosys.com/client-api/api`.

    Olá b.In **URL de identificador** caixa de texto, tipo Olá URL no Olá seguir o padrão: `https://<company-name>.Halosys.com`. 
         
4. No Olá **configurar o início de sessão único em Halosys** página, clique em **transferir metadados**e, em seguida, guarde o ficheiro de Olá no seu computador:

    ![Configurar o início de sessão único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget SSO configurado para a sua aplicação, contacte a equipa de suporte de Halosys e forneça-los com o seguinte Olá:

    Olá • transferido **ficheiro de metadados**
    
    • Olá **SAML SSO URL**
    

6. No portal clássico Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**.
    
    ![Azure AD início de sessão único][10]

7. No Olá **único início de sessão confirmação** página, clique em **concluída**.  
 
    ![Azure AD início de sessão único][11]


### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
Nesta secção, vai criar um utilizador de teste no portal clássico Olá chamado Britta Simon.


![Criar utilizador do Azure AD][20]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.

3. lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. No Olá **diga-nos informações sobre este utilizador** diálogo página, execute os seguintes passos de Olá: ![criação de um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. Como tipo de utilizador, selecione o novo utilizador na sua organização.

    b. No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.

    c. Clique em **Seguinte**.

6.  No Olá **perfil de utilizador** diálogo página, execute os seguintes passos de Olá: ![criação de um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. No Olá **nome próprio** caixa de texto, tipo **Britta**.  

    b. No Olá **Apelido** caixa de texto, tipo, **Simon**.

    c. No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.

    d. No Olá **função** lista, selecione **utilizador**.

    e. Clique em **Seguinte**.

7. No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Anote o valor Olá Olá **nova palavra-passe**.

    b. Clique em **Concluído**.   



### <a name="creating-a-halosys-test-user"></a>Criar um utilizador de teste Halosys

Nesta secção, vai criar um utilizador chamado Britta Simon Halosys. . Funciona com Halosys suporte equipa tooadd Olá utilizadores numa plataforma de Halosys Olá.


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooHalosys de acesso.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooHalosys, execute Olá os seguintes passos:**

1. No portal clássico Olá, clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Halosys**.

    ![Configurar o início de sessão único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. No menu de Olá na parte superior do Olá, clique em **utilizadores**.

    ![Atribua o utilizador][203]

4. Na lista de utilizadores Olá, selecione **Britta Simon**.

5. Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.

    ![Atribua o utilizador][205]


### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá Halosys na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour Halosys aplicação.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
